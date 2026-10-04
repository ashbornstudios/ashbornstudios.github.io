# Gnosis Lab — directives after the peacock episode (2026-09-30)

Paste the **ACTIVE DIRECTIVES** block into `Projects/Gnosis Lab/_pipeline/LEARNINGS.md`
and the **NEXT 12** block into `_pipeline/TOPIC_BANK.md`. The factory's Analyst step
reads both at the start of every run.

Signal this is built on (Wilder, 2026-09-30): the peacock episode is the channel's best
performer on Instagram. What worked: vivid colour, cinematic macro, nature, contrast
(dull → vivid), smooth motion. Keep the current quality bar.

---

## ACTIVE DIRECTIVES — v5 (2026-09-30, after EP peacock)

- **D0 THE PEACOCK EPISODE IS THE STANDARD (Wilder 2026-10-04).** Before writing a script,
  open the peacock episode's folder (`SCRIPT_60s.md`, `JOB_MAP.md`, `EDIT_NOTES.md`) and copy its
  shape: the same shot mix, beat order, pacing, prompt wording and motion style, with only the
  subject and accent colour changed. What that means in practice:
  - **Almost all macro/micro on warm near-black.** The peacock had 14 of 15 shots as extreme
    macro or microscope views; the whole animal appears **once**, as the final reveal.
  - **Arc:** the colour up close (≈6 shots) → the mechanism under the microscope (≈5) → the
    proof that the colour isn't what it seems (the colour vanishes: the brown backlit feather)
    → the full animal, one slow pull-back, then the name.
  - **Only the light moves.** Light slides, colour swells with the angle, glints travel along
    the structure, air stirs the fine fibres; one slow camera move per shot. No animal action
    except the final reveal (the peacock's train quiver), unless Wilder asks for a specific shot.
  - **Prompt wording:** "Hyper-realistic extreme macro photograph of … warm near-black
    background, photoreal specimen macro. The <accent> is the only saturated colour; everything
    else bronze, brown, black. No illustration, no CGI plastic sheen, no text."
  - Where D1–D8 disagree with the peacock episode, the peacock wins.

- **D1 Subject = colour in nature.** Every episode is about a colour, a pattern or a
  light effect in a living thing or a natural material. Animals first (tiger, mantis
  shrimp, chameleon, morpho, hummingbird, poison frog, cuttlefish, jewel beetle),
  then minerals and phenomena (opal, bismuth, aurora, bioluminescence).
- **D2 The contrast beat is mandatory.** One shot shows the subject with its colour
  *gone* (backlit, wet, dead, under the wrong light, through another animal's eyes).
  Place it where the peacock placed its brown backlit feather (per D0), not at a fixed
  time.
- **D3 Three colour acts.** Act 1 dull/near-black with one accent. Act 2 the subject
  at full saturation, macro. Act 3 the mechanism (micro/electron scale) in the same
  palette. No random hue shifts between shots.
- **D4 Macro ratio ≥ 60 %.** At least 9 of 15 shots are macro or micro. Wide
  establishing shots ≤ 3, and only as the payoff.
- **D5 Motion stays slow and physical.** One camera move per shot, ≤ 5 s, light or
  air is what moves, never the subject's shape. Keep the Kling suffix "Natural and
  physically coherent, no warping, no morphing, no shape change."
- **D6 Saturation is earned, not graded.** The vivid colour must be in the still
  (prompt it as "the only saturated colour in the frame"); do not push saturation in
  the edit. Backgrounds stay warm near-black.
- **D7 Title shape.** "Why is a tiger orange?" / "The colour that isn't there" —
  a question or a paradox, never the animal + "explained".
- **D8 Instagram = winners only (revised 2026-10-04).** Every episode goes to YouTube;
  Instagram gets an episode only after ≥ 48 h on YouTube at or above the channel median
  in both views and retention. (The original D8 said queue every colour-in-nature episode
  to both; the horse episode flopped on IG, so that is withdrawn.)

## Removed from Instagram
- Horse episode — removed by Wilder 2026-10-04, low engagement. Stays on YouTube.
  Never re-promote.

## Hypotheses to test next (one per episode)
1. Animal with warm palette (tiger) vs the cool peacock palette → does warm hold?
(Hold every other variable at the peacock standard while testing one.)

---

## TOPIC_BANK → 🎯 NEXT 12 (colour-in-nature series)

| # | Topic | Hook / paradox | Contrast beat | Mechanism shot |
|---|-------|----------------|---------------|----------------|
| 1 | Tiger | Why is a tiger orange if deer can't see orange? | Tiger through a deer's eyes: green-grey, invisible | Pheomelanin in a single hair, cross-section |
| 2 | Mantis shrimp | The animal that sees colours we can't name | Grey rock-pool → the strike, the flash | 16 photoreceptor types, compound eye macro |
| 3 | Morpho butterfly | This blue is not a pigment | Wing wet or backlit → brown | Christmas-tree nanostructure, SEM |
| 4 | Chameleon | It doesn't change colour to hide | Calm brown → excited neon | Guanine crystal lattice stretching |
| 5 | Hummingbird gorget | A black throat that ignites at one angle | Dark → the flash as the head turns | Melanin platelets with air pockets |
| 6 | Poison dart frog | The brightest animal is a warning | Rainforest floor dim → one electric blue | Skin gland macro, pigment cells |
| 7 | Cuttlefish | Skin that thinks | Sand-matching grey → passing cloud waves | Chromatophore opening in real time |
| 8 | Jewel beetle | The metal that isn't metal | Dead-looking husk → green-gold fire | Multilayer chitin reflector |
| 9 | Opal | A stone made of rain | Milky white → play of colour under a torch | Silica spheres in a grid |
| 10 | Bismuth | The rainbow you can grow in a kitchen | Dull grey ingot → stair-step hopper crystal | Oxide-layer thickness = colour |
| 11 | Bioluminescent bay | Water that lights up when you touch it | Black water → blue wake | Dinoflagellate single cell |
| 12 | Aurora | Colour from the sun hitting air | Grey night → green curtain | Oxygen atom emission, 557 nm |

---

## Pipeline: what to check on the Mac (the factory has not run since 2026-09-25)

1. Open the Gnosis Lab scheduled task in the Claude desktop app → run history.
   The last message of the last run says where it stopped.
2. Confirm the task's folder path. Two roots exist now:
   `/Users/mac/Claude/Projects/…` and `/Users/mac/Documents/Claude/Projects/Gnosis Lab`.
   If the task points at the old root it fails on its first file read.
3. Confirm the Higgsfield connector is attached to the task (the Ashborn factory
   checks this in Step 0; copy that check if the Gnosis prompt lacks it).
4. Run once manually while watching; approve any permission prompt it hits, then
   pre-approve that tool so the 3 AM runs don't stall on it.
5. Cloud side is healthy: publisher `/api/publish/run` returns 200 every 5 min;
   Higgsfield balance 2,972 credits (an episode costs ~150–200).
