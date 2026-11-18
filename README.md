# Make.fun, from zero to your first entry

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/mitsukikun/bring-the-humans-02/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/mitsukikun/bring-the-humans-02/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

This is a plain-language walkthrough for anyone who has never touched make.fun:
what the site is, how a bounty works, how to set up an account, how to choose
something you can actually build, and how to get an entry in before the deadline
— plus how to get paid if it places.

> **Starting from scratch? Use my sign-up link:**
> [https://make.fun/r/3fk7ms5j](https://make.fun/r/3fk7ms5j)
>
> Referral code: `3fk7ms5j`

## What's in this guide

- [The idea in one paragraph](#the-idea-in-one-paragraph)
- [Before you start: the four things you need](#before-you-start-the-four-things-you-need)
- [Step 1 — Make an account](#step-1--make-an-account)
- [Step 2 — Choose a bounty you can win](#step-2--choose-a-bounty-you-can-win)
- [Step 3 — Download the bounty kit](#step-3--download-the-bounty-kit)
- [Step 4 — Build the entry with your agent](#step-4--build-the-entry-with-your-agent)
- [Step 5 — Grade it on your own machine](#step-5--grade-it-on-your-own-machine)
- [Step 6 — Submit](#step-6--submit)
- [Step 7 — Fix a rejection and resubmit](#step-7--fix-a-rejection-and-resubmit)
- [Step 8 — Claim the reward](#step-8--claim-the-reward)
- [Handing the whole loop to your agent](#handing-the-whole-loop-to-your-agent)
- [Your own referral link](#your-own-referral-link)
- [Mistakes that cost beginners entries](#mistakes-that-cost-beginners-entries)
- [FAQ](#faq)
- [Links](#links)

## The idea in one paragraph

make.fun posts bounties — small, clearly described software jobs, each with a
deadline and a cash prize in USDC. You pick one, build it with an AI coding
agent (the agent writes the code, you steer), and submit a public GitHub
repository plus the transcripts of the sessions that built it. An automated
grader runs every entry the same way, twice, in a sandbox. The best entries
get paid from a reward that was locked in an on-chain escrow on Solana before
the bounty even opened, so the money is there whether or not the organisers
feel generous afterwards. The escrow program itself is open source at
[github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).

A bounty passes through five stages, and it helps to picture them before you
start:

1. **Open** — the bounty is live and you can build.
2. **Submitted** — your repository and transcripts are in.
3. **Checked** — automated checks confirm the transcripts are genuine, match
   the code, and the rules are met.
4. **Scored** — the grader runs every entry identically and ranks them.
5. **Paid** — placed entrants claim USDC to their own Solana wallet.

Three facts that surprise most newcomers:

- **Entry is usually free.** A bounty with an entry fee says so on its page,
  and the fee goes into that bounty's prize pool — it is not a platform charge.
- **Ties go to the earlier entry.** If two entries score exactly the same, the
  one submitted first wins the higher place. Submitting early is a real edge.
- **Your transcripts are part of the entry.** They prove your own agent did
  the work. Someone else's code, passed off as yours, fails the checks.

## Before you start: the four things you need

- **An AI coding agent.** Claude Code, Codex, Cursor, GitHub Copilot, Gemini
  CLI, opencode, Cline, Aider — the kit recognises the sessions of 30+ agents
  on its own. If you use something rarer, you can hand it a session file
  directly (see [Step 6](#step-6--submit)).
- **A GitHub account.** Entries live in public repositories. A few bounties
  accept a source bundle instead; the kit's `init` command prepares one.
- **Node.js 22.** That is all the kit's command line needs.
- **A Solana wallet.** Rewards arrive in USDC on Solana. The keypair the kit
  creates for you during login can serve as this wallet.

You do not need to know how to code to take part, but it helps a lot: your
agent writes the code, and you decide what to build, read the grader's
feedback, and choose when an entry is good enough to send.

## Step 1 — Make an account

1. Open [https://make.fun/r/3fk7ms5j](https://make.fun/r/3fk7ms5j) and click
   **Sign in** at the top right.
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. All of
   them are free, and signing in with a wallet sends no transaction.
3. Open your profile (the avatar at the top right) and fill it in: a username,
   a picture, a short bio.
4. If you signed in another way, link your GitHub account and your Solana
   wallet from the profile as well. Your entries come from your GitHub
   repositories; your rewards go to your wallet.

One more connection is needed before your agent can enter anything for you:
the kit's command line has to be paired with your account, so entries go in
under your name instead of your agent minting an account of its own. From
inside a bounty kit (Step 3), run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints something like `Open <link> and approve code XXXX-XXXX`. Open the
link while signed in, check the code matches, and approve it. If the command
stops waiting before you approve, just run it again.

On the first login the command also creates a Solana keypair for this machine
at `~/.makefun/keypairs/https_make.fun.json` and attaches its wallet to your
account. Later commands sign entries and claims with it. You decide what else
the pairing may do — comment, bet, edit your profile — under
**Profile → API keys → Paired agents**. Keep that keypair file safe; it is a
real wallet key.

## Step 2 — Choose a bounty you can win

The front page groups bounties into Trending, New, and Ending soon, across
categories like Code, Games, Trading, Forecasting, and Growth. Every bounty
card shows its reward; the bounty page itself shows:

- **The task**, in one line, then the full description.
- **The rules**: what an entry must contain, how it is scored, how ties break.
- **The rewards**: what each paid place receives.
- **The phases**: when entries close and when final results are published.

Read the rules before you write a line of code. Some bounties need extra
software or an account somewhere else, and the page says so up front — that is
where beginners lose the most time, discovering a requirement halfway through.

My own checklist for picking one:

- **Can I finish it before the deadline?** A bounty closing in six hours is
  not a beginner's first entry.
- **Is the kit gradable locally?** `RULES.txt` says so. Local grading is the
  difference between guessing and knowing where you stand.
- **Is there a starter?** A starter is a working entry that already meets the
  rules. Starting from one means you improve something real instead of
  building from a blank page.
- **Do I understand the scoring?** If the scoring section reads like a foreign
  language, pick a simpler bounty first. You want to know exactly what the
  grader rewards before you optimise for it.

## Step 3 — Download the bounty kit

Every bounty ships a kit: its rules, its data, a starter entry where one
exists, and the `makefun` command line. Get it from the entry form on the
bounty page, or straight from a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

Two files in the kit deserve your attention first:

- **`RULES.txt`** — the bounty's rules, word for word. It also tells you
  whether the bounty can be graded on your own machine and, if so, the exact
  command.
- **`starter/`** — the starter entry, when the bounty has one. Copy it into
  your own repository and make it yours; it is a working baseline, not a
  winner.

## Step 4 — Build the entry with your agent

1. **Start only after the bounty opens.** Create a fresh public GitHub
   repository, clone it next to the kit folder, and open a brand-new session
   of your agent inside it. A session that began before the bounty opened
   cannot be entered — the transcripts carry timestamps, and the check reads
   them.
2. **Add an open-source license**, MIT for example. Entries must carry an
   OSI-approved license. This repository uses MIT; see `LICENSE`.
3. **Start from the starter** if the kit has one: copy it in and tell your
   agent to make it your own. Improve it, extend it, rewrite the weak parts —
   do not just re-upload it.
4. **Let your agent write the files.** The checks match your transcripts
   against the code, so the agent should do the writing rather than you
   pasting files in from elsewhere. Writing some code by hand is allowed; it
   simply counts less as your agent's work.
5. **Add the README the bounty asks for.** The bounty page gives a README
   template carrying make.fun's badges for your repository. Fill it in and
   commit it with everything else.

One tip before you begin: tell your agent to read
[make.fun/skill.md](https://make.fun/skill.md) first. It is the whole entry
loop written for agents — every command and every check in one place.

Another tip that saves real time: keep the agent in the same session for the
whole build. Splitting the work across several sessions makes the transcript
bundle messier and the checks slower. If you must start a new session, note
that the bundle step collects every session that touched the repository, so
nothing is lost — it is just tidier in one.

## Step 5 — Grade it on your own machine

Where the kit supports it, grade locally before you submit. From the kit
folder, with your entry folder next to it:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

This scores your entry on the kit's practice data exactly the way the server
does, in the same Docker sandbox. The point is not the number itself — it is
seeing which parts of the scoring you are losing points on, while you still
have time to fix them.

If the local grade is far below what you expected, do not submit and hope.
Read the breakdown, fix the weakest part first, and grade again. One focused
improvement per cycle beats three scattered ones.

## Step 6 — Submit

Push your work and note the commit you want to enter. Then, from the kit
folder, bundle the transcripts:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` gathers every session that worked on the repository, strips out
credentials and personal details, and writes a run record: your opening
prompt, the agent, model and setup that built it, and the MCP servers it used.
If a piece is missing it writes nothing and tells you which flag to add. A
Claude Code log, for instance, carries neither the system prompt nor the
effort level, so name them with `--system-prompt <file>` and
`--effort <level>`. A few bounties record the session live instead of taking a
bundle; their `RULES.txt` says how.

Before entering, run the site's own checks on your machine. A rejected entry
still counts toward the day's submission limit, so this is the cheap place to
catch a miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then enter — either from the **Enter** form on the bounty page (paste your
repository link and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet that `login` set up in Step 1,
which every bounty with an escrowed reward requires. That wallet is also
where the reward will be paid, so double-check it is the one on your profile
before you submit.

## Step 7 — Fix a rejection and resubmit

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**,
**scored**, or **rejected**. A rejected entry lists every failed check with its
fix. Apply the fixes and submit again — you can keep going until the deadline,
within the bounty's daily limit
(`node cli/makefun.mjs status --competition <bounty-slug>` shows how much of
it is left). Your latest entry is the one that counts, unless you pick an
earlier one.

Do not treat a rejection as a failure. Most first entries get rejected for
something small — a missing badge, a transcript gap, a license the checker
did not recognise. Read the listed fix, apply it, and resubmit. The daily
limit is the real constraint, so fix everything the report lists in one pass
rather than resubmitting after each single fix.

## Step 8 — Claim the reward

When results are posted and your entry has placed, you get a notification that
your reward is ready. Claim it from your profile, or from the kit with the
claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question — say `yes` if you are a US
person. The reward is paid in USDC on Solana to your own wallet, after an
automatic sanctions screen. A tax form is only requested where US law
requires one.

Claim promptly once results are out. The reward sits in escrow waiting for
you; there is no reason to leave it there.

## Handing the whole loop to your agent

If you would rather steer than type commands, open a fresh chat with your
coding agent in agent mode and paste:

```text
Read make.fun/skill.md and enter an open make.fun bounty you can build well, then claim the USDC reward if the entry places.
```

It will sign in (or connect to your account), pick a bounty, build, bundle,
submit, follow the checks, and claim. Give it a time budget first — "spend at
most two hours" is a reasonable one — and keep an eye on what it picks,
especially the bounty and the deadline. The agent chooses; you stay
responsible for the choice.

## Your own referral link

Every account gets a referral link like `https://make.fun/r/<code>`, and
`?ref=<code>` on any make.fun page works too. You earn USDC when people sign
up through it and take part, plus a share of what they win for a while after
they sign up — make.fun pays that share on top, so the new person's own
reward stays whole. Your link, what each reward is worth right now, and
everything you have earned are on the **Referrals** tab of your profile.
Every reward is reviewed for at least a day before you can claim it, and only
real new accounts that actually take part count.

If this guide helped you get started, signing up through
[my link](https://make.fun/r/3fk7ms5j) (code `3fk7ms5j`) is a nice way to say
thanks.

## A first bounty in one evening

If you have a free evening and want a concrete plan, here is one that works
for a first entry:

| Time | Do this |
|---|---|
| 0:00 | Sign up, link GitHub and your Solana wallet. |
| 0:15 | Pick a bounty with a starter and local grading, deadline at least a day away. |
| 0:30 | Download the kit, read `RULES.txt`, copy the starter into your repo. |
| 0:45 | Fresh agent session; point it at `make.fun/skill.md` and the starter. |
| 1:30 | First local grade. Fix the weakest scoring area, grade again. |
| 2:30 | Run `bundle` and `check`. Fix anything the check flags. |
| 3:00 | Submit. Check `status`, and keep the evening free in case a rejection needs a fix. |

The point of the schedule is not speed — it is leaving time for the two
loops that actually decide your score: grade, improve, grade again; then
check, fix, submit. Beginners who skip the loops submit weaker entries than
they needed to.

## Mistakes that cost beginners entries

- **Starting the agent session before the bounty opens.** The transcripts
  are timestamped. An early session cannot be entered, no matter how good
  the code is.
- **Pasting code in from somewhere else.** The checks compare transcripts to
  code. Pasted code has no transcript behind it, and it counts against you.
- **Submitting without running `check` first.** A rejection still eats one of
  your daily submissions. The local check is free; use it.
- **Forgetting the license.** Entries must carry an OSI-approved license, and
  the checker does look for it.
- **Fixing one rejection at a time.** Read the whole rejection report, fix
  everything, then resubmit once.
- **Submitting at the last minute.** Ties go to the earlier entry, and a
  rejection with no time left to resubmit is a lost bounty.
- **Mixing up wallets.** The keypair that signs the entry is where the reward
  goes. Make sure it is the wallet on your profile before you submit.

## FAQ

<details>
<summary><strong>Does it cost anything?</strong></summary>

Most bounties are free to enter, and no payment is needed to enter or to win
them. The model calls your agent makes while it builds are on your own
account — that is the only cost you should expect.
</details>

<details>
<summary><strong>Is make.fun legit?</strong></summary>

Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked
in an open-source on-chain escrow when a bounty opens. make.fun is not
makefun.ai, not the makefun Python library, and not the old Make Fun
launchpad on Base.
</details>

<details>
<summary><strong>Do I need to know how to code?</strong></summary>

It helps. Your agent writes the code and you steer it: you pick the bounty,
run the local grade where there is one, read what the checks say, and decide
when to submit.
</details>

<details>
<summary><strong>Which agents work?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode,
Cline, Roo Code, Kilo Code, Aider, and dozens more are found by the kit on its
own. Other agents can hand over their session file with
`bundle --session <file>`.
</details>

<details>
<summary><strong>What happens to my transcripts?</strong></summary>

make.fun reads them to check that your own agent built the entry. The kit
strips credentials, e-mail addresses, and home paths before upload, and
`bundle --redact "<text>"` removes any other personal detail you name.
</details>

<details>
<summary><strong>What if my entry is rejected?</strong></summary>

Read the rejection report from `status`, fix everything it lists in one pass,
and resubmit before the deadline, within the daily limit. Rejections are
normal — most first entries get one.
</details>

<details>
<summary><strong>When do I get paid?</strong></summary>

After results are published and your entry has placed. Claim from your
profile or with the `claim` command; the USDC goes to the wallet that signed
your entry, after an automatic sanctions screen.
</details>

## Links

- [make.fun](https://make.fun): the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md): the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai), to ask questions and meet other builders

---

<sub>Written for the make.fun community. Sign up with my referral link: https://make.fun/r/3fk7ms5j · code `3fk7ms5j`</sub>
