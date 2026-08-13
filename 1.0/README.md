# Construction Takes Talent — A/B Review

One URL that opens both builds, separately or side by side.

## Files — all at the repo root, no folders

```
index.html      landing page — pick a build, or go to compare
compare.html    both builds in one window (Only A / Both / Only B)
build-a.html    Build A
build-b.html    Build B
openings.json   Build A's job board data
404.html        not-found page
favicon.svg     browser-tab icon
robots.txt
.nojekyll       tells Pages to serve files as-is
```

Everything is flat on purpose. There are no subfolders, so nothing can be
dropped during upload — which is what caused the earlier 404s.

## Publishing

1. github.com → **+** → **New repository** → name it, set **Public**, create
2. **Add file** → **Upload files**
3. Open the unzipped folder, select **all 9 files** (Ctrl+A), drag them in.
   Drag the *files*, not the folder that contains them.
4. **Commit changes**
5. **Settings** → **Pages** → Source = **Deploy from a branch**,
   branch `main`, folder `/ (root)` → **Save**
6. Wait 1–2 minutes

Your link: `https://YOURUSERNAME.github.io/REPONAME/`

### Check it worked

Your repo's main page should list all 9 files with no folder icons. If you see a
folder named `talent-review`, you dragged the container folder instead of its
contents — open it, delete it, and re-upload the files themselves.

### Faster alternative

Zip the folder and drag it onto `app.netlify.com/drop`. Netlify unpacks the zip
itself, so folder structure can't get lost. Live in seconds.

---

## How the two builds differ

Same brand, same voice, same square-cornered light palette.

| | Build A | Build B |
|---|---|---|
| Job board source | `openings.json`, a separate file | `SEED_OPENINGS`, hardcoded in the page |
| Roles listed | 15 | 10 |
| Role groups | Field Staff · Project Engineering · Precon & Estimating | Field Leadership · Project Support · Corporate |
| Scope | Field and precon only | Adds corporate — marketing, accounting, recruiting |
| Editing postings | Edit one JSON file on GitHub, no code | Edit a JavaScript array |

**The grouping is the real decision.** A sorts by what stage of a job someone
works in. B sorts by where in the company they sit, and includes corporate roles
A leaves out. That changes what a candidate concludes you're hiring for.

**Board maintenance matters too.** A's separate JSON file means whoever posts
roles edits one file in GitHub's web editor and commits — no code. B needs
someone editing JavaScript, where a stray comma blanks the page.

---

## Before either faces real candidates

Both builds share the same three placeholders. Safe to show colleagues, not safe
to run a campaign through.

**1. The intake form silently loses resumes.** `ENDPOINT` is `null` in both, so
submitting opens a `mailto:` draft — and a `mailto:` link cannot carry a file
attachment. The form asks candidates to attach manually; most won't. This is the
one that costs you a hire.

Fix: set `ENDPOINT` to a URL accepting a `POST` with `multipart/form-data`.
Formspree, Basin, and Formcarry have free tiers and handle uploads. An ATS
inbound endpoint (Greenhouse, Lever, Workable) is better long-term because it
also gives you a real job feed.

Resumes are personal data. Whatever receives them needs access control, a
retention policy, and encryption at rest — and CCPA applies to California
sourcing.

**2. The email address is invented.** `hello@constructiontakestalent.com` appears
in both. Nobody has confirmed the domain exists or that mail routes anywhere.

**3. Every job link points at LinkedIn's generic jobs page.** Not one goes to a
real posting. Clicking through looks broken.

**Also:** anyone with the Pages URL can open it. Free public repos have no
password option.
