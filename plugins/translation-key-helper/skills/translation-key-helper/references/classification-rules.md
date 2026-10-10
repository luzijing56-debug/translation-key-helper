# Kuril classification evidence

Observed on 2026-10-10 through read-only UI searches at https://lemon-i18n.echo.tech/projects/Kuril. The project displayed 3032 keys. These are sampled real entries, not a full export, code-usage audit, stored key-type verification, or official written classification policy. Guidance below is inferred from the samples; recheck relevant live entries for each task.

## Directory structure

Observed business roots: `01_LoginIn`, `02_VisualSearch`, `03_Islands`, `04_Local`, `05_Inbox`, `06_Me`, `07_Post`, `08_SPU`, `09_Product`, `10_Order`, `11_AfterSaleTicker`, `12_Payment`, `13_Wallet`, `14_Withdraw`.

Other roots: `Button`, `DateTimePicker`, `Empty`, `Placeholder`, `Popup`, `PriceAndStatistic`, `Tag`, `Time`, `Tips`, `Toast`, `Web`.

Product branches include `Auction`, `InstantBuy`, `Listing`, `Lottery`, `Luckybag`, `Meetup`, `Nearby`, and `Service`. `09_Product.Listing.Seller` is a further business/role grouping. `Tag.Spec` groups specification-related labels and descriptions. Preserve exact spelling and nesting. Do not assign all product copy to Listing without identifying its flow.

## Patterns and limits

| Family | Observed examples | Classification guidance |
|---|---|---|
| Button | `Button.Add`, `Button.Confirm`, `Button.AuctionBid`, `Button.AuctionSubscribed`, `Button.ByAmount`, `Button.ByRatio` | Actions, control states, and option labels; business-specific controls can also live here. |
| Toast | `Toast.AddAttribute`, `Toast.AddedSuccessfully`, `Toast.AfterSaleTicketStatus10`, `Toast.CameraPermissionDenied` | Strong precedent for validation and transient feedback. “Please select/add” alone does not imply Placeholder. |
| Placeholder | `Placeholder.EnterPrice`, `Placeholder.SearchAttributes`, `Placeholder.Select`, `Placeholder.SelectOptional`, `Placeholder.ListingTagSearch` | Primarily input hints, including feature-specific hints. Broader messages such as `Placeholder.NoListingsInYourCurrentRegion` also exist, so this is not a strict UI taxonomy. |
| Popup | `Popup.AfterSaleTicketStatusTitle1`, `Popup.AfterSaleTicketStatusContent1`, `Popup.Cancel`, `Popup.AgreeAndPay`, `Popup.AfterSaleReasonMapAUCTION10` | Dialog-related families can include titles, bodies, actions, and reason options. Popup does not mean title only. |
| Empty | `Empty.NoContent`, `Empty.NoItemsMatchYourFilters`, `Empty.FailedToLoad`, `Empty.GoExplore`, `Empty.GoRefresh` | Empty/error states and their actions may be grouped together; an imperative does not automatically require Button. |
| Tips | `Tips.GameServiceVoiceRecordHint`, `Tips.CurrencyDuplicateListing`, `Tips.StoreClosedBeforeListing`, `Tips.CurrencyAdultsOnlyTitle`, `Tips.CopyLinkFeedback` | Guidance and restrictions are common, but titles and feedback also occur. Use feature context rather than sentence length. |
| Tag | `Tag.Added`, `Tag.Default`, `Tag.GameServiceSellerAvailable`, `Tag.GameServiceVoiceUnderReview`, `Tag.Spec.AccessoriesOnly`, `Tag.Spec.AccessoriesOnlyDescription` | Labels, states, specifications, and related descriptions; not exclusively short badges. |
| Business paths | `09_Product.Listing.SelectAttributes`, `09_Product.Listing.NoSearchResults`, `09_Product.Listing.StoreClosed`, `09_Product.Listing.Seller.ApplyToAll`, `09_Product.Listing.Seller.Description`, `09_Product.Listing.Seller.CountInStock`, `09_Product.Listing.Seller.Expired` | Business groups mix roles. Preserve a suitable existing business path even when a generic UI prefix seems plausible. |
| PriceAndStatistic | `PriceAndStatistic.People`, `PriceAndStatistic.WaitingFor` | Shared quantity formats exist, but business directories also contain counts; having a number does not decide the directory. |

`Time`, `DateTimePicker`, and `Web` were observed as roots, but their contents were not sampled in this review. Inspect live neighbors before assigning keys there.

## Verified reuse distinctions

| Chinese source | Observed key(s) | Selection consideration |
|---|---|---|
| 请选择 {n} | `09_Product.Listing.SelectN`, `Toast.SelectXFormTitle` | Determine listing prompt versus validation feedback from the design or explanation. |
| 请添加{n} | `Toast.AddAttribute` | Verify that the intended interaction is validation. |
| 请选择属性 | `09_Product.Listing.SelectAttributes` | Existing business path; do not invent a Placeholder replacement. |
| 搜索无结果，换个搜索词试试！你可能还想找： | `09_Product.Listing.NoSearchResults` | Includes the suggestions lead-in. |
| 搜索无结果，换个搜索词试试！ | `Empty.NoSearchResult` | Shorter copy; not interchangeable with the longer version. |
| 确定添加 {n} | `Button.AddN`, `Button.ConfirmAdd` | Observed English differs: “Add {n}” versus “Confirm adding {n}”. Compare languages and intent; no canonical preference or code usage was verified. |
| 营业状态未开启 | `09_Product.Listing.StoreClosed` | Existing business path. |
| 你处于营业关闭状态，发布或更新挂单前，请先更改营业状态 | `Tips.StoreClosedBeforeListing` | The related title and body use different directories. |

## Naming and compatibility

PascalCase is common, but numeric legacy names and other casing exist. Preserve exact names on reuse. Extend a coherent local family for new keys rather than copying unrelated historical naming anomalies. Duplicates are not evidence that either key can be removed or that one is canonical.

The actual library is not exclusively `{n}`: `Placeholder.SearchProductInTag` uses `{tag}`, `Tips.LoginBeforeTrading` uses `{login}`, and `09_Product.Listing.Seller.ListingsFromAvgSold` uses `{n1}`/`{n2}`. Preserve existing contracts for reuse. Use the user's `{n}` convention for new copy in this workflow unless the user specifies otherwise; distinguish multiple independent values before proposing a contract.

## Decision order

Understand the design's business purpose and interaction → find exact/near matches → verify meaning, placeholders, and relevant translations → reuse when suitable → otherwise compare the closest feature family with shared categories → propose a path with real sibling examples. Mark conflicts or missing context instead of claiming universal rules. These observations guide classification, not authorization. Follow the two-confirmation workflow in SKILL.md: confirm reuse/scope first, then present new keys with translations and these classification precedents for exact write-set approval. Kuril remains read-only until that second confirmation; only approved entries may then be saved. Under the user’s updated workflow, the second review covers writing and release: verify saved entries and then release, unless the user asks to save only. Follow the release-scope checks in SKILL.md.
