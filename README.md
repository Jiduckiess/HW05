# HW05 — Performance Testing

> This repository contains the verified local test artifacts. Items marked pending need to be completed before final course submission.

## Submission checklist

- [x] Create three distinct endpoint scenarios and JMeter plans.
- [x] Use one CSV input file for each endpoint group.
- [x] Attach raw JTL files and HTML reports for Load, Stress and Spike.
- [x] Capture JMeter with Activity Monitor in the same frame for the three scenarios.
- [x] Complete a 14.98-minute endurance run with six CPU/RAM evidence points.
- [x] Complete the AI audit, critique and raw-log analysis.
- [x] Add a hardware-spec screenshot in `evidence/hardware/`.
- [x] Upload an unlisted Vietnamese video of at least 6 minutes and paste its URL.
- [ ] Replace audit timestamps with exact chat timestamps and retain full AI outputs.
- [ ] Export the Markdown reports to PDF and create the required ZIP.

## Test summary

| Field | Value |
| --- | --- |
| Student ID | `23127172` |
| Student name | `Nguyễn Chí Đức` |
| Public repository | `https://github.com/Jiduckiess/HW05` |
| Demo video (unlisted YouTube) | `https://youtu.be/lv36drb4dDE` |
| Date tested | 2026-08-15 |
| Hardware / hostname evidence | MacBook Pro 14-inch, Apple M4 Pro, 24 GB unified memory, 512 GB SSD; hardware screenshot: `evidence/hardware/macbook-pro-m4-pro-specs.png`; hostname screenshot: `evidence/hardware/hostname.png` (`jiduckiess@192`) |
| Endurance threshold | At least 9.66 stable samples/s at 10 users; backend Node real memory 29.9–34.1 MB |
| Bugs / performance issues filed | No confirmed issue filed; completed scenarios had 0.00% errors. |

| Scenario | Endpoint group / workflow | Plan | Input CSV | Raw log | HTML report | Result |
| --- | --- | --- | --- | --- | --- | --- |
| Load | `GET /api/products?search=` → `GET /api/products/:id` | `test-plans/23127172_Load_20260812.jmx` | `data/read-heavy_products.csv` | `results/load/23127172_Load_20260812.jtl` | `results/load/html-report/` | Passed: 200 samples, 0.00% errors |
| Stress | `POST /api/login` | `test-plans/23127172_Stress_20260812.jmx` | `data/auth-heavy_credentials.csv` | `results/stress/23127172_Stress_20260812.jtl` | `results/stress/html-report/` | Passed: 100 samples, 0.00% errors |
| Spike | login → `POST /api/cart` → `POST /api/checkout` | `test-plans/23127172_Spike_20260812.jmx` | `data/transactional_orders.csv` | `results/spike/23127172_Spike_20260812.jtl` | `results/spike/html-report/` | Passed: 180 samples, 0.00% errors |

## Self-assessment

| Criterion | Max | Self-assessed |
| --- | ---: | ---: |
| Load testing | 20 | 20 |
| Stress testing | 20 | 20 |
| Spike testing | 20 | 20 |
| AI analysis + misinterpretation hunt | 10 | 10 |
| Continuous performance testing proposal | 10 | 10 |
| Agent Skill | 10 | 10 |
| **Total** | **100** | **100** |

## Packaging

Create `23127172_HW05_AI_Performance_100.zip` from the prepared folder `23127172_HW05_AI_Performance_100/`. Exclude the local `eshop-sut/` clone and local secrets/build artefacts.
