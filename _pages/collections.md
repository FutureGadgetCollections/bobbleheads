---
title: "Collection Inventory"
layout: single
permalink: /collection/
author_profile: false
classes: wide
---

<script src="https://cdnjs.cloudflare.com/ajax/libs/PapaParse/5.4.1/papaparse.min.js"></script>
<style>
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
  .collection-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
    gap: 30px;
    margin-top: 30px;
  }
  .team-card {
    background: white;
    border-radius: 12px;
    overflow: hidden;
    box-shadow: 0 4px 6px rgba(0,0,0,0.1);
    transition: transform 0.3s ease, box-shadow 0.3s ease;
  }
  .team-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 8px 15px rgba(0,0,0,0.2);
  }
  .team-card-image {
    width: 100%;
    height: 200px;
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
    position: relative;
  }
  .team-card-content {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    padding: 25px;
    color: white;
  }
  .team-card-title {
    font-size: 24px;
    font-weight: bold;
    margin: 0 0 20px 0;
    color: white;
    border-bottom: 2px solid rgba(255,255,255,0.3);
    padding-bottom: 10px;
  }
  .team-card-stats {
    display: flex;
    justify-content: space-between;
    margin-bottom: 20px;
    gap: 15px;
  }
  .stat-item {
    text-align: center;
    flex: 1;
  }
  .stat-label {
    display: block;
    font-size: 12px;
    opacity: 0.9;
    margin-bottom: 5px;
    text-transform: uppercase;
    letter-spacing: 0.5px;
  }
  .stat-value {
    display: block;
    font-size: 20px;
    font-weight: bold;
  }
  .team-card-link {
    display: inline-block;
    padding: 10px 20px;
    background-color: rgba(255,255,255,0.2);
    color: white;
    text-decoration: none;
    border-radius: 6px;
    border: 2px solid rgba(255,255,255,0.3);
    transition: background-color 0.3s ease;
    font-weight: 600;
  }
  .team-card-link:hover {
    background-color: rgba(255,255,255,0.3);
    color: white;
  }
</style>

Welcome to the bobblehead collection inventory! View all teams and their current inventory status.

<div style="margin-bottom: 20px;">
  <a href="https://docs.google.com/spreadsheets/d/e/2PACX-1vTfkT65pf6IY_a1icZKFAlVGSpTWtJ7n0ebSW5F3iHgcQ7wbX75UyspePFJe-b55ws8tkW4Gz4rGUD3/pubhtml" target="_blank" class="sheets-link">View Full Inventory in Google Sheets</a>
</div>

<div id="collection-inventory" class="collection-grid">
  <p>Loading inventory data...</p>
</div>

<script>
const teamMapping = {
  'Baseball': {
    name: 'Detroit Tigers',
    slug: 'detroit-tigers',
    image: '{{ site.baseurl }}/assets/images/themes/tigers.png'
  },
  'Basketball': {
    name: 'Detroit Pistons',
    slug: 'detroit-pistons',
    image: '{{ site.baseurl }}/assets/images/themes/pistons.png'
  },
  'Football': {
    name: 'Detroit Lions',
    slug: 'detroit-lions',
    image: '{{ site.baseurl }}/assets/images/themes/lions.jpg'
  },
  'Hockey': {
    name: 'Detroit Red Wings',
    slug: 'detroit-red-wings',
    image: '{{ site.baseurl }}/assets/images/themes/red-wings.png'
  },
  'College': {
    name: 'University of Michigan',
    slug: 'university-of-michigan',
    image: '{{ site.baseurl }}/assets/images/themes/michigan.png'
  }
};

document.addEventListener('DOMContentLoaded', function() {
  const csvUrl = 'https://docs.google.com/spreadsheets/d/e/2PACX-1vTfkT65pf6IY_a1icZKFAlVGSpTWtJ7n0ebSW5F3iHgcQ7wbX75UyspePFJe-b55ws8tkW4Gz4rGUD3/pub?output=csv';

  Papa.parse(csvUrl, {
    download: true,
    header: true,
    skipEmptyLines: true,
    complete: function(results) {
      if (!results.data || results.data.length === 0) {
        document.getElementById('collection-inventory').innerHTML = '<p>No inventory data available.</p>';
        return;
      }

      const teamStats = {};

      results.data.forEach(row => {
        const sport = row.Sport;
        if (!sport || !teamMapping[sport]) return;

        if (!teamStats[sport]) {
          teamStats[sport] = {
            count: 0,
            totalValue: 0
          };
        }

        teamStats[sport].count += parseInt(row['Total Quantity'] || row.Qty || 0);
        const totalInvestment = parseFloat((row['Total Investment'] || row.Total || '0').replace('$', '').replace(',', ''));
        teamStats[sport].totalValue += totalInvestment;
      });

      // Fetch market value data
      const marketValueUrl = 'https://docs.google.com/spreadsheets/d/e/2PACX-1vSQprUmzPWIKWrmDIxr8fwzH2Di-ms4RpBOUwPAeQ32LihvkxoRZEms4fucNkpgF4OzIgB8NHuurMPN/pub?output=csv';

      Papa.parse(marketValueUrl, {
        download: true,
        header: true,
        skipEmptyLines: true,
        complete: function(marketResults) {
          const marketData = {};
          let globalLatestDate = null;

          if (marketResults.data && marketResults.data.length > 0) {
            // First pass: find the global latest date
            marketResults.data.forEach(row => {
              const dateChecked = row['Date Last Checked'] || row['Last Checked'] || row['Date Checked'] || row['Date'];
              if (dateChecked) {
                try {
                  const parsedDate = new Date(dateChecked);
                  if (!isNaN(parsedDate.getTime())) {
                    if (!globalLatestDate || parsedDate > globalLatestDate) {
                      globalLatestDate = parsedDate;
                    }
                  }
                } catch (e) {
                  console.error('Error parsing date:', dateChecked, e);
                }
              }
            });

            // Second pass: aggregate data by sport
            marketResults.data.forEach(row => {
              const sport = row.Sport;
              if (!sport || !teamMapping[sport]) return;

              if (!marketData[sport]) {
                marketData[sport] = {
                  marketValue: 0
                };
              }

              const marketVal = parseFloat((row['Market Value'] || row['Current Value'] || '0').replace('$', '').replace(',', ''));
              marketData[sport].marketValue += marketVal;
            });
          }

          // Format the global latest date
          let formattedDate = 'N/A';
          if (globalLatestDate) {
            formattedDate = globalLatestDate.toLocaleDateString('en-US', {
              year: 'numeric',
              month: 'short',
              day: 'numeric'
            });
          }

          let html = '';
          Object.keys(teamMapping).forEach(sport => {
            const team = teamMapping[sport];
            const stats = teamStats[sport] || { count: 0, totalValue: 0 };
            const market = marketData[sport] || { marketValue: 0 };

            html += `
              <div class="team-card">
                <div class="team-card-image" style="background-image: url('${team.image}')"></div>
                <div class="team-card-content">
                  <h3 class="team-card-title">${team.name}</h3>
                  <div class="team-card-stats">
                    <div class="stat-item">
                      <span class="stat-label">Items</span>
                      <span class="stat-value">${stats.count}</span>
                    </div>
                    <div class="stat-item">
                      <span class="stat-label">Cost Basis</span>
                      <span class="stat-value">$${stats.totalValue.toFixed(2)}</span>
                    </div>
                    <div class="stat-item">
                      <span class="stat-label">Market Value</span>
                      <span class="stat-value">$${market.marketValue.toFixed(2)}</span>
                    </div>
                    <div class="stat-item">
                      <span class="stat-label">Last Checked</span>
                      <span class="stat-value stat-date">${formattedDate}</span>
                    </div>
                  </div>
                  <a href="{{ site.baseurl }}/collection/${team.slug}/" class="team-card-link">View Collection →</a>
                </div>
              </div>
            `;
          });

          document.getElementById('collection-inventory').innerHTML = html;
        },
        error: function(error) {
          console.error('Error loading market value data:', error);
          // Still show inventory data even if market value fails
          let html = '';
          Object.keys(teamMapping).forEach(sport => {
            const team = teamMapping[sport];
            const stats = teamStats[sport] || { count: 0, totalValue: 0 };

            html += `
              <div class="team-card">
                <div class="team-card-image" style="background-image: url('${team.image}')"></div>
                <div class="team-card-content">
                  <h3 class="team-card-title">${team.name}</h3>
                  <div class="team-card-stats">
                    <div class="stat-item">
                      <span class="stat-label">Items</span>
                      <span class="stat-value">${stats.count}</span>
                    </div>
                    <div class="stat-item">
                      <span class="stat-label">Cost Basis</span>
                      <span class="stat-value">$${stats.totalValue.toFixed(2)}</span>
                    </div>
                  </div>
                  <a href="{{ site.baseurl }}/collection/${team.slug}/" class="team-card-link">View Collection →</a>
                </div>
              </div>
            `;
          });

          document.getElementById('collection-inventory').innerHTML = html;
        }
      });
    },
    error: function(error) {
      console.error('Error loading inventory data:', error);
      document.getElementById('collection-inventory').innerHTML = '<p>Error loading inventory data. Please try again later.</p>';
    }
  });
});
</script>
