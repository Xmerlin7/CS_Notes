
> 🔹 `transform` (blur, scale, translate)  
> 🔹 `animation` (from/to, 0%/50%, infinite)

---

# 🎯 **التحولات والتحريك في CSS**  
> "إزاي تُحرّك، تكبّر، تموّه، وتحوّل العناصر بسلاسة"

---

## 1. `transform` → "غير شكل العنصر من غير ما يأثر على غيره"

> ✅ التحويلات ما تأثرش على باقي العناصر  
> ✅ تتم في طبقة منفصلة (أسرع في الأداء)

### 🧩 الأنواع:

| الدالة | المعنى | مثال |
|-------|--------|------|
| `translate(x, y)` | يحرك العنصر | `transform: translate(20px, 10px)` |
| `scale(x, y)` | يكبّر أو يصغّر | `transform: scale(1.5)` |
| `rotate(angle)` | يدوّره | `transform: rotate(45deg)` |
| `skew(x, y)` | يميله | `transform: skew(10deg)` |

> ⚠️ لا يوجد `blur()` في `transform` — الـ `blur` بيتكتب في `filter`

---

### ✅ `filter: blur()` → "الضبابية" (موه النص أو الصورة)

```css
.blur {
  filter: blur(5px);
  filter: brightness(100%);
  filter: blur(2px) opacity(50%);
}
```

> ✅ يُستخدم في:
- صور خلفية مموهة
- تأثيرات عند الـ hover
- Loading states

> ❌ `transform: blur()` → **غير موجود**  
> ✅ الصحيح: `filter: blur(3px)`

---

### 💡 مثال عملي: زر يكبر عند الهوفر

```css
.button {
  padding: 12px 24px;
  background: #007BFF;
  color: white;
  border: none;
  transition: transform 0.3s ease;
}

.button:hover {
  transform: scale(1.1) translateY(-2px);
}
```

> النتيجة: الزر يكبر شوية ويرتفع — يعطي إحساس "بالضغط"

---

## 2. `animation` → "سلسلة حركات متتالية"

> ✅ تستخدم مع `@keyframes`  
> ✅ تتحكم في: من أين يبدأ، فين يمر، وينتهي

---

### 🔁 الطريقة: `from` و `to`

```css
@keyframes slideIn {
  from { transform: translateX(-100%); }
  to   { transform: translateX(0); }
}
```

> يعني: يبدأ من اليسار، ويتحرك للوسيط

---

### 📊 الطريقة: `0%`, `50%`, `100%`

```css
@keyframes pulse {
  0%   { transform: scale(1); opacity: 1; }
  50%  { transform: scale(1.2); opacity: 0.8; }
  100% { transform: scale(1); opacity: 1; }
}
```

> يعني: يكبّر، يصغر، يرجع — مثل "نبض"

---

### 🔧 استخدم التحريك مع:

```css
.element {
  animation: slideIn 2s ease-in-out;
}
```

| الخاصية | المعنى |
|--------|--------|
| `animation-duration` | المدة (مثلاً: `2s`) |
| `animation-timing-function` | نوع الحركة (`ease`, `linear`, `cubic-bezier`) |
| `animation-delay` | مؤخر كم ثانية قبل ما يبدأ |
| `animation-iteration-count` | كم مرة يكرر؟ |
| `animation-direction` | قدام، رجع، تبادل (`normal`, `reverse`, `alternate`) |
| `animation-fill-mode` | يحافظ على الحالة (`forwards`) |
| `animation-play-state` | `paused` أو `running` |

---

### ✅ `infinite` → "كرر الحركة للأبد"

```css
.loading {
  animation: spin 1s linear infinite;
}

@keyframes spin {
  to { transform: rotate(360deg); }
}
```

> ✅ يُستخدم في:
- أيقونات تحميل (Loading spinner)
- تأثيرات متكررة
- حركات ديكور

---

## 🧠 خلاصة: الفرق بين `transform` و `animation`

| السؤال | `transform` | `animation` |
|-------|-------------|-------------|
| هل يتحرك العنصر؟ | نعم، لحظي | نعم، على فترة |
| هل يكرر الحركة؟ | لا (إلا مع `transition`) | نعم، مع `infinite` |
| هل يمر بمحطات؟ | لا | نعم (`0%`, `50%`, `100%`) |
| هل يموّه؟ | لا | لا، لكن `filter: blur()` يموّه |

---

## ✅ نسخة جاهزة: نبض + تدوير

```css
@keyframes pulse-spin {
  0% {
    transform: scale(1) rotate(0deg);
  }
  50% {
    transform: scale(1.3) rotate(180deg);
    filter: blur(1px);
  }
  100% {
    transform: scale(1) rotate(360deg);
    filter: blur(0);
  }
}

.pulse-element {
  width: 100px;
  height: 100px;
  background: #ff6b6b;
  border-radius: 50%;
  animation: pulse-spin 2s ease-in-out infinite;
}
```

> النتيجة: دائرة تكبر، تدور، تموه شوية، وتعيد

---

## ✅ خلاصة واحدة تُخزن في دماغك

> - `transform`: **تغيير فوري** (تحريك، تكبير، تدوير)  
> - `filter: blur()`: **الضبابية** — مش في `transform`  
> - `@keyframes`: **المسار الكامل للحركة**  
> - `from/to` أو `0%/50%/100%`: **المحطات**  
> - `infinite`: **كرر للأبد** — زي الموسيقى في اللوب

