---

### ✅ **2. Ajouter un workflow CI/CD (GitHub Actions)**
Pour **NestJS** (`marketplace-api`) :
```yaml
# .github/workflows/ci.yml
name: CI API
on:
  push:
    branches: [develop, staging, main]
  pull_request:
jobs:
  build-test:
    runs-on: ubuntu-latest
    services:
      postgres:
        image: postgres:16
        env:
          POSTGRES_DB: testdb
          POSTGRES_USER: postgres
          POSTGRES_PASSWORD: postgres
        ports: ["5432:5432"]
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
      - run: npm ci
      - run: npx prisma generate
      - run: npm run test
