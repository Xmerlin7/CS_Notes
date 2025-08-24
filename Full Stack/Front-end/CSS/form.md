
# 📝 **تغطية متقدمة لتزيين النماذج (Form Styling)**

إذا كنت بتحب تبني نماذج (Forms) احترافية، جميلة، وسهلة الاستخدام، فهذا الشرح لك.  
هنا راح نغطي من **الألف إلى الياء** — من الأساسيات إلى الحيل المتقدمة اللي يستخدمها المبرمجون المحترفون.

---

## 🔹 1. **احذف التصميم الافتراضي أولًا**

كل متصفح يضيف "ستايل" افتراضي للنماذج — وهذا يسبب مشاكل في التصميم.

### الحل: نظّف كل شيء أولًا
```css
input, select, textarea, button {
  border: none;
  outline: none;
  background: transparent;
  font-family: inherit;
  font-size: 100%;
  padding: 0;
  margin: 0;
}
```

> ✅ بعد هذا، أنت تبني التصميم من الصفر، وبطريقة موحدة على كل المتصفحات.

---

## 🔹 2. **تزيين الحقول (مثل: الاسم، الإيميل، الباسوورد)**

### مثال: حقل نصي جميل واحترافي
```css
.form-input {
  width: 100%;
  padding: 12px 16px;
  border: 2px solid #ddd;
  border-radius: 8px;
  font-size: 16px;
  color: #333;
  transition: all 0.3s ease;
}
```

### عند التركيز (Focus) — اجعله يبدو نشطًا
```css
.form-input:focus {
  border-color: #4CAF50; /* لون أخضر عند النقر */
  outline: 2px solid #4CAF50;
  outline-offset: 2px; /* مسافة بين الحد والآوتلاين */
  box-shadow: 0 0 0 4px rgba(76, 175, 80, 0.1); /* هالة خفيفة */
}
```

> 💡 النصيحة: لا تحذف `outline` أبدًا — لأنه مهم جدًا للمستخدمين اللي يستخدمون لوحة المفاتيح.

---

## 🔹 3. **تحديث خانات التأشير (Checkboxes) والإشعارات (Radio Buttons)**

الـ checkboxes الأصلية قبيحة ولا تُستَعرض بشكل موحد على المتصفحات.

### الحل: أخفِ الأصلية وابني واحدة جديدة

### الـ HTML
```html
<label class="custom-checkbox">
  <input type="checkbox" />
  <span class="checkmark"></span>
  أوافق على الشروط
</label>
```

### الـ CSS
```css
.custom-checkbox {
  display: flex;
  align-items: center;
  gap: 8px;
  cursor: pointer;
  user-select: none;
}

.custom-checkbox input {
  position: absolute;
  opacity: 0;
  z-index: -1;
}

.checkmark {
  width: 18px;
  height: 18px;
  border: 2px solid #999;
  border-radius: 4px;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: 0.2s;
}

/* عندما يتم التأشير */
.custom-checkbox input:checked + .checkmark {
  background: #4CAF50;
  border-color: #4CAF50;
}

.checkmark::after {
  content: "✓";
  color: white;
  font-weight: bold;
  opacity: 0;
  transform: scale(0);
}

.custom-checkbox input:checked + .checkmark::after {
  opacity: 1;
  transform: scale(1);
}
```

> ✅ النتيجة: خانة تأشير جميلة، مع تأثير دخول علامة الصح.

---

## 🔹 4. **الـ Dropdown (Select) المخصص**

الـ `<select>` لا يمكن تزيينه بشكل كامل. الحل؟ نبني واحد مخصص.

### نستخدم `div` بدل `select`، ونتحكم فيه بـ JavaScript.

لكن باختصار:
- نستخدم زرًا يُظهر قائمة عند النقر
- القائمة مبنية بـ `div` أو `ul`
- نستخدم `aria` لجعلها **مُيسّرة للإعاقة البصرية**

> سنعمل هذا معًا لاحقًا إذا أردت.

---

## 🔹 5. **الـ Floating Label (التسمية الطائرة)**

التسمية (Label) تكون داخل الحقل، وعند النقر عليها، ترتفع لأعلى.

### HTML
```html
<div class="floating-label">
  <input type="text" id="name" placeholder=" " />
  <label for="name">الاسم</label>
</div>
```

### CSS
```css
.floating-label {
  position: relative;
  margin: 20px 0;
}

.floating-label input {
  width: 100%;
  padding: 12px;
  border: 2px solid #ddd;
  border-radius: 8px;
}

.floating-label label {
  position: absolute;
  left: 12px;
  top: 12px;
  color: #777;
  pointer-events: none;
  transition: 0.3s;
}

/* عندما يكون في محتوى أو عند التركيز */
.floating-label input:focus + label,
.floating-label input:not(:placeholder-shown) + label {
  top: -10px;
  font-size: 12px;
  color: #4CAF50;
  background: white;
  padding: 0 4px;
}
```

> ✅ تجربة مستخدم رائعة، وتُستخدم في Google وMaterial Design.

---

## 🔹 6. **التحقق من الصحة (Validation) بصريًا**

أظهر للمستخدم إذا كان الحقل صحيحًا أو خاطئًا.

```css
input:valid {
  border-color: #4CAF50;
}

input:invalid {
  border-color: #f44336;
}

input:focus:invalid {
  outline-color: #f44336;
}
```

> ✅ أضف أيقونة (مثل علامة صح أو خطأ) باستخدام `::before` أو `::after`.

---

## 🔹 7. **سهولة الوصول (Accessibility)**

> ❗ لا تهمل هذا — هو **أساسي**.

### يجب أن يكون عندك:
- `label` لكل `input`
- `aria-invalid="true"` إذا كان الحقل خاطئًا
- `aria-describedby` للرسائل
- لا تُزِل `outline` بدون بديل

مثال:
```css
input:focus-visible {
  outline: 2px solid blue;
}
```

> ✅ فقط `focus-visible` يظهر عند المستخدمين اللي يستخدمون لوحة المفاتيح.

---

## 🔹 8. **وضع الليلي (Dark Mode)**

استخدم متغيرات CSS:

```css
:root {
  --bg: white;
  --border: #ddd;
  --focus: #4CAF50;
}

[data-theme="dark"] {
  --bg: #222;
  --border: #555;
  --focus: #66bb6a;
}

.form-input {
  background: var(--bg);
  border: 2px solid var(--border);
}

.form-input:focus {
  border-color: var(--focus);
  outline-color: var(--focus);
}
```

> 💡 غيّر الوضع بـ JavaScript:  
> `document.body.setAttribute("data-theme", "dark")`

---

## 🔹 9. **التنسيق باستخدام Flexbox أو Grid**

### مثال: صفان من الحقول
```css
.form-grid {
  display: grid;
  gap: 16px;
}

@media (min-width: 600px) {
  .form-grid {
    grid-template-columns: 1fr 1fr;
  }
}
```

> ✅ يناسب: الاسم الأول + الأخير، المدينة + الرمز البريدي، إلخ.

---

## 🔹 10. **تأثيرات صغيرة (Micro-Interactions)**

أضف لمسة احترافية:

```css
.form-input {
  transition: all 0.3s ease;
}

.form-input:focus {
  transform: scale(1.02);
  box-shadow: 0 0 10px rgba(76, 175, 80, 0.2);
}
```

أو اهتزاز عند الخطأ:
```css
@keyframes shake {
  0%, 100% { transform: translateX(0); }
  25% { transform: translateX(-4px); }
  75% { transform: translateX(4px); }
}

input:invalid:focus {
  animation: shake 0.5s ease;
}
```

---

## ✅ خلاصة: قائمة المراجعة

| ما يجب أن يكون موجودًا | ✔️ |
|------------------------|----|
| تنظيف التصميم الافتراضي | ✅ |
| تزيين الحقول الأساسية | ✅ |
| خانات تأشير مخصصة | ✅ |
| تسميات طائرة (Floating Labels) | ✅ |
| تحقق بصري (Validation) | ✅ |
| دعم الوضع الليلي | ✅ |
| تنسيق متجاوب (Responsive) | ✅ |
| تأثيرات ناعمة | ✅ |
| دعم سهولة الوصول (Accessibility) | ✅ |

---

## 👇 هل تحب نبني نموذج كامل معًا؟

قل لي:
> "عايز نبني نموذج تواصل كامل بـ تسميات طائرة وخانات مخصصة"  
أو  
> "روح معايا لـ Flexbox دلوقتي"

أنا معاك خطوة بخطوة — وأنت تتعلم بسرعة رهيبة! 💪🔥