# 📘 SOLID Principle: OCP (Open/Closed Principle)

## ✅ التعريف:

**OCP** هو المبدأ الثاني من مبادئ SOLID، ويعني:

> "الكائنات (classes) يجب أن تكون **مفتوحة للإضافة**، لكنها **مغلقة للتعديل**."

يعني: تقدر تضيف سلوك جديد للكلاس **من غير ما تعدل عليه نفسه**.

---

## 🎯 الهدف من OCP:

| الفائدة                | التوضيح                                                          |
| ---------------------- | ---------------------------------------------------------------- |
| ✅ تسهيل التوسع         | تقدر تضيف وظائف جديدة بدون كسر الكود القديم                      |
| ✅ تقليل الأخطاء        | التعديلات أقل = فرص أخطاء أقل                                    |
| ✅ دعم الـ Polymorphism | التعامل مع الكلاسات الجديدة بنفس الطريقة بفضل الوراثة أو التركيب |

---

## ❌ مثال على كسر OCP:

```python
class DiscountCalculator:
    def calculate(self, customer_type, amount):
        if customer_type == "regular":
            return amount * 0.9
        elif customer_type == "vip":
            return amount * 0.8
        elif customer_type == "employee":
            return amount * 0.7
```

🔴 المشكلة:

- كل مرة تضيف نوع جديد (زي student)، لازم تعدّل على الكلاس.
    
- ده مخالف لمبدأ OCP.
    

---

## ✅ إعادة التصميم حسب OCP:

```python
from abc import ABC, abstractmethod

class DiscountCalculator(ABC):
    @abstractmethod
    def calculate(self, amount):
        pass

class RegularCustomer(DiscountCalculator):
    def calculate(self, amount):
        return amount * 0.9

class VipCustomer(DiscountCalculator):
    def calculate(self, amount):
        return amount * 0.8

class EmployeeCustomer(DiscountCalculator):
    def calculate(self, amount):
        return amount * 0.7
```

🔵 الآن:

- لما تضيف نوع جديد، كل اللي تعمله هو تضيف كلاس جديد يرث من `DiscountCalculator`.
    
- مش بتعدل على الكلاسات القديمة.
    

---

## 🧠 استخدام الكود:

```python
def print_final_price(calculator: DiscountCalculator, amount):
    final_price = calculator.calculate(amount)
    print(f"Final price: {final_price}")

customers = [RegularCustomer(), VipCustomer(), EmployeeCustomer()]
for c in customers:
    print_final_price(c, 100)
```

---

## 🧱 OCP + Composition:

لو عندك كلاس `Order` ممكن تستخدم الـ Composition:

```python
class Order:
    def __init__(self, customer: DiscountCalculator, amount: float):
        self.customer = customer
        self.amount = amount

    def final_price(self):
        return self.customer.calculate(self.amount)
```

---

## 🔁 قاعدة التلخيص:

> "لو احتجت تعدّل على كلاس علشان تضيف له ميزة جديدة → غالبًا أنت كاسر OCP."

---

## 📌 مفيد في:

- الأنظمة اللي بتتوسع كتير
    
- تصميم Plugins أو Features إضافية
    
- كتابة كود مرن وسهل التطوير