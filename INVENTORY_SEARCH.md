---
layout: default
title: Inventory Search
nav_order: 6
permalink: /inventory
---
# 🔎 Inventory Search

Search the live inventory spreadsheet and filter items by any text value.

> Source sheet: [Inventory spreadsheet](https://docs.google.com/spreadsheets/d/18TwnlgLCAB2be3Lkxc88MYYK7kQ2talrEXlg7IwrvVI/edit?usp=drivesdk)

<style>
  .inventory-request {
    margin: 0.6rem 0 0.85rem 0;
  }
  .inventory-request-button {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    min-height: 44px;
    border: 2px solid var(--brand-red);
    border-radius: 6px;
    padding: 0.85rem 1.6rem;
    font-size: 0.95rem;
    font-weight: 800;
    background: var(--brand-red);
    color: #fff !important;
    text-decoration: none;
    transition: transform 0.15s, box-shadow 0.15s;
  }
  .inventory-request-button:visited {
    background: var(--brand-red);
    border-color: var(--brand-red);
    color: #fff;
  }
  .inventory-request-button:hover {
    transform: translateY(-2px);
    box-shadow: 0 6px 20px rgba(0,0,0,0.4);
    text-decoration: none;
    background: var(--brand-red-dark);
    border-color: var(--brand-red-dark);
    color: #fff;
  }
  .inventory-request-button:active {
    background: var(--brand-red-dark);
    border-color: var(--brand-red-dark);
    color: #fff;
  }
  .inventory-request-button:focus-visible {
    outline: 3px solid #ffffff;
    outline-offset: 3px;
    box-shadow: 0 0 0 6px rgba(204,0,0,0.6), 0 0 0 10px rgba(255,255,255,0.25);
    color: #fff;
  }
  .inventory-controls {
    display: grid;
    grid-template-columns: 2fr 1fr auto;
    gap: 0.6rem;
    margin: 1rem 0 0.75rem 0;
    align-items: end;
  }
  .inventory-control {
    display: grid;
    gap: 0.35rem;
  }
  .inventory-label {
    font-size: 0.9rem;
    font-weight: 600;
  }
  .inventory-input,
  .inventory-select,
  .inventory-button {
    min-height: 2.3rem;
    border: 1px solid #b9b9b9;
    border-radius: 0.2rem;
    padding: 0.45rem 0.6rem;
    font-size: 0.95rem;
  }
  .inventory-button {
    background: var(--brand-red);
    color: #fff;
    border-color: #7a0000;
    cursor: pointer;
    font-weight: 600;
  }
  .inventory-button:hover {
    background: #990000;
  }
  .inventory-meta {
    margin: 0.45rem 0 0.65rem 0;
    color: var(--muted);
    font-size: 0.9rem;
  }
  .inventory-chart {
    margin: 1.1rem 0 1rem 0;
    padding: 0.9rem;
    border: 1px solid #d8d8d8;
    border-radius: 0.35rem;
    background: rgba(255, 255, 255, 0.45);
  }
  .inventory-chart-title {
    margin: 0 0 0.6rem 0;
    font-size: 1.1rem;
  }
  .inventory-chart-controls {
    grid-template-columns: repeat(2, minmax(0, 1fr));
    margin-top: 0.4rem;
  }
  .inventory-chart-summary {
    margin: 0.75rem 0 0.6rem 0;
    font-weight: 600;
    color: var(--text);
  }
  .inventory-chart-list {
    display: grid;
    gap: 0.55rem;
  }
  .inventory-chart-row {
    display: grid;
    grid-template-columns: minmax(10rem, 1fr) minmax(0, 2fr) auto;
    gap: 0.7rem;
    align-items: center;
  }
  .inventory-chart-name {
    font-weight: 600;
    overflow-wrap: anywhere;
  }
  .inventory-chart-track {
    width: 100%;
    height: 1rem;
    border-radius: 999px;
    background: #ececec;
    overflow: hidden;
  }
  .inventory-chart-fill {
    height: 100%;
    min-width: 0;
    background: linear-gradient(90deg, var(--brand-red), var(--brand-red-dark));
    border-radius: 999px;
  }
  .inventory-chart-total {
    font-variant-numeric: tabular-nums;
    white-space: nowrap;
  }
  .inventory-table-wrap {
    overflow-x: auto;
    -webkit-overflow-scrolling: touch;
    border: 1px solid #d8d8d8;
    border-radius: 0.2rem;
  }
  .inventory-table {
    width: 100%;
    border-collapse: collapse;
    min-width: 720px;
  }
  .inventory-table th,
  .inventory-table td {
    border-bottom: 1px solid #e2e2e2;
    padding: 0.5rem 0.6rem;
    text-align: left;
    vertical-align: top;
  }
  .inventory-table th {
    background: #f7f7f7;
    position: sticky;
    top: 0;
    z-index: 1;
  }
  .inventory-empty {
    padding: 0.9rem;
    color: var(--muted);
  }
  @media (max-width: 760px) {
    .inventory-request-button {
      display: flex;
      width: 100%;
    }
    .inventory-controls {
      grid-template-columns: 1fr;
    }
    .inventory-chart-row {
      grid-template-columns: 1fr;
      gap: 0.35rem;
    }
  }
</style>

<p class="inventory-request">
  <a
    class="inventory-request-button"
    href="https://docs.google.com/spreadsheets/d/1ND5yHu2dxlJKNNGT6ja19kb7lLZpjMubFtNuRZ90mW4/edit?gid=85868532#gid=85868532"
    aria-label="Add Reagent Request (opens in a new tab)"
    target="_blank"
    rel="noopener"
  >➕ Add Reagent Request</a>
</p>

<form class="inventory-controls" aria-label="Inventory search controls" onsubmit="return false;">
  <div class="inventory-control">
    <label class="inventory-label" for="inventorySearchInput">Search inventory</label>
    <input id="inventorySearchInput" class="inventory-input" type="search" placeholder="Enter text to match">
  </div>
  <div class="inventory-control">
    <label class="inventory-label" for="inventoryColumnSelect">Filter by column</label>
    <select id="inventoryColumnSelect" class="inventory-select">
      <option value="__all__">All columns</option>
    </select>
  </div>
  <button id="inventoryClearButton" class="inventory-button" type="button">Clear search</button>
</form>

<section class="inventory-chart" aria-labelledby="inventoryChartTitle">
  <h2 id="inventoryChartTitle" class="inventory-chart-title">Inventory Totals Chart</h2>
  <div class="inventory-controls inventory-chart-controls" aria-label="Inventory chart controls">
    <div class="inventory-control">
      <label class="inventory-label" for="inventoryChartGroupSelect">Group totals by</label>
      <select id="inventoryChartGroupSelect" class="inventory-select" disabled>
        <option value="">Loading columns…</option>
      </select>
    </div>
    <div class="inventory-control">
      <label class="inventory-label" for="inventoryChartValueSelect">Total using</label>
      <select id="inventoryChartValueSelect" class="inventory-select" disabled>
        <option value="__rows__">Row count</option>
      </select>
    </div>
  </div>
  <p id="inventoryChartSummary" class="inventory-chart-summary" aria-live="polite">
    Loading chart…
  </p>
  <div id="inventoryChartList" class="inventory-chart-list" role="list" aria-live="polite">
    <div class="inventory-empty" role="listitem">Loading chart…</div>
  </div>
  <p class="inventory-meta">
    Choose any column to see grouped totals, or switch to row count when a numeric total is not needed.
  </p>
</section>

<p id="inventoryMeta" class="inventory-meta" aria-live="polite">Loading inventory…</p>

<div class="inventory-table-wrap" tabindex="0" aria-label="Scrollable inventory results table">
  <table id="inventoryTable" class="inventory-table" aria-label="Inventory results">
    <thead></thead>
    <tbody>
      <tr><td class="inventory-empty">Loading inventory…</td></tr>
    </tbody>
  </table>
</div>

<script>
  (() => {
    const SHEET_ID = "18TwnlgLCAB2be3Lkxc88MYYK7kQ2talrEXlg7IwrvVI";
    const SHEET_GID = "0";
    const csvUrl = `https://docs.google.com/spreadsheets/d/${SHEET_ID}/gviz/tq?tqx=out:csv&gid=${SHEET_GID}`;

    const searchInput = document.getElementById("inventorySearchInput");
    const columnSelect = document.getElementById("inventoryColumnSelect");
    const clearButton = document.getElementById("inventoryClearButton");
    const table = document.getElementById("inventoryTable");
    const thead = table.querySelector("thead");
    const tbody = table.querySelector("tbody");
    const meta = document.getElementById("inventoryMeta");
    const chartGroupSelect = document.getElementById("inventoryChartGroupSelect");
    const chartValueSelect = document.getElementById("inventoryChartValueSelect");
    const chartSummary = document.getElementById("inventoryChartSummary");
    const chartList = document.getElementById("inventoryChartList");

    let headers = [];
    let records = [];

    const parseCsv = (text) => {
      const rows = [];
      let row = [];
      let field = "";
      let inQuotes = false;

      for (let i = 0; i < text.length; i++) {
        const char = text[i];
        const next = text[i + 1];

        if (char === '"') {
          if (inQuotes && next === '"') {
            field += '"';
            i++;
          } else {
            inQuotes = !inQuotes;
          }
        } else if (char === "," && !inQuotes) {
          row.push(field);
          field = "";
        } else if ((char === "\n" || char === "\r") && !inQuotes) {
          if (char === "\r" && next === "\n") i++;
          row.push(field);
          if (row.some((cell) => cell.trim() !== "")) rows.push(row);
          row = [];
          field = "";
        } else {
          field += char;
        }
      }

      row.push(field);
      if (row.some((cell) => cell.trim() !== "")) rows.push(row);
      return rows;
    };

    const updateMeta = (count, total) => {
      meta.textContent = `${count} of ${total} row${total === 1 ? "" : "s"} shown`;
    };

    const renderTable = (items) => {
      thead.innerHTML = "";
      tbody.innerHTML = "";

      if (!headers.length) {
        tbody.innerHTML = `<tr><td class="inventory-empty">No headers found in sheet.</td></tr>`;
        meta.textContent = "No inventory headers found.";
        return;
      }

      const headerRow = document.createElement("tr");
      headers.forEach((header) => {
        const th = document.createElement("th");
        th.scope = "col";
        th.textContent = header || "(Unnamed column)";
        headerRow.appendChild(th);
      });
      thead.appendChild(headerRow);

      if (!items.length) {
        const tr = document.createElement("tr");
        const td = document.createElement("td");
        td.className = "inventory-empty";
        td.colSpan = headers.length;
        td.textContent = "No matching inventory rows.";
        tr.appendChild(td);
        tbody.appendChild(tr);
        updateMeta(0, records.length);
        return;
      }

      const fragment = document.createDocumentFragment();
      items.forEach((item) => {
        const tr = document.createElement("tr");
        headers.forEach((key) => {
          const td = document.createElement("td");
          td.textContent = item[key] ?? "";
          tr.appendChild(td);
        });
        fragment.appendChild(tr);
      });
      tbody.appendChild(fragment);
      updateMeta(items.length, records.length);
    };

    const applyFilter = () => {
      const term = searchInput.value.trim().toLowerCase();
      const selected = columnSelect.value;

      if (!term) {
        renderTable(records);
        return;
      }

      const filtered = records.filter((record) => {
        if (selected !== "__all__") {
          return String(record[selected] ?? "").toLowerCase().includes(term);
        }
        return headers.some((header) =>
          String(record[header] ?? "").toLowerCase().includes(term)
        );
      });
      renderTable(filtered);
    };

    const populateColumnFilter = () => {
      columnSelect.innerHTML = `<option value="__all__">All columns</option>`;
      headers.forEach((header) => {
        const option = document.createElement("option");
        option.value = header;
        option.textContent = header || "(Unnamed column)";
        columnSelect.appendChild(option);
      });
    };

    const findHeader = (pattern, fallback = "") =>
      headers.find((header) => pattern.test(String(header || ""))) || fallback;

    const parseCount = (value) => {
      const cleaned = String(value ?? "").replace(/[^0-9.-]/g, "");
      const numeric = Number.parseFloat(cleaned);
      return Number.isFinite(numeric) ? Math.max(0, numeric) : NaN;
    };

    const getNumericHeaders = () =>
      headers.filter((header) =>
        records.some((record) => Number.isFinite(parseCount(record[header])))
      );

    const formatChartLabel = (value) => value || "(Blank)";

    const formatChartTotal = (value) =>
      Number.isInteger(value) ? String(value) : value.toLocaleString(undefined, { maximumFractionDigits: 2 });

    const buildGroupedSeries = (groupHeader, valueHeader) => {
      if (!groupHeader) return [];

      const grouped = new Map();
      records.forEach((record) => {
        const groupName = formatChartLabel(String(record[groupHeader] ?? "").trim());
        const increment = valueHeader === "__rows__"
          ? 1
          : parseCount(record[valueHeader]);

        if (!Number.isFinite(increment) || increment <= 0) return;
        grouped.set(groupName, (grouped.get(groupName) || 0) + increment);
      });

      return Array.from(grouped.entries())
        .map(([name, total]) => ({ name, total }))
        .sort((a, b) => b.total - a.total || a.name.localeCompare(b.name));
    };

    const populateChartControls = () => {
      const numericHeaders = getNumericHeaders();
      const preferredGroupHeader =
        chartGroupSelect.value ||
        findHeader(/category|type|group|class|section|department/i, "") ||
        findHeader(/item|reagent|name|material|product/i, "") ||
        headers[0] ||
        "";
      const preferredValueHeader =
        chartValueSelect.value ||
        findHeader(/count|qty|quantity|stock|on\s*hand|amount|units?/i, "") ||
        numericHeaders[0] ||
        "__rows__";

      chartGroupSelect.innerHTML = "";
      headers.forEach((header) => {
        const option = document.createElement("option");
        option.value = header;
        option.textContent = header || "(Unnamed column)";
        chartGroupSelect.appendChild(option);
      });

      chartValueSelect.innerHTML = "";
      const rowCountOption = document.createElement("option");
      rowCountOption.value = "__rows__";
      rowCountOption.textContent = "Row count";
      chartValueSelect.appendChild(rowCountOption);

      numericHeaders.forEach((header) => {
        const option = document.createElement("option");
        option.value = header;
        option.textContent = header || "(Unnamed numeric column)";
        chartValueSelect.appendChild(option);
      });

      chartGroupSelect.disabled = !headers.length;
      chartValueSelect.disabled = !headers.length;

      if (headers.includes(preferredGroupHeader)) {
        chartGroupSelect.value = preferredGroupHeader;
      } else if (headers.length) {
        chartGroupSelect.value = headers[0];
      }

      if (preferredValueHeader === "__rows__" || numericHeaders.includes(preferredValueHeader)) {
        chartValueSelect.value = preferredValueHeader;
      } else {
        chartValueSelect.value = "__rows__";
      }
    };

    const renderInventoryChart = () => {
      const groupHeader = chartGroupSelect.value;
      const valueHeader = chartValueSelect.value;
      const selectedSeries = buildGroupedSeries(groupHeader, valueHeader);

      chartList.innerHTML = "";

      if (!groupHeader || !selectedSeries.length) {
        chartSummary.textContent = headers.length
          ? "No totals are available for the selected chart settings."
          : "Load inventory data to view totals.";
        chartList.innerHTML = `<div class="inventory-empty" role="listitem">No grouped totals available.</div>`;
        return;
      }

      const maxTotal = Math.max(...selectedSeries.map((item) => item.total), 0);
      const valueLabel = valueHeader === "__rows__" ? "row count" : valueHeader;
      chartSummary.textContent = `Showing ${selectedSeries.length} grouped total${selectedSeries.length === 1 ? "" : "s"} by ${groupHeader} using ${valueLabel}.`;

      const fragment = document.createDocumentFragment();
      selectedSeries.forEach((item) => {
        const row = document.createElement("div");
        row.className = "inventory-chart-row";
        row.setAttribute("role", "listitem");

        const name = document.createElement("div");
        name.className = "inventory-chart-name";
        name.textContent = item.name;

        const track = document.createElement("div");
        track.className = "inventory-chart-track";
        track.setAttribute("aria-hidden", "true");

        const fill = document.createElement("div");
        fill.className = "inventory-chart-fill";
        fill.style.width = `${maxTotal > 0 ? (item.total / maxTotal) * 100 : 0}%`;
        track.appendChild(fill);

        const total = document.createElement("div");
        total.className = "inventory-chart-total";
        total.textContent = formatChartTotal(item.total);

        row.append(name, track, total);
        fragment.appendChild(row);
      });

      chartList.appendChild(fragment);
    };

    const loadSheet = async () => {
      try {
        const response = await fetch(csvUrl, { cache: "no-store" });
        if (!response.ok) throw new Error(`HTTP ${response.status}`);
        const csvText = await response.text();
        const rows = parseCsv(csvText);
        if (!rows.length) throw new Error("No rows returned.");

        headers = rows[0].map((h) => (h || "").trim());
        records = rows.slice(1).map((cells) => {
          const entry = {};
          headers.forEach((key, index) => {
            entry[key] = (cells[index] || "").trim();
          });
          return entry;
        });

        populateColumnFilter();
        populateChartControls();
        renderInventoryChart();
        renderTable(records);
      } catch (error) {
        thead.innerHTML = "";
        tbody.innerHTML = `<tr><td class="inventory-empty">Could not load sheet data. Ensure the sheet is published/shared for public viewing.</td></tr>`;
        meta.textContent = "Inventory load failed.";
        chartGroupSelect.innerHTML = `<option value="">Inventory unavailable</option>`;
        chartGroupSelect.disabled = true;
        chartValueSelect.innerHTML = `<option value="__rows__">Row count</option>`;
        chartValueSelect.disabled = true;
        chartSummary.textContent = "Inventory chart unavailable.";
        chartList.innerHTML = `<div class="inventory-empty" role="listitem">Could not load chart data.</div>`;
        console.error("Inventory load failed:", error);
      }
    };

    searchInput.addEventListener("input", applyFilter);
    columnSelect.addEventListener("change", applyFilter);
    chartGroupSelect.addEventListener("change", renderInventoryChart);
    chartValueSelect.addEventListener("change", renderInventoryChart);
    clearButton.addEventListener("click", () => {
      searchInput.value = "";
      columnSelect.value = "__all__";
      renderTable(records);
      searchInput.focus();
    });

    loadSheet();
  })();
</script>
