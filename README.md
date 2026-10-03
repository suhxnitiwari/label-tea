# Label Tea

*Your one and only source for what's really in your makeup. XOXO.*

**Live:** https://suhxnitiwari.github.io/label-tea/

## What it is

A clean makeup and skincare ingredient checker, dressed as a society-page beauty magazine. Scan a label with your phone camera or paste an ingredient list, and it spills the tea: what the product's base is, which common "free-from" claims it passes, and an In / Out / It depends verdict on every ingredient.

The look borrows from Gossip Girl's Upper East Side, Blair Waldorf's headbands, the In/Out verdicts of a legendary fashion editor, Olive Smith's lab notebook (*The Love Hypothesis*), Bree's bionic speed (*Lab Rats*) and Hermione Granger's potions class. So the scanner is "bionic vision," every ingredient gets a spell name, and the decoder is "the spellbook."

## How it's built

**On-device OCR.** Camera scanning runs [Tesseract.js](https://github.com/naptha/tesseract.js) entirely in the browser, and the photo is never uploaded. The OCR library is lazy-loaded only when you tap scan, so the page itself stays light. Before recognition, the photo is downscaled to at most 1800px and run through a grayscale and contrast filter on a canvas, which makes OCR faster and more accurate. A cleanup pass then turns messy OCR text into a clean list: it finds where "Ingredients:" starts, re-joins words hyphenated across lines, splits out "+/- May contain" shade pigments, and fixes commas that OCR misread as periods.

**Base detection from ingredient order.** Labels list ingredients by concentration, so the checker reads the top of the list to classify the formula as water-based, silicone-based (including water-in-silicone), oil-based, or powder/anhydrous, separates out sunscreen actives, and gives primer-pairing advice so foundation doesn't pill.

**Free-from checklist.** Seven regex checks (paraben, formaldehyde releaser, phthalate, fragrance, talc, BHA/BHT and oxybenzone) name the exact ingredient that fails each one. Matching also retries with spaces removed, so a name split across label lines like "Phenoxy ethanol" still matches.

**A 49-entry ingredient decoder** with a plain-English lab note, a vibe line, and a ☕ "tea" note that explains the nuance on controversial ingredients.

**Sourced editorial features.** *Scandals* covers beauty lawsuits (J&J talc, hair relaxers, benzene in sunscreen, PFAS in mascara) with linked sources and a reminder that a lawsuit is an accusation, not a verdict. *The Great Sunscreen Debate* weighs anti-sunscreen claims against the research, mineral vs. chemical filters, Australia's SPF scandal and the FDA's new filter.

All of it is one `index.html` with vanilla JavaScript and CSS: no framework, no build step, no backend.

## Design choices

- A one-column magazine layout with a masthead, Bodoni Moda headlines, and In / Out / It depends "stamps" on every ingredient card.
- Playful voice, careful claims: a flag means some people choose to avoid an ingredient, not that it's dangerous, and the evidence varies a lot from one to the next.
- Honest about limits: contaminants like lead or benzene aren't on labels, so no label checker can catch them, and the site says so.

## Tech stack

HTML, CSS, vanilla JavaScript, Tesseract.js (in-browser OCR), Canvas API, GitHub Pages.

## Run it locally

Open `index.html` in any browser. There's nothing to install.

**Scanning tips:** lay the label flat, use good light, and fill the frame with just the ingredient list. Curved bottles scan best a small section at a time. Always double-check the scanned text, because OCR makes typos.

## Contributing

The ingredient decoder lives in the `DB` array in `index.html`. Each entry looks like this:

```js
[/pattern/i, "in" | "depends" | "out" | "neutral", "What it is (lab note)", "The vibe", "Optional tea note"]
```

PRs adding ingredients are welcome. Please keep claims accurate and link a source in the PR.

## Disclaimer

This is not medical advice. A flag means some people choose to avoid that ingredient, and the evidence varies a lot from one ingredient to another.

Built by [Suhani Tiwari](https://suhanitiwari.com).
