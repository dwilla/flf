# Stripe Donation Setup Guide

## Overview
This guide will walk you through setting up Stripe Payment Links for Fourth Light Farm donations. The entire process takes about 10-15 minutes.

---

## Step 1: Access Stripe Dashboard

1. Go to **https://dashboard.stripe.com/test** (for test mode)
2. Log in to your Stripe account
3. Make sure you're in **Test Mode** (toggle in top-right corner should say "Test mode")

---

## Step 2: Create One-Time Donation Payment Link

### 2.1 Navigate to Payment Links
1. In the left sidebar, click **Product catalog** → **Payment Links**
2. Or go directly to: https://dashboard.stripe.com/test/payment-links
3. Click **+ New** button (top right)

### 2.2 Configure the Payment Link

**Product Information:**
- **Product name**: `One-Time Donation to Fourth Light Farm`
- **Description**: `Support sustainable agriculture and community education programs`

**Pricing:**
- Select: **☑ Customers choose what to pay**
- **Minimum amount**: `$5.00` (or your preference)
- **Suggested amount** (optional): `$25.00`
- Leave **Maximum amount** blank (or set to something high like `$10,000`)

**Payment Options:**
- Payment type: **One-time**
- Collect customer addresses: **Don't collect** (optional - you can enable if you want mailing addresses)

**After payment:**
- **Success page**: Select "Redirect to a page" and enter:
  ```
  https://YOUR-GITHUB-USERNAME.github.io/flf/?donation=success
  ```
  Replace `YOUR-GITHUB-USERNAME` with your actual GitHub username
  
- **Cancellation**: Check "Customize" and enter:
  ```
  https://YOUR-GITHUB-USERNAME.github.io/flf/?donation=cancelled
  ```

**Additional options:**
- Enable "Allow promotion codes" if you want to offer discount codes later
- You can add a custom image/logo if desired

### 2.3 Create and Copy the Link
1. Click **Create link**
2. Copy the Payment Link URL (looks like `https://buy.stripe.com/test_xxxxx`)
3. **Save this URL** - you'll need it in Step 4

---

## Step 3: Create Monthly Recurring Donation Payment Link

### 3.1 Create New Payment Link
1. Go back to Payment Links page
2. Click **+ New** button again

### 3.2 Configure the Payment Link

**Product Information:**
- **Product name**: `Monthly Recurring Donation to Fourth Light Farm`
- **Description**: `Become a sustaining supporter - monthly donations provide ongoing support for our programs`

**Pricing:**
- Select: **☑ Customers choose what to pay**
- **Minimum amount**: `$5.00` (or your preference)
- **Suggested amount** (optional): `$25.00`
- Leave **Maximum amount** blank

**Payment Options:**
- Payment type: **Recurring**
- Billing period: **Monthly**
- Collect customer addresses: **Don't collect**

**After payment:**
- Use the **same success and cancel URLs** as Step 2:
  - Success: `https://YOUR-GITHUB-USERNAME.github.io/flf/?donation=success`
  - Cancel: `https://YOUR-GITHUB-USERNAME.github.io/flf/?donation=cancelled`

### 3.3 Create and Copy the Link
1. Click **Create link**
2. Copy this Payment Link URL
3. **Save this URL** - you'll need it in Step 4

---

## Step 4: Update Your Website Code

### 4.1 Open index.html
Open the file `/Users/drewwillard/workspace/github_repos/flf/index.html`

### 4.2 Find and Replace Payment Link Placeholders

Search for these two lines in the file (around line 283-289):

```html
<a id="oneTimeDonateBtn" href="YOUR_ONE_TIME_PAYMENT_LINK_HERE"
```

Replace `YOUR_ONE_TIME_PAYMENT_LINK_HERE` with your **one-time donation** Payment Link from Step 2.

Then find:

```html
<a id="monthlyDonateBtn" href="YOUR_MONTHLY_PAYMENT_LINK_HERE"
```

Replace `YOUR_MONTHLY_PAYMENT_LINK_HERE` with your **monthly donation** Payment Link from Step 3.

### 4.3 Save the File
Save `index.html` with the updated Payment Links.

---

## Step 5: Test Your Donation Flow

### 5.1 Open Your Website Locally
1. Open `index.html` in your web browser
2. Navigate to the donation section (or click "Support Our Mission" in the hero)

### 5.2 Test One-Time Donation
1. Click **"Make a One-Time Donation"** button
2. You should be redirected to Stripe's checkout page
3. Enter a test amount (e.g., $10.00)
4. Use Stripe's test card number:
   - **Card number**: `4242 4242 4242 4242`
   - **Expiry**: Any future date (e.g., `12/34`)
   - **CVC**: Any 3 digits (e.g., `123`)
   - **Name**: Your name
   - **Email**: Your email
5. Click "Pay"
6. You should be redirected back to your site with a success message

### 5.3 Test Monthly Donation
1. Go back to the donation section
2. Click **"Become a Monthly Supporter"** button
3. Follow the same test process as above
4. Note: This creates a test subscription (you can cancel it in Stripe Dashboard later)

### 5.4 Test Cancellation
1. Click one of the donation buttons
2. On the Stripe page, click the back button or close the tab
3. Manually navigate back to: `https://YOUR-SITE.github.io/flf/?donation=cancelled`
4. You should see a "Donation Cancelled" notification

---

## Step 6: View Test Donations in Stripe

1. Go to **https://dashboard.stripe.com/test/payments**
2. You should see your test donations listed
3. Go to **https://dashboard.stripe.com/test/subscriptions** to see test recurring donations
4. You can view customer details, send receipts, issue refunds, etc.

---

## Step 7: Go Live (When Ready)

### When you're ready to accept real donations:

1. **Switch to Live Mode** in Stripe Dashboard (toggle in top-right)
2. **Complete Stripe account activation** (if not done already):
   - Provide business information
   - Add bank account for payouts
   - Verify identity
3. **Create the same two Payment Links in Live Mode**:
   - Follow Steps 2 and 3 again, but in Live mode
   - Use the same URLs for success/cancel redirects
4. **Update index.html** with the **Live** Payment Link URLs
5. **Remove test mode note** (if you added one)
6. **Push to GitHub** and deploy

### Important Live Mode Notes:
- Test cards won't work in live mode
- Real credit cards will be charged
- You'll receive payouts to your bank account
- Stripe fees apply: 2.9% + $0.30 per transaction

---

## Step 8: Customize Donation Impact Examples

The website currently shows placeholder impact examples. Update these in `index.html` (around line 278-317) to reflect real Fourth Light Farm impacts:

Current placeholders:
- $10 - Supports seed distribution
- $25 - Feeds chickens for a week
- $50 - Supports a family garden for a month
- $100+ - Builds community infrastructure

Edit these to match your actual program costs and impacts.

---

## Optional Enhancements

### Email Receipts
- Stripe automatically sends email receipts to donors
- Customize receipt emails in: Dashboard → Settings → Emails → Customer emails

### Donation Tracking
- View all donations: Dashboard → Payments
- Export data: Payments → Export
- Set up webhooks for real-time tracking (advanced)

### Thank You Emails
- Set up automated thank-you emails in Stripe
- Or use a service like Mailchimp to send custom thank-you messages

### Recurring Donation Management
- Donors can manage their subscriptions through Stripe's Customer Portal
- Enable this in: Dashboard → Settings → Customer portal

### Add Donation Widget
- Consider adding a small "Donate" widget in the corner of every page
- Could be a sticky floating button that appears when scrolling

---

## Troubleshooting

### "Payment Link Not Working"
- Verify you copied the complete URL (should start with `https://buy.stripe.com/`)
- Check that you're using the correct test/live mode link
- Ensure the link is active in Stripe Dashboard

### "Not Redirecting After Payment"
- Verify your success/cancel URLs in Payment Link settings
- Make sure URLs include the full domain and query parameter
- Check that you're using `https://` not `http://`

### "No Notification Appearing"
- Check browser console for JavaScript errors
- Verify the URL parameter is in the address bar (`?donation=success`)
- Make sure the notification element exists in HTML

### "Test Card Not Working"
- Use `4242 4242 4242 4242` exactly (most common test card)
- Use any future expiry date
- Use any 3-digit CVC
- Other test cards: https://stripe.com/docs/testing

---

## Support

**Stripe Documentation:**
- Payment Links: https://stripe.com/docs/payment-links
- Testing: https://stripe.com/docs/testing
- Going Live: https://stripe.com/docs/development/setup

**Fourth Light Farm Contact:**
- Email: fourthlightfarm@gmail.com
- Phone: (603) 265-1380

---

## Summary Checklist

- [ ] Create Stripe account (if needed)
- [ ] Switch to Test Mode
- [ ] Create one-time donation Payment Link
- [ ] Create monthly donation Payment Link
- [ ] Copy both Payment Link URLs
- [ ] Update `index.html` with Payment Links
- [ ] Save and deploy website
- [ ] Test one-time donation flow
- [ ] Test monthly donation flow
- [ ] Test cancellation flow
- [ ] View donations in Stripe Dashboard
- [ ] Customize donation impact examples
- [ ] When ready: Switch to Live Mode and repeat
- [ ] Celebrate! 🎉

---

## Your Payment Links (Fill in after creation)

**Test Mode:**
- One-time donation: `_________________________________`
- Monthly donation: `_________________________________`

**Live Mode:**
- One-time donation: `_________________________________`
- Monthly donation: `_________________________________`

---

Good luck! Your supporters will appreciate the easy and secure donation process.
