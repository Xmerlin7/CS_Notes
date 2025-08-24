# 🐍 Python Exception Handling – Full Guide

## ❗ ما هي الاستثناءات (Exceptions)؟

الـ **Exception** هي حدث غير طبيعي يحصل أثناء تنفيذ البرنامج، ويؤدي إلى إيقاف التدفق الطبيعي للتنفيذ.

> أمثلة: القسمة على صفر، محاولة فتح ملف غير موجود، نوع بيانات غير متوقع، إلخ.

---

## 🧩 أنواع الاستثناءات في بايثون:

### 🔹 Built-in Exceptions:

- `ZeroDivisionError`
    
- `TypeError`
    
- `ValueError`
    
- `FileNotFoundError`
    
- `IndexError`
    

### 🔹 Custom Exceptions:

- تقدر تعمل Exception خاص بيك لو عايز تعبر عن خطأ محدد خاص بتطبيقك.
    

```python
class CustomError(Exception):
    def __init__(self, message):
        super().__init__(message)
```

---

## 🛠️ كيفية التعامل مع الاستثناءات:

### ✅ Try-Except:

```python
try:
    result = 10 / 0
except ZeroDivisionError:
    print("لا يمكن القسمة على صفر")
```

### ✅ Catch Multiple Exceptions:

```python
try:
    risky_code()
except (ValueError, TypeError) as e:
    print(f"حدث خطأ: {e}")
```

### ✅ Finally Block:

```python
try:
    open_file()
except FileNotFoundError:
    print("الملف غير موجود")
finally:
    print("نهاية المعالجة - يتم تنفيذ هذا دائمًا")
```

### ✅ Raise Exception:

```python
def divide(a, b):
    if b == 0:
        raise ZeroDivisionError("لا يمكن القسمة على صفر")
    return a / b
```

---

## 🧪 مثال تطبيقي:

```python
def divide(a, b):
    if b == 0:
        raise ZeroDivisionError("Division by zero")
    return a / b

try:
    result = divide(10, 0)
    print("Result:", result)
except ZeroDivisionError:
    print("خطأ: لا يمكن القسمة على صفر")
```

---

## ✅ أفضل الممارسات:

1. لا تترك الأخطاء بدون معالجة → عالجها بشكل واضح.
    
2. استخدم أنواع Exceptions دقيقة بدل `except:` العام.
    
3. استعمل `finally` في حالة وجود خطوات تنظيف (مثل إغلاق الملفات).
    
4. اكتب رسائل خطأ مفيدة تسهّل عليك التصحيح لاحقًا.
    
5. استخدم Custom Exceptions لما يكون عندك حالات خطأ منطقية خاصة بتطبيقك.
    

---

## 🧠 ملخص سريع:

|الأداة|الاستخدام|
|---|---|
|`try`|تغليف الكود اللي ممكن يرمي Exception|
|`except`|معالجة نوع الخطأ|
|`finally`|تنظيف أو تنفيذ كود دايمًا|
|`raise`|إطلاق (رمي) Exception يدويًا|
|`class ... Exception`|تعريف استثناء مخصص (Custom)|

---