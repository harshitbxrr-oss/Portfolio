# Shatranj City

A portfolio you can drive. Take the **VAJRA-S1** through Shatranj City, an Indian-inspired open world built in raw WebGL 2, and pull up at each landmark to open part of the portfolio of **Harshit Kumar Sinha, UI/UX Designer**.

![Shatranj City](assets/og-image.jpg)

**Gameplay video:** [media/shatranj-city-gameplay.mp4](media/shatranj-city-gameplay.mp4) (56 s)

**Live site:** `https://<your-username>.github.io/<repository-name>/` once you've deployed it (see below).

---

## What's inside

- **The city.** The Old City with havelis and the Darwaza gate, Chandni Bazaar, the temple complex, the railway junction with moving trains, the Cyber-Chowk neon district, the business district and three bridges including the cable-stayed Vajra Setu.
- **Five landmarks, five sections.** About me, Skills, Case studies, Resume and Contact. There's also a plain-page **Quick view** for visitors in a hurry.
- **Real driving physics.** Tyre grip, weight transfer, a 6-speed gearbox, ABS, stability control, a drift-capable handbrake and an instant brake. Hitting walls at an angle spins the car.
- **A physical world.** Traffic you can shunt, cones and crates that tumble, lamp posts that snap, solid trees, and level crossings that stop traffic for trains.
- **Working lights.** Headlights that light the road, brake, reversing and tail lamps, indicators that switch themselves off, hazards, and a horn.
- **Time of day.** Golden hour switches to neon night automatically in Cyber-Chowk. Midday and night are available in Settings.
- **Every device.** Keyboard and mouse, touch (joystick or arrows) and game controllers, on desktop, tablet and phone.
- **Settings.** Five camera views, full screen, and choices for graphics quality, steering sensitivity, brake pedal feel, sound, minimap and reduced motion.
- **Fallback.** Browsers without WebGL 2 get the Quick view instead.

## Controls

| Action | Keyboard | Touch | Controller |
|---|---|---|---|
| Drive / brake, then reverse | W / S or ↑ / ↓ | Drive / Brake | RT / LT |
| Steer | A / D or ← / → | Joystick or arrows | Left stick |
| Handbrake (stop; steer to drift) | Space | Hand brake | X / Square |
| Instant brake | B (hold) | Stop (red) | B / Circle (hold) |
| Boost | Shift | Boost | RB |
| Enter a landmark | E or Enter | Enter | A / Cross |
| Headlights | L | Headlight button | D-pad up |
| Indicators | Z / X | Arrow buttons | L3 / R3 |
| Horn | H (hold) | Horn button | LB |
| Camera | C, mouse drag, wheel | Camera button, drag, pinch | Y / Triangle |
| City map | M | Map button | View / Select |
| Settings | Settings button | Settings button | Start / Options |
| Full screen | F | Full-screen button | |
| All controls | ? | Settings → Controls | |

## Deploy on GitHub Pages

The site is one self-contained file, `index.html`. Scripts and images are inlined, and only Google Fonts load from the web. Either method below works.

### Option A: GitHub Actions (recommended)

The site rebuilds itself from `src/` on every push.

1. Create a new repository on GitHub, for example `shatranj-city`.
2. Upload everything in this folder, including the hidden `.github` folder and `.nojekyll` file:
   ```bash
   git init
   git add .
   git commit -m "Shatranj City portfolio"
   git branch -M main
   git remote add origin https://github.com/<your-username>/<repository-name>.git
   git push -u origin main
   ```
3. On GitHub, open **Settings → Pages**. Under **Build and deployment → Source**, choose **GitHub Actions**.
4. Open the **Actions** tab. The "Deploy to GitHub Pages" run takes about a minute. Your site is then live at `https://<your-username>.github.io/<repository-name>/`.

### Option B: Deploy from a branch

No workflow needed.

1. Push the files as in steps 1–2 above. If you like, delete `.github/workflows/deploy.yml` first.
2. In **Settings → Pages**, set **Source: Deploy from a branch**, **Branch: `main`**, **Folder: `/ (root)`**, and save.
3. After editing anything in `src/`, run `python build.py` and commit the new `index.html`.

> **Uploading through the GitHub website instead of git?** Drag the folder contents into "Add file → Upload files". Every file here is under GitHub's 25 MB browser limit. Hidden files (`.github`, `.nojekyll`, `.gitignore`) can be skipped by some browsers. If the workflow doesn't appear, use Option B.

## Make it yours

All portfolio text lives in one place: **`src/content.js`**, in the `PORTFOLIO` object. Every panel, hologram, departure board and the Quick view read from it. Replace everything in `[square brackets]`:

- `about.facts`: your city
- `skills`: your skill levels, 1–5 (the current numbers are placeholders)
- `caseStudies`: durations and outcomes for WallVista, plus case studies 2 and 3
- `resume.experience`, `resume.education` and `resume.pdfUrl`: link your PDF, for example `assets/resume.pdf` after adding the file (see the note below)
- `contact.email` and `contact.links`: LinkedIn, Behance, Dribbble and GitHub

Then either push (Option A rebuilds automatically) or run:

```bash
python build.py          # needs Python 3.8+, no packages
```

> A resume PDF added under `assets/` is only published by Option B, or by Option A if you also copy it in the workflow's "Collect the files to publish" step. For example, add `cp assets/resume.pdf _site/assets/`. Linking to a PDF hosted elsewhere (Google Drive, Dropbox) works with either option.

**Share previews.** Social sites need an absolute image URL. After deploying, change `og:image` in `src/template.html` to `https://<your-username>.github.io/<repository-name>/assets/og-image.jpg` and rebuild.

## Preview locally

Double-click `index.html`, or serve the folder:

```bash
python -m http.server 8000
# then open http://localhost:8000
```

## Project structure

```
.
├── index.html                  ← the built site (what GitHub Pages serves)
├── build.py                    ← rebuilds index.html from src/ and assets/images/
├── .nojekyll                   ← tells GitHub Pages to serve files as they are
├── .github/workflows/deploy.yml← optional automatic build + deploy (Option A)
├── src/
│   ├── template.html           ← page shell: loader, HUD, panels, settings, styles
│   ├── content.js              ← PORTFOLIO — all your text and links
│   ├── engine.js               ← WebGL 2 renderer: maths, shaders, geometry, bloom
│   ├── world.js                ← the city: districts, roads, bridges, railway, signs
│   ├── game.js                 ← car model, camera rigs, traffic, effects, render loop
│   ├── vehicles.js             ← traffic vehicles, VAJRA-S1 lamps, trains
│   ├── physics.js              ← vehicle dynamics, collisions, props, lamp posts
│   ├── ui.js                   ← HUD, minimap, map, panels, quick view, sound
│   ├── device.js               ← desktop / tablet / phone layouts, touch, controllers
│   └── lights.js               ← headlights, indicators, horn, steering sensitivity
├── assets/
│   ├── images/                 ← web-optimised art embedded into index.html
│   ├── source-art/             ← original full-size concept art
│   └── og-image.jpg            ← social share preview
└── media/
    └── shatranj-city-gameplay.mp4
```

The JavaScript modules are joined in the order listed in `build.py`, because later modules extend earlier ones. Keep that order if you add files.

## Browser support

The game needs WebGL 2, which current Chrome, Edge, Firefox and Safari 15+ all support, on desktop and mobile. Graphics quality adapts on its own; older phones can choose Settings → Graphics → Low. Browsers without WebGL 2 automatically get the Quick view.

## Notes

- Settings such as camera, graphics and time of day are saved in the browser's local storage. Steering sensitivity deliberately starts at 100% every visit.
- The concept art in `assets/` was supplied for this project and is used for the loading screen and section panels.
- No license file is included. Add one if you want others to reuse the code.
