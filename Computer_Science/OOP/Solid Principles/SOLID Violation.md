**مثال شامل ينتهك جميع مبادئ SOLID مع الشرح**

---

## الكود:

```python
class Report:
    def __init__(self, data):
        self.data = data

    def generate_report(self):
        # منطق إنشاء التقرير
        print(f"Generating report with {self.data}")

    def save_to_pdf(self, filename):
        # منطق الحفظ في PDF
        print(f"Saving report to {filename}.pdf")

    def send_email(self, email):
        # منطق إرسال التقرير عبر البريد
        print(f"Sending report to {email}")

class ReportPrinter:
    def print_report(self, report: Report):
        report.generate_report()
        print("Printing the report")

class Manager:
    def __init__(self):
        self.report = Report("some data")

    def work(self):
        self.report.generate_report()
        self.report.save_to_pdf("report")
        self.report.send_email("test@example.com")
```

---

## الشرح: أين تم انتهاك كل مبدأ من مبادئ SOLID؟

### 1. **SRP** (Single Responsibility Principle)

- **المشكلة:**
    
    - كلاس `Report` يقوم بثلاث مهام مختلفة:
        
        1. إنشاء التقرير.
            
        2. حفظ التقرير كـ PDF.
            
        3. إرسال التقرير عبر البريد.
            
    - كل مهمة من هذه المهام تعتبر سببًا مستقلًا لتغيير الكود.
        
- **الأثر:** أي تعديل في طريقة الحفظ أو الإرسال قد يؤثر على منطق إنشاء التقرير نفسه.
    

---

### 2. **OCP** (Open/Closed Principle)

- **المشكلة:**
    
    - إذا أردنا إضافة طريقة جديدة لحفظ التقرير (مثل الحفظ في قاعدة بيانات) سنضطر لتعديل كلاس `Report` مباشرة.
        
- **الأثر:** هذا يكسر المبدأ لأن الكلاس غير مغلق أمام التعديل.
    

---

### 3. **LSP** (Liskov Substitution Principle)

- **المشكلة:**
    
    - إذا أنشأنا كلاس فرعي من `Report` مثل `ReadOnlyReport` الذي لا يدعم الحفظ أو الإرسال، فهذا سيجعل الدوال ترمي استثناءات.
        
- **الأثر:** الكائنات من النوع الفرعي لن تكون قابلة للاستبدال بشكل كامل مع الكائنات من النوع الأصلي.
    

---

### 4. **ISP** (Interface Segregation Principle)

- **المشكلة:**
    
    - إذا قمنا بعمل Interface لتقرير يحتوي على `generate_report`, `save_to_pdf`, `send_email`، فالكلاسات التي لا تحتاج الإرسال أو الحفظ ستضطر إلى تنفيذها بدون حاجة.
        
- **الأثر:** يجبر الكلاسات على الاعتماد على وظائف لا تحتاجها.
    

---

### 5. **DIP** (Dependency Inversion Principle)

- **المشكلة:**
    
    - كلاس `Manager` يعتمد مباشرة على كلاس `Report` الملموس بدلاً من الاعتماد على abstraction (مثل Interface أو Abstract Class).
        
- **الأثر:** أي تغيير في `Report` قد يجبر `Manager` على التعديل، ولا يمكن بسهولة تبديل `Report` بتنفيذ آخر.
    

---

## ملخص الأخطاء:

- **SRP:** تعدد المهام داخل كلاس واحد.
    
- **OCP:** الحاجة لتعديل الكلاس لإضافة سلوك جديد.
    
- **LSP:** وجود كائنات فرعية غير متوافقة مع الأصل.
    
- **ISP:** إجبار الكلاسات على تنفيذ وظائف غير لازمة.
    
- **DIP:** الاعتماد على تفاصيل بدلاً من الاعتماد على تجريدات.
    

---

يمكننا لاحقًا إعادة تصميم هذا المثال بحيث نصلح الأخطاء الخمسة مرة واحدة.