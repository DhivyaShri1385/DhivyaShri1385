# Setup Instructions

These files turn your static GitHub profile README into a self-updating one.

## File placement

Your special profile repo must be named exactly the same as your username
(e.g. github.com/YOUR_USERNAME/YOUR_USERNAME). Place the files like this:

```
YOUR_USERNAME/                       <- repo named after your username
├── README.md
└── .github/
    └── workflows/
        ├── blog-posts.yml
        └── recent-projects.yml
```

## Two find-and-replace edits

1. **YOUR_USERNAME** → your GitHub username (appears in README.md and
   recent-projects.yml).
2. **YOUR_HASHNODE_BLOG** → your Hashnode domain in blog-posts.yml.
   The feed URL must end in `/rss.xml`, e.g.
   `https://DhivyaShri1385.hashnode.dev/rss.xml` or your custom domain.

## What updates, and when

| Section            | Mechanism            | Refresh                       |
|--------------------|----------------------|-------------------------------|
| Stats / Top Langs  | Image widget         | Every page load (live)        |
| Streak             | Image widget         | Every page load (live)        |
| Activity Graph     | Image widget         | Every page load (live)        |
| Latest Projects    | GitHub Action        | Daily (midnight UTC)          |
| Latest Blog Posts  | GitHub Action        | Every 6 hours                 |

## First run / testing

The scheduled jobs won't fire instantly. To test now:
1. Push these files to your repo.
2. Go to the **Actions** tab.
3. Select each workflow → **Run workflow** (this is the `workflow_dispatch`
   trigger).

## Notes

- No secrets or tokens to add — the workflows use the built-in `GITHUB_TOKEN`
  that GitHub provides automatically.
- GitHub's scheduled Actions can run a few minutes late or skip during heavy
  load; that's normal and fine for a profile.
- If the blog section stays empty, double-check your Hashnode RSS URL loads in
  a browser and actually lists posts.
