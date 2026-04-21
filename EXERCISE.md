# Plugin Exercise: "Definition of Done"

You've just joined the team that builds this issue tracker. The PM has sent you
the note below. Your job is to extend the team's Claude Code plugin so that
both asks work out-of-the-box for any dev who installs it.

Read the brief, decide which plugin building blocks you need, then build them.

---

> **From:** Jordan (PM, Issue Tracker)
> **To:** you
> **Subject:** two things driving me nuts
>
> Hey — now that devs are driving the board through the coding agent, two
> problems keep coming up:
>
> **1. Cards land in Done that don't even compile.**
> A dev says "move it to done," the agent obliges, card moves — but
> `npm run typecheck` is red. Our team rule is simple: *nothing reaches the
> Done column unless typecheck passes.* I don't want devs to have to remember
> to run it first, and I don't want to rely on the agent choosing to be
> helpful about it. It needs to be enforced — if anything tries to move a card
> to Done while typecheck is failing, the move doesn't happen and the dev sees
> why.
>
> **2. Nobody does the full wrap-up ritual.**
> When a card *is* actually finished, three things are supposed to happen:
> the card moves to Done, the assignee is cleared, and a one-line summary of
> what changed gets appended to the issue description. Devs do step one and
> forget the other two every time. I'd like a dev to be able to say "wrap up
> the board-layout issue" or "I'm done with #3" — honestly, whatever words
> come out of their mouth — and the agent just does all three steps correctly.
> They shouldn't have to look up a specific command name for this.
>
> Can you make both of these work for anyone who installs our plugin?

---

## Ground rules

- Everything you add must live inside the plugin so it ships with one install.
- Prove it works: introduce a type error, try to move a card to Done, watch it
  get blocked. Fix the error, tell the agent you're done with the issue in
  plain English, watch all three steps happen on the board.
