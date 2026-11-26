# LUXORA – Curated Living, Elevated Style

> **Interactive Mini E-Commerce Application**  
> Built for the **InternCircle Web Development Internship Assessment & Portfolio**.  
> Pure Vanilla Stack: Semantic HTML5, Minimal Luxury CSS3, and Vanilla JavaScript.

---

## 🌟 Overview

**LUXORA** is a modern lifestyle e-commerce boutique application inspired by high-end design houses such as Aesop, The Row, and Cuyana. It features a curated product catalog of 12 luxury items spanning Skincare, Accessories, Home Decor, and Lifestyle, complete with interactive shopping bag management, real-time total calculations, free shipping threshold tracking, wishlist persistence, and a validated demonstration checkout modal.

---

## 🚀 Key Features

1. **Curated Product Catalog (12 Items)**:
   - Dynamic JavaScript rendering via `renderProducts()` from a structured array of product objects.
   - Realistic Indian Rupee pricing (`₹349` to `₹1,499`) with formatted currency (`Intl.NumberFormat('en-IN')`).
   - High-resolution editorial lifestyle photography with automatic fallback SVG handling.
   - Interactive badge labels (*Bestseller*, *Staff Pick*, *Popular*, *Limited*, *New*).
   - Dynamic Star rating displays (e.g. ★ 4.9 (184)).
2. **Interactive Shopping Bag Drawer**:
   - Slide-in cart panel from the right with frosted glass backdrop blur.
   - Live quantity controls (`+` and `-`) with auto-removal when quantity reaches zero.
   - Individual item subtotal calculations.
   - **Free Delivery Progress Indicator**: Dynamically calculates remaining amount needed to reach the ₹2,000 Free Shipping threshold.
3. **Cart Calculations**:
   - Total items count: Calculated with JavaScript `reduce()`.
   - Subtotal & Grand Total: Calculated with `reduce()`.
   - Delivery fee rule: ₹49 flat delivery fee, automatically waived (FREE) when subtotal reaches ₹2,000 or above.
4. **LocalStorage Persistence**:
   - Cart contents (`luxora_cart`) persist across reloads and browser sessions.
   - Wishlist item IDs (`luxora_wishlist`) persist and update the live wishlist badge in the header.
5. **Search, Filter & Sort Controls**:
   - Real-time search by product name and description with clear button.
   - Category filtering (*All Products*, *Skincare*, *Accessories*, *Home Decor*, *Lifestyle*).
   - Multi-option sorting (*Featured*, *Price: Low to High*, *Price: High to Low*, *Highest Rated*).
   - Dedicated Wishlist view filter.
6. **Checkout Preview Modal & Order Confirmation**:
   - Accessible modal window displaying order itemization, subtotal, delivery fee, and final payable amount.
   - Complete form validation (Customer Name, Email regex validation, Address length check).
   - Instant order confirmation view with simulated unique order number (e.g. `LX-849204`).
   - Automatically clears cart and resets LocalStorage upon confirmed order.
7. **Responsive & Accessible**:
   - Tested down to 360px mobile width with zero horizontal overflow.
   - Semantic tags, visible `:focus-visible` gold rings, and `prefers-reduced-motion` compliance.

---

## 🛠️ How to Run the Project

### Option 1: VS Code Live Server (Recommended)

1. Open **Visual Studio Code**.
2. Click **File** → **Open Folder...** and select `C:\Users\BELL\.gemini\antigravity\scratch\luxora-store`.
3. If not already installed, install the **Live Server** extension by Ritwick Dey from the VS Code Extensions Marketplace (`Ctrl+Shift+X` → search "Live Server").
4. Right-click `index.html` in the file explorer and select **"Open with Live Server"** (or click **"Go Live"** in the status bar).
5. The application will launch in your browser at `http://127.0.0.1:5500/index.html`.

### Option 2: Direct Browser Launch

Double-click `index.html` or drag and drop it into Google Chrome, Microsoft Edge, Mozilla Firefox, or Safari.

---

## 🧩 Architectural Explanation

### 1. Dynamic Product Rendering (`renderProducts()`)
Instead of hardcoding cards into HTML, the entire product catalog is generated dynamically:
- `getProcessedProducts()` chains filtering (category, search keyword, wishlist state) and sorting (price ascending/descending, rating).
- `renderProducts()` maps the filtered array into semantic `<article class="product-card">` nodes using template literals with HTML escaping to prevent XSS vulnerabilities.
- Event listeners are attached cleanly to dynamic "Add to Bag" and "Wishlist" buttons.

### 2. Cart Calculations (`calculateCartTotal()`)
- Uses JavaScript `Array.prototype.reduce()` to calculate both total item count and monetary subtotal:
  ```javascript
  const totalItems = state.cart.reduce((sum, item) => sum + item.quantity, 0);
  const subtotal = state.cart.reduce((sum, item) => {
    const product = PRODUCTS.find(p => p.id === item.id);
    return sum + (product ? product.price * item.quantity : 0);
  }, 0);
  ```
- Evaluates the free shipping condition:
  ```javascript
  const deliveryFee = subtotal >= 2000 || subtotal === 0 ? 0 : 49;
  const grandTotal = subtotal + deliveryFee;
  ```
- All currency values are formatted via `new Intl.NumberFormat('en-IN', { style: 'currency', currency: 'INR', maximumFractionDigits: 0 })`.

---

## 📁 File Structure

```text
luxora-store/
├── index.html        # Semantic HTML5 layout and accessibility markup
├── style.css         # Minimal luxury design system, CSS grid, and responsive rules
├── script.js         # Products data, cart engine, calculations, and modal logic
├── README.md         # Comprehensive setup instructions and architecture notes
└── screenshots/      # High-resolution screenshots of the working store
    ├── catalog-desktop.png
    ├── cart-drawer.png
    ├── checkout-preview.png
    └── mobile-view.png
```

---

## 📄 License & Attribution

Assessment and portfolio project built for **LUXORA**. All product names and prices are fictional demonstration values. Product photography sourced from Unsplash under open editorial licenses.
