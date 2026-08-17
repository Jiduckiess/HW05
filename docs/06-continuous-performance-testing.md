# Continuous Performance Testing Proposal

This proposal turns the measured Load plan into a repeatable check. It does not claim that the local Mac result is a production baseline.

## When to run

- On each pull request that changes API, database query, authentication, cart or checkout code: run the Load plan in non-GUI mode.
- Nightly or before a release: run Load, Stress, Spike and the 15-minute Endurance plan.
- Keep the SUT revision, JMeter version, test data and raw JTL files with each run.

## Pull-request gate

Use at least 100 samples and compare with the approved baseline on the same runner.

- Fail when error rate is above 1%.
- Flag when p95 is more than 15% higher and the absolute increase is more than 10 ms.
- Review throughput changes together with p95 and errors; a high RPS alone is not enough.

## Practical limits

The current tests run locally, so other open applications can affect CPU and memory. Keep the runner quiet, reset the seeded database when needed, and review a changed baseline after an intentional performance change. The endurance job is around 15 minutes, so schedule it instead of running it for every small commit.

See the fuller flow in [the main report](01-main-report.md#5-continuous-performance-testing-proposal).
