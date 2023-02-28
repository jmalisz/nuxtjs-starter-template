# Nuxt3 starter template

This is an opinionated starter template for Nuxt3 to facilitate faster project creation.

Main points:

- Set up with recommended `VSCode` extensions, `EditorConfig`, `Eslint` and `Prettier` for better developer experience.
- Uses strict `TypeScript` and `Zod` to ensure good type safety.
- Uses `ChakraUI` for components (CSS-in-JS with `Emotion`).
- Communicates with BE by `tRPC`. Uses DataCell concept.
- Uses `PostgreSQL` along with `Prisma` ORM.
- Has integration/unit tests with Jest.
- Has E2E tests with Playwright.

See `package.json` for specific packages. Check `.nvmrc` for NodeJS version.

Look at the [Nuxt 3 documentation](https://nuxt.com/docs/getting-started/introduction) to learn more about Nuxt3.

## Development

Add environment variables to `.env` from `.env.example`.

Install dependencies with `npm install` (or any other package manager, `npm` is assumed going forward).

Start development database (empty, requires `docker-compose` to work):

```
docker-compose up
```

Run database migrations:

```
npx prisma migrate dev
```

Start the development server on http://localhost:3000:

```
npm run dev
```

Run integration and unit tests:

```
npm run jest
```

Run E2E tests:

```
npm run playwright:headed
```

See `package.json` for full list of commands.

## Production

Add environment variables to `.env` from `.env.example`.

Install dependencies with `npm install` (or any other package manager, `npm` is assumed going forward).

Build the application for production:

```bash
npm run build
```

Locally preview production build:

```bash
npm run preview
```

Check out the [deployment documentation](https://nuxt.com/docs/getting-started/deployment) for more information.
