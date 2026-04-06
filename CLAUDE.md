# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm install      # install dependencies (required before first run)
npm run dev      # start dev server at http://localhost:5173
npm run build    # production build
npm run lint     # ESLint
npm run preview  # preview production build
```

## Architecture

Single-file React app — all state and UI lives in `src/App.jsx`. No routing, no external state management, no backend.

**State in App.jsx:**
- `transactions` — array of `{ id, description, amount, type, category, date }` where `type` is `"income"` or `"expense"`
- `description`, `amount`, `type`, `category` — controlled form inputs for adding a transaction
- `filterType`, `filterCategory` — filter state for the transaction table

**Known bugs (intentional — this is a course starter project):**
- `amount` is stored as a string, so `totalIncome`/`totalExpenses` use string concatenation instead of numeric addition. Fix: parse `amount` to a float when creating a transaction or when computing totals.
- Transaction #4 "Freelance Work" has `type: "expense"` but `category: "salary"` — likely meant to be `type: "income"`.

**Styling:** plain CSS in `src/App.css`, no utility framework. CSS classes follow a flat naming convention (`.summary-card`, `.income-amount`, `.expense-amount`, `.delete-btn`).
