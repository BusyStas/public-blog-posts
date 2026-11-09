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

This repository is public on purpose, so the job can download the files without a token.
Keep everything in it fit for the public: no drafts with private notes, no personal data.

## Adding a post
Every post needs both of these, in the same commit:
1. The file `<code>.html` here (lowercase letters, digits and dashes only).
2. Its entry in `posts.json` with the title, summary, **`publishedOn` date (YYYY-MM-DD)** and the three
   flags. A post without a date is rejected by the job, so it is never published.
3. Push to `main`. The next nightly run publishes it, or run the job by hand.
