# Interface Segregation Principle (ISP)

## الفكرة الأساسية

> Clients should not be forced to depend on methods they do not use

أي **class** أو **interface** يجب أن يكون متخصص، وما يجبرش العميل على استخدام أو تنفيذ وظائف غير ضرورية له.

---

## ❌ مثال مكسور (مخالفة ISP)

```python
from abc import ABC, abstractmethod

class Machine(ABC):
    @abstractmethod
    def print_doc(self, doc):
        pass

    @abstractmethod
    def scan_doc(self, doc):
        pass

    @abstractmethod
    def fax_doc(self, doc):
        pass

class OldPrinter(Machine):
    def print_doc(self, doc):
        print(f"Printing {doc}")

    def scan_doc(self, doc):
        raise NotImplementedError("Scan not supported")

    def fax_doc(self, doc):
        raise NotImplementedError("Fax not supported")
```

### المشكلة

`OldPrinter` مضطر يطبق `scan_doc` و `fax_doc` مع إنه لا يحتاجهم.

---

## ✅ مثال صحيح (تطبيق ISP)

```python
from abc import ABC, abstractmethod

class Printer(ABC):
    @abstractmethod
    def print_doc(self, doc):
        pass

class Scanner(ABC):
    @abstractmethod
    def scan_doc(self, doc):
        pass

class Fax(ABC):
    @abstractmethod
    def fax_doc(self, doc):
        pass

class OldPrinter(Printer):
    def print_doc(self, doc):
        print(f"Printing {doc}")

class ModernPrinter(Printer, Scanner, Fax):
    def print_doc(self, doc):
        print(f"Printing {doc}")

    def scan_doc(self, doc):
        print(f"Scanning {doc}")

    def fax_doc(self, doc):
        print(f"Faxing {doc}")
```

### الحل

تقسيم الـ interfaces إلى أجزاء صغيرة بحيث كل كلاس يورّث فقط ما يحتاجه.
![[Pasted image 20250810212210.png]]

![[isp_violation_vs_solution.png]]

---
وهنا ال ISP vs RSP بيكون واضح يعني آه أنا عندي method مترابطة فأنا هنا مكسرتش ال  SRP بس ال methods دي كسرت ال ISP عشان مش ضرورية لكل الكلاسات

الخلاصة:

- **SRP** بيركز على _مسؤولية واحدة للكلاس_.
    
- **ISP** بيركز على _إن كل كلاس ياخد بس الواجهات اللي هو محتاجها، من غير ما يتحمل methods مش بيستخدمها_.