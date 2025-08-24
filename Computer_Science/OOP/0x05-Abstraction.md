# 🧱 OOP Concept: Abstraction in Python

## 🔹 ما هو Abstraction؟
Abstraction هو مبدأ في OOP هدفه إخفاء التفاصيل الداخلية المعقدة، وتقديم واجهة بسيطة وواضحة للمستخدم.

> ✅ "المستخدم يهمه يشغّل الوظيفة، مش يعرف إزاي الكود جوّه شغّال."

---

## 🧪 مثال عملي: `MusicPlayer`

```python
mp = MusicPlayer()
mp.play("Night Drive.mp3")
mp.pause()
```

---

## ✨ كيف يحقق الكلاس Abstraction؟

### ✅ 1. واجهة علنية بسيطة:
```python
def play(self, song_name)
def pause(self)
```
- دي الدوال اللي بيتعامل معاها المستخدم.
- لا يحتاج المستخدم معرفة تفاصيل تحميل أو تشغيل الأغنية.

### 🔐 2. تفاصيل داخلية مخفية:
```python
def __load_song(self, song_name)
def __start_playback(self)
def __pause_playback(self)
```
- الدوال دي خاصة (private) باستخدام `__`
- بتخفي التفاصيل الداخلية من المستخدم، ودي جوهر الـ abstraction

---

## 🎯 لماذا abstraction مهم؟
- يقلل من التعقيد
- يسهل تعديل الكود بدون التأثير على واجهة الاستخدام
- يحمي الكود من الاستخدام غير المقصود

---

## 📌 ملخص سريع:
| العنصر                          | وظيفته                          |
|-------------------------------|---------------------------------|
| `play()` / `pause()`          | الواجهة البسيطة للمستخدم        |
| `__load_song()` وغيره         | منطق داخلي مخفي                |
| `__` (double underscore)      | convention لتحديد الدوال الخاصة |

---

## ✅ الكود التطبيقي:

```python
class MusicPlayer:
    def __init__(self):
        pass

    def play(self, song_name):
        # Public method representing the abstraction
        # The user calls play() without needing to know how the song is loaded or played internally
        self.__load_song(song_name)
        self.__start_playback()

    def pause(self):
        # Another public method; the internal implementation is hidden from the user
        self.__pause_playback()

    # --- Internal (abstracted) methods ---

    def __load_song(self, song_name):
        print(f"Loading song: {song_name}")

    def __start_playback(self):
        print("Now playing")

    def __pause_playback(self):
        print("Playback paused.")

# --- Example usage ---

mp = MusicPlayer()
mp.play("Night Drive.mp3")
mp.pause()
```

## 🔖 علاقة Abstraction بمبادئ SOLID:

- تستخدم مع **OCP (Open/Closed Principle)** عشان تفصل ما بين الواجهة والتنفيذ
    
- تدعم **Polymorphism** لما تربط بين واجهات مجردة (مثل ABCs) وتطبيقات مختلفة
    
- **تستخدم ABC (Abstract Base Classes)** لتحقيق abstraction رسمي في بايثون، وده بيتم باستخدام مكتبة `abc`
    

---

## ✅ توضيح ABC و @abstractmethod في بايثون:

``` python
from abc import ABC, abstractmethod

class Customer(ABC):
    @abstractmethod
    def get_discount(self):
        pass
```

### 🧠 ما معنى هذا؟

- `ABC` معناها إن `Customer` هي **class مجرّدة (Abstract Class)** لا يمكن إنشاء كائنات منها.
    
- `@abstractmethod` تعني أن أي `subclass` لازم **يطبّق (override)** هذه الدالة.
    
- أي كلاس يرث من `Customer` **لازم يوفّر تعريف لـ** `get_discount()`، وإلا هيرمي خطأ.
    

### ✅ الهدف منها:

- فرض قواعد على الكلاسات المتفرعة.
    
- تمكين الـ Polymorphism في سياق مُنظم.
    
- ضمان إن كل الكلاسات المشاركة تتبع نفس الواجهة.
    

---

## 🌐 ملخّص سريع:

```text
Abstraction = استخدم دوال بسيطة علنية
             + أخفِي منطق التنفيذ الداخلي
             + حدّد سلوكيات أساسية باستخدام ABC
```

- ✅ فكّر في "وش الكائن" اللي الناس بتتعامل معاه
    
- ✅ خبي المكنة من جوّه، وخلي التعامل سهل وواضح
    
- ✅ لو فيه سلوك لازم يتطبق = افرضه بـ `@abstractmethod`