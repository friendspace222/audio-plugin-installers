# Tideglass and Ironvale

Two original audio plugins for Intel Macs, available as Audio Unit, VST3, and
optional standalone applications. These are development previews.

- **Tideglass:** stereo delay and algorithmic reverb, with straight, dotted, and
  triplet timing, tempo sync, feedback, independent effect switches, and mix controls.
- **Ironvale:** guitar and bass amplification with Clean, Edge, Crunch, and Lead
  channels; 1x12 through 8x12 cabinet voicings; custom cabinet IR loading; and
  compressor, overdrive, bass dirt, chorus, phaser, and stereo delay pedals.

## Install

1. Open [Actions](https://github.com/friendspace222/audio-plugin-installers/actions/workflows/build-installers.yml)
   and select a successful build. Download `Tideglass-macOS-Intel-Installer` or
   `Ironvale-macOS-Intel-Installer` from its artifacts. Artifacts expire after one day.
2. Extract the downloaded ZIP and quit Logic Pro or GarageBand.
3. Double-click the `.pkg` installer and follow Apple's Installer. Alternatively,
   open the `.dmg` and launch the installer inside it. Select **Audio Unit** for
   Logic/GarageBand and enter your Mac administrator password when requested.
4. Reopen your DAW and select the plugin from its Audio Units menu.

The compiled installers require no developer tools or source compilation on the
destination Mac. Each download includes checksums, installation instructions,
a build validation record, and corresponding source.

Installers are **unsigned and not notarized**; plugin binaries have ad-hoc code
signatures. If Catalina blocks an installer, Security & Privacy preferences may
offer **Open Anyway** after the first attempt. Only approve files you trust.

## Compatibility and builds

The deployment target is **Intel x86_64, macOS 10.15**, including the intended
Catalina 10.15.7 target. Builds and automated runtime checks run on **macOS 15**.
Successful checks there do not establish Catalina or Logic/GarageBand compatibility;
testing and listening in the destination environment remain necessary.

The public workflow uses GitHub's free standard `macos-15-intel` runners and skips
private repositories. It builds both plugins, runs DSP and processor tests,
checks binary metadata, creates native packages, inspects their payloads, validates
the packaged Audio Units with `auval`, and verifies disk images and checksums.
Installer artifacts are uploaded only after those checks pass.

## Source and license

`audio-plugins-source.zip` contains the development source, tests, scripts,
documentation, and license notices. Its SHA-256 is checked before each build.
JUCE 7.0.12 is pinned to commit `4f43011b96eb0636104cb3e433894cda98243626`.

The combined plugins are distributed under **GPLv3**. Original copyright and
license notices are retained. Each installer download includes corresponding
source with the full JUCE source tree used for that build; keep that archive and
the notices alongside the installer when redistributing it.
