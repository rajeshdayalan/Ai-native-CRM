# PRD 1: Customer context timeline

## Goal

Give each customer account a single page where you paste in call notes, emails and meeting summaries and see them stacked in date order, with each entry recording who added it and when. This is the first building block of your AI native CRM's full customer context.

## User story

As a revenue operations lead or customer success team member, I want to paste call notes, emails and meeting summaries onto one page per customer account and see them in date order, so that I get the full story of the customer in one place instead of a thin record saved by hand.

## Project setup

1. Create a new Replit project using the Python template, and connect it to a new Git repository so your code and the PRD file live together.
2. Use a simple, common stack: Python with Flask for the web server, server-rendered HTML templates (Jinja) for the pages, and SQLite for storage. No front-end framework is needed for this feature.
3. Add Flask to the project dependencies, and pytest for tests.
4. Create main.py with a Flask app that listens on host 0.0.0.0 and the port Replit provides, and set the Replit Run button to start it.
5. Add the PRD file PRD-1-customer-context-timeline.md to the root of the repository.
6. Press Run and open the Replit preview to check a basic home page loads before building the feature.
7. Run the tests locally in the Replit shell with pytest.

## Requirements

**R1.** You can create a customer account with a name and see a list of all accounts. Each account in the list links to its own timeline page.

- [ ] Submitting the new account form with a name creates the account and it appears in the account list.
- [ ] Submitting the form with an empty name is rejected with an error message and no account is created.
- [ ] Clicking an account in the list opens that account's timeline page.

**R2.** Each account has a single timeline page showing the account name, a form to add an entry, and all entries for that account.

- [ ] The timeline page shows the correct account name.
- [ ] The page shows only entries belonging to that account, never entries from another account.
- [ ] An account with no entries shows an empty-state message instead of a blank page; the wording is To be decided.

**R3.** You can add an entry by choosing its type (call note, email or meeting summary), giving the date the interaction happened, and pasting the text.

- [ ] Submitting a valid entry saves it and it appears on the timeline without needing to re-enter anything.
- [ ] The type can only be one of: call note, email, meeting summary.
- [ ] Submitting with empty text, no type or no date is rejected with an error message and nothing is saved.

**R4.** Each entry automatically records who added it and when it was added, and both are shown on the entry. How the person is identified (sign-in or a typed name) is To be decided.

- [ ] Every saved entry stores an author and a date-and-time it was added, set by the app rather than typed by the user for the time.
- [ ] Each entry on the timeline displays its author and the date and time it was added.
- [ ] An entry cannot be saved without an author.

**R5.** Entries are stacked in date order using the date the interaction happened. Whether newest or oldest appears first is To be decided. Entries with the same interaction date are ordered by the time they were added.

- [ ] Adding three entries with different interaction dates in a mixed order shows them sorted by interaction date.
- [ ] Two entries with the same interaction date appear in the order they were added.
- [ ] Each entry shows its type and interaction date.

**R6.** Pasted text is shown exactly as written, keeping line breaks, and is displayed safely as plain text.

- [ ] Text with several paragraphs keeps its line breaks on the timeline.
- [ ] Text containing HTML or script tags is shown as plain text and is not run or rendered as HTML.

**R7.** Accounts and entries are stored in SQLite and survive the app restarting.

- [ ] After stopping and restarting the app, all previously created accounts and entries are still shown.
- [ ] Each entry is linked to exactly one account in the database.

**R8.** There is a maximum length for pasted text, and text over the limit is rejected with a clear message. The limit itself is To be decided.

- [ ] Text at or under the limit saves successfully.
- [ ] Text over the limit is rejected with an error message and nothing is saved.

## Out of scope

- Editing or deleting entries or accounts.
- AI summaries, customer intelligence or any AI agent access.
- Automatic import from email, calendars, call recording tools or an existing CRM.
- File uploads or attachments.
- Search and filtering across entries or accounts.
- Roles, permissions and team or multi-company accounts.
- Contacts, deals or any other CRM records beyond the account and its entries.

## Test checklist

- [ ] Create an account with a name and confirm it appears in the list.
- [ ] Try to create an account with no name and confirm it is rejected.
- [ ] Add a call note, an email and a meeting summary to one account and confirm all three appear with type, interaction date, author and time added.
- [ ] Confirm entries on one account do not appear on another account's page.
- [ ] Add entries with mixed interaction dates and confirm they are sorted in date order.
- [ ] Add two entries with the same interaction date and confirm they appear in the order added.
- [ ] Try to save an entry with empty text, no type or no date and confirm each is rejected.
- [ ] Paste multi-paragraph text and confirm line breaks are kept.
- [ ] Paste text containing a script tag and confirm it shows as plain text.
- [ ] Paste text over the length limit and confirm it is rejected.
- [ ] Restart the app and confirm all accounts and entries are still there.
- [ ] Run pytest and confirm all automated tests pass.

## To be decided

- How is the person who adds an entry identified: a simple sign-in, or a name typed when adding the entry?
- Should the timeline show the newest entries first or the oldest first?
- What is the maximum length of pasted text for one entry?
- What wording should the empty timeline message use?
- Are call note, email and meeting summary the only entry types you want for now?

## Build prompt

Paste this into Replit:

```text
You are building one feature in a new Replit project. Read the PRD file PRD-1-customer-context-timeline.md in the root of this repository before writing any code, and follow it closely.

First, do the project setup described in the PRD: a Python Flask app with server-rendered Jinja templates and SQLite storage, listening on host 0.0.0.0 and the port Replit provides, started by the Run button. Add pytest for tests.

Then build only the Customer context timeline feature: a list of customer accounts, and a single page per account where the user pastes call notes, emails and meeting summaries and sees them stacked in date order, with each entry recording who added it and when. Do not build anything listed as out of scope in the PRD, such as editing or deleting, AI features, imports, file uploads, search or permissions.

Meet every acceptance criterion for requirements R1 to R8. Show pasted text safely as plain text with line breaks kept, and store everything in SQLite so it survives a restart.

Add automated tests with pytest that cover each acceptance criterion, including validation errors, ordering by interaction date with the tie-break by time added, entries not leaking between accounts, and safe display of HTML in pasted text. Make sure all tests pass.

Some things in the PRD are marked To be decided: how the author is identified, whether newest or oldest entries appear first, the maximum text length, and the empty timeline wording. Do not choose these yourself. Stop and ask me about each one before building the parts that depend on it.

When you finish, tell me how to run the app and the tests, and list any acceptance criterion you could not meet.
```
