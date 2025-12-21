---
title: "2022 T.J. Hockenson Bobblehead - Stadium Giveaway"
date: 2025-12-16
categories:
  - collection
  - detroit-lions
tags:
  - lions
  - nfl
  - stadium-giveaway
  - tj-hockenson
  - bobblehead
excerpt: "Detailed analysis and market research for the 2022 T.J. Hockenson stadium giveaway bobblehead"
permalink: /collection/detroit-lions/tj-hockenson-bobblehead/
classes: wide
---

## 2022 T.J. Hockenson Bobblehead

### Overview

| Attribute | Details |
|-----------|---------|
| Year | 2022 |
| Player | T.J. Hockenson (#88) |
| Item Type | Stadium Giveaway |
| Distribution | Given to the first 25,000 fans in attendance |
| Team | Detroit Lions |

This bobblehead was a stadium giveaway promotional item distributed to the first 25,000 fans who attended a Detroit Lions game during the 2022 season. T.J. Hockenson was the Lions' starting tight end before being traded to the Minnesota Vikings mid-season in 2022, adding a unique historical context to this collectible.

**Historical Note:** T.J. Hockenson was traded from the Detroit Lions to the Minnesota Vikings on November 1, 2022, partway through the season in which this bobblehead was distributed. This makes the item particularly interesting as a historical snapshot of the Lions roster before the trade.

---

## Images

### Boxed & Unboxed Item

![tj-hockenson]({{ site.baseurl }}/assets/images/lions/tj-hockenson-boxed.jpg)

---

{% assign item_data = site.data.bobbleheads.detroit-lions.tj-hockenson %}

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
| {{ analysis.dateChecked }} | {% if analysis.lastSoldPrice %}${{ analysis.lastSoldPrice }}{% else %}N/A{% endif %} | ${{ analysis.marketValue }} | {{ analysis.historicalSellThrough }} | {{ analysis.numberOfActiveListings }}{% if analysis.numberOfActiveListingsNote %} ({{ analysis.numberOfActiveListingsNote }}){% endif %} | ${{ analysis.currentAskingPrice }} |
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
