# Public handoff security

Before publishing any handoff:

- scan for tokens, passwords, API keys, connection strings and `.env` contents;
- exclude customer PII, production records and database dumps;
- avoid private project references or infrastructure identifiers unless explicitly public;
- include only the minimum code context required for deterministic execution;
- verify that patches target code already intended for the same visibility level;
- record checksums without embedding credentials or signed URLs.

If any potentially sensitive value is found, stop publication and request review.
