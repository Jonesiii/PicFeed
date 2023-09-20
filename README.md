# PicFeed

This is a simple frontend application developed with Vue 3. It fetches photos from unsplash.com's API and displays them in a gallery.

Show latest button shows the latest pictures uploaded to unsplash.com. The random button fetches a random picture and the searchbar allows the user to search for pictures.

A working version of the application can be checked out at [GitHub Pages](https://jonesiii.github.io/PicFeed/).

The application does not currently work with Safari.

## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Compile and Minify for Production

```sh
npm run build
```

### Run Unit Tests with [Vitest](https://vitest.dev/)

```sh
npm run test:unit
```

### Run End-to-End Tests with [Cypress](https://www.cypress.io/)

```sh
npm run test:e2e:dev
```

This runs the end-to-end tests against the Vite development server.
It is much faster than the production build.

But it's still recommended to test the production build with `test:e2e` before deploying (e.g. in CI environments):

```sh
npm run build
npm run test:e2e
```

### Lint with [ESLint](https://eslint.org/)

```sh
npm run lint
```
