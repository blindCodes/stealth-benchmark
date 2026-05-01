# stealth-benchmark

Open-source tool that simulates what coding interview platforms detect.  
Test your setup before the real thing.

Built by [blind.codes](https://blind.codes) — the invisible AI assistant for coding interviews.

## Live demo

👉 [blindcodes.github.io/stealth-benchmark](https://blindcodes.github.io/stealth-benchmark)

## What it detects

| Check | Risk | Method |
|---|---|---|
| Window focus lost | 🔴 High | `blur` / `focus` events |
| Tab switch | 🔴 High | Page Visibility API |
| Global shortcut (Cmd+Shift+[key]) | 🔴 High | `keydown` event |
| DevTools open | 🟡 Medium | Window size delta + console getter heuristic |
| Multiple screens | 🟡 Medium | `window.screen.isExtended` |
| Clipboard access granted | 🟡 Medium | Permissions API |
| Screen share availability | 🔵 Low | `navigator.mediaDevices.getDisplayMedia` |
| User agent / OS | 🔵 Low | `navigator.userAgent` |
| Timezone & locale | 🔵 Low | `Intl.DateTimeFormat` |

## What it can't detect (browser limitation)

- Running processes — requires a native app
- Specific overlay windows — not accessible from the web
- Kernel-level hooks

## Usage

Just open `index.html` in a browser. No build step, no dependencies.

```bash
git clone https://github.com/blindCodes/stealth-benchmark
cd stealth-benchmark
open index.html
```

## Contributing

PRs welcome. If you know of a detection technique used by interview platforms that isn't covered, open an issue or submit a PR.

Each check follows this interface:

```js
{
  id: 'my-check',         // unique identifier
  name: 'My Check',       // display name
  desc: 'What it does',   // shown under the name
  risk: 'high',           // 'high' | 'medium' | 'low'
  run: async () => ({
    pass: true,           // true = safe, false = flagged, null = info only
    detail: 'message'     // shown in the event log
  })
}
```

## License

MIT
