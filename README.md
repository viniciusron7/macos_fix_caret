# Caret Fix: real `^` and `~` on the macOS U.S. International – PC layout

On Apple's **U.S. International – PC** layout, `^` (Shift+6) and `~` (Shift+\`) are dead keys.

- Followed by a letter that takes the accent, they combine as expected: `^a` becomes `â`, `~a` becomes `ã`, `~n` becomes
  `ñ`.
- Followed by any other key (consonant, digit, symbol, Return), macOS types a character that **looks similar but is
  different**: `ˆ` (U+02C6, modifier letter circumflex accent) and `˜` (U+02DC, small tilde), instead of `^` (U+005E)
  and `~` (U+007E).
- Examples: `x^2` becomes `xˆ2` and `~/` becomes `˜/`. This breaks code, LaTeX, regular expressions and shell paths.

**Why:** those are the dead keys' "terminator" characters in Apple's layout, which macOS types when the next key doesn't
combine. Space has its own mapping, which is why `^` followed by Space works.

**What this layout changes:** it's a copy of Apple's layout, identical except for those 2 terminators, which are now
`^` and `~`.

- Accents, `ç`, Option combinations and shortcuts are unchanged.
- Verified by comparing the compiled layout with Apple's original across every key, modifier and dead-key state. The
  only differences are `ˆ`→`^` and `˜`→`~`.

## Install

1. Copy the `CaretFix.bundle` folder to `~/Library/Keyboard Layouts/`.
   - In Finder: press Cmd+Shift+G and type `~/Library/Keyboard Layouts`.
   - If you downloaded it as a ZIP, run this in Terminal:
     `xattr -dr com.apple.quarantine ~/Library/Keyboard\ Layouts/CaretFix.bundle`
2. Log out and log back in.
3. Open System Settings › Keyboard › Text Input › Input Sources › Edit… › **+** › English, and add **US International
   PC Caret Fix**.
4. Select it from the input menu in the menu bar, or with Ctrl+Space.

## Uninstall

1. On the same Input Sources screen, select "US International PC Caret Fix" and click **–**. Keep another layout
   enabled, such as "U.S. International – PC".
2. Delete `~/Library/Keyboard Layouts/CaretFix.bundle`.
3. Log out and log back in.

## Notes

- `^` before a, e, i, o, u and `~` before a, o, n still combine. For a literal `^a`, type `^`, Space, `a`.
- `^` followed by Space types only `^`, because the space is consumed. For `^ `, press Space twice.
- Option+i and Option+n also produce `^` and `~` now when nothing combines. Shift+Option+i and Shift+Option+n still type
  `ˆ` and `˜`.
- **Password:** if your account password has `^` or `~` followed by a key that doesn't combine with it, this layout
  types it differently. The login window uses the system layout. If needed, switch to Apple's layout to type it.
- Many other Apple layouts with dead keys use the same `ˆ` and `˜` terminators. This repo only fixes
  U.S. International – PC / Brazilian.
- Built and tested on macOS 27.2.
