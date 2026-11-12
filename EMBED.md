# Embedding the Rental Property Snapshot

This calculator is built to sit inside an iframe about 360–1200px wide. It does not break out of the frame. **Download PDF** uses the browser’s print dialog and works in an iframe if the frame is allowed to open dialogs.

Published URL: https://nardthefox.github.io/harbor-rental-public/

## Suggested snippet

```html
<iframe
  id="rental-snapshot"
  title="Rental Property Snapshot"
  src="https://nardthefox.github.io/harbor-rental-public/"
  loading="lazy"
  style="width:100%;max-width:1200px;border:0;min-height:7800px;"
  sandbox="allow-scripts allow-same-origin allow-modals"
></iframe>
<script>
  window.addEventListener("message", function (event) {
    var data = event.data;
    if (!data || data.source !== "harbor-rental-snapshot" || data.type !== "resize") return;
    var frame = document.getElementById("rental-snapshot");
    if (frame && typeof data.height === "number" && data.height > 0) {
      frame.style.minHeight = "0";
      frame.style.height = data.height + "px";
    }
  });
</script>
```

The starting `min-height` avoids a short flash before the first resize message. The handler must set `frame.style.minHeight = "0"` (or set `min-height` to the reported height) **before** setting `height`. If it does not, the 7,800px starting `min-height` wins over a shorter desktop height and leaves a large blank gap below the page.

## Sandbox notes

- `allow-scripts` is required for the calculator to run.
- `allow-same-origin` lets **Clear my data** and optional saving use `localStorage` on the framed origin (the calculator’s own origin, not the parent page). Saved numbers never leave the visitor’s device.
- `allow-modals` is required for **Download PDF** (`window.print`). If you omit it, the rest of the tool still works but print may be blocked.
- Do not add `allow-top-navigation` or similar. The calculator does not navigate the parent and does not frame-bust.
- The resize message is only `{ source, type, height }`. It does not include the visitor’s inputs or results. You can check `event.origin` against the calculator’s published origin if you want to be stricter than the example.

## Recommended height

The iframe posts its content height whenever the layout changes. Measured on the default starting figures (loan rate, down payment and term blank; More detail closed):

- **Mobile (about 390px wide):** about **7,500px** tall (7,447px measured on the default starting figures, including the Example APR “Enter loan terms” line). Use a starting `min-height` of **7,800px** so the page is not clipped before the first resize message.
- **Desktop (about 1,200–1,280px wide, two-column layout):** about **4,500px** tall (4,453px measured on the same default starting figures). Use a starting `min-height` of **4,700px** only if you serve a desktop-only starting height. For a single snippet that also works on phones before the first resize message, prefer the mobile starting height (**7,800px**) as in the example above, and rely on the handler to clear `min-height`.

If the visitor opens “More detail,” adds many unit rows, or a balloon notice appears, the posted height will grow and the script above will stretch the frame. If `postMessage` is unavailable, use the mobile starting height so the page is not clipped on a phone.

The calculator is comfortable from about 360px up to 1200px wide. On a wider parent, cap the iframe (`max-width: 1200px`) and center it.
