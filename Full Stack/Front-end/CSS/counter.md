
# 📝 **CSS Counters – دليلك البسيط**

> 💡 الـ **CSS Counter** مش رقم عادي — هو **عداد تلقائي** تخلّيه المتصفح يزيد كل ما يلاقي عنصر معين.

مثلاً:
- عدّ الأقسام (`Section 1`, `Section 2`, ...)
- عدّ العناصر في قائمة
- ترقيم العناوين بدون HTML

---

## 🔢 1. إزاي يشتغل؟

الـ counter له **جزئين أساسيين**:

### 1. `counter-increment` → يزيد العداد
### 2. `counter()` أو `counters()` → يعرض الرقم

---

## 🧩 2. مثال بسيط: ترقيم العناوين

```css
body {
  counter-reset: section; /* يبدأ العداد من 0 */
}

h2::before {
  counter-increment: section;        /* يزيد 1 كل مرة */
  content: "القسم " counter(section) ": ";
}
```

```html
<h2>مقدمة</h2>
<h2>الفصل الأول</h2>
<h2>الفصل الثاني</h2>
```

### النتيجة:
```
القسم 1: مقدمة
القسم 2: الفصل الأول
القسم 3: الفصل الثاني
```

✅ العداد زاد تلقائيًا من غير ما تكتب الأرقام في HTML.

---

## 🧠 شرح الكود

| السطر                         | معناه                                     |
| ----------------------------- | ----------------------------------------- |
| `counter-reset: section;`     | أنشئ عداد اسمه `section` وابدأ من 0       |
| `counter-increment: section;` | كل ما تلاقي عنصر فيه هذا، زِد العداد بـ 1 |
| `counter(section)`            | اعرض قيمة العداد `section`                |

---

## 🔁 3. مثال: ترقيم العناصر في قائمة

```css
ol {
  counter-reset: item;
}

li::before {
  counter-increment: item;
  content: counter(item) ". ";
  font-weight: bold;
  color: #007BFF;
}
```

```html
<ol>
  <li>اول خطوة</li>
  <li>تاني خطوة</li>
  <li>تالت خطوة</li>
</ol>
```

> ✅ النتيجة: أرقام تظهر من CSS، مش من HTML

---

## 🎯 4. استخدامات حقيقية

| الاستخدام | الوصف |
|---------|-------|
| ترقيم الأقسام | `Section 1`, `Section 2`... |
| ترقيم الجداول | `Table 1`, `Figure 2` |
| عدّ العناصر | "فيه 5 منتجات" تلقائيًا |
| صفحات PDF | ترقيم الصفحات في التحويل لـ PDF |

---

## 🧰 5. أنواع الدوال

| الدالة | الاستخدام |
|-------|----------|
| `counter(name)` | يعرض الرقم البسيط |
| `counter(name, style)` | يعرض بالنمط (مثلاً: `decimal`, `lower-roman`, `upper-alpha`) |
| `counters(name, string)` | للعدّ المتداخل (مثلاً: 1.1, 1.2, 2.1) |

### مثال: أرقام رومانية
```css
h2::before {
  counter-increment: sec;
  content: counter(sec, upper-roman) " - ";
}
```
> النتيجة: `I -`, `II -`, `III -`

---

## 🔁 6. عدادات متداخلة (مثل 1.1, 1.2)

```css
body {
  counter-reset: section;
}

h2 {
  counter-reset: subsection;
  counter-increment: section;
}

h2::before {
  content: counter(section) ". ";
}

h3 {
  counter-increment: subsection;
}

h3::before {
  content: counter(section) "." counter(subsection) " ";
}
```

```html
<h2>فصل</h2>
  <h3>مقدمة</h3>
  <h3>تحليل</h3>
<h2>فصل</h2>
  <h3>تجربة</h3>
```

### النتيجة:
```
1. فصل
1.1 مقدمة
1.2 تحليل
2. فصل
2.1 تجربة
```

---

## ✅ 7. نصائح مهمة

| النصيحة | الشرح |
|--------|------|
| دائمًا ابدأ بـ `counter-reset` | لو نسيته، العداد مش يشتغل |
| اسم العداد حرّك | `section`, `item`, `step` — أي اسم |
| يشتغل في `::before` و `::after` بس | مش يشتغل في `content` مباشر |
| مناسب للعرض، مش للمنطق | لا تعتمد عليه في الوصول (accessibility) |

---

## 🚫 لا تستخدمه في:

- عدادات مهمة (مثل "السعر الكلي")
- بيانات ديناميكية من JavaScript
- إذا كان الترقيم مهم للإعاقة البصرية (يفضل HTML)

---
## ✅ خلاصة

| الخطوة | ما تعمله |
|-------|--------|
| 1 | `counter-reset` في الأب (مثل `body`) |
| 2 | `counter-increment` في العنصر اللي تبي يزيد |
| 3 | `counter(name)` في `content` علشان تعرض الرقم |
