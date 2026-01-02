---
permalink: /portfolio-summary/
title: "Portfolio Summary"
layout: archive
author_profile: false
---

<script src="https://cdnjs.cloudflare.com/ajax/libs/PapaParse/5.4.1/papaparse.min.js"></script>
<style>
  .portfolio-metrics {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 20px;
    margin: 30px 0;
  }
  .metric-card {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    padding: 25px;
    border-radius: 12px;
    color: white;
    box-shadow: 0 4px 6px rgba(0,0,0,0.1);
    text-align: center;
  }
  .metric-label {
    font-size: 14px;
    opacity: 0.9;
    margin-bottom: 10px;
    text-transform: uppercase;
    letter-spacing: 0.5px;
  }
  .metric-value {
    font-size: 32px;
    font-weight: bold;
    margin: 0;
  }
  .metric-subtext {
    font-size: 12px;
    opacity: 0.8;
    margin-top: 5px;
  }
</style>

This section showcases portfolio summary entries and analysis.

## Portfolio Evaluation

<div id="portfolio-evaluation"></div>

<script>
document.addEventListener('DOMContentLoaded', function() {
  const inventoryUrl = 'https://docs.google.com/spreadsheets/d/e/2PACX-1vTfkT65pf6IY_a1icZKFAlVGSpTWtJ7n0ebSW5F3iHgcQ7wbX75UyspePFJe-b55ws8tkW4Gz4rGUD3/pub?output=csv';
  const salesUrl = 'https://docs.google.com/spreadsheets/d/e/2PACX-1vQF_Cjn-h-NNle2OXlXlLxwNfCmt-vDHqx3hHBuUbVjszS45zLvQPpEiIkkpDhDUB3bC64-PI3_FuKd/pub?gid=0&single=true&output=csv';
  const marketValueUrl = 'https://docs.google.com/spreadsheets/d/e/2PACX-1vSQprUmzPWIKWrmDIxr8fwzH2Di-ms4RpBOUwPAeQ32LihvkxoRZEms4fucNkpgF4OzIgB8NHuurMPN/pub?gid=0&single=true&output=csv';

  let totalCostBasis = 0;
  let realizedProfits = 0;
  let currentValue = 0;

  // Fetch inventory data for cost basis
  Papa.parse(inventoryUrl, {
    download: true,
    header: true,
    skipEmptyLines: true,
    complete: function(inventoryResults) {
      if (inventoryResults.data && inventoryResults.data.length > 0) {
        inventoryResults.data.forEach(row => {
          const total = parseFloat((row['Total Investment'] || row['Total'] || '0').replace('$', '').replace(',', ''));
          totalCostBasis += total;
        });
      }

      // Fetch sales data
      Papa.parse(salesUrl, {
        download: true,
        header: true,
        skipEmptyLines: true,
        complete: function(salesResults) {
          if (salesResults.data && salesResults.data.length > 0) {
            salesResults.data.forEach(row => {
              const saleAmount = parseFloat((row['Sale Amount'] || row['Total'] || row['Amount'] || '0').replace('$', '').replace(',', ''));
              const cost = parseFloat((row['Cost'] || row['Cost Basis'] || '0').replace('$', '').replace(',', ''));
              realizedProfits += (saleAmount - cost);
            });
          }

          // Fetch market value data
          Papa.parse(marketValueUrl, {
            download: true,
            header: true,
            skipEmptyLines: true,
            complete: function(marketResults) {
              if (marketResults.data && marketResults.data.length > 0) {
                marketResults.data.forEach(row => {
                  const marketVal = parseFloat((row['Market Value'] || row['Current Value'] || '0').replace('$', '').replace(',', ''));
                  currentValue += marketVal;
                });
              }

              displayMetrics();
            },
            error: function(error) {
              console.error('Error loading market value data:', error);
              displayMetrics();
            }
          });
        },
        error: function(error) {
          console.error('Error loading sales data:', error);
          // Continue to market value even if sales fails
          Papa.parse(marketValueUrl, {
            download: true,
            header: true,
            skipEmptyLines: true,
            complete: function(marketResults) {
              if (marketResults.data && marketResults.data.length > 0) {
                marketResults.data.forEach(row => {
                  const marketVal = parseFloat((row['Market Value'] || row['Current Value'] || '0').replace('$', '').replace(',', ''));
                  currentValue += marketVal;
                });
              }
              displayMetrics();
            },
            error: function(error) {
              console.error('Error loading market value data:', error);
              displayMetrics();
            }
          });
        }
      });
    },
    error: function(error) {
      console.error('Error loading inventory data:', error);
      document.getElementById('portfolio-evaluation').innerHTML = '<p style="color: #f87171;">Error loading portfolio evaluation data. Please check the console for details.</p>';
    }
  });

  function displayMetrics() {
    // Calculate ROI
    const unrealizedGains = currentValue - totalCostBasis;
    const totalGains = unrealizedGains + realizedProfits;
    const roi = totalCostBasis > 0 ? (totalGains / totalCostBasis * 100) : 0;

    // Display results
    const html = `
      <div class="portfolio-metrics">
        <div class="metric-card">
          <div class="metric-label">Total Cost Basis</div>
          <div class="metric-value">$${totalCostBasis.toFixed(2)}</div>
          <div class="metric-subtext"><a href="https://docs.google.com/spreadsheets/d/e/2PACX-1vTfkT65pf6IY_a1icZKFAlVGSpTWtJ7n0ebSW5F3iHgcQ7wbX75UyspePFJe-b55ws8tkW4Gz4rGUD3/pubhtml" target="_blank" style="color: rgba(255,255,255,0.9); text-decoration: underline;">View source</a></div>
        </div>
        <div class="metric-card">
          <div class="metric-label">Current Value</div>
          <div class="metric-value">$${currentValue.toFixed(2)}</div>
          <div class="metric-subtext"><a href="https://docs.google.com/spreadsheets/d/e/2PACX-1vSQprUmzPWIKWrmDIxr8fwzH2Di-ms4RpBOUwPAeQ32LihvkxoRZEms4fucNkpgF4OzIgB8NHuurMPN/pubhtml" target="_blank" style="color: rgba(255,255,255,0.9); text-decoration: underline;">View source</a></div>
        </div>
        <div class="metric-card">
          <div class="metric-label">Realized Profits</div>
          <div class="metric-value">$${realizedProfits.toFixed(2)}</div>
          <div class="metric-subtext">From sales</div>
        </div>
        <div class="metric-card">
          <div class="metric-label">ROI</div>
          <div class="metric-value">${roi.toFixed(2)}%</div>
          <div class="metric-subtext">Total gains / cost basis</div>
        </div>
      </div>
      <p style="font-size: 14px; color: #666; margin-top: 20px; font-style: italic;">
        <strong>Calculation Notes:</strong><br>
        • <strong>Total Cost Basis:</strong> Sum of all "Total Investment" values from the inventory spreadsheet<br>
        • <strong>Current Value:</strong> Sum of all "Market Value" entries from the market research spreadsheet<br>
        • <strong>ROI:</strong> Calculated as [(Current Value - Cost Basis + Realized Profits) / Cost Basis] × 100
      </p>
    `;

    document.getElementById('portfolio-evaluation').innerHTML = html;
  }

});
</script>

---

## Cash Flow Analysis

The cash flow analysis tracks monthly cash flows and the current value of the collection over time.

[View Cash Flow Analysis in Google Sheets](https://docs.google.com/spreadsheets/d/e/2PACX-1vRw68_RrtyUAY2IJmBYNN9MHtp9uz2ure7AhrhodWs7TK-eJ8wmpI6pIAOxDVaR7ZQBPCzVxWjzFzxK/pubhtml?gid=0&single=true)

<iframe src="https://docs.google.com/spreadsheets/d/e/2PACX-1vRw68_RrtyUAY2IJmBYNN9MHtp9uz2ure7AhrhodWs7TK-eJ8wmpI6pIAOxDVaR7ZQBPCzVxWjzFzxK/pubhtml?gid=0&single=true&widget=true&headers=false" width="100%" height="600" frameborder="0"></iframe>

---

## Internal Rate of Return (IRR)

The IRR analysis shows the internal rate of return for the bobblehead collection investment.

[View IRR Analysis in Google Sheets](https://docs.google.com/spreadsheets/d/e/2PACX-1vRw68_RrtyUAY2IJmBYNN9MHtp9uz2ure7AhrhodWs7TK-eJ8wmpI6pIAOxDVaR7ZQBPCzVxWjzFzxK/pubhtml?gid=548434745&single=true)

<iframe src="https://docs.google.com/spreadsheets/d/e/2PACX-1vRw68_RrtyUAY2IJmBYNN9MHtp9uz2ure7AhrhodWs7TK-eJ8wmpI6pIAOxDVaR7ZQBPCzVxWjzFzxK/pubhtml?gid=548434745&single=true&widget=true&headers=false" width="100%" height="600" frameborder="0"></iframe>

---

## Portfolio Entries

{% assign portfolio_posts = site.categories.portfolio-summary %}
{% if portfolio_posts.size > 0 %}
  {% for post in portfolio_posts reversed %}
    {% include archive-single.html %}
  {% endfor %}
{% else %}
  *No portfolio summary entries yet.*
{% endif %}
