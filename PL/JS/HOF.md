**Js Higher Order Functions**

---

### ✅ ما هي الـ Higher Order Functions؟

هي دوال يمكنها:

1. أخذ دوال أخرى كـ arguments.
    
2. أو إرجاع دالة (function) أخرى كناتج.
    

وهذا ما يجعلها "عالية المستوى" (Higher Order)، لأنها تتعامل مع الدوال كـ **قيم** (Values).

---

### ✳️ أولًا: First-class Functions vs Higher Order Functions

- **First-class functions** تعني أن الدوال في JavaScript تُعامل مثل أي قيمة أخرى (مثل رقم أو string).
    
    - يمكن تخزينها في متغير.
        
    - تمريرها كـ argument.
        
    - إرجاعها من دالة.
        

✅ إذًا: **Higher Order Functions** هي نتيجة طبيعية لدعم اللغة لـ First-class functions.

---

### 🧠 استخدامات HOFs في JavaScript:

- ✅ التكرار (`forEach`)
    
- ✅ التصفية (`filter`)
    
- ✅ التحويل (`map`)
    
- ✅ التجميع (`reduce`)
    
- ✅ العثور على عنصر (`find`)
    
- ✅ الفحص (`some`, `every`)
    

---

### 📌 أمثلة أساسية

```js
const numbers = [1, 2, 3, 4, 5];

// map: تحويل كل عنصر
const doubled = numbers.map(n => n * 2);

// filter: تصفية العناصر الزوجية
const even = numbers.filter(n => n % 2 === 0);

// reduce: جمع كل الأعداد
const sum = numbers.reduce((acc, curr) => acc + curr, 0);
```

---

### 🧪 تطبيق عملي - إنشاء HOF يدويًا

```js
function repeatNTimes(n, callback) {
  for (let i = 0; i < n; i++) {
    callback(i);
  }
}

repeatNTimes(3, (i) => console.log("Run #", i));
```

---

### 🔁 HOFs متقدمة: `compose` و `pipe`

```js
const add = x => x + 1;
const double = x => x * 2;

// compose: تنفذ من اليمين لليسار
const compose = (f, g) => x => f(g(x));
const addThenDouble = compose(double, add);
console.log(addThenDouble(5)); // 12

// pipe: تنفذ من اليسار لليمين
const pipe = (f, g) => x => g(f(x));
const doubleThenAdd = pipe(double, add);
console.log(doubleThenAdd(5)); // 11
```

---

### 🍛 Currying باستخدام HOFs

```js
function multiply(a) {
  return function (b) {
    return a * b;
  };
}

const double = multiply(2);
console.log(double(5)); // 10
```

---

### 💡 Memoization (تحسين الأداء)

```js
function memoize(fn) {
  const cache = {};
  return function (x) {
    if (cache[x]) return cache[x];
    const result = fn(x);
    cache[x] = result;
    return result;
  };
}

const slowSquare = memoize((n) => {
  console.log("Computing...");
  return n * n;
});

console.log(slowSquare(5)); // Computing... 25
console.log(slowSquare(5)); // 25 (no computing)
```

---

### 🛠️ استخدام HOFs في الواقع العملي

#### ✅ React:

```js
const withLogger = (Component) => {
  return (props) => {
    console.log("Rendering", Component.name);
    return <Component {...props} />;
  };
};
```

#### ✅ Express.js:

```js
app.use((req, res, next) => {
  console.log(`${req.method} ${req.url}`);
  next();
});
```

---

### ⚠️ ملاحظات هامة

- الإفراط في استخدام HOFs قد يؤدي إلى تعقيد غير ضروري.
    
- من المهم معرفة متى تستخدم loop عادية بدلًا من `map` أو `reduce`.
    

---

### 🏁 خلاصة

- HOFs تجعل الكود أكثر مرونة، قابلية لإعادة الاستخدام، ووضوحًا.
    
- استخدامها بذكاء يفتح لك بابًا لفهم البرمجة الدالية (Functional Programming) بشكل أعمق.
 