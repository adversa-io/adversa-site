# Integration Documentation: Adversa.io Marketing Site & Main Application

This document outlines the integration between the Adversa.io marketing website (adversa.io) and the main application (app.adversa.io).

## Overview

The marketing website serves as the public-facing platform for Adversa.io, while the main application at `https://app.adversa.io` provides the actual functionality for users to monitor competitor websites. The integration ensures seamless user navigation between both platforms.

## Integration Points

### 1. Navigation Header

The website header includes direct access to the application:

- **Login Link**: `https://app.adversa.io/login`
  - Location: Desktop navigation (top right)
  - Location: Mobile navigation menu
  - Purpose: Allow existing users to access their accounts

- **Sign Up Button**: `https://app.adversa.io/signup`
  - Location: Desktop navigation (highlighted button in top right)
  - Location: Mobile navigation menu
  - Purpose: Enable new users to create accounts

### 2. Hero Section CTAs

The main hero section includes two primary call-to-action buttons:

- **Get Started Button**: `https://app.adversa.io/signup`
  - Primary action button with accent color
  - Directs users to sign up for the service

- **See Pricing Button**: `#pricing`
  - Secondary action button
  - Scrolls to the pricing section on the same page

### 3. Pricing Plans

All pricing plan buttons link to the signup page with plan-specific query parameters:

- **Founder Nano Plan**: `https://app.adversa.io/signup?plan=nano`
  - Price: $9 one-time payment
  - Features: 1 competitor, up to 5 URLs, weekly scraping, email notifications

- **Founder Micro Plan**: `https://app.adversa.io/signup?plan=micro`
  - Price: $59 one-time payment (marked as "Popular")
  - Features: 1 competitor, up to 5 URLs, daily scraping, AI summaries, email notifications

- **Founder Macro Plan**: `https://app.adversa.io/signup?plan=macro`
  - Price: $179 one-time payment
  - Features: 3 competitors, up to 10 URLs each, twice daily scraping, advanced AI analysis, priority support

**Query Parameters**: The `?plan=` parameter allows the application to pre-select the appropriate plan for the user during signup, streamlining the onboarding process.

### 4. Footer Links

Footer links provide access to legal and support pages:

- **Terms of Service**: `https://app.adversa.io/terms`
- **Privacy Policy**: `https://app.adversa.io/privacy`
- **Contact**: `https://app.adversa.io/contact`

## Technical Implementation

### URL Structure

```
Marketing Site: https://adversa.io/
Main Application: https://app.adversa.io/
```

### Integration Pattern

The integration follows a simple static linking approach:
1. All application links use absolute URLs pointing to `https://app.adversa.io`
2. Query parameters are used to pass context (e.g., plan selection)
3. No JavaScript API calls or dynamic content loading required
4. Pure HTML anchor tags with `href` attributes

### User Flow

```
1. User visits adversa.io
2. User browses features, pricing, and information
3. User clicks on a CTA or pricing plan button
4. User is redirected to app.adversa.io with appropriate context
5. User completes signup or login in the application
6. User begins using the monitoring service
```

## Configuration Requirements

### Application Requirements

The main application at `https://app.adversa.io` must support:

1. **Authentication Routes**:
   - `/login` - User login page
   - `/signup` - User registration page

2. **Query Parameter Handling**:
   - `?plan=nano` - Pre-select Founder Nano plan
   - `?plan=micro` - Pre-select Founder Micro plan
   - `?plan=macro` - Pre-select Founder Macro plan

3. **Legal & Support Pages**:
   - `/terms` - Terms of Service
   - `/privacy` - Privacy Policy
   - `/contact` - Contact page

### DNS & Hosting

- **Marketing Site**: Hosted on GitHub Pages (or similar) at `adversa.io`
- **Main Application**: Hosted at `app.adversa.io`
- **CNAME Records**: Ensure proper DNS configuration for both domains

### CORS & Security

Since the integration uses simple navigation (HTML links) rather than API calls:
- No CORS configuration needed
- No authentication token passing required
- No cross-domain JavaScript communication

## Testing

### Manual Testing Checklist

- [ ] Desktop navigation "Login" button redirects to app login page
- [ ] Desktop navigation "Sign Up" button redirects to app signup page
- [ ] Mobile menu "Login" link works correctly
- [ ] Mobile menu "Sign Up" link works correctly
- [ ] Hero "Get Started" button redirects to app signup
- [ ] Founder Nano plan button includes `?plan=nano` parameter
- [ ] Founder Micro plan button includes `?plan=micro` parameter
- [ ] Founder Macro plan button includes `?plan=macro` parameter
- [ ] Footer "Terms" link goes to app terms page
- [ ] Footer "Privacy" link goes to app privacy page
- [ ] Footer "Contact" link goes to app contact page

### Validation

```bash
# Check all app.adversa.io links in the HTML
grep -n "app.adversa.io" index.html

# Verify no broken javascript:void(0) links remain
grep -n "javascript:void(0)" index.html
```

## Maintenance

### Adding New Links

When adding new links to the application:

1. Use absolute URLs: `https://app.adversa.io/path`
2. Include relevant query parameters for context
3. Update this documentation with new integration points
4. Test the link in both desktop and mobile views

### Updating Links

If the application URL structure changes:

1. Update all relevant links in `index.html`
2. Run validation commands to ensure consistency
3. Test all user flows thoroughly
4. Update this documentation

## Troubleshooting

### Common Issues

**Issue**: Links not working or showing 404 errors
- **Solution**: Verify the application routes exist and are accessible
- **Check**: Ensure `app.adversa.io` is properly configured and deployed

**Issue**: Query parameters not being recognized by the application
- **Solution**: Confirm the application's signup page handles the `plan` parameter
- **Check**: Review application code for parameter parsing

**Issue**: Mobile menu not showing new navigation items
- **Solution**: Clear browser cache and reload
- **Check**: Verify mobile menu HTML structure includes all navigation items

## Contact & Support

For integration issues or questions:
- Check application documentation at `app.adversa.io`
- Contact development team through the contact page
- Review application logs for routing issues

## Changelog

### 2025-12-14
- Initial integration implementation
- Added Login and Sign Up links to navigation
- Connected all CTA buttons to application
- Added plan-specific query parameters to pricing buttons
- Updated footer links to application pages
- Created comprehensive integration documentation
