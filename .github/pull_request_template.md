<!--
Title: `<type>(<scope>): MAIR-XXX <ticket name>` (Conventional Commits, it drives the release).
Ask a review from the team (CarolinHugo, LAURETbenjamin, MathTek, Quentintnrl), minus yourself.
-->

Closes #<issue> · Jira: https://mairie-360.atlassian.net/browse/MAIR-XXX

## What

## Tests

## Personal data
<!--
GDPR (MAIR-295): tick exactly one, the CI checks it (mairie360/CICD gdpr-pr-cicd.yml).
Personal data is anything that identifies or describes an agent: names, e-mail, phone, user ids,
what they did and when, free text they write, IP addresses, devices, sessions, cookies.
"Yes" when the PR adds, renames or drops such a column, returns it in a response, stores, logs,
exports, sends it to a third party, deletes it, or changes who can read it.
-->
- [ ] No: this PR does not add, change, expose, log, send or delete personal data.
- [ ] Yes: it does.
  Inventory: <!-- Database: update gdpr/inventory.yaml in this PR. Other repos: link the Database PR that updates it, or say why it does not change. -->
