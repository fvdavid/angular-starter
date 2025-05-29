# Angular 20 Project Setup

## Installation

```sh
pnpm create @angular@latest [project-name]
```

In this case:
✔ Do you want to create a 'zoneless' application without zone.js (Developer Preview)? Yes
✔ Which stylesheet format would you like to use? Sass (SCSS) [ https://sass-lang.com/documentation/syntax#scss]
✔ Do you want to enable Server-Side Rendering (SSR) and Static Site Generation (SSG/Prerendering)? No

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

## Development server

To start a local development server, run:

```bash
ng serve
```

navigate to `http://localhost:4200/`.

## Code scaffolding

Angular CLI includes powerful code scaffolding tools. To generate a new component, run:

```bash
ng generate component component-name
```

For a complete list of available schematics (such as `components`, `directives`, or `pipes`), run:

```bash
ng generate --help
```

## Building

To build the project run:

```bash
ng build
```

This will compile your project and store the build artifacts in the `dist/` directory. By default, the production build optimizes your application for performance and speed.

## Running unit tests

To execute unit tests with the [Karma](https://karma-runner.github.io) test runner, use the following command:

```bash
ng test
```

## Running end-to-end tests

For end-to-end (e2e) testing, run:

```bash
ng e2e
```

Angular CLI does not come with an end-to-end testing framework by default. You can choose one that suits your needs.

## Additional Resources

For more information on using the Angular CLI, including detailed command references, visit the [Angular CLI Overview and Command Reference](https://angular.dev/tools/cli) page.
