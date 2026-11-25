# Ocular — WebGL build

Built output only. The source lives elsewhere and is not public.

A glaucoma optic nerve head viewer. Give it a fundus photograph and it
segments the disc and cup, fits the nerve head surface, measures it, and shows
a 3D eye that can be rotated.

## Use

```
https://kartikey33311.github.io/ocular-web/?image=<url-encoded image URL>
```

Optional: `&eye=OD|OS`, `&field=30|45|50|60`.

Pass `field` if the fundus camera's setting is known — it sets the whole
millimetre scale, and a 45-degree image read as 30 reports a normal disc as
"Small".

## service.json

Points the viewer at the 3D generation service, which holds the Tripo API key
server-side. Edit this file to re-point it; no rebuild is needed.

```json
{ "serviceUrl": "https://ocular-tripo.<subdomain>.workers.dev" }
```

Empty means no 3D generation: the measurements, the fitted nerve head and the
on-screen numbers all still work, and the status line says the globe is
unavailable.

## Note

Measurements are a fit from the photograph, not instrument readings, and the
generated eye is anatomical scenery rather than a reconstruction of this
patient's eye. The automatic cup trace reports UNCONFIRMED on real photographs
by design; hand-tracing is the measurement path.
