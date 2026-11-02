# Build journal

## 2026-11-02: Phase 0 finished

**Problem 1: Ubuntu would not start.** WSL error E_ACCESSDENIED on the disk file.
The disk file, the D: drive and the permissions were all fine. Restarting the
Windows virtual machine service (`vmcompute`) cleared it.

**Problem 2: `docker` not found inside Ubuntu.** Restarting that service had
switched off Docker Desktop's WSL integration. Re-enabled it in Docker Desktop
settings under Resources, WSL integration.

**Problem 3: gitleaks would not build.** pre-commit compiles gitleaks with Go,
which fires many parallel downloads. They timed out (TLS handshake timeout) even
though a single download worked. Fix: download the ready-made gitleaks binary
(v8.21.2) into ~/.local/bin and run it as a local pre-commit hook.
On a new machine, install that binary before running `pre-commit install`.

**Verified:** the secret scanner refuses a commit containing a fake GitHub token.
Note: gitleaks ignores keys containing the word EXAMPLE, so the usual AWS
example key is NOT a valid test.
