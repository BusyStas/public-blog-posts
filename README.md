# public-blog-posts

The text of my blog posts, one HTML file per post, named by the post's code
(`free-cloud-tiers.html` is the post with code `free-cloud-tiers`).

A file is only the body: no `<html>`, no `<head>`, no site layout. Every site that shows a post
wraps it in its own layout.

The post's title, date, summary and topic flags (crypto, AI, trading) live in the
`BlogPosts` table of the PersonalAssistants database, not here. A nightly Google Cloud job
(`BusyStas/gcp-jobs`, `lists-cache-uploader`) reads that table, then copies each listed post's
file from this repo into the Cloudflare R2 bucket `public-blog-posts`. A file in this repo that is
not in the table is never published.

This repository is public on purpose, so the job can download the files without a token.
Keep everything in it fit for the public: no drafts with private notes, no personal data.

## Adding a post
1. Add `<code>.html` here (lowercase letters, digits and dashes only).
2. Add its row to `BlogPosts` (`EXEC WebAPI.BlogPost_Save ...`) with the title, summary, date and flags.
3. The next nightly run publishes it, or run the job by hand.
