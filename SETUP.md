MARIO KART TOUR 4.0.0 — ANDROID 16 EMULATOR SETUP
==================================================

**NOTE. THIS FILE IS AI GENERATED FOR EFFICIENCY. We will make a better version later, but wanted to document our notes quickly.**

Host:
- Apple Silicon Mac (tested on Apple M4)

Android:
- Android 16
- API Level 36

Android Emulator:
- Version 37.1.11.0
- Graphics backend: GFXStream

GAME:
- Package: com.nintendo.zaka
- Version: 4.0.0
- Unity: 2022.3.69f1
- Architecture: arm64-v8a

SETUP:
1. Create/start an Android 16 (API 36) AVD.
2. Install Mario Kart Tour 4.0.0 and its required split APK(s).
3. Force Mario Kart Tour to use the native GLES driver instead of ANGLE:

   adb shell settings put global angle_gl_driver_selection_pkgs com.nintendo.zaka
   adb shell settings put global angle_gl_driver_selection_values native

4. IMPORTANT: Launch the emulator using SwiftShader software rendering:

   ~/Library/Android/sdk/emulator/emulator @YOUR_AVD_NAME -gpu swiftshader_indirect

5. Launch Mario Kart Tour.

KNOWN WORKING CONFIGURATION:
- Android 16 / API 36
- Android Emulator 37.1.11
- GFXStream
- Native GLES (ANGLE disabled for Mario Kart Tour)
- SwiftShader rendering

WHY SWIFTSHADER IS REQUIRED:
- Hardware GFXStream → Apple M4 Metal produced a black screen.
- GFXStream repeatedly reported:

  GL error 0x506
  checkFramebufferCompleteness(GL_FRAMEBUFFER) != GL_FRAMEBUFFER_COMPLETE

- `adb exec-out screencap -p` also produced a completely black image.
- Audio and touchscreen input continued to work.
- Switching the emulator to SwiftShader made Mario Kart Tour render correctly.

HARDWARE RENDERING:
- Current hardware path:
  GLES → GFXStream → Apple M4 Metal
- This currently results in an incomplete framebuffer and black video output.
- Do NOT rely on hardware rendering for this setup until the GFXStream/Metal issue is resolved.

OPTIONAL: REMOVE THE ANGLE OVERRIDE
-----------------------------------
To restore the default ANGLE settings:

adb shell settings delete global angle_gl_driver_selection_pkgs
adb shell settings delete global angle_gl_driver_selection_values

Then reboot the emulator if necessary.

KNOWN-GOOD BASELINE:
--------------------
Android 16/API 36
+ Emulator 37.1.11
+ GFXStream
+ Native GLES
+ SwiftShader
= Mario Kart Tour 4.0.0 WORKS
```
