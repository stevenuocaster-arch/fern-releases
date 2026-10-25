---
title: Fern Privacy Policy
permalink: /privacy/
---

# Fern Privacy Policy

Last updated: October 24, 2026

Fern is a desktop songwriting notebook for Windows. This policy explains what Fern keeps on your computer, what it sends to servers, and what it does not do. It is written for the Fern desktop app. It is provided by Steven Caster ("we"). Contact: [stevenuocaster@gmail.com](mailto:stevenuocaster@gmail.com).

This is a plain-language description of how the app works. It is not legal advice.

## The short version

- Your songs live in a database file on your own computer, and you can keep working while offline.
- You need a Fern account to use Fern: the app shows a sign-in screen and has no guest or skip option. Once you are signed in, your library syncs by default to a hosted service (Supabase) so it appears on your other devices. Sync is not an opt-in setting. That sync is not end-to-end encrypted: the service can technically read what is synced.
- Fern uploads your recording audio files (takes and voice memos) to the same service automatically, for sync, with no prompt: when a recording finishes, and again after each successful connection to the service, so recordings made earlier, before you signed in, or on another device also upload. Files over 45 MiB are never uploaded and stay on your computer.
- Fern has no analytics, no advertising, and no crash reporting.
- We do not sell your data.
- Today there is no "delete my account" button in the app. See "Deleting your data" below for what you can do, including how to ask us to delete your account and cloud data.

## What stays on your computer

Fern stores these in its data folder on your computer (normally `%APPDATA%\com.fern.app`):

- Your library: songs, lyrics, notes, chords, checklists, tags and settings, in one SQLite database file. This file is not encrypted by Fern.
- Your recordings, as WAV audio files in `recordings` (takes) and `voice` (voice memos) folders. These are not encrypted by Fern.
- Optional downloaded models (see "Transcription and search" below).
- Data kept by the app's built-in web view, in a second folder with the same name under `%LOCALAPPDATA%\com.fern.app`.
- Your sign-in session and, if you use it, your Google Drive connection. These are stored in files protected with the Windows per-user data protection feature (DPAPI), so they are tied to your Windows user account.

Fern also makes snapshots of your library database (Settings, Backup & recovery). By default they are saved in a `recovery` folder inside the Fern data folder; you can optionally choose another destination. Snapshot files are not encrypted by Fern. Fern does not send them anywhere.

## What is sent to our hosted service

Fern uses a hosted Supabase project (database, sign-in, file storage) in the United States (AWS us-east-2, Ohio). Because Fern requires an account, signing in sends the items below to this service by default. Whether new accounts can be created at any given time is up to us, and we may limit or close sign-ups.

- Account: your email address and password, handled by Supabase Auth. Fern keeps a sign-in session on your computer (see above), not your password.
- Synced library content: the content of your songs and related items (for example lyrics, notes, chords, checklists, tags, saved chord shapes, recording labels and lengths, and any links you add to Google Drive or SoundCloud files, with the label you type for them or, for a Google Drive link, the Drive file name Fern fills in). Each sync entry carries your account ID, an item ID, a table name, the kind of change (insert, update or delete), the ID of the device that made it, timestamps, and the item's content. The service also keeps a list of the change IDs it has already processed.
- Recording audio: Fern uploads each recording's WAV file (takes and voice memos) to a private storage bucket named `demo-audio`, in a folder named after your account ID, as described above. The bucket's file-size limit is 45 MiB; larger recordings are not uploaded.
- Connection details: Supabase's API gateway and Auth logs can include your IP address and your app's user agent. Supabase keeps these logs for a period set by its plan (its documentation currently lists 7 days for the Pro plan). We do not use them.
- Access control: the sync tables and the audio bucket use Postgres row-level security so that your signed-in account can read and write only its own rows and its own folder.

Plainly: Fern does not encrypt your synced content or uploaded audio before sending it. It is protected in transit by HTTPS and separated per account by the access rules above, but the service operator (Supabase, and the person running this project) is technically able to read it. We do not intend to look at your content. Do not use the sync feature for anything you would not be comfortable storing on a cloud service.

We use Supabase as our service provider; its handling of data is described in its own terms and privacy policy.

## Sign-in options

- Email and password, through Supabase Auth.
- Google sign-in. Fern asks Google only for the basic sign-in scopes `openid`, `email` and `profile`. It is used to identify your account. Fern does not use it to read your Google files. Supabase Auth receives the basic profile details Google returns for those scopes.

## Google Drive (optional)

If you choose to link an audio file from Google Drive:

- Fern asks for the Google scope `drive.file`, which limits access to files you select for Fern. You paste a Drive link in Fern and confirm that one file on Google's own consent screen. In this version Fern plays WAV audio files only, up to 45 MiB. (Google's file-picker request also allows MP3 files to be selected, but MP3 playback is switched off, so an MP3 you pick would not play.)
- Fern reads that file only to play it inside the app. The audio is held in memory for playback; Fern does not save a copy to disk and does not upload it to our service.
- Fern asks Google Drive for the file's name, to fill in the link's label. That label is saved in your song and is part of your synced song data. When you play the file, Fern also asks Drive for basic details (such as its size, type, version, checksum, whether it is in the trash, whether it can be downloaded, and whether its revision is kept forever) to check that it can be played.
- Fern stores the file's Drive ID (and its resource key, if Google provides one) with your song so you can play it again. That link information is part of your synced song data.
- Fern stores a Drive refresh token, the Drive account's email address and ID, and the IDs of the files you authorized in a DPAPI-protected file on your computer so you stay connected. It is not sent to our service.
- You can disconnect Google Drive inside Fern (Settings, Connected services). That deletes the stored token and account details from your computer. It does not revoke Fern's access at Google, so to do that, visit https://myaccount.google.com/permissions

## Google user data

This section covers all the data Fern receives from Google: the basic sign-in details and, if you use Drive links, the access described above.

- What we access: with Google sign-in, your Google email address and basic profile details (scopes `openid`, `email`, `profile`); with Drive links, only the specific files you select (scope `drive.file`): the audio for playback, the file's ID, its name, basic file details (such as size, type, version, checksum and trash status), and the email address of the Drive account.
- How we use it: Google sign-in details are used only to identify and sign you in to your Fern account. Drive files are used only to play them for you inside Fern. We do not use Google user data for advertising, and we do not transfer or sell it to advertising platforms, data brokers or information resellers.
- Where it is stored: sign-in details are held by Supabase Auth in the hosted service and in the protected sign-in session on your computer. The Drive file's ID, resource key and the file name (as the link's label) are stored in your song data on your computer and in the hosted service (synced). The Drive token, the Drive account email and ID, and the IDs of files you authorized are stored only on your computer. Drive audio is never stored.
- Who it is shared with: Supabase, our service provider, receives the sign-in details and the synced Drive file IDs and file names, only to run Fern for you. We do not share Google user data with anyone else, except where the law requires it or where needed for security (for example, investigating abuse).
- Human access: we do not read your Google user data, except with your agreement, where needed for security or abuse investigation, or where the law requires it. As the operator we may run aggregate counts (for example the number of sync entries by type) and automated format checks that process synced entries on the operator's own computer without anyone reading them, to keep the sync service working.
- How long it is kept, and deleting it: sign-in details stay in the hosted service until your account is deleted (see "Deleting your data"); the hosting provider's authentication activity log may keep entries (such as sign-in time and IP address) for a deleted account; we do not remove these entries as part of an account deletion, and how long they are kept is set by Supabase. A Drive link (including its file name) stays in your song data until you delete or change it in Fern. The Drive token, account details and authorized file IDs on your computer are deleted when you disconnect Drive in Fern, and with the app's data folder if you delete it.

Fern's use and transfer to any other app of information received from Google APIs will adhere to the [Google API Services User Data Policy](https://developers.google.com/terms/api-services-user-data-policy), including the Limited Use requirements.

## SoundCloud links (optional)

You can add a public SoundCloud track link to a song. Fern has no SoundCloud account or login. To play it, Fern asks SoundCloud's public oEmbed service about the link and shows SoundCloud's official player. Your computer then contacts SoundCloud, which can see your IP address and what you play, under SoundCloud's own policies. If you paste a private SoundCloud link with a secret token, that token is stored with your song and synced like other song data.

## Transcription and search (on your computer)

- Voice-to-lyrics uses a speech-recognition program (whisper.cpp) that runs on your computer. Your audio is not sent anywhere for transcription.
- Semantic search uses a small embedding program that runs on your computer, listening only on a local address. This version has no Settings button that downloads the search model.
- The speech-recognition model is downloaded when you start the download in Settings. The file comes from Hugging Face (huggingface.co) or its content-delivery hosts, which can see your IP address and that you downloaded the file.

## Updates

Fern checks once a short while after it starts (about 30 seconds), and when you press the button in Settings, for a new version. It requests a file named latest.json from the Releases page of this project's public GitHub repository (github.com/stevenuocaster-arch/fern-releases). GitHub therefore sees your IP address and standard connection details under GitHub's own policies. Fern does not add your account or library information to that request. If you choose to update, the installer is downloaded from the same place.

## What Fern does not do

- No analytics, usage tracking, advertising or crash-reporting services are built into Fern.
- Fern's code does not send your songs, lyrics or recordings to any AI service.
- Fonts are bundled with the app; Fern does not load fonts from a web font service.

## Deleting your data

- On your computer: delete songs, items and recordings inside Fern. To remove everything, uninstall Fern and tick the uninstaller's option to delete the application data, which removes Fern's folders named `com.fern.app` under your Windows roaming and local application data (including `%APPDATA%\com.fern.app`). If you do not tick it, or if the uninstall is an automatic update, that folder stays and you can delete it yourself. Copies you made elsewhere, such as a backup destination you chose or files you exported, are not removed.
- In the cloud, inside Fern: deleting an item in Fern syncs a deletion, which clears its content from the sync service and leaves a small marker (item ID, table name, device ID and timestamps, with no content). Deleting a recording also removes its uploaded audio file. Cloud copies can remain in some cases, for example a recording deleted while its upload was in progress, a recording deleted while you are offline or signed out, or after restoring an older snapshot of your library.
- Your whole account: Fern does not yet have an in-app way to delete your account or all your cloud data. To ask for your account and cloud data to be deleted, email [stevenuocaster@gmail.com](mailto:stevenuocaster@gmail.com) from the address on your account. We will complete the deletion within 30 days of your request. Copies in the hosting provider's own backups or logs may persist for a limited time under its policies. In particular, Supabase Auth's activity log may keep entries (such as sign-in time and IP address) for a deleted account. We do not remove these entries as part of an account deletion, and how long they are kept is set by Supabase.
- Signing out removes the session from your computer. It does not delete anything from the cloud.

## Your copy of your data

Your library and recordings are ordinary files on your computer, and you can copy them at any time. Fern has MIDI and printable export for songs and chords. There is no single "download everything from the cloud" button yet.

## Children

Fern is not directed at children. You must be at least 13 years old to create an account or use Fern. If you believe a child under 13 has created an account, contact [stevenuocaster@gmail.com](mailto:stevenuocaster@gmail.com) and we will delete it.

## Changes to this policy

If this policy changes, we will update the "Last updated" date above and add a note to the release notes on the Fern releases page on GitHub.

## Contact

[stevenuocaster@gmail.com](mailto:stevenuocaster@gmail.com)

Steven Caster, operator of Fern. Governing law is stated in the [Terms of Service](../terms/).

[Home](../) | [Terms of Service](../terms/)
