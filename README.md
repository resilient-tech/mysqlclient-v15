# MySQLClient for Frappe v15

**App Name:** `mysqlclient_v15`  
**App Title:** MySQLClient for v15  
**Publisher:** Resilient Tech  
**Email:** info@resilient.tech  
**License:** MIT

A custom Frappe app that overrides the default MariaDB database connection logic to enable the use of the `mysqlclient` Python package on Frappe v15.

---

## 🔧 What It Does

This app overrides `frappe.database.get_db()` to conditionally use a custom `MariaDBDatabase` class from `mysqlclient_v15.mysqlclient`. This is activated based on the `use_mysqlclient` flag in `site_config.json`.

Supports dynamic selection between:
- PostgreSQL
- Standard MariaDB
- MariaDB via `mysqlclient` (this app)

---

## ✅ Why Use This

- Improved compatibility with `mysqlclient`
- Performance optimization in specific environments
- Clean modular override approach for Frappe v15

---

## ⚠️ Risks & Considerations

- Must maintain compatibility with Frappe DB interface
- May conflict with future Frappe updates
- Affects all database operations globally
- Requires proper configuration in `site_config.json`

---

## 🚀 Setup Instructions

### 1. Install the App
```bash
bench get-app mysqlclient_v15
bench --site your-site install-app mysqlclient_v15
````

### 2. Enable in `site_config.json`

```json
{
  "db_type": "mariadb",
  "use_mysqlclient": 1
}
```

### 3. Ensure the override is active

In your `__init__.py` or `hooks.py`:

```python
from frappe import database
from mysqlclient_v15.custom_db import get_db

database.get_db = get_db
```

### 4. Restart Bench

```bash
bench restart
```

---

## 🔄 How to Disable

1. Set the flag to false or remove it from `site_config.json`:

```json
"use_mysqlclient": 0
```

2. Comment or remove the override:

```python
# database.get_db = get_db
```

3. Restart:

```bash
bench restart
```

4. (Optional) Uninstall the app:

```bash
bench --site your-site uninstall-app mysqlclient_v15
```

---

## 📦 App Structure

This app follows standard Frappe app conventions and can be extended with:

* Custom permissions
* Notifications
* Page/Doctype hooks
* Integration events

---

## 📧 Support

For support, contact: [info@resilient.tech](mailto:info@resilient.tech)

---



# Enjoy upto 4x faster database speeds! 🚀

#### Sponsor

[Aakvatech](https://github.com/Aakvatech-Limited)

#### License

MIT
