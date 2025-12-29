# Uniform Star Rating & Review Count – Shopify (Liquid-Only)

A **deterministic, uniform star rating system** for Shopify product pages that generates **consistent star ratings and review counts** using **only Liquid** (no apps, no JavaScript).

Ideal for stores that want a **clean review UI** without third-party review apps.

---

## ✨ Features

* ✅ Works on **product pages**
* ✅ Uses **pure Liquid logic** (no JS)
* ✅ Consistent rating per product (ID-based)
* ✅ Star rating (out of 5)
* ✅ Review count with **formatted thousands** (e.g. `3,245`)
* ✅ Clean glowing star UI
* ✅ Lightweight & fast
* ✅ Can be pasted **anywhere**
* ✅ Works with **Custom Liquid blocks or Snippets**

---

## 📂 Usage Options

You can use this snippet in **two ways**:

1. **Paste directly into a Custom Liquid block** (quick test / instant use)
2. **Create a reusable snippet** and render it in product templates

---

## 🚀 Option 1: Paste Directly (Custom Liquid Block)

### Steps

1. Go to **Shopify Admin → Online Store → Themes**
2. Click **Customize**
3. Open a **Product page**
4. Click **Add block**
5. Choose **Custom Liquid**
6. Paste the code below
7. Click **Save**

---

### ✅ Code (Copy–Paste Ready)

```liquid
{%- assign base = product.id | modulo: 11 -%}
{%- assign rating = base | times: 0.1 | plus: 4.0 -%}
{%- assign rating_display = rating | round: 1 -%}
{%- assign star_count = rating | round: 0 -%}
{%- assign max_stars = 5 -%}

{%- assign raw_count = product.id | modulo: 9000 | plus: 200 -%}
{%- assign thousands = raw_count | divided_by: 1000 -%}
{%- assign remainder = raw_count | modulo: 1000 -%}
{%- assign remainder_str = remainder -%}
{%- if thousands > 0 -%}
  {%- if remainder < 10 -%}
    {%- assign remainder_str = '00' | append: remainder_str -%}
  {%- elsif remainder < 100 -%}
    {%- assign remainder_str = '0' | append: remainder_str -%}
  {%- endif -%}
  {%- assign formatted_count = thousands | append: ',' | append: remainder_str -%}
{%- else -%}
  {%- assign formatted_count = remainder_str -%}
{%- endif -%}

<div class="uniform-stars-review">
  <span class="stars">
    {%- for i in (1..max_stars) -%}
      {%- if i <= star_count -%}
        <span class="star active">★</span>
      {%- else -%}
        <span class="star inactive">★</span>
      {%- endif -%}
    {%- endfor -%}
  </span>

  <span class="rating-pill">({{ rating_display }})</span>
  <span class="review-count">{{ formatted_count }} REVIEWS</span>
</div>

<style>
.uniform-stars-review {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  margin-top: 2px !important;
  margin-bottom: 2px !important;
  white-space: nowrap;
}

.uniform-stars-review .stars {
  display: inline-flex;
  gap: 4px;
}

.uniform-stars-review .star {
  font-size: 16px;
  display: inline-block;
  transform: translateY(1px);
}

.uniform-stars-review .star.active {
  color: #FFD14D !important;
  text-shadow: 0 0 6px rgba(255,209,77,0.9),
               0 0 10px rgba(255,230,120,0.45);
}

.uniform-stars-review .star.inactive {
  color: rgba(255,255,255,0.2) !important;
}

.uniform-stars-review .rating-pill {
  display: inline-flex;
  align-items: center;
  padding: 1px 6px;
  min-width: 34px;
  border-radius: 10px;
  background: linear-gradient(180deg,#2ecc71,#1fa85a);
  color: #fff;
  font-weight: 700;
  font-size: 12px;
  line-height: 1;
}

.uniform-stars-review .review-count {
  font-size: 12px;
  font-weight: 800;
  color: #ffffff !important;
  letter-spacing: 0.4px;
  text-transform: uppercase;
  line-height: 1;
}
</style>
```

---

## 🚀 Option 2: Create a Reusable Snippet (Recommended)

### Step 1: Create Snippet

1. Go to **Online Store → Themes → Edit code**
2. Open **Snippets**
3. Click **Add a new snippet**
4. Name it:

```
uniform-stars-review.liquid
```

5. Paste the same code above
6. Click **Save**

---

### Step 2: Render Snippet Anywhere

Add this line wherever you want the rating to appear:

```liquid
{% render 'uniform-stars-review' %}
```

Best placements:

* Under product title
* Near price
* Inside `main-product.liquid`
* Product info blocks

---

## 🧩 How It Works

* Rating is calculated from `product.id` → **stable & consistent**
* Always generates ratings between **4.0 – 5.0**
* Review count is auto-formatted (e.g. `1,245`)
* No database, no metafields, no apps

---

## 🎨 Customization

### 🔹 Change Rating Range

```liquid
plus: 4.0  → minimum rating
modulo: 11 → rating spread
```

### 🔹 Change Review Count Range

```liquid
modulo: 9000
plus: 200
```

### 🔹 Change Star Color

```css
.star.active { color:#FFD14D; }
```

---

## 🛒 Best Use Cases

* Stores without review apps
* Clean UI with social proof
* Fast-loading product pages
* CRO-focused layouts
* Demo / staging stores

---

## ⭐ Support

If this snippet helped you, consider **starring ⭐ the repository**.
Feel free to fork, reuse, and customize it for your Shopify projects.

---
