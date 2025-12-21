---
title: "2023 Riley Green Bobblehead - Stadium Giveaway"
date: 2025-12-13
categories:
  - collection
  - detroit-tigers
tags:
  - tigers
  - mlb
  - stadium-giveaway
  - riley-green
  - bobblehead
excerpt: "Detailed analysis and market research for the 2023 Riley Green stadium giveaway bobblehead"
permalink: /collection/detroit-tigers/riley-green-bobblehead/
classes: wide
---

## 2023 Riley Green Bobblehead

### Overview

| Attribute | Details |
|-----------|---------|
| Year | 2023 |
| Player | Riley Green |
| Item Type | Stadium Giveaway |
| Distribution | Given to the first 15,000 fans in attendance |
| Team | Detroit Tigers |

This bobblehead was a stadium giveaway promotional item distributed to the first 15,000 fans who attended a Detroit Tigers game during the 2023 season. Riley Green, a highly-touted prospect and outfielder for the Tigers, represents the team's young core and future. Player bobbleheads for emerging stars can appreciate significantly if the player develops into a franchise cornerstone.

---

## Images

### Boxed & Unboxed Item

![riley-green]({{ site.baseurl }}/assets/images/tigers/riley-green-boxed.jpg)

---

{% assign item_data = site.data.bobbleheads.detroit-tigers.riley-green %}

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
| {{ analysis.dateChecked }} | ${{ analysis.lastSoldPrice }} | ${{ analysis.marketValue }} | {{ analysis.historicalSellThrough }} | {{ analysis.numberOfActiveListings }} | ${{ analysis.currentAskingPrice }} |
{%- endfor %}

---

## Purchase History

| Date | Price | Source | Quantity | Condition | Status | Notes |
|------|-------|--------|----------|-----------|--------|-------|
{%- for purchase in item_data.purchaseHistory %}
| {{ purchase.datePurchased }} | ${{ purchase.purchasePrice }} | [{{ purchase.source }}](/bobbleheads/purchases/snoopy-bobblehead-buyout/) | {{ purchase.quantity }} | {{ purchase.condition }} | {{ purchase.status }} | {{ purchase.notes }} |
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

[Back to Detroit Tigers Collection Summary](/bobbleheads/collection/detroit-tigers/collection-summary/)
