# E-Commerce Hardware Store — Final Project 🎓

A full-featured, responsive e-commerce website built with PHP and MySQL, designed for selling computer hardware components. This project features a **Zero-Configuration Demo Mode** allowing anyone to run the full application locally with a single click—no web server or database installation required.

[![PHP](https://img.shields.io/badge/PHP-8.2-777BB4?style=for-the-badge&logo=php&logoColor=white)](#-technologies-used)
[![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)](#-technologies-used)
[![SQLite](https://img.shields.io/badge/SQLite-003B57?style=for-the-badge&logo=sqlite&logoColor=white)](#-the-demo-mode-architecture)
[![Bootstrap](https://img.shields.io/badge/Bootstrap-5.3-7952B3?style=for-the-badge&logo=bootstrap&logoColor=white)](#-technologies-used)

---

## 🚀 Quick Start: Zero-Config Demo Mode

Want to test the project immediately without setting up XAMPP, Apache, or MySQL? 

Just double-click the included script (Windows):
```bat
Start-Demo.bat
```

**What happens under the hood?**
1. The script automatically downloads a portable version of PHP 8.2 (if not already present).
2. It initializes a self-contained **SQLite** database containing sample products, categories, and brands.
3. It starts the built-in PHP web server.
4. It opens your default web browser to `http://localhost:8080`.

### 🔑 Demo Accounts

| Role | Username | Password |
|------|----------|----------|
| **Admin** | `morad` | `123456` |
| **Customer** | `amine` | `Amine2002+` |

*(Note: You can access the admin panel by typing `0000` into the search bar!)*

---

## ✨ Key Features

### 🛒 For Customers
* **Dynamic Product Catalog**: Browse products with real-time filtering by Brand (Nvidia, Intel, AMD, etc.) and Category (CPU, GPU, RAM, Motherboard).
* **Smart Search System**: Keyword-based search with a hidden easter egg (`0000`) for quick admin access.
* **Guest Shopping Cart**: Add items to your cart without creating an account. The system tracks guests securely using their IP address (handling proxies and load balancers).
* **Discount Engine**: Automated rule-based discounts (e.g., 50% off based on cart item quantity).
* **User Accounts**: Registration with strict validation (9-digit phone numbers, complex passwords, unique emails), profile management, and order history tracking.
* **Checkout & Payment**: Secure checkout flow offering both Online (PayPal) and Offline (Cash on Delivery) payment methods.

### ⚙️ For Administrators
* **Secure Dashboard**: Protected admin panel with prepared SQL statements.
* **Full CRUD Operations**: Manage Products (with 4-image galleries), Categories, Brands, and Discount Rules.
* **Order Management**: Track customer orders, manage payments, and view invoice details.
* **User Management**: View and manage registered customer accounts.

---

## 🏗️ The Architecture & Techniques

This project was built from scratch without relying on heavy MVC frameworks, demonstrating a deep understanding of core web development concepts.

### 1. The Dual-Database Adapter Pattern
The most unique technical feature of this project is its ability to seamlessly switch between **MySQL** (for production) and **SQLite** (for the zero-config demo mode) **without modifying a single line of application code**.

* **How it works**: In demo mode, a custom adapter class (`SQLiteDemoConnection`) intercepts standard `mysqli_*` function calls (like `mysqli_query` or `mysqli_fetch_assoc`) and translates them into PHP Data Objects (PDO) calls for SQLite. It even translates MySQL-specific SQL syntax (like `ORDER BY RAND()`) into SQLite syntax (`ORDER BY RANDOM()`) on the fly.

### 2. Custom Front Controller (Router)
The demo mode utilizes a custom `router.php` script that acts as a Front Controller. It intercepts HTTP requests, serves static assets (CSS, images, JS), and automatically injects the SQLite database connection before rendering any PHP page, simulating a traditional Apache server environment perfectly.

### 3. Procedural & Object-Oriented Mix
The core business logic is centralized in `functions/common_function.php`, containing over 15 pure functions responsible for everything from rendering the UI components to calculating cart totals. The database adapter utilizes Object-Oriented Programming (OOP) to encapsulate the PDO logic.


---

## 🎥 Project Demonstration

A complete video walkthrough of the project, showcasing the customer shopping experience, product catalog, search and filtering, cart and checkout system, user accounts, administration features, and the overall technical architecture.

### ▶️ Watch the Video

[![Project Demonstration](https://img.youtube.com/vi/aBU8aCfKNyw/maxresdefault.jpg)](https://youtu.be/aBU8aCfKNyw)

**Project Two: An E-commerce Website**

[Watch on YouTube](https://youtu.be/aBU8aCfKNyw)

---
## 💻 Technologies Used

### Backend
* **PHP 8.2**: The core server-side scripting language.
* **MySQL / MariaDB**: Relational database for the production environment.
* **SQLite**: Embedded database used exclusively for the portable Demo Mode.

### Frontend
* **HTML5 & CSS3**: Semantic markup and custom styling.
* **Bootstrap 5.3**: Utilized for the responsive grid system, cards, forms, and alert components.
* **Vanilla JavaScript (ES6)**: Used for interactive UI elements:
  * An automated, pausable hero image slider on the homepage.
  * A 4-image interactive product gallery with hover-to-swap functionality on product detail pages.
* **FontAwesome 6**: For scalable vector icons.

---

## 📁 Repository Structure

```text
📦 ecommerce-website
 ┣ 📂 admin_area/          # Admin dashboard and CRUD interfaces
 ┣ 📂 demo/                # Portable environment (Router, SQLite adapter, init scripts)
 ┣ 📂 functions/           # Core business logic (common_function.php)
 ┣ 📂 images/              # Static UI assets
 ┣ 📂 includes/            # Production database connection scripts
 ┣ 📂 user_area/           # Customer authentication and profile management
 ┣ 📜 Start-Demo.bat       # Windows launcher for Demo Mode
 ┣ 📜 cart.php             # Shopping cart interface
 ┣ 📜 checkout.php         # Payment processing and order creation
 ┣ 📜 display_all.php      # Full product catalog
 ┣ 📜 main.php             # Homepage with slider and random products
 ┣ 📜 product_details.php  # Individual product page with image gallery
 ┣ 📜 search_product.php   # Search results handler
 ┗ 📜 style.css            # Custom CSS overrides
```

---

## 🛡️ Security Implementation
* **SQL Injection Prevention**: Uses Prepared Statements in the admin area and the PDO wrapper in demo mode.
* **XSS Protection**: HTML special characters are escaped upon rendering.
* **Password Security**: Structured validation rules for password complexity during registration.
* **Session Management**: Secure PHP session handling for user state across the application.

---

*This project was developed as a 3rd year license professional computer science thesis/mémoire project to demonstrate full-stack web development capabilities, database architecture, and portable environment configuration.*
