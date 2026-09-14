# Laboratory System — Web Lab 1 (NICE UI + Borrow Approval)

This version keeps the polished NICE UI and reuses the original Python database/controller logic. Flask is the web bridge between the browser and the existing Python system.

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

The original Tkinter desktop views remain in `Laboratorysystem.py` for teaching comparison. The web app does not call `start_app()`.

### Borrow Quantity

Users select the number of units they want to borrow from the Hardware Catalog. The requested quantity is saved with the borrow request. Stock is not deducted while the request is pending; when an Admin approves the request, the approved quantity is deducted. Existing databases are automatically migrated so older borrow records receive quantity `1`.
