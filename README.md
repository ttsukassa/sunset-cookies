# 🍪 Sunset Cookies

> Simple ingredients, sweet moments — Algiers, Algeria

A single-file ordering website for a home cookie business. Customers browse, customize, and place orders directly from their phone. Orders are logged to Google Sheets and the owner is notified via WhatsApp.

---

## Features

- **3 cookie types** — Chocolate chip, Nutty & fruity, Custom build-your-own
- **Multi-step order form** — product → format → details → review → confirm
- **Google Sheets integration** — every order appended as a row automatically
- **WhatsApp fallback** — if the sheet is unreachable, a prefilled WA message is offered
- **Order reference number** — generated at submit, shown on confirmation screen
- **Phone validation** — Algerian mobile numbers (05x / 06x / 07x)
- **3 languages** — English, Français, العربية (with full RTL support)
- **Fully responsive** — built mobile-first, no frameworks
- **Zero dependencies** — one HTML file, no build step, no npm

---

## Stack

| Layer | Tech |
|---|---|
| Frontend | Vanilla HTML / CSS / JS |
| Fonts | Cormorant Garamond + DM Sans (Google Fonts) |
| Backend | Google Apps Script (Web App) |
| Database | Google Sheets |
| Hosting | GitHub Pages |

---

## Project Structure

```
sunset-cookies/
├── index.html   # entire app — HTML, CSS, and JS in one file
└── README.md
```

---

## Google Sheets Setup

Row 1 headers must be in this exact order:

| A | B | C | D | E | F | G | H | I | J | K | L | M |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Timestamp | Ref | Name | Phone | Address | Delivery Zone | Delivery Fee | Product | Format | Mix | Subtotal | Est. Total | Note |

---

## Apps Script

Paste this into your Google Apps Script project and deploy as a Web App (Execute as: Me, Access: Anyone):

```javascript
function doPost(e) {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName('Feuille 1');
  var data  = JSON.parse(e.postData.contents);
  sheet.appendRow([
    data.timestamp,
    data.ref,
    data.name,
    data.phone,
    data.location,
    data.delivery_zone,
    data.delivery_fee,
    data.product,
    data.format,
    data.mix,
    data.subtotal,
    data.est_total,
    data.note
  ]);
  return ContentService
    .createTextOutput('OK')
    .setMimeType(ContentService.MimeType.TEXT);
}
```

---

## Contact

📸 [@sun_setcookies](https://instagram.com/sun_setcookies)  
💬 [WhatsApp](https://wa.me/213555092508)
