# Playwright Practice Projects

This repository contains two independent Playwright projects. Each project has its own `package.json`, lockfile, Playwright configuration, and test suite. There are no root-level npm scripts; run commands from the project you want to work with.

## Projects

| Folder | Purpose |
| --- | --- |
| `saucedemo_practice` | UI tests for the SauceDemo shopping site |
| `kenya-airways` | Playwright examples and a flight-search investigation for the Kenya Airways website |

## Prerequisites

- Git
- Node.js 20 or later, with npm

Each project manages its dependencies separately. Install dependencies and browser binaries from inside that project's folder.

## Install

From the repository root, install either or both projects:

```powershell
cd .\saucedemo_practice
npm ci
npx playwright install
```

```powershell
cd ..\kenya-airways
npm ci
npx playwright install
```

`npx playwright install` downloads the browsers used by the Playwright configuration. Run it again after changing the Playwright version if the required browser binaries are missing.

## Run Tests

Run these commands from the relevant project folder.

```powershell
# List discovered tests without launching a browser
npx playwright test --list

# Run the full suite in Chromium, Firefox, and WebKit
npx playwright test

# Run a single spec in Chromium
npx playwright test tests/example.spec.ts --project=chromium

# Open Playwright's interactive test UI
npx playwright test --ui

# Open the HTML report after a test run
npx playwright show-report
```

To run the other project, change to its folder first. The reports and test results are generated separately inside each project and are excluded from Git.

## Troubleshooting

- **Browser executable is missing:** Run `npx playwright install` from the project folder.
- **Windows says Application Control blocked a browser file:** Installing the browser may succeed while launching it is still blocked by Windows security policy. Check Windows Security and the Code Integrity event log; reinstalling npm packages does not override that policy.
- **A live website test is denied or times out:** The site may block automated traffic or change its UI. Check the browser output and current page before treating this as a Playwright setup problem.

## Current Test Notes

- The SauceDemo problem-user test currently expects a specific hashed image URL. That asset path can change, causing the assertion in `tests/login.spec.ts` to fail in all three browser projects.
- The Kenya Airways booking investigation depends on the public website and may be denied by its anti-bot service. The generic Playwright example tests do not depend on that booking flow.