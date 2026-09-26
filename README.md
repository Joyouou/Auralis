# Auralis

A free, open-source menu-bar equalizer for Apple Silicon Macs running macOS 26 or later. Licensed under MIT.

## Build and run

Install Xcode with the macOS 26 SDK and select its command-line tools. From this folder:

```sh
bash build.sh
bash test.sh
```

Open the resulting `Auralis.app`. Click its menu-bar waveform icon to show the panel. Click outside to dismiss it; audio keeps running. Start audio enables local system-audio processing. macOS may ask for system-audio capture permission. Quit from the ••• menu.

This is an experimental Apple Silicon build. Intel Macs and older macOS versions are not supported. The local build is ad-hoc signed, not Developer ID signed or notarized. For a public binary release, sign and notarize with your own Apple developer credentials. Do not commit signing credentials.

## Presets

Click directly into the text editor to edit. Clicking elsewhere removes the caret without changing layout. Save writes to the selected preset; Load applies its text to audio. New creates a blank draft. Existing legacy PA/bell and JSON presets remain readable.

Default text format:

```text
Preamp: -6.0 dB
Filter 1: ON PK Fc 1000 Hz Gain -3.0 dB Q 1.500
Filter 2: ON LSC Fc 160 Hz Gain -2.0 dB Q 0.900
Filter 3: ON HSC Fc 6000 Hz Gain 2.0 dB Q 0.707
```

`PK` = bell, `LSC`/`HSC` = shelves with Q, `HPQ`/`LPQ` = high/low pass, `NO` = notch. ON/OFF is supported. Disabled zero-frequency/zero-Q placeholder rows are ignored. Frequencies accept Hz or kHz. Type `Flat` for no filters. Up to 64 filters; gain −24 to +24 dB; Q 0.1–24; frequency 10–24,000 Hz; preamp −48 to +12 dB. Shelves default to Q 0.707 when omitted.

Text displays and exports use numbered filters. Comments beginning with # are retained above normalized filter lines. Existing files are only changed when you Save. Generated preamp text and slider gains use one decimal. Control labels show frequency and Q to at most two decimals; precise values in preset text remain preserved.

## Automatic output presets

1. Connect and select an output.
2. Choose a saved preset in **Preset for this output**.
3. Keep **Auto-switch** enabled.

Mappings persist across launches. A macOS default-output change loads that output's saved preset. A newly connected mapped output can also become the system output. Disconnecting Bluetooth or unplugging headphones follows the available/default output and loads its mapping. Data-source identity distinguishes a headphone jack from speakers when the driver uses a shared device ID. Unmapped or unavailable preset files fall back to flat EQ at −6 dB on a route change.

Unsaved editor text is preserved during switching. Audio restarts on a new route only if processing was already enabled. It remains off if you stopped it. Launch starts with audio off; sleep stops processing. One headphone-jack mapping represents the jack, not individual analog headphone models (the jack cannot identify those).

## Delete and recover

The trash button removes a selected preset after confirmation and clears its mappings. App-managed files move to a local `Deleted Presets` folder; imported external files stay untouched and are removed from the library only. **••• → Undo delete** restores the most recently removed preset and its unassigned mappings, including after a restart. Older managed deletions remain in `Deleted Presets` for manual recovery.

## Privacy and storage

No account, network client, telemetry, audio recording, or cloud service is used. Live audio is processed in memory on the Mac. Settings, preset files, and device mappings stay under `~/Library/Application Support/Auralis/`; user defaults store imported preset paths and the last output UID. Those local data files must not be uploaded with source code.

This source package contains no personal presets, real device identifiers, recordings, session files, private diagnostics, developer username, or signing credentials. Test data are fixed EQ examples and fake device identifiers. Inter is used if installed in the user's Fonts folder; otherwise the system font is used. No third-party font is redistributed.

## Validation and limitations

Automated DSP, parser, preset, deletion, and simulated device-switch tests are included. Physical Bluetooth reconnect and headphone-plug transitions still need validation across different hardware. A short UI check is not a battery-life measurement. Audio Unit hosting, spatial effects, spectrum analysis, automatic login startup, and cross-platform builds are not included.

## Sharing on GitHub

Upload this folder's contents to a new repository, including LICENSE and .gitignore. Do not upload the original development workspace or your Application Support folder. Build artifacts belong in release attachments, not source control. No repository has been created or published as part of preparing this package.
