# launchpage.xyz

A modern, minimalist landing page for domains waiting to launch. Perfect for showing a professional presence while you build your main site, collect early interest, or prevent domain parking spam flags.

## Features

- **Clean, Modern Design** - Responsive layout that works beautifully on all devices
- **Email Collection** - Built-in form to collect visitor emails and build your waitlist
- **Multi-Domain Support** - Automatically detects and displays the current domain name
- **Dark Mode** - Animated toggle with rocket icon
- **Zero Dependencies** - Pure HTML, CSS, and JavaScript - no frameworks needed
- **Free Hosting** - Deploy to Netlify, Vercel, GitHub Pages, Cloudflare Pages, or your own VPS
- **Easy Customization** - Simple to update colors, text, and branding

## Why?

Originally created to avoid Facebook blocking newly registered domains. Facebook was flagging domain registrar parking pages (like GoDaddy's ad-filled parkers) as spam. By pointing new domains to a clean, professional launchpage instead, you can:

- Maintain domain reputation
- Collect early interest from visitors
- Show a professional presence immediately
- Build a waitlist before your product launches

## Quick Start

### 1. Deploy Your Launchpage

Choose your preferred hosting platform:

- **[Netlify](https://launchpage.xyz/deploy-netlify.html)** - Easiest setup, automatic SSL
- **[Vercel](https://launchpage.xyz/deploy-vercel.html)** - Lightning-fast edge network
- **[GitHub Pages](https://launchpage.xyz/deploy-github-pages.html)** - 100% free with Git integration
- **[Cloudflare Pages](https://launchpage.xyz/deploy-cloudflare-pages.html)** - Global CDN with 275+ PoPs
- **[Hetzner VPS](https://launchpage.xyz/deploy-hetzner.html)** - Full control, unlimited domains

See full deployment guides at [launchpage.xyz/docs.html](https://launchpage.xyz/docs.html)

### 2. Customize Your Page

Edit `index.html` to personalize:

```html
<!-- Update colors -->
<style>
:root {
    --color-bg-start: #1A2F42;
    --color-bg-end: #2C5F7C;
    --color-accent: #4A9BAE;
}
</style>

<!-- Update text -->
<h1 class="title">
    <span class="domain-name">yourdomain.com</span><br>
    is launching soon
</h1>
```

The domain name will automatically update based on the URL!

### 3. Setup Email Collection (Optional)

To collect visitor emails, deploy the Cloudflare Worker:

**Repository:** [github.com/simplebytes-com/launchpage-contact-worker](https://github.com/simplebytes-com/launchpage-contact-worker)

**Quick setup:**

```bash
# Clone the worker repository
git clone https://github.com/simplebytes-com/launchpage-contact-worker.git
cd launchpage-contact-worker

# Install Wrangler CLI
npm install -g wrangler

# Login to Cloudflare
wrangler login

# Create KV namespace for storing submissions
wrangler kv:namespace create "SUBMISSIONS"

# Deploy the worker
wrangler deploy
```

Then update the form action in `index.html`:

```html
<form class="email-form" id="emailForm" method="POST"
      action="https://YOUR-WORKER-URL.workers.dev">
```

**Full setup guide:** [launchpage.xyz/setup-notifications.html](https://launchpage.xyz/setup-notifications.html)

## How It Works

### The Launchpage

- Pure HTML/CSS/JavaScript - no build process needed
- Automatically detects the domain name via `window.location.hostname`
- Responsive design works on all screen sizes
- Dark mode toggle with smooth animations
- Form validation and spam protection (honeypot field)

### The Email Collection Worker

The Cloudflare Worker (separate repository):

- Receives form submissions via POST request
- Validates data and checks honeypot for spam
- Stores submissions in Cloudflare KV storage
- Supports CORS for cross-origin requests
- Works with unlimited domains from a single worker

**What gets stored in KV:**
- Email address
- Domain submitted from
- Timestamp
- Any additional form fields

**Note:** The worker stores submissions - it does not send email notifications. You access submissions by viewing your Cloudflare KV namespace in the dashboard.

## Customization

### Update Analytics

Replace the Plausible analytics script with your own:

```html
<script defer data-domain="yourdomain.com"
        src="https://analytics.simplebytes.com/js/script.pageview-props.tagged-events.js">
</script>
```

Or use Google Analytics, Fathom, or any other analytics provider.

### Change the Rocket Icon

The rocket SVG is inline in the HTML. You can replace it with any emoji or icon:

```html
<!-- Replace with emoji -->
<div class="rocket-container">🚀</div>

<!-- Or use an image -->
<div class="rocket-container">
    <img src="your-logo.png" alt="Logo">
</div>
```

### Multi-Domain Setup

The page automatically detects the domain, but you can customize the display logic:

```javascript
// In the <script> section
const currentDomain = window.location.hostname;
const prettyDomain = currentDomain
    .replace('www.', '')
    .replace('.xyz', ''); // Remove .xyz TLD if desired

domainElement.textContent = prettyDomain;
```

## File Structure

```
launchpage.xyz/
├── index.html          # Main launchpage (copy this to your project)
├── img/
│   ├── favicons/      # Favicon files
│   ├── screenshot.jpg # Desktop preview
│   └── screenshot-mobile.jpg # Mobile preview
├── example.html        # Live example (for marketing site)
├── docs.html          # Documentation hub
├── deploy-*.html      # Platform-specific deployment guides
└── setup-notifications.html # Email collection setup guide
```

**For your launchpage deployment:** You only need `index.html` and the `img/favicons/` folder.

## Live Examples

- **Demo:** [launchpage.xyz/example.html](https://launchpage.xyz/example.html)
- **Documentation:** [launchpage.xyz/docs.html](https://launchpage.xyz/docs.html)
- **Worker Repository:** [github.com/simplebytes-com/launchpage-contact-worker](https://github.com/simplebytes-com/launchpage-contact-worker)

## Browser Support

- Chrome/Edge (modern versions)
- Firefox (modern versions)
- Safari 12+
- Mobile browsers (iOS Safari, Chrome Android)

## Contributing

Pull requests are welcome! Improvements and optimizations are appreciated.

### Ideas for Contributions

- Additional color themes
- More animation options
- Accessibility improvements
- Performance optimizations
- Alternative form handlers

## License

[MIT](https://choosealicense.com/licenses/mit/)

---

**Proudly powered by [TCG](https://www.codeero.com?ref=launchpage) and [Simple Bytes](https://simplebytes.com?ref=launchpage)**
