this repo is used to generate files in Cloudfare R2

# Adding a blog post (instructions for Claude)
When asked to add a post: create `<code>.html` (body only, no html/head) AND add its entry to `posts.json`
in the same commit, with title, summary, `publishedOn` (YYYY-MM-DD, never omit the date) and the flags
`isCrypto`, `isAi`, `isTrading`. Keep posts.json newest first. Push straight to main. Nothing private may go
in this repo: it is public.

# Languages
English is the original and lives at the root (`<code>.html`, `posts.json`). The other languages each have a folder:
es (Spanish), tr (Turkish), ru (Russian), zh (Chinese), ja (Japanese), de (German), pl (Polish), pt (Portuguese),
hr (Croatian), ar (Arabic), th (Thai), ms (Malay). In each folder:
- `<lang>/posts.json`: `{"posts": {"<code>": {"title": ..., "summary": ...}}}`, the translated title and summary
  of each post, by code.
- `<lang>/<code>.html`: the translated body, same format as the English file (HTML fragment, nothing else).
When asked to add a post, also add its title and summary to all 12 `<lang>/posts.json` files and translate the
body into all 12 `<lang>/<code>.html` files, in the same commit as the English post. Keep product names, code,
tickers, URLs and numbers as they are; translate the prose naturally, not word by word. A translation that is
missing is not an error: that language shows the English text until it exists (the 8 posts written before
2026-11-12 have translated titles and summaries only; bodies are still English). The job ignores a code that
is not in the root `posts.json`.

