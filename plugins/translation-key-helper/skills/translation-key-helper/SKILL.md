---
name: translation-key-helper
description: Match Kuril design or document copy against the live i18n library, obtain reuse confirmation, propose missing keys with translations and classification evidence, then write, verify, and release the exact entries the user approves in a second review.
---

# Translation Key Helper

Use for Kuril i18n key selection, naming, translation, classification, or review from design screenshots, Chinese copy, or usage descriptions. A request for translation alone needs only the requested translation, not a key workflow.

## Required workflow with two user confirmations

The user requires two separate review stages for each batch. Updating this skill or enabling write capability is not authorization to write any pending or future keys. Keep the current batch and stage clear across turns; preserve approvals already given for the unchanged scope.

### 1. Understand and check duplicates (read-only)

Read the supplied design, document, or explanation. Extract each copy item, module, placement, trigger, placeholders, and any removed/out-of-scope/uncertain annotations. Distinguish “not yet integrated in code” from “absent from the library.” Do not modify the source document.

Check the live Kuril project at `https://lemon-i18n.echo.tech/projects/Kuril`, an existing authenticated tab, or a current user-provided export/API. Search exact Chinese, distinctive fragments, relevant English/key terms, and near-duplicates. Preserve existing placeholder contracts; `{n}` can be an additional search normalization for design annotations. Wait for results to settle. Read full key paths and relevant language values before describing them as verified. Do not claim a complete audit from partial searches.

Return a first-review table with copy/context, verified reusable key(s), meaningful differences, and status: reusable / no suitable entry found / needs clarification / excluded. Do not finalize new key names or translations yet. If no suitable entry is found, report the search scope rather than claiming universal absence.

**Confirmation 1 — reuse and scope:** Ask the user to confirm the reuse choices and which missing items should proceed to key design. Wait for that answer before designing the missing keys. Explain briefly that this is the first review required by this skill's user-defined workflow, and link this SKILL.md when requesting confirmation. Generic praise, silence, or permission to update the skill is not confirmation of this batch. A clear approval of the displayed batch is sufficient; do not ask again for unchanged approved items.

### 2. Prepare missing keys and classification evidence (still read-only)

After confirmation 1, design only the approved missing items. Follow the classification logic below and inspect actual neighboring entries. Reuse approved existing keys unchanged. Resolve essential ambiguities before putting an item in the write set; excluded/unresolved items remain outside it.

Present a concrete second-review table with a stable row identifier, operation (normally create), complete proposed key and directory, Chinese, English, Thai, placeholder contract, and classification rationale citing one or two inspected existing full key paths. Distinguish UI role from stored key-type metadata. Inspect the platform's actual fields read-only if necessary so the proposal is complete; never infer a stored type from a prefix. If proposing an explicit update to an existing entry, include exact before/after values and scope; reuse by itself does not authorize such an update.

**Confirmation 2 — exact write set:** Ask the user to review the full proposal, including classification evidence, and confirm the rows to write to Kuril and release after verification. State explicitly in this review that approval includes writing and releasing. Explain that this is the second review required by this skill's user-defined workflow, with a link to this SKILL.md. Wait for explicit approval of this concrete write set. Confirmation 1 is not write approval. If the user requests revisions, present the revised values and obtain confirmation of those revisions before writing; previously approved unchanged rows need no repeated approval. A partial approval applies only to the named rows.

### 3. Write the approved entries, verify, and release

After confirmation 2, use an available supported connector/API or browser tool to write the exact approved entries to Kuril. Proceed without a third confirmation for unchanged approved content, subject to actual tool permission requirements. Do not add unreviewed AI translations, alter approved copy, or expand the batch during execution.

Immediately before creating an entry, recheck its exact key and relevant duplicates. If an identical entry now exists with all approved values, skip creation and report it. If it exists with different values, do not overwrite: show the conflict for review. If a newly discovered equivalent changes the reuse decision, return that item to review rather than silently substituting or duplicating it.

The user wants release included in this workflow. After saving and verifying all approved entries, execute Release Translations without requesting a third confirmation. If the user explicitly requests save-only, do not release. Inspect any displayed release scope or pending-change summary: if it reveals unrelated unpublished changes outside the approved batch, pause for scope confirmation rather than silently including them. If the tool only offers a project-level release, accurately report that scope; do not claim a single-key release. Do not deploy application code, write back to the source document, delete keys, rename existing keys, or reorganize the library without a separate specific request. The default write set is newly approved keys and their approved language values.

Read back each saved full path and all approved language values, preserving placeholders, punctuation, spaces, and line breaks. A click or transient success toast alone is not full verification. Follow the browser tool's screenshot proof requirements for changes. Report created / updated (if explicitly approved) / already existed / failed / unverified entries accurately. On partial failure, preserve the successful result list and recheck remote state before retrying only unfinished entries; never blindly replay the full batch. Stop on access/validation conflicts that require new user input without widening permissions or changing approved values. After successful readback, release and verify the platform release result. Save screenshot evidence when using browser tools. Distinguish saved from released in the result; if release fails, report saved-but-unreleased and do not recreate the keys.

## Classification decision logic

Read [Kuril classification evidence and decision rules](references/classification-rules.md) when assigning or reviewing keys. It records observed examples and their limits, not an official universal taxonomy. Recheck the relevant examples in the current library.

Keep three things separate: **UI role**, **key directory**, and **stored key-type metadata**. Do not infer the third from either of the first two. Kuril mixes business modules, reusable UI categories, and feature-specific groups; prefix does not uniquely identify a control type.

Choose in this order:

1. Follow the user's explicit project convention or an applicable verified written convention.
2. Reuse a live entry whose meaning, interaction context, translations, and placeholder contract fit. An identical Chinese string alone is insufficient.
3. For a new entry, identify the design's business module and feature. Search both that feature's existing family and the relevant shared namespace. Prefer the closest coherent family by business purpose, role, and sibling naming. A business-specific label can be in a shared namespace (`Button.AuctionBid`), and an action can be in a business directory (`09_Product.Listing.Seller.ApplyToAll`). Neither business words nor an action verb decide the prefix alone.
4. Use repeated comparable entries as the default pattern. Treat isolated outliers, duplicate keys, numeric legacy names, and unusual casing as compatibility evidence, not a rule to extend everywhere. Preserve existing paths; do not propose renaming them during ordinary key assignment.
5. If patterns conflict, use the user's screenshot/explanation to choose the closest family. Where that evidence cannot discriminate, give the concrete alternatives and ask the one missing context question. Do not fabricate a canonical key or assert the library is consistent.

For each proposed new path, retain the full paths of one or two inspected precedents and explain the choice briefly. Do not generate generic UI prefixes first and look for justification afterward.

## Evidence and unavailable access

The [catalog snapshot](references/key-catalog.md) is a partial historical aid for locating candidates, not the current library. It cannot prove that a key is absent, validate its source text, or substitute for the required lookup. Current library evidence takes priority over the snapshot and generic naming habits.

If the library is inaccessible, state the concrete blocker and request login or an export. Continue analyzing the supplied design, but do not present definitive key assignments or assert “not found.” If the user explicitly requests provisional suggestions without access, label every such suggestion as unverified.

## Translation and placeholder checks

- Use [the glossary](references/translation-glossary.md) and the actual project's terminology; collectible-card “存世量” is `Population`.
- For newly proposed copy in this workflow, use `{n}` as requested and normalize design annotations such as `{属性名}` or `N` explicitly. For reuse, preserve the existing entry’s exact placeholder names and count: the live library also contains `{tag}`, `{login}`, and `{n1}`/`{n2}`. Flag incompatible contracts instead of silently rewriting them. Multiple distinct variables require checking the relevant existing family before proposing their contract.
- English and Thai should fit the UI role and space. Prefer established library translations for reused entries. Flag translation mismatches without silently replacing library values.

## Output and authorization boundary

Use the first-review and second-review tables defined above. Classification evidence is required for new keys in the second review, not optional commentary. Keep unresolved items separate from the proposed write set. Pure translation requests can remain concise and do not trigger website writes.

Kuril is read-only until confirmation 2 for the current concrete write set. The user's permission to edit this local skill does not grant website write permission. Respect any later per-task read-only restriction. Skill/reference maintenance must not silently add, update, translate, or release online entries.

Use credentials only for the intended site's normal authentication. Do not store or reproduce tokens, refresh tokens, or credential-bearing URLs in skill files, references, artifacts, or answers. Store only the clean project URL.
