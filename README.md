# Label Maker

A single-page web tool that turns one line of text into a printable label. It supports **3″ × 4″**, **4″ × 6″** and **2 5/16″ × 4″** labels, each tall or wide. Use `//` to split the text into lines. Each line is centered, and the text is scaled to fill the label.

**Example input**

```
text 1//text 2//text 3//text 4
```

**Prints as**

```
text 1
text 2
text 3
text 4
```

## Using it

1. Open the site in Chrome or Edge.
2. Type your text in the box. The preview updates as you type.
3. Pick the label size and orientation.
4. Press **Enter** or click **Print label**.
5. The first time you print with a given label size, set the print dialog to:
   - **Printer:** your label printer
   - **Paper size:** the label size you picked on the page
   - **Margins:** None
   - **Scale:** 100% / Actual size (not "Fit to page")

   Most browsers remember these settings for later prints. If you switch label sizes, check the paper size in the dialog again. Some printer drivers need each label size added as a custom paper size first.

### Options

| Option | What it does |
| --- | --- |
| Label size | 3″ × 4″ (default), 4″ × 6″, or 2 5/16″ × 4″. |
| Orientation | **Tall** puts the short side across the top (e.g. 3″ wide × 4″ tall). **Wide** turns it sideways (4″ wide × 3″ tall). |
| Bold | Prints the text in bold. On by default. |
| Size each line separately | Lets each line scale on its own, so short lines print larger. When it's off, every line uses the same size. |

The page keeps your last text, label size and orientation in your browser (localStorage). Nothing is sent anywhere.

## Printing without the dialog (optional)

To send labels straight to your **default** printer with no dialog, start Chrome with the `--kiosk-printing` flag, then open the site:

- **Windows:** make a shortcut with the target
  `"C:\Program Files\Google\Chrome\Application\chrome.exe" --kiosk-printing https://YOUR-USERNAME.github.io/label-maker/`
- **macOS:** run in Terminal
  `open -a "Google Chrome" --args --kiosk-printing https://YOUR-USERNAME.github.io/label-maker/`

Chrome has to be fully closed before you launch it this way, or the flag is ignored. Make sure your label printer is the system default printer.

## Deploying to GitHub Pages

1. Create a new repository on GitHub, for example `label-maker`.
2. Upload `index.html` and `README.md` to the root of the repository: **Add file → Upload files**, then commit.
3. Go to **Settings → Pages**.
4. Under **Build and deployment**, set **Source** to *Deploy from a branch*. Choose the `main` branch and the `/ (root)` folder, then click **Save**.
5. After a minute or two the site is live at
   `https://YOUR-USERNAME.github.io/label-maker/`

## Customizing

All the settings are near the top of the `<script>` block in `index.html`:

| Setting | Default | Meaning |
| --- | --- | --- |
| `MARGIN_IN` | `0.15` | Blank margin on every side, in inches |
| `LINE_GAP` | `0.18` | Space between lines, as a fraction of the font size |
| `FONT` | `Helvetica, Arial, sans-serif` | Font family |

### Adding or changing label sizes

The sizes are listed in the `SIZES` object in `index.html`, in inches, as `[short side, long side]`:

```js
const SIZES = { "3x4": [3, 4], "4x6": [4, 6], "2.3125x4": [2.3125, 4] };
```

To add a size, add an entry here, for example `"2x3": [2, 3]`. Then add a matching button inside `<span class="seg" id="sizes">`:

```html
<button data-s="2x3">2″ × 3″</button>
```

The `data-s` value must match the key in `SIZES`. The default size is the button with `class="on"`, together with `let labelSize = "3x4";` in the script.

## Files

- `index.html` – the whole app. It has no dependencies and no build step.
- `README.md` – this file.
