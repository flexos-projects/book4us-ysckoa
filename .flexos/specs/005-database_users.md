---
id: database-users
title: Users Collection Database Specification
description: Detailed specification for the `users` data collection, outlining its structure, fields, and relationships.
type: spec
subtype: database
status: draft
sequence: 5
tags:
  - database
  - collection
  - users
  - schema
relatesTo:
  - user-authentication-profiles
  - club-creation-management
  - book-ratings-reviews
  - goodreads-integration
  - dashboard
  - user-profile
  - settings
  - club_members
  - reviews
  - discussions
createdAt: 2026-02-08T00:29:02.596Z
updatedAt: 2026-02-08T00:29:02.596Z
---
## Users Collection (`users`)

The `users` collection is the foundational data store for all user-specific information within PageTurners. Each document in this collection represents a unique user account, storing their authentication details, profile information, and preferences. It is central to almost every feature requiring user interaction.

**Fields:**
*   `id` (string, required): Unique Firebase Auth UID. Primary key for the user document.
*   `email` (email, required): User's primary email address, used for login and notifications.
*   `displayName` (string, optional): User's chosen public display name. Defaults to part of email if not provided.
*   `avatarUrl` (url, optional): URL to the user's profile picture.
*   `goodreadsId` (string, optional): External ID for linked Goodreads account.
*   `createdAt` (date, required): Timestamp when the user account was first created.
*   `lastLogin` (date, required): Timestamp of the user's most recent successful login.
*   `preferences` (object, optional): JSON object storing various user settings, e.g., `{"notifications": {"email": true, "inApp": true}}`.

**Relationships:**
*   **One-to-Many (Admin):** A user can be the `adminId` for multiple `book_clubs`.
*   **One-to-Many (Member):** A user can be linked to multiple `club_members` records, indicating their participation in various clubs.
*   **One-to-Many (Reviews):** A user can create many `reviews` for books.
*   **One-to-Many (Discussions):** A user can author many `discussions` posts.

**Acceptance Criteria:**
1.  Every user document must have a unique `id` corresponding to a Firebase Authentication UID.
2.  `email`, `createdAt`, and `lastLogin` fields must always be present and correctly populated upon user creation and login.
3.  Optional fields (`displayName`, `avatarUrl`, `goodreadsId`, `preferences`) should be correctly stored and retrieved when provided, and absent otherwise without causing errors.
4.  Data types for all fields must adhere to the specified schema.

**Edge Cases:**
*   **Missing Optional Data:** The application must gracefully handle scenarios where `displayName`, `avatarUrl`, or `goodreadsId` are not set.
*   **Goodreads Link Failure:** If Goodreads linking fails, `goodreadsId` should remain null, and the user should be notified.
*   **Data Integrity:** Ensure that `createdAt` and `lastLogin` are immutable or updated only by system processes.

**Cross-references:**
*   **Features:** `user-authentication-profiles`, `goodreads-integration`, `notifications-alerts`
*   **Pages:** `user-profile`, `settings`
*   **Collections:** `book_clubs`, `club_members`, `reviews`, `discussions`
