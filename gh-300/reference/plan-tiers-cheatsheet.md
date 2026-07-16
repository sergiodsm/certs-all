# Plan Tiers Cheat Sheet (Memorize)

> Product packaging changes. Re-verify against [GitHub Copilot plans](https://docs.github.com/en/copilot/about-github-copilot/subscription-plans-for-github-copilot) the week before your exam. This matrix captures **exam-style distinctions** commonly tested.

## Tier map

| Capability | Free | Pro | Pro+ | Business | Enterprise |
|---|---|---|---|---|---|
| Inline completions | ✓ (limits) | ✓ | ✓ | ✓ | ✓ |
| Copilot Chat | ✓ (limits) | ✓ | ✓ | ✓ | ✓ |
| Agent / Edit / Plan modes | Limited / evolving | ✓ (policy/product) | ✓ | ✓ (org policy) | ✓ (org/enterprise policy) |
| Copilot CLI | Varies | ✓ | ✓ | ✓ | ✓ |
| **Content exclusions** | ✗ | ✗ | ✗ | ✓ | ✓ |
| **IP indemnity** (with public-code controls) | ✗ | ✗ | ✗ | ✓ | ✓ |
| **Org policy management** | ✗ | ✗ | ✗ | ✓ | ✓ |
| **Audit logs** (admin) | ✗ | ✗ | ✗ | ✓ | ✓ (often richer) |
| SAML SSO enforcement | ✗ | ✗ | ✗ | ✓ | ✓ |
| PR summaries / Knowledge Bases / fine-tuned models / Bing-grounded web (as offered) | ✗ / limited | limited | limited | limited | **Often Enterprise** |
| Seat management via admin/API | ✗ | ✗ | ✗ | ✓ | ✓ |

**Exam distractor rule:** the correct plan is frequently **one tier higher** than the tempting answer.

---

## Must-memorize gates

1. Need **content exclusions** → Business or Enterprise  
2. Need **IP indemnity** posture → Business or Enterprise + public-code **Blocked**  
3. Need org-wide feature lockdown + audit → Business/Enterprise  
4. Need advanced enterprise knowledge/customization features → often **Enterprise**  
5. Individual users cannot “just enable” org exclusion admin controls  

---

## Billing note (avoid the trap)

Packaging/billing models have shifted (e.g., premium request units vs AI credits). For exam prep:

- Know that **premium/agentic interactions may consume billable units/credits** beyond basic completions.  
- Prefer answers about **policy and capability**, not ephemeral price numbers.  
- Re-read current billing docs; do not memorize only a blog’s dollar figures.

---

## Quick drill

Without looking, answer:

1. Can Copilot Free configure org content exclusions?  
2. Which plans support IP indemnity-style protections?  
3. Where do audit logs for Copilot admin actions live?  
4. Is “public code matching: Blocked” an Individual-only setting story or Business+ governance story on the exam?

Answers: 1) No  2) Business/Enterprise  3) Org/Enterprise audit log  4) Business+ governance story for indemnity/org policy scenarios
