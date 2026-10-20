# nc-clothing-images

Clothing thumbnail pack for the **nc-clothing** resource's `local` image mode.

Each file is a rendered GTA V clothing component/prop thumbnail named
`<gender>_<component>_<drawable>_<texture>.webp` (props use `p<index>` in
place of the component).

## Usage

1. Download `nc-clothing-images-male.zip` and/or `nc-clothing-images-female.zip`
   from the [latest release](../../releases/latest).
2. Extract the zip(s) into the resource's `interface/` folder so the files end
   up at `interface/images/male/` and `interface/images/female/`.
3. In `customize/config.lua`, set `Config.ClothImages = { mode = 'local' }`.
4. In `fxmanifest.lua`, enable the image globs in `files`:
   `interface/images/**/*.webp` (and `interface/images/**/*.png` if you
   ship PNGs). `**` is required — files sit one level under
   `images/<gender>/`, so a single `*` glob matches nothing.

## Remote / CDN mode (recommended)

`Config.ClothImages = { mode = 'remote', url = '<template>' }` serves
thumbnails from any CDN — the resource ships pointing at our Cloudflare R2
bucket, so most servers need nothing extra.

When hosting your own bucket (R2 or another CDN), the URL template is:

    https://<domain>/images/{gender}/{id}_{tex}.webp

The objects **must be stored under `images/male/` and `images/female/`**
prefixes — `{gender}` is a path segment, not part of the file name.

File naming inside each gender folder (remote mode):

    <gender>_<component>_<collection>_<localIndex>[_<texture>].webp

- `<collection>` is the clothing-pack collection name in lower case; the
  base game has an empty collection, producing a double underscore
  (`male_11__0.webp`).
- Texture 0 has **no** `_0` suffix (`male_11__0.webp`); textures 1+ append
  `_<n>` (`male_11__0_1.webp`). The NUI strips `_{tex}` for texture 0.
- Props use `prop_<n>` in place of the component (`male_prop_0__12.webp`).

Note: the zips in this repo are drawable-indexed for `local` mode — they
are **not** the remote naming and will 404 under the `{id}` template.

Use `local` only when you want fully self-contained images.
