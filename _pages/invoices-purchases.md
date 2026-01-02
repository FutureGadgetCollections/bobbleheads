---
title: "Purchases"
layout: archive
permalink: /invoices/purchases/
author_profile: false
classes: wide
---

All purchase transactions for the bobblehead collection.

[View Purchases in Google Sheets](https://docs.google.com/spreadsheets/d/e/2PACX-1vTwQkcL471u0DmAWslgX1m4HK0wf1jqKp7d6CD9s80O2hw-a8VRIH87LD16HivOg46gQzsQhrDZXhrM/pubhtml?gid=0&single=true)

<link rel="stylesheet" type="text/css" href="https://cdn.datatables.net/1.13.7/css/jquery.dataTables.min.css">
<script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
<script src="https://cdn.datatables.net/1.13.7/js/jquery.dataTables.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/PapaParse/5.4.1/papaparse.min.js"></script>

<div id="purchases-table-container">
  <p>Loading purchase data...</p>
</div>

<script>
$(document).ready(function() {
  const csvUrl = 'https://docs.google.com/spreadsheets/d/e/2PACX-1vTwQkcL471u0DmAWslgX1m4HK0wf1jqKp7d6CD9s80O2hw-a8VRIH87LD16HivOg46gQzsQhrDZXhrM/pub?gid=0&single=true&output=csv';

  Papa.parse(csvUrl, {
    download: true,
    header: true,
    skipEmptyLines: true,
    complete: function(results) {
      if (!results.data || results.data.length === 0) {
        $('#purchases-table-container').html('<p>No purchase data available.</p>');
        return;
      }

      const headers = results.meta.fields;
      let tableHtml = '<table id="purchases-table" class="display" style="width:100%"><thead><tr>';

      headers.forEach(header => {
        tableHtml += '<th>' + header + '</th>';
      });
      tableHtml += '</tr></thead><tbody>';

      results.data.forEach(row => {
        tableHtml += '<tr>';
        headers.forEach(header => {
          const value = row[header] || '';
          tableHtml += '<td>' + value + '</td>';
        });
        tableHtml += '</tr>';
      });

      tableHtml += '</tbody></table>';
      $('#purchases-table-container').html(tableHtml);

      $('#purchases-table').DataTable({
        pageLength: 25,
        order: [[0, 'desc']],
        responsive: true
      });
    },
    error: function(error) {
      console.error('Error loading purchase data:', error);
      $('#purchases-table-container').html('<p>Error loading purchase data. Please check your browser console for details.</p>');
    }
  });
});
</script>
