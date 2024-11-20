---
id: visual-reporter
title: Visual Reporter
---

The Visual Reporter is a new feature introduced in the `@wdio/visual-service`, starting from version [v5.2.0](https://github.com/webdriverio/visual-testing/releases/tag/%40wdio%2Fvisual-service%405.2.0). This reporter allows users to visualize the JSON diff reports generated by the Visual Testing service and transform them into a human-readable format. It helps teams better analyze and manage the visual testing results by providing a graphical interface for reviewing the output.

To utilize this feature, ensure you have the required configuration to generate the necessary `output.json` file. This document will guide you through setting up, running, and understanding the Visual Reporter.

# Prerequisites

Before using the Visual Reporter, make sure you have configured the Visual Testing service to generate JSON report files:

```ts
export const config = {
    // ...
    services: [
        [
            "visual",
            {
                createJsonReportFiles: true, // Generates the output.json file
            },
        ],
    ],
};
```

For more detailed setup instructions, refer to the WebdriverIO [Visual Testing Documentation](./) or the [`createJsonReportFiles`](./service-options.md#createjsonreportfiles-new)

# Installation

To install the Visual Reporter, add it as a development dependency to your project using npm:

```bash
npm install @wdio/visual-reporter --save-dev
```

This will ensure the necessary files are available to generate reports from your visual tests.

# Usage

## Building the Visual Report

Once you have run your Visual tests and they generated the `output.json` file, you can build the visual report using either the CLI or interactive prompts.

### CLI Usage

You can use the CLI command to generate the report by running:

```bash
npx wdio-visual-reporter --jsonOutput=<path-to-output.json> --reportFolder=<path-to-store-report> --logLevel=debug
```

#### Required options:

- `--jsonOutput`: The relative path to the `output.json` file generated by the Visual Testing service. This path is relative to the directory from which you execute the command.
- `--reportFolder`: The relative directory where the generated report will be stored. This path is also relative to the directory from which you execute the command.

#### Optional options:

- `--logLevel`: Set to `debug` to get detailed logging, especially useful for troubleshooting.

#### Example

```bash
npx wdio-visual-reporter --jsonOutput=/path/to/output.json --reportFolder=/path/to/report --logLevel=debug
```

This will generate the report in the specified folder and provide feedback in the console. For example:

```bash
✔ Build output copied successfully to "/path/to/report".
⠋ Prepare report assets...
✔ Successfully generated the report assets.
```

#### Viewing the Report

:::warning
Opening `path/to/report/index.html` directly in a browser **without serving it from a local server** will **NOT** work.
:::

To view the report, you need to use a simple server like [sirv-cli](https://www.npmjs.com/package/sirv-cli). You can start the server with the following command:

```bash
npx sirv-cli /path/to/report --single
```

This will produce logs similar to the example below. Note that the port number may vary:

```logs
  Your application is ready~! 🚀

  - Local:      http://localhost:8080
  - Network:    Add `--host` to expose

────────────────── LOGS ──────────────────
```

You can now view the report by opening the provided URL in your browser.

### Using Interactive Prompts

Alternatively, you can run the following command and answer the prompts to generate the report:

```bash
npx @wdio/visual-reporter
```

The prompts will guide you through providing the required paths and options. In the end the interactive prompt will also ask if you want to start a server to view the report. If you choose to start the server, the tool will launch a simple server and display a URL in the logs. You can open this URL in your browser to view the report.

![Visual Reporter CLI](/img/visual/cli-screen-recording.gif)

![Visual Reporter](/img/visual/visual-reporter.gif)

#### Viewing the Report

:::warning
Opening `path/to/report/index.html` directly in a browser **without serving it from a local server** will **NOT** work.
:::

If you opted **not** to start the server via the interactive prompt, you can still view the report by running the following command manually:

```bash
npx sirv-cli /path/to/report --single
```

This will produce logs similar to the example below. Note that the port number may vary:

```logs
  Your application is ready~! 🚀

  - Local:      http://localhost:8080
  - Network:    Add `--host` to expose

────────────────── LOGS ──────────────────
```

You can now view the report by opening the provided URL in your browser.

# Report Demo

To see an example of how the report looks, visit our [GitHub Pages demo](https://webdriverio.github.io/visual-testing/).

# Understanding the Visual Report

The Visual Reporter provides an organized view of your visual test results. For each test run, you will be able to:

- Easily navigate between test cases and see aggregated results.
- Review metadata such as test names, browsers used, and comparison results.
- View diff images showing where visual differences were detected.

This visual representation simplifies the analysis of your test results, making it easier to identify and address visual regressions.

# CI Integrations

We are working on supporting different CI tools like Jenkins, GitHub Actions and so on. If you like to help us then please contact us on [Discord - Visual Testing](https://discord.com/channels/1097401827202445382/1186908940286574642).