# SvelteKit / shadcn Web-App template

Below you'll find all the necessary information to get started with the project, including setup instructions and common commands.

# 🛠️ Technologies used

### Framework: [SvelteKit](https://kit.svelte.dev/docs/introduction) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Runtime: [Bun](https://bun.sh)

#### UI: [shadcn-svelte](https://www.shadcn-svelte.com/) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ORM: [Prisma](https://www.prisma.io/)

##### Testing: [Playwright](https://playwright.dev/), [Vitest](https://vitest.dev/) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Code Quality: [ESLint](https://eslint.org/), [Prettier](https://prettier.io/)

###### Language: [TypeScript](https://www.typescriptlang.org/)

<br>

# 🚀 Getting started

To get the project up and running on your local machine, follow these steps:

### 1. Clone the repository

```bash
git clone https://github.com/Robodealz/webapp.git
cd webapp
```

### 2. Install dependencies

- Using Bun as the package manager:

  ```bash
  bun install
  ```

### 3. Environment setup

- Set type of db in `prisma/schema.prisma`file:

  ```prisma
  datasource db {
      provider = "mysql"
      url      = env("DATABASE_URL")
  }
  ```

- Create a `.env` file in the root directory and populate it with the necessary environment variables:

  ```
  DATABASE_URL="mysql://user:password@hostnameOrIp:port/dbname"
  ```

### 4. Generate Prisma client

```bash
bun prisma generate
```

### 5. Run migrations

```bash
bun prisma migrate dev
```

# 🎨 Run and Build with SvelteKit

### Development server

```bash
bun dev
```

### Build production version

- Building it:

  ```bash
  bun run build

  bun preview # To preview the production build
  ```

- And running the production build with bun:

  ```bash
  cd build

  bun run start
  ```

# 🔗 Useful commands for Prisma

### Open Prisma Studio

```bash
bun prisma studio
```

### Create a New Migration

```bash
bun prisma migrate dev --name add_new_feature
```

# 📦 Using shadcn-svelte components

shadcn-svelte is a anti-component component library for Svelte. Anti component means it's components source code is installed to your `src/lib/components/ui` directory by using it's CLI.

### Component installation

```bash
bunx shadcn-svelte@latest add button
```

Takes component names as space separated input to directly install them.  
Without any component name behind the command, an installer is started where components can be selected.

### Component usage

Inside your Svelte component:

```html
<script lang="ts">
	import { Button } from '$lib/components/ui/button';
</script>

<button>Button</button>
```

<div align="center">
    <img src="./README-assets/shadcn-button.png" alt="shadcn-svelte Button" width="100" />
</div>

### Component update

```bash
bunx shadcn-svelte@latest update button
```

# 🧪 Testing

To run tests using Playwright and Vitest:

### Unit and Integration Tests with Vitest

```bash
bun vitest
```

### E2E Tests with Playwright

```bash
bun playwright test
```

# 🧹 Code Quality

To ensure your code adheres to the set standards using ESLint and Prettier:

### Linting with ESLint

```bash
bun lint
```

### Formatting with Prettier

```bash
bun prettier --write .
```

# 🕸️ WebSocket Server

https://bun.sh/docs/api/websockets

```js
// hooks.server.js

/** @type {import("svelte-adapter-bun").WebSocketHandler} */
export const handleWebsocket = {
	open(ws) {
		console.log('WebSocket opened');
		ws.send('Finally');
	},
	/**
	 * @param {Request} request
	 * @param {Function} upgrade
	 */
	upgrade(request, upgrade) {
		const url = new URL(request.url);
		if (url.pathname.startsWith('/ws')) {
			return upgrade(request);
		}
	},
};
```
