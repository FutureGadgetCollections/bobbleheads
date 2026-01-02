---
title: "Sales"
layout: archive
permalink: /invoices/sales/
author_profile: false
classes: wide
---

All sale transactions for the bobblehead collection.

[View Sales in Google Sheets](https://docs.google.com/spreadsheets/d/e/2PACX-1vQF_Cjn-h-NNle2OXlXlLxwNfCmt-vDHqx3hHBuUbVjszS45zLvQPpEiIkkpDhDUB3bC64-PI3_FuKd/pubhtml)

<link rel="stylesheet" type="text/css" href="https://cdn.datatables.net/1.13.7/css/jquery.dataTables.min.css">
<script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
<script src="https://cdn.datatables.net/1.13.7/js/jquery.dataTables.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/PapaParse/5.4.1/papaparse.min.js"></script>

<div id="sales-table-container">
  <p>Loading sales data...</p>
</div>

<script>
$(document).ready(function() {
  const csvUrl = 'https://docs.google.com/spreadsheets/d/e/2PACX-1vQF_Cjn-h-NNle2OXlXlLxwNfCmt-vDHqx3hHBuUbVjszS45zLvQPpEiIkkpDhDUB3bC64-PI3_FuKd/pub?gid=0&single=true&output=csv';

  Papa.parse(csvUrl, {
    download: true,
    header: true,
    skipEmptyLines: true,
    complete: function(results) {
      if (!results.data || results.data.length === 0) {
        $('#sales-table-container').html('<p>No sales data available.</p>');
        return;
      }

      const headers = results.meta.fields;
      let tableHtml = '<table id="sales-table" class="display" style="width:100%"><thead><tr>';

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
      $('#sales-table-container').html(tableHtml);

      $('#sales-table').DataTable({
        pageLength: 25,
        order: [[0, 'desc']],
        responsive: true
      });
    },
    error: function(error) {
      console.error('Error loading sales data:', error);
      $('#sales-table-container').html('<p>Error loading sales data. Please check your browser console for details.</p>');
    }
  });
});
</script>
