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
  .inventory-table-wrap {
    overflow-x: auto;
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
    .inventory-controls {
      grid-template-columns: 1fr;
    }
  }
</style>

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

<p id="inventoryMeta" class="inventory-meta" aria-live="polite">Loading inventory…</p>

<div class="inventory-table-wrap">
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
        renderTable(records);
      } catch (error) {
        thead.innerHTML = "";
        tbody.innerHTML = `<tr><td class="inventory-empty">Could not load sheet data. Ensure the sheet is published/shared for public viewing.</td></tr>`;
        meta.textContent = "Inventory load failed.";
        console.error("Inventory load failed:", error);
      }
    };

    searchInput.addEventListener("input", applyFilter);
    columnSelect.addEventListener("change", applyFilter);
    clearButton.addEventListener("click", () => {
      searchInput.value = "";
      columnSelect.value = "__all__";
      renderTable(records);
      searchInput.focus();
    });

    loadSheet();
  })();
</script>
