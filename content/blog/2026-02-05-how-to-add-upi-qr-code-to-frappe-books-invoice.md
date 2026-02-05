---
title: "How to Add Dynamic UPI QR Code to Frappe Books Invoice Template"
slug: "how-to-add-upi-qr-code-to-frappe-books-invoice"
date: 2026-02-05T14:25:00+05:30
# author
author : ["Ronak Vanpariya"]
# categories
categories: ["solutions", "Technology"]
tags: ["Frappe Books", "UPI", "QR Code", "Invoice", "India"]
# meta description
description: "Learn how to add a dynamic UPI QR code to your Frappe Books invoice template that auto-generates based on invoice amount and details."
keywords: ["Frappe Books UPI QR", "Frappe Books Invoice QR Code", "UPI Payment QR Invoice"]
# save as draft
draft: false  
---

Hello everyone, :wave:

## How to Add Dynamic UPI QR Code to Frappe Books Invoice

If you're using [Frappe Books](https://frappebooks.com/) for invoicing in India, adding a **dynamic UPI QR code** to your invoices makes it incredibly easy for customers to pay you. 

**The best part?** The QR code automatically includes the invoice amount and reference number - no manual work needed!

## What You'll Get

✅ QR code with **exact invoice amount**  
✅ Invoice number as **payment reference**  
✅ Your UPI ID pre-filled  
✅ Works with **any UPI app** (GPay, PhonePe, Paytm, etc.)

---

## Step 1: Open Your Print Template

1. Open **Frappe Books**
2. Go to **Settings** → **Print Template**
3. Click on your invoice template to edit it

---

## Step 2: Copy & Paste This Code

Add this code inside your `<footer>` section:

```html
<!-- Payment Details with QR Code -->
<section class="mt-12 flex justify-between">
  <!-- Bank Details (Left Side) -->
  <div>
    <h3 class="text-lg font-semibold">Payment Details:</h3>
    <p class="mt-4 text-lg whitespace-pre-line">
      <strong>Account Name:</strong> Your Company Name <br>
      <strong>Account No:</strong> 1234 5678 9012 <br>
      <strong>IFSC:</strong> BANKCODE1234 <br>
      <strong>Bank Name:</strong> Your Bank <br>
      <strong>UPI:</strong> yourcompany@upi <br>
    </p>
  </div>
  
  <!-- UPI QR Code (Right Side) -->
  <div>
    <p class="text-xl"><strong>Pay with UPI QR:</strong></p>
    <div class="border-4 p-1 border-black border-dashed">
      <img 
        :src="'https://api.qrserver.com/v1/create-qr-code/?size=150x150&data=' + encodeURIComponent('upi://pay?pa=YOUR_UPI_ID&pn=YOUR_COMPANY_NAME&tn=For Bill ' + doc.name + '&cu=INR&am=' + doc.grandTotal.toString().replace(/[^\d.]/g, ''))" 
        alt="UPI QR Code"
        class="w-full h-auto"
      />
    </div>
  </div>
</section>
```

---

## Step 3: Replace With Your Details

**You only need to change 2 things:**

### 🔹 1. Your UPI ID
Find `YOUR_UPI_ID` and replace with your actual UPI ID.

**Example:** `mybusiness@okaxis` or `9876543210@paytm`

### 🔹 2. Your Company Name  
Find `YOUR_COMPANY_NAME` and replace with your business name.

**Example:** `ABC Traders` or `My Business Pvt Ltd`

That's it! No URL encoding needed - the template handles it automatically using `encodeURIComponent()`.

---

## Understanding the Code

Here's what the UPI URL looks like (before encoding):

```
upi://pay?pa=YOUR_UPI_ID&pn=YOUR_COMPANY_NAME&tn=For Bill SINV-0001&cu=INR&am=1500.00
```

| Parameter | What It Does | Value |
|-----------|--------------|-------|
| `pa` | Payee Address (UPI ID) | Your UPI ID |
| `pn` | Payee Name | Your company name |
| `tn` | Transaction Note | "For Bill" + Invoice Number |
| `cu` | Currency | INR |
| `am` | Amount | Invoice grand total |

The `encodeURIComponent()` function automatically converts special characters:
- Spaces become `%20`
- `@` becomes `%40`
- etc.

---

## How Dynamic Values Work

```javascript
// Invoice number - pulled automatically
doc.name  // → "SINV-0001"

// Amount - extracts only numbers from grand total
doc.grandTotal.toString().replace(/[^\d.]/g, '')  // → "1500.00"
```

---

## Test Your QR Code

⚠️ **Before using in production:**

1. Create a test invoice
2. Preview the invoice
3. Scan the QR code with any UPI app
4. Verify amount and details are correct

---

## Troubleshooting

**QR code shows wrong amount?**
> Make sure `doc.grandTotal` exists in your template.

**QR code not scanning?**
> Double-check your UPI ID is correct.

**Layout looks broken?**
> Adjust the CSS classes to match your template's styling.

---

Thanks For Reading 🙏

> This article is based on my personal implementation in Frappe Books. Please let me know if you found any issues, in comment section below.

{{< footer-donation >}}
