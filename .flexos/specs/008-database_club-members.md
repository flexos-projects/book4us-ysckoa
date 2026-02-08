---
id: database-club-members
title: Club Members Collection Database Specification
description: Detailed specification for the `club_members` data collection, outlining its structure, fields, and relationships between users and book clubs.
type: spec
subtype: database
status: draft
sequence: 8
tags:
  - database
  - collection
  - club_members
  - schema
relatesTo:
  - club-creation-management
  - user-authentication-profiles
  - my-clubs
  - individual-club-page
  - users
  - book_clubs
  - reading-progress-tracker
  - private-club-discussion-feeds
createdAt: 2026-02-08T00:29:02.596Z
updatedAt: 2026-02-08T00:29:02.596Z
---
## Club Members Collection (`club_members`)

The `club_members` collection serves as a join table, linking users to the book clubs they are a part of. It also stores member-specific information within each club, such as their role and joining date.

<flex_block type="schema">
{
  "collection": "club_members",
  "fields": [
    { "name": "id", "type": "string", "required": true, "description": "Unique ID for the club membership record." },
    { "name": "clubId", "type": "string", "required": true, "description": "ID of the book club this member belongs to." },
    { "name": "userId", "type": "string", "required": true, "description": "ID of the user who is a member of this club." },
    { "name": "role", "type": "string", "required": true, "description": "The member's role within the club (e.g., 'member', 'admin', 'moderator')." },
    { "name": "joinedAt", "type": "date", "required": true, "description": "Timestamp when the user joined this club." },
    { "name": "isApproved", "type": "boolean", "required": true, "description": "For private clubs, indicates if the member's request to join has been approved." }
  ]
}
</flex_block>

**Relationships:**
*   **Many-to-One (Club):** Many `club_members` can belong to one `book_club`.
*   **Many-to-One (User):** Many `club_members` records can point to one `user`.
*   **One-to-One (Reading Progress):** Each `club_member` might have a related `reading_progress` record for the current book.

**Acceptance Criteria:**
1.  Every `club_member` document must have a unique `id`.
2.  `clubId`, `userId`, `role`, `joinedAt`, and `isApproved` fields must always be present and correctly populated.
3.  The combination of `clubId` and `userId` should be unique to prevent a user from joining the same club multiple times.
4.  `role` should be restricted to predefined values (e.g., 'member', 'admin', 'moderator').

**Edge Cases:**
*   **User Leaves Club:** When a user leaves, their `club_member` record should be removed or marked as inactive.
*   **Club Deletion:** When a club is deleted, all associated `club_member` records must also be removed.
*   **Role Changes:** The system must support changing a member's role and ensure permissions are updated accordingly.
