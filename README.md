# Warehouse Management System
### Group G22 — Topic 3 | Programming Techniques

| | |
|---|---|
| **Members** | Thieu Quang Minh (20227025) · Le Thi Thu Hien (20227109) · Nguyen Tuan Dung (20227191) |
| **Language** | Python 3.x |
| **Data storage** | JSON files (no external database required) |

---

## Project Structure

```
NhomG22_QuanLyKhoHang/
├── src/
│   ├── main.py          # Entry point — main menu loop
│   ├── models.py        # Data classes: SanPham (Product), GiaoDich (Transaction)
│   ├── storage.py       # Read / write JSON files
│   ├── inventory.py     # Add / edit / delete products, import & export stock
│   ├── search.py        # Search by code / name / category, low-stock filter
│   ├── report.py        # Monthly log report, inventory value statistics
│   └── categories.py    # Manage product category & unit-of-measure lists
├── data/
│   ├── products.json        # Product catalog
│   ├── transactions.json    # Import / export transaction log
│   └── categories.json      # Category & unit lists (auto-created on first run)
└── README.md
```

---

## Requirements

- **Python 3.7 or higher**
- No third-party libraries needed — only Python standard library (`json`, `os`, `datetime`)

Check your Python version:
```bash
python --version
# or
python3 --version
```

---

## How to Run

### 1. Prerequisites
- **Python 3.7 or higher**
- Thư viện xử lý ảnh `Pillow` (dùng để hiển thị logo HUST trên giao diện đồ họa GUI). Cài đặt bằng lệnh:
  ```bash
  pip install Pillow
  ```
  *(Lưu ý: Nếu không cài đặt `Pillow`, giao diện GUI vẫn khởi chạy bình thường nhưng sẽ tự động bỏ qua logo).*

### 2. Run the Application

Navigate into the `src/` folder and run `main.py`:

#### Chạy chế độ giao diện đồ họa (GUI - Mặc định)
```bash
python main.py
```
*Hệ thống sẽ khởi chạy giao diện cửa sổ trực quan hiện đại, hỗ trợ các chức năng bằng nút nhấn.*

#### Chạy chế độ dòng lệnh (CLI - Console)
Nếu bạn chạy trên máy chủ không có màn hình (headless) hoặc muốn sử dụng menu console truyền thống, hãy thêm tham số `--console`:
```bash
python main.py --console
```

> **Note:** Make sure you are inside the `src/` folder before running, so the program can find the `data/` files or the HUST logo correctly.

---

## Features & Menu Navigation

```
HE THONG QUAN LY KHO HANG - NHOM G22
======================================
  1. Quan ly danh muc san pham     → Product catalog management
  2. Nhap kho / Xuat kho           → Stock import / export
  3. Tim kiem san pham             → Product search
  4. Bao cao & Thong ke            → Reports & statistics
  0. Thoat chuong trinh            → Exit
```

### 1 · Product Catalog Management
| Option | Description |
|--------|-------------|
| View all products | Displays full table with stock status |
| Add new product | Shows existing products first to avoid duplicates; select category & unit from a managed list (add new ones on the fly) |
| Edit product | Shows full list → select by code → edit individual fields |
| Delete product | Only allowed when stock quantity = 0 |

### 2 · Stock Import / Export
- **Import:** Displays product table → enter product code → enter quantity & unit price → transaction is logged automatically with today's date.
- **Export:** Same flow; system validates that requested quantity does not exceed current stock. A warning is shown if stock drops below the minimum threshold after export.

### 3 · Product Search
| Option | Description |
|--------|-------------|
| Search by code | Exact match |
| Search by name | Partial keyword match (case-insensitive) |
| Search by category | Partial match |
| Low-stock alert | Lists all products at or below minimum threshold, sorted ascending by quantity |

### 4 · Reports & Statistics
| Option | Description |
|--------|-------------|
| Monthly log | Shows available data range first, then displays import/export log for the selected month/year |
| Inventory value | Full table sorted by value (descending) + breakdown by category with percentage |
| General stocktake | Summary: total products, total value, low-stock count, transaction count |

---

## Data Files

All data is stored as plain JSON in the `data/` folder and is updated automatically after every operation. You can open these files in any text editor to inspect or manually back up the data.

| File | Contents |
|------|----------|
| `products.json` | Product list (code, name, category, unit, stock qty, price, min threshold) |
| `transactions.json` | Every import/export transaction with date, quantity, and unit price |
| `categories.json` | User-managed lists of product categories and units of measure |

**10 sample products and 10 sample transactions** are included so you can explore all features immediately after launch.

---

## Sample Walkthrough

1. Run `python main.py` from the `src/` folder.
2. Select **1** → **1** to view all products in the catalog.
3. Select **2** → **1** to import stock for an existing product.
4. Select **2** → **2** to export stock (system will warn if quantity goes below minimum).
5. Select **3** → **4** to see which products are running low.
6. Select **4** → **1**, choose a year and month (e.g. 2025 / 5) to view the transaction log.
7. Select **4** → **2** to see the current total inventory value broken down by category.

---

## Notes

- All algorithms (search, sort) are implemented from scratch without built-in Python sorting or search functions, in accordance with course requirements.
- Transaction IDs are generated automatically (`GD0001`, `GD0002`, …).
- Product codes are case-insensitive and must be unique.
- Duplicate product names trigger a warning but can be overridden by the user.
- The `categories.json` file is created automatically on first run if it does not exist.
