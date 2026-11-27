# DRG Company – Online Store

A Jumia-style online fashion store for DRG Company (Uganda). Pure HTML/CSS/JS, hosted free on GitHub Pages, with Firebase (free tier) for orders, products and admin login.

## Files
| File | Purpose |
|---|---|
| `index.html` | The whole website (shop, cart, checkout, contact, admin area) with your product photos built in |
| `README.md` | This guide |

## Features
- Home page, categories, search, cart, checkout (pay on delivery / MTN / Airtel)
- Admin area (`#admin`): see all orders, reply to customers by email, mark as replied, add products, edit or lower prices, remove products

## Setup (about 15 minutes)

### 1. Firebase
1. Go to https://console.firebase.google.com and create a project (e.g. `drg-company`).
2. **Build → Firestore Database → Create database** (production mode).
3. **Build → Authentication → Get started → Email/Password → Enable**. Then open the **Users** tab, **Add user**: email `gorettiasiimwe2@gmail.com` and a strong password of your choice. This is the admin login.
4. **Project settings → Your apps → Web (`</>`)**: register an app and copy the config values.
5. In `index.html`, find `const FB={...}` and paste in your `apiKey`, `authDomain`, `projectId` and `appId`.
6. **Firestore → Rules**, paste this and publish:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{db}/documents {
    match /products/{id} { allow read: if true; allow write: if request.auth != null; }
    match /orders/{id}   { allow create: if true; allow read, update, delete: if request.auth != null; }
    match /status/{id}   { allow read, write: if request.auth != null; }
  }
}
```
Customers can place orders and view products. Only the logged-in admin can read orders or change products.

### 2. GitHub Pages
1. Create a new repository (e.g. `drg-company`) on GitHub.
2. Upload `index.html` and `README.md` (the product photos are already inside `index.html`).
3. **Settings → Pages → Source: Deploy from a branch → `main` / root → Save.**
4. Your store goes live at `https://YOUR-USERNAME.github.io/drg-company/`.
5. In Firebase **Authentication → Settings → Authorized domains**, add `YOUR-USERNAME.github.io`.

## Using the admin area
Open the site, click **Admin**, log in with the Firebase user you created.
- **Orders** tab: customer details; **Reply by email** opens your email app with a message ready.
- **Products** tab: type an amount in **Deduct from price** and save to lower a price; add or remove products.

## Notes
- Change `ADMIN_EMAIL` near the top of the script if your email changes.
- Orders don't take payment online. Confirm payment with the customer when you reply.
