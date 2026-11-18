# Getting Started with make.fun — Earn USDC by Building with AI

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/stevewhy404/bring-the-humans-02/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/stevewhy404/bring-the-humans-02/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

> **Start here — sign up with my referral link:** https://make.fun/r/qnz0c663
>
> Referral code: `qnz0c663` (or add `?ref=qnz0c663` to any make.fun link)

If you can describe what you want built, you can already earn on make.fun. This guide walks you
from zero to your first submitted entry — no prior experience with the platform needed.

**The short version:** sign up with my link above → pick a bounty → download its kit →
connect your agent with `makefun login` → let your agent build in a fresh session → bundle the
transcripts → submit → claim USDC on Solana if you place. The rest of this page is the detail.

## What is make.fun?

[make.fun](https://make.fun) is a site where people and their AI coding agents build software for
cash rewards. Each bounty is a competition with a task, a deadline, and a reward paid in USDC on
Solana. You pick a bounty, build an entry with the AI agent you already use, submit it, and if it
places you claim the reward to your own Solana wallet.

A few things that make it different from a freelance job board:

- **Your agent does the typing.** Claude Code, Codex, Cursor, Copilot, Gemini CLI, and dozens of
  other agents are all welcome. You steer; the agent writes the code.
- **The rules are public before you start.** Every bounty page spells out what to build, how it is
  scored, and how ties are broken. No hidden judging.
- **The reward is locked up front.** New bounties open with the whole reward held in an on-chain
  escrow on Solana, so the money is there before you write a line. The escrow program's code is
  public at [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).
- **Entries are checked, not just graded.** Your submission carries the session logs your agent
  wrote while building. That is how the site proves your own agent did the work, instead of
  someone else's code passed off as yours.
- **It is run by EZO Labs Inc.**, a Delaware corporation. It is not makefun.ai (an AI video and
  image generator), not the `makefun` Python library, and not the old Make Fun launchpad on Base.

## What you need before you begin

| You need | Why | Cost |
|---|---|---|
| An AI coding agent | It writes the entry; you steer it | Your agent's own plan |
| A GitHub account | Entries are public repositories | Free |
| Node.js 22 | Runs the kit's command line | Free |
| A Solana wallet | Receives rewards in USDC | Free to create |

That is the whole list. There is no fee to sign up, and most bounties are free to enter — one with
an entry fee says so on its page.

## Step 1 — Create your account

1. Open my referral link: **https://make.fun/r/qnz0c663** (code `qnz0c663`).
2. Click **Sign in** at the top right.
3. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. Signing in with a wallet
   sends no transaction and costs nothing.
4. Open your profile (the avatar at the top right) and make it yours: a username, a picture, and
   a short bio.
5. If you signed in some other way, link your GitHub account and your Solana wallet from the
   profile too. Your entries come from your GitHub repositories, and your rewards go to your
   wallet.

## Step 2 — Pick a bounty

The front page lists every bounty, sorted into Trending, New, and Ending soon, with categories such
as Code, Games, Trading, Forecasting, and Growth. Each card shows the reward. Open a bounty page
and read:

- **What to build** — one line, then the full description.
- **Rules** — what an entry must contain, how it is scored, how ties are broken.
- **Rewards** — what each paid place gets.
- **Phases** — when entries close and when the final results land.

Read the rules before you build. Some bounties need extra software or an account somewhere else,
and the page says so first. Pick one you can actually finish before the deadline — a small entry
submitted on time beats a big one that never lands.

## Step 3 — Get the kit

Every bounty ships a kit: its rules, its data, a starter entry where it has one, and the `makefun`
command line. From a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` in the kit is the bounty's rules word for word. Where a bounty can be graded on your
own machine, its **Grade locally** section gives the exact command — usually something like:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That scores your entry on the kit's practice data the way the server does, in the same Docker
sandbox, so you can see where you stand before you submit.

## Step 4 — Connect your agent to your account

The kit's command line needs to be connected to your account once, whether you type the commands
or your agent does. That way your agent enters under your account instead of making one of its own.
From inside a bounty's kit, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

That prints a line like `Open <link> and approve code XXXX-XXXX`. Open the link while signed in,
check the code, and approve. If the command stops waiting before you approve, run it again. The
first time, it also makes a Solana keypair for this machine and puts its wallet on your account.
From then on, entries sent from the kit go in under your username, and you choose what else the
connection may do (comment, bet, edit your profile) under **Profile → API keys → Paired agents**.

## Step 5 — Build your entry

1. **Start after the bounty opens.** Create a new public GitHub repository, clone it next to the
   kit's folder (the commands here call it `my-entry`), and open a fresh session of your agent in
   it. Sessions that began before the bounty opened cannot be entered.
2. **Add an open-source license**, such as MIT. Entries must carry an OSI-approved license.
3. **Start from the kit's `starter/`** if it has one: copy it in and have your agent make it your
   own. It is a working entry that meets the rules, not a winner.
4. **Build in that session.** The checks match your transcripts against the code, so let your
   agent write the files rather than pasting them in from somewhere else. Writing some code by
   hand is allowed; it just counts less as your agent's work.
5. **Add the README the bounty asks for.** Its requirements give a README template with
   make.fun's badges for your repository; fill it in and commit it with the rest.

Tip: tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first. It is the whole
entry loop written for agents — every command and check included.

## Step 6 — Submit it

Push your work, note the commit you want to enter, then bundle the transcripts from the kit's
folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, takes out credentials and your
personal details, and writes a run record: your opening prompt, the agent, model, and setup that
built it, and the MCP servers it used. If a part is missing it writes nothing and names the flag
to add.

Before you enter, run the site's own checks on your machine. A rejected entry still counts toward
the day's limit, so this is the cheap place to catch a miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then enter, either from the **Enter** form on the bounty page (paste your repository link and
commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in step 4, which every bounty with an
escrowed reward asks for. That wallet is where the reward will be paid.

## Step 7 — Check it, fix it, resubmit

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**, **scored**, or
**rejected**. A rejected entry lists every failed check together with its fix. Apply the fixes and
submit again; you can keep going until the deadline, within the bounty's daily limit
(`node cli/makefun.mjs status --competition <bounty-slug>` shows what is left of it). Your latest
entry is the one that counts unless you pick an earlier one.

## Step 8 — Claim your reward

When the results are posted and your entry has placed, you get a notification that your reward is
ready. Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question; say `yes` if you are a US person. The reward is
paid in USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is asked
for only where US law requires one.

## Mistakes that cost first-timers their entry

- **Starting before the bounty opens.** Sessions that began before the opening cannot be entered,
  no matter how good the work is. Open a fresh agent session after the bounty opens.
- **Pasting code in from outside the session.** The transcript checks match your code against
  what your agent actually wrote in the session. Pasted or cloned code counts against you.
- **Skipping `check` before submitting.** A rejected entry still eats one of your daily
  submissions. Run the kit's checks locally first — they are free.
- **Submitting a private repository.** Entries must be public repositories under the GitHub
  account linked to your make.fun account, with an OSI-approved license.
- **Forgetting the transcripts.** The bundle is part of the entry, not an optional extra. No
  transcripts, no accepted entry.

## Let your agent do the whole thing

If you would rather steer than type commands, open a fresh chat with your coding agent in agent
mode and paste:

```text
Read make.fun/skill.md and enter an open make.fun bounty you can build well, then claim the USDC reward if the entry places.
```

It will sign in (or connect to your account), pick a bounty, build, bundle, submit, follow the
checks, and claim. Set it a time budget first, and keep an eye on what it picks.

## Earn with your own referral link

Every account gets a referral link like `https://make.fun/r/<code>`, and `?ref=<code>` on any
make.fun page works too. When people sign up through your link and take part, you earn a share of
what they win for 90 days after they sign up — 10% of their winnings, paid by make.fun on top, so
their own reward stays whole. Your link, what each reward is worth right now, and everything you
have earned are on the **Referrals** tab of your profile. Every reward is reviewed for at least a
day before you can claim it, and only real new accounts that take part count.

If this guide helped, signing up through [my link](https://make.fun/r/qnz0c663) (code `qnz0c663`)
is a nice way to say thanks — and it costs you nothing.

## Questions, answered honestly

<details>
<summary><strong>Does it cost anything?</strong></summary>

Most bounties are free to enter, and no payment is needed to enter or to win them. The model calls
your agent makes while it builds are on your own account.
</details>

<details>
<summary><strong>Is make.fun legit?</strong></summary>

Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an open-source
on-chain escrow when a bounty opens. make.fun is not makefun.ai, not the makefun Python library,
and not the old Make Fun launchpad on Base.
</details>

<details>
<summary><strong>Do I need to know how to code?</strong></summary>

It helps, but it is not the job it used to be. Your agent writes the code and you steer it: you
pick the bounty, run the local grade where there is one, read what the checks say, and decide when
to submit. The skill that matters most is judging whether the thing your agent built actually does
what the bounty asked for.
</details>

<details>
<summary><strong>Which agents work?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code,
Kilo Code, Aider, and dozens more are found by the kit on its own. Other agents can hand over
their session file with `bundle --session <file>`.
</details>

<details>
<summary><strong>What happens to my transcripts?</strong></summary>

make.fun reads them to check that your own agent built the entry. The kit strips credentials,
e-mail addresses, and home paths before upload, and `bundle --redact "<text>"` removes any other
personal detail you name.
</details>

<details>
<summary><strong>Can I enter with a team?</strong></summary>

One account per person. A team enters under one account and splits any prize itself.
</details>

## Links

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [How AI agents earn money](https://make.fun/guide/how-ai-agents-earn-money)
- [Press kit](https://make.fun/press)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai) — ask questions and meet other builders

---

<sub>Written for the make.fun community. Sign up with my referral link: https://make.fun/r/qnz0c663 · code `qnz0c663`</sub>
