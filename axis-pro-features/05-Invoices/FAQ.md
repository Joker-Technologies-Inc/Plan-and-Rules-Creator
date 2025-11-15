# Invoices Module - Frequently Asked Questions (FAQ)

## General Questions

### Q: How do I create an invoice?
**A:** Go to Invoices → "New Invoice" and follow the step-by-step wizard:
1. Select invoice type (Session-based, Manual, or Recurring)
2. Select client
3. Select sessions (if session-based) or add items (if manual)
4. Configure invoice details
5. Preview and save

### Q: What's the difference between session-based and manual invoices?
**A:** 
- **Session-based**: Automatically creates invoice items from selected sessions
- **Manual**: You add custom line items manually
- **Recurring**: Automatically generates invoices on a schedule

### Q: Can I edit an invoice after creating it?
**A:** Yes, you can edit invoices that haven't been fully paid. Click "Edit" on the invoice to make changes.

### Q: Can I delete an invoice?
**A:** Yes, but you may not be able to delete invoices that have payments recorded. The system will warn you before deletion.

---

## Creating Invoices

### Q: How do I create an invoice from sessions?
**A:** 
1. Select "Session-based Invoice"
2. Choose the client
3. Select the confirmed sessions you want to invoice
4. Review the total
5. Configure invoice details (dates, discount, tax, notes)
6. Save and optionally send

### Q: Which sessions can I invoice?
**A:** Only "Confirmed" sessions that haven't been invoiced yet can be selected for invoicing.

### Q: Can I invoice the same session twice?
**A:** No, once a session is invoiced, it's marked as "Invoiced" and cannot be added to another invoice.

### Q: How do I add custom items to an invoice?
**A:** Use "Manual Invoice" type and add line items with description, quantity, rate, and amount.

### Q: Can I mix sessions and manual items in one invoice?
**A:** Currently, you choose either session-based or manual. Mixing both in one invoice is planned for future updates.

---

## Invoice Details

### Q: How is the invoice number generated?
**A:** Invoice numbers are auto-generated (e.g., INV-001, INV-002) but you can override with a custom number if needed.

### Q: What's the difference between Issue Date and Due Date?
**A:** 
- **Issue Date**: When the invoice is created/issued
- **Due Date**: When payment is expected

### Q: How do I add a discount?
**A:** Enter a discount amount or percentage in the invoice details. The system will calculate the discounted total.

### Q: How do I add tax?
**A:** Enter a tax amount or percentage. Tax is calculated on the subtotal (after discount if applicable).

### Q: How is the total calculated?
**A:** Total = (Subtotal - Discount) + Tax
Subtotal = Sum of all line items

---

## Invoice Status

### Q: What do the different invoice statuses mean?
**A:** 
- **Created**: Draft invoice, not yet sent
- **Sent**: Invoice has been sent to client
- **Paid**: Invoice is fully paid
- **Overdue**: Past due date, not yet paid

### Q: How does an invoice become "Overdue"?
**A:** An invoice automatically becomes "Overdue" when the due date passes and the invoice hasn't been marked as paid.

### Q: Can I change an invoice status manually?
**A:** Status changes automatically based on actions (sending, payment recording). Some status changes can be made manually when editing.

---

## Sending Invoices

### Q: How do I send an invoice to a client?
**A:** Click "Send" on the invoice, which opens an email composition dialog. Customize the message if needed and send.

### Q: What email address is used to send invoices?
**A:** The invoice is sent to the client's primary email address (the email on the client record).

### Q: Can I send an invoice to multiple email addresses?
**A:** Multiple recipient support is planned for future updates. Currently, invoices are sent to the client's primary email.

### Q: Can I customize the email message?
**A:** Yes, you can customize the email message when sending the invoice.

### Q: What if the client doesn't receive the email?
**A:** Check that the client's email address is correct. You can resend the invoice or send it manually via the "Send" button again.

---

## Payment Recording

### Q: How do I record a payment?
**A:** Open the invoice, click "Record Payment," enter the payment amount, date, method, and any notes, then save.

### Q: Can I record partial payments?
**A:** Yes! You can record multiple partial payments for an invoice. The system tracks the outstanding balance.

### Q: What payment methods can I record?
**A:** You can record payments via:
- PayPal
- Venmo
- Zelle
- Bank Transfer
- Other (custom)

### Q: How do I know how much is still owed?
**A:** The invoice shows:
- Total amount
- Total paid
- Outstanding balance (Total - Paid)

### Q: What happens when I record full payment?
**A:** The invoice status automatically changes to "Paid" when the outstanding balance reaches zero.

### Q: Can I edit or delete a payment?
**A:** Payment editing and deletion functionality is available. You can modify payment records if needed.

---

## Payment Reminders

### Q: How do I send a payment reminder?
**A:** Click "Remind" on an invoice. This sends a payment reminder email to the client.

### Q: Can I customize the reminder message?
**A:** Yes, you can customize the reminder message before sending.

### Q: How often can I send reminders?
**A:** You can send reminders as often as needed. There's no limit, but be mindful of not spamming clients.

### Q: Will reminders be sent automatically?
**A:** Automatic payment reminders are planned for future updates. Currently, reminders must be sent manually.

---

## Recurring Invoices

### Q: How do I set up a recurring invoice?
**A:** 
1. Select "Recurring Invoice" type
2. Choose client
3. Configure recurring settings (frequency, days)
4. Set up the initial invoice
5. Save

### Q: What frequencies are available for recurring invoices?
**A:** 
- Monthly
- Bi-Monthly (twice per month)
- Weekly

### Q: Can I set specific days for recurring invoices?
**A:** Yes, you can set specific days:
- Monthly: Specific day of month (e.g., 1st, 15th)
- Bi-Monthly: Two specific days
- Weekly: Specific day of week (e.g., Monday)

### Q: Can I stop a recurring invoice?
**A:** Yes, you can pause or cancel recurring invoices from the invoice settings.

### Q: When are recurring invoices generated?
**A:** Recurring invoices are automatically generated on the scheduled dates.

---

## Invoice Templates

### Q: Can I customize how invoices look?
**A:** Invoice template customization is planned for future updates. Currently, invoices use standard templates.

### Q: Can I add my logo to invoices?
**A:** Logo customization is planned for future updates.

### Q: What invoice templates are available?
**A:** Currently, standard templates are available. Custom templates are planned for future updates.

---

## Invoice Preview and PDF

### Q: Can I preview an invoice before sending?
**A:** Yes, click "Preview" to see how the invoice will look to your client.

### Q: Can I download an invoice as PDF?
**A:** PDF download functionality is planned for future updates.

### Q: Can I print invoices?
**A:** You can print invoices from the preview or details page using your browser's print function.

---

## Troubleshooting

### Q: I can't select sessions for invoicing. Why?
**A:** Possible reasons:
- Sessions aren't confirmed (must be "Confirmed" status)
- Sessions are already invoiced
- No sessions exist for the selected client
- Sessions are for a different client

### Q: The invoice total seems wrong
**A:** Check:
- All line items are included
- Discount is calculated correctly
- Tax is applied correctly
- Manual calculations match system calculations

### Q: I can't send an invoice
**A:** Check:
- Client has a valid email address
- Email service is configured
- Internet connection is stable
- Try refreshing and sending again

### Q: Payment isn't recording
**A:** Check:
- Payment amount doesn't exceed outstanding balance
- All required fields are filled
- Try refreshing and recording again

---

## Best Practices

### Q: When should I send invoices?
**A:** Send invoices promptly after creating them, or set up recurring invoices for regular clients.

### Q: How often should I send payment reminders?
**A:** Send a reminder a few days before the due date, and another if the invoice becomes overdue. Don't send too frequently to avoid annoying clients.

### Q: Should I record payments immediately?
**A:** Yes, record payments as soon as you receive them to keep your financial records accurate and up-to-date.

### Q: How should I organize invoice numbers?
**A:** Use consistent numbering. The system auto-generates numbers, but you can customize them if needed.

---

## Future Features

### Q: Will I be able to accept online payments?
**A:** Yes, online payment processing integration (Stripe, PayPal) is planned for future updates.

### Q: Can I set up automatic payment reminders?
**A:** Yes, automated payment reminder scheduling is planned.

### Q: Will there be invoice approval workflows?
**A:** Invoice approval workflows are planned for teams and organizations.

### Q: Can I create invoice estimates/quotes?
**A:** Estimate/quote functionality is planned, allowing you to send estimates before creating final invoices.

