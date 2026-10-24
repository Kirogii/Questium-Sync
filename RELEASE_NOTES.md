# Questium Reader v1.1.0

- Remove the 32 MiB hard limit from Questium Sync payloads; larger libraries can sync within the wire protocol's framing limits.

First Questium Sync release, based on Komikku.

- Pair Android and Questium on the same local network and select one or multiple devices.
- Designate the Android main device. Its library settings win while furthest chapter/page progress advances across devices.
- Keep a per-manga progress change log and restore previous progress in the Revert tab.
- Keep a low-activity background endpoint available with a Stop action; no idle library polling or permanent wake lock.
- Create manual backups through Google Drive and Proton Drive.
- Use the controller app icon and a separate application ID.
- Check updates only from Kirogii/Questium-Sync. Upstream Komikku tags are removed; this fork starts at v1.0.0.

Initial release: two-device Android/Quest testing and cloud-provider upload confirmation still need real-device validation.

- Compress Questium Sync transfers with maximum gzip compression and no 5 MB cutoff. Sync only reading history/progress and library membership, with a checked-by-default option to sync new books to the main device. Update both devices for the new protocol.

- Sync extension repositories before missing extensions, and keep per-device JSON checkpoints so repeat syncs transfer changed chapter progress instead of the whole library.

- Use the same Questium launcher and themed icon as the VR reader.
