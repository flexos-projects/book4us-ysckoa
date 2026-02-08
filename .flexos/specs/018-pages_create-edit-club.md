---
id: page-create-edit-club
title: Create/Edit Club Page Specification
description: A dynamic page for users to create new book clubs or modify the details of existing clubs they administer.
type: spec
subtype: page
status: draft
sequence: 18
tags:
  - page
  - club
  - management
  - creation
  - form
relatesTo:
  - club-creation-management
  - book_clubs
  - my-clubs
  - individual-club-page
createdAt: 2026-02-08T00:29:02.596Z
updatedAt: 2026-02-08T00:29:02.596Z
---
## Create/Edit Club Page (`/clubs/new` or `/clubs/:id/edit`)

This page serves a dual purpose: enabling users to create entirely new book clubs and allowing club administrators to modify the details of their existing clubs. The form dynamically adapts based on whether a new club is being created or an existing one is being edited.

**Sections/Form Fields:**
*   **Club Name:** Required text input.
*   **Club Description:** Optional multiline text input.
*   **Privacy Setting:** Radio buttons/toggle for "Public" or "Private".
    *   If "Private" is selected, a `joinCode` field might be displayed or automatically generated.
*   **Current Book (Optional):** Searchable input to select an initial book for the club.
*   **Submit/Save Button:** To finalize creation or updates.
*   **Cancel Button:** To discard changes and return to the previous page.

<flex_block type="flow">
{
  "steps": [
    { "type": "action", "name": "User navigates to Create/Edit Club Page", "actor": "user", "route": "/clubs/new" },
    { "type": "decision", "question": "Creating or Editing?", "options": ["Creating → Fill empty form", "Editing → Load existing club data"] },
    { "type": "action", "name": "User fills/modifies form fields", "actor": "user" },
    { "type": "action", "name": "User submits form", "actor": "user" },
    { "type": "action", "name": "System processes club data", "actor": "system" },
    { "type": "decision", "question": "Submission successful?", "options": ["Yes → Redirect to Individual Club Page", "No → Show error message"] }
  ]
}
</flex_block>

**Acceptance Criteria:**
1.  Users can successfully create new public or private book clubs with a name and optional description.
2.  Club administrators can update all editable details of their clubs.
3.  `joinCode` is correctly generated and displayed for private clubs.
4.  Form validations prevent submission of invalid or incomplete data.
5.  After successful creation or update, the user is redirected to the `Individual Club Page`.

**Edge Cases:**
*   **Duplicate Club Name:** Inform the user if a club name is already taken.
*   **Invalid Join Code:** If a `joinCode` is manually entered (e.g., for editing), validate its format.
*   **Permissions:** Only club administrators should be able to access the edit functionality for a club.
*   **Error Handling:** Display clear error messages for any issues during submission.

**Cross-references:**
*   **Features:** `club-creation-management`
*   **Collections:** `book_clubs`
*   **Pages:** `my-clubs`, `individual-club-page`
