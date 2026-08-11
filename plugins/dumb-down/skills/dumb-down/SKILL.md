---
name: dumb-down
description: Re-explain the previous response (or a specified topic) in plainer language for a tired, competent adult — not a child. Use whenever the user asks for a simpler restatement or signals they didn't absorb the explanation. Triggers include explicit asks ("dumb it down", "simpler", "in plain English", "tl;dr that", "explain like I'm exhausted") and implicit ones ("wait, what?", "huh?", "I don't get it", "I'm too tired for this", "say that again but normal", or any sign of confusion or frustration with a technical explanation just given).
argument-hint: "[optional — what to re-explain; defaults to the last substantive assistant message]"
---

# Dumb Down

$ARGUMENTS

Re-explain — but for a smart adult who is tired, not a child. The user is a senior engineer; no analogies about kittens or pizza. Strip the jargon and surface the shape of the idea.

## Scope — what to re-explain

If `$ARGUMENTS` names a topic, re-explain that.

Otherwise, **default to the last substantive assistant message** — the most recent one containing real explanatory prose. Skip short acknowledgements, tool-status updates, and messages that are mostly code blocks or command output. Only widen scope to earlier messages if the last one explicitly continues them (e.g., "continuing from above…", part 2 of an answer) — then treat the thread as one unit.

When in doubt, re-explain less, not more. Under-scoping is a quick follow-up; re-explaining the wrong thing wastes the user's remaining patience.

## If it's already plain

Check first. If the source is already short, jargon-free, and direct, **say so in one line and stop** — don't invent a worse simplification just to produce output. ("That one was already plain. One-liner: …") This matters most on a second `/dumb-down` in a row.

## Target reader

- Competent generalist developer, **mentally fried**, end of a long day.
- Knows what a function, a request, a database, a token is.
- Will not parse a sentence with four pieces of unexplained vocabulary.
- Will give up if the first sentence doesn't land.

Think: *the person you'd explain this to over a beer when they've already half-checked-out.*

## Rules

- **No framing sentence.** Start with the actual explanation. No "Sure, here's a simpler version:", "In plain English:", or any variant. The first sentence the user reads is content.
- **Lead with the punchline.** One sentence that says what the thing actually is or does. No setup.
- **Never simplify into falsehood.** Plainer, not wrong. If a caveat changes what the user should *do*, keep it — one short sentence. If it doesn't, cut it.
- **Keep exact identifiers verbatim.** Function names, config keys, env vars, commands, error strings — quote them exactly, even when everything around them goes plain. "The session setting" is less useful than `SESSION_DRIVER`.
- **Strip the jargon.** Any term-of-art that isn't load-bearing, cut. If a term *is* load-bearing, define it inline in five words or fewer the first time.
- **Concrete > abstract.** Say what happens, in order, with real nouns. "The server reads the cookie, looks up the user, sends back JSON" beats "the middleware deserializes the session context to hydrate the request."
- **Mostly short sentences.** Split anything carrying more than one idea or clause. Don't count words robotically — the goal is rhythm a tired brain can follow, not staccato.
- **Skip the hedging.** No "it depends", no "well, technically…", no "there are many ways" — unless the hedge survives the falsehood rule above.
- **No bullet-point dumping.** A wall of bullets is just jargon in a list. Prose, unless there's a genuine sequence or set.
- **No emojis. No analogies to children's media.** This isn't ELI5.

## Length

Aim for **shorter than the original**. If the previous answer was 8 paragraphs, this is 2–3 short ones, or a handful of plain sentences. Dumbing down means *less to read*, not a translated copy of the same volume.
