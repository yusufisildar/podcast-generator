# Podcast Generator

Generates an RSS feed for a podcast from a YAML file — can be used as a standalone tool or as part of a CI/CD workflow (e.g. via GitHub Actions / Docker).

## Features

- Convert a simple YAML file describing your podcast metadata + episodes into a valid podcast RSS feed.  
- No external database required.  
- Easy to integrate in automated workflows (e.g. CI/CD, GitHub Actions).  
- Supports standard RSS/podcast metadata (title, description, link, language, episodes, etc.).  
- Licensed under MIT — free for personal or commercial use.

## Quick Start

### 1. Prepare a YAML file

Create a YAML file (e.g. `podcast.yml`) with metadata and episode list. Example format:

```yaml
title: "My Awesome Podcast"
description: "A podcast about interesting topics."
link: "https://example.com/podcast"
language: "en-us"
image: "/path/to/podcast-cover.jpg"

episodes:
  - title: "Episode 1 – Welcome"
    description: "Introduction to the show."
    published: "2025-01-01T10:00:00Z"
    file: "/audio/episode1.mp3"
    duration: "00:45:23"
    length: 12345678
  - title: "Episode 2 – Deep Dive"
    description: "In-depth discussion on topic X."
    published: "2025-01-15T10:00:00Z"
    file: "/audio/episode2.mp3"
    duration: "01:02:10"
    length: 23456789
  # ... add more episodes as needed
````

Make sure to update fields as appropriate: `title`, `description`, `link`, `language`, `image`, and under `episodes` — for each episode: `title`, `description`, `published`, `file`, `duration`, and `length`.

### 2. Run the generator

If you use Docker (provided in this repository):

```bash
docker build -t podcast-generator .
docker run --rm -v /path/to/your/podcast:/data podcast-generator /data/podcast.yml
```

Alternatively, you can run the generator directly (if applicable) to produce the `rss.xml` (or feed) file in the output directory of your choice.

### 3. Publish / Deploy

Once you have the generated feed (e.g. `rss.xml`), you can host it (alongside your audio files) on any static site or hosting solution.
Then submit the feed URL to directories / podcast platforms (e.g. Apple Podcasts, Spotify, etc).

## Usage in CI / CD / GitHub Actions

You can integrate the generator into an automated workflow to regenerate the feed every time you update your YAML file (e.g. add a new episode).
This makes it easy to maintain a podcast purely from version-controlled source (YAML + audio files).

## Project Structure

```
.
├── dockerfile           # Dockerfile for building a container image
├── entrypoint.sh        # Entrypoint script (for Docker / CLI usage)
├── feed.py              # Main script to parse YAML and generate RSS feed
└── LICENSE              # MIT License
```

## Prerequisites

* Docker (if you prefer containerized usage) **or** Python (depending on how feed.py is structured)
* A correctly formatted YAML file for your podcast metadata and episodes.
* Audio (or video) files for each episode, hosted so your feed links point to accessible URLs.

## License

This project is licensed under the [MIT License](LICENSE).

## Contributing

Contributions are welcome! Whether it’s bug reports, feature requests, improvements in feed format or metadata, feel free to open issues or pull requests.
If you integrate new features — please update documentation and add tests / examples when appropriate.

## Why This Project?

Maintaining a podcast feed manually (editing XML by hand) — especially for many episodes — is error-prone.
By using a YAML-driven approach + automation (Docker / CI), you get a clean, repeatable, version-controlled pipeline.
Ideal for developers, static-site publishers, or anyone who prefers automation over manual feed editing.

---

> **Note:** If your podcast grows in complexity (e.g. many episodes, cover images, multiple channels), you can extend the YAML schema / feed generator logic to support additional metadata (e.g. iTunes tags, categories, custom tags) as needed.
