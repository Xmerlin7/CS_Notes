
# 🧠 Compilation Process in C (المعالجة الكاملة للكود)

![Compilation Diagram]![[Pasted image 20250721084352.png]]
---

## 🔄 مراحل تحويل الكود من Source إلى Executable

```text
1️⃣ Preprocessor
- يحلّ محل #include و #define ويزيل التعليقات
- ينتج كود موسّع (expanded source code)

2️⃣ Compiler
- يحوّل الكود إلى Assembly (لغة منخفضة المستوى)
- يتحقق من الأخطاء اللغوية والنحوية

3️⃣ Assembler
- يترجم كود الـ Assembly إلى Machine Code (object file)

4️⃣ Linker
- يربط ملفات الـ object مع بعضها (والدوال الخارجية من المكتبات)
- ينتج ملف تنفيذي واحد جاهز للتشغيل (.exe / a.out)
```

### 🔁 الـ Linker بيتعامل مع:
- `Other object files`: ملفات Object أخرى ناتجة من ترجمة ملفات مختلفة.
- `Libraries`: دوال جاهزة زي `printf` و `scanf` من مكتبة `libc` مثلًا.

---

## 🔍 الفرق بين `#include` و Linking

| العنصر | التوقيت | الوظيفة |
|--------|---------|----------|
| `#include` | Preprocessing | بيضيف إعلان الدالة فقط من Header |
| Linking   | بعد الترجمة | بيربط الكود الفعلي الحقيقي للدوال من مكتبات جاهزة |

❗ بدون Linking ➜ خطأ مثل:
```
undefined reference to 'printf'
```

---

## 📌 أمر `gcc` كمثال عملي:

```bash
gcc main.c -o my_program
```

- `main.c`: الكود المصدر
- `-o`: اسم الملف الناتج
- يقوم بكل الخطوات: Preprocess → Compile → Assemble → Link

