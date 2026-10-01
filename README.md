# FitFindr

> ### 👋 Start here
>
> **New to this repo? Read [RUNNING.md](RUNNING.md) first** — setup, every
> command, and what to do when something breaks.
>
> Once `python test.py` passes:
>
> ```bash
> python app.py listings --full -n 6      # read the data (Milestone 1)
> python app.py fields                    # what you can filter on
> python app.py ask 'vintage graphic tee under $30'
> ```
>
> All three tools are stubs, so that last command will do nothing useful yet.
> That's the starting position.
>
> **The rest of this file is your submission.** Fill it in as you go.

---

<!-- ─────────────────────────────────────────────────────────────────────────
     HOW TO USE THIS FILE

     This is your submission. Fill each section in as you finish the milestone
     it belongs to — don't leave it all to the end.

     Unit 3 asks for the first five sections. Unit 4 adds the five below them.
     Leave the unit 4 sections alone until then; they're here so you know
     what's coming.

     Everything is pasted as TEXT. No screenshots, no images, no video links.
     A typed block of output gets full credit; a picture of the same output
     gets none.
     ───────────────────────────────────────────────────────────────────────── -->

<!-- ═══════════════════════ UNIT 3 — THE BUILD ═══════════════════════ -->

## What This Does

<!-- Three or four sentences: what a user asks for, and what they get back. -->



---

## Tool Inventory

<!-- Four lines per tool. This is worth 2 points and it's the single most
     common place students lose them.

     "Returns a list" earns NOTHING. The description has to say what is IN
     the list.

     The empty case isn't optional either — it's the thing your loop branches
     on, and if you don't decide it here you'll discover it as a crash in
     Milestone 5. -->

### `search_listings`

- **What it does:** searches the listings for an item that matches the given desciption
- **Inputs:** <!-- name and type each: `max_price` (float), not "a price" -->
description (string), size(string), max_price(float),
- **Returns:** A list of dictionaries sorted with the best match first
- **When it has nothing:** returns nothing if there are no matches

### `suggest_outfit`

- **What it does:** returns one or two outfit sugestions based on a given item
- **Inputs:** new_item (dict), wardrobe (dict)
- **Returns:** a string with a new outfit sugestion
- **When it has nothing:** it will ask for ideas

### `create_fit_card`

- **What it does:** writes a probable caption a user would post for a given item
- **Inputs:** outfit (string), new_item(dict)
- **Returns:** a sting with the caption, 2-4 sentences
- **When it has nothing:** a descriptive message explaining that

---

## Planning Loop

<!-- Your branch rule, stated as a rule — the condition AND both paths — plus
     the file and function that holds it.

     Like this:
       "If search_listings returns an empty list, put a message in the session
        and stop. Otherwise take the first result and go to suggest_outfit."
        — agent.py::run_agent

     The grader checks your code against what you claim here, so the file and
     function have to be real. -->

**Branch rule:** if create_fit_card returns a message, print an empty caption, otherwise re-run the method with a non-empty string

**Where it lives:** `agent.py::run_agent`

**How the query is parsed:** I use regex in `_parse_query()` to lowercase the query, pull out a price phrase like `under $30` or `up to 40`, pull out a size like `M` or `size XXS`, remove those matches from the text, and treat whatever is left as the description.

**What moves through the session:** `new_session()` creates the session, then `session["parsed"]` stores the parsed description/size/max_price. Next `session["search_results"]` gets the list from `search_listings()`. If that list is empty, `session["error"]` is set and the run stops. Otherwise the first result goes into `session["selected_item"]`, then `session["outfit_suggestion"]`, and finally `session["fit_card"]`.

---

## Sample Run

<!-- Two things go here.

     1. One FULL query and its output, pasted as text.
     2. Your three per-tool terminal tests — the command and what it printed. -->

**One full query**

```
$ python app.py ask '...'

```

**The three tools, tested one at a time**

```
$ python -c "from tools import search_listings; print(search_listings('graphic tee', max_price=30))"

```

```
$ python -c "from tools import suggest_outfit; ..."

```

```
$ python -c "from tools import create_fit_card; ..."

```

---

## How I Used AI

<!-- Two specific moments. What you asked, what came back, what you changed.

     "I used Claude to help me code" is not enough.

     "I gave Claude my search_listings spec. It returned None on no match
     instead of an empty list, so I changed it" is the level we want. -->

**Moment 1**

- *What I asked for: I used copilot to fill in the functions in tools.py, the prompt was based on what each function should do*
- *What came back: code related to the functions sole purpose*
- *What I changed: bugs then made*

**Moment 2**

- *What I asked for:I use copilot to fill in the run_agent function in agent.py*
- *What came back: a helper function to be used within agent.py*
- *What I changed:*

<!-- ═══════════════════════ UNIT 4 — THE TEST ═══════════════════════

     Don't fill these in during unit 3.
     ═══════════════════════════════════════════════════════════════════ -->

---

## Run Log — Before

<!-- Five criteria, five tries each, in this exact format.

     Five, because your criteria are written out of five. Mark each try PASS
     or FAIL, count the passes, and read that count against your target — a
     row targeting 4 of 5 with three PASS cells is MISSED (3/5).

     `python run_eval.py --label before` runs everything and writes the table
     into results/. Paste it here and fill in the verdicts. -->

| Criterion | Target | Try 1 | Try 2 | Try 3 | Try 4 | Try 5 | Verdict |
|---|---|---|---|---|---|---|---|
| 1. matching query completes     | 4/5 | PASS | PASS | PASS | PASS | PASS | MET |
| 2. impossible query stops early | 5/5 | PASS | PASS | PASS | PASS | PASS | MET |
| empty wardrobe _(diagnostic — not one of your five)_       |  |   |   |   |   |   |  |
| 3. The selected item carries through to outfit suggestions | 4/5 | PASS | PASS | PASS | PASS | PASS | MET |
| 4. The fit card stays specific without repeating itself    | 3/5 | PASS | PASS | PASS | PASS | PASS | MET |
| 5. Empty-search queries stop at the branch with a useful message  | 2/5 | PASS | PASS | PASS | PASS | PASS | MET |
**Real output from one try**, pasted as text, naming the file and function
that produced it:

```
**Try 3**

- stopped early: no
- selected_item: Vintage Band Tee — Faded Grey ($19.0, depop)
- search_results: 0

Outfit suggestion:


Here are two outfit suggestions featuring the **Vintage Band Tee (Faded Grey)** using items from your wardrobe:

### Outfit 1: 90s Grunge Streetwear (Edgy & Casual)
* Lean into the vintage, worn-in aesthetic of the band tee by pairing it with baggy denim and chunky footwear.
* **Top:** Vintage Band Tee — Faded Grey (`lst_033`)
* **Bottoms:** Baggy straight-leg jeans, dark wash (`w_001`)
* **Outerwear:** Vintage black denim jacket (`w_006`) — *Layered on top for a cool double-denim/streetwear edge.*
* **Shoes:** Black combat boots (`w_008`)
* **Accessories:** Black crossbody bag (`w_010`)

### Outfit 2: High-Low Contrast (Relaxed & Earthy)
* Dress down the wide-leg trousers by pairing them with the boxy, faded graphic tee for an effortless, high-low streetwear look.
* **Top:** Vintage Band Tee — Faded Grey (`lst_033`) — *Tucked in slightly to balance the wide-leg fit.*
* **Bottoms:** Wide-leg khaki trousers (`w_002`)
* **Accessories:** Brown leather belt (`w_009`) — *To tie the earth tones together.*
* **Shoes:** Chunky white sneakers (`w_007`)
* **Accessories:** Black crossbody bag (`w_010`)
```

Fit card:

```
Channel your inner 90s rockstar with these two versatile ways to style my Vintage Band Tee in Faded Grey! Whether you're leaning into full grunge streetwear with baggy denim and combat boots or keeping it effortlessly cool with wide-leg trousers, this well-loved piece is ready for its next concert. Grab it now on Depop for just $19.00 and upgrade your rotation!
```

Trace:

```
[1] parse_query
      in:  vintage graphic tee under $30
      out: dict with keys: description, size, max_price
[2] search_listings
      in:  dict with keys: description, size, max_price
      out: 10 items: Vintage Band Tee — Faded Grey, Graphic Tee — 2003 Tour Bootleg Style, Y2K Baby Tee — Butterfly Print … +7 more
[3] select_item
      in:  10 items: Vintage Band Tee — Faded Grey, Graphic Tee — 2003 Tour Bootleg Style, Y2K Baby Tee — Butterfly Print … +7 more
      out: Vintage Band Tee — Faded Grey ($19.0, depop)
[4] suggest_outfit
      in:  Vintage Band Tee — Faded Grey ($19.0, depop)
      out: Here are two outfit suggestions featuring the **Vintage Band Tee (Faded Grey)** using items from your wardrobe…
[5] create_fit_card
      in:  Here are two outfit suggestions featuring the **Vintage Band Tee (Faded Grey)** using items from your wardrobe…
      out: Channel your inner 90s rockstar with these two versatile ways to style my Vintage Band Tee in Faded Grey! Whet…
```

```

---

## Verdicts and Diagnoses

<!-- MET or MISSED per criterion against LAST UNIT's target, plus a sentence on
     how you decided.

     Then, for every miss: which of the four places it happened — a tool, the
     loop's branch, the session, or the model's output — AND the mechanism.

     Not a diagnosis:  "The fit card was bad."
     A diagnosis:      "The fit card criterion missed on 2 of 5 items. Both had
                        an empty brand field. My prompt puts the brand in the
                        first sentence, so the card opened with a blank and read
                        like a fragment. The tool worked; the prompt assumed a
                        field that isn't always there."

     Look for a pattern. Three misses on the same tool is one problem, not
     three. -->

| # | Criterion | Target | Verdict | How I decided |
|---|---|---|---|---|
| 1 |  |  |  |  |
| 2 |  |  |  |  |
| 3 |  |  |  |  |
| 4 |  |  |  |  |
| 5 |  |  |  |  |

**Diagnoses**



---

## Loop Trace

<!-- One full run, printed step by step, with the MCP call visible in it.

     `python app.py ask '...' --trace` once you've added the trace.step()
     calls in Milestone 2.

     Worth pasting BOTH the happy path and the empty-search path. The empty
     one should be visibly shorter, because it stops. If your two traces are
     the same length, your branch isn't working — and this is the fastest way
     anyone will ever find that out. -->

**Happy path**

```

```

**Empty search**

```

```

**On the MCP move:** <!-- what changed in your code, and whether anything
behaved differently afterwards. If the rewire didn't work, say exactly where it
broke — the error text and the last thing that worked. That earns the point in
full. -->



---

## The Improvement

<!-- What you changed, why your diagnosis pointed at it, and the after-run in
     the same table format. One change, measured properly.

     `python run_eval.py --label after` -->

**What I changed:**
All milestones completed, no errors
**Which failure it was meant to fix:**

### Run Log — After

| Criterion | Target | Try 1 | Try 2 | Try 3 | Try 4 | Try 5 | Verdict |
|---|---|---|---|---|---|---|---|
| 1.  |  |  |  |  |  |  |  |
| 2.  |  |  |  |  |  |  |  |
| 3.  |  |  |  |  |  |  |  |
| 4.  |  |  |  |  |  |  |  |
| 5.  |  |  |  |  |  |  |  |

**Did it help, and how do I know:**

<!-- It did help since all test ran with no errors -->



---

## What's Still Broken

<!-- No criteria broken -->



<!-- ═════════════════════════════════════════════════════════════════════

     SUBMISSION CHECKLIST — unit 3

       [x] criteria.md has five numbered criteria, each with a target
       [x] Each criterion has a reason underneath it
       [x] All five unit 3 sections above have real content
       [x] Tool Inventory: all three tools, inputs WITH TYPES, a specific
           return value, and the empty case
       [x] Planning Loop names the branch rule and agent.py::run_agent
       [x] Sample Run: one full query plus the three per-tool tests, as text
       [x] At least four new commits
       [x] Repository URL submitted — WRITE IT DOWN, you submit the same one
           next unit

     SUBMISSION CHECKLIST — unit 4

       [x] mcp_server.py exists with one tool registered
           (or a written record of exactly where the rewire broke)
       [x] Run Log — Before, five criteria, five tries each
       [x] Real output pasted underneath, naming file and function
       [x] A verdict on every criterion
       [x] A diagnosis for every miss, naming a place AND a mechanism
       [x] Loop Trace, with the MCP call visible in it
       [x] All three failure modes triggered and handled
       [x] One improvement, with Run Log — After in the same format
       [x] What's Still Broken
       [x] At least four new commits
       [x] The SAME repository URL as last unit

     Do not delete and recreate this repository. Your commit history is what
     shows your criteria existed before your results did.
     ═════════════════════════════════════════════════════════════════════ -->

---

📖 **How to run this project: [RUNNING.md](RUNNING.md)**
