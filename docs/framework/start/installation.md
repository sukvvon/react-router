---
title: Installation
order: 1
---

# Installation

React Router can be used minimally with your own bundling and data loading (like previous versions) or maximally with the built-in Vite plugin (that adds framework features that came from Remix).

The full feature-set is easiest to use with Vite plugin so the getting started guides will focus there.

To use React Router minimally with your own bundling, server rendering, etc. refer to [Manual Usage][manual_usage] guide.

## Starter Template

Most projects start with a template. Let's use a basic template maintained by React Router:

```shellscript nonumber
npm create react-router@pre <projectDir>
# or
pnpm create react-router@pre <projectDir>
# or
bunx create-react-router@pre <projectDir>
# or
yarn create react-router@pre <projectDir>
```

Now change into the new directory and start the app

```shellscript nonumber
cd my-react-router-app
npm i
npm run dev
```

You can now open your browser to `http://localhost:5173`

<!-- TODO: Show how to find and use community templates -->

## Without the Vite Plugin

## Manual Installation with Vite

Instead of a starter template, you can set up a project from scratch.

First create a new directory and install dependencies:

```shellscript nonumber
mkdir my-new-app
cd my-new-app
npm init -y
npm install react react-dom react-router@pre @react-router/node@pre @react-router/serve@pre
npm install -D vite @react-router/dev@pre
```

Now create the following files:

```shellscript nonumber
mkdir app
touch app/root.jsx
touch app/home.jsx
touch app/routes.js
touch vite.config.js
```

And then fill them in:

```tsx filename=app/root.jsx
import {
  Outlet,
  Scripts,
  ScrollRestoration,
} from "react-router";

export function Layout() {
  return (
    <html lang="en">
      <body>
        <Outlet />
        <ScrollRestoration />
        <Scripts />
      </body>
    </html>
  );
}

export function HydrateFallback() {
  return <div>Loading...</div>;
}

export default function Root() {
  return <h1>Hello, world!</h1>;
}

export function ErrorBoundary() {
  return <h1>Something went wrong</h1>;
}
```

```tsx filename=app/home.jsx
export default function Home() {
  return <h2>Home</h2>;
}
```

```ts filename=app/routes.js
import { index } from "@react-router/dev/routes";

export const routes = [index("./home.jsx")];
```

```tsx filename=vite.config.js
import { reactRouter } from "@react-router/dev/vite";
import { defineConfig } from "vite";

export default defineConfig({
  plugins: [reactRouter()],
});
```

```json filename=package.json
{
  // add these two keys to your package.json
  "type": "module",
  "scripts": {
    "dev": "react-router dev",
    "build": "react-router build",
    "start": "react-router-serve ./build/server/index.js"
  }
}
```

And finally run the app:

```shellscript nonumber
npm run dev
```

## Next Steps

[Routing](./routing)

[manual_usage]: ../how-to/manual-usage