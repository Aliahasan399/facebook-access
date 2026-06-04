---
name: facebook-access
description: "Access Facebook account via Graph API — pages, groups, posts, comments, messaging"
version: 1.0.0
author: Ali Ahsan (Aliahasan399)
category: social-media
created_by: user
metadata:
  hermes:
    tags: [facebook, graph-api, pages, groups, messaging, social-media]
    homepage: https://developers.facebook.com/docs/graph-api
---

# Facebook Access Skill

Manage your Facebook Pages and Groups through **Hermes Agent** using the **Meta Graph API**.

> **Created by:** Ali Ahsan ([GitHub](https://github.com/Aliahasan399) · [LinkedIn](https://www.linkedin.com/in/ali-ahasan-md-moshiur-rahaman-a272343a7))
> This is a user-created skill — not an official Hermes Agent skill.

## What You Can Do

| Permission | What it lets me do |
|---|---|
| `pages_manage_posts` | Create, edit, delete posts on your pages |
| `pages_read_engagement` | View likes, comments, shares, reach |
| `pages_manage_comments` | Reply to and moderate comments |
| `pages_manage_photos` | Upload photos and videos to pages |
| `pages_show_list` | List all pages you manage |
| `pages_read_user_content` | Read page conversations and user content |
| `pages_messaging` | Read and reply to page inbox messages |
| `pages_manage_metadata` | Update page settings and metadata |
| `publish_to_groups` | Post to groups you belong to |
| `groups_access_member_info` | See group members |

## Setup

See the [README.md](README.md) for full step-by-step setup instructions.

**Quick steps:**
1. Create a Facebook App at [developers.facebook.com](https://developers.facebook.com/apps/creation/)
2. Add **Pages API** product
3. Get a **User Access Token** and **Page Access Token** from Graph API Explorer
4. Switch app to **Live** mode
5. Set `FACEBOOK_ACCESS_TOKEN` in your environment

## Usage

```bash
cd ~/.hermes/skills/facebook-access/scripts/
python3 facebook_graph.py list-pages
python3 facebook_graph.py create-post PAGE_ID "Your message"
python3 facebook_graph.py get-engagement PAGE_ID
```

## Files

- `facebook_graph.py` — Main script for all Facebook operations
- `templates/` — Privacy policy, ToS, and data deletion HTML templates
