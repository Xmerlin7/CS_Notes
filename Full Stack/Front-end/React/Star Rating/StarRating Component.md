# 🌟 React - فهم العلاقة بين StarRating و Star

## 📌 ما الفكرة الأساسية؟

في هذا المثال، لدينا مكونان:

- `StarRating`: المكون الأب الذي يتحكم في التقييم.
- `Star`: مكون فردي يمثل نجمة واحدة.

---

## 🧱 مكون StarRating

### ✅ وظيفته:
- إنشاء مجموعة من النجوم لعرض تقييم من 1 إلى `maxRating` (الافتراضي 5).
- حفظ حالة التقييم (`rating`) وحالة مرور الماوس (`hoverRating`).
- تمرير السلوك والتنسيق إلى كل نجمة (`Star`) عبر props.

### 🔁 كيف يُنشئ النجوم؟
```js
Array.from({ length: maxRating }, (_, i) => ( ... ))
```
- يُولّد عددًا من مكونات `Star` حسب القيمة المحددة.
    
- لكل نجمة، يتم تمرير البيانات والسلوك المناسب.
    

### 💡 مثال تمرير props:
```jsx
<Star
  key={i}
  onClickHandler={() => clickHandler(i)}
  fill={hoverRating ? hoverRating >= i + 1 : rating >= i + 1}
  onHoverIn={() => hoverHandlerIn(i)}
  onHoverout={() => hoverHandlerOut(i)}
/>
```

## 🌟 مكون Star

### ✅ وظيفته:

- عرض نجمة واحدة باستخدام SVG.
    
- تمرير التفاعلات (hover, click) إلى المكون الأب عبر props.
    

### ❌ لا يمتلك أي حالة (state)!

هو مجرد واجهة بسيطة للتفاعل، كل شيء يُدار من المكون الأب.

### 🧩 الأحداث المستقبَلة:

- `onClickHandler`: تنفيذ عند الضغط.
    
- `onHoverIn`: تنفيذ عند دخول الماوس.
    
- `onHoverout`: تنفيذ عند خروج الماوس.
    
- `fill`: هل النجمة مضيئة أم لا.
  
  ## 🔗 كيف يتواصل StarRating مع Star؟

|جهة|ترسل|تستقبل|الوظيفة|
|---|---|---|---|
|StarRating (الأب)|`props`|-|يمرر بيانات وسلوك|
|Star (الابن)|-|`props`|يعرض النجمة ويرسل الأحداث للأب|

> كل تفاعل في `Star` يتم ترحيله إلى `StarRating`، والذي بدوره يُحدث حالته ويعيد رسم كل النجوم بالقيمة الجديدة.

---

## ✨ مثال بصري للتقييم

|`rating`|`hoverRating`|`i` (فهرس النجمة)|`fill`|
|---|---|---|---|
|3|0|2|✅|
|3|0|3|❌|
|3|4|3|✅|
|0|2|1|✅|

---

## 🧠 ملاحظات سريعة

- `useState` يستخدم لحفظ التقييمات داخل `StarRating`.
    
- `hoverRating` يسمح للمستخدم بمشاهدة معاينة قبل الاختيار.
    
- `fill` يُحسب ديناميكيًا من القيمتين `hoverRating` و `rating`.
  
  ```jsx
 import React, { useState } from "react";

const style = { display: "flex", gap: "4px" };

const StarRating = ({ maxRating = 5 }) => {

  const [rating, setRating] = useState(0);

  const [hoverRating, setHoverRating] = useState(0);

  const clickHandler = (i) => {

    setRating(i + 1);

  };

  const hoverHandlerIn = (i) => {

    setHoverRating(i + 1); // Save which star we're hovering over

  };

  
  const hoverHandlerOut = () => {

    setHoverRating(0); // Clear on mouse leave

  };

  return (

    <div style={style}>

      <div style={{ display: "flex" }}>

        {Array.from({ length: maxRating }, (_, i) => (

          <Star

            key={i}

            onClickHandler={() => clickHandler(i)}

            fill={hoverRating ? hoverRating >= i + 1 : rating >= i + 1}

            onHoverIn={() => hoverHandlerIn(i)}

            onHoverout={() => hoverHandlerOut(i)}

          />

        ))}

      </div>

  

      <p style={{ margin: 0, fontSize: "20px" }}>

        {" "}

        u set a rating of {hoverRating ? hoverRating : rating || ""}

      </p>

    </div>

  );

};

const Star = ({ onClickHandler, fill, onHoverIn, onHoverout }) => {

  return (

    <div>

      <span

        onMouseEnter={onHoverIn}

        onMouseLeave={onHoverout}

        onClick={onClickHandler}

      >

        <svg

          style={{ width: "25px", height: "25px", cursor: "pointer" }}

          xmlns="http://www.w3.org/2000/svg"

          fill={fill ? "gold" : "none"}

          viewBox="0 0 24 24"

          stroke="#000"

        >

          <path

            strokeLinecap="round"

            strokeLinejoin="round"

            strokeWidth="{2}"

            d="M11.049 2.927c.3-.921 1.603-.921 1.902 0l1.519 4.674a1 1 0 00.95.69h4.915c.969 0 1.371 1.24.588 1.81l-3.976 2.888a1 1 0 00-.363 1.118l1.518 4.674c.3.922-.755 1.688-1.538 1.118l-3.976-2.888a1 1 0 00-1.176 0l-3.976 2.888c-.783.57-1.838-.197-1.538-1.118l1.518-4.674a1 1 0 00-.363-1.118l-3.976-2.888c-.784-.57-.38-1.81.588-1.81h4.914a1 1 0 00.951-.69l1.519-4.674z"

          />

        </svg>

      </span>

    </div>

  );

};

  

export default StarRating;

```