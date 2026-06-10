[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=24112876&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student Email:** 26ai.tuanvh@vinuni.edu.vn
**Name:** Vu Hai Tuan

---

## Mo ta

Bai lab nay xay dung mot ETL pipeline don gian cho du lieu san pham. Pipeline doc du lieu tu `raw_data.json`, kiem tra chat luong du lieu, loai bo cac record khong hop le, chuan hoa category, tinh gia sau khi giam 10%, them timestamp xu ly va luu ket qua ra file `processed_data.csv`.

Phan observability duoc them bang cach in ra so record hop le va so record bi loai trong qua trinh validation. Bai lab cung co stress test de so sanh cach mot simple agent tra loi khi dung clean data va garbage data.

---

## Cach chay (How to Run)

### Prerequisites
```bash
pip install pandas
```

### Chay ETL Pipeline
```bash
python solution.py
```

Sau khi chay, file `processed_data.csv` se duoc tao hoac cap nhat trong thu muc hien tai.

### Chay Agent Simulation (Stress Test)
```bash
python generate_garbage.py
python -c "from agent_simulation import simulate_agent_response as s; print(s('What is the best electronic product?', 'processed_data.csv')); print(s('What is the best electronic product?', 'garbage_data.csv'))"
```

---

## Cau truc thu muc

```
├── solution.py              # ETL Pipeline script
├── raw_data.json            # Du lieu dau vao
├── processed_data.csv       # Output cua pipeline
├── generate_garbage.py      # Tao garbage_data.csv cho stress test
├── agent_simulation.py      # Simple agent simulation
├── experiment_report.md     # Bao cao thi nghiem
└── README.md                # File nay
```

---

## Ket qua

Pipeline da doc 5 records tu `raw_data.json`. Sau validation, co 3 valid records duoc giu lai va 2 errors dropped do du lieu khong hop le:

- `Mystery Box` bi loai vi `price = -10`.
- `Phone` bi loai vi `category` rong.

File `processed_data.csv` gom cac san pham hop le: Laptop, Chair va Monitor. Cot `category` da duoc chuan hoa sang Title Case, cot `discounted_price` da duoc tinh bang `price * 0.9`, va cot `processed_at` ghi lai thoi diem du lieu duoc xu ly.

Khi dung clean data, simple agent co the tim san pham electronics phu hop tu du lieu da xu ly. Khi dung garbage data, agent co the tra loi sai hoac gap loi do du lieu co duplicate ID, sai kieu du lieu, outlier va null value.
