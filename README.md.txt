# คู่มือติดตั้งและใช้งาน Jupyter Notebook (Local) ผ่าน PowerShell

คู่มือนี้สอนขั้นตอนการติดตั้งและเริ่มใช้งาน Jupyter Notebook บนเครื่อง Windows โดยใช้ **PowerShell** ทุกขั้นตอน ตั้งแต่เริ่มต้นจนใช้งานได้จริง

---

## 1. เปิด PowerShell

- กด `Win + X` แล้วเลือก **Windows PowerShell** หรือ **Terminal**
- หรือกด `Win` แล้วพิมพ์ `powershell` จากนั้นกด Enter

---

## 2. ตรวจสอบว่ามี Python แล้วหรือยัง

พิมพ์คำสั่งนี้ใน PowerShell:

```powershell
python --version
```

- ถ้าขึ้นเวอร์ชัน เช่น `Python 3.12.x` แปลว่ามีแล้ว ข้ามไปข้อ 3 ได้เลย
- ถ้าขึ้น error หรือไม่มีเวอร์ชัน ให้ไปดาวน์โหลดจาก [https://www.python.org/downloads/](https://www.python.org/downloads/)

> **สำคัญ**: ตอนติดตั้ง Python ให้ติ๊กช่อง **"Add python.exe to PATH"** ก่อนกด Install ไม่งั้นจะเรียกใช้จาก PowerShell ไม่ได้

หลังติดตั้งเสร็จ ให้ปิดแล้วเปิด PowerShell ใหม่ แล้วเช็คเวอร์ชันอีกครั้งเพื่อยืนยัน

---

## 3. อนุญาตให้รัน Script (ทำครั้งเดียว)

PowerShell ปกติจะบล็อกการรัน script บางส่วนที่ virtual environment ต้องใช้ (ไฟล์ `activate.ps1`) ให้ตั้งค่าอนุญาตด้วยคำสั่งนี้ (รันครั้งเดียวพอ):

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

ถ้าระบบถาม ให้พิมพ์ `Y` แล้วกด Enter

---

## 4. สร้างโฟลเดอร์โปรเจกต์บน Desktop และเข้าไปในโฟลเดอร์

```powershell
cd Desktop
mkdir jupyter-project
cd jupyter-project
```

โฟลเดอร์โปรเจกต์จะอยู่ที่ `C:\Users\ชื่อเรา\Desktop\jupyter-project`

---

## 5. สร้างและเปิดใช้งาน Virtual Environment

```powershell
# สร้าง virtual environment ชื่อ venv
python -m venv venv

# เปิดใช้งาน venv
.\venv\Scripts\Activate.ps1
```

เมื่อ activate สำเร็จ จะเห็นข้อความ `(venv)` ขึ้นด้านหน้า prompt เช่น:

```
(venv) PS C:\Users\ชื่อเรา\jupyter-project>
```

---

## 6. ติดตั้ง Jupyter Notebook

ขณะที่ `(venv)` ยัง active อยู่ ให้รัน:

```powershell
pip install notebook
```

รอจนติดตั้งเสร็จ (จะเห็นข้อความ `Successfully installed ...`)

> ถ้าอยากได้อินเทอร์เฟซรุ่นใหม่กว่า (JupyterLab) ให้ใช้คำสั่งนี้แทน/เพิ่มเติม:
> ```powershell
> pip install jupyterlab
> ```

---

## 7. เปิดใช้งาน Jupyter Notebook

ยังอยู่ใน PowerShell ที่ `(venv)` active อยู่ ให้รัน:

```powershell
jupyter notebook
```

หรือถ้าติดตั้ง JupyterLab ไว้:

```powershell
jupyter lab
```

ระบบจะ:
1. แสดง URL ใน PowerShell เช่น `http://localhost:8888/tree?token=...`
2. เปิดเบราว์เซอร์อัตโนมัติไปยังหน้า Jupyter

ถ้าเบราว์เซอร์ไม่เปิดเอง ให้คัดลอก URL ที่ขึ้นใน PowerShell ไปวางในเบราว์เซอร์เอง

> **ห้ามปิดหน้าต่าง PowerShell นี้** ระหว่างใช้งาน Jupyter เพราะเป็นตัวรันเซิร์ฟเวอร์อยู่เบื้องหลัง

---

## 8. การใช้งานเบื้องต้น

### สร้าง Notebook ใหม่
1. ที่หน้า Jupyter ให้กดปุ่ม **New** มุมขวาบน
2. เลือก **Python 3** (ipykernel)
3. จะได้ไฟล์ `.ipynb` ใหม่พร้อมใช้งาน

### เขียนโค้ดใน Cell
- พิมพ์โค้ด Python ลงใน cell
- กด `Shift + Enter` เพื่อรันและไปยัง cell ถัดไป
- กด `Ctrl + Enter` เพื่อรันโดยไม่เลื่อน cell

### เปลี่ยนประเภท Cell
- **Code**: สำหรับเขียนโค้ด
- **Markdown**: สำหรับเขียนข้อความ/หัวข้ออธิบาย (กด `M` ขณะเลือก cell แล้วกด Enter เพื่อแก้ไข)

### คีย์ลัดที่ใช้บ่อย

| คีย์ลัด | หน้าที่ |
|---|---|
| `Shift + Enter` | รัน cell แล้วไป cell ถัดไป |
| `A` | แทรก cell ด้านบน |
| `B` | แทรก cell ด้านล่าง |
| `D D` (กด D สองครั้ง) | ลบ cell |
| `M` | เปลี่ยนเป็น Markdown cell |
| `Y` | เปลี่ยนเป็น Code cell |
| `Ctrl + S` | บันทึกไฟล์ |

### บันทึกและปิดงาน
- บันทึกไฟล์ด้วย `Ctrl + S` หรือ File > Save
- กลับไปที่ PowerShell แล้วกด `Ctrl + C` เพื่อหยุดเซิร์ฟเวอร์ จากนั้นพิมพ์ `y` แล้วกด Enter เพื่อยืนยัน

---

## 9. ปิด Virtual Environment เมื่อใช้เสร็จ

```powershell
deactivate
```

---

## 10. ครั้งถัดไปที่จะใช้งาน (ไม่ต้องสร้าง venv ใหม่)

แค่เปิด PowerShell แล้วรัน:

```powershell
cd Desktop\jupyter-project
.\venv\Scripts\Activate.ps1
jupyter notebook
```

---

## 11. ปัญหาที่พบบ่อย

| ปัญหา | วิธีแก้ |
|---|---|
| รัน `Activate.ps1` แล้วขึ้น error "running scripts is disabled" | รันคำสั่งในข้อ 3 อีกครั้ง: `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser` |
| คำสั่ง `python` ไม่รู้จัก | ลง Python ใหม่แล้วติ๊ก "Add python.exe to PATH" หรือเปิด PowerShell ใหม่ |
| คำสั่ง `jupyter` ไม่รู้จัก | ตรวจสอบว่า `(venv)` ขึ้นหน้า prompt อยู่หรือยัง (ต้อง activate ก่อน) |
| พอร์ต 8888 ถูกใช้งานอยู่ | รันคำสั่ง `jupyter notebook --port 8889` แทน |
| ต้องการหยุดเซิร์ฟเวอร์ | กด `Ctrl + C` ใน PowerShell แล้วพิมพ์ `y` ยืนยัน |
| ต้องการติดตั้งไลบรารีเพิ่ม | รัน `pip install ชื่อไลบรารี` ขณะที่ `(venv)` active อยู่ |

---

## สรุปคำสั่งทั้งหมด (Quick Reference)

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser   # อนุญาต script (ทำครั้งเดียว)
cd Desktop                                                              # ไปที่ Desktop
mkdir jupyter-project                                                  # สร้างโฟลเดอร์โปรเจกต์
cd jupyter-project                                                     # เข้าโฟลเดอร์
python -m venv venv                                                    # สร้าง venv
.\venv\Scripts\Activate.ps1                                            # activate venv
pip install notebook                                                   # ติดตั้ง Jupyter Notebook
jupyter notebook                                                       # เปิดใช้งาน
deactivate                                                             # ปิด venv เมื่อใช้เสร็จ
```