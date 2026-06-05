# Marketplace — Android Shopping App

A full-stack Android marketplace app where buyers can browse products by category, manage a cart and wishlist, and place orders — while sellers manage their inventory, track sales, and list new products. Built with Java and a live MySQL backend on Google Cloud SQL.

---

## Screenshots

> _Add screenshots here once running on emulator_

---

## Features

### Buyer
- Browse products across 4 categories: **Food, Electronics, Fashion, Home Appliances**
- Add items to **cart** or **wishlist**
- **Checkout** with a live order total
- Orders automatically update seller inventory

### Seller
- **Dashboard** showing total revenue and top 5 best-selling products
- **Add** new products with name, quantity, price, and category
- **Update** product quantity and price
- **Delete** products from inventory
- **Inventory view** with full stock overview

### Auth
- Single login screen for both buyers and sellers
- Auto-registers new users on first login

---

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Android (Java), Material Design 3 |
| Database | MySQL 8.0 on Google Cloud SQL |
| Connectivity | JDBC via `mysql-connector-java-5.1.49` |
| Build | Gradle 8.9, AGP 8.7.0 |
| Min SDK | Android 12 (API 31) |

---

## Database Schema

7 tables: `buyers`, `sellers`, `product`, `warehouse`, `cart`, `wishlist`, `orders`

Two stored procedures:
- `sp1` — adds a product to inventory, creating a new product entry if it doesn't already exist
- `warehouse_quantity` — handles checkout: decrements stock, records the order, and clears the buyer's cart

---

## Getting Started

### Prerequisites
- Android Studio (Hedgehog or newer)
- A MySQL database (Google Cloud SQL or local)
- JDK 8+

### 1. Clone the repo

```bash
git clone https://github.com/KTB2110/MarketplaceAndroidStudio.git
cd MarketplaceAndroidStudio
```

### 2. Set up your database

Run `schema.sql` on your MySQL instance to create all tables and stored procedures, then run `data.sql` to load sample data.

### 3. Configure credentials

Create a `local.properties` file in the project root (this file is gitignored and never committed):

```properties
sdk.dir=YOUR_ANDROID_SDK_PATH
db.ip=YOUR_MYSQL_HOST_IP
db.name=cs348
db.user=YOUR_DB_USERNAME
db.pass=YOUR_DB_PASSWORD
```

### 4. Build and run

Open the project in Android Studio, sync Gradle, create an emulator (Pixel 6, API 33 recommended), and hit **Run**.

---

## Project Structure

```
app/src/main/java/com/example/cs348project/
├── ConnectionHelper.java       # JDBC connection using BuildConfig credentials
├── loginActivity.java          # Login + auto-registration
├── buyerHomeActivity.java      # Category selection grid
├── buyerActivity.java          # Product listing by category
├── cartActivity.java           # Shopping cart
├── checkoutActivity.java       # Order summary + place order
├── wishlistActivity.java       # Saved wishlist
├── SellerHomeActivity.java     # Seller dashboard + sales stats
├── AddActivity.java            # Add new product
├── InventoryActivity.java      # View full inventory
├── UpdateActivity.java         # Update price / quantity
└── DeleteActivity.java         # Remove product
```

---

## Security Note

Database credentials are never stored in the codebase. They are read from `local.properties` at build time via Gradle `buildConfigField` and injected into the app as `BuildConfig` constants. Never commit `local.properties`.

---

## Sample Accounts

After running `data.sql`, you can log in with these test accounts:

| Role | Username | Password |
|---|---|---|
| Seller | `smruti` | `1234` |
| Seller | `kris` | `1234` |
| Seller | `aadi` | `1234` |
| Seller | `dhruv` | `1234` |

Buyers can self-register on the login screen.
