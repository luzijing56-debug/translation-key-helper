---
name: translation-key-helper
description: Generate and review Kuril i18n keys from Chinese copy, screenshots, or UI context. Automatically infer the UI type and product module, produce a concise key plus English and Thai translations, preserve the project's {n} placeholder, and flag likely duplicates or ambiguity.
---

# Translation Key Helper

Use this skill whenever the user asks to create, name, translate, classify, or review a Kuril translation key. The user may provide only Chinese copy, copy plus a usage description, or a screenshot.

## Goal

Return a practical result the user can paste into the i18n website:

```text
类型：Button
Key：Button.QuickPricing
中文：快速定价
英文：Quick Pricing
泰文：<concise Thai translation>
占位符检查：通过
```

Keep the response compact. If the user asks only for an English translation, give only the translation. If they ask for a key, include the key and English; include Thai unless they explicitly ask for a single language.

## Infer the UI type

Use evidence in this order:

1. Screenshot location and visual treatment.
2. The user's stated usage, such as “按钮”, “标题”, “toast”, “tips”, “占位符”, “tag”, or “空态”.
3. Wording and interaction cues.

Classify common cases as follows:

- A visible action control or imperative action: `Button`.
- A transient success, error, or validation message: `Toast`.
- Persistent guidance or explanatory copy: `Tips`.
- A short state or badge: `Tag`.
- Input hint text: `Placeholder`.
- No-data or no-result state: `Empty`.
- A page, section, field, or explanatory title: use the relevant business module path, usually `09_Product.Listing` for listing flows.

If the screenshot and wording disagree, prefer the screenshot and mention the inferred type briefly. If ambiguity would change the namespace, provide the best guess and one alternative instead of blocking the user.

## Infer the key path

Use the existing project conventions:

- Generic UI types use top-level namespaces: `Button.X`, `Toast.X`, `Tips.X`, `Tag.X`, `Empty.X`, `Placeholder.X`.
- Business copy uses the numbered module path, for example `09_Product.Listing.X`, `09_Product.InstantBuy.X`, or `09_Product.Auction.X`.
- Use `PascalCase`, no spaces, and the shortest name that remains unambiguous.
- Prefer the existing module and folder pattern over inventing a new namespace.
- For listing-related copy, do not automatically add an `Empty` segment; check the established project pattern and the UI context first.

## Translation rules

- Always preserve the project placeholder exactly as `{n}`. Never introduce `{name}`, `{total}`, or translated placeholder names.
- Keep `{n}` in every language that uses the value.
- English should be concise and fit the UI type: action labels are short, Toasts are direct, and Tips are natural sentences.
- Thai should be natural and concise for UI space, not a word-for-word machine translation.
- Use the glossary in [references/translation-glossary.md](references/translation-glossary.md) for established terminology.
- When a term has a domain-specific meaning, prefer the project's established translation over a generic dictionary translation. For example, collectible-card “存世量” is `Population`.

## Duplicate and consistency checks

Before proposing a new key, compare it with the known catalog in [references/key-catalog.md](references/key-catalog.md). Treat that catalog as a partial snapshot, not a complete source of truth. If a matching key exists, recommend reusing it. If a near-duplicate exists, call it out.

Check that:

- The key does not duplicate an existing key.
- All language values contain the same number of `{n}` placeholders.
- The key namespace matches the inferred UI type.
- The English meaning matches the Chinese meaning and the UI context.

## Output behavior

For ordinary requests, output only the inferred type, key, English, and Thai. Include Chinese only when the user supplied a phrase that needs confirmation. Add a one-line note when an existing key or ambiguity matters.

Examples:

Input: `批量设置`

```text
类型：Button
Key：Button.BulkSettings
英文：Bulk Settings
泰文：การตั้งค่าแบบกลุ่ม
```

Input: `页面数据不完整，请退出重进 toast`

```text
类型：Toast
Key：Toast.IncompletePageData
英文：Page data is incomplete. Please exit and reopen.
泰文：ข้อมูลหน้าไม่ครบถ้วน โปรดออกแล้วเปิดใหม่
```

## Website integration boundary

This skill generates and reviews output but does not log in to or mutate the translation website by default. If a live key export or API is supplied, use it read-only for duplicate checks. Do not expose or store login tokens in the skill or references. Any website write should require an explicit user request at the time of the action.
