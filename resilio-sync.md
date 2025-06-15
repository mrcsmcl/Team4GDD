---
title: Resilio Sync Info
description: 
published: true
date: 2025-06-14T16:09:03.895Z
tags: resilio, sync, share
editor: markdown
dateCreated: 2025-05-10T15:13:21.835Z
---

Resilio Sync is a **peer‑to‑peer** (P2P) file synchronization tool that leverages your own devices to share folders directly, **no central cloud storage involved**. It’s ideal for game development teams because it:

- **Maximizes speed**: Direct LAN transfers can saturate your local network.  
- **Ensures privacy**: All data is encrypted end‑to‑end (AES‑128) before it leaves your machine.  
- **Scales seamlessly**: Add new peers (artists, developers, build servers) with a single share key.  
- **Handles large files**: Perfect for multi‑gigabyte PSDs, 3ds Max scenes, WAV multitracks and video edits.

# How Resilio Sync Works Under the Hood  
1. **Folder Keys & Links**  
   - Each synced folder is identified by a unique 33‑character “secret” or “link.”  
   - Peers paste this secret into their Resilio client to join the share.  

2. **Peer Discovery & Connection**  
   - By default, peers discover each other via LAN broadcast, LAN multicast, and (optionally) through Resilio’s relay/tracker servers if peers aren’t on the same network.

3. **Encrypted Transfer**  
   - All data in transit is encrypted with AES‑128.  
   - Metadata (file names, sizes) can also be encrypted if you choose “Encrypted Folder” mode.

4. **Block‑Level Sync & Versioning**  
   - Files are split into 32 KB blocks; only changed blocks re‑transfer on updates.  
   - Built‑in versioning can keep snapshots of overwritten or deleted files.

5. **Selective Sync & Bandwidth Control**  
   - Each peer can choose which subfolders to keep locally.  
   - You can throttle upload/download speeds per folder to avoid saturating your Internet link.

# Why Use Resilio Sync for Source Assets?  
- **Raw Assets Are Large & Frequently Updated**  
  Source PSDs, MAX/BLEND scenes and DAW sessions change every artist save—resyncing gigabytes of binaries is wasteful.  
- **Separation from Engine Binaries**  
  Keep your compiled `.uasset` and `.umap` traffic on a different channel or CI system.  
- **Offline & Zero‑Trust**  
  No dependency on external cloud—peers can sync over LAN without Internet, and encryption keeps assets safe over public networks.

---

# Folders to Sync (Source‑Editable Only)

| **Folder Path**                           | **Description**                                                   | **Key File Types**                                  | **Sync Secret** |
|-------------------------------------------|-------------------------------------------------------------------|-----------------------------------------------------|-----------------|
| `Documentation`           | Documentations PDF                       | `.pdf`        | [LINK](https://link.resilio.com/#f=Documentation&sz=27E6&t=2&s=TZMDSYGMEM5S56E6J4BDLD4LYRVG54ZRBPEIIVUT342AB4WWWMYQ&i=CXHHP5YLJAGXTC2AKUEPORXI3BEJGLUW6&v=3.0&a=2)      |
| `Art`           | Raw character models, sculpts, concept art, DCC animation files & motion capture data.                       | `.max`, `.blend`, `.fbx`, ZBrush `.ztl`, PSD, Maya `.ma`/`.mb`, `.anim`, Blender `.blend`, FBX        | [LINK](https://link.resilio.com/#f=Art&sz=0&t=2&s=WDSOL2YN4RUMTTMMU3U635UL4JDWN2ICYOGIMWGYC43IVR5ALWAA&i=CCFMOVIZ6VMRS6DLOUHUN2UMHNLQG4AWP&v=3.0&a=3)      |
| `Textures`                        | High‑resolution and layered textures before engine import         | `.psd`, `.exr`, `.tga`, `.png`                      | [LINK](https://link.resilio.com/#f=Textures&sz=0&t=2&s=JHRH5PDV4TD2JOVLUJFIM7QW2AB6TCMMMGKC5XQLA7TDUORQFLDQ&i=CT5BDJ34AKWBKWFKYWRGGSKXBV5BE4D4R&v=3.0&a=3)      |
| `Materials`                | Substance Designer/Alchemist projects and material authoring      | `.sbs`, `.sbsar`, `.sbsprs`, `.substance`           | [LINK](https://link.resilio.com/#f=Materials&sz=0&t=2&s=H5R3G2HJXWXF5YSHPBJOTRORTYXDRHBX6HJNQXTHRYDIZI2DZHDQ&i=CESEWCQWIVPD3VJ5KTJ4AT32PABSWWY3F&v=3.0&a=3)      |
| `FX`                       | Raw effect definitions (text‑based or source files)               | `.json`, `.xml`, HLSL `.hlsl`, `.fx`, custom scripts| [LINK](https://link.resilio.com/#f=FX&sz=0&t=2&s=ZLH6A54YAYOIMVJVZMCM6JBOUSWDC5AVOGKHWFETXN4WVJS3PYEA&i=CRQACV67HJAKJ3V7CTNNCC4F3XDEY3EWN&v=3.0&a=3)      |
| `UI`                       | UI mockups, wireframes, icon masters                              | `.psd`, `.ai`, `.fig`, `.svg`, Sketch `.sketch`     | [LINK](https://link.resilio.com/#f=UI&sz=0&t=2&s=J7XY5FA7DGZKVKGZUJAMVDI4DARTCJTHSU4GYUQWKQ6WBNAUA6FQ&i=CO7HA46RKYF5OAYAQ673YUNKHV3FKWSNV&v=3.0&a=3)      |
| `Audio`                    | Untouched audio recordings & DAW sessions                         | `.wav`, `.aif`, Ableton `.als`, Pro Tools `.ptx`    | [LINK](https://link.resilio.com/#f=Audio&sz=0&t=2&s=XQWPLODHC43PW4OX5UG6YGAYA4DHRYG7PLAKTNXXO4UUOBIAIELA&i=CV6TABLJ2TXOHJL5HQJ2DOITOHH64URTD&v=3.0&a=3)      |
| `Video`                    | Original footage & edit project files                             | `.mov`, `.mp4`, Premiere `.prproj`, DaVinci `.drp`  | [LINK](https://link.resilio.com/#f=Video&sz=0&t=2&s=WRGRBM2MVET45UNPLCDJ7HWKJUAXXGJ7JODXSXPAZVYUNJMZKHIQ&i=CLFXNTUI4G5FLZBZLUYAFUALTOU4TMZPZ&v=3.0&a=3)      |
| `_External`                       | Third‑party packs (Quixel, ZBrush, Marketplace downloads)         | `.zip`, `.rar`, raw archives, vendor DCC files      | [LINK](https://link.resilio.com/#f=_External&sz=0&t=2&s=W4O262E6ERBCP5ODPKTXHQ72VCDK345CFXORTL6R5WADFFZUSNSA&i=CNGQG2HPQS2OBUWPYCIJSKG44ROVERWD3&v=3.0&a=3)      |
| `Developers/[YourName]`           | Personal WIPs for each artist/tech‑artist                         | Any source file (`.psd`, `.max`, `.ma`, `.nk`, etc.)| [LINK](https://link.resilio.com/#f=Developers&sz=0&t=2&s=BEK3F3623OTT3WLYFND6D6BFTMQYNZN4P73MQPVBKUKJ2C5JMV6A&i=CPISB73EVZNVAHYZEK6BE6BCQEX47YVBS&v=3.0&a=3)      |

<br>

> **Note:** Do **not** include compiled Unreal assets (`.uasset`, `.umap`) in this share. Keep those on a separate channel or CI feed.

---

# Step‑by‑Step Setup

1. **Install Resilio Sync**  
   - Download for Windows/macOS/Linux at:  
     ```
     https://www.resilio.com/sync/
     ```

2. **Create the Root Share**  
   - Open Resilio Sync → **Add → Standard Folder**.  
   - Point to your desired `Content/` directory.

<br>

> Do not use the game project folder.
{.is-warning}


3. **Add Each Source Subfolder**  
   - In Resilio, right‑click your `Content/` share → **Enter a key or link**.  
   - Paste the corresponding **Sync Secret** for `Art/Characters`, then repeat for the others as you need.
   - Confirm the **local path** matches exactly (case‑sensitive).

4. **Configure Selective Sync (Optional)**  
   - In the folder’s **Preferences → Selective Sync**, uncheck subfolders you don’t need on a particular machine (e.g., animators may skip UI/Video).

5. **Set Bandwidth Limits (Optional)**  
   - In **Preferences → Bandwidth**, throttle upload/download speeds if you share over Internet links to avoid saturating your pipe.

6. **Verify & Collaborate**  
   - Once peers join, Resilio Sync will transfer all source files.  
   - Artists save a new PSD, and only the changed file blocks propagate, keeping sync lean.

---

# Best Practices & Troubleshooting

- **Keep Secrets Confidential**  
  Only share folder secrets with authorized team members.  
- **Backup the `.sync` Folder**  
  Periodically copy your Resilio client’s `.sync` folder (peer list, history database) along with your project backups.  
- **Check Peer Status**  
  In the Resilio UI, verify peers are **‘Up to date’** or **‘Syncing’**. Red exclamation marks can indicate path mismatches.  
- **Resolve Conflicts**  
  If two peers edit the same file simultaneously, Resilio creates conflict copies (e.g. `filename (device).psd`). Merge these manually and remove the outdated copy.  

