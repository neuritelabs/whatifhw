# whatifhw

**What if the hardware were different?** whatifhw is an open-source simulator for that question. It predicts how AI model serving benchmarks would perform on hardware that is described as data.

**Status: early.** This repository holds the project's goals, its license and its lint check. There is no code yet.

## Why

Building or buying hardware to test an idea is slow and costly. whatifhw lets you ask the question first, for:
- hardware that is still in development;
- hardware that is too expensive to buy for a test;
- a proposed change to existing hardware, such as a faster link or a new memory level.

## Goals

1. **Benchmark-shaped results.** Run the MLPerf Inference scenarios (Offline, Server, SingleStream and MultiStream) on modeled hardware, with the benchmark's own settings files. Other load generators can be added later.
2. **Time only.** The simulator predicts time: throughput, latency, time to first token, and where each delay comes from. It never computes a model's outputs.
3. **Hardware as data.** A device is a file of values. Each value says where it comes from: a datasheet, a measurement, a calculation from other values, or an assumption. Code is needed only for new behavior.
4. **Several levels of detail.** Each part of the hardware can use a formula, a table of measurements, results from another simulator, or a cycle-by-cycle model for a short window of time. The level is a setting, not a code change.
5. **Hybrid mode.** Run a real system on real hardware with one part replaced by a model. Examples are the memory management, or a memory level the machine does not have.
6. **Honest output.** Every result is labeled simulated or hybrid. A simulated result is never presented as a measured or official one.
7. **Repeatable.** The same inputs and the same random seed give the same result files, byte for byte. A hybrid run uses real hardware, so it is repeated and its spread is reported.
8. **Practical.** A 10-minute simulated benchmark runs in minutes to tens of minutes on a laptop or one server core.
9. **Easy to learn and to extend.** A small core with few concepts. New hardware, serving engines, memory policies and load generators are plug-ins.

**Not goals:**
- accuracy results or token values;
- power and energy;
- training;
- official MLPerf results or submissions.

## Open-source guidance

**License.** The Apache License 2.0, in [LICENSE](LICENSE). You may use, change and share the code, also for commercial use. Keep the license and the copyright notices, and mark the files you changed.

**Contributing.**
- For a larger change, open an issue first and describe the problem it solves.
- Keep each pull request small, with one change.
- Every pull request must pass the lint check. Run it on your machine first:

  ```bash
  python -m pip install ruff==0.17.1
  ruff check .
  ruff format --check .
  ```

- A contribution is made under the project's license (section 5 of the Apache License 2.0).

**What may go into the project.**
- Only material you have the right to share. Do not add confidential data, or figures from an employer or a vendor, without their permission.
- Every hardware value carries its source and its provenance label. A guess is labeled "assumed".
- Code taken from another project must have a compatible license, such as MIT, BSD or Apache 2.0. Keep its copyright and license notices.

**Names.** MLPerf is a trademark of MLCommons. This project is not part of MLCommons and is not endorsed by it. Its results are not MLPerf results.

**Security.** Do not report a security problem in a public issue. A private contact will be named before the first release.

## Quality checks

On every push to `main` and every pull request, CI runs `ruff`, a Python linter and formatter. It checks the lint rules and the formatting. The settings are in [ruff.toml](ruff.toml), and the workflow is in [.github/workflows/lint.yml](.github/workflows/lint.yml).
