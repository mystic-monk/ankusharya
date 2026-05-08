# Portfolio Site Deployment Guide — Render

## Quick Start

This is a static portfolio site ready to deploy on Render. All files are production-ready with no build step required.

---

## Step 1: Create a Free Render Account

1. Go to [render.com](https://render.com)
2. Sign up with email or GitHub account
3. Verify your email
4. You now have a free tier account ready for static site deployment

---

## Step 2: Deploy This Portfolio as a Static Site

### Option A: Deploy from Folder (Recommended for Quick Start)

1. In Render dashboard, click **+ New**
2. Select **Static Site**
3. Upload this folder (or drag and drop)
4. Render auto-detects `index.html` as the entry point
5. Click **Deploy**
6. Your site is live at `https://your-random-name.onrender.com`

### Option B: Deploy from GitHub (Recommended for Ongoing Updates)

1. Push this portfolio folder to a GitHub repository
2. In Render dashboard, click **+ New → Static Site**
3. Connect your GitHub account
4. Select the repository
5. Set **Build Command**: (leave empty)
6. Set **Publish Directory**: `.` (the root folder containing index.html)
7. Click **Create Static Site**
8. Render will redeploy automatically when you push changes

---

## Step 3: Connect Custom Domains

### Connect ankusharya.dev (or ankusharya.io)

1. In Render, open your Static Site
2. Go to **Settings → Custom Domain**
3. Enter `ankusharya.dev`
4. Render provides DNS instructions
5. Go to your domain registrar (Namecheap, GoDaddy, etc.)
6. Update DNS to Render's nameservers (or add CNAME record if using subdomains)
7. Wait 5–30 minutes for DNS propagation
8. Your portfolio is live at `https://ankusharya.dev`

### Optional: Connect sheknowstoomuch.com Later

Repeat the above for a second static site pointing to the same folder (or a newsletter-specific version).

---

## Step 4: Replace Placeholders

### GA4 Measurement ID

In **all HTML files** (index.html, about.html, projects.html, etc.):

```html
<!-- BEFORE -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-VD4V5PJECV"></script>
<script>
  gtag('config', 'G-VD4V5PJECV');
</script>

<!-- AFTER -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-YOUR-ACTUAL-ID"></script>
<script>
  gtag('config', 'G-YOUR-ACTUAL-ID');
</script>
```

Get your GA4 ID from [analytics.google.com](https://analytics.google.com).

### Formspree Endpoint (contact.html)

1. Go to [formspree.io](https://formspree.io)
2. Sign up (free)
3. Add a new form
4. Copy your form endpoint (e.g., `https://formspree.io/f/xyzabc123`)
5. In `contact.html`, replace:

```html
<!-- BEFORE -->
<form class="contact-form" action="https://formspree.io/f/YOUR_FORM_ID" method="post">

<!-- AFTER -->
<form class="contact-form" action="https://formspree.io/f/xyzabc123" method="post">
```

### Render Service URLs (projects.html)

Once you deploy your Python projects as Render Web Services (see Step 5 below), replace the placeholders in `projects.html`:

```html
<!-- BEFORE -->
<!-- Replace with your Render service URL -->
<a class="button button-secondary" href="https://your-rag-app.onrender.com">Live Demo</a>

<!-- AFTER -->
<a class="button button-secondary" href="https://actual-rag-service-name.onrender.com">Live Demo</a>
```

---

## Step 5: Deploy Python Projects as Render Web Services

Each of your 4 Python projects (Route Licensing, Bus Scorecard, RAG App, Intake App) deploys separately.

### For Each Project:

1. **Push your project repo to GitHub**
   - Ensure it has a `requirements.txt` and your app entry point (e.g., `main.py` for FastAPI or `app.py` for Streamlit)

2. **In Render Dashboard, click + New → Web Service**

3. **Connect GitHub repo**
   - Select the repository
   - Branch: `main`

4. **Configure the service:**
   - **Name**: `route-licensing-ui` (use descriptive names)
   - **Environment**: `Python 3.11` (or appropriate version)
   - **Build Command**: `pip install -r requirements.txt`
   - **Start Command**: 
     - For FastAPI: `uvicorn main:app --host 0.0.0.0 --port 10000`
     - For Streamlit: `streamlit run app.py --server.port=10000 --server.address=0.0.0.0`

5. **Click Create Web Service**

6. **Render auto-deploys and provides a URL** like `https://route-licensing-ui.onrender.com`

7. **Copy this URL and update projects.html**

### Services to Deploy:

| Project | Service Name | Start Command |
|---------|--------------|--------------|
| Route Licensing UI | `route-licensing-ui` | `streamlit run app.py --server.port=10000` |
| Bus Scorecard | `bus-scorecard` | `streamlit run app.py --server.port=10000` |
| RAG Policy App | `rag-policy-app` | `streamlit run app.py --server.port=10000` |
| AI Intake App | `ai-intake-app` | `uvicorn main:app --host 0.0.0.0 --port 10000` |

---

## Step 6: Add New Blog Articles

To add blog posts without a CMS:

1. Create a new HTML file (e.g., `blog-my-first-post.html`)
2. Copy the template from `blog.html`, keeping the header, nav, and footer
3. Update the title and main content
4. In `blog.html`, add a link to the new post:

```html
<ul>
  <li><a href="blog-my-first-post.html">My First Post</a></li>
  <li><a href="blog-another-post.html">Another Insight</a></li>
</ul>
```

5. Push the new files to GitHub
6. Render auto-redeploys

---

## Render Account Structure Reference

Once fully set up, your Render dashboard will look like:

```
Render Account (ankush@example.com)
├── ankusharya.dev              Static Site    ← This portfolio
├── sheknowstoomuch.com         Static Site    ← Newsletter site (optional)
├── route-licensing-ui          Streamlit App
├── bus-scorecard               Streamlit App
├── rag-policy-app              Streamlit App
└── ai-intake-app               Web Service (FastAPI)
```

---

## Troubleshooting

### Static Site Not Deploying

- Ensure `index.html` is in the root folder
- Check that all CSS and JS files use relative paths (no absolute `/` paths)
- In Render, set **Publish Directory** to `.` (not a subfolder)

### Custom Domain Not Resolving

- Wait 30+ minutes for DNS propagation
- Check that DNS records match Render's instructions exactly
- Use [mxtoolbox.com](https://mxtoolbox.com) to verify DNS

### Python Service Fails to Start

- Ensure `requirements.txt` lists all dependencies
- Check **Build Logs** in Render dashboard for error messages
- Verify start command matches your app file name
- For Streamlit: add `--logger.level=debug` to see errors

### Forms Not Submitting

- Verify Formspree endpoint in form `action` attribute
- Test locally first
- Check Formspree dashboard for form submissions
- Update email in Formspree to receive notifications

---

## Security & Best Practices

- **Never commit secrets** (API keys, passwords) to GitHub
  - Use Render **Environment Variables** for sensitive data
  - In Render service settings → **Environment**

- **Keep GA4 ID private** (it's public-facing but not sensitive)

- **Monitor costs** — Render free tier includes:
  - 3 static sites (400 hours/month)
  - 1 web service instance (750 hours/month)
  - Paid upgrades available if needed

- **Auto-redeploys** — Any push to GitHub auto-deploys on Render

---

## Next Steps

1. ✅ Create Render account
2. ✅ Deploy this portfolio
3. ✅ Connect ankusharya.dev domain
4. ✅ Replace GA4 placeholder
5. ✅ Replace Formspree endpoint
6. ✅ Deploy Python projects (when ready)
7. ✅ Update projects.html with live demo links
8. ✅ Add blog articles as needed

---

**Questions?** Render docs: [render.com/docs](https://render.com/docs)
