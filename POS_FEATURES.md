# Nodedr OrderRestro — Complete POS Feature Analysis

> **Repository**: [nodedr-restaurant-pos](file:///c:/Users/yashr/OneDrive/Desktop/gitpos/nodedr-restaurant-pos)  
> **Developer**: NodeDR Infotech Private Limited / Raktim Ranjit  
> **License**: AGPL-3.0 (open-source, self-hosted)  
> **Status**: Active Development (v0.1.0)  

---

## 1. Executive Summary

**Nodedr OrderRestro** is a **purpose-built, offline-first, self-hosted Restaurant Management System** — not a generic retail POS repurposed for food service. It spans **20 product domains** covering point-of-sale billing, kitchen display systems (KDS), table and floor management, inventory tracking, procurement, staff HR/payroll, accounting, CRM, and multi-branch management.

The entire stack — **PostgreSQL + NestJS API + Next.js web application** — runs on a single local server on the restaurant's local area network (LAN). Ordering, billing, KDS tickets, and receipt/KOT printing function seamlessly **even when the internet is completely disconnected**.

### Key Differentiators
- 🇮🇳 **India-first**: Dynamic UPI QR payments, GST-inclusive pricing (CGST/SGST backed out with decimal precision).
- 🔌 **Offline-first**: Zero cloud reliance for day-to-day operations.
- 🏠 **Self-hosted**: Your data stays on your machine, AGPL-3.0 licensed.
- 🍽️ **Restaurant-native**: Built for dine-in tables, takeaway counter, delivery dispatch, and multi-station kitchen workflows.
- 🎨 **Modern Aesthetics**: Built with Next.js App Router, Tailwind CSS, and shadcn/ui.

---

## 2. Tech Stack

| Layer | Technology | Purpose |
|---|---|---|
| **Monorepo** | pnpm workspaces + Turborepo | Manages apps and shared packages |
| **Backend** | NestJS (TypeScript) | REST API on `:4001`, Swagger docs at `/api/docs` |
| **Database** | PostgreSQL 15/16 + Prisma ORM | Relational data persistence with migrations |
| **Realtime** | Socket.IO | Live KDS tickets, order state transitions, table status |
| **Frontend** | Next.js 16 + React 19 + Tailwind CSS | POS terminal, manager dashboard, customer QR menu |
| **UI Components** | shadcn/ui + Radix / Base UI + Lucide Icons | Clean, responsive POS interface |
| **State & Data** | TanStack Query + React Hook Form + Zod | Cached data synchronization & schema validation |
| **Auth** | JWT in httpOnly cookie + Quick PIN switch | Fast staff switching on shared terminals |

---

## 3. Complete Feature Breakdown (20 Modules)

### Status Key
- ✅ **Shipped** — Fully implemented and functional in code
- 🟡 **Partial** — Core logic present; specific extensions pending
- 🚧 **Planned** — Roadmapped in architecture specifications

---

### Module 1: 🧾 POS & Billing
| Feature | Status | Details |
|---|---|---|
| Touch-friendly billing screen | ✅ | Product grid + cart, tablet & desktop responsive |
| Category & Product grid search | ✅ | Category tabs + real-time search |
| Add-ons & Modifier groups | ✅ | Min/max selection limits, default items, price additions |
| Combo & Bundle products | ✅ | Bundled item selections |
| Table transfer & Bill merge | ✅ | Move open bills between tables; merge multiple checks |
| Order cancellations & item voiding | ✅ | Reason required, audit trail captured |
| Order-level discounts & tips | ✅ | Percentage and fixed discounts; tax-exempt tip lines |
| Multi-region tax computation | ✅ | India GST (CGST/SGST), US Sales Tax, EU VAT, Spain IVA |
| Multi-tender payment methods | ✅ | Cash, Card, UPI, Digital Wallets |
| Split bill calculator | 🟡 | Equal split calculation |
| Multi-tender split payments | 🚧 | Single payment method per order currently |

---

### Module 2: 🪑 Table & Floor Management
| Feature | Status | Details |
|---|---|---|
| Visual floor plan | ✅ | Position coordinates (`posX`, `posY`) and shape rendering |
| Multi-floor support | ✅ | Floor switcher with custom zones |
| Table status lifecycle | ✅ | Available → Occupied → Reserved → Cleaning → Out of Service |
| Waiter assignment | ✅ | Assign staff to individual tables |
| Table QR codes | ✅ | Secure, rotatable tokenized QR codes for self-ordering |
| Reservation lifecycle | ✅ | Reserved → Confirmed → Arrived → Completed/Cancelled |
| Live waitlist | ✅ | Queue management with estimated wait time |

---

### Module 3: 👨‍🍳 Kitchen Display System (KDS)
| Feature | Status | Details |
|---|---|---|
| Realtime kitchen tickets | ✅ | Live Socket.IO ticket push |
| Status pipeline | ✅ | New → Preparing → Ready → Completed |
| Urgency timers & priority | ✅ | Ticket elapsed timers, visual alerts past 15 min, rush order flag |
| Sound notifications | ✅ | Audio chimes on new incoming tickets |
| Kitchen station routing | ✅ | Route appetizers to Fryer station, mains to Grill station |
| Performance metrics | ✅ | Average preparation times tracked per station |

---

### Module 4: 🍽️ Menu Management
| Feature | Status | Details |
|---|---|---|
| Categories & Menu Items | ✅ | Full catalog with images, pricing, and descriptions |
| Modifier groups | ✅ | Optional and mandatory customization groups |
| Recipe & Ingredient mapping | ✅ | Link menu items to raw ingredients for auto-deduction |
| Allergen & Dietary tags | ✅ | Vegan, vegetarian, spice levels, allergen declarations |
| Availability scheduling | ✅ | Active time windows and manual item out-of-stock toggles |

---

### Module 5: 📦 Inventory & Stock Control
| Feature | Status | Details |
|---|---|---|
| Ingredient stock tracking | ✅ | Ledger-based stock adjustments |
| Low stock warnings | ✅ | Automatic alerts when inventory drops below threshold |
| Batch & Expiry tracking | ✅ | Track goods receipt notes (GRN) with batch dates |
| Recipe-based auto-deduction | ✅ | Deducts raw ingredients automatically upon order checkout |
| Waste & Spoilage logging | ✅ | Record wasted stock with reason codes and FIFO valuation |
| Weighted average food cost | ✅ | Dynamically recalculated on every procurement receipt |

---

### Module 6: 🛒 Procurement & Suppliers
| Feature | Status | Details |
|---|---|---|
| Supplier directory | ✅ | Vendor contacts, catalog items, and payment terms |
| Purchase Orders (PO) | ✅ | Draft → Approved → Sent → Received workflow |
| Goods Received Notes (GRN) | ✅ | Verify quantities received against purchase orders |
| Quotation comparison | ✅ | Multi-supplier quote comparison |
| Supplier payments & invoices | ✅ | Track outstanding vendor balances and payment history |

---

### Module 7: 👤 Customer CRM & Loyalty
| Feature | Status | Details |
|---|---|---|
| Customer profiles | ✅ | Contact information, dietary preferences, order history |
| Loyalty points | ✅ | Earn points on purchases and redeem for discounts |
| Customer notes & tags | ✅ | Special customer instructions and preferences |
| Automated customer tiers | 🚧 | VIP tiers planned |

---

### Module 8: 👨‍💼 Staff & Shift Management
| Feature | Status | Details |
|---|---|---|
| Role-based access control (RBAC)| ✅ | 11 granular system roles (Owner, Manager, Cashier, Waiter, Chef, etc.) |
| Quick PIN authentication | ✅ | Switch users quickly at POS terminals |
| Attendance clock-in / clock-out | ✅ | Timekeeping with shift tracking |
| Shift scheduling | ✅ | Roster creation with clash detection |
| Tip distribution | ✅ | Tip pool split proportional to clocked hours |

---

### Module 9: 📊 Accounting & Finance
| Feature | Status | Details |
|---|---|---|
| End-of-day register closing | ✅ | Cash drawer count, card summary, cash over/short variance |
| Expense tracking | ✅ | Categorized operational expense records |
| Profit & Loss statements | ✅ | Revenue minus COGS and operating expenses |
| Tax summaries | ✅ | Breakdown of collected tax rates for tax filing |

---

### Module 10: 🚚 Delivery Management
| Feature | Status | Details |
|---|---|---|
| Delivery zones | ✅ | Zones mapped by postal code with delivery fees and minimum order values |
| Driver dispatch | ✅ | Assign delivery orders to in-house drivers |
| Order status tracking | ✅ | Dispatched → Delivered lifecycle |

---

### Module 11: 📱 Customer QR Ordering & Kiosk
| Feature | Status | Details |
|---|---|---|
| Table QR Ordering | ✅ | Customer opens digital menu on mobile, adds modifiers, submits order |
| Call waiter / Request bill | ✅ | Real-time service requests sent to staff dashboard |
| Self-service Kiosk mode | ✅ | Dedicated kiosk layout (`/kiosk/[token]`) |

---

### Module 12: 🏪 Multi-Branch Management
| Feature | Status | Details |
|---|---|---|
| Multi-branch hierarchy | ✅ | Organization level `Restaurant` with multiple `Branch` locations |
| Branch switcher | ✅ | Seamless branch switching for administrative users |
| Inter-branch stock transfers | ✅ | Move ingredients between physical locations |

---

### Module 13: 📈 Reports & Analytics
| Feature | Status | Details |
|---|---|---|
| Realtime metrics dashboard | ✅ | Daily sales volume, popular items, table occupancy |
| 18 operational reports | ✅ | Peak sales hours, ingredient margins, customer retention |
| Export capabilities | ✅ | PDF, Excel, CSV, and thermal print formats |

---

### Module 14: 🔐 Security & Administration
| Feature | Status | Details |
|---|---|---|
| Two-factor authentication (TOTP)| ✅ | Authenticator app 2FA with emergency backup codes |
| Immutable audit log | ✅ | Audits every price override, void, refund, and role change |
| Database backups | ✅ | In-app backup creation and restoration |

---

### Module 15: 🔌 Hardware & Integrations
| Feature | Status | Details |
|---|---|---|
| Thermal Receipt & KOT Printing | ✅ | Direct ESC/POS via USB and Network TCP/9100 |
| Cash drawer kick | ✅ | ESC/POS pulse on cash payment completion |
| Dynamic UPI QR | ✅ | Direct UPI string generation for exact bill amount |
| Webhooks | ✅ | Event notifications for external system integrations |
| MCP Server | ✅ | Model Context Protocol integration for AI agents |

---

## 4. Local Development & Running the App

### Running Locally on Windows
```powershell
# In the cloned directory:
cd nodedr-restaurant-pos

# Run both backend and web frontend:
pnpm dev
```

### Access Points
- **Web App**: [http://localhost:1995](http://localhost:1995)
- **API Swagger Documentation**: [http://localhost:4001/api/docs](http://localhost:4001/api/docs)
- **Demo Owner Login**:
  - Email: `owner@demo.local`
  - Password: `Password123!`
  - PIN: `1234`
