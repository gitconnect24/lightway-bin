# Connectix Lightway Linux binaries

Download tested server binaries from [Releases](https://github.com/gitconnect24/lightway-bin/releases).

| Architecture | Release asset |
| --- | --- |
| Linux x86-64 | `connectix-lightway-linux-amd64` |
| Linux ARM64 | `connectix-lightway-linux-arm64` |

Builds use Rust 1.98.1, the locked Cargo dependencies, and Ubuntu 22.04.
The vServer installer downloads a pinned release over HTTPS and checks its ELF
architecture before replacing the installed executable. No compiler is needed
on the VPN host.

Source and build instructions are maintained in the private
[`gitconnect24/lightway`](https://github.com/gitconnect24/lightway) repository,
under `CONNECTIX.md` and `packaging/connectix/`. Each release identifies its
matching source commit.

Based on [ExpressVPN Lightway](https://github.com/expressvpn/lightway), licensed
under AGPL-3.0. The upstream license and copyright notices are preserved.
