# Donation Section Overview

## What Was Implemented

### 1. New Donation Section
**Location:** Between Newsletter and Contact sections

**Components:**
- Section header: "Support Our Mission"
- Subheading explaining the purpose
- Four donation impact cards showing what different amounts accomplish
- Main donation form with two large buttons
- Success/error notification system

### 2. Updated Navigation
- **Navbar:** Added "Donate" link that scrolls to donation section
- **Hero section:** "Donate" button now says "Support Our Mission" and links to #donate
- **Footer:** Added "Donate" link in Quick Links section

### 3. Donation Impact Cards

Visual cards showing what donations accomplish:
- **$10** - Supports seed distribution (seedling icon)
- **$25** - Feeds chickens for a week (drumstick icon)
- **$50** - Supports a family garden for a month (leaf icon)
- **$100+** - Builds community infrastructure (tractor icon)

**Note:** These are placeholders. Update them with actual Fourth Light Farm impacts.

### 4. Donation Buttons

Two prominent call-to-action buttons:

#### One-Time Donation Button (Green)
- Text: "Make a One-Time Donation"
- Icon: Hand holding heart
- Links to: Your Stripe one-time Payment Link
- Helper text: "You'll choose your donation amount on the next page"

#### Monthly Recurring Button (Earth brown)
- Text: "Become a Monthly Supporter"
- Icon: Calendar check
- Links to: Your Stripe monthly Payment Link
- Helper text: "Recurring donations provide sustainable support"

### 5. Additional Context Box
Light tan notification box with:
- Info icon
- Explanation of where donations go
- Note about email receipts

### 6. Success/Cancel Notifications

**When users return from Stripe:**

**Success notification** (Green):
- Shows at top-right of screen
- Message: "Thank you for your generous support!"
- Details about receipt
- Auto-scrolls to donation section
- Auto-dismisses after 8 seconds

**Cancel notification** (Yellow):
- Shows at top-right of screen
- Message: "Donation Cancelled"
- Friendly reassurance
- Auto-dismisses after 8 seconds

---

## User Flow

### Donation Process
1. User visits site
2. Clicks "Support Our Mission" in hero OR "Donate" in nav
3. Scrolls to donation section
4. Sees impact examples
5. Decides between one-time or monthly
6. Clicks appropriate button
7. Redirected to Stripe checkout page
8. Enters custom donation amount
9. Completes payment with credit card
10. Redirected back to site with success message
11. Receives email receipt from Stripe

### If User Cancels
1. User clicks donation button
2. Arrives at Stripe page
3. Changes mind, clicks back button
4. Returns to site
5. Sees friendly "Donation Cancelled" message

---

## Technical Details

### No Backend Required
- Uses Stripe Payment Links (hosted by Stripe)
- All payment processing happens on Stripe's servers
- Site remains 100% static
- Works perfectly on GitHub Pages

### Security
- No payment data touches your site
- PCI compliance handled by Stripe
- HTTPS required (GitHub Pages provides this)
- Payment Links have built-in fraud protection

### URL Parameters Used
- `?donation=success` - Shows success notification
- `?donation=cancelled` - Shows cancel notification

These parameters are automatically added when Stripe redirects back to your site.

---

## What You Need to Do

### Required Steps:
1. **Create two Stripe Payment Links** (see STRIPE_SETUP_GUIDE.md)
   - One-time donation (customers choose amount)
   - Monthly recurring donation (customers choose amount)

2. **Update index.html** with your Payment Link URLs
   - Replace `YOUR_ONE_TIME_PAYMENT_LINK_HERE`
   - Replace `YOUR_MONTHLY_PAYMENT_LINK_HERE`

3. **Customize impact examples** (optional but recommended)
   - Edit the four donation amount cards
   - Use real Fourth Light Farm program costs

4. **Test everything** in test mode
   - Use Stripe test card: 4242 4242 4242 4242
   - Verify both donation types work
   - Check success/cancel flows

5. **Go live** when ready
   - Create live Payment Links in Stripe
   - Update index.html with live URLs
   - Deploy to GitHub Pages

---

## Files Modified

### `/index.html`
**Changes:**
- Added donation section (lines ~270-380)
- Updated navbar to include Donate link
- Changed hero "Donate" button to link to #donate section
- Added donation link to footer Quick Links
- Added JavaScript for success/cancel notification handling
- Uses existing Bulma CSS and Fourth Light Farm theme

**No New Files Created:**
- Everything integrates into existing index.html
- Uses existing theme.css for styling
- Uses existing Font Awesome icons

---

## Styling

### Colors Used (from theme.css)
- **Primary green** (`--flf-medium-green`): Icons, borders
- **Earth brown** (`--flf-earth-brown`): Text, buttons
- **Light tan** (`--flf-light-tan`): Backgrounds, dividers
- **Sage green** (`--flf-sage-green`): Secondary elements

### Components Used (from Bulma)
- `.section` - Section containers
- `.container` - Content width control
- `.box` - Card containers
- `.button` - Call-to-action buttons
- `.notification` - Success/error messages
- `.columns` - Responsive grid layout

### Custom Styling
- Impact cards have 2px tan borders
- Main donation box has 3px green border
- Buttons use custom Fourth Light Farm colors
- Notification is fixed position top-right
- Responsive design for mobile/tablet/desktop

---

## Testing Checklist

### Before Going Live:
- [ ] Verify Payment Links are created in Stripe
- [ ] Replace placeholder URLs in HTML
- [ ] Test one-time donation in test mode
- [ ] Test monthly donation in test mode
- [ ] Test cancel flow
- [ ] Verify success notification appears
- [ ] Verify cancel notification appears
- [ ] Check mobile responsiveness
- [ ] Verify email receipt arrives
- [ ] View test payment in Stripe Dashboard
- [ ] Customize donation impact examples
- [ ] Update any placeholder text

### When Going Live:
- [ ] Create live Payment Links in Stripe
- [ ] Complete Stripe account activation
- [ ] Add bank account for payouts
- [ ] Replace test URLs with live URLs
- [ ] Make a small real donation to test
- [ ] Announce to supporters!

---

## Future Enhancements (Optional)

### Easy Additions:
- Add more impact examples (education, workshops, specific programs)
- Include photos of programs being supported
- Add donation goal tracker/thermometer
- Show recent donor names (with permission)
- Add specific program donation options

### Medium Complexity:
- Add "donation in honor of" field
- Create donor wall/recognition page
- Integrate with Mailchimp for thank-you emails
- Add donation widget that follows on scroll
- Create monthly donor benefits/perks

### Advanced:
- Webhook integration for real-time tracking
- Custom Stripe Checkout session (requires backend)
- Donation matching campaigns
- Crowdfunding for specific projects
- Grant tracking and reporting

---

## Support Resources

### Stripe Resources:
- Payment Links guide: https://stripe.com/docs/payment-links
- Test mode: https://stripe.com/docs/testing
- Customer portal: https://stripe.com/docs/customer-management/portal

### Site Files:
- Setup guide: `/STRIPE_SETUP_GUIDE.md`
- Main website: `/index.html`
- Styling: `/theme.css`

### Questions?
Contact me if you need help with:
- Setting up Payment Links
- Customizing the donation section
- Testing the flow
- Going live with real payments
- Adding new features

---

## Summary

**What you have now:**
- ✅ Beautiful donation section matching your site theme
- ✅ Support for one-time and monthly donations
- ✅ Custom donation amounts (users choose)
- ✅ Donation impact examples to inspire giving
- ✅ Multiple CTAs throughout the site
- ✅ Success/cancel notification system
- ✅ Mobile-responsive design
- ✅ Zero backend code required
- ✅ Secure, PCI-compliant payment processing
- ✅ Automatic email receipts

**What you need to do:**
- 🔲 Create two Stripe Payment Links (10 minutes)
- 🔲 Add Payment Links to HTML (2 minutes)
- 🔲 Test the donation flow (5 minutes)
- 🔲 Customize impact examples (5 minutes)
- 🔲 Go live when ready!

**Total setup time:** ~20-30 minutes

---

Good luck with your fundraising! 🌱
