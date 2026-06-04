# Preview Workflow — VaultaPay Pitch Deck

## How to get a live preview server running

1. Start a Python HTTP server in the background (Bash tool):
   ```
   python -m http.server 4321 --directory "C:\Projects\Vaulta-Pay-Model"
   ```
   Use `run_in_background: true`. Server is ready when you can eval `document.title`.

2. The preview browser (serverId) is **NOT** the vaultapay launch.json server —
   it reuses whatever server was already running at port 5174 for a different app.
   The pitch deck server is on **port 4321**.

3. Navigate the preview browser to the pitch deck:
   ```js
   window.location.assign('http://localhost:4321/pitch-embed.html')
   ```
   Then verify: `document.title + ' @ ' + window.location.href`
   Expected: `"VaultaPay — Seed Pitch Deck @ http://localhost:4321/pitch-embed.html"`

4. The `preview_screenshot` tool **times out** consistently on this machine.
   Use `preview_eval` for all verification instead.

## Navigating slides

```js
goTo(0)   // slide 1 (0-indexed)
goTo(13)  // slide 14
```

Both `goTo` and `go` are defined as globals in pitch-embed.html.

## Measuring slide content vs nav bar

Nav bar is at `bottom: 22px`, ~40px tall → needs **62px clearance** from bottom.
`navTop = window.innerHeight - 62`

```js
(function() {
  const navTop = window.innerHeight - 62;
  goTo(slideIndex);  // 0-indexed
  const s = document.getElementById('s' + slideNumber);  // 1-indexed id
  // Measure specific card elements
  const els = s.querySelectorAll('.your-card-class');
  const maxB = Math.max(...[...els].map(e => e.getBoundingClientRect().bottom));
  return { maxBottom: Math.round(maxB), overflow: Math.round(maxB - navTop) };
})()
```

`overflow > 0` = content hidden behind nav bar (bad)
`overflow < 0` = clearance (absolute value = px of empty space below content)

## Checking computed styles

```js
const body = document.querySelector('#s5 .slide-body');
const cs = getComputedStyle(body);
return { justifyContent: cs.justifyContent, flexDirection: cs.flexDirection };
```

## Key layout measurements (viewport height = 720px on preview browser)

| Element | Value |
|---|---|
| `window.innerHeight` | 720px |
| `navTop` | 658px |
| `.slide-inner` padding | `24px 48px 68px` (top/sides/bottom) |
| `#s14 .slide-inner` padding | `20px 48px 68px` |
| Typical title+label area | ~120–130px |
| Available `.slide-body` height | ~519px |

## Slide content bottom measurements (after Session 21 fixes)

| Slide | Content bottom (y) | Overflow vs navTop=658 | Status |
|---|---|---|---|
| 2 | 381 | -277 (277px space) | OK, space to use |
| 4 | 435 | -223 (223px space) | OK, space to use |
| 5 | ~436 | -222 | Centered vertically |
| 6 | 574 | -84 | Good |
| 9 | 501 | -157 | Centered vertically |
| 10 | varies | ~-307 on table rows | OK |
| 13 | 438 | -220 | OK |
| 14 | 652 | -6 | Very tight, just fits |

## What does NOT work

- `preview_screenshot` → always times out (30s). Do NOT use it. Use eval-based measurement instead.
- `preview_start("vaultapay")` → reuses the wrong server (port 5174, different app)
- Direct `file://` URLs → cross-origin issues with some browsers
- `npx serve` → failed to start on this machine

## Workflow before committing

1. Edit the file
2. Reload: `window.location.reload()` in eval — wait 1-2 seconds
3. Navigate to the slide: `goTo(slideIndex)`
4. Measure content bottom vs navTop using the snippet above
5. Check computed styles if needed
6. Only commit when overflow values look correct

## File locations

- Pitch deck: `C:\Projects\Vaulta-Pay-Model\pitch-embed.html`
- Main model: `C:\Projects\Vaulta-Pay-Model\index.html`
- GitHub Pages: `https://moazzamkhoja.github.io/Vaulta-Pay-Model/`
- Pitch direct: `https://moazzamkhoja.github.io/Vaulta-Pay-Model/pitch-embed.html`
