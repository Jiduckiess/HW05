# JMeter test plans

Final plans in this directory:

- `23127172_Load_20260812.jmx` — read-heavy
- `23127172_Stress_20260812.jmx` — auth-heavy
- `23127172_Spike_20260812.jmx` — transactional
- `23127172_Endurance_20260812.jmx` — 15-minute read-heavy soak

Keep files human-reviewable and commit each plan as a separate procedure step. Do not commit generated `.jtl` data here; place it in `results/`.
