# Job search starter

<img src="assets/mascot/pip_flight_loop.gif" alt="Courier bird" width="120">

A local workspace for searching job boards, drafting applications, and preparing for interviews.

## Setup for a new user

1. Extract this archive into a new folder. It contains the workflow and blank templates, with no previous user's files or Git history. Keep your personalized copy private.
2. Install Python 3.10 or later, Bun, and the signed-in coding assistant used by this framework. For PDF output, install a LaTeX distribution with `lualatex` and `xelatex`. See `SETUP.md` for packages and troubleshooting.
3. Put your resume in `documents/cv/`. Optional source material belongs in `documents/linkedin/`, `documents/diplomas/`, and `documents/references/`.
4. Copy `profile.example.yaml` to `profile.local.yaml`. Fill in your own contact details, work history, preferences, and eligibility. Copy `answers.example.yaml` to `answers.local.yaml` and answer each question yourself. Blank eligibility and EEO fields mean unanswered; they are never assumed to be Yes or No.
5. Start the coding assistant in this folder and run `/setup`. Ask it to read your resume and the two local YAML files, confirm the facts with you, then populate `CLAUDE.md`, the candidate and behavioral profile files, and the resume/cover-letter templates. The YAML files are onboarding inputs, not an automatically loaded runtime configuration.
6. Install search-tool dependencies. In PowerShell:

```powershell
Get-ChildItem .agents/skills -Directory | ForEach-Object {
  Push-Location (Join-Path $_.FullName 'cli')
  bun install
  Pop-Location
}
```

7. Use `/scrape` to find postings, `/rank` to review matches, `/apply <posting-url>` to draft application documents, and `/interview` for preparation. Search connectors ship with several Danish job boards and a professional-network search tool; use `/add-portal` to add a board for your market. Review every document before submitting it yourself.
8. The default workflow uses your signed-in subscription and needs no API keys. If you choose an optional integration that requires a credential, copy `.env.example` to `.env` and enter only your own credential locally. No dotenv loader or paid integration is configured in this copy; follow the chosen integration's setup instructions. Do not paste credentials into chat or commit them.

`resume.example.md` and `cover-letter.example.md` are writing starters. The compilable templates are `cv/main_example.tex` and `cover_letters/cover_example.tex`.

## Privacy and scope

This copy restores the generic framework from before candidate-specific customization. Private application records, portal autofill/submit automation, personal document builders, hosted dashboards, mail evidence, machine settings, browser sessions, and platform issue wiring are excluded. No accounts or services are connected.

After onboarding, `CLAUDE.md`, profile methodology files, and the LaTeX examples will contain your personal data. Keep the repository private and do not share it again without a fresh privacy review. The ignore rules cover common runtime files, but cannot keep personalized tracked templates out of a later commit.

The attached Git bundle, if supplied, contains one new root commit with a neutral author and no parent commits. To start your own repository from the ZIP instead, run `git init -b main`, then review files before committing. Do not copy a `.git` directory from another workspace.

## Validation

```powershell
python -m unittest discover -s tests -t .
python tools/security_guards.py
python tools/lint_skills.py
```

The source framework is licensed under the MIT license; see `LICENSE`. General command documentation is in `WORKFLOW.md`.
