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

React app split into four components. No routing, no external state management, no backend.

**Component tree:**
```
App
├── Summary
├── TransactionForm
└── TransactionList
```

**`src/App.jsx`** — root component, owns `transactions` state and passes it down.
- `transactions` — array of `{ id, description, amount, type, category, date }` where `type` is `"income"` or `"expense"`
- Passes `onAdd` callback to `TransactionForm` to append new transactions

**`src/Summary.jsx`** — displays income, expenses, and balance cards.
- Receives `transactions` and computes `totalIncome`, `totalExpenses`, `balance` internally

**`src/TransactionForm.jsx`** — controlled form for adding a transaction.
- Owns its own form state: `description`, `amount`, `type`, `category`
- Calls `onAdd(transaction)` prop on submit; resets fields after

**`src/TransactionList.jsx`** — filtered table of transactions.
- Receives `transactions` as a prop
- Owns its own filter state: `filterType`, `filterCategory`

**Shared constant:** `categories` array is defined locally in both `TransactionForm` and `TransactionList` (no shared module — kept simple for a course project).

**Known bugs (intentional — this is a course starter project):**
- `amount` is stored as a string, so `totalIncome`/`totalExpenses` use string concatenation instead of numeric addition. Fix: parse `amount` to a float when creating a transaction or when computing totals.
- Transaction #4 "Freelance Work" has `type: "expense"` but `category: "salary"` — likely meant to be `type: "income"`.

**Styling:** plain CSS in `src/App.css`, no utility framework. CSS classes follow a flat naming convention (`.summary-card`, `.income-amount`, `.expense-amount`, `.delete-btn`).
