# 📚 توثيق بنية البيانات: Linked List

---

## 🧠 ما هي Linked List؟

هي بنية بيانات (Data Structure) تتكون من **سلسلة من العقد (Nodes)**، كل عقدة تحتوي على:

- قيمة (value)
- مؤشر إلى العقدة التالية (next)

---

## ❗ لماذا نستخدم Linked List بدلًا من Array؟

| المقارنة         | Array                      | Linked List                  |
|------------------|----------------------------|------------------------------|
| حجم البيانات     | يجب تحديده مسبقًا غالبًا  | مرن ويزيد أثناء التشغيل     |
| الإضافة/الحذف من البداية | مكلف زمنيًا (O(n))         | سريع جدًا (O(1))            |
| الوصول العشوائي | سريع (O(1))                | بطيء (O(n))                 |
| استخدام الذاكرة | متجاور ومباشر              | غير متجاور (بواسطة الـ References) |

---

## 🧱 كيف يتم الحجز في الذاكرة؟

- الـ Linked List **لا تحجز ذاكرة متجاورة**.
- كل `Node` يتم إنشاؤها في أي مكان في الذاكرة.
- الربط بين العقد يتم عبر `next` (أي pointer أو reference).
- لذلك، **يسهل توسيعها بدون إعادة تخصيص الذاكرة مثل الـ Arrays**.

---

## ✅ الميثودات الحالية في الكلاس:

### 1. `push(value)`
- **تضيف عنصر في نهاية القائمة.**
- الزمن: `O(1)` لأن لدينا `tail`.

---

### 2. `pop()`
- **تحذف آخر عنصر في القائمة.**
- الزمن: `O(n)` لأننا نمر على جميع العناصر لإيجاد ما قبل الأخير.

---

### 3. `unshift(value)`
- **تضيف عنصر في بداية القائمة.**
- الزمن: `O(1)`.

---

### 4. `shift()`
- **تحذف أول عنصر في القائمة.**
- الزمن: `O(1)`.

---

### 5. `print()`
- **تطبع القيم الحالية في القائمة.**

---

## 🧩 الميثودات المقترحة للتنفيذ لاحقًا:

### 🔍 `get(index)`
- ترجع العقدة عند رقم معين.
- الزمن: `O(n)`

---

### ✏️ `set(index, value)`
- تغير قيمة نود عند index معين.

---

### ➕ `insert(index, value)`
- تدخل عنصر في مكان معين داخل القائمة.

---

### ❌ `remove(index)`
- تحذف عنصر عند index معين.

---

### 🔁 `reverse()`
- تعكس ترتيب العناصر داخل القائمة.

---
## ✅
### 📐 `size()`
- تحسب عدد العقد في القائمة.

---
## ✅
### ⚖️ `isEmpty()`
- ترجع `true` إذا كانت القائمة فارغة.

---

## 📎 ملاحظات هامة:

- دائمًا تحقق من الحالة الخاصة: `head === tail` أو `head === null`.
- الـ JavaScript يجمع القمامة (Garbage Collection)، لذا لا حاجة لتحرير العقد يدويًا، مجرد فصل الـ reference كافٍ.
- كل `Node` مربوطة فقط بـ `next`، لذلك الانتقال يكون في اتجاه واحد.

---
## 🧑‍💻 الكود:
```Javascript

// تعريف كائن العقدة الأساسية المستخدمة في كل عنصر من عناصر القائمة
class Node {
  constructor(value) {
    this.value = value;     // القيمة المخزنة داخل العقدة
    this.next = null;       // مؤشر للعقدة التالية
  }
}

// تعريف الكلاس الرئيسي للقائمة المرتبطة
class List {
  constructor() {
    this.head = null; // أول عنصر في القائمة
    this.tail = null; // آخر عنصر في القائمة
    this.ctr = 0;     // عداد لتتبع حجم القائمة
  }

  /**
   * isEmpty()
   * Check if the linked list is empty.
   * @return {boolean}
   */
  isEmpty() {
    return this.head === null;
  }

  /**
   * push(value)
   * Add a new node to the end of the linked list.
   * @param {*} value - The value to insert
   */
  push(value) {
    let newNode = new Node(value);
    if (!this.head) {
      // إذا كانت القائمة فارغة
      this.head = newNode;
      this.tail = newNode;
    } else {
      // ربط العنصر الجديد بآخر عنصر حالي
      this.tail.next = newNode;
      this.tail = newNode;
    }
    this.ctr++; // زيادة العداد
  }

  /**
   * pop()
   * Remove the last node from the linked list.
   */
  pop() {
    if (!this.head) {
      console.log("This Linked List is empty");
      return;
    }

    if (this.head === this.tail) {
      // عنصر واحد فقط
      this.tail = null;
      this.head = null;
      this.ctr--;
      return;
    }

    let currentNode = this.head;
    while (currentNode.next !== this.tail) {
      currentNode = currentNode.next;
    }

    currentNode.next = null;
    this.tail = currentNode;
    this.ctr--;
  }

  /**
   * shift()
   * Remove the first node from the linked list.
   */
  shift() {
    if (!this.head) {
      console.log("This Linked List is empty");
      return;
    }

    if (this.head === this.tail) {
      // عنصر واحد فقط
      this.head = null;
      this.tail = null;
    } else {
      this.head = this.head.next; // تحريك الرأس للعقدة التالية
    }

    this.ctr--;
  }

  /**
   * unshift(value)
   * Add a new node at the beginning of the list.
   * @param {*} value - The value to insert
   */
  unshift(value) {
    let newNode = new Node(value);
    if (!this.head) {
      this.head = newNode;
      this.tail = newNode;
    } else {
      newNode.next = this.head;
      this.head = newNode;
    }
    this.ctr++;
  }

  /**
   * print()
   * Display all values of the linked list from head to tail.
   */
  print() {
    if (!this.head) {
      console.log("This Linked List is empty");
      return;
    }

    let currentNode = this.head;
    let result = [];

    while (currentNode) {
      result.push(currentNode.value);
      currentNode = currentNode.next;
    }

    console.log(`The current values of linked list are ${result.join(" -> ")}`);
  }

  /**
   * size()
   * Display the current size of the linked list.
   */
  size() {
    console.log(this.ctr); // طباعة القيمة المحفوظة في ctr

    // البديل اليدوي لو لم نستخدم العداد:
    /*
    if (!this.head) {
      console.log("This Linked List is empty");
      return;
    }

    let currentNode = this.head;
    let ctr = 0;

    while (currentNode) {
      ctr++;
      currentNode = currentNode.next;
    }

    console.log(`The size of linked list is ${ctr}`);
    */
  }
}





```
## ✅ مثال على الاستخدام:

```js
// 🔬 تجربة الكود
let list = new List();

list.push(5);      // [5]
list.push(6);      // [5 -> 6]
list.push(7);      // [5 -> 6 -> 7]
list.push(8);      // [5 -> 6 -> 7 -> 8]
list.unshift(4);   // [4 -> 5 -> 6 -> 7 -> 8]

list.print();      // طباعة الحالة الحالية
list.size();       // طباعة الحجم

list.shift();      // حذف أول عنصر -> [5 -> 6 -> 7 -> 8]
list.print();

list.pop();        // حذف آخر عنصر -> [5 -> 6 -> 7]
list.print();

list.size();

```

