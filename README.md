# Banana Native — Ocarina Android investigation

The current workflow rebuilds upstream v0.2.4 with the official play-mode behavior, default supported profiles and unchanged renderer/shader translator. It removes the earlier diagnostic environment defaults. This is a baseline to investigate a gameplay crash, not a verified lighting fix.

The only app identity change is the separate package `dev.nxnative.android.ootdebug`; the official app stays installed. Signing is unofficial, so this is not byte-identical to the official APK. The matching official APK supplies the on-device preparation runtime, verified by its published SHA-256.

Reuse prepared shaders: in the official app, Manage → Export pack to a folder in Download. In this app, add the same game then Manage → Import pack. Import saves separately. The Vulkan driver pipeline cache is separate and may warm up again. Do not choose Prepare again unless the pack compatibility check requires it.

The first diagnostic build used a temporary signing key. The current workflow caches its debug key for subsequent builds. If Android rejects this update due to a different signature, first export any needed saves and pack from the diagnostic app, then reinstall only that diagnostic app. Keep the official app installed.

Artifacts contain the APK and matching build source with upstream license notices. No games, keys, user logs or saves are uploaded. Not affiliated with Nintendo, NVIDIA, Qualcomm or Banana Native maintainers. Upstream: https://git.eden-emu.dev/moceure/BananaNative
