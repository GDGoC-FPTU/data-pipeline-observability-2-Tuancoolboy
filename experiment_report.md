# Experiment Report: Data Quality Impact on AI Agent

**Student Email:** 26ai.tuanvh@vinuni.edu.vn
**Name:** Vu Hai Tuan
**Date:** 2026-06-10

---

## 1. Ket qua thi nghiem

Da chay `generate_garbage.py` de tao `garbage_data.csv`, sau do chay `agent_simulation.py` voi 2 bo du lieu: clean data va garbage data.

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | Agent: Based on my data, the best choice is Laptop at $1200. | 9 | Cau tra loi hop ly vi clean data chi giu lai records hop le va category electronics duoc chuan hoa. Laptop la san pham electronics co price cao nhat trong clean data. |
| Garbage Data (`garbage_data.csv`) | Agent: Based on my data, the best choice is Nuclear Reactor at $999999. | 2 | Cau tra loi sai ve mat thuc te vi garbage data co outlier cuc lon. Agent chi chon theo price cao nhat nen bi du lieu rac dan sai. |

Output khi chay test:

```text
Testing with CLEAN data:
Agent: Based on my data, the best choice is Laptop at $1200.

Testing with GARBAGE data:
Agent: Based on my data, the best choice is Nuclear Reactor at $999999.
```

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

Agent tra loi sai khi dung garbage data vi logic cua agent phu thuoc truc tiep vao chat luong du lieu dau vao. Trong file garbage data co duplicate ID, wrong data type, outlier va null value. Duplicate ID lam cho du lieu khong con dai dien ro rang cho tung san pham rieng biet. Wrong data type nhu price bang chu co the lam cac phep so sanh bi loi hoac thieu chinh xac. Null value lam mat thong tin quan trong nhu id hoac category. Nghiem trong nhat la outlier `Nuclear Reactor` co price `999999` va category `electronics`, nen agent tuong day la san pham electronics tot nhat chi vi no co gia cao nhat.

Ket qua nay cho thay simple agent khong hieu ngu canh that su cua san pham. No chi loc category va chon record co price lon nhat. Khi du lieu dau vao bi poisoned, agent van lam dung logic lap trinh nhung dua ra ket qua sai voi nguoi dung. Vi vay validation, cleaning va observability la cac buoc rat quan trong truoc khi dua du lieu vao agent hoac he thong RAG.

---

## 3. Ket luan

**Quality Data > Quality Prompt?** Dong y.

Prompt tot co the giup agent hieu yeu cau ro hon, nhung neu du lieu dau vao sai thi cau tra loi van co the sai. Trong thi nghiem nay, cau hoi khong thay doi, nhung khi doi tu clean data sang garbage data thi ket qua da sai ngay. Dieu do chung minh chat luong du lieu la nen tang quan trong de agent dua ra cau tra loi dang tin cay.
