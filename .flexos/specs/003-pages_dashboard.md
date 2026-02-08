---
id: page-dashboard
title: Dashboard Page Specification
description: Detailed specification for the personalized user dashboard, providing an overview of club activities and reading progress.
type: spec
subtype: page
status: draft
sequence: 3
tags:
  - page
  - dashboard
  - overview
  - user
relatesTo:
  - user-authentication-profiles
  - reading-progress-tracker
  - book-voting-selection
  - private-club-discussion-feeds
  - individual-club-page
  - my-clubs
  - users
  - book_clubs
  - club_members
  - discussions
createdAt: 2026-02-08T00:29:02.596Z
updatedAt: 2026-02-08T00:29:02.596Z
---
## Dashboard Page (`/dashboard`)

The Dashboard serves as the central personalized hub for logged-in users, offering a quick overview of their book club activities and reading progress. It's designed to provide immediate access to relevant information and encourage engagement with their clubs.

**Sections:**
*   **Current Reads widget:** Displays the book currently being read in each joined club, along with the user's individual progress and a club-wide progress summary.
*   **Upcoming Votes widget:** Highlights any active or upcoming book voting rounds across the user's clubs, with direct links to cast a vote.
*   **Recent Activity Feed:** Shows a chronological feed of new discussion posts, comments, and important club announcements from all joined clubs.
*   **My Clubs list:** A concise list of all clubs the user belongs to, with links to their respective `Individual Club Pages`.
*   **Quick Actions:** Buttons or links for common actions like "Create New Club" or "Update Reading Progress."

**Acceptance Criteria:**
1.  The dashboard loads quickly and displays accurate, up-to-date information for all sections.
2.  The "Current Reads" widget correctly shows individual and club-wide progress for the `currentBookId` in each club.
3.  The "Upcoming Votes" widget lists all active votes and allows direct navigation to the voting section of the `Individual Club Page`.
4.  The "Recent Activity Feed" aggregates new posts from all joined clubs, ordered by recency.
5.  Clicking on a club in "My Clubs" navigates to the corresponding `Individual Club Page`.
6.  Only authenticated users can access the dashboard.

**Edge Cases:**
*   **No Clubs Joined:** The dashboard should gracefully handle a user who has not joined any clubs, prompting them to create or join one.
*   **No Current Read:** If a club has no `currentBookId` set, the "Current Reads" widget should reflect this.
*   **Empty Activity Feed:** If there's no recent activity, a friendly message should be displayed.
*   **Loading States:** Appropriate loading indicators should be shown while data is being fetched.

**Cross-references:**
*   **Features:** `reading-progress-tracker`, `book-voting-selection`, `private-club-discussion-feeds`, `club-creation-management`
*   **Pages:** `individual-club-page`, `my-clubs`, `create-edit-club`
*   **Collections:** `users`, `book_clubs`, `club_members`, `discussions`
