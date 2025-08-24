# 🐍 Object-Oriented Programming in Python (Basics)

## What is a Class?
- A class is a **blueprint** for creating objects.
- Example: A `Car` class with attributes and methods.

```python
class Car:
    def __init__(self, brand=None, model=None, year=None):
        self.brand = brand
        self.model = model
        self.year = year

    def display_info(self):
        print(f"Brand: {self.brand}")
        print(f"Model: {self.model}")
        print(f"Year: {self.year}")
```

##  What is an Object?
- An object is an **instance** of a class.
- Example:

```python
my_car = Car("Toyota", "Corolla", 2020)
my_car.display_info()
```

---

## Constructors in Python
- `__init__` is the constructor method in Python.
- It's automatically called when an object is created.

```python
class Person:
    def __init__(self, name):
        self.name = name
```

---

##  Encapsulation: Private vs Protected

### Protected (`_name`)
- Convention only – you can still access it.
- Like putting a “Please don’t touch” label.

```python
class Example:
    def __init__(self):
        self._protected = "I'm protected"
```

### Private (`__name`)
- Python performs **name mangling**.
- Harder to access from outside accidentally.

```python
class Example:
    def __init__(self):
        self.__private = "I'm private"

obj = Example()
print(obj._Example__private)  # Access with mangled name
```

### How to access Private (__name)
- you can still access it but with some knowledge 
- using name Mangling by adding the class name
```python
class Person:
    def __init__(self, name):
        self._greet = f"Hello {name}"     # Protected
        self.__secret = "Hidden data"     # Private

p = Person("Ali")
print(p._greet)              # مسموح ولكن غير منصوح به
print(p._Person__secret)     # ممكن ولكن ملتف (مخفي)
```

---

## Property Decorators (`@property`, `@setter`)
- Used to **control access** to private attributes.
- Let you access methods like attributes.

```python
class Email:
    def __init__(self):
        self._email = None

    @property
    def email(self):
        return self._email

    @email.setter
    def email(self, value):
        if "@" not in value:
            raise ValueError("Invalid email")
        self._email = value

user = Email()
user.email = "hello@example.com"
print(user.email)
```


##  `self` Keyword
- المفتاح الذي يربط الخصائص (attributes) بالنسخة (instance) نفسها.

```python
class Person:
    def __init__(self, name):
        self.name = name  # self تشير للكائن الحالي
```

---

## Class Attributes vs Instance Attributes
- Attributes التي تنتمي للكلاس نفسه مقابل تلك التي تنتمي للكائن.

```python
class Dog:
    species = "Canis"  # Class attribute

    def __init__(self, name):
        self.name = name  # Instance attribute
```

---

##  `__str__` and `__repr__`
- لعرض الكائن بشكل مفهوم عند طباعته

```python
class Book:
    def __init__(self, title):
        self.title = title

    def __str__(self):
        return f"Book: {self.title}"

    def __repr__(self):
        return f"Book('{self.title}')"
```

---

## Method Types: Instance, Class, Static
- **Instance Method**: يأخذ `self` كوسيط
- **Class Method**: يأخذ `cls` ويُزين بـ `@classmethod`
- **Static Method**: لا يأخذ `self` ولا `cls`

```python
class MathUtils:
    @staticmethod
    def add(x, y):
        return x + y

    @classmethod
    def description(cls):
        return f"Utility class: {cls.__name__}"
```

---

## Duck Typing
- مفهوم شهير في بايثون: "If it walks like a duck and quacks like a duck…"

```python
class Duck:
    def quack(self):
        print("Quack!")

def make_it_quack(duck):
    duck.quack()  # لا نهتم بالنوع، فقط بالواجهة
```

**Static Attributes**

في بايثون، يمكن تعريف الخصائص (Attributes) على مستوى الكائن (Instance) أو على مستوى الكلاس (Class). عندما نعرّف متغيرًا داخل الكلاس لكن خارج أي دالة، فهو خاص بالكلاس نفسه ويُعرف باسم "Static Attribute" أو "Class Attribute".

```python
class Dog:
    species = "Canis"  # Class attribute

    def __init__(self, name):
        self.name = name  # Instance attribute
```

- `species` هنا هو ثابت مشترك بين جميع الكائنات المشتقة من `Dog`.
    
- `self.name` خاص بكل كائن على حدة.
    

**Static Attributes vs Instance Attributes**

|الخاصية|Static Attribute|Instance Attribute|
|---|---|---|
|موقع التعريف|داخل الكلاس، خارج الدوال|داخل دالة (مثل **init**) باستخدام self|
|تخص من؟|الكلاس وكل الكائنات|الكائن الحالي فقط|
|إمكانية التغيير|ممكن ولكن يؤثر على الجميع|مستقل لكل كائن|
|كيفية الوصول|ClassName.attribute أو self.|self.attribute|

**Static Methods**

هي دوال داخل الكلاس لكنها لا تتعامل مع كائن معين (`self`) ولا حتى مع الكلاس نفسه (`cls`). تُستخدم عندما لا تحتاج الدالة للوصول إلى خصائص الكلاس أو خصائص الكائن.

يتم تزيينها باستخدام `@staticmethod`

```python
class MathUtils:
    @staticmethod
    def add(x, y):
        return x + y

print(MathUtils.add(2, 3))  # 5
```

**Static Methods: When to Use Them?**

- عند وجود وظيفة منطقية مرتبطة بالكلاس لكنها لا تعتمد على حالته أو حاله أي كائن من الكلاس.
    
- للفصل المنطقي: تفصل المنطق الخاص بالكلاس في مكانه المناسب بدلًا من وضعه في ملف خارجي.
    
- مثال: أدوات رياضية، تحويل وحدات، التحقق من الصيغ، إلخ.
    

**Protected and Private Methods**

Python لا تدعم الحماية التامة للبيانات (مثل Java أو C++)، ولكنها تعتمد على **الاتفاقيات** (conventions):

- `_method()` → Protected: تُفهم على أنها مخصصة للاستخدام الداخلي، لكنها لا تُمنع تقنيًا.
    
- `__method()` → Private: تُفعل ميكانيكية **name mangling** لجعل الوصول صعبًا من الخارج.
    

```python
class Person:
    def __init__(self, name):
        self._greet = f"Hello {name}"     # Protected
        self.__secret = "Hidden data"     # Private

p = Person("Ali")
print(p._greet)              # مسموح ولكن غير منصوح به
print(p._Person__secret)     # ممكن ولكن ملتف (مخفي)
```

- الحماية الحقيقية في بايثون تعتمد على الاحترام المتبادل بين المطورين وليس على القيود الصارمة.
    

---

هل ترغب بإضافة هذا الملف إلى ملف الـ Obsidian لديك؟ يمكنني تهيئته لك أيضًا بتنسيق Markdown لو رغبت.

**Static Attributes**

في بايثون، يمكن تعريف الخصائص (Attributes) على مستوى الكائن (Instance) أو على مستوى الكلاس (Class). عندما نعرّف متغيرًا داخل الكلاس لكن خارج أي دالة، فهو خاص بالكلاس نفسه ويُعرف باسم "Static Attribute" أو "Class Attribute".

```python
class Dog:
    species = "Canis"  # Class attribute

    def __init__(self, name):
        self.name = name  # Instance attribute
```

- `species` هنا هو ثابت مشترك بين جميع الكائنات المشتقة من `Dog`.
    
- `self.name` خاص بكل كائن على حدة.
    

**Static Attributes vs Instance Attributes**

|الخاصية|Static Attribute|Instance Attribute|
|---|---|---|
|موقع التعريف|داخل الكلاس، خارج الدوال|داخل دالة (مثل **init**) باستخدام self|
|تخص من؟|الكلاس وكل الكائنات|الكائن الحالي فقط|
|إمكانية التغيير|ممكن ولكن يؤثر على الجميع|مستقل لكل كائن|
|كيفية الوصول|ClassName.attribute أو self.|self.attribute|

**Static Methods**

هي دوال داخل الكلاس لكنها لا تتعامل مع كائن معين (`self`) ولا حتى مع الكلاس نفسه (`cls`) موجودة فقط في ال `Class`. تُستخدم عندما لا تحتاج الدالة للوصول إلى خصائص الكلاس أو خصائص الكائن.

يتم تزيينها باستخدام `@staticmethod`

```python
class MathUtils:
    @staticmethod
    def add(x, y):
        return x + y

print(MathUtils.add(2, 3))  # 5
```

**Static Methods: When to Use Them?**

- عند وجود وظيفة منطقية مرتبطة بالكلاس لكنها لا تعتمد على حالته أو حاله أي كائن من الكلاس.
    
- للفصل المنطقي: تفصل المنطق الخاص بالكلاس في مكانه المناسب بدلًا من وضعه في ملف خارجي.
    
- مثال: أدوات رياضية، تحويل وحدات، التحقق من الصيغ، إلخ.
    

**Protected and Private Methods**

Python لا تدعم الحماية التامة للبيانات (مثل Java أو C++)، ولكنها تعتمد على **الاتفاقيات** (conventions):

#### 🔸 Protected Methods – `_method()`

- تُعتبر مخصصة للاستخدام الداخلي داخل الكلاس أو الكلاسات المشتقة منه (subclasses).
    
- يمكن الوصول إليها من خارج الكلاس، لكن من الأفضل **عدم فعل ذلك**.
    
- تُعتبر بمثابة "إشارة للمطورين" أن هذه الطريقة ليست جزءًا من الواجهة العامة.

```python
class Base:
    def _helper(self):
        print("I'm a protected method")

class Child(Base):
    def use_helper(self):
        self._helper()

b = Base()
b._helper()  # ممكن ولكن غير منصوح به

```
#### 🔸 Private Methods – `__method()`

- تُفعل **name mangling** تلقائيًا: أي أن `__method` تصبح داخل الكلاس مثل `_ClassName__method`.
    
- الهدف: **منع الوصول العرضي** للطرق الخاصة، لكن يمكن الوصول إليها بشكل ملتف.
    
```python
class Secret:
    def __hidden(self):
        print("This is a private method")

s = Secret()
# s.__hidden()  # خطأ
s._Secret__hidden()  # مسموح لكن ملتف

```
### ⚠️ ملاحظة مهمة:

- لا يوجد "private" أو "protected" حقيقي في بايثون.
- كتابة `__method()` لا تمنع الوصول تمامًا، لكنها تشير أن هذه الطريقة **ليست للاستخدام الخارجي أبدًا*
- الحماية الحقيقية في بايثون تعتمد على الاحترام المتبادل بين المطورين وليس على القيود الصارمة.
    

