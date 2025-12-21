---
title: "2024 Jahmyr Gibbs Bobblehead - Stadium Giveaway"
date: 2025-12-16
categories:
  - collection
  - detroit-lions
tags:
  - lions
  - nfl
  - stadium-giveaway
  - jahmyr-gibbs
  - bobblehead
excerpt: "Detailed analysis and market research for the 2024 Jahmyr Gibbs stadium giveaway bobblehead"
permalink: /collection/detroit-lions/jahmyr-gibbs-bobblehead/
classes: wide
---

## 2024 Jahmyr Gibbs Bobblehead

### Overview

| Attribute | Details |
|-----------|---------|
| Year | 2024 |
| Player | Jahmyr Gibbs (#26) |
| Item Type | Stadium Giveaway |
| Distribution | Given to the first 25,000 fans in attendance |
| Team | Detroit Lions |

This bobblehead was a stadium giveaway promotional item distributed to the first 25,000 fans who attended a Detroit Lions game during the 2024 season. Jahmyr Gibbs, the Lions' dynamic running back, has quickly become a fan favorite, making this collectible highly sought after in the secondary market.

---

## Images

### Boxed & Unboxed Item

![jahmyr-gibbs]({{ site.baseurl }}/assets/images/lions/jahmyr-gibbs-boxed.jpg)

---

{% assign item_data = site.data.bobbleheads.detroit-lions.jahmyr-gibbs %}

## Position Analysis

| Date Checked | Cost Basis | Value | Realized Profits | ROI | Post Fee ROI |
|--------------|------------|-------|------------------|-----|--------------|
{%- for position in item_data.positionAnalysis %}
| {{ position.dateChecked }} | ${{ position.costBasis }} | ${{ position.value }} | ${{ position.realizedProfits }} | {{ position.roi }}% | {{ position.postFeeRoi }}% |
{%- endfor %}

---

## Current Inventory

| Date | Quantity | Condition | Current Value Per Unit |
|------|----------|-----------|------------------------|
{%- for inventory in item_data.currentInventory %}
| {{ inventory.date }} | {{ inventory.quantity }} | {{ inventory.condition }} | ${{ inventory.currentValuePerUnit }} |
{%- endfor %}
{%- if item_data.currentInventory.size == 0 %}
| | | | *No items in inventory* |
{%- endif %}

---

## Market Research

**eBay Research Links:**
- [Historical Sales Data]({{ item_data.marketResearch.ebayMarketAnalysis[0].historicalDataLink }})
- [Current Active Listings]({{ item_data.marketResearch.ebayMarketAnalysis[0].activeListingsLink }})

### eBay Market Analysis

| Date Checked | Last Sold Price | Market Value | Historical Sell Through | Active Listings | Asking Price |
|--------------|-----------------|--------------|------------------------|-----------------|--------------|
{%- for analysis in item_data.marketResearch.ebayMarketAnalysis %}
| {{ analysis.dateChecked }} | ${{ analysis.lastSoldPrice }} | ${{ analysis.marketValue }} | {{ analysis.historicalSellThrough }} | {{ analysis.numberOfActiveListings }} | ${{ analysis.currentAskingPrice }}{% if analysis.currentAskingPriceNote %} ({{ analysis.currentAskingPriceNote }}){% endif %} |
{%- endfor %}

---

## Purchase History

| Date | Price | Source | Quantity | Condition | Status | Notes |
|------|-------|--------|----------|-----------|--------|-------|
{%- for purchase in item_data.purchaseHistory %}
| {{ purchase.datePurchased }} | ${{ purchase.purchasePrice }} | [{{ purchase.source }}](/bobbleheads/purchases/season-ticket-holder-buyout/) | {{ purchase.quantity }} | {{ purchase.condition }} | {{ purchase.status }} | {{ purchase.notes }} |
{%- endfor %}
| **TOTAL** | **${{ item_data.roiAnalysis.totalPurchaseAmount }}** | | **{{ item_data.purchaseHistory | size }}** | | | |

---

## Sale History

| Date Sold | Sale Price | Platform | Buyer | Quantity | Profit/Loss | Notes |
|-----------|------------|----------|-------|----------|-------------|-------|
{%- for sale in item_data.saleHistory %}
| {{ sale.dateSold }} | ${{ sale.salePrice }} | {{ sale.platform }} | {{ sale.buyer }} | {{ sale.quantity }} | ${{ sale.profitLoss }} | {{ sale.notes }} |
{%- endfor %}
{%- if item_data.saleHistory.size == 0 %}
| | | | | | | *No sales yet* |
{%- endif %}

---

[Back to Detroit Lions Collection Summary](/bobbleheads/collection/detroit-lions/collection-summary/)
