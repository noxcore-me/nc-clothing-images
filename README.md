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
   `interface/images/*.webp` (and `interface/images/*.png` if you ship PNGs).

The default `remote` mode (Cloudflare R2 or any CDN via a URL template) is
recommended — it needs no bundled files and stays correct when clothing
packs change. Use `local` only when you want fully self-contained images.
