# react-app-with-gh-actions

This repository shows the example of github actions workflow for deploying react app. Since, we don't have a deployment server, we are only printing the output.

```yaml
name: Deploy
on:
  push:
    branches:
      - master
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - name: Get code
        uses: actions/checkout@v3
      - name: Install node
        uses: actions/setup-node@v3
        with:
          node-version: 18
      - name: Install dependencies
        run: npm ci
      - name: Run tests
        run: npm test
        
  deploy:
    needs: test # This job runs only when test job runs successfully
    runs-on: ubuntu-latest
    steps:
      - name: Get code
        uses: actions/checkout@v3
      - name: Install node
        uses: actions/setup-node@v3
        with:
          node-version: 18
      - name: Install dependencies
        run: npm ci
      - name: Build the project
        run: npm run build
      - name: Deploy the react app
        run: |
          echo "Deploying...."
          echo "Deployment successful!"
```
