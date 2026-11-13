# public-blog-posts

The text of my blog posts, one HTML file per post, named by the post's code
(`free-cloud-tiers.html` is the post with code `free-cloud-tiers`).

A file is only the body: no `<html>`, no `<head>`, no site layout. Every site that shows a post
wraps it in its own layout.

`posts.json` is the master list: one entry per post with its `code`, `title`, `summary`,
`publishedOn` (YYYY-MM-DD) and three topic flags, `isCrypto`, `isAi` and `isTrading`. The flags say
which sites list the post (stas.club: crypto, agentics.actor: AI, exchanges.bet: trading); one post can
have several. They are set by hand.

A nightly Google Cloud job (`BusyStas/gcp-jobs`, `lists-cache-uploader`) reads `posts.json` and copies
each listed post's file into the Cloudflare R2 bucket `public-blog-posts`, then writes the lists
(`blog-posts-all.json`, `-crypto`, `-ai`, `-trading`) into the bucket `public-blog-lists`. A file in
this repo that is not listed in `posts.json` is never published.

## Languages
English is the original, at the root. Every other language has a folder named by its code: `es`, `tr`, `ru`,
`zh`, `ja`, `de`, `pl`, `pt`, `hr`, `ar`, `th`, `ms` (Spanish, Turkish, Russian, Chinese, Japanese, German,
Polish, Portuguese, Croatian, Arabic, Thai, Malay). A folder holds:

- `<lang>/posts.json`: the translated `title` and `summary` of each post, by code
  (`{"posts": {"free-cloud-tiers": {"title": "...", "summary": "..."}}}`);
- `<lang>/<code>.html`: the translated body of the post with that code.

Both are optional, post by post: a post without a translated body shows the English text in that language
(the title and summary can still be translated), and a post without any translation shows entirely in English.
Dates, codes and the topic flags are not translated; they come from the root `posts.json`.
The job copies the same layout to R2: English at the root of the buckets, each language in its own folder
(`es/<code>.html` in `public-blog-posts`, `es/blog-posts-crypto.json` in `public-blog-lists`, and so on).
Today the 8 posts have translated titles and summaries in all 12 languages; the bodies are English for now.

This repository is public on purpose, so the job can download the files without a token.
Keep everything in it fit for the public: no drafts with private notes, no personal data.

## Adding a post
Every post needs both of these, in the same commit:
1. The file `<code>.html` here (lowercase letters, digits and dashes only).
2. Its entry in `posts.json` with the title, summary, **`publishedOn` date (YYYY-MM-DD)** and the three
   flags. A post without a date is rejected by the job, so it is never published.
3. Push to `main`. The next nightly run publishes it, or run the job by hand.
4. Its translations (see Languages): title and summary in each `<lang>/posts.json`, and the body as
   `<lang>/<code>.html` for each of the 12 languages, in the same commit.
