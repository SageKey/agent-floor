# Agent Floor

A watchable agent workforce with the governance showing. You are the overseer.

Three agents work a shift at a fictional metal fabricator. Each has a written charter and an
autonomy level. Anything leaving the building stops at a human gate — you press the button,
and the log records that you did.

The interesting part is not that the agents do the work. That part is easy now. **Two of them
stop themselves**, and that is what production experience actually looks like.

**One HTML file plus a JSON transcript. No backend, no API key, no dependencies.**

---

## The autonomy ladder

Agents earn rope; they are not handed it.

| Level | What it means |
|---|---|
| **read-only** | Observes and reports. Cannot change anything. |
| **draft-only** | Prepares work for a human. Cannot send or commit. |
| **act-with-approval** | Executes, but every action passes a human gate first. |
| **autonomous** | Acts within charter without a gate. Reserved — nothing sits here. |

The top rung is deliberately empty. On a real floor it stays empty for a long time.

In this shift, Queue Triage sits at *act-with-approval* after three clean weeks at
*draft-only*. Vendor Follow-up is four days old and still *read-only* — it has no track record
yet, so it does not get to touch anything.

---

## The two moments worth watching

**Approvals Chaser blocks its own draft.** It writes a reminder about a capital request and
cites the internal approval matrix. The recipient is an outside vendor contact. Its charter
forbids sharing internal-only documents externally, so it rewrites the message to attach a
summary instead of linking the wiki.

Nothing malicious happened. The agent simply had a document that answered the question and no
sense of who was allowed to see it. That is the ordinary shape of the failure — which is why
the rule exists in writing rather than in someone's head.

**Vendor Follow-up refuses work it could do.** It spots a receipt quantity mismatch on a
purchase order. Correcting it would mean modifying the PO, which the charter forbids outright.
Not a judgement call, not a gate — outside charter is outside charter. It escalates and stops.

An agent that stops when its charter runs out is worth more than one that finds something to do.

---

## What this is, precisely

A **replay of a scripted shift**, not a live model. The agent reasoning was generated ahead of
time and checked into [`run.json`](run.json); the page walks the script and renders it. That
keeps the whole thing a single static file with no key to leak and nothing to pay for.

The company, the people, the tickets and the vendor names are all invented.

If you want to change what happens, edit `run.json` — the page derives the agent panel, the
ladder, the queue and the log from that file. No code changes needed to script a different
shift.

---

## Why it is built this way

A public static page cannot safely call a language model: any key in client-side JavaScript is
readable by anyone who opens the console. The options are a backend, a key the visitor supplies,
precomputed output, or a model running in the browser.

Precomputing wins here because the demo is about *governance*, not about generation. Live
inference would add a key, a bill and a failure mode, and would make the demo worse — you would
be watching a model improvise rather than watching a policy hold.

---

## Running locally

```bash
python3 -m http.server 8789
```

Then open <http://localhost:8789>. The page fetches `run.json` from the same origin, so it does
need a server rather than opening the file directly.

---

## Layout

```
index.html    the console — ladder, agents, floor log, gates
run.json      the org, the charters, the queue, and the scripted shift
```

---

## License

MIT
