# Laboratory System — Web Lab 1 (UI + Borrow Approval)

This version keeps the polished UI and reuses the original Python database/controller logic. Flask is the web bridge between the browser and the existing Python system.

## Run locally

```powershell
conda activate gender_env
python -m pip install -r requirements.txt
python app.py
```

Then open Google Chrome:

`http://127.0.0.1:5000`

The terminal also prints the portal address when the server starts.

## Dashboard workflow

- User: choose a borrow quantity → request borrow → Admin approval → item becomes BORROWED and stock decreases by the approved quantity.
- User: request return → Admin approval → item becomes RETURNED and stock increases by the borrowed quantity.
- Admin: approve/reject borrow requests, approve/reject returns, process password resets, manage hardware, and review Borrow Audit.
- Dashboard uses Total Stocks, Borrowed Items, Pending Borrow Requests, Pending Returns, and Password Reset Requests instead of Total Asset Valuation / Visible Items.

## Important

The original Tkinter desktop views remain in `Laboratorysystem.py` for comparison. The web app does not call `start_app()`.

### Borrow Quantity

Users select the number of units they want to borrow from the Hardware Catalog. The requested quantity is saved with the borrow request. Stock is not deducted while the request is pending; when an Admin approves the request, the approved quantity is deducted. Existing databases are automatically migrated so older borrow records receive quantity `1`.


## Lab 2: Supabase PostgreSQL

This version keeps the original desktop code and web interface, but can use Supabase PostgreSQL when the `DATABASE_URL` environment variable is set. Without `DATABASE_URL`, it continues to use the original SQLite database for Lab 1.

### 1. Install dependencies

```powershell
python -m pip install -r requirements.txt
```

### 2. Migrate the original SQLite database

Place `hardware_inventory.db` beside `migrate_sqlite_to_postgresql.py`, set `DATABASE_URL` to the Supabase Session Pooler URI, then run:

```powershell
python migrate_sqlite_to_postgresql.py
```

Do not upload `hardware_inventory.db` or `.env` to GitHub.

### 3. Test the web app with Supabase

Set `DATABASE_URL` in the same PowerShell session and run:

```powershell
python app.py
```

The Flask app will use Supabase instead of SQLite while the original Tkinter classes remain in `Laboratorysystem.py` as desktop-only code.
