# Connectix RADIUS v1

Linux server binaries with asynchronous RADIUS authentication, per-user traffic
accounting, and active-session authorization leases. All RADIUS protocols share
the client UUID as both username and password. User creation and revocation do
not restart the VPN service.

Source: private repository `gitconnect24/lightway`, commit
`3c76ce377b2098631391fb34c5937848cf74026b`.
Upstream ExpressVPN revision: `a69a711b006b30a3003eb6cba36fdff54b12bc1a`.
Build recipe: `packaging/connectix/` in the source repository.

Assets:

- `connectix-lightway-linux-amd64`: Linux x86-64.
- `connectix-lightway-linux-arm64`: Linux AArch64.
- `LICENSE`: upstream AGPL-3.0 license and copyright notices.

Built locally with Rust 1.98.1, locked Cargo dependencies, and Ubuntu 22.04.
Both executables require glibc 2.34 or newer and libgcc. VPN hosts download
binaries; they do not compile source. The installer validates ELF architecture
and replaces the binary atomically, without a binary SHA-256 check.

Validation:

- Seven native authentication/accounting tests passed on Linux.
- TCP and UDP delayed-authentication integration tests passed with traffic.
- Both architectures passed executable startup checks; ARM64 ran under QEMU.
- Live amd64 connection authenticated through FreeRADIUS and the application API.
- A client transferred 490 responses over one TCP socket while another account
  was created, disabled, re-enabled and deleted through the API. The runtime PID
  remained unchanged; disabled/deleted sessions lost access.

Deploy with the matching vServer RADIUS bridge, manager and authorization APIs.
Switching an existing snapshot inbound to RADIUS requires one runtime upgrade
and refreshed client profiles using `{{id}}` for both credentials.
The live test covered a few connected clients against the development database
containing 300,000 synthetic users; 2,000 concurrent connections were not tested.
