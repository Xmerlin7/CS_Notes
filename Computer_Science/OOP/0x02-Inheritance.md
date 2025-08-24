# 🧱 OOP Concept: Inheritance in Python

## 🔹 Introduction to Inheritance:
Inheritance هو مفهوم مهم جدًا في البرمجة كائنية التوجه (OOP)، بيسمح لكلاس (ابن / فرعي / Derived) إنه يرث الخصائص والسلوك من كلاس آخر (أب / أساسي / Base).

- يساعد على إعادة استخدام الكود (Code Reusability)
- بيأسس علاقة هرمية بين الكلاسات

---

## 📚 Key Terminology:

- **Superclass (Parent / Base Class):** الكلاس اللي بيتم وراثة خصائصه ودواله.
- **Subclass (Child / Derived Class):** الكلاس اللي بيرث من الكلاس الأب.
- **`super()` keyword:** تُستخدم في بايثون للوصول إلى خصائص أو دوال الكلاس الأب من داخل الكلاس الابن.

---

## 🧱 Access and Inheritance in Python:

- **Public members:** متاحة في الكلاس الابن.
- **Private members (`__var`)**: لا يمكن الوصول لها مباشرة من الابن.
- **Protected members (`_var`)**: يمكن الوصول لها من الكلاسات الفرعية (باتفاقية، مش حماية حقيقية).

> ✅ بايثون ما فيهاش access modifiers حقيقية زي Java و C++، لكن بتعتمد على conventions.

---

## 🔁 Types of Inheritance in Python:

1. **Single Inheritance**: كلاس فرعي يرث من كلاس أب واحد.
2. **Multilevel Inheritance**: كلاس يرث من كلاس، وهو نفسه يُورّث منه.
3. **Hierarchical Inheritance**: كلاس واحد يكون أب لأكثر من كلاس فرعي.
4. **Multiple Inheritance**: كلاس يرث من أكتر من كلاس (مدعومة في بايثون).

---

## 🧰 Constructors in Inheritance:

- Constructors لا تُورّث، لكن يتم استدعاؤها تلقائيًا من الكلاس الأب عند إنشاء object من الكلاس الابن.
- `super().__init__()` تُستخدم لاستدعاء constructor الكلاس الأب يدويًا.

```python
class Person:
    def __init__(self, name):
        self.name = name

class Student(Person):
    def __init__(self, name, student_id):
        super().__init__(name)
        self.student_id = student_id
```

---

## 🔄 Method Overriding:

- الكلاس الابن يقدر يعيد تعريف دوال الكلاس الأب.
- لازم تحتفظ بنفس اسم الدالة وعدد البراميتر.

```python
class Animal:
    def speak(self):
        print("Animal sound")

class Dog(Animal):
    def speak(self):  # override
        print("Dog barks")
```

> ✅ بايثون ما بتستخدمش `@override`، مجرد أنك تعرّف الدالة بنفس الاسم بيكفي.

---

## 🧩 `super()` in Methods:

- بتُستخدم لاستدعاء دالة الكلاس الأب من جوه override في الابن.
- في الوراثة المتعددة، `super()` بيتبع ترتيب MRO (Method Resolution Order)، وده معناه إنه ممكن يعدي على كذا كلاس بالتتابع.

```python
class Animal:
    def speak(self):
        print("Animal speaks")

class Bird(Animal):
    def speak(self):
        print("Bird chirps")
        super().speak()

class Mammal(Animal):
    def speak(self):
        print("Mammal growls")
        super().speak()

class Bat(Bird, Mammal):
    def speak(self):
        print("Bat screeches")
        super().speak()

Bat().speak()
```

**الناتج سيكون:**
```
Bat screeches
Bird chirps
Mammal growls
Animal speaks
```

---

## 🧨 The Diamond Problem & MRO:

- بيظهر لما كلاس يرث من كلاسَين، وكل واحد منهم ورث من نفس الأب.
- بايثون بيحل المشكلة باستخدام ترتيب MRO تلقائيًا.
- ✅ super() تتبع ترتيب MRO: تبحث في الكلاسات بالترتيب اللي بيرجعه `YourClass.__mro__`

- تقدر تشوف MRO باستخدام:
```python
print(YourClass.__mro__)

```

---

## 🔒 Final Methods and Classes:

- بايثون ما فيهاش `final` زي Java أو C++، لكن ممكن تمنع override عن طريق رفع خطأ في الكود يدويًا.
- ممكن استخدام مكتبات زي `typing.final` (بدءًا من Python 3.8)

```python
from typing import final

class Base:
    @final
    def cannot_override(self):
        print("This method cannot be overridden")
```

> ✅ مش منتشرة قوي في بايثون، لكن مفيدة في المشاريع الكبيرة.

---

## 🧠 Summary:
| المفهوم               | في بايثون                  |
|------------------------|-----------------------------|
| extends keyword        | ❌ غير موجود                |
| `super()`              | ✅ موجود وفعال              |
| `@override`            | ❌ مش مطلوب                 |
| private/protected      | ✅ conventions فقط           |
| final                  | ❌ مش أساسي، لكن موجود في typing |
| multiple inheritance   | ✅ مدعومة بالكامل           |
| MRO                    | ✅ موجود لحل التعارض         |
| diamond problem        | ✅ محسومة تلقائيًا بـ MRO   |