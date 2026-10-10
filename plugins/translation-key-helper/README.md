# Translation Key Helper

A Codex skill plugin for matching design screenshots, documents, and Chinese UI copy against the live Kuril i18n library.

## Workflow

1. Read the design or document and check the live library for exact and near-duplicate entries.
2. Present reusable keys, missing copy, and unresolved items. Wait for the user's first confirmation of reuse choices and scope.
3. Propose only the approved missing keys, with Chinese, English, Thai, placeholder contracts, and classification evidence from actual neighboring entries.
4. Wait for the user's second confirmation of the exact write and release set.
5. Recheck conflicts, save approved entries, read back every language value, and release translations. Report saved and released results separately.

Kuril remains read-only until the second confirmation. Approval to update this local skill does not authorize online changes. Reuse never implies permission to overwrite existing entries. If release exposes unrelated pending changes, confirm that additional scope first; honor explicit save-only requests.

## Classification

Kuril mixes business directories, shared UI categories, and feature groups. Determine placement from the design's purpose and verified neighboring entries, rather than routing solely by a word such as “button” or “title.” The bundled classification reference contains observed examples and their limits; it is not an official exhaustive taxonomy.

Use the live library as the source of truth. The bundled catalog is historical and partial. Preserve existing placeholder contracts when reusing entries; newly proposed copy uses the user's `{n}` convention unless specified otherwise.

## Files

- `skills/translation-key-helper/SKILL.md`: workflow and approval boundaries.
- `skills/translation-key-helper/references/classification-rules.md`: observed classification patterns and examples.
- `skills/translation-key-helper/references/key-catalog.md`: partial historical catalog.
- `skills/translation-key-helper/references/translation-glossary.md`: established terminology.

No website tokens, refresh tokens, or credentials are bundled. A separately authenticated browser or supported connector/API is required to access Kuril; this plugin does not itself provide an authenticated connector.

## Development

Update the skill and relevant references together. Keep versions in `plugin.json` and `.codex-plugin/plugin.json` aligned before tagging a release.
