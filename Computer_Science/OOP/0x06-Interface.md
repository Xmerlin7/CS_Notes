# 🐍 Abstraction and Interfaces in Python

## 🎯 ما هو المقصود بـ "Interface" في بايثون؟

في بايثون، لا يوجد نوع خاص اسمه `interface` زي لغات زي Java، لكن بنحقق نفس الفكرة باستخدام:

- `Abstract Base Classes (ABCs)` من مكتبة `abc`
    
- الزامية الدوال باستخدام `@abstractmethod`
    

يعني نقدر نقول إن **الـ interface في بايثون = كلاس تجريدي (ABC) فيه دوال مجردة**.

---

## 🧱 بناء واجهة مجردة (Abstract Interface):

```python
from abc import ABC, abstractmethod
# Data Class

class Report:

    def __init__(self, data):

        self.data = data

  

# Export Strategy Interface

class ReportExporter(ABC):

    @abstractmethod

    def export(self, report: Report):

        pass



class Animal(ABC):
    @abstractmethod
    def eat(self):
        pass

    @abstractmethod
    def sleep(self):
        pass

    def breathe(self):
        print("Breathing...")

    @staticmethod
    def info():
        print("This is an Animal abstract class")
```

- `@abstractmethod` بتجبر أي كلاس يرث `Animal` إنه يطبّق `eat()` و `sleep()`
    
- ممكن نضيف دوال عادية (زي `breathe`) أو static (زي `info`) عادي جدًا
    

---

## ✅ تطبيق عملي:

```python
class Dog(Animal):
    def eat(self):
        print("Dog is eating...")

    def sleep(self):
        print("Dog is sleeping...")

# استخدام الكائن:
dog = Dog()
dog.eat()
dog.sleep()
dog.breathe()
Animal.info()
```

---

## ⚖️ مقارنة سريعة:

|الجانب|Python ABC|
|---|---|
|الإنشاء|وراثة من `ABC`|
|الإلزام بتطبيق الدوال|كل `@abstractmethod`|
|دعم تنفيذ افتراضي|نعم – يمكن تعريف دوال عادية|
|دعم static methods|نعم|
|التعدد|يمكن الوراثة من أكثر من ABC|
|الهدف|فرض شكل (Contract) للكلاسات الفرعية|

---

## 🧠 الخلاصة:

- ✅ الـ ABCs بتديك طريقة لبناء هيكل Interface محترم في بايثون
    
- ✅ باستخدام `@abstractmethod` بتضمن إن الكلاسات الفرعية هتلتزم بتنفيذ الدوال المطلوبة
    
- ✅ بفضل المرونة في بايثون، تقدر تضيف دوال جاهزة + دوال static بسهولة
    

![[Pasted image 20240327162650.png]]