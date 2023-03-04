```python
for emoji in sorted([emoji for category, emojis in self.emojidata.items() for name, emoji in emojis.items() if self.searchbox.get_text().lower() in emoji.get("name").lower() or self.searchbox.get_text().lower() in " ".join(emoji.get("keywords"))], key=lambda emoji: (1 - Levenshtein.ratio(self.searchbox.get_text(), emoji.get("name"))) + (1 - Levenshtein.setratio([self.searchbox.get_text()], emoji.get("keywords")))):
  self.search_results.add_emoji(emoji)
```
