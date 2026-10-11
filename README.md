# Questium Sync v1.0.0

Questium Sync is a **Komikku fork for syncing your manga library with [Questium](https://github.com/Kirogii/Questium)** on Meta Quest. Questium itself remains based on Houri. The Android companion retains Komikku's reader, extension support and backup compatibility, and installs separately from Komikku.

## Pair and sync

1. Connect the Android phone and Quest to the same Wi-Fi network. Open **Settings → Questium Sync** on Android; open **Settings → Questium Settings → Questium Sync** in Questium.
2. Enable Questium Sync on both. Android displays a persistent notification while the local endpoint is enabled.
3. Turn on **Main sync device** on the Android companion only. Copy one device's pairing link into the other device's Pairing link field and select **Pair device**. Treat the complete pairing link as a password; it is replaced after pairing.
4. Select one or more paired devices and choose **Sync selected devices**. The main Android device reads the selected libraries, merges them and sends the result to every selected device. All selected devices must be reachable.

Main-device metadata, library membership and categories take precedence for books already known to the main device. Newly discovered books are imported uncategorized. Reading progress keeps each chapter's furthest page/read state, so Quest chapter 20 advances an Android copy at chapter 10. Sources must use the same source ID and manga URL on both devices; matching titles alone are never combined. Install the corresponding source extensions on each device; sync does not transfer extension APKs, downloaded pages or login credentials.

## Did you want this change? / Revert

The main Android device keeps a durable per-manga change log in the **Revert** tab before applying reading progress. Choose the manga's change to restore its previous chapter/page state and reading history. Then sync to update selected devices. A deliberate revert starts a new progress revision so old progress from an offline device cannot immediately undo it. Reading on an offline device before it receives that revision is intentionally superseded by the revert.

## Cloud backups

The **Cloud backups** tab creates a standard `.tachibk` library backup and opens **Google Drive** or **Proton Drive** to upload it. Install the selected provider app, sign in, and confirm its destination/upload. These are manual uploads using your account's available storage; Questium Sync does not need your cloud password or a paid backend. Restore through Komikku's normal Data and storage backup restore screen. Device pairing keys and the local Revert journal stay in app-private storage and are not included in ordinary backups.

## Background operation

The endpoint uses a blocking local socket rather than polling your library. No library database scan or backup is performed while waiting; transfer work and database reads start only after an authenticated request. Disable the switch or press **Stop** in the notification to close it. There is no permanent wake lock. Android's battery-saving/Doze behavior and Wi-Fi client isolation may make a sleeping device unreachable; open the companion and retry. Pair again if the main device's IP changes. The first implementation supports local IPv4, up to two active connections and a 32 MiB encrypted metadata payload. It does not expose a public internet endpoint.

## Updates

App updates check only [Kirogii/Questium-Sync releases](https://github.com/Kirogii/Questium-Sync/releases), including debug/preview checks. Komikku release feeds are not used. Install the signed stable APK to receive future in-place updates.

## Build

Use JDK 21 and Android SDK 36. Run `./gradlew spotlessApply`, `./gradlew spotlessCheck`, then `./gradlew assembleDebug`. Run the sync merge/encrypted transport tests with `./gradlew :app:testDebugUnitTest --tests "*.QuestiumSyncTest"`. The application ID is `app.questium.sync` (`.dev` for debug builds).

## Download and support

Download the signed APK from [Questium Sync releases](https://github.com/Kirogii/Questium-Sync/releases/latest). Choose `arm64-v8a` for most modern Android phones, or the universal APK if unsure. Report fork-specific problems in [Questium Sync issues](https://github.com/Kirogii/Questium-Sync/issues).

## Credits

Based on [Komikku](https://github.com/komikku-app/komikku), with its Mihon, Tachiyomi and TachiyomiSY heritage. Thank you to the [original contributors](https://github.com/komikku-app/komikku/graphs/contributors). Original copyright and license notices remain in the source and [LICENSE](LICENSE).

## License

    Copyright 2015 Javier Tomás

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
