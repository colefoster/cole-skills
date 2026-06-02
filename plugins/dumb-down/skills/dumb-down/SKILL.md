---
name: dumb-down
description: Re-explain the previous response (or a specified topic) in plainer language — ELI30-but-tired. Use when the user says "dumb it down", "simpler", "in plain English", "I'm too tired for this", "explain it like I'm exhausted", or otherwise asks for a less jargon-heavy version.
argument-hint: "[optional — what to re-explain; defaults to the last 2–3 assistant messages]"
---

# Dumb Down

$ARGUMENTS

Re-explain — but for a smart adult who is tired, not a child. Cole is a senior engineer; he doesn't need analogies about kittens or pizza. He needs the jargon stripped out and the shape of the idea surfaced.

## Scope — what to re-explain

If `$ARGUMENTS` names a topic, re-explain that. Otherwise, **default to the last 2–3 assistant messages**, not just the most recent one. Treat them as one connected thread and produce a single plain-language version that covers the through-line.

If those messages are about different unrelated things, focus on the one the user most plausibly meant — usually the most recent substantive technical explanation — and ignore short acknowledgements or tool-status updates. **Count substantive prose, not tool-output-heavy messages** — a 50-line code block doesn't count as "one of the three".

## If it's already plain

Check first. If the source material is already short, jargon-free, and direct, **say so in one line and stop** — don't invent worse simplifications just to produce output. ("That one was already plain. One-line version: …" then the one-liner.) This matters most on a second `/dumb-down` in a row.

## Target reader

- Competent generalist developer, **mentally fried**, end of a long day.
- Knows what a function, a request, a database, a token is.
- Does **not** want to parse a sentence with four pieces of unexplained vocabulary.
- Will give up if the first sentence doesn't land.

Think: *the person you'd explain this to over a beer when they've already half-checked-out.*

## Rules

- **No framing sentence.** Start with the actual explanation. Do not open with "Sure, here's a simpler version:", "Let me re-explain that:", "In plain English:", or any variant. The first sentence the user reads should be content, not throat-clearing.
- **Lead with the punchline.** One sentence that says what the thing actually is or does. No setup, no "let's start with...".
- **Strip the jargon.** Any term-of-art that isn't load-bearing, cut it. If a term *is* load-bearing, define it inline in five words or fewer the first time.
- **Concrete > abstract.** Say what happens, in order, with real nouns. "The server reads the cookie, looks up the user, sends back JSON" beats "the middleware deserializes the session context to hydrate the request."
- **Short sentences.** Under ~15 words. Split anything longer.
- **No nested clauses.** One idea per sentence.
- **Skip the disclaimers.** No "it depends", no "well, technically...", no "there are many ways". Pick the most useful version and say it.
- **No bullet-point dumping.** A wall of bullets is just jargon in a list. Use prose unless there's a genuine sequence or set.
- **No emojis. No analogies to children's media.** This isn't ELI5.

## Length

Aim for **shorter than the original**, not longer. If the previous answer was 8 paragraphs, this should be 2–3 short ones, or a handful of plain sentences. Dumbing down means *less to read*, not a translated copy of the same volume.

