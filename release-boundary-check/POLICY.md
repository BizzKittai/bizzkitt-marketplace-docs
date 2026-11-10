# Version 1 policy

A saved UTF-8 JSON object, maximum 32,768 bytes. Unknown or duplicate properties and trailing JSON are rejected.

```json
{
  "version": 1,
  "allow": ["README.md", "LICENSE.txt", "lib/*.jar", "lib/*.jar!/**"],
  "deny": ["**/.env", "**/.env.*", "**/*.test.*", "**/.git/**"],
  "require": ["README.md", "LICENSE.txt", "lib/*.jar!/com/example/App.class"],
  "maxEntryBytes": 20971520
}
```

`allow` must contain at least one pattern. `deny` and `require` may be empty. Each list contains at most 50 distinct patterns, each at most 200 characters. `maxEntryBytes` is an integer from 1 to 20,971,520; it is a policy limit below the independent hard scan limits. If omitted, deny and require default to empty lists and maxEntryBytes to 20,971,520. version and nonempty allow are required.

Patterns are case-sensitive, forward-slash paths relative to the archive root. `*` matches zero or more non-slash characters; `?` one non-slash character; `**` any characters including slashes; `**/` zero or more directory prefixes. Brackets are literal, not shell character classes. Absolute paths, any `..` substring, backslashes and control characters are rejected in policy patterns. Nested paths use `outer.jar!/inner/path`. The container entry and its members need their own allowed patterns.

Every file must match allow; any matching deny wins. Every require pattern must match at least one file in a complete inspection. Directory entries do not satisfy these rules. Path safety, duplicate entry, corruption and hard resource checks are independent of the declared rules. A require match does not excuse a deny match.

Reports contain rule, archive-relative entry or pattern, explanation, status, completeness, counts and both input hashes. No input contents or absolute host input paths are included. An export is a snapshot, not a continuous monitor or trusted attestation. A user can alter exported JSON; no cryptographic report signature is claimed.
