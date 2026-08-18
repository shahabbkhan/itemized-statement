# Itemized Statement for Manager.io

A detailed, print-ready statement extension for [Manager.io](https://www.manager.io) that shows every transaction line-by-line with full tax breakdowns, running balances, and more — delivered as a single HTML file that runs inside Manager's Extension system.

---

## Features

- Customer and supplier statements with full line-item detail
- Line-level tax breakdown — amounts excl. tax, tax components, amounts incl. tax
- Quantity × unit price calculation when those columns are enabled in Manager
- Discount support (percentage and fixed amount)
- Withholding tax — separate transaction for invoices, embedded detail line for credit/debit notes
- Freight-in / landed cost lines with tax (purchase invoices, only when inventory items are present)
- Foreign currency support with exchange rate conversion
- Journal entries with line description or narration display
- Cross-type invoice references — receipts and payments can reference both sales and purchase invoices
- **Combined statement** — pair a customer and supplier into one merged statement, useful when a party is both
- Dashboard with sortable table, summary cards, and hide-zero-balance filter
- Batch generation — select multiple parties and print all statements at once
- CSV export
- Professional print layout with business letterhead, B&W ready, repeating table headers
- Period presets: This Month / Quarter / Year, Last Month / Quarter / Year, Last 3 / 6 / 12 Months, From Start
- Permission-aware — shows a warning when data cannot be accessed due to user restrictions

---

## How to add this extension in Manager.io

1. Open **Settings**
2. Click **Extensions**
3. Click **New Extension**
4. Enter a **Name** (e.g. Itemized Statement)
5. Set **Source** = `URL`
6. Paste this into **Endpoint**: `https://shahabbkhan.github.io/itemized-statement/`
7. Choose a **Placement** (e.g. `/`)
8. Click **Create**

The extension will appear in your Manager sidebar. No installation, no build step, no dependencies.

---

## API Endpoints used

The extension reads from the following Manager api4 endpoints. The user running the extension must have access to the relevant modules for the statement to be complete.

| Endpoint | Purpose |
|---|---|
| `/api4/customer-batch` | Customer list |
| `/api4/supplier-batch` | Supplier list |
| `/api4/sales-invoice-batch` | Sales invoices |
| `/api4/purchase-invoice-batch` | Purchase invoices |
| `/api4/credit-note-batch` | Credit notes |
| `/api4/debit-note-batch` | Debit notes |
| `/api4/receipt-batch` | Receipts |
| `/api4/payment-batch` | Payments |
| `/api4/journal-entry-batch` | Journal entries |
| `/api4/late-payment-fee-batch` | Late payment fees |
| `/api4/control-account-for-customers-batch` | AR control accounts |
| `/api4/control-account-for-suppliers-batch` | AP control accounts |
| `/api4/balance-sheet-accounts-receivable-account` | Main AR account |
| `/api4/balance-sheet-accounts-payable-account` | Main AP account |
| `/api4/bank-or-cash-account-batch` | Bank/cash accounts (for currency) |
| `/api4/foreign-currency-batch` | Foreign currency info |
| `/api4/exchange-rate-batch` | Exchange rates |
| `/api4/tax-code-batch` | Tax codes |
| `/api4/balance-sheet-account-batch` | Chart of accounts |
| `/api4/profit-and-loss-statement-account-batch` | P&L accounts |
| `/api4/inventory-item-batch` | Inventory items |
| `/api4/non-inventory-item-batch` | Non-inventory items |
| `/api4/inventory-kit-batch` | Inventory kits |
| `/api4/base-currency` | Base currency |
| `/api4/date-and-number-format` | Date and number formatting |
| `/api4/business-details` | Business name and address |

All calls are read-only GET requests. The extension never writes to your Manager database.

---

## How it works

The extension communicates with Manager exclusively through the native `postMessage` API — no external servers, no data leaves your machine. Everything runs inside Manager's iframe sandbox.

Amounts follow Manager's own column settings on each document — if unit price and quantity columns are enabled, the amount is calculated from `qty × unitPrice`. Discounts are applied on top. For foreign currency documents, the extension uses `lineCurrencyAmount` when available, falls back to the document-level exchange rate, then the exchange rate list.

---

## Contributing

Issues and pull requests are welcome. If you find a bug, open an issue with your Manager version, what you expected, and what actually happened.

---

## License

MIT License — free to use, modify, and distribute.

Copyright (c) 2026 shahabkhann
