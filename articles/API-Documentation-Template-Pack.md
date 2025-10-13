
# 🧭 API Documentation Template Pack for AI Readability
**Version:** 1.0  
**Owner:** [Your Name / Team]  
**Last Updated:** [YYYY-MM-DD]  

---

## 📘 Template 1: API Guide (Conceptual & Use-Case Focused)

```markdown
# [Guide Title: e.g., Authenticating with the Example API]

**Purpose:**  
Explain *why* and *how* a developer should complete a specific task or use case with your API.  
Each guide should map closely to one or more related endpoints.

---

## 1. Overview
Provide a short, high-level summary of what the guide covers.  

**Example:**  
This guide shows how to authenticate with the Example API using OAuth 2.0. You’ll learn how to obtain an access token and use it to authorize subsequent requests.

---

## 2. Prerequisites
List what developers need before following the guide (API keys, permissions, setup).

**Example:**
- An active developer account
- A registered OAuth client ID and secret
- Access to the Example API base URL (`https://api.example.com/v1/`)

---

## 3. Step-by-Step Instructions

### Step 1: Obtain an Access Token
Explain the process clearly and reference relevant endpoints.

Example request:
```bash
curl -X POST https://api.example.com/v1/auth/token \
  -H "Content-Type: application/json" \
  -d '{"client_id": "abc123", "client_secret": "xyz789"}'
```

Expected response:
```json
{
  "access_token": "abcd1234token",
  "expires_in": 3600,
  "token_type": "Bearer"
}
```

**Explanation:**  
This endpoint issues a temporary bearer token valid for 1 hour. Use this token in the `Authorization` header for all subsequent requests.

---

### Step 2: Use the Token in API Calls
Show how the previous output connects to the next step.

Example:
```bash
curl -X GET https://api.example.com/v1/users/me \
  -H "Authorization: Bearer abcd1234token"
```

---

## 4. Common Errors

| Code | Message | Cause | Resolution |
|------|----------|--------|-------------|
| 400 | Invalid client ID | The client_id is not recognized | Verify credentials |
| 401 | Unauthorized | Missing or expired token | Obtain a new token |
| 500 | Server Error | Internal issue | Retry later |

---

## 5. Summary

**In summary:**  
This guide explained how to authenticate using the Example API’s OAuth 2.0 flow. You now know how to generate and use access tokens in authorized requests.

**See also:**  
- [Reference: POST /auth/token](#post-authtoken)  
- [Guide: Refreshing Access Tokens](#refreshing-access-tokens)
```

---

## 📗 Template 2: API Reference (Endpoint-by-Endpoint)

```markdown
# API Reference: [Service or Resource Name]
**Base URL:** `https://api.example.com/v1`  
**Version:** v1.0  

---

## POST /users

**Purpose:**  
Creates a new user in the system.

**Description:**  
Registers a new user with an email, password, and optional profile metadata.

**Parameters:**
| Name | Type | Required | Description |
|------|------|-----------|--------------|
| `email` | string | ✅ | User’s email address. Must be unique. |
| `password` | string | ✅ | Minimum 8 characters with a number. |
| `profile` | object | ❌ | Optional user profile metadata. |

**Request Example:**
```bash
curl -X POST https://api.example.com/v1/users \
  -H "Content-Type: application/json" \
  -d '{"email": "user@example.com", "password": "Example123"}'
```

**Response Example:**
```json
{
  "id": "u_12345",
  "email": "user@example.com",
  "created_at": "2025-10-11T08:42:00Z"
}
```

**Errors:**
| Code | Message | Explanation |
|------|----------|--------------|
| 400 | Invalid Email | Email format is invalid. |
| 409 | Duplicate Email | Email already registered. |

**See also:**  
[GET /users/{id}](#get-users-id), [PATCH /users/{id}](#patch-users-id)

---

## GET /users/{id}

**Purpose:**  
Retrieve a user by their unique ID.

**Description:**  
Returns user information such as ID, email, and timestamps. Requires a valid access token.

**Path Parameters:**
| Name | Type | Required | Description |
|------|------|-----------|--------------|
| `id` | string | ✅ | The unique user ID. |

**Request Example:**
```bash
curl -X GET https://api.example.com/v1/users/u_12345 \
  -H "Authorization: Bearer abcd1234token"
```

**Response Example:**
```json
{
  "id": "u_12345",
  "email": "user@example.com",
  "created_at": "2025-10-11T08:42:00Z"
}
```

**Errors:**
| Code | Message | Explanation |
|------|----------|--------------|
| 401 | Unauthorized | Missing or invalid token. |
| 404 | Not Found | No user exists with that ID. |

---

**Summary:**  
The `/users` endpoints provide user management functionality, including creation, retrieval, and updates.

**Common Questions:**
- How do I create a new user?
- What errors can occur during user creation?
- How can I retrieve a specific user by ID?
```

---

## 🧩 Notes for Writers

When using these templates:
1. **Align terminology** between the Guides, Reference docs, and the OpenAPI spec.
2. Use **natural language in descriptions** — e.g., “Creates a new user record” instead of “Adds user.”
3. Add **end-to-end flow examples** in Guides; **detailed parameter-level clarity** in Reference.
4. Include **FAQs and “See also” sections** wherever relevant.
5. Keep **examples realistic** — domain-specific names, real timestamps, and expected values.
6. Add **front matter metadata** when supported (title, version, tags, last_updated).

---

## ✅ Deliverables in This Pack

- **Template 1:** `API_Guide_Template.md` — for conceptual, task-based writing.  
- **Template 2:** `API_Reference_Template.md` — for endpoint-level documentation.  
- **Usage Notes:** Best practices and authoring guidance for AI-readable documentation.

---
