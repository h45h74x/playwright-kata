# Playwright Kata

## Setup guide

- Install [Git](https://git-scm.com/downloads)
- Install [Node.js](https://nodejs.org/en/download/) (v20.15.1)
- Install [Yarn](https://yarnpkg.com/getting-started/install)
- Clone this repository (see instructions on top)
- Run `yarn` in terminal, at the root of repository

### Test locally

Run `npx playwright install` in terminal to download all necessary browsers for testing (in case of failure try running `npx playwright install --with-deps`)

### Test via Docker server

- For running Playwright in a Docker setup, start a local server instance using this command:

  ```sh
  docker run \
    -d \
    -p 3000:3000 \
    --name playwright-server \
    --rm \
    --init \
    --workdir /home/pwuser \
    --user pwuser \
    mcr.microsoft.com/playwright:v1.51.1-noble \
    /bin/sh -c "npx -y playwright@1.51.1 run-server --port 3000 --host 0.0.0.0"
  ```

- Once your testing is complete, stop the Playwright server by running: `docker stop playwright-server`.

> **Important:** Ensure the Docker image version aligns with your locally installed Playwright version obtained by running `playwright --version`.

#### More information

Check out the [Playwright Docker Docs](https://playwright.dev/docs/docker) for more details about using Playwright with Docker. Or take your setup to the next level as shown in the [playwright-ct-docker-demo](https://github.com/mihkeleidast/playwright-ct-docker-demo) project.

## Verify you are ready for the Kata

- Run `yarn test` in terminal
- Verify that tests are running and the following result is showing up: `8 passed and 8 skipped`
- In case these results are not showing up / something is wrong, please open a Github issue.

## Instructions (during the Kata)

Once in the Kata, follow the instructions [here](https://github.com/cscheffauer/playwright-kata/blob/main/INSTRUCTIONS.md).

## Background

In this repository [fixtures](https://playwright.dev/docs/test-fixtures) and [Page Object Models](https://playwright.dev/docs/pom) are used for abstraction.

- The `mainPage` fixture does automatically navigate to the provided `baseURL` (can be set in test.use) before the actual test code.
- The `mainPage` fixture does automatically close the tab after the test code has been executed.
- To access [page](https://playwright.dev/docs/api/class-page), use `mainPage.page` (mainPage is passed into the test as a argument)
- Accessibility and visual regression utils are in the corresponding Page object models, which can be accessed through `mainPage.accessibility` or `mainPage.visualRegression`
- [@axe-core/playwright](https://playwright.dev/docs/accessibility-testing) is used to scan the page on accessibility issues.
- Visual regression snapshots are automatically generated for LTR, RTL direction and High Contrast mode.
