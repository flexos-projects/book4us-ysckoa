---
id: page-my-clubs
title: My Clubs Page Specification
description: A dedicated page for authenticated users to view, manage, and discover book clubs they are associated with.
type: spec
subtype: page
status: draft
sequence: 13
tags:
  - page
  - clubs
  - user
  - management
relatesTo:
  - club-creation-management
  - private-club-discussion-feeds
  - individual-club-page
  - create-edit-club
  - dashboard
  - book_clubs
  - club_members
createdAt: 2026-02-08T00:29:02.596Z
updatedAt: 2026-02-08T00:29:02.596Z
---
## My Clubs Page (`/clubs`)

The My Clubs Page provides a comprehensive view of all book clubs the logged-in user is a member of or administers. It serves as a central hub for navigating to individual club details, creating new clubs, or searching for existing ones.

**Sections:**
*   **Club List:** A scrollable list or grid of book club cards, each displaying: club name, current book (if any), number of members, and a quick link to the `Individual Club Page`.
    *   Filter/Sort options (e.g., "My Administered Clubs", "Public Clubs", "Private Clubs", "Recently Active").
*   **Create New Club Button:** A prominent call-to-action to navigate to the `Create/Edit Club Page`.
*   **Search/Join Club:** A search bar and/or an option to join a private club using a `joinCode`.

<flex_block type="flow">
{
  "steps": [
    { "type": "action", "name": "User navigates to My Clubs Page", "actor": "user", "route": "/clubs" },
    { "type": "action", "name": "System fetches user's clubs", "actor": "system" },
    { "type": "action", "name": "System displays club list", "actor": "system" },
    { "type": "decision", "question": "User wants to interact with clubs?", "options": ["Yes → View individual club", "Yes → Create new club", "Yes → Join a club", "No → Return to Dashboard"] }
  ]
}
</flex_block>

**Acceptance Criteria:**
1.  All clubs the user is a member of are accurately displayed, with correct membership status and current book information.
2.  Filtering and sorting options work as expected.
3.  Clicking a club card navigates to the correct `Individual Club Page`.
4.  The "Create New Club" button correctly leads to the `Create/Edit Club Page`.
5.  The search/join functionality allows users to find and join clubs.

**Edge Cases:**
*   **No Clubs:** Display a friendly message and strong call-to-action to create or join a club.
*   **Loading States:** Show appropriate loading indicators while clubs are being fetched.
*   **Club Privacy:** Public clubs should be discoverable; private clubs should only be accessible via `joinCode` or direct invitation.

**Cross-references:**
*   **Features:** `club-creation-management`, `private-club-discussion-feeds`
*   **Collections:** `book_clubs`, `club_members`
*   **Pages:** `individual-club-page`, `create-edit-club`, `dashboard`
