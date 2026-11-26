# Ocular — WebGL build

Built output only. The source lives elsewhere and is not public.

A glaucoma optic nerve head viewer. Give it a fundus photograph and it
segments the disc and cup, fits the nerve head surface, measures it, and shows
a 3D eye that can be rotated.

**Live:** https://kartikey33311.github.io/ocular-web/

## Giving it an image

Three ways, all equivalent once the bytes arrive:

1. **Drag a photograph onto the page.** No button needed.
2. **Click "Load Eye Image…"** and pick a file.
3. **Link to it with `?image=`**, which is how another site hands one over:

```
https://kartikey33311.github.io/ocular-web/?image=<url-encoded image URL>
```

Optional: `&eye=OD|OS`, `&field=30|45|50|60`, `&service=<url>`.

Pass `field` if the fundus camera's setting is known — it sets the whole
millimetre scale, and a 45-degree image read as 30 reports a normal disc as
"Small".

Note on `?image=`: most image hosts send no `Access-Control-Allow-Origin`, so
this page usually cannot read a remote photograph by itself. When a generation
service is configured the page fetches through it instead, which is not a
browser and is not bound by that rule. With no service configured, only a
CORS-enabled host works (GitHub raw and GitHub Pages both send `*`).

## service.json

Points the viewer at the 3D generation service, which holds the Tripo API key
server-side. Edit this file to re-point it; **no rebuild is needed**.

```json
{ "serviceUrl": "https://your-site.com/api", "referenceModelUrl": "none" }
```

Empty means no 3D generation: the measurements, the fitted nerve head and the
on-screen numbers all still work, and the status line says so.

The service cannot live here. GitHub Pages is static, so it could not hold a
key even if that were wise — and Tripo sends no CORS headers on any response,
so the browser cannot call it directly in any case. The service runs on Vercel.

## Note

Measurements are a fit from the photograph, not instrument readings, and the
generated eye is anatomical scenery rather than a reconstruction of this
patient's eye. The automatic cup trace reports UNCONFIRMED on real photographs
by design; hand-tracing is the measurement path.
