# Ocarina foliage depth candidate

Based on the supplied BananaNative v0.2.4 source archive:
- Source commit: d2ba0dc9bd0ab3e5657c95adf8bc4bd5e417109a
- ZIP SHA-256: 644494f4ea60553bd561869937ca0f758058bb91b8a19f7ddd276414ccd779fc
- Official APK SHA-256: 972ad854455727531ef70440179954e26054ee253555b6c05dfd7c3c7b9f38b5

The upstream Qualcomm foliage workaround skips known broken mesh prepasses and
changes their paired colour draws from EQUAL to LEQUAL. It leaves depth writes
disabled, so the affected geometry remains absent from depth.

This candidate makes only the paired, depth-tested, read-only EQUAL colour draws
write depth with LEQUAL. Other comparisons, unpaired shaders and disabled depth
tests retain their state. It keeps the existing upstream spike workaround.

This corrects missing depth after the colour pass. It does not repair Qualcomm's
prepass compiler issue, recover depth for consumers before the colour pass, or
prove the cause of every black patch or lighting error. Visual results and the
reported gameplay exit remain unverified. Do not describe this as a confirmed
graphics or crash fix.

No shader translation, chain version, shader profile input, preparation runtime,
or forced environment setting is changed. Existing compatible shader libraries
and this custom application's pipeline cache can be reused. An official app's
private cache is separate. No save migration or deletion is performed.

Package: dev.nxnative.android.ootdebug, same as the previous custom baseline.
Uses an explicit custom keystore path cached by Actions (banana-oot-signing-v2).
The old cache did not save a key, so this candidate's certificate is different
from earlier custom builds; an in-place update over those builds is not promised. It cannot update the official release;
an update over a custom build also requires matching signing certificates.
Keep existing app data and saves. Version: 0.2.4-depth1, versionCode 3.

Validation:
- The production depth-state helper is compiled and exercised over 64 combinations
  of paired/unpaired, test on/off, write on/off, and the eight depth comparisons.
- Related specialization and shader ABI tests run in the workflow.
- No phone is connected here: system-driver and Turnip gameplay, before/after
  screenshots, memory usage, and crash behavior require device verification.
- Local host tests could not build without clang; Metal graphics tests require
  Apple's xcrun. The full Python suite has environment-related failures; only
  the explicitly reported focused suite is passing.
