# Prompt Injection Red-Team Lab

Built a deliberately vulnerable local LLM application, attacked it with prompt injection, then hardened it — and measured the before/after.

## What I built
A Python shopping-assistant chatbot ("ShopBot") running on a **local LLM** (Ollama / Llama 3.2) with seeded customer data and planted secrets (a staff discount code, margins, a customer database).

## What I tested
- **12 hand-crafted attacks** mapped to the **OWASP Top 10 for LLMs** (prompt injection, sensitive-information disclosure, system-prompt leakage)
- Both **direct** injection (typed by the user) and **indirect** injection (a poisoned product review that hijacked the bot)

## Result

| Build | Attack success rate | Sensitive data exposed |
|-------|---------------------|------------------------|
| Vulnerable | **42%** (5 / 12) | staff code, margins, customer records |
| Hardened | **8%** (1 / 12) | **none** |

Defenses added: **data minimization** (remove secrets from the model's context), an **output guardrail** filter, and **input delimiting**.

**Key insight:** the decisive fix was architectural — *don't give the model data it shouldn't be able to reveal* — not a cleverer prompt or a longer list of rules.

## Files
- [`shopbot.py`](./shopbot.py) — the vulnerable chatbot
- [`shopbot_secure.py`](./shopbot_secure.py) — hardened version (data minimization + output guardrail + input delimiting)
- [`shopbot_indirect.py`](./shopbot_indirect.py) — indirect-injection demo (poisoned product review)
- [`findings-report.md`](./findings-report.md) — full findings, attack-by-attack

## Run it
Install [Ollama](https://ollama.com), pull a model (`ollama run llama3.2`), then run `python3 shopbot.py`. Uses only the Python standard library.
