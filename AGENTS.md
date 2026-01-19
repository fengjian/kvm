# Repository Guidelines

## Project Structure & Module Organization
- `arch/`, `drivers/`, `fs/`, `mm/`, `net/`, `kernel/`, `lib/`, `sound/`, `virt/` contain architecture- and subsystem-specific source.
- `include/` holds exported and internal headers.
- `Documentation/` is the canonical developer/user reference; start with `Documentation/admin-guide/README.rst`.
- `tools/` and `scripts/` provide build, testing, and analysis utilities (e.g., `tools/testing/selftests/`).
- Top-level `Makefile`, `Kconfig`, and `Kbuild` drive configuration and builds.

## Build, Test, and Development Commands
- `make menuconfig` or `make defconfig`: configure the kernel (see `arch/<ARCH>/configs/`).
- `make -j$(nproc)`: build the kernel and modules in-tree.
- `make O=/path/to/out ...`: build in a separate output directory.
- `make modules_install install`: install modules and kernel (requires root).
- `make htmldocs` or `make pdfdocs`: build documentation.
- `make mrproper`: clean tree and reset generated files.

## Coding Style & Naming Conventions
- Follow `Documentation/process/coding-style.rst`.
- Use tabs for indentation (8 columns), keep lines within 80 columns.
- K&R braces for control blocks; function opening brace on its own line.
- Prefer existing subsystem naming patterns; avoid introducing new top-level directories.
- Run style checks with `scripts/checkpatch.pl -f path/to/file.c` when practical.

## Testing Guidelines
- Kselftest lives in `tools/testing/selftests/`.
- Build: `make -C tools/testing/selftests`.
- Run: `make -C tools/testing/selftests run_tests` (some tests require root).
- Full build+run: `make kselftest` or limit with `TARGETS=ptrace`.

## Commit & Pull Request Guidelines
- Use kernel-style subjects: `subsystem: short summary` in imperative mood.
- Wrap commit message bodies at 75 columns and include rationale + impact.
- Include `Signed-off-by:` per the Developer Certificate of Origin; add `Fixes:` when applicable.
- Use `MAINTAINERS` to find the correct subsystem and submission path; patches are typically emailed rather than PRs. If using a PR workflow downstream, include a clear description, test results, and links to issues or discussions.

## Security & Configuration Tips
- Check `Documentation/process/changes.rst` for toolchain requirements.
- Prefer out-of-tree builds (`O=...`) to keep the source tree clean.
