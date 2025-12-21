---
title: "2023 Detroit Lions Collector Coin - Season Ticket Holder Gift"
date: 2025-12-16
categories:
  - collection
  - detroit-lions
tags:
  - lions
  - nfl
  - season-ticket-holder
  - collector-coin
  - collectible
excerpt: "Detailed analysis and market research for the 2023 Detroit Lions collector coin season ticket holder gift"
permalink: /collection/detroit-lions/detroit-collector-coin/
classes: wide
---

## 2023 Detroit Lions Collector Coin

### Overview

| Attribute | Details |
|-----------|---------|
| Year | 2023 |
| Item | Detroit Lions Collector Coin |
| Item Type | Season Ticket Holder Gift |
| Distribution | Exclusive gift for Detroit Lions season ticket holders |
| Team | Detroit Lions |

This collector coin was distributed as an exclusive gift to Detroit Lions season ticket holders during the 2023 season. Season ticket holder gifts are premium items given to loyal fans as a token of appreciation for their continued support. These items are not available to the general public, making them unique collectibles with limited distribution.

---

## Images

### Item Photos

![detroit-collector-coin]({{ site.baseurl }}/assets/images/lions/detroit-collector-coin.jpg)

---

{% assign item_data = site.data.bobbleheads.detroit-lions.detroit-collector-coin %}

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
| {{ analysis.dateChecked }} | {% if analysis.lastSoldPrice %}${{ analysis.lastSoldPrice }}{% else %}N/A{% endif %} | ${{ analysis.marketValue }} | {{ analysis.historicalSellThrough }} | {{ analysis.numberOfActiveListings }} | ${{ analysis.currentAskingPrice }}{% if analysis.currentAskingPriceNote %} ({{ analysis.currentAskingPriceNote }}){% endif %} |
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
