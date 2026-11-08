# Banana Native — Ocarina Android diagnostics

Unofficial diagnostic builds for Ocarina of Time on Android. Not a verified graphics fix and not affiliated with Nintendo, NVIDIA, Qualcomm, or Banana Native's maintainers.

The Actions workflow builds the Ocarina host from upstream v0.2.4 and reuses the matching official APK's embedded preparation runtime. It installs separately as `dev.nxnative.android.ootdebug`, preserving the official app. Add your own game to the test app; saves and prepared packs are not automatically shared.

Diagnostics enable texture-binding logging for the merge and fog shaders and disable asynchronous pipeline skipping. Expect slower diagnostic runs and larger logs. Use Share log after reproducing the problem.

No games, keys, user logs, or saves are included. Artifacts include the APK and exact source used to build it, including upstream license notices. Upstream: https://git.eden-emu.dev/moceure/BananaNative
