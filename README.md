# ⚔️ Git It Good Innit — Repo 3: `git-it-resolved`

**Difficulty:** 🔴 Hard
**Skills practiced:** Branching, merging, reading conflict markers, resolving conflicts

---

## 📖 The Scenario

Two teams worked on the same workshop event page at the same time without coordinating.

**Team A (main branch)** left some fields incomplete — you'll see them marked as `[ERROR]` in red on the page. The event title, date, venue, time, and footer are all broken.

**Team B (feature/update-styles branch)** finished the HTML properly — correct workshop name, correct venue details, correct footer — but never merged their branch.

**Your job:** merge `feature/update-styles` into `main`. When you hit a conflict, the rule is simple:

> ✅ If one side says `[ERROR]` — pick the **other** side.
> ⚠️ One conflict is a trick — **main** has the correct CTA tagline, not the feature branch!

---

## 🌿 Branch Overview

| Branch | Status |
|---|---|
| `main` | Has `[ERROR]` placeholders — incomplete |
| `feature/update-styles` | Approved, complete version |

---

## 🧠 Understanding Merge Conflict Markers

When Git can't automatically merge a file, it marks both versions in the file:

```
<<<<<<< HEAD
  This is the code from your current branch (main)
=======
  This is the code from the branch you're merging in (feature/update-styles)
>>>>>>> feature/update-styles
```

- `<<<<<<< HEAD` to `=======` → your branch (main)
- `=======` to `>>>>>>> feature/update-styles` → incoming branch
- **Delete the markers and keep the correct version**

---

## 🚀 Step-by-Step Instructions

### Step 1 — Fork & Clone

1. Fork this repo to your GitHub account
2. Clone your fork:
   ```bash
   git clone https://github.com/YOUR-USERNAME/git-it-resolved.git
   cd git-it-resolved
   ```

### Step 2 — Explore Both Branches

See all available branches:

```bash
git branch -a
```

Switch to the feature branch and open the page in your browser — notice it looks complete. Then switch back to main and notice the `[ERROR]` placeholders in red.

```bash
git checkout feature/update-styles
git checkout main
```

### Step 3 — Start the Merge

Make sure you're on `main`, then merge the feature branch in:

```bash
git checkout main
git merge feature/update-styles
```

Git will pause and tell you which files have conflicts:

```
CONFLICT (content): Merge conflict in index.html
Automatic merge failed; fix conflicts and then commit the result.
```

### Step 4 — See What's Conflicted

```bash
git status
```

Files listed as `both modified` are the ones you need to fix.

### Step 5 — Resolve the Conflicts

Open each conflicted file in your editor. For each conflict block:

1. Read both versions (above and below `=======`)
2. Keep the correct one (use the `[ERROR]` rule above)
3. Delete all three marker lines (`<<<<<<<`, `=======`, `>>>>>>>`)
4. Make sure the file is still valid HTML after editing

> 💡 **Tip:** VS Code highlights conflicts and shows **Accept Current Change / Accept Incoming Change** buttons — you can click those instead of editing manually.

**Answer key:**

| File | Conflict | Keep |
|---|---|---|
| `index.html` | Event title | Feature branch (`Git It Good Innit: GitHub Workshop`) |
| `index.html` | Date | Feature branch (`4th April 2026, Saturday`) |
| `index.html` | Venue | Feature branch (`LR14A, Level 2, Block D, KICT`) |
| `index.html` | Time | Feature branch (`9:00 AM – 5:00 PM`) |
| `index.html` | Footer | Feature branch (proper credit line) |
| `index.html` | CTA tagline | Main branch (`Spots filling up fast...`) |

### Step 6 — Stage the Resolved Files

Once you've fixed all conflicts in a file, mark it as resolved:

```bash
git add index.html
```

Check nothing is left conflicted:

```bash
git status
```

All files should show `Changes to be committed`, not `both modified`.

### Step 7 — Complete the Merge Commit

```bash
git commit -m "Resolve merge conflicts: keep feature/update-styles approved design"
```

### Step 8 — Push and Open a PR

```bash
git push origin main
```

Then go to GitHub and open a Pull Request if required by your facilitator.

---

*Part of the **Git It Good Innit** workshop series.*
