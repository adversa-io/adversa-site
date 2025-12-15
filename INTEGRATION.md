# Integration Documentation: Adversa.io Marketing Site & Main Application

This document outlines the integration between the Adversa.io marketing website (adversa.io) and the main application (app.adversa.io).

## Overview

The marketing website serves as the public-facing platform for Adversa.io, while the main application at `https://app.adversa.io` provides the actual functionality for users to monitor competitor websites. The integration ensures seamless user navigation between both platforms.

## Integration Points

### 1. Navigation Header

The website header includes direct access to the application:

- **Login Link**: `https://app.adversa.io/?intent=login`
  - Location: Desktop navigation (top right)
  - Location: Mobile navigation menu
  - Purpose: Allow existing users to access their accounts
  - Query parameter hints user intent to the application

- **Sign Up Button**: `https://app.adversa.io/?intent=signup`
  - Location: Desktop navigation (highlighted button in top right)
  - Location: Mobile navigation menu
  - Purpose: Enable new users to create accounts
  - Query parameter hints user intent to the application

### 2. Hero Section CTAs

The main hero section includes two primary call-to-action buttons:

- **Get Started Button**: `https://app.adversa.io/?intent=signup`
  - Primary action button with accent color
  - Directs users to the application with signup intent
  - Query parameter hints user intent to the application

- **See Pricing Button**: `#pricing`
  - Secondary action button
  - Scrolls to the pricing section on the same page

### 3. Pricing Plans

All pricing plan buttons link to the application root with intent and plan-specific query parameters:

- **Founder Nano Plan**: `https://app.adversa.io/?intent=signup&plan=nano`
  - Price: $9 one-time payment
  - Features: 1 competitor, up to 5 URLs, weekly scraping, email notifications

- **Founder Micro Plan**: `https://app.adversa.io/?intent=signup&plan=micro`
  - Price: $59 one-time payment (marked as "Popular")
  - Features: 1 competitor, up to 5 URLs, daily scraping, AI summaries, email notifications

- **Founder Macro Plan**: `https://app.adversa.io/?intent=signup&plan=macro`
  - Price: $179 one-time payment
  - Features: 3 competitors, up to 10 URLs each, twice daily scraping, advanced AI analysis, priority support

**Query Parameters**: 
- `intent` parameter hints user intent (login/signup) to the application
- `plan` parameter allows the application to pre-select the appropriate plan during signup

### 4. Footer Links

Footer links provide access to legal and support pages:

- **Terms of Service**: `https://app.adversa.io/?page=terms`
- **Privacy Policy**: `https://app.adversa.io/?page=privacy`
- **Contact**: `https://app.adversa.io/?page=contact`

**Note**: All footer links point to the application root with a `page` parameter to indicate the desired page.

## Technical Implementation

### URL Structure

```
Marketing Site: https://adversa.io/
Main Application: https://app.adversa.io/
```

### Integration Pattern

The integration follows a simple static linking approach:
1. All application links use absolute URLs pointing to `https://app.adversa.io/` (root)
2. Query parameters are used to pass context (e.g., plan selection for pricing links)
3. The application handles all routing based on user authentication status
4. No JavaScript API calls or dynamic content loading required
5. Pure HTML anchor tags with `href` attributes

### User Flow

```
1. User visits adversa.io
2. User browses features, pricing, and information
3. User clicks on a CTA or pricing plan button
4. User is redirected to app.adversa.io (root) with optional query parameters
5. Application determines routing based on:
   - User authentication status (logged in or not)
   - Query parameters (e.g., plan selection)
   - Context of the request
6. User completes signup, login, or is routed to appropriate page
7. User begins using the monitoring service
```

## Configuration Requirements

### Application Requirements

The main application at `https://app.adversa.io` must support:

1. **Root Route Handling**:
   - `/` - Root route that handles authentication-based routing
   - Application determines where to direct users (login, signup, dashboard, etc.) based on authentication status and query parameters

2. **Query Parameter Handling at Root**:
   - `?intent=login` - Hints that user wants to log in
   - `?intent=signup` - Hints that user wants to sign up
   - `?intent=signup&plan=nano` - User wants to sign up for Founder Nano plan
   - `?intent=signup&plan=micro` - User wants to sign up for Founder Micro plan
   - `?intent=signup&plan=macro` - User wants to sign up for Founder Macro plan
   - `?page=terms` - User wants to view Terms of Service
   - `?page=privacy` - User wants to view Privacy Policy
   - `?page=contact` - User wants to access Contact page

3. **Intelligent Routing**:
   - The application should detect authenticated users and route them appropriately
   - Unauthenticated users should be directed to signup/login flows based on `intent` parameter
   - Query parameters should be preserved and used during the signup process
   - `page` parameters should direct users to the appropriate informational pages

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

- [ ] Desktop navigation "Login" button redirects to app root
- [ ] Desktop navigation "Sign Up" button redirects to app root
- [ ] Mobile menu "Login" link works correctly
- [ ] Mobile menu "Sign Up" link works correctly
- [ ] Hero "Get Started" button redirects to app root
- [ ] Founder Nano plan button includes `?plan=nano` parameter
- [ ] Founder Micro plan button includes `?plan=micro` parameter
- [ ] Founder Macro plan button includes `?plan=macro` parameter
- [ ] Footer "Terms" link redirects to app root
- [ ] Footer "Privacy" link redirects to app root
- [ ] Footer "Contact" link redirects to app root
- [ ] Application correctly routes users based on authentication status
- [ ] Query parameters are preserved during routing

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

1. Use absolute URLs pointing to root: `https://app.adversa.io/`
2. Include relevant query parameters for context (e.g., `?plan=nano`)
3. Let the application handle routing based on authentication
4. Update this documentation with new integration points
5. Test the link in both desktop and mobile views

### Updating Links

If the application URL structure changes:

1. Update all relevant links in `index.html`
2. Run validation commands to ensure consistency
3. Test all user flows thoroughly
4. Update this documentation

## Troubleshooting

### Common Issues

**Issue**: Links not working or showing 404 errors
- **Solution**: Verify the application root route is properly configured
- **Check**: Ensure `app.adversa.io` is properly deployed and the root route handles routing

**Issue**: Query parameters not being recognized by the application
- **Solution**: Confirm the application's root route handles the `plan` parameter
- **Check**: Review application code for parameter parsing at the root level

**Issue**: Users not being routed correctly
- **Solution**: Verify the application's authentication-based routing logic
- **Check**: Test with both authenticated and unauthenticated users

**Issue**: Mobile menu not showing new navigation items
- **Solution**: Clear browser cache and reload
- **Check**: Verify mobile menu HTML structure includes all navigation items

## Contact & Support

For integration issues or questions:
- Check application documentation at `app.adversa.io`
- Contact development team through the contact page
- Review application logs for routing issues

## Changelog

### 2025-12-15
- Updated all links to point to application root (`https://app.adversa.io/`)
- Application now handles routing based on authentication status
- Simplified integration pattern with centralized routing logic

### 2025-12-14
- Initial integration implementation
- Added Login and Sign Up links to navigation
- Connected all CTA buttons to application
- Added plan-specific query parameters to pricing buttons
- Updated footer links to application pages
- Created comprehensive integration documentation
