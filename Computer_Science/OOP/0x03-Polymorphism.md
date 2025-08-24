# 🧬 Polymorphism in Python (تعدد الأشكال)

## 🔹 ما هو Polymorphism؟

Polymorphism تعني "تعدد الأشكال". وهي قدرة نفس الواجهة (نفس اسم الدالة) على تنفيذ سلوك مختلف بحسب نوع الكائن.

> **مثال بسيط:**
> 
> - جميع الكائنات لديها دالة `speak()`، ولكن كل كائن يطبع صوت مختلف.
>     

```python
class Dog:
    def speak(self):
        print("Woof!")

class Cat:
    def speak(self):
        print("Meow!")

animals = [Dog(), Cat()]

for animal in animals:
    animal.speak()
```

## ✅ أنواع Polymorphism في Python:

### 1. **Method Overriding** (إعادة تعريف الدوال)

- يحدث داخل نظام الوراثة.
    
- الكلاس الابن يعيد تعريف دالة موجودة في الكلاس الأب.
    
- لما تنادي الدالة على كائن من الكلاس الابن، يتم تنفيذ النسخة الجديدة (وليس نسخة الأب).
    

```python
class Animal:
    def speak(self):
        print("Generic sound")

class Dog(Animal):
    def speak(self):
        print("Bark")

d = Dog()
d.speak()  # Bark
```

> 🔹 **هذا النوع هو أشهر أشكال Polymorphism في OOP.**

---

### 2. **Duck Typing**

- فلسفة بايثونية: _"إذا كان يتصرف كالبطة، فهو بطة!"_
    
- لا يهم نوع الكائن، بل المهم أنه يملك نفس الدالة أو الخاصية.
    

```python
class Duck:
    def quack(self):
        print("Quack")

class Person:
    def quack(self):
        print("I can quack like a duck")

def make_it_quack(thing):
    thing.quack()  # المهم أن فيه دالة quack

make_it_quack(Duck())     # Quack
make_it_quack(Person())   # I can quack like a duck
```

> ✅ Duck Typing = **Polymorphism بدون وراثة**

---

### 3. **Method Overloading (NOT supported natively)**

- في لغات مثل Java وC++: يمكنك تعريف أكثر من دالة بنفس الاسم ولكن بتواقيع مختلفة (عدد/نوع البراميتر).
    
- بايثون لا تدعم ذلك صراحةً، لكن ممكن تحاكيه باستخدام قيم افتراضية أو `*args`.
    

```python
class Math:
    def add(self, a, b=0, c=0):
        return a + b + c

m = Math()
print(m.add(1))        # 1
print(m.add(1, 2))     # 3
print(m.add(1, 2, 3))  # 6
```

> ❌ مفيش Overloading حقيقي في بايثون: لو عرّفت دالة بنفس الاسم مرتين، التانية هتغطي على الأولى.

---

## 🧠 مقارنة بين الأنواع:

|النوع|يعتمد على الوراثة؟|مدعوم في بايثون؟|الاستخدام|
|---|---|---|---|
|Method Overriding|✅ نعم|✅ نعم|عند إعادة تعريف دوال في الكلاس الابن|
|Duck Typing|❌ لا|✅ نعم|لما تتعامل مع كائنات بدون التحقق من نوعها|
|Method Overloading|❌ لا|⚠ جزئيًا (باستخدام *args)|لتعدد أشكال الدالة حسب عدد البراميتر|

---

## ✳️ العلاقة مع الـ Inheritance:

- **Polymorphism و Inheritance مرتبطين جدًا.**
    
- Inheritance بيوفر الأساس، وPolymorphism بيخلّي الكائنات تتصرف بطرق مختلفة رغم وجود نفس الواجهة.
    

---

## 📝 الخلاصة:

- **Polymorphism** = تعدد سلوكيات للدوال بنفس الاسم.
    
- **Overriding** = شكل من أشكاله (داخل الوراثة).
    
- **Duck Typing** = شكل مرن بدون وراثة.
    
- **Overloading** = غير مدعوم رسميًا، ولكن ممكن التحايل عليه.
    

> 🧪 حدد نوع polymorphism من السياق:
> 
> - لو فيه وراثة و`super().method()` → ده Overriding.
>     
> - لو بتتعامل مع كائن مش مهتم بنوعه، بس بيقدّم method معينة → ده Duck Typing.
>     
> - لو عندك دالة بتاخد عدد متغير من البراميتر → ده أسلوب Overloading.
>