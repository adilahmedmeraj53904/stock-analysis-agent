# Stock Analysis Agent

A **Telegram stock analysis agent** in **n8n** — send a ticker, get a 60-day chart photo + AI Verdict with Confidence.

## What it does

Send a message on Telegram like:

```
Analyse MSFT
```

In seconds you get back:

1. **A 60-day chart photo** — price line + 50-day average
2. **An AI analysis** — Trend, Key Levels, and a Verdict (Bullish / Neutral / Bearish) with Confidence

The verdict comes from an **AI Agent that reads the chart data**, not from a Code node calculating it.

## How it works

```
Telegram Trigger
        ↓
Get Price - Yahoo (free, no API key)
        ↓
Build Chart Data (Code — last 60 days, 50-day average)
        ↓
        ├→ Get Chart Image (QuickChart) → Send Photo (Telegram)
        ↓
        └→ AI Agent - Chart Analyst (reads chart data) → Send Report (Telegram)
```

The Chart Analyst reads the same chart data from `Build Chart Data` in its Prompt / User Message, using `$('Build Chart Data')` — so it works even after the photo is sent.

## Files

- `stock-analysis-agent-workflow.json` — import this file into n8n (export your working workflow from n8n with this name)

## How to import in n8n

1. In n8n, go to **Workflows → ... → Import from File**
2. Select `stock-analysis-agent-workflow.json`
3. Connect your own credentials: Telegram Bot, OpenRouter
4. Set the AI Agent model to a free OpenRouter model, for example `nvidia/nemotron-3-ultra-550b-a55b:free`
5. Test with `Analyse MSFT` on Telegram first, then Activate

## Built with

n8n • Yahoo Finance (free) • QuickChart (free) • Telegram • OpenRouter (free models) • JavaScript (Code nodes)

## Example

Tested on Telegram:

- **MSFT** — Price: $536.25, 60-day change: +11%
- **NVDA** — chart + AI analysis received on Telegram

Prices above are from the test on 2026-11-11, not live market prices.

## Status

> ✅ Tested working on Telegram. Educational analysis only — not financial advice, and never Buy / Sell advice.

## Author

**Adil Ahmed** — AI Automation Developer, Dhaka, Bangladesh
