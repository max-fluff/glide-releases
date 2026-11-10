# glide releases

Signed builds of glide, a software KVM for Mac and Windows: one mouse and keyboard across machines, a shared clipboard, files copied and dragged between them. The source is private; this repository only builds and publishes it.

## Windows

Download `glide-setup-x64.exe` from the [latest release](https://github.com/max-fluff/glide-releases/releases/latest) and run it. The installer:

- puts glide in `C:\Program Files\glide`;
- trusts the project's code signing certificate on this machine. glide needs that to type into windows of programs running as administrator (uiAccess). The certificate is limited to code signing;
- allows glide through Windows Firewall on private networks;
- offers to start glide at sign-in, and starts it.

On the first install Windows does not know the certificate yet, so SmartScreen and UAC show an unknown publisher. The installer is signed by `glide code signing (max-fluff)`, SHA-1 thumbprint `A66D7ADA73A16183E2DC5AE2730790659ED65FB0` (Properties → Digital Signatures).

To uninstall, use Settings → Apps → glide. Settings and pairings stay in `%APPDATA%\glide`.

## macOS (Apple Silicon)

`glide-macos-arm64.tar.gz` holds `glide.app`, signed by the same certificate.

## How releases are made

[`release.yml`](.github/workflows/release.yml) checks out a tag of the source with a read-only deploy key, builds it, and signs it with a key that only exists in this repository's secrets (`release` environment, `main` branch only). It then builds the installer with [Inno Setup](https://jrsoftware.org/isinfo.php) and publishes the release.
