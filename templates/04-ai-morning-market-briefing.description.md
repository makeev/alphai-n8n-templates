# Submission description (n8n Creator Hub)

Title: **Send daily AI market briefings to email and Discord using AlphaAI and GPT**

---

Wake up to a personal market brief for your watchlist — written by your own AI model from enriched, pre-scored financial data instead of scraped headlines.

## Who's it for

Investors and traders who want a pre-open readout on their tickers without opening five tabs. Builders looking for a production pattern that combines an enriched news API with an LLM — where code, not the model, decides what counts as an alert.

## How it works

Every weekday at 07:00 the workflow calls four [AlphaAI](https://alphai.io) endpoints in parallel: last-day news per watchlist ticker (every article arrives with a 1–10 relevance score and per-ticker sentiment — no GPT-classification sub-flow needed), a 7-day sentiment tally, a 30-day SEC Form 4 insider summary, and market-wide trending stories. A Code node merges the branches and derives **red flags deterministically** (bearish high-relevance news or a notable insider filing in the last 24h) — the LLM only writes the narrative, so it cannot invent alerts. The brief lands in your inbox as clean HTML; red flags also ping a Discord channel immediately and flip the email subject to 🚩.

## How to set up

1. Free AlphaAI API key (Bearer Auth credential shared by the four AlphaAI nodes)
2. OpenAI credential on the model node — or swap it for any chat model
3. SMTP credential plus your from/to addresses
4. Optional Discord webhook for urgent alerts
5. Enter your tickers in *Watchlist & settings* and activate — about 5 minutes total

## Requirements

An AlphaAI account (the free tier covers up to 6 tickers per briefing), an OpenAI (or other LLM) key, and an SMTP mailbox.

## How to customize

Edit the prompt to change the brief's voice or structure, tune `min_relevance` / `urgent_min_score`, change the schedule, or replace delivery — everything downstream of *Render email & alerts* is plain n8n, so Slack, Telegram or Google Sheets archiving drop in naturally.
