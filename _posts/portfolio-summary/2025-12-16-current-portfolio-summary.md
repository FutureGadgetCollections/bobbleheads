---
title: "Current Portfolio Summary"
date: 2025-12-16
categories:
  - portfolio-summary
tags:
  - portfolio
  - roi
  - analysis
excerpt: "Overall portfolio performance and valuation summary"
permalink: /portfolio-summary/current/
classes: wide
---

## Portfolio Overview

{% assign portfolio_data = site.data.portfolio.summary %}

### Portfolio Metrics

| Date | Cost Basis | Market Value | Firesale Value (85%) | ROI | Fee Adjusted ROI | YTD Realized Profits |
|------|------------|--------------|----------------------|-----|------------------|----------------------|
{%- for metric in portfolio_data.portfolioMetrics %}
| {{ metric.date }} | ${{ metric.costBasis }} | ${{ metric.marketValue }} | ${{ metric.firesaleValue }} | {{ metric.roi }}% | {{ metric.feeAdjustedRoi }}% | ${{ metric.ytdRealizedProfits }} |
{%- endfor %}

---

[View Detailed Collection Summaries](/bobbleheads/collection/)
[View Purchase History](/bobbleheads/purchases/)
