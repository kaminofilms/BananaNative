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

Package: dev.kaminofilms.bananative.ootfix; app label: Banana OOT Fix.
This is a separate installation alongside the official app and all earlier
ootdebug custom builds. It does not need their signing keys or uninstalling them.
The logs provider authority follows the new application ID.
Version: 0.2.4-depth1-side, versionCode 4. Uses the cached custom signing key.
The APK's actual package ID and label are checked with aapt before publication.

Android gives this app its own data folder. Existing saves and shader libraries
are not automatically shared; use the app's supported export/import to reuse
them. Nothing in this change deletes or modifies the original app's files.

Validation:
- The focused depth and shader tests run in the workflow.
- The APK signature, package ID and app label are checked after compiling.
- Device installation and gameplay remain unverified here.
