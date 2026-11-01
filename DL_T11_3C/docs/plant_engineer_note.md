# Early-warning system for bearing faults: a note for plant engineers

**What it does.** It listens to a motor's vibration and learns what a healthy bearing looks like. When the vibration stops looking healthy, it raises an alert.

**What it never saw.** It was taught on healthy data only. It was never shown a broken bearing, so it can also react to fault types it has not met.

**How it did on our test.** On laboratory test recordings it flagged all 18 faulty test recordings (inner race, ball and outer race, at motor loads of 2 and 3 HP). The first alert came within one reading, about 0.09 seconds. It raised no false alerts in the 27.7 seconds of healthy test data we held back.

**The honest limit.** Our healthy test data lasted only 27.7 seconds, so we cannot promise how many false alerts per day you will see. These were also strong, laboratory-made faults; real wear grows slowly and may be harder to catch. A simple "is the vibration much stronger than usual" rule also worked almost as well on this test, so the test was easy.

**The alert level.** A missed fault costs about Rs 4 lakh and a false alert about Rs 2,000, so we lean towards catching faults. We recommend alerting when the pattern error is roughly three times its usual healthy level (setting A in the report). It caught every faulty reading in our test and gave no false alert on healthy readings. A higher setting (B) saved nothing in our test and let some faulty readings through.

**Before you rely on it.** Run it in watch-only mode on your own machine for a few weeks and count the alerts, then set the alert level using your own data. Do not let it stop a machine automatically until then.

**What to do on an alert.** Check bearing temperature and noise; if both look normal, inspect at the next planned stop.

**When to retrain.** After a bearing or motor change, or a big change in load or speed.
