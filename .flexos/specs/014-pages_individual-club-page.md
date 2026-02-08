---
id: page-individual-club
title: Individual Club Page Specification
description: The central hub for a specific book club, displaying its details, current book, discussion feeds, and management options.
type: spec
subtype: page
status: draft
sequence: 14
tags:
  - page
  - club
  - details
  - discussion
  - voting
relatesTo:
  - club-creation-management
  - book-voting-selection
  - reading-progress-tracker
  - private-club-discussion-feeds
  - book-ratings-reviews
  - my-clubs
  - book-details-page
  - users
  - book_clubs
  - club_members
  - club_votes
  - discussions
createdAt: 2026-02-08T00:29:02.596Z
updatedAt: 2026-02-08T00:29:02.596Z
---
## Individual Club Page (`/clubs/:id`)

The Individual Club Page is the primary interface for members to interact with a specific book club. It aggregates all relevant information and functionalities, including club details, the current book, discussion forums, and voting for future reads.

**Sections:**
*   **Club Header:** Club name, description, admin information, and membership count.
    *   **Management Options (Admin/Moderator):** Edit club details, manage members, send invites.
*   **Current Book Section:** Cover image, title, author, and a summary of the `currentBookId`.
    *   **Reading Progress Tracker:** User's personal progress and aggregate club progress for the current book.
    *   Link to `Book Details Page`.
*   **Discussion Feed:** A chronological feed of all discussions and comments within the club, with options to start new threads or reply to existing ones.
    *   Filters for discussions (e.g., "By Chapter", "General").
*   **Book Voting Section:** Displays nominated books, allows members to cast/change votes, and shows current vote tallies.
*   **Member List:** A list of all members in the club, with their roles.

<flex_block type="flow">
{
  "steps": [
    { "type": "action", "name": "User navigates to Individual Club Page", "actor": "user", "route": "/clubs/{clubId}" },
    { "type": "action", "name": "System fetches club details and related data", "actor": "system" },
    { "type": "action", "name": "System displays club information, discussions, and voting", "actor": "system" },
    { "type": "decision", "question": "User wants to interact?", "options": ["Yes → Participate in discussion", "Yes → Vote for a book", "Yes → Manage club (admin)", "No → Return to My Clubs"] }
  ]
}
</flex_block>

**Acceptance Criteria:**
1.  Displays accurate and up-to-date information for the club and its current book.
2.  The discussion feed is interactive, allowing users to post and reply.
3.  Book voting functionality works correctly, reflecting real-time tallies.
4.  Admin/moderator specific controls are only visible to authorized users.
5.  User's reading progress is correctly displayed and updatable.

**Edge Cases:**
*   **No Current Book:** The page should adapt gracefully if no `currentBookId` is set for the club.
*   **No Discussions:** Display a prompt to start the first discussion.
*   **Private Club Access:** Ensure only members can view private club pages.
*   **Empty Vote Pool:** Handle clubs with no books nominated for voting.

**Cross-references:**
*   **Features:** `book-voting-selection`, `reading-progress-tracker`, `private-club-discussion-feeds`, `club-creation-management`
*   **Collections:** `book_clubs`, `club_members`, `books`, `club_votes`, `discussions`
*   **Pages:** `my-clubs`, `book-details-page`, `create-edit-club`
