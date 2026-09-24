# PROVENANCE — how this rendering came to be

*Saraiki (سرائیکی), chair 82. Lit and burned 2026-09-19; the last holes
filled 2026-09-20; the corpus completed and committed 2026-09-21. Floor
23,213 verses, 305,507 token rows.*

This is the record of how the text in this repository was produced and
what is still wrong with it. A machine-assisted rendering has no standing
unless you can see how it was made, so this file says both — including
the one thing this chair has not had.

---

## The approach

Every verse is rendered from the Hebrew of that verse — OSHB / WLC 4.20 —
under a written discipline: `docs/methodology/translation-discipline/skr.md`
in the Selah repository, itself written in Saraiki and following the
Tigrinya and isiXhosa chairs' structure, with the Name's forms taken from
the Sindhi and Urdu chairs. Eight rules govern it: the Hebrew token is the
unit; the Name stays the Name; both truths of Deut 6:4; no foreknowledge
(Gen 22:1 does not know Gen 22:13); the Tanakh register only; the four
registers held apart; numbers and marks stay put; the translator has no
word of his own.

**The script is Shahmukhi** — Perso-Arabic, right to left — by the
script-home ruling: a chair writes in the script its readers actually
read, and a Roman orthography never wins v1. Saraiki's own letters —
**ٻ ڄ ݙ ڳ ݨ** — are letters, not diacritics, and are never dropped.

**The `⟨ ⟩` brackets do two different jobs.** `⟨את⟩` is the Hebrew
direct-object marker, which Saraiki has no word for; it is left standing
so the reader sees it. `⟨لفظ⟩` is a word Hebrew did not write but Saraiki
grammar requires — visibly marked, so you can always tell what the Hebrew
said from what the grammar needed.

**Word order is Saraiki, alignment is Hebrew.** Saraiki puts the verb
last; Hebrew often puts it first. The `tokens` array holds the Hebrew
order strictly, one gloss per token; the assembled `translation` follows
Saraiki grammar. Alignment lives at the token level so the reading can
stay natural.

The rendering was produced with `glm-5.3` at tier `glm-5.2`, every verse,
through the relay (`relay-move-on! [:skr]`), engine-side, queued behind
the isiXhosa press.

## The fight on this chair is a neighbour with the same script

**Urdu is the hazard.** Same script, same letters, a large shared
vocabulary, and a model that has seen many times more Urdu than Saraiki.
One Urdu word inside a Saraiki sentence is easy to write and hard to see —
and a Saraiki reader schooled in Urdu may not hear it either. Majhi
Punjabi is the second front, Sindhi the third (it shares ٻ ڄ ڳ), English
the fourth.

**And Saraiki has no closed-letter probe.** ٻ ڄ ڳ are shared with Sindhi;
ݙ (U+0759) is Saraiki's own, against Sindhi's ڏ; ݨ (U+0768) is shared
with Shahmukhi Punjabi. Urdu has none of them — so their **presence**
proves the line is not Urdu, and their **absence proves nothing**. Genesis
1:1 carries no ٻ, ڄ, ݙ or ڳ and is plain Saraiki. A probe that read their
absence as evidence would convict most of the corpus.

So the thermometer is whole words, **whitelist first**. Two collisions
were caught on the gate's first run and whitelisted before any count:
**تھی** is Saraiki (*became*, from تھیوݨ), and **دو** is a spelling slip
for ݙو, not another language.

## The Name

| Hebrew | here | rejected |
|---|---|---|
| יהוה | **یاہوہ** | خداوند · رب · ربّ · مالک · سائیں · خدا · اللہ · یہوواہ |
| אלהים | **ایلوہیم** | خدا · اللہ · رب in the Name's place |
| אל · אלוה | **ایل** · **ایلوہ** | خدا · معبود in the Name's place |
| אדני | **ادونای** | خداوند · آقا · مالک · سائیں |
| שדי | **شدّای** | قادرِ مطلق alone |
| יה · צבאות | **یاہ** · **تصواوت** | ربّ الافواج |

**یاہوہ** is י־ה־ו־ה plus one alif: ی (U+06CC) · ا · ہ (U+06C1) · و · ہ,
never Arabic ي or ه. It is the Perso-Arabic family's form (Sindhi ياهوه,
Persian and Pashto یاهوه) written in Urdu-Shahmukhi codepoints; the Urdu
chair's یاہویہ is lawful on its own chair and is repaired to یاہوہ here.

**خداوند and سائیں are this chair's two great hazards.** خداوند is what
the Urdu and Saraiki Bibles put where יהוה stands, and the model has seen
it many times. سائیں is Saraiki's own warm word — the Sufis' word, Khwaja
Farid's word, the household's word. Neither is a bad word; the point is
that both stand **in the Name's place, instead of the Name**.

Where the Hebrew speaks of the nations' gods or of a human lord, *معبود*,
*دیوتا*, *مالک*, *سائیں*, *آقا* stand lawfully. **The Hebrew token
decides, never the Saraiki word.**

## The burn and the gate

A first-hour gate (`dev/scripts/skr_gate.clj`) read Genesis 1:1 by hand
against the rails, then ran on the batches: the Name, the ⟨את⟩ family, the
foreign-word tables, the Sindhi closed letters, bidi controls. Its regex
escapes came out doubled on the first build — it flagged `:` everywhere —
and that was fixed before the burn was read.

The relay rendered 23,184 of 23,213 and moved on with a residue of **29**;
the engine-side gleaning ladder landed all of them.

## Finding: the file the relay will never retry

Sixty-five verse files were present but wrong — no token rows at all, or a
row count that did not match the floor's Hebrew. The batched burn writes
such a file, and **the relay retries only what is missing**, so a
present-but-wrong file is never pressed again. It reads as complete and is
not.

The cure is to delete them and let the relay's own retry refill them. All
65 were pruned, refilled, and their surfaces restored. The class was found
on this generation of chairs and the fleet's prune tool came out of it.

## Finding: the surface is the Hebrew record, and this chair rewrote it

The `surface` field is the Hebrew, not the chair's to write. The fleet's
`surface_restore` found **3,593 token surfaces** on this chair that had
drifted from the floor, **2,714 of them carrying characters that are not
Hebrew at all** — most often a Shahmukhi letter standing in for its Hebrew
cognate. Perso-Arabic and Hebrew run in the same direction and their
letters are relatives, so the substitution is nearly invisible: the chair
spends its own alphabet in the wrong place. Every one was restored from
the floor, and a second run reported zero.

## The cure, in order

| pass | what |
|---|---|
| gleaning ladder | the relay's 29 residue seats |
| surface restoration | **3,593** token surfaces restored from the floor; non-Hebrew characters reported; count-mismatched files named, not guessed at |
| prune | **65** present-but-wrong verse files deleted |
| refill | the relay's own retry wrote all 65 again; surfaces restored after |

That is the whole list. **There were no re-press rounds and no census.**

## Open — declared, not repaired

- **No census has been taken on this chair.** The sister chairs of this
  generation were censused and re-pressed after skr was filled; skr kept
  its place in the queue and the lane moved on. The classes a census will
  find, measured with the rails' own definitions, are tabulated in
  [NOTES.md](NOTES.md): Latin letters in the flow, Hebrew outside the
  markers, Sindhi closed letters, bidi controls, and the counted Urdu and
  Punjabi markers — `نے` among them.
- **The Name's 38 form slips.** 6,828 Name seats; no title anywhere in the
  Name's place; 38 seats where the stem broke (یہوہ, یاہووہ, a Hebrew or
  Arabic letter fused in). Under the rails these are form slips, and they
  are a deterministic token-guided repair class — not yet run.
- **The marker gap.** The flow's ⟨את⟩ count and its rows' do not agree in
  a substantial minority of verses. The counting convention has to be
  fixed before a number for it means anything.
- **No native Saraiki reader has read this chair, or the rails it was
  rendered under.** The rails' author says so in the rails, and lists
  every decision a speaker should confirm — the `نے` probe first, then
  یاہوہ against the Urdu chair's یاہویہ, تصواوت, the Sindhi letter list,
  and a page of spellings. Until then the thermometer tables are
  **candidate** probes, and this file should be read as the honest state
  of a first pass rather than a finished account.

No verse in this repository was hand-rendered.

## Final

**23,213 / 23,213 verses · 305,507 / 305,507 token rows.** یاہوہ in
6,790 of 6,828 Name seats, with no title standing in the Name's place
anywhere in the corpus and 38 seats carrying a broken stem. A first pass,
whole, restored to the Hebrew record, and honestly un-censused.

Read it alongside the Hebrew.
