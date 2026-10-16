# forge-spike-r1-lookalike

A test fixture for R1 test T7 in [forge-spike-r1](https://github.com/Taha7486/forge-spike-r1). It is not part of the product.

**What it does.** One manual workflow (`.github/workflows/`) builds the same thin podinfo image as the trusted repo, with `LABEL variant=lookalike`, pushes it into the trusted repo's GHCR and Docker Hub packages, and signs it keylessly with cosign v3.1.3. The signature identity is this repo's workflow, not the trusted one.

**Why.** To prove that the admission policy checks the signer's identity and not just that "some valid Sigstore signature exists". T7 result (Pass on both registries): the exact subject denied this image, and an unanchored `subjectRegExp` admitted it. The lesson is recorded in `forge-spike-r1/RESULTS.md` (T7) and ADR-001: anchor identity regexes with `^…$` and include the slash after the repo name.

**State.** Closed with R1 on 2026-10-06. The workflow logs in to Docker Hub unconditionally and the Docker Hub tokens were deleted at R1 close, so a new run fails until the secrets are recreated. Nothing here needs running again unless T7 is re-tested.
