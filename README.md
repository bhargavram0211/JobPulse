# JobPulse

**Find freshly posted LinkedIn jobs instantly.**

JobPulse is a single-page web tool that generates filtered LinkedIn job search URLs using the `f_TPR` (time posted range) parameter — so you only see jobs posted in the last 1, 3, 6, 12, or 24 hours instead of sifting through weeks-old listings.

🔗 **Live:** [bhargavram0211.github.io/JobPulse](https://bhargavram0211.github.io/JobPulse)

---

## How It Works

1. Enter a **Job Title** (e.g. "Software Engineer")
2. Enter a **Location** (suggestions provided, or type your own)
3. Select a **Time Range**
4. Click **Search on LinkedIn ↗** — opens filtered results in a new tab instantly

The URL it constructs:
```
https://www.linkedin.com/jobs/search/?keywords={title}&location={location}&f_TPR=r{seconds}
```

| Time Range  | `f_TPR` value |
|-------------|---------------|
| Last 1 Hour | `r3600`       |
| Last 3 Hours| `r10800`      |
| Last 6 Hours| `r21600`      |
| Last 12 Hours| `r43200`     |
| Last 24 Hours| `r86400`     |

---

## Tech Stack

- Vanilla HTML, CSS, and JavaScript — no frameworks, no dependencies
- Single file (`index.html`) — no build step required
- Hosted on GitHub Pages

## Local Development

Just open `index.html` in any browser. No server or install needed.

---

Built by [@bhargavram0211](https://github.com/bhargavram0211)
