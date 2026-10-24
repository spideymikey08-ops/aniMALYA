# Aniya — Agricultural Navigation and Yield Activity Tracker

Aniya is a PHP/MySQL web application for tracking rice plots, plantings, watering and farm tasks,
harvest records, seed inventory, farm finances, and calendar dates. It includes a built-in
chat assistant ("Ask Ani") on every page.

## Project Structure

```text
Ani-chatbot2/
├── index.html              smart redirect (landing page or dashboard if logged in)
├── landing.html            welcome and onboarding page
├── landing.css             landing page styling
├── config.php              session, database connection, global error handler, JSON helpers
├── config.local.example.php  copy to config.local.php for custom database password / API key
├── aniyatrack.sql          database schema, auto-migrations + starter sample data
├── .gitignore              ignores local secrets and temp files
├── .htaccess               prevents direct browser access to sensitive files
│
├── assets/                 code shared across modules
│   ├── css/
│   │   ├── base.css        reset, colours, typography, page defaults
│   │   ├── layout.css      sidebar, main area, page header, responsive styles
│   │   └── components.css  cards, forms, buttons, tables, badges, toast
│   ├── js/
│   │   ├── core.js         api(), post(), toast(), templates, date helpers
│   │   └── layout.js       sidebar loader, active link highlighter, logout
│   └── images/             graphics and illustration assets
├── partials/
│   └── sidebar.html        the navigation menu markup (shared by all pages)
│
├── Auth/                   login.html, register.html, auth.js, auth.css + PHP backend
├── Dashboard/              index.html, dashboard.js, dashboard.css + PHP backend
├── Plots/                  plots.html, plots.js, plots.css + PHP backend
├── Tasks/                  watering.html, watering.js, watering.css + PHP backend
├── Inventory/              inventory.html, inventory.js (tabs), seeds.js, harvest.js + PHP
├── Finance/                finance.html, finance.js, finance.css + PHP backend
├── Calendar/               calendar.html, calendar.js, calendar.css + PHP backend
└── Chat/                   chat-widget.html, chat.js, chat.css, chat.php
```

---

## Step-by-Step XAMPP Setup Guide

### 1. Place the Project in XAMPP
Make sure this project folder is located inside your XAMPP web directory:
```text
C:\xampp\htdocs\Ani-chatbot2
```

### 2. Start Apache and MySQL
1. Open the **XAMPP Control Panel** (`C:\xampp\xampp-control.exe`).
2. Click **Start** next to **Apache**. (Status turns green)
3. Click **Start** next to **MySQL**. (Status turns green)

### 3. Import the Database in phpMyAdmin
1. Open your web browser and navigate to:
   [http://localhost/phpmyadmin/](http://localhost/phpmyadmin/)
2. Click on the **Import** tab at the top.
3. Click **Choose File** (or "Browse...").
4. Select `C:\xampp\htdocs\Ani-chatbot2\aniyatrack.sql`.
5. Scroll down and click **Import** (or **Go**).
6. phpMyAdmin will execute the script, creating the `aniyatrack` database along with tables, necessary column migrations, and starter sample records.

### 4. Database Password Configuration (If Applicable)
By default, XAMPP's MySQL `root` user has **no password**. If you have set a MySQL root password:
1. In the project folder, copy `config.local.example.php` to a new file named `config.local.php`.
2. Open `config.local.php` in a text editor and update:
   ```php
   <?php
   $pass = 'your-mysql-password';
   ```

### 5. Open the Web Application
1. In your browser, open:
   [http://localhost/Ani-chatbot2/](http://localhost/Ani-chatbot2/)
2. You will be greeted by the **Aniya Welcome Landing Page**.
3. Click **REGISTER** to create your user account (enter full name, email, phone, username, and password).
4. After registration, click **LOGIN** and sign in with your credentials.
5. You will be redirected to the **Dashboard** with full access to plots, tasks, inventory, finance, calendar, and the "Ask Ani" assistant.

> **Note**: Always access the application via `http://localhost/Ani-chatbot2/` in your browser. Do not double-click `.html` files directly (e.g. `file:///...`), because browser security restricts JavaScript `fetch()` on local file URLs.

---

## Chatbot Configuration (Optional)

- **Default / Offline Mode**: Without any configuration, "Ask Ani" answers questions regarding your farm's plots, tasks, harvests, seeds, and finances using built-in database queries.
- **AI Mode (Claude AI)**:
  To enable Claude AI answers:
  1. Open or create `config.local.php`.
  2. Add your Anthropic API key:
     ```php
     <?php
     define('ANTHROPIC_API_KEY', 'sk-ant-api03-...');
     define('ANTHROPIC_MODEL', 'claude-3-5-haiku-20241022');
     ```
  *(Note: `config.local.php` is listed in `.gitignore` so your private key is never committed).*

---

## Features

- **Dashboard**: High-level farm KPIs (active plots, tasks due today, harvests this week) and quick summary cards.
- **Plots**: Add, edit, and delete rice plots; assign plantings, crop varieties, planted dates, and expected harvest dates.
- **Tasks**: Schedule activities (Water, Fertilize, Weed, Pest Control, Inspect, Other) and check them off.
- **C&I Inventory**: Manage seed stock with low-quantity alerts and log harvest yields.
- **Farm Finance**: Track expenses (seeds, fertilizer, labor, fuel, etc.) and income, with net balance calculations.
- **Calendar**: Interactive monthly calendar showing farm tasks, expected harvests, and completed harvests across the full 6-week view.
- **Ask Ani Chatbot**: Floating assistant on all pages ready to answer questions about your current farm records.
