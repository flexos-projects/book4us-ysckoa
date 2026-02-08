---
id: pages-sitemap
title: Pages, Site Map & User Journeys
description: An inventory of all pages in the application, the overall site structure, and key user journeys.
type: doc
subtype: core
status: draft
sequence: 3
tags:
  - ux
  - pages
  - sitemap
createdAt: 2026-02-08T00:29:02.596Z
updatedAt: 2026-02-08T00:29:02.596Z
---

## 1. Site Map

The following represents the hierarchical structure of the PageTurners application.

*   **Public Pages (Unauthenticated)**
    *   `/` - **Landing Page**: The main marketing page with feature highlights and a signup CTA.
    *   `/auth` - **Auth Page**: A single page containing forms for both Login and Signup.

*   **Authenticated Pages**
    *   `/dashboard` - **Dashboard**: The user's personalized home page after logging in.
    *   `/clubs` - **My Clubs**: A list of all clubs the user is a member of.
        *   `/clubs/new` - **Create Club Page**: Form to create a new book club.
        *   `/clubs/:id` - **Individual Club Page**: The main hub for a specific club. This is the most complex and feature-rich page.
        *   `/clubs/:id/edit` - **Edit Club Page**: Form for the admin to edit club details.
    *   `/books/:id` - **Book Details Page**: Shows detailed information about a single book, including reviews.
    *   `/profile/:id` - **User Profile Page**: Public profile view of a user's reading activity.
    *   `/settings` - **Settings Page**: For managing account details, notifications, and linked accounts.

## 2. Navigation

Once a user is logged in, a primary sidebar navigation will be present on all authenticated pages. It will provide consistent access to the main sections of the app:

*   **Dashboard** (`/dashboard`)
*   **My Clubs** (`/clubs`)
*   **My Profile** (`/profile/me`)
*   --- (Separator) ---
*   **Settings** (`/settings`)
*   **Logout**

## 3. Page Inventory & Key Components

*   **`/dashboard` (Dashboard)**
    *   **Purpose**: Provide a high-level overview of all user activity and prompt action.
    *   **Key Components**: 
        *   *Current Reads Widget*: Shows each club's current book and the user's progress.
        *   *Upcoming Votes Widget*: Lists any active voting rounds that require the user's attention.
        *   *Recent Activity Feed*: A consolidated feed of the latest discussion posts from all joined clubs.

*   **`/clubs/:id` (Individual Club Page)**
    *   **Purpose**: The central workspace for a book club.
    *   **Key Components**:
        *   *Club Header*: Displays the club name and description.
        *   *Current Book Card*: Highlights the current read, shows the user's progress tracker, and displays the club-wide average progress.
        *   *Voting Panel*: Shows the status of the current vote (or a button to start a new one for admins).
        *   *Discussion Feed*: The main component, with tabs or filters for 'General' and chapter-specific threads.
        *   *Member List*: A sidebar or modal showing all club members and their reading progress.

*   **`/books/:id` (Book Details Page)**
    *   **Purpose**: To act as a central repository of information for any given book.
    *   **Key Components**:
        *   *Book Metadata*: Cover image, title, author, synopsis (from Goodreads).
        *   *PageTurners Ratings*: Average rating and list of reviews from PageTurners users.
        *   *Goodreads Info*: Link to Goodreads page and their average rating.

## 4. Key User Journeys

These journeys illustrate how users will navigate through the pages to accomplish core tasks, referencing the flows from the [Flows Doc](.flexos/docs/core/005-flows.md).

*   **Journey: Joining a Club via Invite Code**
    1.  A logged-in user receives an invite code from a friend.
    2.  They navigate to `/clubs` (My Clubs).
    3.  They click a "Join a Club" button, which opens a modal.
    4.  They enter the code and submit.
    5.  Upon success, the system adds them to the club and redirects them to the `/clubs/:id` page for their new club.

*   **Journey: Participating in a Chapter Discussion**
    1.  A user logs in and lands on the `/dashboard`.
    2.  They see a recent post from their club in the *Recent Activity Feed* and click on it.
    3.  They are taken directly to the `/clubs/:id` page, with the discussion feed scrolled to the relevant post.
    4.  After reading, they decide to update their progress. They use the slider in the *Current Book Card* on the same page.
    5.  They then navigate to a different chapter's discussion thread using the filter options in the *Discussion Feed*.