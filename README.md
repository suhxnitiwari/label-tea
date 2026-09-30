# Label Tea ☕💄

A clean makeup and skincare ingredient checker. Paste an ingredient list and it spills the tea:

- **Base detection.** Tells you whether it's water-based 💧, silicone-based ✨, oil-based 🫒, or a powder, plus primer-pairing tips so your foundation doesn't pill.
- **Free-from checklist.** Paraben-free, talc-free, fragrance-free, phthalate-free, formaldehyde-releaser-free and BHA/BHT-free, with the exact ingredient that fails a check.
- **Ingredient decoder.** Plain-English explanations for about 40 common ingredients, with a fun vibe line for each and a ☕ "tea" note that gives the nuance on controversial ones.

## Try it

Open `index.html` in any browser. There's no build step and nothing to install.

**Phone tip:** on an iPhone, use Live Text in the Camera app to copy an ingredient label, then paste it in.

## Contributing

The ingredient decoder lives in the `DB` array in `index.html`. Each entry looks like this:

```js
[/pattern/i, "green" | "yellow" | "red" | "grey", "What it is", "The vibe", "Optional tea note"]
```

PRs adding ingredients are very welcome. Please keep claims accurate and link a source in the PR.

## Disclaimer

This is not medical advice. A flag means some people choose to avoid that ingredient, and the evidence varies a lot from one ingredient to another. Contaminants like lead aren't listed on labels, so no label checker can detect them.
