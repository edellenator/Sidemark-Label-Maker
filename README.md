# 3×4 Label Maker

A single-page web tool that turns one line of text into a printable 3″ × 4″ label. Use `//` to split the text into lines. Each line is centered, and the text is scaled to fill the label.

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
3. Press **Enter** or click **Print label**.
4. The first time you print, set the print dialog to:
   - **Printer:** your label printer
   - **Paper size:** 3×4 (or 4×3 if you use landscape)
   - **Margins:** None
   - **Scale:** 100% / Actual size (not "Fit to page")

   Most browsers remember these settings for later prints.

### Options

| Option | What it does |
| --- | --- |
| Orientation | Switches between 3″ wide × 4″ tall (default) and 4″ wide × 3″ tall. |
| Bold | Prints the text in bold. On by default. |
| Size each line separately | Lets each line scale on its own, so short lines print larger. When it's off, every line uses the same size. |

The page keeps your last text and orientation in your browser (localStorage). Nothing is sent anywhere.

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

To change the label dimensions, edit the `size()` function, which returns `{ w: 3, h: 4 }` for portrait and `{ w: 4, h: 3 }` for landscape. You can also change the button labels in the HTML.

## Files

- `index.html` – the whole app. It has no dependencies and no build step.
- `README.md` – this file.
