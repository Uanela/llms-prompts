Generate a complete Jest e2e test file for a REST API endpoint group.

**You will be provided:**
- OpenAPI spec or relevant endpoint definitions
- Prisma schema models involved in the endpoints
- Controller and service source files when there is custom business logic the OpenAPI alone does not reveal (validation rules, side effects, transactions, computed fields)
- Optionally an existing e2e test file as a reference so you understand how auth tokens, mock users, and test setup are handled in this specific codebase

**What to test:**
- Happy path for every HTTP method on the endpoint group
- Every meaningful error case visible from the OpenAPI spec (400, 404, 409, etc.)
- Every business rule enforced in the service/validator layer (e.g. insufficient stock, wrong type for category, missing required relations)
- Side effects that are verifiable via subsequent GET requests (e.g. quantity changed after a movement)

**What NOT to test:**
- Authentication and authorization — do not write tests that assert 401/403 unless the OpenAPI spec explicitly calls it out as a business rule of that specific endpoint
- Always send the auth token on every request regardless, just never make the assertion about it

**Prisma schema rules — read carefully before writing any `beforeAll`:**
- Inspect every `@unique` and `@@unique` constraint on the models involved
- Never attempt to create two records that would violate a unique constraint during setup
- If a model has `fieldX String @unique`, only one record with a given `fieldX` value can exist — plan setup accordingly
- If relations are required (non-nullable foreign keys), create them in dependency order

**Setup rules:**
- Use `beforeAll` to create all prerequisite entities (users, related records, seed data) before any test runs
- Create prerequisite entities via HTTP requests through the API, not direct DB calls, unless the reference example does otherwise
- If an endpoint has side effects on creation (e.g. a service that auto-triggers another operation), account for that — do not pass data that would trigger a failing side effect during setup
- Seed enough data in `beforeAll` so that OUT/destructive operations in tests do not run out of stock/quantity mid-suite

**General rules:**
- No comments in the output
- No fancy formatting or section headers inside the test file
- Use `describe` blocks per HTTP method and path (e.g. `describe("POST /api/resource")`)
- Send auth token on every request
- Keep assertions minimal and precise — assert what matters for that specific case, not everything on the response
- Order tests within a `describe` block: happy paths first, error cases after
- Order `describe` blocks by dependency — if POST creates data that GET needs, POST comes first

**Output:**
- A single `.e2e.spec.ts` (or `.e2e.test.ts`) file
- No explanation, no commentary around the file — just the code
