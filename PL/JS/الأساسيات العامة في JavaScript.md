## 📍 المرحلة الأولى: الأساسيات العامة في JavaScript

---

### 1️⃣ **Primitive vs Reference Types**

#### ✅ الأنواع البدائية (Primitive):

القيم بتتخزن في **stack memory** وبيتم نسخها مباشرة عند الإسناد.

```js
let x = 5;
let y = x;
y++;

console.log(x); // 5
console.log(y); // 6
```

> هنا `x` و `y` كل واحد فيهم نسخة مستقلة، لأن `number` نوع بدائي.

---

#### ✅ الأنواع المرجعية (Reference Types):

بتتخزن في **heap memory**، والمتغير بيحمل **مرجع (reference)** للمكان في الذاكرة، مش القيمة نفسها.

```js
let obj1 = { name: "Seif" };
let obj2 = obj1;

obj2.name = "Ahmed";

console.log(obj1.name); // "Ahmed"
```

> لأن `obj1` و `obj2` بيشيروا لنفس الكائن في الذاكرة، فالتغيير في واحد بيأثر على التاني.

---

### 2️⃣ **Pass by Value vs Pass by Reference**

#### ✅ Pass by Value

بيتم نسخ القيمة وتمريرها.

```js
function increment(n) {
  n++;
}
let a = 10;
increment(a);
console.log(a); // 10
```

#### ✅ Pass by Reference

بيتم تمرير **المرجع** للكائن، فبيتم التعديل عليه مباشرة.

```js
function update(obj) {
  obj.name = "Ali";
}
let user = { name: "Seif" };
update(user);
console.log(user.name); // "Ali"
```

---

### 3️⃣ **Memory Model: Stack vs Heap**

#### ✅ Stack:

- سريع
    
- يخزن القيم البدائية
    
- يُستخدم في استدعاء الدوال والـ Execution Context
    

#### ✅ Heap:

- أبطأ
    
- يخزن الكائنات والبيانات المرجعية
    
- يُستخدم لحفظ البيانات اللي حجمها كبير أو متغيرة باستمرار
    

📌 مثال يجمع الاثنين:

```js
let name = "Seif"; // stack
let user = { age: 25 }; // user موجود في stack لكن يشير إلى object في heap
```

