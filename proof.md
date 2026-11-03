# User budget quick action proof

Tested feature commit c9dfd6411d3e4376c55c974e0f30e67087b77b2a
Baseline 4187e1ae890aabd87f156caae80e4e5bcf3cfd8f

Local frontend http://127.0.0.1:3097/ui/users, real proxy http://127.0.0.1:4097, dedicated PostgreSQL and Redis, two serving proxy workers with reload and the v2 migration resolver. Seeded public e2e dummy users only. No inference calls are involved

Before and after show the same user, budget and URL. The baseline uses the feature commit's SVG license relocation so the unchanged logo can compile. Feature screenshots were captured before the equivalent numeric validation expression was split into named variables for lint, then all 54 tests passed again at the final code

Before, open the row menu for e2e-internal-user. It has no Adjust budget action
After, select Adjust budget. The current amount is 12.345 and reset period is weekly. Save 42.765. POST /user/update returns 200, the exact request contains only user_id and max_budget, and the value survives a reload. Spend and budget_reset_at remain unchanged
After, select Unlimited budget and monthly. POST /user/update returns 200 with max_budget null and budget_duration 30d. Both values survive a reload
After, sign in as the seeded read-only admin and open the same row menu. Adjust budget is absent

Validation passed with 54 focused Vitest tests, npm run build, npm run typecheck and BASE_REF=upstream/main make check. A direct Next image-size check also proves that the baseline logo fails recognition, the adjusted logo passes, and its license comment is preserved verbatim
