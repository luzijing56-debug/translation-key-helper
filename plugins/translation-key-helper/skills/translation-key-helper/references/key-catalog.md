# Kuril Key Catalog Snapshot

This is a partial catalog observed from the Kuril project. It is for pattern matching and duplicate warnings; the live project remains the source of truth.

## Generic namespaces

Known top-level namespaces include:

```text
Button
Tips
Toast
Tag
Empty
Placeholder
Popup
PriceAndStatistic
Time
```

## Known Button keys

```text
Button.AddMoreProducts
Button.ApplyToProducts
Button.Batch
Button.BulkPricing
Button.ByAmount
Button.ByRatio
Button.Confirm
Button.ConfirmAdd
Button.ConfirmDelete
Button.EditBundleSale
Button.EditFromImage
Button.EditIndividualItem
Button.FixedPrice
Button.GradingAgency
Button.LowestListingPrice
Button.NotSoldSeparately
Button.PriceIndividually
Button.Retry
Button.RetryRecognition
Button.SellAsBundle
```

## Known Product Listing keys

```text
09_Product.Listing.BulkPublish
09_Product.Listing.BulkReprice
09_Product.Listing.BulkSettings
09_Product.Listing.BundleDiscountSummary
09_Product.Listing.BundlePrice
09_Product.Listing.BundlePricePublishTip
09_Product.Listing.BundlePriceSuggestion
09_Product.Listing.BundleSaleTitle
09_Product.Listing.CurrentMarketDescription
09_Product.Listing.DeleteProduct
09_Product.Listing.DeleteRecognitionArea
09_Product.Listing.DescriptionRequired
09_Product.Listing.EditProduct
09_Product.Listing.GlobalMarketDescription
09_Product.Listing.GlobalTradeHistory
09_Product.Listing.IndividualPricingTip
09_Product.Listing.MarketTrendChartDescription
09_Product.Listing.NoBulkEditableAttributes
09_Product.Listing.NoConfigurableProducts
09_Product.Listing.NoPublishableItemsFound
09_Product.Listing.NoSearchResults
09_Product.Listing.PostPublishPricing
09_Product.Listing.ProductName
09_Product.Listing.ProductNamePlaceholder
09_Product.Listing.ProductTag
09_Product.Listing.QuantityForSale
09_Product.Listing.RecognitionResultCount
09_Product.Listing.SelectListingMethod
09_Product.Listing.SelectProductStyle
09_Product.Listing.SetInventory
09_Product.Listing.SetPrice
09_Product.Listing.Sold
09_Product.Listing.SoldStatus
09_Product.Listing.TradeHistoryDescription
```

## Existing naming signals

- Generic actions and controls are usually under `Button`, even when their Chinese text looks like a noun.
- Persistent explanations are usually under `Tips`.
- Listing-specific labels and descriptions are under `09_Product.Listing`.
- Existing catalog has a few near-duplicates, such as `IndividualPriceTip`/`IndividualPricingTip` and `Sold`/`SoldStatus`; warn before adding another similar key.
