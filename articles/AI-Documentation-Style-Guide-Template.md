
# 🧭 Documentation Style Guide for AI Readability  
**Version:** 1.0  
**Owner:** [Your Name / Team]  
**Last Updated:** [YYYY-MM-DD]  

---

## 1. Purpose

This guide defines writing and formatting standards that make documentation **easy for AI systems to parse, retrieve, and reason over**, while remaining **clear and useful for humans**.  
AI agents consume text by extracting semantic meaning from sections (“chunks”), not full documents — this guide ensures each chunk is independently meaningful and context-rich.  

---

## 2. Core Principles

| Principle | Description |
|------------|--------------|
| **Atomicity** | Each section should express one complete idea or procedure. |
| **Clarity** | Prefer explicit, declarative sentences over conversational or figurative language. |
| **Consistency** | Use uniform terminology and heading conventions throughout. |
| **Retrievability** | Write so AI search systems can easily match user questions to document answers. |
| **Context Completeness** | Each section must stand alone — never rely on “as mentioned above” or “below.” |

---

## 3. Document Structure

### 3.1 Front Matter Metadata
Provide structured metadata at the top of each document if your system supports it.

```yaml
title: "API Authentication"
category: "Security"
last_updated: "2025-10-11"
version: "v2.0"
related_topics: ["OAuth", "Access Tokens", "Bearer Authentication"]
tags: ["authentication", "api", "security"]
```

### 3.2 Hierarchical Headings
Use clear, semantic hierarchy:
```
# Title  
## Section  
### Subsection  
#### Subtopic
```
Headings should describe **exactly** what’s inside (avoid wordplay or abbreviations).

✅ **Good:** `## Error Handling in API v2`  
❌ **Bad:** `## Oops and Edge Cases`

---

## 4. Language and Tone

| Guideline | Example |
|------------|----------|
| Use declarative sentences | “Include an API key in every request.” |
| Avoid vague pronouns | Replace “it” with the specific noun. |
| Prefer active voice | “The system stores logs” → not “Logs are stored by the system.” |
| Define terms on first use | “A webhook is an HTTP callback triggered by an event.” |
| Use consistent terminology | “access token” throughout, not “API key,” “credential,” “auth token.” |

---

## 5. Content Design for AI Consumption

### 5.1 Chunk Independence
Each section should be understandable on its own. Avoid phrases like:
- “As shown above”  
- “In the next section”  
- “Previously discussed”

Instead, restate briefly for context:
> “As described in the Authentication section, each API request requires a bearer token.”

### 5.2 Natural-Language Alignment
Include **natural question phrasing** that mirrors what users might ask:
> “How do I authenticate with the API?”  
> “Where can I find my API key?”  
> “What causes a 401 error?”

You can add an “FAQ” or “Common Questions” subsection per topic.

### 5.3 Repetition for Clarity
Use key terms multiple times naturally — it improves retrieval accuracy.  
Example: if the page is about “webhooks,” ensure “webhook” appears throughout, not just once.

---

## 6. Code and Data Blocks

### 6.1 Format
Use fenced code blocks with syntax highlighting:
```python
response = requests.get(url, headers={"Authorization": "Bearer <token>"})
```

### 6.2 Explanation
Follow each code block with a short description:
> This example shows how to authenticate a request using a bearer token in Python.

### 6.3 Sample Inputs/Outputs
Where applicable, show both:
```bash
curl -X GET https://api.example.com/v1/users
```
```json
{
  "id": "123",
  "name": "Jane Doe"
}
```

---

## 7. Linking and References

- Use **descriptive anchor text**:  
  ✅ `[Learn about Rate Limits](#rate-limits)`  
  ❌ `[Click here](#rate-limits)`

- Use “See also” sections to connect related topics:  
  > See also: [Error Codes](#error-codes), [Troubleshooting](#troubleshooting)

---

## 8. Versioning and Deprecation

- Mark version applicability clearly:  
  > Applies to API v3.1 and later.  
  > Deprecated as of v2.5 — use `GET /users/profile` instead.

- Avoid assuming the reader or AI knows which version applies.

---

## 9. Summaries and Key Takeaways

Add summaries at the end of each major section.

### Example:
**Summary:**  
Authentication uses OAuth 2.0 bearer tokens. Tokens expire after 60 minutes and can be refreshed using `/refresh`.

**Key Points:**
| Concept | Description |
|----------|-------------|
| Token Type | Bearer |
| Expiration | 60 minutes |
| Refresh | `/refresh` endpoint |

---

## 10. Glossary (Optional)
Include a glossary of domain-specific terms with consistent definitions.

| Term | Definition |
|------|-------------|
| **Webhook** | A user-defined callback triggered by an event. |
| **Bearer Token** | A security token used for API authentication. |

---

## 11. Quality Checklist

✅ Does every section stand alone?  
✅ Are headings descriptive and consistent?  
✅ Are important terms used consistently?  
✅ Does the document answer natural-language questions?  
✅ Are examples accompanied by explanations?  
✅ Are deprecated or versioned items clearly labeled?  
✅ Is there a summary or key takeaway section?  

---
