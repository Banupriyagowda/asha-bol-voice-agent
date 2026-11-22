# 🎙️ ASHA Voice Visit Agent

Synthetic beneficiaries only · Prototype, not a clinical tool

Endpoint wait 900 ms

Say, e.g. “Sunita Devi, ID 4 5 2 1, ANC visit, weight 54 kilo, TT due, next visit 25 November, no bleeding.”

Time to first audio: **–** · State: **idle**

## Visit record

## Follow-up list

## No mic or loud room? Simulate speech

## Saved records

None yet.

## Log

**README (how it works, limits, citations)**

**Flow.** Speak notes → streaming recognition with interim results → own endpointing timer (slider) → rule-based extractor fills name, ID, visit type, weight, vaccines due, next visit date → danger-sign list is checked on every utterance and spoken first → agent reads the form back → she says “save” / “haan”, or corrects by voice (“no, weight is 2.8 kilo” overwrites only weight).

**Speech layer.** Uses the browser’s Web Speech API (Chrome/Android), streaming, with language set per ASHA (hi, en-IN, kn, ta, te, mr, bn). Barge-in: speech detected while the agent talks cancels playback. Use a headset or low volume to avoid the agent hearing itself. Browser STT gives no control over noise suppression, so noise robustness is only as good as the engine; the production plan is to swap `startRec()` for a streaming STT WebSocket (e.g. Gnani) and keep the rest unchanged.

**Danger-sign list** (keywords only, no diagnosis or advice): vaginal bleeding, convulsions, severe headache with blurred vision, fever, reduced fetal movement, severe abdominal pain, newborn not feeding, fast breathing/chest indrawing, newborn cold/limp, jaundice, cord pus. Adapted from WHO, *Pregnancy, childbirth, postpartum and newborn care: a guide for essential practice* (2015), and MoHFW/NHM HBNC and ASHA module danger signs. Verify against your team’s final guideline before use.

**Known limits.** Hindi/English cover is deepest; other languages have a smaller danger vocabulary and spoken read-back falls back to English. Negation (“no bleeding”) is handled per clause; mixed sentences can fool it, and fever is flagged without temperature thresholds. Records live in memory and are exported as JSON. No real beneficiary data.