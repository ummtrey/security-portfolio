# API Testing Checklist

Focused checklist for REST / GraphQL targets.

## REST

- [ ] Enumerate endpoints from docs, JS, mobile apps, and traffic
- [ ] Test each HTTP method per endpoint (GET/POST/PUT/PATCH/DELETE)
- [ ] BOLA / IDOR on every resource identifier
- [ ] Broken function-level authorization (admin routes as a normal user)
- [ ] Mass assignment: send extra fields (`role`, `isAdmin`, `verified`)
- [ ] Excessive data exposure: compare API response fields vs UI
- [ ] Rate limiting on sensitive/expensive endpoints
- [ ] Inconsistent authz between v1/v2 or internal/external variants
- [ ] Improper input validation on numeric, enum, and nested fields

## GraphQL

- [ ] Introspection enabled? Dump the schema
- [ ] Query depth / complexity limits (nested query DoS)
- [ ] Field-level authorization on sensitive resolvers
- [ ] Batching abuse (array of queries to bypass rate limits)
- [ ] IDOR via node/id arguments
- [ ] Mutations that shouldn't be exposed to the current role
- [ ] Information leakage in error messages
- [ ] Alias-based request amplification

## Auth tokens

- [ ] JWT structure and claims review
- [ ] Token scope broader than needed
- [ ] Refresh token handling and revocation
- [ ] API keys in client-side code
