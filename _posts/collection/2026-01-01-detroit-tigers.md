---
title: "Detroit Tigers"
layout: single
permalink: /collection/detroit-tigers/
author_profile: false
classes: wide
categories: collection
---

<script src="https://cdnjs.cloudflare.com/ajax/libs/PapaParse/5.4.1/papaparse.min.js"></script>
<style>
  .google-sheets-table {
    width: 100%;
    border-collapse: collapse;
    margin: 20px 0;
    font-size: 14px;
    box-shadow: 0 2px 3px rgba(0,0,0,0.1);
  }
  .google-sheets-table thead tr {
    background-color: #009879;
    color: #ffffff;
    text-align: left;
  }
  .google-sheets-table th,
  .google-sheets-table td {
    padding: 12px 15px;
    border: 1px solid #ddd;
  }
  .google-sheets-table tbody tr {
    border-bottom: 1px solid #dddddd;
  }
  .google-sheets-table tbody tr:nth-of-type(even) {
    background-color: #f3f3f3;
  }
  .google-sheets-table tbody tr:last-of-type {
    border-bottom: 2px solid #009879;
  }
  .google-sheets-table tbody tr:hover {
    background-color: #f1f1f1;
  }
  .sheets-link {
    display: inline-block;
    margin: 10px 0 20px 0;
    padding: 8px 16px;
    background-color: #0066cc;
    color: white;
    text-decoration: none;
    border-radius: 4px;
  }
  .sheets-link:hover {
    background-color: #0052a3;
    color: white;
  }
  .back-link {
    display: inline-block;
    margin: 10px 20px 20px 0;
    padding: 8px 16px;
    background-color: #666;
    color: white;
    text-decoration: none;
    border-radius: 4px;
  }
  .back-link:hover {
    background-color: #444;
    color: white;
  }
  .collection-overview {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    padding: 30px;
    border-radius: 12px;
    margin: 20px 0;
    color: white;
  }
  .overview-title {
    font-size: 24px;
    font-weight: bold;
    margin-bottom: 20px;
    border-bottom: 2px solid rgba(255,255,255,0.3);
    padding-bottom: 10px;
  }
  .overview-stats {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 20px;
  }
  .overview-stat {
    text-align: center;
    padding: 15px;
    background-color: rgba(255,255,255,0.1);
    border-radius: 8px;
  }
  .overview-label {
    font-size: 14px;
    opacity: 0.9;
    margin-bottom: 8px;
    text-transform: uppercase;
    letter-spacing: 0.5px;
  }
  .overview-value {
    font-size: 28px;
    font-weight: bold;
  }
  .gain-positive {
    color: #4ade80;
  }
  .gain-negative {
    color: #f87171;
  }
  .set-hero-image {
    width: 100%;
    max-height: 400px;
    object-fit: cover;
    border-radius: 12px;
    margin: 20px 0;
    box-shadow: 0 4px 8px rgba(0,0,0,0.2);
  }
</style>

<a href="{{ '/collection/' | relative_url }}" class="back-link">← Back to All Collections</a>

<div style="margin-bottom: 20px;">
  <a href="https://docs.google.com/spreadsheets/d/e/2PACX-1vTfkT65pf6IY_a1icZKFAlVGSpTWtJ7n0ebSW5F3iHgcQ7wbX75UyspePFJe-b55ws8tkW4Gz4rGUD3/pubhtml" target="_blank" class="sheets-link">View Full Inventory</a>
  <a href="https://docs.google.com/spreadsheets/d/e/2PACX-1vSQprUmzPWIKWrmDIxr8fwzH2Di-ms4RpBOUwPAeQ32LihvkxoRZEms4fucNkpgF4OzIgB8NHuurMPN/pubhtml?gid=0&single=true" target="_blank" class="sheets-link">View Market Prices</a>
</div>

<img src="{{ '/assets/images/themes/tigers.png' | relative_url }}" alt="Detroit Tigers Collection" class="set-hero-image">

<div id="collection-overview-tigers">
  <p>Loading collection overview...</p>
</div>

<div id="set-detail-tigers">
  <p>Loading inventory details...</p>
</div>

<script>
  document.addEventListener('DOMContentLoaded', function() {
    const inventoryUrl = 'https://docs.google.com/spreadsheets/d/e/2PACX-1vTfkT65pf6IY_a1icZKFAlVGSpTWtJ7n0ebSW5F3iHgcQ7wbX75UyspePFJe-b55ws8tkW4Gz4rGUD3/pub?output=csv';
    const marketValueUrl = 'https://docs.google.com/spreadsheets/d/e/2PACX-1vSQprUmzPWIKWrmDIxr8fwzH2Di-ms4RpBOUwPAeQ32LihvkxoRZEms4fucNkpgF4OzIgB8NHuurMPN/pub?gid=0&single=true&output=csv';

    const overviewContainer = document.getElementById('collection-overview-tigers');
    if (overviewContainer) {
      let costBasis = 0;
      let currentValue = 0;

      Papa.parse(inventoryUrl, {
        download: true,
        header: true,
        skipEmptyLines: true,
        complete: function(inventoryResults) {
          if (inventoryResults.data && inventoryResults.data.length > 0) {
            inventoryResults.data.forEach(row => {
              if (row.Sport === 'Baseball') {
                const total = parseFloat((row['Total Investment'] || row['Total'] || '0').replace('$', '').replace(',', ''));
                costBasis += total;
              }
            });
          }

          Papa.parse(marketValueUrl, {
            download: true,
            header: true,
            skipEmptyLines: true,
            complete: function(marketResults) {
              if (marketResults.data && marketResults.data.length > 0) {
                marketResults.data.forEach(row => {
                  if (row.Sport === 'Baseball' || row.Team === 'Detroit Tigers') {
                    const marketVal = parseFloat((row['Market Value'] || row['Current Value'] || row['Value'] || '0').replace('$', '').replace(',', ''));
                    currentValue += marketVal;
                  }
                });
              }

              const gain = currentValue - costBasis;
              const gainPercent = costBasis > 0 ? (gain / costBasis * 100) : 0;
              const gainClass = gain >= 0 ? 'gain-positive' : 'gain-negative';
              const gainSign = gain >= 0 ? '+' : '';

              overviewContainer.innerHTML = `
                <div class="collection-overview">
                  <div class="overview-title">Detroit Tigers Collection Overview</div>
                  <div class="overview-stats">
                    <div class="overview-stat">
                      <div class="overview-label">Total Cost Basis</div>
                      <div class="overview-value">$${costBasis.toFixed(2)}</div>
                    </div>
                    <div class="overview-stat">
                      <div class="overview-label">Current Value</div>
                      <div class="overview-value">$${currentValue.toFixed(2)}</div>
                    </div>
                    <div class="overview-stat">
                      <div class="overview-label">Total Gain</div>
                      <div class="overview-value ${gainClass}">${gainSign}$${Math.abs(gain).toFixed(2)}</div>
                    </div>
                    <div class="overview-stat">
                      <div class="overview-label">Percentage Gain</div>
                      <div class="overview-value ${gainClass}">${gainSign}${gainPercent.toFixed(2)}%</div>
                    </div>
                  </div>
                </div>
              `;
            },
            error: function(error) {
              console.error('Error loading market value data:', error);
            }
          });
        },
        error: function(error) {
          console.error('Error loading inventory data:', error);
          overviewContainer.innerHTML = '<p>Error loading collection overview.</p>';
        }
      });
    }

    const detailContainer = document.getElementById('set-detail-tigers');
    if (detailContainer) {
      Papa.parse(inventoryUrl, {
        download: true,
        header: true,
        skipEmptyLines: true,
        complete: function(results) {
          if (!results.data || results.data.length === 0) {
            detailContainer.innerHTML = '<p>No inventory data available.</p>';
            return;
          }

          const filteredData = results.data.filter(row => row.Sport === 'Baseball');

          if (filteredData.length === 0) {
            detailContainer.innerHTML = '<p>No Detroit Tigers items in inventory.</p>';
            return;
          }

          const headers = results.meta.fields;
          let tableHtml = '<h2>Inventory Details</h2><table class="google-sheets-table"><thead><tr>';

          headers.forEach(header => {
            tableHtml += `<th>${header}</th>`;
          });
          tableHtml += '</tr></thead><tbody>';

          filteredData.forEach(row => {
            tableHtml += '<tr>';
            headers.forEach(header => {
              const value = row[header] || '';
              tableHtml += `<td>${value}</td>`;
            });
            tableHtml += '</tr>';
          });

          tableHtml += '</tbody></table>';
          detailContainer.innerHTML = tableHtml;
        },
        error: function(error) {
          console.error('Error loading inventory details:', error);
          detailContainer.innerHTML = '<p>Error loading inventory details.</p>';
        }
      });
    }
  });
</script>
