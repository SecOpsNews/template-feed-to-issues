# Feed to issues

Watch the RSS and Atom feeds your team cares about, such as vendor advisories, status pages and security blogs, and get each new item as a GitHub issue. Assign issues, comment on them, link them to your own work, and let old ones close themselves.

It's the set-up behind [SecOpsNews](https://secops.thechels.uk), cut down to one file you edit.

## Use it

1. Select **Use this template** → **Create a new repository**. A private repository works too.
2. Edit the feed list in [`.github/workflows/feeds.yml`](.github/workflows/feeds.yml). Each feed needs a `name` (one word, used for the issue prefix and label) and a `feed` URL:

   ```yaml
   - name: Cloudflare
     feed: "https://www.cloudflarestatus.com/history.atom"
   ```

3. Run **Feeds** once from the **Actions** tab to check it works. After that it runs every 2 hours and opens an issue for each item from the last 24 hours, unless an issue with the same title already exists.

To get notified, watch your new repository (**Watch** → **All activity**), or filter notifications by label.

## Options

- **How often it runs:** change the `cron` line in `feeds.yml`.
- **How long issues stay open:** [`.github/workflows/stale.yml`](.github/workflows/stale.yml) closes items after 3 days with no activity. Add the `keep` label to an issue to keep it open, or delete the file to keep everything.
- **Ignore some items:** add `titleFilter` or `contentFilter` to the action's settings with a regular expression. Items that match are skipped, such as `titleFilter: "(?i)scheduled maintenance"`.
- **More labels:** set `labels` in `feeds.yml` to a comma-separated list, such as `${{ matrix.name }}, vendor`.

## Finding feeds

[SecOpsNews's feed list](https://secops.thechels.uk/feeds.opml) has more than 30 security news, advisory, CVE, breach and status-page feeds to start from. The dashboard at [secops.thechels.uk](https://secops.thechels.uk) shows them all in one place.

## Credits

Issues are created by [guilhem/rss-issues-action](https://github.com/guilhem/rss-issues-action). MIT licensed: see [LICENSE](LICENSE).
