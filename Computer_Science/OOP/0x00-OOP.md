#TOPICS
- [[0x01-Basic_Concepts]]
- [[0x02-Inheritance]]
- [[0x03-Polymorphism]]
	- [Super](https://www.youtube.com/watch?v=Qb_NUn0TSAU)
	- [Upcasting & Downcasting](https://www.youtube.com/watch?v=HpuH7n9VOYk)
- [[0x04-Types Of Relationships]]
- [[0x05-Abstraction]]
- [[0x06-Interface]]
- [[0x07-Throw Catch]]

**Python OOP Naming Conventions: Terms Demystified**

فهم المصطلحات في البرمجة كائنية التوجه (OOP) مهم جدًا لتفادي اللبس، خاصةً في لغة مثل بايثون. المصطلحات مثل: method, attribute, instance, parameter, وغيرها تُستخدم بطريقة دقيقة. إليك توضيحًا منهجيًا:

---

**1. Class**

- هي القالب (البلو برنت) الذي نستخدمه لإنشاء كائنات.
    
- تُكتب عادةً بحروف كبيرة في بايثون:
    

```python
class Car:
    pass
```

---

**2. Instance == object**

- هو كائن (Object) مُنشأ من الكلاس.
    

```python
my_car = Car()  # my_car is an instance of class Car
```

- نقول عليه "instance" لأنه نُسخة حية من الكلاس.
    

---

**3. Attribute**

- هو متغير يُخزن داخل كائن (أو الكلاس نفسه).
    
- نوعان:
    
    - **Instance Attribute**: خاص بكائن معين ويُكتب باستخدام `self`.
        
    - **Class Attribute (Static)**: مشترك بين كل الكائنات ويُكتب مباشرة في الكلاس.
        

```python
class Car:
    wheels = 4  # Class attribute
    
    def __init__(self, color):
        self.color = color  # Instance attribute
```

---

**4. Method**

- هي دالة داخل الكلاس وتُستخدم لتنفيذ وظائف متعلقة بالكائن أو بالكلاس.
    
- ثلاثة أنواع:
    
    - **Instance Method**: تعمل على كائن معين. تستقبل `self` كمُعامل أول.
        
    - **Class Method**: تعمل على الكلاس نفسه. تستقبل `cls` كمُعامل أول وتُزيّن بـ `@classmethod`.
        
    - **Static Method**: لا تتعامل مع الكائن ولا الكلاس. تُزيّن بـ `@staticmethod`.
        

```python
class Car:
    def drive(self):            # Instance method
        print(f"Driving {self.color} car")

    @classmethod
    def general_info(cls):      # Class method
        print("All cars have engines")

    @staticmethod
    def honk():                # Static method
        print("Beep!")
```

---

**5. Parameter vs Argument**

- **Parameter**: هو اسم المُدخل عند تعريف الدالة.
    
- **Argument**: هو القيمة الفعلية المُمررة عند استدعاء الدالة.
    

```python
def greet(name):  # 'name' is a parameter
    print("Hello", name)

greet("Ali")  # "Ali" is an argument
```

---

**6. Field**

- مصطلح يُستخدم أحيانًا كمرادف لـ Attribute، لكنه يُستخدم غالبًا في لغات أخرى (مثل Java). في بايثون، المصطلح الأقرب هو `attribute`.
    

---

**7. Property**

- خاصية (property) تُستخدم للوصول إلى سمات الكائن بطريقة تبدو كالوصول إلى متغير، لكنها تُنفذ دالة.
    

```python
class Person:
    def __init__(self, age):
        self._age = age

    @property
    def age(self):
        return self._age

p = Person(30)
print(p.age)  # تستخدم دالة لكن تظهر كأنها attribute
```

---

**ملخص بصري:**

|المصطلح|وظيفته|يظهر في|مثال|
|---|---|---|---|
|Class|تعريف القالب|في الكود|`class Car:`|
|Instance|كائن حي من الكلاس|أثناء التنفيذ|`car1 = Car()`|
|Attribute|متغير خاص بكائن أو بالكلاس|داخل الكلاس|`self.color`, `Car.wheels`|
|Method|دالة مرتبطة بالكلاس أو الكائن|داخل الكلاس|`def drive(self):`|
|Parameter|اسم مدخل في تعريف دالة|في التعريف|`def func(x):`|
|Argument|القيمة المُمررة إلى الدالة|عند النداء|`func(5)`|
|Property|واجهة ذكية للقراءة/الكتابة على attribute|داخل الكلاس|`@property`|

---

هل ترغب أن أعد لك ملخص Markdown جاهز للنسخ في Obsidian؟