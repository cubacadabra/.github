## Cubacadabra documentation authority

- Keep hand-written, cross-repository Cubacadabra product documentation in the
  sibling `docs` repository. Read and update its canonical contract whenever
  a public or cross-repository contract changes, in the same piece of work.
- Do not create competing hand-written contract pages in an implementation
  repository's `docs/` directory. Keep local build, test, release, and
  implementation-specific instructions in its README or CONTRIBUTING file;
  generated references stay with their generators, and executable fixtures
  stay under tests.
- Do not delete or empty existing sibling `docs/` directories until the
  central source-disposition ledger is complete and the owner explicitly
  authorizes source cleanup.
