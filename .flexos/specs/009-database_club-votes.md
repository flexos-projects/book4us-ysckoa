---
id: database-club-votes
title: Club Votes Collection Database Specification
description: Detailed specification for the `club_votes` data collection, outlining its structure for recording member votes on potential books for their club.
type: spec
subtype: database
status: draft
sequence: 9
tags:
  - database
  - collection
  - club_votes
  - schema
relatesTo:
  - book-voting-selection
  - individual-club-page
  - book_clubs
  - books
  - users
createdAt: 2026-02-08T00:29:02.596Z
updatedAt: 2026-02-08T00:29:02.596Z
---
## Club Votes Collection (`club_votes`)

The `club_votes` collection records individual member votes for books nominated within a specific club. This allows clubs to collectively decide on their next read.

<flex_block type="schema">
{
  "collection": "club_votes",
  "fields": [
    { "name": "id", "type": "string", "required": true, "description": "Unique ID for the vote record." },
    { "name": "clubId", "type": "string", "required": true, "description": "ID of the book club for which the vote was cast." },
    { "name": "bookId", "type": "string", "required": true, "description": "ID of the book that received the vote." },
    { "name": "userId", "type": "string", "required": true, "description": "ID of the user who cast the vote." },
    { "name": "votedAt", "type": "date", "required": true, "description": "Timestamp when the vote was cast." }
  ]
}
</flex_block>

**Relationships:**
*   **Many-to-One (Club):** Many `club_votes` can be associated with one `book_club`.
*   **Many-to-One (Book):** Many `club_votes` can be for one `book`.
*   **Many-to-One (User):** Many `club_votes` can be cast by one `user`.

**Acceptance Criteria:**
1.  Every `club_vote` document must have a unique `id`.
2.  `clubId`, `bookId`, `userId`, and `votedAt` fields must always be present and correctly populated.
3.  A user should only be able to cast one vote per book within a specific club (uniqueness constraint on `clubId`, `bookId`, `userId`).

**Edge Cases:**
*   **Book/Club Deletion:** If a book or club related to a vote is deleted, the corresponding `club_vote` records should also be removed or marked for archival.
*   **Vote Changes:** The system should allow users to change their vote, updating the existing record rather than creating a new one.
*   **Invalid Book/Club/User IDs:** The system must validate that `bookId`, `clubId`, and `userId` refer to existing documents.
