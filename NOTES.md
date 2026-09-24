# NOTES — selah-skr, chair 82

*کم دیاں ایہ تحریراں انگریزی وِچ لکھیاں ہوئیاں ہن — انگریزی اوں ضابطے
دے کم دی ٻولی ہے جیہڑا ساریاں کرسیاں اُتے ہِکو ہے، تے ایہ تحریراں
صرف و نحو، ڳݨتری تے پارس دے کوڈ دا حوالہ ݙیندیاں ہن۔ پڑھݨ آلے کیتے
لکھیاں فائلاں —* `README.md` *تے* `CONTRIBUTING.md` *— سرائیکی وِچ
ہن، جیویں ایں کرسی دیاں اپݨیاں فائلاں ہووݨیاں چاہیدیاں ہن۔ جو کجھ تھیا
تے جو فیصلے کیتے ڳئے، اوندا پورا ریکارڈ* `PROVENANCE.md` *وِچ ہے۔*

Lit 2026-09-19. Burn landed 2026-09-19 → 2026-09-20. Corpus completed
and committed 2026-09-21. Floor 23,213 verses · 305,507 token rows.

---

## Burn signature

| | |
|---|---|
| relay | `relay-move-on! [:skr]`, engine-side, queued behind the isiXhosa press |
| model · tier | `glm-5.3` · `glm-5.2`, every verse |
| after the relay | 23,184 / 23,213 — residue **29** |
| gleaning | the engine-side ladder — all 29 landed |
| pruned and refilled | **65** present-but-wrong files (no rows, or a row off the floor) |
| final | **23,213 / 23,213 verses · 305,507 / 305,507 token rows** |

The 65 were a fleet-wide class discovered on this chair's generation: the
batched burn *writes* a damaged file, and the relay retries only what is
**missing**, so a present-but-wrong file is never pressed again. The cure
is to delete them and let the relay's own retry refill them.

## The thermometer

Saraiki has **no closed-letter probe** — ٻ ڄ ڳ are shared with Sindhi,
ݙ (U+0759) is Saraiki's own, ݨ (U+0768) is shared with Shahmukhi
Punjabi, and **Urdu has none of them**. So their presence proves the text
is not Urdu, and their absence proves nothing at all: Gen 1:1 carries no
ٻ, ڄ, ݙ or ڳ and is plain Saraiki. The probe is therefore **whole words,
whitelist first**, against four neighbours: Urdu (the largest hazard —
same script, same letters, and the model has seen far more of it),
Majhi Punjabi, Sindhi, English.

Two collisions were caught on the gate's first run and whitelisted before
any count: **تھی** is Saraiki (*became*, from تھیوݨ), not the Urdu
feminine past copula; **دو** is a spelling slip for ݙو, not another
language. And the gate's own regex escapes came out doubled on the first
build, flagging `:` everywhere — fixed before the burn.

## The Name

Saraiki and Urdu Bibles print **خداوند**; **سائیں** and **رب** are the
reader's own devotional words for God. This chair writes **یاہوہ** — the
four letters of יהוה (ی · ہ · و · ہ) with one alif, in Urdu-Shahmukhi
codepoints (ی U+06CC, ہ U+06C1), never Arabic ي or ه. The rest of the
table: ایلوہیم · ایل · ایلوہ · ادونای · شدّای · یاہ · تصواوت.

**6,828 Name seats. No title stands in the Name's place — not خداوند,
not رب, not سائیں, not خدا, not اللہ, anywhere in the corpus.**

**38 seats carry a spelling drift** off یاہوہ: یہوہ (16) · یہووہ (4) ·
یاہووہ (3) · a few with a Hebrew letter fused into the Shahmukhi
(یاہוה, یاہوׁ) or an Arabic ه (یاهوہ), and two seats where the gloss
lost the Name altogether. Under the rails these are **form slips, not
erasures** — the stem broke, a title did not replace it. They are a
deterministic repair class (the Sorani chair's token-guided pass is the
model), not yet run here.

## No hand-rendered verse

**No verse in this repository was written or spliced by hand, and no
per-token review verdict has been taken.** Every seat is machine-pressed
under the rails. The only passes that have touched the corpus are
mechanical and are diffs you can read in the git history: the gleaning
ladder, the surface restoration, and the prune-and-refill of the 65.

## What a census will find — this chair has not had one

This chair went whole and was committed; **the census and the re-press
rounds were never run.** The sister chairs cleaned after this one was
filled, and skr kept its place in the queue. A probe run as these notes
were written, with the rails' own definitions, found:

| class | verses |
|---|---|
| a Latin letter in the flow, outside ⟨ ⟩ | 163 |
| a Hebrew letter in the flow, outside the ⟨את⟩ family | 34 |
| a Sindhi closed letter (ڪ ٽ ٿ ڀ ٺ ڇ ڌ ڍ ڊ ڦ) or ۾ | 22 |
| a bidi control character or a tatweel (U+0640) | 8 |
| Punjabi `نوں` · `مینوں` | 48 rows |
| the ergative `نے` — Urdu/Punjabi, which the rails say Saraiki does not use | 37 rows |
| Urdu `نہیں` | 21 rows |

The flow's ⟨את⟩ count and its rows' count disagree in a substantial
minority of verses. That gap is the one class the fleet's own counter
should take, because the counting convention matters and this chair's has
not been fixed — do not trust a number for it until `skr_census` exists.

`ہم` appears as a whole word about a hundred times. The rails count it as
Urdu *we* (Saraiki اساں), but it may be lawful in compounds a
whole-word probe cannot separate. **It is a whitelist question, not a
defect count, until a native ear rules.**

## Open — waiting on a native Saraiki ear

The rails themselves declare their Saraiki prose non-native and their
thermometer tables **candidate** probes. Nothing in the list below has
been confirmed by a speaker; this chair has never been read by one.

- **`نے` as a counted marker** — highest priority. The whole probe rests
  on the claim that standard Saraiki has no ergative postposition. If
  eastern Saraiki writers use نے, the probe drops, and the Gen 1:1,
  1:26 and 22:1 worked examples in the rails change with it.
- **یاہوہ vs یاہویہ** — this chair chose the Perso-Arabic family's form
  (sd ياهوه, fa/ps یاهوه) in Shahmukhi codepoints. Risk: unvowelled,
  یاہوہ may be read *Yāhoh*. The fallback is the Urdu chair's یاہویہ.
  Scott's ruling.
- **تصواوت** for צבאות is a construction — تص for צ after the Urdu
  chair's مِتصرایم, و for soft ב. No sibling Perso-Arabic chair had a
  Tsevaot row when it was made.
- **The Sindhi closed-letter list** leaves **ڃ** and **ڱ** off, because
  it is not known whether some Saraiki orthographies use them. Until
  that is settled the probe is not closed.
- **Spellings least sure of:** ݙینہہ · ڳالھ · کائنی · ہئی / ہیاں ·
  تُہاݙا · کیوں جو · جݙاں / تݙاں / کݙاں · اِتھاں / اُتھاں / کتھاں ·
  ونڄݨ · ڳیا.
- **The honorific rail** — singular verbs kept, فرمایا and فرمیندے ہن
  rejected where the Hebrew is plain ויאמר. This is the posture ruling
  applied by the rail's author, not a ruling Scott made explicitly.
- **The coined method terms** in the rails: اندر-کھچویں آوازاں
  (implosives) · بند امتحان (closed probe) · شکل دی بھُل (form slip) ·
  مُڈھ دا قاعدہ (the stem rule) · بچیا ہویا ٹولا (the remnant).
- **The UI catalog** for this chair was held at seating, on cost.

The full list, written by the rail's author against his own work, is at
the end of `docs/methodology/translation-discipline/skr.md` in the Selah
repository.
