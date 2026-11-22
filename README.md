# ASHA Bol – Voice Visit Register

Speak a home-visit note, hear it read back, fix it by voice, and get a follow-up list. No typing. Built for the BolBharat Voice AI Challenge (Healthcare: Voice field register for ASHA workers).

**Live demo:** https://banupriyagowda.github.io/asha-bol-voice-agent/
(Open in Chrome on Android or desktop and allow the microphone.)

> Synthetic beneficiaries only. Prototype, not a clinical tool.

## What it does
1. **Voice capture:** streaming speech recognition (Hindi, English, Kannada, Tamil, Telugu, Marathi, Bengali) with English code-mix such as "TT injection" and "ANC checkup".
2. **Structured record:** fills name, beneficiary ID, visit type, weight, vaccines due, next visit date.
3. **Read-back and voice correction:** the agent reads the form aloud. Say "save" or "haan" to confirm, or correct: "no, weight is 2.8 kilo" changes only the weight.
4. **Danger-sign escalation:** if a sign from the list below is spoken, the agent immediately says in her language to refer to the PHC now, shows a red banner and flags the record. No diagnosis or treatment advice.
5. **Follow-up list:** referral, vaccines due, revisit date, missing fields.

## Try it (60-second demo)
1. Choose a language and tap **Start visit**.
2. Say: "Sunita Devi, ID 4 5 2 1, ANC checkup, weight 54 kilo, TT injection due, next visit 25 November."
3. Listen to the read-back. Say: "no, weight is 52 kilo". Hear the updated read-back.
4. Say: "save". Check the follow-up list.
5. Danger test: say "newborn visit, ID 7 7 0 3, baby has fever and is not feeding". The red alert and spoken referral fire.
6. No mic or noisy room? Use the **Send as speech** box and the sample buttons.

## Speech layer
- Streaming recognition with interim text shown live.
- Own endpointing timer, adjustable with the slider (500–1800 ms).
- Barge-in: speaking while the agent talks cuts it off.
- Time to first audio (end of speech to agent audio) is displayed on screen.
- Digit words ("four five two one") and "2 point 8" are normalised.
- Noise: uses the browser engine, which gives no noise-suppression control. Production plan: replace `startRec()` with a streaming STT WebSocket (e.g. Gnani) and keep the rest unchanged. Use a headset to avoid the agent hearing itself.

## Danger-sign list (keywords only)
Vaginal bleeding, convulsions, severe headache with blurred vision, fever, reduced or absent fetal movement, severe abdominal pain, newborn not feeding, fast breathing or chest indrawing, newborn cold/limp/unconscious, jaundice, pus at the cord.

Sources:
- WHO, *Pregnancy, childbirth, postpartum and newborn care: a guide for essential practice* (3rd ed., 2015).
- MoHFW / NHM, Home Based Newborn Care (HBNC) guidance and ASHA module danger signs.

Verify against the team's final guideline before any real use.

## Responsible AI guardrails
- Synthetic data only; nothing is sent to a server; records live in browser memory and are exported as JSON on request.
- Escalation follows the list only. No diagnosis, no treatment advice.
- Read-back before save, so a human confirms every record.
- Negations ("no bleeding") are skipped per clause.

## Known limits
- Hindi and English are deepest; other languages have a smaller danger vocabulary and read-back falls back to English (the escalation line is localised).
- Rule-based extraction can miss unusual phrasing; a mixed sentence can fool negation handling.
- Fever is flagged without temperature thresholds.
- Requires a browser with the Web Speech API (Chrome recommended).

## Run locally
Open `index.html` in Chrome. No build step.
