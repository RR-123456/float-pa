# Pragon Mobile v13: Pragon PA Manage mode (from the Manage Calls spec + 13 key rules)

**Not compiled** (no Kotlin compiler here). Build with GitHub Actions and send any `e:` lines.

## New
* Call choices are now: **manage, speaker, answer, ignore, decline** (voice, or the MANAGE / ANSWER / DECLINE buttons on the ring notification; speaker and ignore by voice).
  * manage = Pragon talks to the caller, keeps you updated, can ask you to CONNECT.
  * answer = Pragon takes a message only (cannot put the caller through).
  * speaker = answers and puts the call on the loudspeaker, no AI.
* **Caller wants the owner:** Gemini says "please hold", calls the new `request_owner` tool; phone vibrates; notification shows **CONNECT / I'M BUSY / TAKE OVER**.
  * One app-owned 30 s timer per request (Gemini does not time it). Timeout = I'M BUSY. A late CONNECT does nothing; repeated taps do nothing.
  * I'M BUSY / timeout: the app tells Gemini to say you're busy, take a message, say goodbye and end the call.
  * CONNECT: Gemini is stopped, audio returns to the normal route and you carry on the call.
* **Live owner updates:** notification text follows what the caller said (name, purpose, urgency, callback). Scam and emergency flags vibrate and change the title.
* **Gemini prompt:** identifies itself as an AI, collects organisation / message, flags emergencies (never claims emergency services were called), follows language switches, never invents numbers.
* **Summary** now includes organisation, message, emergency, outcome, length and mode; lock-screen content is hidden (private visibility). Last 20 kept as before.
* Manifest: VIBRATE permission.

## Not done (needs your decision or a device)
* **Hear Pragon on/off:** not built. With audio only through the loudspeaker you hear Pragon whenever the caller does; "off" would need a way to mute it for you but not the caller, which Android doesn't offer.
* CONNECT/I'M BUSY on the **floating bubble** itself (only notification buttons for now; a bubble tap still means take over).
* Empty-call fallback if Gemini cannot connect: it says so and hands over (existing behaviour).
* Spec's full 18-state machine: replaced by the few flags above (waiting / manage / pendingAi).
