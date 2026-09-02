# Contributing

Thank you for helping improve the DELPHI-to-EDM4hep tooling.

## Before you start

1. Choose the repository that owns the affected code or documentation.
2. Search its open issues and pull requests for existing work.
3. For a substantial change, open an issue before implementation so the scope,
   data requirements and validation strategy can be agreed.

Questions and proposals should include enough context to be reproducible:

- the repository and revision used;
- the DELPHI and Key4hep environments or releases;
- the input data or simulated sample, without sharing restricted data;
- the command that was run and the relevant output;
- the expected and observed behaviour.

## Pull requests

- Keep a pull request focused on one logical change.
- Explain why the change is needed and how it was tested.
- Add or update tests and documentation when behaviour changes.
- Preserve event provenance and collection semantics; call out any schema or
  physics-impacting change explicitly.
- Do not commit generated data, credentials, access tokens or restricted DELPHI
  material.
- Follow the build, formatting and test instructions in the target repository.

The project maintainers may ask for validation on representative data and Monte
Carlo samples before merging changes that affect conversion or reconstruction.

## Licensing and provenance

Only contribute material that you have the right to submit. Record the origin
and licence of vendored code, schemas, calibration material and sample data.
Each repository's own licence notice is authoritative; the absence of a licence
does not grant permission to reuse its contents.

