# 📘 SOLID Principle: SRP (Single Responsibility Principle)

## ✅ التعريف:

**SRP** هو أول مبدأ من مبادئ SOLID الخمسة.

> "كل كلاس يجب أن يكون مسؤولًا عن شيء واحد فقط، ويغير فقط لسبب واحد."

يعني: الكلاس المفروض يكون عنده **سبب واحد فقط للتغيير**. كل ما زادت مسؤولياته، زاد تعقيده، وصار التعديل فيه خطر.

---

## 🎯 الهدف من SRP:

| الفائدة         | التوضيح                                |
| --------------- | -------------------------------------- |
| ✅ تقليل التداخل | كل كلاس يكون واضح المهمة، وسهل التعديل |
| ✅ سهولة الصيانة | تعديل شيء ما ما يأثر على مسؤوليات أخرى |
| ✅ اختبار أسهل   | كل كلاس يُختبر بشكل معزول              |

---

## ❌ مثال على كسر SRP:

```python
class Order:
    def __init__(self, items):
        self.items = items

    def calculate_total(self):
        return len(self.items) * 20

    def save_to_db(self):
        print("Saving order to database")

    def send_email(self):
        print("Sending confirmation email")
```

🔴 المشكلة: كلاس `Order` بيحسب السعر، وبيحفظ في قاعدة البيانات، وبيبعت إيميل! 3 مسؤوليات مختلفة.

---

## ✅ إعادة التصميم حسب SRP:

```python
class Order:
    def __init__(self, items):
        self.items = items

class OrderCalculator:
    def calculate_total(self, order):
        return len(order.items) * 20

class OrderSaver:
    def save_to_db(self, order):
        print("Saving order to database")

class EmailSender:
    def send_email(self, email):
        print(f"Sending email to {email}")
```

🔵 الآن:

- `Order`: مسؤول فقط عن البيانات.
    
- `OrderCalculator`: مسؤول عن الحساب.
    
- `OrderSaver`: مسؤول عن الحفظ.
    
- `EmailSender`: مسؤول عن الإرسال.
    

> كل كلاس عنده مسؤولية واحدة. ولو حصل تعديل في منطق الحساب، مش هيأثر على منطق الحفظ.

---

## 💡 ملاحظات:

- SRP لا يعني "دوال قليلة"، بل "مسؤولية واضحة ومحددة".
    
- ممكن تستخدم composition لربط الكلاسات ببعض.
    

---
## 🔁 قاعدة التلخيص:

> "لو الكلاس بيجاوب على أكثر من سؤال (مثل: كيف أحسب؟ كيف أحفظ؟ كيف أرسل؟)، فغالبًا هو بيخالف SRP."

---

## 📌 مفيد في:

- تصميم الأنظمة القابلة للتوسعة
    
- كتابة كود نظيف وقابل للاختبار
    
- تقليل الأخطاء الناتجة عن تغييرات غير مباشرة