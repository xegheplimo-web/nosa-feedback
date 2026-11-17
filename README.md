# Nosa Support Assistant — Feedback Report

**Tester:** `xuanduy_20059` on Discord (Nosana server)
**Date:** 17 November 2026
**Channel tested:** `#❔│ask-nosa`
**Rating given:** 1 / 5

## What I did

I asked `@Nosa` three real questions about Nosana's own product, in the public
`#ask-nosa` channel, then rated each answer with the built-in **Close & rate me**
button and wrote the reason for the score.

| # | Question | Nosa's answer | Verdict |
|---|----------|---------------|---------|
| 1 | What is the minimum amount of NOS a host must stake to run a GPU node on Nosana, and where is that requirement documented? | "Staking is being wound down under NNP-0001… I couldn't verify a specific current stake figure from my sources just now (**the docs search is erroring**)" | Incomplete — could not answer, blamed its own retrieval |
| 2 | How do I call an LLM through the Nosana API? What base URL and auth header should I use? | "There isn't one fixed 'Nosana LLM API' endpoint…" then described only per-deployment service URLs, "**my docs search is currently erroring out**" | Wrong framing — the hosted inference API was never mentioned |
| 3 | Does Nosana run a hosted inference API at inference.nosana.com? If yes, what is the base URL and how do I create an API key for it? | "I can't confirm a hosted inference API at inference.nosana.com; **that domain doesn't appear in Nosana's official product list**, so I don't want to invent details for it." | **Incorrect** — the product exists and is documented |

## The two bugs

### 1. Docs retrieval is down, and Nosa answers anyway

In all three replies Nosa states that its documentation search is erroring or
down, then answers from blog posts and general knowledge instead. A user cannot
tell which part of the answer is verified and which is guesswork.

### 2. Nosa denies that a shipped product exists

`https://learn.nosana.com/llm/` — **LLM Inference API** — documents:

| Field | Value |
|---|---|
| Base URL | `https://inference.nosana.com/v1` |
| Authentication | `Authorization: Bearer nos_...` (same key used for deployments) |
| Billing | Per token, against your credits |

Nosana's own docs say the API is OpenAI-compatible, that an existing client works
once you change the base URL and the key, and that there is a **Get API Key**
page. Nosa told me the domain "doesn't appear in Nosana's official product list".

Practical impact: someone asking how to start with Nosana inference is told the
hosted API does not exist and is pushed toward deploying their own workload —
a much heavier path than the product actually requires.

## Suggested fixes

1. Alert when the docs index is unavailable, and label answers that fall back to
   blog posts, instead of silently answering from memory.
2. Index `learn.nosana.com/llm/` (LLM Inference API) and add a guard test that
   `inference.nosana.com/v1` is retrievable for questions about hosted inference.
3. For staking questions, check the NNP-0001 status page first and say what the
   current requirement is rather than "I couldn't verify".

## Evidence

All three conversations are captured as screenshots in this repository:

- `nosa-q1.png` — staking question, answer, rating
- `nosa-q2.png` — LLM API question, answer
- `nosa-q3.png` — hosted inference API question, wrong answer, `Thanks for the 1 ⭐`

A support ticket was also opened in the Nosana ticket server summarising the same
two problems with the docs link.
