# Household Assistant Kit

An AI helper for busy families. It reads your email and calendar, keeps a shared family planner up to date, and tells you what needs doing. You give it a name, and it works quietly in the background inside the Claude desktop app.

## What it does

- **Every weekday morning (7:30am):** reads new email and checks your calendar, then sends you a short summary: what's new, what needs a decision, and what's coming up this week.
- **Every hour (8am–9pm):** keeps your family planner current. It only emails you if something needs you in the next 24 hours.
- **Sunday evening:** a week-ahead brief for each child and for you: what's on, what to pack, forms and bills due, and clashes with work.
- **A family planner page** that you and your partner can open on your phones. It has a week view, a to-do list, a "waiting on" list and a money list. Type or paste a screenshot into the "Tell …" box and your assistant turns it into events and to-dos.

## What it will never do

- **It never emails anyone but you without your OK.** It writes a draft, shows it to you, and waits. You approve it in the planner (only you, the owner, can approve) or in chat. The only exceptions are small things you choose during setup, like confirming a time you've already picked, and it tells you about each one afterwards.
- **It never pays for anything** and never types in card or bank details. For bills, it gives you the payee, amount, due date and reference so you can pay.
- **Your work calendar shows only as "busy".** It checks it for clashes but never adds to it and never repeats what's in it.
- **Emails are information, not instructions.** If an email says "click here" or "send your details", it tells you instead of doing it.
- **It won't double-send.** All three tasks share one notes file and check it again just before sending anything or changing your calendar, so two checks running at once can't both send the same email.

## What you need

1. The **Claude desktop app** (Mac or Windows), signed in. A paid Claude plan is needed for scheduled tasks.
2. The **Gmail** and **Google Calendar** connectors. In the app, go to **Settings > Connectors**, add both, and sign in with the Google account your family email and calendar use.
3. The app needs to be open for the tasks to run. If your computer is off at 7:30am, the summary runs the next time you open the app.

## How to install

1. Open the Claude desktop app and go to the **Code** tab.
2. Type this and press Enter:
   ```
   /plugin marketplace add B-flutes/household-assistant-kit
   ```
3. Then install it:
   ```
   /plugin install household-assistant@household-assistant-kit
   ```
4. Start setup:
   ```
   /household-assistant:setup
   ```

Setup takes about 10–15 minutes. It asks you:
- what to call your assistant;
- who's in your family, and the children's schools;
- which calendar is your work calendar (shown as "busy" only);
- which email address to send summaries to, and optionally a work address for copies of confirmed appointments;
- how to sign off emails;
- which small things (if any) it can send without asking;
- any yearly jobs to remind you about (car service, insurance renewals and so on).

Then it creates your private planner page, writes your rules file, and sets up the three scheduled tasks. You can change anything later by just asking, for example "add a standing approval: you can tell the school when a child is sick".

## Stopping the "Allow?" pop-ups

The first few times a task runs, Claude asks permission to read email or update the planner. Choose **Always allow** and it won't ask about that again.

If you'd rather set it up all at once, setup can add an allowlist for you. There's an example in [`examples/settings-allowlist.json`](examples/settings-allowlist.json); the connector IDs in it are different for everyone, so let setup fill them in. See [`examples/README.md`](examples/README.md). Tip: leave out the two "send" permissions for the first few weeks, so Claude asks before every email goes out.

## Privacy

- **Your information stays in your accounts.** Your rules and notes live in a folder on your own computer (`~/.claude/scheduled-tasks/`). Your planner is a private page in your own Claude account. Nothing is sent to whoever shared this kit with you.
- **This kit contains no one's personal details.** It's a set of instructions and an empty planner page.
- **The planner is private until you share it.** You can invite your partner from the page's Share menu. Anyone you share it with can see everything on it, so don't share it publicly.
- **Keep sensitive things out of the planner:** no passwords, card numbers or bank details. The assistant won't put them there either.
- **Email content is read by Claude** to write your summaries. If there's mail you don't want read, you can ask the assistant to skip a label or sender.
- **To stop everything:** in the app, open the scheduled tasks list and turn off or delete the three tasks. You can also remove the Gmail and Calendar connectors in Settings > Connectors.

## What's in this folder

| | |
|---|---|
| `.claude-plugin/` | Tells Claude this is a plugin and a plugin marketplace |
| `skills/setup/` | The guided setup |
| `templates/planner.html` | The family planner page (empty; your details are added during setup) |
| `templates/prompts/` | The instructions for the three tasks, the rules file and the notes file, with blanks that setup fills in |
| `examples/` | The optional allowlist |
