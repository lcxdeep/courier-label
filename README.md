# courier-label

Custom courier label and envelope printing for Zoho Books.
Hosted on GitHub Pages. Triggered by custom buttons on Customer and Vendor records in Zoho Books.

**Owner:** Studio LCX Fashion Pvt Ltd
**Live URLs:**
- Courier label: https://lcxdeep.github.io/courier-label/
- Envelope: https://lcxdeep.github.io/courier-label/envelope.html

---

## Files

| File | Purpose | Paper size |
|---|---|---|
| `index.html` | Courier label with To + From block | A4 or A5 landscape (selectable) |
| `envelope.html` | Envelope address printing, To only | #10 envelope, 241mm × 105mm |

---

## How it works

1. User opens a Customer or Vendor record in Zoho Books
2. User clicks the custom button (**To & From** for courier, **Envelope** for envelope)
3. New tab opens with the address auto-populated from Zoho via URL parameters
4. User presses Ctrl+P → prints to PDF or directly to printer

No backend. No database. No Zoho API. Pure HTML + CSS + vanilla JS.

---

## Zoho Books Custom Button URLs

All four buttons are configured in:
**Settings → Module Settings → General → Customers and Vendors → Custom Buttons tab**

### To & From — Customer
```
https://lcxdeep.github.io/courier-label/?name=${CONTACT.CUSTOMER_NAME}&addr1=${CONTACT.BILLING_ADDRESS}&area=${CONTACT.CF.Area}&city=${CONTACT.BILLING_CITY}&state=${CONTACT.BILLING_STATE}&zip=${CONTACT.BILLING_CODE}&country=${CONTACT.BILLING_COUNTRY}&phone=${CONTACT.WORK_PHONE}&mobile=${CONTACT.MOBILE_PHONE}
```

### To & From — Vendor
```
https://lcxdeep.github.io/courier-label/?name=${CONTACT.COMPANY_NAME}&addr1=${CONTACT.BILLING_ADDRESS}&area=${CONTACT.CF.Area}&city=${CONTACT.BILLING_CITY}&state=${CONTACT.BILLING_STATE}&zip=${CONTACT.BILLING_CODE}&country=${CONTACT.BILLING_COUNTRY}&phone=${CONTACT.WORK_PHONE}&mobile=${CONTACT.MOBILE_PHONE}
```

### Envelope — Customer
```
https://lcxdeep.github.io/courier-label/envelope.html?name=${CONTACT.CUSTOMER_NAME}&addr1=${CONTACT.BILLING_ADDRESS}&area=${CONTACT.CF.Area}&city=${CONTACT.BILLING_CITY}&state=${CONTACT.BILLING_STATE}&zip=${CONTACT.BILLING_CODE}&country=${CONTACT.BILLING_COUNTRY}&phone=${CONTACT.WORK_PHONE}&mobile=${CONTACT.MOBILE_PHONE}
```

### Envelope — Vendor
```
https://lcxdeep.github.io/courier-label/envelope.html?name=${CONTACT.COMPANY_NAME}&addr1=${CONTACT.BILLING_ADDRESS}&area=${CONTACT.CF.Area}&city=${CONTACT.BILLING_CITY}&state=${CONTACT.BILLING_STATE}&zip=${CONTACT.BILLING_CODE}&country=${CONTACT.BILLING_COUNTRY}&phone=${CONTACT.WORK_PHONE}&mobile=${CONTACT.MOBILE_PHONE}
```

**Difference between Customer and Vendor URLs:** only the name placeholder.
Customer → `${CONTACT.CUSTOMER_NAME}`
Vendor → `${CONTACT.COMPANY_NAME}`

---

## Courier label (index.html)

- Top control bar (hidden on print): Paper Size dropdown (A4 / A5), From Address dropdown (C Wing / A Wing), Print, Load Demo, Clear
- To block: name + address from Zoho URL parameters
- Editable Street 2 line: yellow strip with dashed border, click to type extra address info. Hides on print if empty.
- From block: hardcoded — Studio LCX Fashion Pvt Ltd, Mhatre Pen Industrial Estate, Senapati Bapat Marg, Dadar West, Mumbai 400028. Two options: C-101 (C Wing) or A-112 1st Floor (A Wing). A Wing is default.
- A5 is default (used ~90% of the time). Switch to A4 only for large packages or very long addresses.

---

## Envelope (envelope.html)

- Fixed size: 241mm × 105mm landscape (#10 envelope)
- Layout: To block only, positioned on the right side of the envelope
- Margins: 130mm left, 30mm right, 20mm top, 30mm minimum bottom (text block is 81mm wide)
- Content: "TO," (bold caps), name (bold caps), then address details
- Editable Street 2 line same as courier label
- Print workflow: load #10 envelope into HP LaserJet envelope feed → Ctrl+P → Print
- Browser print dialog should auto-select "Envelope #10" paper size after first use

---

## Known limitations

- **No Street 2 from Zoho.** `${CONTACT.BILLING_ADDRESS}` only returns Street 1. Workaround: editable yellow strip on the printed label, fill manually before printing. Not persisted.
- **No Shipping Address.** Uses Billing only.
- **GitHub Pages cache:** Ctrl+F5 required to see updates after editing files.
- **Initial deploy delay:** GitHub Pages takes 1-3 minutes to publish changes.

---

## How to edit the HTML

1. Open the file on GitHub (`index.html` or `envelope.html`)
2. Click the pencil icon to edit
3. Make changes or paste new content
4. Commit changes
5. Wait 1-2 minutes
6. Ctrl+F5 on the live URL to see updates
