# Liskov Substitution Principle (LSP) Summary

## التعريف

"الأنواع الفرعية يجب أن تكون قابلة للاستبدال مكان الأنواع الأساسية دون تغيير السلوك المتوقع."

بمعنى: أي كود مكتوب ليتعامل مع الـ **parent class** يجب أن يعمل بنفس الكفاءة لو استبدلناه بـ **child class**.

---

## متى نكسر LSP؟

1. الـ subclass يغير سلوك methods الأصلية بطريقة غير متوقعة.
    
2. الـ subclass يضيف قيود أو يقلل من قدرات الـ superclass.
    
3. الـ subclass يرمي Exceptions في حالات الـ superclass يعالجها طبيعي.
    

---

## مثال على كسر LSP

```python
class Bird:
    def fly(self):
        print("I can fly!")

class Penguin(Bird):
    def fly(self):
        raise Exception("Penguins can't fly!")  # هنا كسرنا LSP

def make_bird_fly(bird: Bird):
    bird.fly()

# الاستخدام
sparrow = Bird()
penguin = Penguin()

make_bird_fly(sparrow)  # تمام
make_bird_fly(penguin)  # هيكسر الكود

```

---

## الحل

نفصل الطيور الطائرة عن غير الطائرة.

```python
class Bird:
    pass

class FlyingBird(Bird):
    def fly(self):
        print("I can fly!")

class Penguin(Bird):
    def swim(self):
        print("I can swim!")

def make_bird_fly(bird: FlyingBird):
    bird.fly()

# الاستخدام
sparrow = FlyingBird()
penguin = Penguin()

make_bird_fly(sparrow)  # تمام
penguin.swim()          # تمام

```

---

## الخلاصة

- حافظ على أن الـ subclasses لا تغير سلوك الـ superclass.
    
- إذا اختلفت طريقة العمل جذرياً، استخدم composition أو abstraction بدلاً من الوراثة.