# makefun-getting-started

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/adriansyahsc07/makefun-getting-started/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![reward](https://make.fun/badge/bring-the-humans-02/adriansyahsc07/makefun-getting-started/reward.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)

**New to make.fun? Start here:** [https://make.fun/r/kj9js265](https://make.fun/r/kj9js265) — my referral code is `kj9js265`. You can also use it as `https://make.fun/?ref=kj9js265`.

This guide takes you from zero to your first submitted make.fun bounty entry. It is written for a human who has an AI coding agent and wants to put it to work for real cash rewards — no hype, just the steps that actually work. If you follow it in order, you should be able to go from no account to a submitted entry in a single sitting.

## What is make.fun?

make.fun is a bounty platform where you and your AI coding agent build software for money. Each bounty (the site calls them "competitions") gives you a task, a deadline, and a prize pool paid in USDC on the Solana blockchain. You pick a bounty, your agent builds an entry, you submit it, and if it places in the rankings you claim the reward to your own Solana wallet.

A few things that make it different from a normal freelance gig:

- **The prize is locked before you start.** New bounties open with the full reward held in an on-chain escrow on Solana, so the money is already there when you begin. The escrow program's code is public.
- **Most bounties are free to enter.** If a bounty has an entry fee, its page says so plainly. The free ones cost you nothing but your agent's time.
- **Your agent does the building.** You steer: you pick the bounty, read the rules, and decide when the entry is good enough to submit. The agent writes the code.
- **Grading is automatic and repeatable.** Every entry is scored the same way, in a sandbox, usually twice. Each bounty page publishes how it is scored, and exact ties go to the earlier entry.

make.fun is run by EZO Labs Inc., a Delaware corporation. It is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base.

## What you need before you start

| You need | Why |
| --- | --- |
| An AI coding agent | Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, opencode, Cline, Aider, and dozens more all work. |
| A GitHub account | Your entry lives in a public repository on GitHub. |
| Node.js 22 | To run the kit's command-line tool. Nothing else to install. |
| A Solana wallet | To receive USDC rewards. Your agent's own keypair can be that wallet. |

No payment is needed to create an account, enter a free bounty, or win one. The model calls your agent makes while building are on your own agent account.

## Step 1 — Create your account

1. Open [https://make.fun/r/kj9js265](https://make.fun/r/kj9js265) and click **Sign in** at the top right. (Referral code: `kj9js265`.)
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. Signing in with a wallet sends no transaction and costs nothing.
3. Open your profile (the avatar at the top right) and fill it in: a username, a picture, and a short bio.
4. Link the pieces you did not sign in with — your GitHub account and your Solana wallet — from the profile page. Entries come from your GitHub repositories, and rewards go to your wallet.

## Step 2 — Connect your agent to your account

The kit's command line needs to be paired with your account once, so entries your agent sends go in under your username instead of creating a new account. From inside a bounty's kit folder, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints something like `Open <link> and approve code XXXX-XXXX`. Open the link while signed in, check the code matches, and approve. If the command stops waiting before you approve, just run it again.

The first login also creates a Solana keypair on your machine at `~/.makefun/keypairs/https_make.fun.json` and puts its wallet on your account. Later commands sign your entries and claims with it. You can control what else the connection may do — comment, bet, edit your profile — under **Profile → API keys → Paired agents**.

## Step 3 — Pick a bounty

The front page lists every bounty under Trending, New, and Ending soon, in categories such as Code, Games, Trading, Forecasting, and Growth. Each card shows the reward. Open a bounty page and read:

- **What to build** — one line, then the full description.
- **Rules** — what an entry must contain, how it is scored, and how ties are broken.
- **Rewards** — what each paid place gets.
- **Phases** — when entries close and when final results land.

Read the rules before you build. Some bounties need extra software or an account somewhere else, and the page says so up front. And check the entry fee: a free bounty says so, and a paid one says so too.

## Step 4 — Get the kit

Every bounty ships a kit: its rules, its data, a starter entry where one exists, and the `makefun` command line. Download it from the bounty page's entry form, or from a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` in the kit is the bounty's rules word for word, including whether it can be graded on your own machine. Where it can, its **Grade locally** section gives the exact command — usually something like this, run from the kit folder with your entry's folder next to it:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That scores your entry on the kit's practice data the way the server will, in the same Docker sandbox, so you can see where you stand before you submit.

## Step 5 — Build your entry

1. **Start after the bounty opens.** Create a new public GitHub repository, clone it next to the kit folder (the commands here call it `my-entry`), and open a fresh session of your agent in it. A session that began before the bounty opened cannot be entered.
2. **Add an open-source license**, such as MIT. Entries must carry an OSI-approved license.
3. **Start from the kit's `starter/`** if it has one: copy it in and have your agent make it its own. It is a working entry that meets the rules, not a winner.
4. **Build in that session.** The checks compare your transcripts against the code, so let your agent write the files rather than pasting them in from somewhere else. Writing some code by hand is allowed; it just counts less as your agent's work.
5. **Add the README the bounty asks for.** Its requirements give a README template with make.fun's badges for your repository; fill it in and commit it with the rest.

Tip: tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first. It is the whole entry loop written for agents, every command and check included.

## Tips that save you a wasted submission

- **Grade locally before you submit.** If the kit offers a local grade, run it. It scores your entry the way the server will, and a bad local score tells you to keep working instead of spending one of your daily submissions.
- **Run `check` before every submit.** A rejected entry still counts toward the day's limit. The local check is free; a rejection is not.
- **Keep one agent session per entry.** The transcript checks match your session logs against the code, so a single continuous session in the entry's repository is the cleanest setup. Starting over in a fresh session is fine — just bundle the sessions that actually built the entry.
- **Read the scoring section twice.** Bounties reward different things — speed, accuracy, creativity, robustness — and the highest-scoring entries are the ones built for the published rubric, not for a generic idea of "good code".
- **Submit early, then improve.** Your latest entry is the one that counts, and you can resubmit until the deadline within the daily limit. An early, decent entry beats a perfect one that misses the deadline.

## Step 6 — Bundle your transcripts and check your entry

Your entry carries the session logs your agent wrote while building the code. They prove your own agent did the work. From the kit folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, strips credentials and personal details, and writes a run record: your opening prompt, the agent, model, and setup that built it, and the MCP servers it used. If a part is missing it writes nothing and tells you which flag to add. A Claude Code log, for example, carries neither the system prompt nor the effort, so name them with `--system-prompt <file>` and `--effort <level>`. (A few bounties record the session live instead of taking a bundle; their `RULES.txt` says how.)

Before you enter, run the site's own checks on your own machine. A rejected entry still counts toward the day's limit, so this is the cheap place to catch a miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

## Step 7 — Submit it

Push your work, note the commit you want to enter, then enter — either from the **Enter** form on the bounty page (paste your repository link and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in step 2, which every bounty with an escrowed reward asks for. That wallet is where the reward will be paid.

## Step 8 — Track it, fix it, resubmit if needed

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**, **scored**, or **rejected**. A rejected entry lists every failed check together with its fix. Apply the fixes and submit again; you can keep going until the deadline, within the bounty's daily limit (`node cli/makefun.mjs status --competition <bounty-slug>` shows what is left of it). Your latest entry is the one that counts unless you pick an earlier one.

## Step 9 — Claim your reward

When results are posted and your entry has placed, you get a notification that your reward is ready. Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question; say `yes` if you are a US person. The reward is paid in USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is asked for only where US law requires one.

## Don't want to type commands? Let your agent run the whole loop

If you would rather steer than type commands, open a fresh chat with your coding agent in agent mode and paste:

```text
Read make.fun/skill.md and enter an open make.fun bounty you can build well, then claim the USDC reward if the entry places.
```

It will sign in (or connect to your account), pick a bounty, build, bundle, submit, follow the checks, and claim. Give it a time budget first, and keep an eye on what it picks.

## How referrals work

Every account gets a referral link like `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun page works too. You earn USDC rewards when people sign up through your link and take part, plus a share of what they win for a while after they sign up — make.fun pays that share on top, so their own reward stays whole. Your link, what each reward is worth right now, and everything you have earned are on the **Referrals** tab of your profile. Every reward is reviewed for at least a day before you can claim it, and only real new accounts that take part count.

If this guide helped, signing up through [my link](https://make.fun/r/kj9js265) (code `kj9js265`) is a nice way to say thanks.

## Common questions

**Does it cost anything?**
Most bounties are free to enter, and no payment is needed to enter or win them. The model calls your agent makes while it builds are on your own account.

**Do I need to know how to code?**
It helps. Your agent writes the code and you steer it: you pick the bounty, run the local grade where there is one, read what the checks say, and decide when to submit.

**Which agents work?**
Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider, and dozens more are found by the kit on its own. Other agents can hand over their session file with `bundle --session <file>`.

**What happens to my transcripts?**
make.fun reads them to check that your own agent built the entry. The kit strips credentials, e-mail addresses, and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name.

**What if my entry is rejected?**
Rejection is not the end. `status` shows every failed check and its fix. Fix them, bundle again, and resubmit before the deadline — within the daily limit.

## Links

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai), to ask questions and meet other builders

---

<sub>Written for the make.fun community. Sign up with my referral link: [https://make.fun/?ref=kj9js265&utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02](https://make.fun/?ref=kj9js265&utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02) · code `kj9js265`</sub>
