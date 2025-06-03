# Angular 20 Project Setup

## Installation

```sh
pnpm create @angular@latest [project-name]
```

In this case:

- Do you want to create a 'zoneless' application without zone.js (Developer Preview)? Yes
- Which stylesheet format would you like to use? Sass (SCSS) [ https://sass-lang.com/documentation/syntax#scss]
- Do you want to enable Server-Side Rendering (SSR) and Static Site Generation (SSG/Prerendering)? No

Manually add the following props to the angular.json

- "changeDetection: "OnPush"

```json
"schematics": {
  "@schematics/angular:component": {
    "style": "scss",
    "changeDetection": "OnPush"
  }
},
```

## UI

### 1. Tailwind CSS 4

```sh
pnpm add tailwindcss @tailwindcss/postcss postcss
```

- Configure PostCSS: Create a .postcssrc.json file in the root of your project and add the Tailwind CSS plugin:

```json
{
  "plugins": {
    "@tailwindcss/postcss": {}
  }
}
```

- Import Tailwind CSS: Add the following import statement to your src/styles.scss file:

```scss
@use "tailwindcss";
```

- Start Using Tailwind: You can now use Tailwind CSS utility classes in your Angular components, such as:

```html
<div class="bg-red-300">
  <h1 class="text-3xl font-bold underline text-center mt-10">Angular v20 + Tailwind CSS 4</h1>
</div>
```

### 2. Material UI

```sh
pnpm ng add @angular/material
```

```html
<div class="text-center mt-10">
  <button matFab extended>
    <mat-icon>favorite</mat-icon>
    from Material UI
  </button>
</div>
```

### 3. Setting up Tailwind v4 in Visual Code (autocomplete)

> Open Setting > Search "tailwindCSS.experimental.configFile" > Edit in setting.json
> then make sure something like this:

```json
"tailwindCSS.experimental.configFile": "src/styles.scss"
```

or if you want available with tailwind v3

```json
"tailwindCSS.experimental.configFile": {
  ".config/tailwind.config.js",
  "src/styles.scss"
}
```

## Testing

Install the Angular Testing Library along the user-event library:

```sh
pnpm i -D @testing-library/angular @testing-library/dom @testing-library/user-event
```

Next, install Playwright and install the accompanying browsers:

```sh
pnpm i -D @playwright/test
pnpm playwright install
```

## Code Quality

For code quality, we install `angular-eslint`, `eslint-plugin-unused-imports`, `husky`, `prettier`,`lint-staged` and Sheriff.

```bash
pnpm ng add @angular-eslint/schematics
pnpm i -D eslint-plugin-unused-imports husky prettier lint-staged @softarc/{sheriff-core,eslint-plugin-sheriff}
```

To integrate `eslint-plugin-unused-imports` and sheriff into ESLint, add the following to `eslint.config.js`:

```javascript
// exsting imports...

const sheriff = require("@softarc/eslint-plugin-sheriff");
const unusedImports = require("eslint-plugin-unused-imports");

module.exports = tseslint.config(
  // exsting setup...
  {
    files: ["**/*.ts"],
    extends: [sheriff.configs.all],
  },
  {
    plugins: { "unused-imports": unusedImports },
    rules: {
      "@typescript-eslint/no-unused-vars": "off",
      "unused-imports/no-unused-imports": "error",
      "unused-imports/no-unused-vars": [
        "warn",
        {
          vars: "all",
          varsIgnorePattern: "^_",
          args: "after-used",
          argsIgnorePattern: "^_",
        },
      ],
    },
  },
);
```

For defining barrel-less modulesyou can initialize the Sheriff configuration by running the following command:

```bash
pnpm sheriff init
```

Code formatting will be done by prettier, but only for staged files and before a commit:

```bash
pnpm husky init
```

Create the `.lintstagedrc` with the following content:

```text
{
  "*.{js,ts,json,html,scss,css,md}": [
    "prettier --write"
  ]
}

```

`.husky/pre-commit`, should have the following content:

```bash
pnpm ng lint
pnpm ng test --watch=false
pnpm lint-staged --allow-empty
```

When running the 'git commit', the project will be tested before committing to GitHub

## State Management

Next on the list is state management with the NgRx SignalStore. We also include the devtools extension for debugging purposes:

```bash
pnpm i @ngrx/signals @angular-architects/ngrx-toolkit
```

It is also important to use the official ESLint rules for NgRx:

```bash
pnpm i -D @ngrx/eslint-plugin
```

Add the following to the ESLint configuration `eslint.config.js`:

```javascript
// existing imports...
const ngrx = require("@ngrx/eslint-plugin/v9");

module.exports = tseslint.config(
  // existing config...
  {
    files: ["**/*.ts"],
    extends: [...ngrx.configs.signals],
  },
);
```

## Package Manager

This example using PNPM as a package manager.
PNPM is Performant NPM, a package manager for Node.js that aims to address some of the limitations of traditional package managers like npm and Yarn, particularly concerning disk space and installation speed.

---

**Enjoy your new Angular project setup! 🚀**

---
