# CSS Attribute Selectors + Pseudo-classes & Pseudo-elements — شاملة

## 1. `[attr]`

يختار أي عنصر يحتوي على الـ Attribute المحدد بغض النظر عن قيمته.

```css
[title] {
  color: blue;
}
```

## 2. `[attr="value"]`

يطابق إذا كانت قيمة الـ Attribute مطابقة تمامًا.

```css
input[type="text"] {
  border: 1px solid red;
}
```

## 3. `[attr^="value"]`

يطابق إذا كانت قيمة الـ Attribute تبدأ بالقيمة المحددة.

```css
a[href^="https"] {
  color: green;
}
```

## 4. `[attr$="value"]`

يطابق إذا كانت قيمة الـ Attribute تنتهي بالقيمة المحددة.

```css
a[href$=".pdf"] {
  color: purple;
}
```

## 5. `[attr*="value"]`

يطابق إذا كانت قيمة الـ Attribute تحتوي على النص المحدد كجزء من كلمة أخرى.

```css
a[href*="example"] {
  text-decoration: underline;
}
```

## 6. `[attr~="value"]`

الكلمة الكاملة تعني أن `[attr~="value"]` يبحث عن القيمة المحددة ككلمة منفصلة في سلسلة القيم، وليس كجزء من كلمة أخرى.

على سبيل المثال، لو عندك:

```html
<div class="btn active primary"></div>
```

الـ Selector:

```css
[class~="active"] {
  background: yellow;
}
```

سيطابق هذا العنصر لأن كلمة `active` موجودة بالكامل ضمن قيمة `class`، مفصولة عن البقية بمسافة. لكن إذا كانت القيمة `inactive` فلن يطابق، لأن `inactive` ليست كلمة منفصلة تساوي `active`، بل كلمة مختلفة تحتويها جزئيًا.



## 7. `[attr|="value"]`

القيمة أو التي تبدأ بها متبوعة بـ `-` تعني أن `[attr|="value"]` يطابق إذا كانت القيمة تساوي تمامًا `value` أو تبدأ بـ `value-`.

هذا غالبًا يُستخدم مع سمات مثل `lang` لتحديد اللغة.

على سبيل المثال:

```html
<p lang="en">Hello</p>
<p lang="en-US">Howdy</p>
<p lang="fr">Bonjour</p>
```

الـ Selector:

```css
[lang|="en"] {
  color: blue;
}
```

سيطابق الفقرة الأولى (`lang="en"`) والفقرة الثانية (`lang="en-US"`) لأن القيم إما تساوي `en` أو تبدأ بـ `en-`. لكنه لن يطابق الفقرة الثالثة (`lang="fr"`).

---

## 8. Pseudo-classes

### التعريف

Pseudo-classes تحدد حالة خاصة للعنصر.

- `:hover` → عند مرور الماوس.
    
- `:focus` → عند تركيز المؤشر داخل العنصر.
    
- `:required` → عناصر الإدخال المطلوبة.
    
- `:first-child` → أول ابن.
    
- `:last-child` → آخر ابن.
    
- `:nth-child(an+b)` → اختيار عنصر/عناصر بترتيب معين.


**مثال `:nth-child(-n+3)`**

```css
li:nth-child(-n+3) {
  background: yellow; /* أول 3 عناصر */
}
```

- `n` تبدأ من 0 وتزيد.
    
- `-n+3` يعني كل عنصر ترتيبه ≤ 3.


**اختيار 5 عناصر من العنصر السادس:**

```css
li:nth-child(n+6):nth-child(-n+10) {
  color: blue;
}
```

---

## 9. Pseudo-elements

### التعريف

Pseudo-elements تُستخدم لإنشاء أو تنسيق أجزاء من العنصر غير موجودة مباشرة في DOM.

- `::before` → يضيف محتوى قبل العنصر. غالبًا يستخدم مع `content` لإضافة نص أو أيقونة.
    
- `::after` → يضيف محتوى بعد العنصر.
    
- `::first-letter` → يحدد أول حرف في العنصر لتنسيقه.
    
- `::first-line` → يحدد أول سطر فقط.
    
- `::selection` → يحدد شكل النص عندما يقوم المستخدم بتحديده.


**مثال:**

```css
p::before {
  content: "→ ";
  color: blue;
}

p::first-letter {
  font-size: 2rem;
  color: red;
}

p::after {
  content: " ← نص مضاف";
  color: gray;
}
%% بتغير التحديد  بالماوس  %%
p::selection {
  background: yellow;
  color: black;
}
%% بتعمل تارجيت لل list-style-type %%
::marker {  color: red;  
  font-size: 23px;}
```

---

## 10. Combinators مع Attribute Selectors

تُستخدم لربط عناصر بناءً على علاقتها ببعض.

- `>` → ابن مباشر (Child Selector) — يختار العناصر الأبناء مباشرة فقط.
    
- `+` → الأخ التالي مباشرة (Adjacent Sibling) — يختار العنصر الذي يأتي فورًا بعد الآخر.
    
- `~` → كل الإخوة بعده (General Sibling) — يختار جميع الإخوة الذين يأتون بعد العنصر.
    

**أمثلة:**

```css
div > span { color: green; } /* أي span ابن مباشر لـ div */
h2 + p { font-style: italic; } /* p الذي يأتي مباشرة بعد h2 */
h2 ~ p { color: grey; } /* أي p يأتي بعد h2 في نفس المستوى */
```

---

## 11. ملاحظات حول `:has()`

Selector متقدم يختار عنصر إذا احتوى على عنصر آخر.

- يمكن اعتباره عكس `:has-not` (غير موجود رسميًا، لكن يمكن محاكاته).
    
- مفيد جدًا لاختيار الأبناء أو تغيير تصميم العنصر بناءً على محتواه.
    

**مثال:**

```css
div:has(span) {
  border: 1px solid red; /* إذا كان يحتوي على span */
}

article:has(h2 + p) {
  background: #f0f0f0; /* إذا كان داخله p بعد h2 مباشرة */
}
```