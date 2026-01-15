# Setting Up GitHub Pages

This guide explains how to enable and configure GitHub Pages for the WindPulse project.

## Quick Setup

### Step 1: Enable GitHub Pages

1. Go to your repository on GitHub: `https://github.com/Samsomyajit/windpulse`
2. Click on **Settings** tab
3. Scroll down to **Pages** section in the left sidebar
4. Under **Source**, select:
   - **Branch**: `main` (or your default branch)
   - **Folder**: `/docs`
5. Click **Save**

### Step 2: Wait for Deployment

GitHub will automatically build and deploy your site. This usually takes 1-2 minutes.

Your site will be available at: `https://samsomyajit.github.io/windpulse/`

### Step 3: Verify

Once deployed, visit your site and verify:
- Homepage loads correctly
- Navigation links work
- Images display properly
- All documentation pages are accessible

## Configuration Details

### Jekyll Theme

The site uses the **Cayman theme**, configured in `docs/_config.yml`:

```yaml
theme: jekyll-theme-cayman
title: WindPulse
description: Heat Map-Based Clustered Diurnal Wind Power Density Analysis
```

### Site Structure

```
docs/
├── _config.yml          # Jekyll configuration
├── index.md            # Homepage
├── methodology.md      # Methodology page
├── results.md          # Results page
└── gallery.md          # Image gallery
```

### Custom Domain (Optional)

To use a custom domain:

1. Create a file named `CNAME` in the `docs/` directory
2. Add your domain name (e.g., `windpulse.yourdomain.com`)
3. Configure DNS with your domain provider:
   - Add a CNAME record pointing to `samsomyajit.github.io`
4. Update the CNAME file in GitHub Pages settings

## Updating the Site

### Making Changes

1. Edit markdown files in the `docs/` directory
2. Commit and push changes:
```bash
git add docs/
git commit -m "Update documentation"
git push origin main
```

3. GitHub Pages will automatically rebuild (1-2 minutes)

### Adding New Pages

1. Create a new `.md` file in `docs/`:
```bash
touch docs/newpage.md
```

2. Add front matter:
```yaml
---
layout: default
title: Your Page Title
---

# Your Page Title

Your content here...
```

3. Add navigation link in `index.md`:
```markdown
- [New Page](newpage.md)
```

### Adding Images

Images are stored in the `images/` directory at the repository root.

To reference in documentation:
```markdown
![Description](../images/image_001.png)
```

## Advanced Configuration

### Custom CSS

Create `docs/assets/css/style.scss`:

```scss
---
---

@import "{{ site.theme }}";

/* Your custom styles here */
.custom-class {
  color: #0066cc;
}
```

### Custom Layout

Create `docs/_layouts/default.html` to override the theme layout:

```html
<!DOCTYPE html>
<html lang="{{ site.lang | default: "en-US" }}">
  <head>
    <!-- Your custom head content -->
  </head>
  <body>
    {{ content }}
  </body>
</html>
```

### Analytics

Add Google Analytics to `_config.yml`:

```yaml
google_analytics: UA-XXXXXXXXX-X
```

## Troubleshooting

### Pages Not Building

**Check build status:**
1. Go to repository **Actions** tab
2. Look for "pages build and deployment" workflow
3. Check for errors in the build log

**Common issues:**
- Syntax errors in markdown files
- Invalid YAML front matter
- Missing theme dependencies

**Solution:**
```bash
# Test locally with Jekyll
gem install bundler jekyll
cd docs
bundle exec jekyll serve
```

### Images Not Displaying

**Issue**: Images show broken link icon

**Solutions:**
1. Check image path is correct (relative to markdown file)
2. Verify images are in the repository
3. Ensure image files are committed and pushed
4. Check image file extensions (case-sensitive)

### Navigation Links Not Working

**Issue**: Clicking links results in 404

**Solutions:**
1. Use relative paths: `methodology.md` not `/methodology.md`
2. Enable relative links in `_config.yml`:
```yaml
plugins:
  - jekyll-relative-links
relative_links:
  enabled: true
```

### Theme Not Applying

**Issue**: Site appears unstyled

**Solutions:**
1. Verify `_config.yml` theme setting
2. Check if theme is supported by GitHub Pages
3. Clear browser cache
4. Wait for full deployment (can take up to 10 minutes)

## Testing Locally

### Install Jekyll

```bash
# On macOS/Linux
gem install bundler jekyll

# On Windows
# Use RubyInstaller: https://rubyinstaller.org/
```

### Create Gemfile

In `docs/` directory:

```ruby
source 'https://rubygems.org'
gem 'github-pages', group: :jekyll_plugins
```

### Run Local Server

```bash
cd docs
bundle install
bundle exec jekyll serve
```

Visit: `http://localhost:4000/windpulse/`

## Performance Optimization

### Image Optimization

Optimize images before committing:

```bash
# Install ImageMagick
# On macOS: brew install imagemagick
# On Linux: apt-get install imagemagick

# Optimize images
for img in images/*.png; do
  convert "$img" -strip -quality 85% "$img"
done
```

### Lazy Loading

Add lazy loading to images in markdown:

```html
<img src="../images/image_001.png" loading="lazy" alt="Description">
```

## SEO Optimization

### Add Meta Tags

In `_config.yml`:

```yaml
title: WindPulse
description: Your detailed description
url: https://samsomyajit.github.io
baseurl: /windpulse
```

### Add Sitemap

GitHub Pages automatically generates a sitemap at:
`https://samsomyajit.github.io/windpulse/sitemap.xml`

### Add robots.txt

Create `docs/robots.txt`:

```
User-agent: *
Allow: /
Sitemap: https://samsomyajit.github.io/windpulse/sitemap.xml
```

## Monitoring

### Check Site Health

1. **Google Search Console**: Submit sitemap
2. **PageSpeed Insights**: Check performance
3. **GitHub Actions**: Monitor build status

### Analytics

Track visitors using:
- Google Analytics (free)
- GitHub traffic insights
- Matomo (privacy-friendly alternative)

## Best Practices

1. **Keep URLs stable**: Don't rename files after publishing
2. **Use descriptive filenames**: `methodology.md` not `page2.md`
3. **Optimize images**: Compress before committing
4. **Test locally**: Before pushing to main branch
5. **Update regularly**: Keep documentation current
6. **Monitor errors**: Check GitHub Actions for build failures

## Additional Resources

- [GitHub Pages Documentation](https://docs.github.com/en/pages)
- [Jekyll Documentation](https://jekyllrb.com/docs/)
- [Markdown Guide](https://www.markdownguide.org/)
- [Cayman Theme](https://github.com/pages-themes/cayman)

## Support

For issues with GitHub Pages setup:
- [GitHub Pages Forum](https://github.community/c/github-pages/24)
- [Jekyll Talk Forum](https://talk.jekyllrb.com/)
- [Stack Overflow](https://stackoverflow.com/questions/tagged/github-pages)

---

Once your site is live, share it! 🚀

Your site will be at: **https://samsomyajit.github.io/windpulse/**
