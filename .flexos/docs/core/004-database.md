---
id: database-schema
title: Database Schema & Security Rules
description: Detailed documentation of the Firestore collections, data schemas, relationships, and security rules that govern the application's data layer.
type: doc
subtype: core
status: draft
sequence: 4
tags:
  - database
  - firestore
  - technical
createdAt: 2026-02-08T00:29:02.596Z
updatedAt: 2026-02-08T00:29:02.596Z
---

## 1. Database Choice

We will use **Firebase Firestore** as our primary database. Its NoSQL, document-oriented structure is well-suited for our application's data model, and its real-time capabilities are perfect for features like discussion feeds and live progress tracking. Its integration with Firebase Authentication allows for robust, rule-based security.

## 2. Collection Schemas

Below are the definitions for our primary Firestore collections.

*   **`users`**
    *   **Description**: Stores public user profile information. The document ID will be the user's Firebase Auth UID.
    *   **Fields**:
        *   `displayName` (string)
        *   `avatarUrl` (string, URL)
        *   `goodreadsId` (string, nullable)
        *   `createdAt` (timestamp)

*   **`book_clubs`**
    *   **Description**: Contains all information about a single book club.
    *   **Fields**:
        *   `name` (string)
        *   `description` (string)
        *   `adminId` (string, references `users.id`)
        *   `currentBookId` (string, references `books.id`, nullable)
        *   `inviteCode` (string, unique)
        *   `createdAt` (timestamp)
        *   `vote` (map, nullable): Contains info about an active vote, e.g., `{ votingRoundId: '...', endDate: '...', options: [{bookId: '...', votes: 0}] }`

*   **`books`**
    *   **Description**: A centralized collection of book data, sourced from Goodreads to prevent duplication. The document ID should be the Goodreads book ID.
    *   **Fields**:
        *   `title` (string)
        *   `author` (string)
        *   `coverImageUrl` (string, URL)
        *   `synopsis` (string)
        *   `pageCount` (number)
        *   `goodreadsRating` (number)
        *   `genres` (array of strings)

*   **`club_members`**
    *   **Description**: A mapping collection that links users to clubs. The document ID should be a composite key like `${clubId}_${userId}` for efficient lookups and to enforce unique membership.
    *   **Fields**:
        *   `clubId` (string, references `book_clubs.id`)
        *   `userId` (string, references `users.id`)
        *   `role` (string, enum: 'admin', 'member')
        *   `joinedAt` (timestamp)
        *   `progress` (map, nullable): `{ bookId: '...', currentPage: 120 }`

*   **`discussions`**
    *   **Description**: Stores discussion posts and comments for clubs.
    *   **Fields**:
        *   `clubId` (string, references `book_clubs.id`)
        *   `userId` (string, references `users.id`)
        *   `bookId` (string, references `books.id`, nullable)
        *   `type` (string, enum: 'general', 'chapter')
        *   `chapterNumber` (number, nullable)
        *   `content` (string)
        *   `parentId` (string, references `discussions.id`, nullable for threaded replies)
        *   `createdAt` (timestamp)

## 3. Data Relationships

*   **Many-to-Many (Users & Clubs)**: This is managed through the `club_members` collection. To find all clubs for a user, we query `club_members` where `userId` matches. To find all members of a club, we query where `clubId` matches.
*   **One-to-Many (Club & Discussions)**: Each document in the `discussions` collection contains a `clubId` field, creating a direct link back to its parent club.

## 4. Firestore Security Rules (Conceptual)

Security is paramount. Our rules will enforce the following logic:

```javascript
// Pseudocode for Firestore Rules
match /databases/{database}/documents {

  // Users can only update their own profile.
  match /users/{userId} {
    allow read: if request.auth != null;
    allow write: if request.auth.uid == userId;
  }

  // Function to check for club membership.
  function isClubMember(clubId) {
    return exists(/databases/$(database)/documents/club_members/$(clubId + '_' + request.auth.uid));
  }

  // Only members can read club data. Only admin can write.
  match /book_clubs/{clubId} {
    allow read: if isClubMember(clubId);
    allow create: if request.auth != null;
    allow update: if isClubMember(clubId) && get(/databases/$(database)/documents/book_clubs/$(clubId)).data.adminId == request.auth.uid;
  }

  // Members can read/write discussions in their own clubs.
  match /discussions/{discussionId} {
    allow read, write: if isClubMember(request.resource.data.clubId);
  }

  // Users can only update their own membership status/progress.
  match /club_members/{membershipId} {
    allow read: if isClubMember(resource.data.clubId);
    allow create: if request.auth != null; // Additional logic for invite codes needed here
    allow update: if request.auth.uid == resource.data.userId;
    allow delete: if request.auth.uid == resource.data.userId || get(/databases/$(database)/documents/book_clubs/$(resource.data.clubId)).data.adminId == request.auth.uid;
  }
}
```