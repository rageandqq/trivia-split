# Trivia Night Cost Splitter – Agent Prompt & UI Wireframe

## Purpose

Build a **static, client-side-only web app** that helps a group split trivia night costs fairly.

The app must:
- Run entirely in the browser
- Be implemented using **ReactJS**
- Be launched from a **single `index.html` file**
- Require **no build step**, **no backend**, and **no persistence**

Opening `index.html` in a browser should fully run the app.

---

## Technical Constraints (Very Important)

- Use **React via CDN** (e.g. unpkg, esm.sh, skypack)
- No Vite, Webpack, Parcel, or build tools
- No backend, database, or authentication
- No routing
- Use modern React:
  - Function components
  - Hooks (`useState`, `useMemo`)
- All state lives in memory (refresh resets everything)

---

## Core Features

### Members
- Add members by name
- Remove members
- Member names must be unique
- Removing a member also removes their expenses

### Expenses
- Each member can have **multiple expenses**
- Expenses are numeric dollar values
- Expenses are **pre-tax and pre-tip**
- Users can add and remove expenses per member

### Tax & Tip
- Global editable:
  - Tax rate (%)
  - Tip rate (%)
- Tax and tip are applied **proportionally** based on each member’s subtotal.
- The tip rate is applied on each member's pre-tax and pre-discount(winning) total.
- The tax rate is applied on the amount minus the discount

### Winnings (discounts)
- Single winnings amount input
- Winnings are:
  - Evenly divided across all members
  - Deducted **after tax and tip*
- Final amount owed per member cannot go below $0
- If there are winnings left over for a member after their amount hits zero, then the remainder should be split evenly across remaining members

---

## Calculation Rules

For each member:

1. **Subtotal**  
   Sum of that member’s expenses

2. **Tax**  
   `(subtotal - discount/member) × taxRate`

3. **Tip**  
   `subtotal × tipRate`

4. **Pre-winnings total**  
   `subtotal + tax + tip`

5. **Winnings share**  
   `totalWinnings / numberOfMembers`

6. **Final owed**  
   `max(preWinningsTotal − winningsShare, 0)`

All values should automatically update when any input changes.

---

## UI Requirements

- Simple, readable layout
- No UI framework required
- Basic CSS is sufficient
- Calculations should be visible and easy to understand

---

## UI Wireframe (ASCII)

┌───────────────────────────────────────────────┐
│ Trivia Night Splitter │
└───────────────────────────────────────────────┘

┌───────────────────────────────────────────────┐
│ Global Settings │
│ │
│ Tax Rate (%): [ 8.875 ] │
│ Tip Rate (%): [ 20.00 ] │
│ Winnings ($): [ 50.00 ] │
└───────────────────────────────────────────────┘

┌───────────────────────────────────────────────┐
│ Add Member │
│ │
│ Name: [______________] [ Add Member ] │
└───────────────────────────────────────────────┘

┌───────────────────────────────────────────────┐
│ Members │
│ │
│ ┌───────────────────────────────────────────┐ │
│ │ Alex [Remove]│ │
│ │ │ │
│ │ Expenses: │ │
│ │ - $12.00 [Remove] │ │
│ │ - $8.50 [Remove] │ │
│ │ │ │
│ │ Add Expense: [_____] [ Add ] │ │
│ │ │ │
│ │ Subtotal: $20.50 │ │
│ │ Tax: $1.82 │ │
│ │ Tip: $4.10 │ │
│ │ Pre-Winnings: $26.42 │ │
│ │ Winnings Share: -$12.50 │ │
│ │ │ │
│ │ Final Owed: $13.92 │ │
│ └───────────────────────────────────────────┘ │
│ │
│ ┌───────────────────────────────────────────┐ │
│ │ Sam [Remove]│ │
│ │ ... ...│ │
│ └───────────────────────────────────────────┘ │
│ │
└───────────────────────────────────────────────┘


---

## UX Notes

- Calculations update instantly
- Currency should display to 2 decimal places
- Prevent negative expense values
- Disable winnings split if there are zero members
- Keep logic simple and readable

---

## Deliverables

- `index.html`
- JavaScript loaded by `index.html` that defines the React app
- Optional CSS (inline or separate file)

No build instructions.
No external services.
No persistence.

The final result should work by simply opening `index.html`.
