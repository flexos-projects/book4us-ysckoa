---
id: page-user-profile
title: User Profile Page Specification
description: A dedicated page for users to view and manage their personal profile information, settings, and activity.
type: spec
subtype: page
status: draft
sequence: 16
tags:
  - page
  - user
  - profile
  - settings
relatesTo:
  - user-authentication-profiles
  - goodreads-integration
  - users
  - club_members
createdAt: 2026-02-08T00:29:02.596Z
updatedAt: 2026-02-08T00:29:02.596Z
---
## User Profile Page (`/profile/:id`)

The User Profile Page allows users to view their own profile, update personal details, and see an overview of their activity within PageTurners. It can also be viewed by other users (with limited information) to foster community.

**Sections:**
*   **Profile Header:** User's `displayName`, `avatarUrl`, and basic status.
    *   **Edit Profile Button:** For the authenticated user to navigate to the `Settings Page` to update their profile.
*   **User Activity:** A summary of clubs joined, books read (if tracked globally), and recent discussion activity.
*   **Goodreads Integration Status:** Shows if a Goodreads account is linked and provides an option to link/unlink.
*   **About Me (Optional):** A configurable section where users can add a short bio or interests.

<flex_block type="flow">
{
  "steps": [
    { "type": "action", "name": "User navigates to User Profile Page", "actor": "user", "route": "/profile/{userId}" },
    { "type": "action", "name": "System fetches user data and activity summary", "actor": "system" },
    { "type": "action", "name": "System displays user profile", "actor": "system" },
    { "type": "decision", "question": "Authenticated user viewing their own profile?", "options": ["Yes → Edit profile", "No → View public profile"] }
  ]
}
</flex_block>

**Acceptance Criteria:**
1.  Displays accurate profile information (display name, avatar, etc.).
2.  Provides a clear path for authenticated users to edit their own profile.
3.  Summarizes user activity (e.g., clubs joined) correctly.
4.  Goodreads integration status is accurately shown.
5.  Privacy considerations for public profiles are handled (e.g., what information is visible to others).

**Edge Cases:**
*   **No Avatar/Display Name:** Display default placeholders.
*   **No Goodreads Linked:** Show the option to link Goodreads.
*   **Inactive User:** Handle profiles of users who have deleted their accounts or are inactive.

**Cross-references:**
*   **Features:** `user-authentication-profiles`, `goodreads-integration`
*   **Collections:** `users`, `club_members`
*   **Pages:** `settings`
