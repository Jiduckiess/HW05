# Test-plan build sheet

Use this as a build checklist before creating the final `.jmx` files. Replace placeholders only after checking the EShop API implementation.

## Common JMeter setup

- [x] Name plans as `23127172_{ScenarioType}_20260812`.
- [x] Add HTTP Request Defaults, required JSON header, and a scenario-specific CSV Data Set Config.
- [x] Add think time and response-code-200 assertions.
- [x] Write full `.jtl` logs and generate HTML reports in non-GUI mode; use GUI listeners for evidence.
- [x] Use a different listener/report view for each scenario.
- [x] Record SUT commit, machine details, backend resource usage, and test parameters in the main report.

## Load / read-heavy

**Workflow:** `GET /api/products?search=${search_term}` → `GET /api/products/${product_id}`  
**CSV:** `data/read-heavy_products.csv`  
**Distinct view:** `Summary Report`

| Item | Final choice | Reason |
| --- | --- | --- |
| Users | 10 | Modest concurrent browse workload. |
| Ramp-up | 20 s | Avoids creating all users at once. |
| Duration | 10 loops; observed 37.087 s | Produces 200 raw samples. |
| Think time | 1,000 ms | Represents a short browse pause. |
| Assertions | Response code 200 | Prevents an HTTP error being counted as a successful sample. |

## Stress / auth-heavy

**Workflow:** `POST /api/login`; use dedicated valid test accounts for the measured load and document the 3-fail/30-second lockout reset when it occurs.  
**CSV:** `data/auth-heavy_credentials.csv`  
**Distinct view:** `Aggregate Report`

| Item | Final choice | Reason |
| --- | --- | --- |
| Start → max users / steps | 0 → 20 users | Standard Thread Group starts users evenly through ramp-up. |
| Ramp-up / hold | 30 s / 5 loops | Produces 100 valid-login requests without claiming a saturation point. |
| Think time | 500 ms | Avoids an unrealistic tight login loop. |
| Lockout reset | Not needed in this run; if lockout is tested, run `node database.js` then restart `node server.js`. | This run used valid credentials; reset deletes local test data. |
| Assertions | Response code 200 | All 100 measured logins were intended to be valid. |

## Spike / transactional

**Workflow:** login for setup → `POST /api/cart` → `POST /api/checkout`; pass the JWT in `Authorization: Bearer <token>` and verify cart cleanup/order creation.  
**CSV:** `data/transactional_orders.csv`  
**Distinct view:** `View Results Tree`

The transactional CSV contains login and product/order fields so this scenario is self-contained. In JMeter, extract `token` from the login JSON response, then use `${product_id}`, `${product_name}`, `${price}`, `${quantity}`, `${total_amount}`, and `${shipping_address}` in the later requests.

| Item | Final choice | Reason |
| --- | --- | --- |
| Baseline → spike VUs | 0 → 30 users | The implemented plan is an abrupt short workload. |
| Ramp-up / spike hold / recovery | 5 s / 2 loops / no recovery stage | This is a limitation: it cannot prove recovery after the spike. |
| Think time | 500 ms | Keeps a brief pause between workflow steps. |
| Correlation / auth | JSON extractor `$.token`; `Authorization: Bearer ${token}` | Sends the token returned by each user's login. |
| Assertions | Response code 200 for all workflow calls | Confirms successful HTTP workflow calls; duplicate/order-state checks are a future improvement. |
