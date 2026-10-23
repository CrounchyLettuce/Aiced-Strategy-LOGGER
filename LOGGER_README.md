# 49.2 Logger (test-only)

Build 49.2 plus the match logger. Menu label: **Build 49.2 LOGGER**. Made Oct 23, 2026 from the clean 49.2 source by `patch492L1.py` (the same logger patch as 49.1.1: own save space, name "Aiced Logger"). Never ships; `8_Google Play\play_guard.py` refuses it. There is no non-logger 49.2 yet (made to order).

## What changed from 49.1.1

### The Shop
- **Home** is now Play, **Shop**, Settings, Stats. A blue dot on Shop means you have enough tokens to buy something.
- **How to Play** moved into the Play menu as the fifth card. "New here? Check How to Play." on Home still opens it.
- **Settings** lost the Sound style and Visual style rows. Styles live in the Shop now.
- **Pause** has a new **Styles** button. It opens the same screen with only the styles you own, no prices and nothing to buy (title "Your styles").
- **The Shop screen**: a strip of the six pairs over the live map. Swipe it, tap a side card, or use the arrows. The centered pair is previewed on the map; its sound starts once the strip stops moving. Tapping a Visual or Sound chip selects it if you own it, or buys it (3 tokens, with a confirm box). **Buy both** buys the pair for 5. Leaving the screen puts back what you actually selected, so a preview never sticks.
- **Earning (Classic only)**: a win pays map size x AI strength, a loss pays the map size only. Quits, Custom, Spectate and lessons pay nothing. Size: Small 1, Medium 1.2, Large 1.4. Strength (wins only): Easy and Normal 1, Hard 1.25, Brutal 1.6, Deadly 2. Points needed for each token in turn: 1, 2, 2, 3, 3, 4, 4, then 5 each. The end card says what you earned.
- **Challenge stars** pay 1 token each, once. Stars you already had pay out the first time 49.2 opens, with a pop-up saying how many.
- **No grandfathering**: if your save had a style picked that you do not own, it goes back to Classic + Simple.
- **Unlock everything** (tester menu) now also owns every style; it gives no tokens. **Reset all data** also clears tokens, progress and bought styles, and puts you back on Classic + Simple.
- Every Shop word and number is in one block at the top of `ui.js`: `SHOP_TEXT` (all the text, for you and WC), `SHOP` (prices, curve, multipliers), `SHOP_PAIRS` (the pairs in order).

### Shared menu styling
Rounded corners on menu buttons, option strips and cards (8px and 12px), option buttons a little taller (48px), roomier Play menu cards. In-match HUD pieces are unchanged.

## Things to try
- A fresh feel: play a few Classic matches on different sizes and strengths and watch the end-card line. Does the pace of tokens feel right?
- Buy a single style, then a pair. Is the confirm box clear? Does the preview on the map help you decide?
- Swipe the strip in portrait and in landscape.
- Mid-match: Pause > Styles, swap something, go back and resume.

## Saving a log
End screen **Save log**; pause menu **Save match log**. Put files in `4_Logger Data`. The logger does not record tokens yet. To use Deadly or other locked options, use Unlock everything (four quick taps on the Settings title, then press it twice).

## Checked
- A new Shop test (`t_shop.py`, 29 checks) on the clean page and on this logger: Home buttons, How to Play in the Play menu, no style rows in Settings, preview not saved, buying with a confirm, selection saved, Pause > Styles shows only owned pairs with no prices, and earning (a Large Hard win paid 1.75 points: the first token plus 0.75). All pass.
- The logger replay still matches every second and the save-key isolation test passes.
- Old suite, quick tier, on the clean 49.2 page: everything about the match, sound and HUD passes. The failures are all tests that drive the old Settings style rows or check the old Settings layout (t35, t42, t51, t52, t77, t80, t83), plus t54, which wants a 49.2 What's New entry. t46 and t48 (How to Play moved) were updated and pass.
- Not checked: a phone, a full match played by hand, sound by ear.
