# Grace AR for Android

This Unity project places Grace's complete liquid chamber in an Android ARCore scene. Grace remains inside the transparent tube. The chamber is a world-space object, so it disappears naturally when the phone camera is pointed away and reappears when the user looks back during the same AR session.

## Current milestone

- Android-only Unity project using AR Foundation and Google ARCore.
- Loads the existing `Grace.vrm` model at runtime.
- Procedural transparent chamber, liquid, illuminated rings, and bubbles.
- Tap a detected floor to place or move the chamber.
- Grace gently floats and has initial **Wave** and **Turn** actions.
- The chamber is attached to an ARCore anchor for the current tracking session.

Persistent recognition of the exact lab corner after fully closing the app will use an image marker mounted near that corner. That is the next milestone; a plain saved coordinate is not reliable because ARCore creates a new origin in each session.

## Open and build

1. Install Unity Hub and Unity 6, including **Android Build Support**, **Android SDK & NDK Tools**, and **OpenJDK**.
2. Open this repository's root directory as a Unity project.
3. Let Unity resolve the AR Foundation, ARCore, and UniVRM packages.
4. Run **Grace AR > Configure Android and Create Scene** from Unity's menu.
5. Open **Edit > Project Settings > XR Plug-in Management > Android** and enable **ARCore**.
6. Connect an ARCore-supported Android phone with USB debugging enabled.
7. Use **File > Build Profiles**, select Android, then **Build and Run**.

The first launch needs camera permission. Move the phone slowly until a floor is detected, then tap where Grace's chamber should stand.

## Mirror Grace's WebUI replies

1. Open the Telepathy WebUI from your phone's browser to confirm that the phone can reach its HTTPS address. Use the existing trusted HTTPS endpoint, such as [Tailscale Serve](https://tailscale.com/kb/1312/serve).
2. In the AR app, tap **Telepathy HTTPS address**, enter that same address, and tap **Connect**. Place Grace's chamber if you haven't already.
3. Send a message to Grace from the WebUI. On the phone, her mouth moves as reply text arrives. Tap **Disconnect** to stop listening.

The app subscribes to the same response topic as the WebUI. The mouth movement follows streamed text and approximates speaking. Audio and timing data for lip sync are not part of that stream. Use an endpoint you control, since the response topic carries live chat text.

## Project layout

- `Assets/StreamingAssets/Grace.vrm`: Grace's runtime model.
- `Assets/GraceAR/Scripts/GraceArApp.cs`: AR session, placement, and controls.
- `Assets/GraceAR/Scripts/GraceChamber.cs`: procedural tube and liquid.
- `Assets/GraceAR/Scripts/GraceVrmLoader.cs`: Android-safe VRM loading.
- `Assets/GraceAR/Scripts/GraceActionController.cs`: floating and actions.
- `Assets/GraceAR/Scripts/GraceReplyStream.cs`: read-only subscription to Telepathy replies.
- `Assets/GraceAR/Editor/GraceArProjectSetup.cs`: Android and scene setup.

