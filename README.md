# Gotham Media House — self-hosted site (GitHub Pages)

This is the full custom build — timecode HUD, viewfinder brackets, the filterable
gallery, the lightbox, dark/light auto-switching — all intact. It's structured so
you can host it yourself on GitHub Pages and add or remove photos without touching
any code.

## What's in here

```
index.html          the whole site (one file, all five pages)
images/              banner/portrait photos — swap by re-uploading a file with the same name
images/gallery/      Our Work gallery + "From the field" photos
gallery.json         the list that drives the Our Work gallery
field.json           the list that drives the Home "From the field" strip
CNAME                tells GitHub Pages this site should answer to gothammediahouse.com
```

## One-time setup

1. **Create a GitHub account** if you don't have one already (github.com — free).
2. **Create a new repository.** Name it anything (e.g. `gmh-site`). Keep it Public
   (GitHub Pages on a free account needs the repo to be public — that only means the
   *code* is visible on GitHub, not anything about who visits your live site).
3. **Upload these files.** On the repo's page, click "Add file" → "Upload files",
   drag this whole folder's contents in (index.html, the images folder, the two
   .json files, and CNAME), and commit.
4. **Turn on Pages.** In the repo, go to Settings → Pages. Under "Build and
   deployment", set Source to "Deploy from a branch", branch `main`, folder `/root`.
   Save.
5. **Point your domain at it.** GitHub Pages will show you a `github.io` address
   immediately — that works right away. To use gothammediahouse.com itself, go to
   your domain's DNS settings (wherever you manage the domain — check Squarespace
   Domains, or your registrar if it's elsewhere) and add:
   - An `A` record for `@` pointing to each of: `185.199.108.153`, `185.199.109.153`,
     `185.199.110.153`, `185.199.111.153`
   - A `CNAME` record for `www` pointing to `<your-github-username>.github.io`
   Back in Settings → Pages, enter `gothammediahouse.com` as the custom domain and
   save (this is what the CNAME file in this folder does automatically once it's
   in the repo). DNS changes can take anywhere from a few minutes to a few hours
   to take effect.
6. **Important:** once gothammediahouse.com points here, it's no longer pointing
   at Squarespace. Don't cancel your Squarespace subscription until you've
   confirmed the new site is live and working — that way you always have a way
   back if something needs fixing.

## Adding or removing a photo — no code required

The Our Work gallery uses a "bento" layout — tiles are different sizes for visual
rhythm, and it automatically shows a "Load more" button once there are more than
12 items in the current filter, so you can keep adding photos (and videos)
without the page ever feeling unwieldy.

Open `gallery.json` in GitHub (click the file, then the pencil/edit icon). It's a
list like this:

```json
{ "type": "photo", "file": "images/gallery/lakeside-camera.jpg", "alt": "Cinema camera on tripod set up at a lakeside location for a scenic shoot", "category": "documentary" }
```

- **To add a photo:** upload the new image file into `images/gallery/` (Add file →
  Upload files), then add one more entry like the one above to `gallery.json` —
  `type` is `"photo"`, `file` is the path you just uploaded to, `alt` is a plain
  description (for accessibility and search), `category` is `narrative`,
  `documentary`, or `live`.
- **To remove one:** delete its entry from `gallery.json`. You can leave the image
  file in place or delete it too — either is fine.

**To add a video:** the gallery can also show videos from YouTube or Vimeo,
mixed right in with the photos — no separate video page. Add an entry like this:

```json
{ "type": "video", "file": "images/gallery/my-video-thumb.jpg", "alt": "Behind the scenes on the Acme Radio shoot", "category": "narrative", "videoEmbed": "https://www.youtube.com/embed/VIDEO_ID" }
```

- `type` is `"video"`.
- `file` is a thumbnail image for the tile (upload one to `images/gallery/` the
  same way as a photo — a still frame or a behind-the-scenes shot works well).
- `videoEmbed` is the video's **embed URL**, not the regular watch/share link:
  - **YouTube:** if the normal link is `https://www.youtube.com/watch?v=VIDEO_ID`,
    the embed URL is `https://www.youtube.com/embed/VIDEO_ID`.
  - **Vimeo:** if the normal link is `https://vimeo.com/VIDEO_ID`, the embed URL
    is `https://player.vimeo.com/video/VIDEO_ID`.
- Video tiles show a play icon over the thumbnail. Clicking one opens the video
  right in the lightbox and starts playing automatically.

Video entries always get a large tile, and every 5th photo gets one too, which is
what creates the varied bento layout — you don't need to set that yourself.

**Home "From the field" strip** works the same way, via `field.json` (no category
needed there, just `file` and `alt`) — keep it to 3 photos, since that's what the
layout is designed for.

**Banner photos** (the one hero shot on Home, the portrait and full-bleed banner on
About, the banner on Services, the background on Contact) are single fixed images —
`images/hero.jpg`, `images/about-portrait.jpg`, `images/about-banner.jpg`,
`images/services-banner.jpg`, `images/contact-bg.jpg`. To swap one, upload a new
file with that exact same name (GitHub will ask if you want to replace it — say
yes) and it updates automatically, no code edit needed.

Either way, changes go live within a minute or two of saving in GitHub — no build
step, no redeploy button to press.

## If you'd rather not manage this yourself

You don't have to use GitHub's web interface for every change — you're welcome to
bring photo changes back to this conversation and I'll make the edits and hand you
updated files to re-upload, the same as before. Self-hosting doesn't lock you out
of that; it's just what makes doing it yourself possible when you want to.
