## 🧱 Composition vs Aggregation vs Association (in Python Context)

في البرمجة كائنية التوجه (OOP)، بنحب نوضح العلاقات بين الكائنات مش بس عن طريق الوراثة (Inheritance)، لكن كمان عن طريق إن كائن يحتفظ بكائن تاني جواه كـ **Attribute**. هنا بنبدأ ندخل في مفاهيم: **Association**، **Aggregation**، و**Composition**.


## 🧠 القاعدة الذهبية:

> ✅ استخدم الوراثة لما تكون العلاقة: "A **is** B"  
> ✅ استخدم composition / association لما تكون العلاقة: "A **has**  B"
### 🔹 Association

- **التعريف**: Association تعني وجود علاقة بين كائنين أو أكثر (مثل طالب ومعلم).
    دي أبسط علاقة ممكنة. الكائنات بتكون مستقلة، بس واحد منهم بيحتفظ بتاني كـ Attribute. العلاقة هنا "ارتباط" مش ملكية.
- **الخصائص**:
    
    - العلاقة قد تكون One-to-One أو One-to-Many أو Many-to-Many.
        
    - كل كلاس مستقل بذاته ويمكن أن يوجد بدون الآخر.
        
- **UML Representation**:
    
    - معلم لديه طلاب عديدون.  
        ![[Pasted image 20240318174319.png]]
        
    - الطالب قد يكون له عدة معلمين.  
        ![[Pasted image 20240318174350.png]]
        

```python
class Engine:
    def start(self):
        print("Engine started")

class Car:
    def __init__(self, engine):
        self.engine = engine  # Association

    def drive(self):
        self.engine.start()
        print("Car is moving")

engine = Engine()
car = Car(engine)
car.drive()
```

- الـ `Engine` اتخلق بره `Car`.
    
- الـ `Car` بس بيستخدمه، مش مسؤول عن حياته أو موته (يعني لو حذفنا `Car`، الـ `Engine` لسه عايش لو في حد تاني بيشاور عليه).
    
- العلاقة دي ممكن تكون (1:1) أو (1:many).
- **🗑️ Garbage Collector**: لو ما فيش مراجع تانية للكائن `engine`، هيتحذف تلقائيًا.
    

---

### 🔹 Composition

- **التعريف**: Composition علاقة أقوى من Association — الكلاس الأب يمتلك بالكامل الكائنات التي يتكون منها.
    
- **الخصائص**:
    
    - الجزء (Part) يتم إنشاؤه داخل الكلاس الأب.
        
    - لا يمكن أن يوجد بمفرده خارج الأب.
        
- **UML Representation**:  
    ![[Pasted image 20240318174634.png]]
    

```python
class Engine:
    def start(self):
        print("Engine started")

class Car:
    def __init__(self):
        self.engine = Engine()  # Composition

    def drive(self):
        self.engine.start()
        print("Car is moving")

car = Car()
car.drive()
```

- هنا `Car` هو اللي أنشأ `Engine` بنفسه.
    
- مفيش وسيلة إن `Engine` يعيش من غير `Car`.
    
- دي علاقة **جزء من كل**. لو حذفنا `Car`، محدش يقدر يستخدم `Engine`.
- **🗑️ Garbage Collector**: لما كائن `Car` يُحذف، يتم حذف `Engine` تلقائيًا.
    

---

### 🔹 Aggregation

- **التعريف**: Aggregation علاقة أضعف من Composition — الكلاس بيحتفظ بمرجع للكائنات لكن لا يملكها بالكامل.
    
- **الخصائص**:
    
    - الجزء يمكن أن يوجد بشكل مستقل.
        
    - نفس الجزء قد ينتمي لأكثر من كائن.
        
- **UML Representation**:  
    ![[Pasted image 20240318174625.png]]
    

```python
class Employee:
    def __init__(self, name):
        self.name = name

class Department:
    def __init__(self):
        self.employees = []  # Aggregation

    def add_employee(self, employee):
        self.employees.append(employee)

emp1 = Employee("Ali")
emp2 = Employee("Sara")
dep = Department()
dep.add_employee(emp1)
dep.add_employee(emp2)
```

- الموظفين مش created داخل `Department`، لكن `Department` بيملكهم كقائمة.
    
- لو حذفنا `Department`، الموظفين لسه موجودين لأنهم مستقلين.
    
- العلاقة دي مفيدة لما تكون الأجزاء ممكن تتشارك بين أكتر من كيان.

- **🗑️ Garbage Collector**: حذف `Department` لا يؤدي لحذف `Employee`، لأنهم مستقلين.
    

---

### 📌 Composition vs Aggregation vs Association:

| خاصية          | Association               | Composition       | Aggregation      |
| -------------- | ------------------------- | ----------------- | ---------------- |
| من ينشئ الجزء؟ | من الخارج غالبًا          | الكلاس الأب       | من خارج الكلاس   |
| من يملك الجزء؟ | لا ملكية – فقط ارتباط     | الأب يملك تمامًا  |   مشاركة جزئية   |
| يعتمد على؟     | العلاقة مرنة وغير ملزمة   | العلاقة قوية جدًا | العلاقة ضعيفة    |
| عند حذف الأب؟  | لا يتأثر – حسب وجود مراجع | الجزء يُحذف       | الجزء يبقى موجود |



![[Pasted image 20240318174545.png]]  
![[Screenshot (58).png]]

---

### 🔒 Garbage Collector في العلاقات:

- **Association**: لو الكائن ملوش مراجع، بيتحذف.
    
- **Aggregation**: حذف الكائن الرئيسي لا يؤثر على الأجزاء.
    
- **Composition**: حذف الكائن الرئيسي يحذف أجزاؤه تلقائيًا.
    

---

### ✨ متى تستخدم كل واحدة؟

- **Association** → علاقة مؤقتة أو خفيفة زي مدرس يدرّس لطالب.
    
- **Aggregation** → علاقة قوية لكن الجزء ممكن يعيش لوحده، زي إدارة فيها موظفين.
    
- **Composition** → الجزء جزء لا يتجزأ من الكل، زي المحرك جوه السيارة.
