---
title: My page title
date: 2020-12-08
---

# 1 - _templates

## component/new/new.ejs

```ejs
---
to: components/<%= [h.inflection.camelize(h.dirName(name)), h.camelizedBaseName(name)].filter(Boolean).join('/') %>.tsx
---
<% formattedPath = h.camelizedPathName(name) -%>
<% component = h.camelizedBaseName(name) -%>
import React from 'react';
import { Heading, Center } from '@chakra-ui/core';

/** Description of component */
export function <%= component %>() {
  const message = 'Hola! <%= component %> Created!';

  return (
    <Center bg="red.300" color="white" padding={{ base: 16, lg: 24 }}>
      <Heading>{message}</Heading>
    </Center>
  );
};
```

# 2 - .github

## PULL_REQUEST_TEMPLATE.md

```md
Description of PR that completes issue here...

## Changes

api:

- Description of changes

web:

- Description of changes

## Screenshots

(prefer animated gif)

## Checklist

- [ ] Requires dependency update?
- [ ] Automated tests
- [ ] Looks good on large screens
- [ ] Looks good on mobile

Closes [chXXXX][view ticket](https://app.clubhouse.io/org/story/XXXX)
```

## workflows

### main.js.yml

```yml
name: CI

on: [push]

jobs:
  ###############
  # Lint & Test
  ###############
  tests:
    name: Tests
    runs-on: ubuntu-latest
    # needs: linters
    env:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: postgres
      POSTGRES_DB: myapp_test
      NODE_ENV: test
    services:
      postgres:
        image: postgres:11.5
        env:
          POSTGRES_USER: postgres
          POSTGRES_PASSWORD: postgres
          POSTGRES_DB: myapp_test
        ports: ['5432:5432']
        # Make sure the database is ready before we use it
        options: --health-cmd pg_isready --health-interval 10s --health-timeout 5s --health-retries 5

    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      # Node
      - name: Setup Node
        uses: actions/setup-node@v2.1.1
        with:
          node-version: 14.6.0

      # Yarn cache/install
      - name: Find yarn cache location
        id: yarn-cache
        run: echo "::set-output name=dir::$(yarn cache dir)"
      - name: JS package cache
        uses: actions/cache@v2.1.0
        with:
          path: ${{ steps.yarn-cache.outputs.dir }}
          key: ${{ runner.os }}-yarn-${{ hashFiles('**/yarn.lock') }}
          restore-keys: |
            ${{ runner.os }}-yarn-
      - name: Install packages
        run: |
          yarn install --frozen-lockfile

      # Setup & configure database
      - name: Setup test database
        env:
          NODE_ENV: test
          DATABASE_URL: postgresql://postgres:postgres@localhost/myapp_test
        run: |
          yarn db:migrate

      # Build app and generate types
      - name: Build App
        run: yarn build

      # Lint Code
      - name: ESLint
        run: yarn lint

      # Jest Tests (API/Frontend)
      - name: Run Jest Tests (API & Frontend)
        run: yarn test:ci

      # E2E Tests via Cypress
      - name: Run Cypress E2E Tests
        uses: cypress-io/github-action@v2
        with:
          # build: yarn build
          start: yarn test:server
          wait-on: 'http://localhost:3001'
        env:
          NODE_ENV: test
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          DATABASE_URL: postgresql://postgres:postgres@localhost/myapp_test

      - name: Upload Cypress Screenshots
        uses: actions/upload-artifact@v1
        # Only capture images on failure
        if: failure()
        with:
          name: cypress-screenshots
          path: cypress/screenshots
      - name: Upload Cypress Videos
        uses: actions/upload-artifact@v1
        # Test run video was always captured, so this action uses "always()" condition
        if: always()
        with:
          name: cypress-videos
          path: cypress/videos

  ###############
  # Deploy!
  ###############
  deployStaging:
    name: Deploy to Preview
    runs-on: ubuntu-latest
    # To speed up CI builds, we deploy this in parallel
    # needs: tests

    ## For a typical JAMstack flow, the ref below should be your default branch.
    ## For a traditional flow that auto-deploys staging and deploys prod is as needed, keep as is
    if: github.ref != 'refs/heads/production' # every branch EXCEPT production
    steps:
      - uses: actions/checkout@v2
      - uses: ngduc/vercel-deploy-action@master
        with:
          vercel-token: ${{ secrets.VERCEL_TOKEN }}
          github-token: ${{ secrets.GITHUB_TOKEN }}
          vercel-org-id: ${{ secrets.VERCEL_ORG_ID}}
          vercel-project-id: ${{ secrets.VERCEL_PROJECT_ID}}
          # SET THIS OR YOU WILL DEPLOY TO YOUR PERSONAL VERCEL NAMESPACE
          # scope: ${{ secrets.VERCEL_TEAM_ID }}

  deployProd:
    name: Deploy to Production
    runs-on: ubuntu-latest
    # For production deploys, make sure tests pass first
    needs: tests
    ## For a typical JAMstack flow, the ref below should be your default branch.
    ## For a traditional flow that auto-deploys staging and deploys prod is as needed, keep as is
    if: github.ref == 'refs/heads/production'
    steps:
      - uses: actions/checkout@v2
      - uses: ngduc/vercel-deploy-action@master
        with:
          vercel-token: ${{ secrets.VERCEL_TOKEN }}
          github-token: ${{ secrets.GITHUB_TOKEN }}
          vercel-org-id: ${{ secrets.VERCEL_ORG_ID}}
          vercel-project-id: ${{ secrets.VERCEL_PROJECT_ID}}
          # SET THIS OR YOU WILL DEPLOY TO YOUR PERSONAL VERCEL NAMESPACE
          # scope: ${{ secrets.VERCEL_TEAM_ID }}
          vercel-args: '--prod'
```

```yml
name: CI

on: [push]

jobs:
  
  tests:
    name: Tests
    
    runs-on: ubuntu-latest
    
    env:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: postgres
      POSTGRES_DB: myapp_test
      NODE_ENV: test
    
    services:
      postgres:
        image: postgres:11.5
        env:
          POSTGRES_USER: postgres
          POSTGRES_PASSWORD: postgres
          POSTGRES_DB: myapp_test
        ports: ['5432:5432']
        options: --health-cmd pg_isready --health-interval 10s --health-timeout 5s --health-retries 5
    
    steps:
      - name: Checkout code
        uses: actions/checkout@v2
      
      - name: Setup Node
        uses: actions/setup-node@v2.1.1
        with:
          node-version: 14.6.0
      
      - name: Find yarn cache location
        id: yarn-cache
        run: echo "::set-output name=dir::$(yarn cache dir)"
      
      - name: JS package cache
        uses: actions/cache@v2.1.0
        with:
          path: ${{ steps.yarn-cache.outputs.dir }}
          key: ${{ runner.os }}-yarn-${{ hashFiles('**/yarn.lock') }}
          restore-keys: |
            ${{ runner.os }}-yarn-
      
      - name: Install packages
        run: |
          yarn install --frozen-lockfile
      
      - name: Setup test database
        env:
          NODE_ENV: test
          DATABASE_URL: postgresql://postgres:postgres@localhost/myapp_test
        run: |
          yarn db:migrate
      
      - name: Build App
        run: yarn build
      
      - name: ESLint
        run: yarn lint
      
      - name: Run Jest Tests (API & Frontend)
        run: yarn test:ci
      
      - name: Run Cypress E2E Tests
        uses: cypress-io/github-action@v2
        with:
          start: yarn test:server
          wait-on: 'http://localhost:3001'
        env:
          NODE_ENV: test
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          DATABASE_URL: postgresql://postgres:postgres@localhost/myapp_test
      
      - name: Upload Cypress Screenshots
        uses: actions/upload-artifact@v1
        if: failure()
        with:
          name: cypress-screenshots
          path: cypress/screenshots
      
      - name: Upload Cypress Videos
        uses: actions/upload-artifact@v1
        if: always()
        with:
          name: cypress-videos
          path: cypress/videos
  
  deployStaging:
    name: Deploy to Preview
    runs-on: ubuntu-latest
    if: github.ref != 'refs/heads/production'
    steps:
      - uses: actions/checkout@v2
      - uses: ngduc/vercel-deploy-action@master
        with:
          vercel-token: ${{ secrets.VERCEL_TOKEN }}
          github-token: ${{ secrets.GITHUB_TOKEN }}
          vercel-org-id: ${{ secrets.VERCEL_ORG_ID}}
          vercel-project-id: ${{ secrets.VERCEL_PROJECT_ID}}
  
  deployProd:
    name: Deploy to Production
    runs-on: ubuntu-latest
    needs: tests
    if: github.ref == 'refs/heads/production'
    steps:
      - uses: actions/checkout@v2
      - uses: ngduc/vercel-deploy-action@master
        with:
          vercel-token: ${{ secrets.VERCEL_TOKEN }}
          github-token: ${{ secrets.GITHUB_TOKEN }}
          vercel-org-id: ${{ secrets.VERCEL_ORG_ID}}
          vercel-project-id: ${{ secrets.VERCEL_PROJECT_ID}}
          vercel-args: '--prod'
```

# 3 - .vscode

## settings.json

```json
{
  "editor.tabSize": 2,
  "files.trimTrailingWhitespace": true,
  "editor.formatOnSave": true,
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  },
  "[html]": {
    "editor.formatOnSave": false
  },
  "[prisma]": {
    "editor.defaultFormatter": "Prisma.prisma"
  }
}
```