**Dependency Inversion Principle (DIP) — مبدأ عكس الاعتماد**

---

## 🔧 الفكرة الرئيسية:

الدوائر (الموديولات) العليا **ما تعتمدش على** تفاصيل الدوائر السفلى، الاتنين يعتمدوا على **تجرد** (Abstract).

---

## 💡 ليه المبدأ دا مهم؟

- الكود بيبقى **قابل للتغيير** من غير ما تعدّل في الدوائر العليا.
    
- تقدر تستبدل تفاصيل التطبيق بسهولة.
    
- تعزل التغييرات عن باقي النظام.
    

---

## 🗒️ مثال (نسخة مكسورة):

```python
class MySQLDatabase:
    def connect(self):
        print("Connecting to MySQL...")

class UserService:
    def __init__(self):
        self.db = MySQLDatabase()  # اعتماد مباشر على تفاصيل
    def get_user(self):
        self.db.connect()
```

**🚫 المشكلة**: UserService مرتبط ب MySQL مباشرةً، مش قابل لتغيير قاعدة البيانات بسهولة.

---

## 🛠️ مثال (حل مطبّق ل DIP):

```python
from abc import ABC, abstractmethod

class Database(ABC):
    @abstractmethod
    def connect(self):
        pass

class MySQLDatabase(Database):
    def connect(self):
        print("Connecting to MySQL...")

class PostgreSQLDatabase(Database):
    def connect(self):
        print("Connecting to PostgreSQL...")

class UserService:
    def __init__(self, db: Database):
        self.db = db  # اعتماد على تجرد
    def get_user(self):
        self.db.connect()

# تشغيل
mysql_service = UserService(MySQLDatabase())
pg_service = UserService(PostgreSQLDatabase())
```

**💡 الفائدة**: UserService الدوقتي مش متقيّد بنوع ديتابيز معيّن، وتقدر تغيّر ال Implementation بسهولة.

---

## 📖 خلاصة:

- دائما خلّي الكود المهم يعتمد على **Interfaces / Abstract classes**.
    
- تفاصيل التطبيق تتبع التجرد مش العكس.