# ISM4421EL — Music Studio

A one-page AI music generator built on the [Suno API](https://docs.sunoapi.org). It's a single static HTML file with no build step and no server, ready for Netlify.

## Bring your own API key

Each visitor clicks **🔑 Add API key** and pastes their own Suno API key from <https://sunoapi.org/api-key>. The key is:

- checked right away against the credits endpoint,
- saved only in that browser's `localStorage`,
- sent only to `api.sunoapi.org`,
- removable at any time with the **Remove key** button.

Generations use the visitor's own credits.

## Features

- **Simple mode**: describe a song, pick a genre, and the AI writes the lyrics and music.
- **Custom mode**: your own title and lyrics, length (10 s–6 min), vocal voice, styles to avoid, style adherence, weirdness, and variety.
- **✨ Write lyrics with AI**: generates lyric options you can drop straight into the song.
- **Instrumental toggle** and a model picker (V6, V6 Wild, V6 Mini).
- **Live progress**: tracks start streaming as soon as the first one is ready. Each request returns 2 versions.
- **Player, MP3 download, copy link, and lyrics** for every track.
- **Extend**: continue any finished track from a point you choose.
- **Credit balance** in the header. Click it to refresh.
- **History** saved in the browser, and unfinished jobs resume after a reload.

## Suno endpoints used

| Feature | Endpoint |
|---|---|
| Credit balance / key check | `GET /api/v1/generate/credit` |
| Generate music | `POST /api/v1/generate` |
| Track status & results | `GET /api/v1/generate/record-info?taskId=` |
| Extend a track | `POST /api/v1/generate/extend` |
| AI lyrics | `POST /api/v1/lyrics` |
| Lyrics results | `GET /api/v1/lyrics/record-info?taskId=` |

The app gets results by polling. Suno requires a `callBackUrl`, so the app sends one, but it doesn't need the callback.

## Deploy to Netlify

1. In Netlify, choose **Add new site → Import an existing project** and pick this repo, on the `main` branch.
2. Leave the build command empty. `netlify.toml` sets the publish directory to `public`.
3. Deploy. No environment variables are needed.

You can also drag the `public/` folder onto <https://app.netlify.com/drop>.

To try it locally, serve the folder with any static server, for example `npx serve public`.
