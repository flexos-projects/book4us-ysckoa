---
id: database-book-clubs
title: Book Clubs Collection Database Specification
description: Detailed specification for the `book_clubs` data collection, outlining its structure, fields, and relationships.
type: spec
subtype: database
status: draft
sequence: 6
tags:
  - database
  - collection
  - book_clubs
  - schema
relatesTo:
  - club-creation-management
  - book-voting-selection
  - private-club-discussion-feeds
  - dashboard
  - my-clubs
  - individual-club-page
  - create-edit-club
  - club_members
  - club_votes
  - discussions
createdAt: 2026-02-08T00:29:02.596Z
updatedAt: 2026-02-08T00:29:02.596Z
---
## Book Clubs Collection (`book_clubs`)

The `book_clubs` collection stores information about each book club created within PageTurners. Each document represents a unique club, including its basic details, the current book being read, and administrative information.

<flex_block type="schema">
{
  "collection": "book_clubs",
  "fields": [
    { "name": "id", "type": "string", "required": true, "description": "Unique ID for the book club." },
    { "name": "name", "type": "string", "required": true, "description": "Name of the book club." },
    { "name": "description", "type": "string", "optional": true, "description": "A brief description of the club." },
    { "name": "adminId", "type": "string", "required": true, "description": "ID of the user who created and administers the club." },
    { "name": "currentBookId", "type": "string", "optional": true, "description": "ID of the book currently being read by the club." },
    { "name": "isPrivate", "type": "boolean", "required": true, "description": "Indicates if the club is private (invite-only) or public." },
    { "name": "joinCode", "type": "string", "optional": true, "description": "Code for private clubs to share for joining." },
    { "name": "createdAt", "type": "date", "required": true, "description": "Timestamp when the club was created." }
  ]
}
</flex_block>

**Relationships:**
*   **One-to-One (Current Book):** Each club can have one `currentBookId` linking to a `books` document.
*   **One-to-Many (Admin):** One user (`adminId`) can administer multiple `book_clubs`.
*   **One-to-Many (Members):** Each club can have many `club_members`.
*   **One-to-Many (Votes):** Each club can have many `club_votes` for upcoming books.
*   **One-to-Many (Discussions):** Each club can host many `discussions`.

**Acceptance Criteria:**
1.  Every `book_club` document must have a unique `id`.
2.  `name`, `adminId`, `isPrivate`, and `createdAt` fields must always be present and correctly populated.
3.  If `isPrivate` is true, `joinCode` should be generated and present. If `isPrivate` is false, `joinCode` should be null.
4.  `currentBookId` should accurately link to an existing `book` document when set.

**Edge Cases:**
*   **Admin Deletion:** If an `adminId` user is deleted, the club should either be transferred to another member or marked as inactive/deleted.
*   **Private Club Management:** Ensure `joinCode` uniqueness and proper validation during club joining.
*   **Book Not Set:** The application must handle clubs without a `currentBookId` gracefully.
