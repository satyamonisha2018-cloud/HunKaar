# HunKaar — Rental Car Business Dashboard Project

## What This Project Is

This is a **rental car business intelligence project** for HunKaar. The owner rents out 2 personal vehicles to customers and tracks everything through **Wave App** (free accounting software). The goal is to build clear HTML dashboards showing financial performance, car utilization, customer analysis, and pricing insights — all deployable as static pages on **GitHub Pages**.

---

## The Business

**Two cars:**

| Car | Year/Model | VIN | Plate | Purchased | Cost |
|-----|-----------|-----|-------|-----------|------|
| Chevy | 2014 Chevy Cruze | 1G1PA5SH8E7104609 | T825590 | Feb 11, 2026 | $7,399.87 |
| Mustang | 2019 Ford Mustang GT | 1FA6P8TH5K5204259 | FT34621 | Feb 18, 2026 | $23,431.00 |

**Insurance:**
- Chevy → Progressive, Policy No: 869502169, Feb 11 – Aug 11, 2026
- Mustang → Geico, Policy No: 6244054968, Feb 18 – Aug 18, 2026

**Data source:** Wave App CSV export. Every transaction appears **twice** in the export (double-entry accounting debit + credit). When reading Wave exports, deduplicate by keeping only the `Income` or `Expense` account type rows — discard the `Cash and Bank` mirror entries.

---

## Current Data (Feb–May 2026)

### All 11 Bookings

| # | Customer | Car | Rental Start | Rental End | Days | Income | Per-Day | Pay Month |
|---|---------|-----|-------------|-----------|------|--------|---------|-----------|
| 1 | Terrance Clark Jr | Chevy | Feb 28 | Mar 1 | 2 | $76.30 | $38.15 | Feb |
| 2 | Katrina Allen | Chevy | Mar 3 | Mar 7 | 5 | $183.04 | $36.61 | Mar |
| 3 | Kathleen Soime | Chevy | Mar 11 | Mar 16 | 6 | $177.12 | $29.52 | Mar |
| 4 | Tina | Mustang | Mar 25 | Mar 29 | 5 | $260.82 | $52.16 | Mar |
| 5 | Dawn | Chevy | Apr 5 | Apr 8 | 4 | $86.40 | $21.60 | Apr |
| 6 | Autumn | Chevy | Apr 11 | Apr 23 | 13 | $378.14 | $29.09 | Apr |
| 7 | Kimberly | Chevy | Apr 25 | Apr 28 | 4 | $115.92 | $28.98 | Apr |
| 8 | Jahyon | Chevy | Apr 30 | May 4 | 5 | $154.87 | $30.97 | Apr |
| 9 | Hope Esther | Chevy | May 17 | May 21 | 5 | $176.64 | $35.33 | May |
| 10 | Kristyana | Chevy | May 22 | May 25 | 4 | $165.28 | $41.32 | May |
| 11 | Karlene | Chevy | May 26 | Jun 1 | 7 | $216.00 | $30.86 | May |

**Days = inclusive count (start date through end date).**
**Pay Month = transaction date in Wave, used for income reporting.**

### Operating Expenses (All Chevy, All March)

| Item | Category | Amount |
|------|----------|--------|
| Gas | Fuel | $6.14 |
| Prime Car Wash | Cleaning | $44.00 |
| Air Freshener | Cleaning | $2.00 |
| Headlight | Maintenance | $25.00 |
| Fuel | Fuel | $31.00 |
| **Total** | | **$108.14** |

### Financial Summary

| Metric | Value |
|--------|-------|
| Total Income | $1,990.53 |
| Total Expenses (operating) | $108.14 |
| Net Operating Profit | $1,882.39 |
| Profit Margin | 94.6% |
| Chevy Income | $1,729.71 |
| Mustang Income | $260.82 |
| Chevy Avg Daily Rate | $32.03/day |
| Mustang Avg Daily Rate | $52.16/day |

**Capital investment excluded from P&L:** Chevy $7,399.87 + Mustang $23,431.00 = $30,830.87 (recorded as fixed assets in Wave).

### Utilization by Month

| Month | Car | Days | Booked | Idle | Utilization |
|-------|-----|------|--------|------|-------------|
| Feb | Chevy | 28 | 1 | 27 | 3.6% |
| Feb | Mustang | 28 | 0 | 28 | 0% |
| Mar | Chevy | 31 | 12 | 19 | 38.7% |
| Mar | Mustang | 31 | 5 | 26 | 16.1% |
| Apr | Chevy | 30 | 22 | 8 | 73.3% |
| Apr | Mustang | 30 | 0 | 30 | 0% |
| May | Chevy | 31 | 19 | 12 | 61.3% |
| May | Mustang | 31 | 0 | 31 | 0% |

---

## Business Logic Rules

### Booked Days — Inclusive Counting
`Booked Days = End Date − Start Date + 1` (owner keeps the car from start through return day).

### Income Recording
Income is tracked by **Wave transaction date** (when payment received), NOT by rental start date. This determines which month the revenue belongs to.

### Utilization
`Utilization % = Booked Days in Month / Total Days in Month`

### Per-Day Rate
`Per-Day Rate = Total Trip Income / Total Trip Days (inclusive)`

### Net P/L
`Net P/L = Total Income − Total Operating Expenses`
Vehicle purchase costs are **capital assets**, not operating expenses.

### Month-Split Bookings
When a booking crosses a month boundary (e.g., Jahyon Apr 30 – May 4), split the booked days into the correct months. Income stays in the pay month.

---

## Key Business Insights (as of May 2026)

- Mustang has only **1 booking** (Tina, March). It has been idle the rest of the time — this is the biggest opportunity to improve business performance.
- Mustang earns **$52.16/day** when rented vs Chevy at **$32.03/day** — higher premium but not being utilized.
- April was the **best month** ($735.33 income, 73% Chevy utilization) with 4 back-to-back Chevy customers.
- Dawn ($21.60/day), Autumn ($29.09/day), Kimberly ($28.98/day) are **below $30/day** — potentially underpriced vs Turo market rates of $40–60/day for a Chevy Cruze.
- No Mustang operating expenses recorded yet — insurance, fuel, maintenance missing.

---

## Files in This Project

| File | What It Is |
|------|-----------|
| `HunKaar Dashboard.html` | Car cost & profitability tracker — main navigation dashboard |
| `Monthly Hunkaar Performance.html` | Monthly performance overview |
| `car-rental-monthly-dashboard.html` | Monthly financial P&L (income/expenses by month and by car) |
| `car-rental-booking-utilization-dashboard.html` | Booking calendar + utilization % (booked/idle days) |
| `car-rental-similar-business-research-report.html` | Market research deck for similar businesses |
| `index.html` | **Comprehensive BI dashboard** (formerly `index.html`, renamed for GitHub Pages) — KPIs, monthly trend, utilization, customer cards, expense breakdown. This is the live homepage. |
| `bookings/index.html` | Car Booking Utilization Dashboard (duplicate/variant) |
| `dashboard/index.html` | Car Rental Monthly Dashboard (duplicate/variant) |
| `bookingutilization-upload/index.html` | Car Booking Utilization Dashboard (upload variant) |

**Most complete dashboard / GitHub Pages homepage:** `index.html` — renamed from `index.html` so GitHub Pages serves it at the repo root. The old root `index.html` ("Car Rental Growth Ideas" team deck) was removed/overwritten.

---

## Design System

All dashboards use the same CSS variable palette and visual language:

```css
:root {
  --ink: #152033;       /* primary text */
  --muted: #657287;     /* secondary text */
  --paper: #fbfcff;     /* page background accent */
  --panel: #ffffff;     /* card backgrounds */
  --line: #dce4ef;      /* borders */
  --blue: #2457c5;      /* Chevy color, primary action */
  --teal: #008f86;      /* utilization, highlights */
  --gold: #d67a18;      /* Mustang color, warnings */
  --red: #c3423f;       /* expenses, loss */
  --green: #238957;     /* income, profit */
  --violet: #6f4bd8;    /* accent */
  --shadow: 0 8px 24px rgba(29,46,73,.10);
  --shadow-lg: 0 16px 40px rgba(29,46,73,.14);
}
```

**Background:** `linear-gradient(135deg, rgba(36,87,197,.15), rgba(0,143,134,.11), rgba(214,122,24,.09)), #edf2f8`

**No external chart libraries.** All charts are pure CSS/JS bar charts using div elements with percentage widths.

**Font:** `Arial, Helvetica, sans-serif`

**Layout:** Centered shell `width: min(1300px, calc(100% - 28px))`, CSS Grid, card-based panels with border-radius 10px.

---

## Tech Stack

- **Pure HTML/CSS/JS** — no frameworks, no build tools, no npm
- **No external dependencies** (all dashboards are self-contained single files)
- **Static files** — deploy directly to GitHub Pages
- **Data is hardcoded** in each HTML file as JS `const` arrays — update the data block when new Wave exports arrive

---

## Git Setup (To Do)

```bash
# Remove nested git in bookingutilization-upload FIRST:
rd /s /q "bookingutilization-upload\.git"

# Then initialize this project:
git init
git add .
git commit -m "Initial commit — HunKaar rental car dashboards"
git remote add origin <YOUR_GITHUB_REPO_URL>
git push -u origin main
```

---

## What's Next / Roadmap

- [ ] Add more bookings as they happen (update `BOOKINGS` array in `index.html`)
- [ ] Add Mustang operating expenses (insurance, fuel) to Wave and re-export
- [ ] Add June 2026 and beyond data monthly
- [ ] Consider raising per-day rate for Chevy (currently averaging $32/day, market is $40–60)
- [ ] Get more Mustang bookings — it's idle and costs money while sitting
- [ ] Connect `bookingutilization-upload/` app to real data input (currently has its own git history)
- [ ] Build a mileage tracker section (some bookings have mileage, some don't)

---

## How to Add New Data

When the user exports a new CSV from Wave:

1. Deduplicate: keep only rows where `Account Type` = `Income` or `Expense`
2. Extract rental dates from the `Notes / Memo` column
3. Map to car using `Account Name` (`Rental Income - Chevy` or `Rental Income - Mustang`)
4. Add to the `BOOKINGS` and `EXPENSES` arrays in `index.html`
5. Update the `MONTHS` array if new months are covered

Wave CSV columns used: `Transaction Date`, `Account Name`, `Transaction Description` (customer name), `Amount`, `Notes / Memo` (rental dates, mileage, gas).
