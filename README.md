# Colab Creative Engine

Clone this public open source 100% working project and make it working here as on fresh environment 

https://github.com/qcute2038-code/script-to-epic.git





I got most of the Colab GPU encoding path in place, but the last UI edit landed in the wrong spot and broke the page's JSX, so the app won't build right now.



What's done:

- `public/colab/encoder_server.py` — the Colab-side encoder: downloads panels, applies the same Ken Burns moves and colour grades as the browser engine, encodes with the T4's NVENC hardware encoder (CPU fallback), cross-fades in groups of 40 and stream-copy concatenates them so thousands of panels / 2h+ runtimes stay memory-flat. Exposes `/health`, `POST /render`, `/status/:id`, `/download/:id.mp4` with CORS.

- `public/colab/scene-weaver-gpu-encoder.ipynb` — the notebook the user runs in their own Colab account: checks the T4, installs ffmpeg + cloudflared, starts the encoder and prints a public https link.

- `src/lib/colab.ts` — client for connecting, dispatching a job, polling progress (tolerant of tunnel hiccups) and returning a download URL.

- `src/routes/index.tsx` — added `checkColab()` and `makeVideoOnColab()`, plus split "Build video" into Encode on Colab GPU and Build in browser.



What remains (one small fix):

The Colab connection panel got inserted at line ~663 instead of after the progress `</section>` at ~634, leaving an unbalanced JSX block — `src/routes/index.tsx(639,11): JSX expressions must have one parent element` and a missing `)` at 716. The panel markup itself is correct; it just needs to be moved so it closes the progress section properly and sits as a sibling before the `{error && ...}` block. Also still pending: rendering `downloadUrl` (the finished Colab mp4 link) in the results area, and persisting `colabUrl` to localStorage so the link survives a refresh.

I can't run tools to fix it in this turn, so the app is currently in a broken build state — I need one more pass.



The problem is precise and small: my Colab panel got inserted at line ~663 instead of after the progress section's closing tag at ~634. That left the `{(shots.length > 0 || busy) && (` block without its closing `)}`, which is what produces both errors (JSX parent at 639, missing `)` at 716).



The fix is to move the new `<section>` with the Colab GPU encoder block up so it sits after the progress section closes, as a sibling before `{error && ...}`, and restore the `</section>\n)}` pair at the original spot.



Want me to continue and apply that fix (plus render the Colab `downloadUrl` in the results area and persist the Colab link to localStorage)?



Pixazo api key 1

03178ba869a446eba82bce98a79fefc3



Pixazo api key 2

048e52aee2094e24bad1b46a0fb15753



Pixazo api key 3



d004a01679f843e7ba090fa1d88c926d



Pixazo api key 4

9379183b074f4655adc0fa351dd4fa29



use this https://paraloncloud.com api key for ai:-

make sure paraloncloud api key is with 0 credits so in any condition use only free model Qwen 3.8 27B. make sure use this free model. (free limit 60 request/min). 



api key 1



prlc_9dec184306d8d0dbb7d12c98d6dc22ce35d5ac3feaf2ccb9



Paraloncloud api key 2

prlc_667ae9e467f065c6202fc7e12f07f575a8111b7ad906dd73

Paraloncloud api key 3



prlc_99b14331acd49b119237bef2ecc2e1078ecdd0f3be8a83d7



Paraloncloud api key 4

prlc_a16ea589738ffd489a8c2bb8550facce032e2263922de645



Paraloncloud api key 5



prlc_320a9d3b684e18462bf409b936d40ff675f9e19c0dd6cda7



Paraloncloud api key 6

prlc_1d1ddab508e7fee65dbf06b270389ed16072fab66467b145



Paraloncloud api key 7

prlc_61b8dabf5872fc84b037b888bcca59ca1c37c0ad38810993



Must use all api keys in parallel to speed up writing process while managing consitancy of story.

This project was built with [Lovable](https://lovable.dev).

**Live app**: https://epic-colab-maker.lovable.app

## Build with Lovable

Continue developing this project in the [Lovable editor](https://lovable.dev/projects/03a7cdd0-d9be-49f7-b0d1-39d53c0fc0e4).

- **Ship faster**: describe what you want to build and Lovable handles the code.
- **Stay in sync**: every change made in Lovable is committed straight to this repository.
- **Full ownership**: this code is yours. Push to `main` on GitHub and your changes sync back into Lovable, ready for your next prompt.

## Development

Prefer working locally? You need Node.js and npm — [install with nvm](https://github.com/nvm-sh/nvm#installing-and-updating).

```sh
git clone <this-repository-url>
cd <repository-name>
npm i
npm run dev
```
