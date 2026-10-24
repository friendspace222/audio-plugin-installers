# Tideglass and Ironvale native Mac installer build

This folder is prepared for review. No repository has been created, files uploaded,
or workflow triggered as part of preparing it. It contains source inputs and a
GitHub Actions workflow, not finished Mac installers.

The workflow builds each product on `macos-15-intel`, targeting Intel `x86_64`
and a minimum deployment version of macOS `10.15`. Successful builds produce
separate downloadable ZIP artifacts for Tideglass and Ironvale containing native
`.pkg` installers, `.dmg` images, checksums, installation instructions, validation
records, and corresponding source archives. End users install the compiled
products without developer tools or building source.

The workflow runs automatically only when the source ZIP or workflow changes on
`main`, and can also be started manually. Each of its two matrix jobs has a
25-minute timeout; at most two run in parallel. It has `contents: read`
permission, does not publish releases, does not deploy anything, and does not
use signing or notarization credentials. It is intended only for a public
repository using GitHub's free standard runners. A job-level guard skips private
repositories before allocating a runner. Only the standard `macos-15-intel`
label is used; there are no larger, custom, self-hosted, or paid runner options.
Both installer and failure-diagnostic artifacts expire after one day. The user
has authorized no costs. This folder does not authorize publishing source or
starting any workflow; approval remains with the parent task.

## Inputs

- `.github/workflows/build-installers.yml`: build and validation workflow.
- `audio-plugins-source.zip`: original Tideglass and Ironvale source trees,
  tests, build/package scripts, documentation, copyright and license notices.
- `audio-plugins-source.zip.sha256`: SHA-256 verified before extraction.

Previews, audio demos, existing binaries, build folders, distribution folders,
dependency copies, validation logs, and generated archives are excluded from the source ZIP.
Each existing CMake configuration fetches JUCE 7.0.12 at commit
`4f43011b96eb0636104cb3e433894cda98243626`. The resulting corresponding-source
archive includes the full JUCE tree used in that build and its license notices.
The default combined plugin distribution uses GPLv3; original project copyright
and license files are preserved without modification.

## Checks and limits

The workflow runs the native DSP and processor tests, the simulated packaging
regression suite, Mach-O architecture and minimum-OS checks, native `pkgbuild`
and `productbuild`, package payload inspection, signature verification, Apple's
`auval` against the AU extracted from the installer, disk-image verification,
and checksum verification. Installer artifacts are uploaded only after all
required checks pass. Failed builds may upload a separate diagnostic artifact.

The newer macOS build host cannot prove compatibility with Catalina 10.15.7.
Neither deployment metadata nor AU validation on macOS 15 replaces runtime and
listening tests in the user's Catalina/Logic/GarageBand environment. The
installers are unsigned and not notarized; the plugin binaries are ad-hoc signed.

References: [GitHub runner labels](https://docs.github.com/en/actions/reference/runners/github-hosted-runners),
[Apple packaging guidance](https://developer.apple.com/documentation/xcode/packaging-mac-software-for-distribution).
