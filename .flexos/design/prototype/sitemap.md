---
id: prototype-sitemap
title: "Prototype Sitemap"
description: "Route map for prototype pages"
type: design
subtype: sitemap
status: draft
sequence: 0
tags: [prototype, routing]
relatesTo: []
createdAt: "2026-02-08T00:29:02.596Z"
updatedAt: "2026-02-08T00:29:02.596Z"
---

# Prototype Sitemap

<flex_block type="config">
{
  "routes": {
    "/home": "landing-page-v1.html",
    "/auth": "auth-page-v1.html",
    "/dashboard": "dashboard-v1.html",
    "/clubs": "my-clubs-v1.html",
    "/clubs/:id": "individual-club-page-v1.html",
    "/books/:id": "book-details-page-v1.html",
    "/profile/:id": "user-profile-v1.html",
    "/settings": "settings-v1.html",
    "/clubs/new": "create-edit-club-v1.html"
  },
  "fallback": "404.html",
  "pages": [
    {
      "id": "landing-page",
      "route": "/home",
      "file": "landing-page-v1.html",
      "auth": true
    },
    {
      "id": "auth-page",
      "route": "/auth",
      "file": "auth-page-v1.html",
      "auth": true
    },
    {
      "id": "dashboard",
      "route": "/dashboard",
      "file": "dashboard-v1.html",
      "auth": true
    },
    {
      "id": "my-clubs",
      "route": "/clubs",
      "file": "my-clubs-v1.html",
      "auth": true
    },
    {
      "id": "individual-club-page",
      "route": "/clubs/:id",
      "file": "individual-club-page-v1.html",
      "auth": true
    },
    {
      "id": "book-details-page",
      "route": "/books/:id",
      "file": "book-details-page-v1.html",
      "auth": true
    },
    {
      "id": "user-profile",
      "route": "/profile/:id",
      "file": "user-profile-v1.html",
      "auth": true
    },
    {
      "id": "settings",
      "route": "/settings",
      "file": "settings-v1.html",
      "auth": true
    },
    {
      "id": "create-edit-club",
      "route": "/clubs/new",
      "file": "create-edit-club-v1.html",
      "auth": true
    }
  ]
}
</flex_block>

## Routes

| Route | File | Auth |
|-------|------|------|
| /home | landing-page-v1.html | Yes |
| /auth | auth-page-v1.html | Yes |
| /dashboard | dashboard-v1.html | Yes |
| /clubs | my-clubs-v1.html | Yes |
| /clubs/:id | individual-club-page-v1.html | Yes |
| /books/:id | book-details-page-v1.html | Yes |
| /profile/:id | user-profile-v1.html | Yes |
| /settings | settings-v1.html | Yes |
| /clubs/new | create-edit-club-v1.html | Yes |

---

*Prototype HTML files pending AI generation*
