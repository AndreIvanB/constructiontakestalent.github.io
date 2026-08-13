# Construction Takes Talent — A/B Review

One URL that lets your team view both builds of the recruiting site, separately or
side by side.

## What's here

```
index.html          landing page — pick a build, or go to compare
compare.html        both builds in one window (Only A / Both / Only B)
404.html            not-found page, served automatically by Pages
favicon.svg         browser-tab icon
.nojekyll           tells Pages to serve files as-is
version-a/
  index.html        build A
  openings.json     build A's job board data
version-b/
  index.html        build B
  favicon.svg
```

## Publishing it

1. github.com → **+** → **New repository**
2. Name it `talent-review`, set it **Public**, create it
3. **Add file** → **Upload files** → drag in everything from this folder,
   keeping the `version-a` and `version-b` folders intact → **Commit changes**
4. **Settings** → **Pages** → Source = **Deploy from a branch**,
   branch `main`, folder `/ (root)` → **Save**
5. Wait 1–2 minutes

Your single link: `https://YOURUSERNAME.github.io/talent-review/`

Faster alternative: zip this folder and drag it onto `app.netlify.com/drop`.
Live in seconds, no repo — but no version history.

---

## How the two builds differ

Same brand, same voice, same square-cornered light palette. The structural
differences worth reviewing:

| | Build A | Build B |
|---|---|---|
| Job board source | `openings.json`, a separate file | `SEED_OPENINGS`, hardcoded in the HTML |
| Roles listed | 15 | 10 |
| Role groups | Field Staff · Project Engineering · Precon & Estimating | Field Leadership · Project Support · Corporate |
| Scope of roles | Field and precon only | Field, project support, and corporate (marketing, accounting, recruiting) |
| Editing postings | Edit the JSON file on GitHub, no code | Edit the JavaScript array |
| Extras | — | 404 page, favicon, robots.txt |

**The grouping difference is the real decision.** A organizes around what stage of
the job someone works in. B organizes around where in the company they sit, and
includes corporate roles A leaves out. Which one you pick shapes what a candidate
thinks you're hiring for.

**The job board mechanics matter too.** A's separate JSON file means whoever
maintains postings never touches code — they edit one file in GitHub's web editor
and commit. B requires editing JavaScript, where a stray comma breaks the page.
A is the more maintainable pattern if a non-developer will own the board.

---

## Before either one faces real candidates

Both builds share the same three placeholders. This is safe to show colleagues and
not safe to run a campaign through.

**1. The intake form silently loses resumes.** `ENDPOINT` is `null` in both, so
submitting opens a `mailto:` draft — and a `mailto:` link cannot carry a file
attachment. The form asks candidates to attach manually; most won't. This is the
one that costs you a hire.

Fix: set `ENDPOINT` to a URL accepting a `POST` with `multipart/form-data`.
Formspree, Basin, and Formcarry all have free tiers and handle uploads. An ATS
inbound endpoint (Greenhouse, Lever, Workable) is the better long-term answer
because it also gives you a real job feed.

Resumes are personal data. Whatever receives them needs access control, a
retention policy, and encryption at rest — and CCPA applies to California sourcing.

**2. The email address is invented.** `hello@constructiontakestalent.com` appears
in both. Nobody has confirmed the domain exists or that mail routes anywhere.

**3. Every job link goes to LinkedIn's generic jobs page.** Not one points at a
real posting. Clicking through looks broken.

**Also:** anyone with the Pages URL can open it. Free public repos have no
password option.
