---
title: Unreal Engine File Organization and Naming Guide
description: 
published: true
date: 2025-09-13T17:24:48.571Z
tags: files, organization, unreal engine
editor: markdown
dateCreated: 2025-05-10T15:11:31.338Z
---

A structured and consistent file organization is the backbone of any successful Unreal Engine project. A well-defined system accelerates development, eases the onboarding of new members, minimizes conflicts, and drastically reduces confusion and redundant work.

This document establishes a detailed guide for the folder structure, naming conventions, and workflow to be adopted, utilizing **Git** for project version control and **Resilio Sync** for source file storage.

---

# **1. Core Principles**

Our organizational philosophy is based on three pillars:

1.  **Clarity of Location:** A file's location should immediately indicate its purpose and type.
2.  **Consistency is Key:** The rules must be followed by everyone, at all times.
3.  **Descriptive Naming:** A file's name should concisely describe what it is and how it is used.

---

# **2. Tools and Project Ecosystem**

Our ecosystem is divided into two main parts, each with a specific tool:

## **A. Git (Project Version Control)**

**Git** will be used to version our Unreal Engine project. This includes all `.uproject`, `.uasset`, `Config/`, and `Source/` files.

* **Git LFS (Large File Storage) is Mandatory:**

Since Git does not handle large binary files well (like most `.uasset` files), the use of Git LFS is **required**. It stores large files on a separate server, keeping the main repository lightweight and fast.

* **`.gitattributes` Configuration:**

A `.gitattributes` file in the project root must be configured to tell LFS which file types to track.

**Example `.gitattributes` file:**

Unreal Engine Assets
```
*.uasset filter=lfs diff=lfs merge=lfs -text
*.umap filter=lfs diff=lfs merge=lfs -text
*.ubulk filter=lfs diff=lfs merge=lfs -text
*.ushader filter=lfs diff=lfs merge=lfs -text
```

Other large files
```
*.fbx filter=lfs diff=lfs merge=lfs -text
*.png filter=lfs diff=lfs merge=lfs -text
*.wav filter=lfs diff=lfs merge=lfs -text
*.mp3 filter=lfs diff=lfs merge=lfs -text
```

<br> 

## **B. Resilio Sync (Source File Repository)**

**[Resilio Sync](/resilio-sync)** will be used for a shared folder containing all **work-in-progress and source files**. These are the files *before* they are imported into Unreal Engine.

* **Purpose:** To keep the Git repository clean by storing only game-ready assets (`.uasset`). Source files (`.blend`, `.psd`, `.spp`, `.zpr`, high-quality audio files, etc.) are heavy and do not need to be versioned along with the project.
* **Suggested Structure:** The folder structure in Resilio Sync should mirror the project's `Content/` folder structure to maintain consistency.

**Example structure in Resilio Sync:**
* `ResilioSync_MainFolder/`
    * `Art_Source/`
        * `Characters/`
            * `Player/` (Contains: `Player.blend`, `Player_Textures.spp`, etc.)
            * `Enemies/`
                * `Grunt/` (Contains: `Grunt.zpr`, `Grunt_Bake.fbx`, etc.)
        * `Environments/`
            * `Props/`
                * `Furniture/` (Contains: `Chair_Dining_A.fbx`, `Chair_Textures/`, etc.)
    * `Audio_Source/`
        * `Music/` (Contains Reaper/FL Studio projects, etc.)
        * `SFX/` (Contains original `.wav` recordings)
    * `Design_Docs/` (Game Design Documents, scripts)

---

# **3. Folder Structure (Content Browser)**

All asset organization will take place within the main `Content/` folder.

* `Content/`
    * `_ProjectName/` (e.g., `_OurAwesomeGame/`) – Core game systems
        * `Core/` – GameMode, PlayerController, GameInstance, GameState, etc.
        * `Data/` – Data Tables, Enums, Structs, Data Assets (e.g., item data, enemy stats)
        * `Input/` – Input Actions, Input Mapping Contexts
        * `Interfaces/` – Blueprint Interfaces (BPIs)
        * `SaveGames/` – Save Game Blueprints
        * `UI_Framework/` – Core UI widgets, HUD, base UI classes
    * `Art/` – Visual assets
        * `Characters/` – Player characters, NPCs, enemies, and their related assets
            * `[CharacterName]/` – Meshes, Materials, Textures, Skeletons, Physics Assets
        * `Animations/` – Shared animations, Animation Blueprints (ABPs)
        * `Environments/` – Props, modular pieces, landscapes, foliage
            * `Props/` – Categorized (e.g., `Furniture/`, `Interactive/`, `Static/`)
            * `Modular/` – Building blocks (walls, floors, etc.)
            * `Foliage/` – Trees, bushes, grass
            * `Landscape/` – Landscape materials, layers
        * `FX/` – Visual effects (Niagara, Cascade)
            * `Particles/` – Niagara Systems (NS), Emitters (NE)
            * `Decals/` – Decal materials
            * `Materials/` – Generic materials and functions
                * `MasterMaterials/` – Base materials
                * `MaterialFunctions/` – Material functions (MF)
                * `Instances/` – Material Instances (MI) organized by type
            * `Textures/` – Generic textures, utility textures (masks, noises)
        * `UI/` – UI specific textures, fonts, widgets
            * `Widgets/` – Specific WBP classes
            * `Icons/` – UI icons
            * `Fonts/` – Font assets
    * `Audio/` – Sound assets
        * `Music/` – Background music, ambience music
        * `SFX/` – Sound effects (weapons, footsteps, UI, environmental)
        * `Voice/` – Character voice lines, dialogues
        * `Cues/` – Sound Cues (SC) for more complex audio
        * `Mixes/` – Sound Mixes, Attenuation, Concurrency settings
    * `Blueprints/` – Game logic (non-core)
        * `Gameplay/` – Interactables, pickups, enemies specific logic, game mechanics
        * `Components/` – Reusable Blueprint Components
        * `Items/` – Item definitions, inventory system related BPs
        * `Weapons/` – Weapon BPs
        * `Traps/` – Trap BPs
    * `Levels/` – Maps
        * `Production/` – Main game levels (e.g., `L_Village_Day`, `L_Dungeon_01`)
        * `Test/` – Levels for testing specific mechanics or assets
        * `Shared/` – Sublevels that are shared with all the other levels (e.g., UI)
        * `Showcase/` – Levels for demonstrations or promotional content
        * `Persistent/` – Persistent level if using world composition
    * `Developers/` – Personal work folders
        * `[YourName]/` – For individual work in progress
    * `_External/` – For assets imported from external marketplaces or specific plugins that might not fit neatly into other categories, or for temporary external content.


---

# **4. Naming Conventions**

Asset naming will follow the format: **`Prefix_BaseName_Variant_Suffix`**.

## **Asset Prefix Table**

| Asset Type | Prefix | Example |
| :--- | :--- | :--- |
| **Blueprint Class** | `BP_` | `BP_PlayerCharacter` |
| **Widget Blueprint** | `WBP_` | `WBP_MainMenu` |
| **Static Mesh** | `SM_` | `SM_Rock_A` |
| **Skeletal Mesh** | `SK_` | `SK_Human_Male` |
| **Animation Blueprint** | `ABP_` | `ABP_PlayerCharacter` |
| **Animation Sequence** | `A_` | `A_Human_Walk_Fwd` |
| **Material** | `M_` | `M_Metal_Steel` |
| **Material Instance** | `MI_` | `MI_Metal_Steel_Rusted` |
| **Material Function** | `MF_` | `MF_ColorTint` |
| **Texture** | `T_` | `T_Wood_Oak_D` |
| **Sound Wave** | `S_` | `S_Explosion_01` |
| **Sound Cue** | `SC_` | `SC_Explosion_Large` |
| **Niagara System** | `NS_` | `NS_Sparks_Impact` |
| **Niagara Emitter** | `NE_` | `NE_Sparks` |
| **Level (Map)** | `L_` | `L_Jungle_Temple` |
| **Data Table** | `DT_` | `DT_WeaponStats` |
| **Enum** | `E_` | `E_WeaponType` |
| **Struct** | `ST_` | `ST_PlayerInfo` |
| **Blueprint Interface** | `BPI_` | `BPI_Interactable` |

<br>

## **Texture Suffixes**

* `_BC`: Base Color
* `_D`: Diffuse / Albedo
* `_N`: Normal Map
* `_ORM`: Mask (usually Ambient Occlusion, Roughness, Metallic)
* `_E`: Emissive
* `_H`: Height / Displacement

---

# **5. Workflow with Git and Resilio Sync**

This is the step-by-step workflow, from source asset creation to its implementation in the game.

**Scenario:** An artist needs to create a new chair for the game.

1.  **Source File Creation:** The artist creates the chair in their 3D software (Blender, Maya). The work file (e.g., `Chair_Modern.blend`) is saved in the appropriate **Resilio Sync** folder (e.g., `Art_Source/Environments/Props/Furniture/`).
2.  **Export:** The model is exported in an engine-compatible format (e.g., `.fbx`).
3.  **Import into Unreal Engine:** The artist opens the Unreal project and imports the `.fbx` into their personal work folder: `Content/Developers/[YourName]/`.
4.  **Asset Development:** Inside their developer folder, the artist creates Materials (`MI_`), adjusts the model (`SM_`), and assembles a Blueprint (`BP_`), if necessary.
5.  **Testing and Validation:** The asset is tested in a test map to ensure it works as expected.
6.  **Migration and Cleanup:** Once the asset is finalized and approved, it is moved from the `Developers/[YourName]/` folder to its final location. After moving, run **"Fix Up Redirectors in Folder"** on the `Content` folder to clean up redirectors.
7.  **Commit to Git:** The artist now "commits" the new `.uasset` files to the Git repository. The commit message should be clear (e.g., "Added SM_Chair_Modern and corresponding materials").

<br>

> Remember, anything inside your `Developers/[YourName]/` folder won’t be synced to GitHub when you push.
{.is-danger}



<br> 

## **The Golden Rule of Git for Unreal Engine:**


> **COMMUNICATE BEFORE YOU WORK.** 
{.is-warning}


Git does not "lock" files like Perforce. If two people edit the same binary file (especially **Levels** and **complex Blueprints**) at the same time, the merge will be impossible, and someone's work will be lost. **Always communicate to the team which Level or major Blueprint you are working on.**

---

# **6. Maintenance and Best Practices**

* **Fix Up Redirectors:** Clean up redirectors regularly, especially after moving or renaming files, by right-clicking the `Content` folder and selecting the option.
* **Regular Cleanup:** At the end of each sprint, the team should dedicate time to audit the project folders, delete unused assets, and ensure conventions are being followed.


# 7. Utilizing Sublevels for Level Organization

In Unreal Engine projects, especially in large and complex environments, the use of **Sublevels** is an essential practice for improving performance, optimizing workflow, and allowing multiple team members to work simultaneously on different parts of the same level.

## What are Sublevels?

A sublevel is essentially a "level within a level." A main level, known as the **Persistent Level**, can load multiple sublevels. Each sublevel contains a specific set of actors (Static Meshes, Blueprints, Lights, Particle Effects, etc.) which, when loaded, become part of the overall level.

### How do they work?

1. **Loading and Unloading:** Sublevels can be dynamically loaded and unloaded at runtime. This is crucial for performance optimization, as you can load only the parts of the level the player is currently seeing or interacting with, and unload those that are not needed.

2. **Collaboration:** The biggest advantage of sublevels for workflow is the ability for multiple artists, designers, and programmers to work on the same level simultaneously without conflicts. Each team member can focus on a specific sublevel (e.g., an environment artist on `L_HouseModel`, a designer on `L_Blueprints`, and a lighting artist on `L_Lighting`). When saved, only the `.umap` files of the modified sublevels are changed, minimizing merge conflicts in Git.

3. **Organization:** Sublevels allow for a logical and thematic organization of level elements. Instead of having thousands of actors in a single monolithic level, you group them by category (3D assets, gameplay, lighting, etc.), making the level more manageable and easier to navigate.

### Sublevel Workflow

When creating a new level, you'll start with a Persistent Level. Instead of adding all your assets directly to it, you'll create and add sublevels for each category of elements.

1. **Creating the Persistent Level:** Create a new main level (e.g., `L_Village_Day`). This will be the Persistent Level and is where you'll manage the sublevels.

2. **Creating Sublevels:** In the "Levels" panel (Window > Levels), click on "Levels" > "Create New..." to create new sublevels. Save them in the folder `Content/Levels/Production/` within a subfolder corresponding to your main level (e.g., `Content/Levels/Production/Village/`).

3. **Adding Assets to Sublevels:** Make the desired sublevel "Current" (by double-clicking the sublevel name in the "Levels" panel). All assets you add or move to the level will now be placed in that sublevel.

4. **Management:** In the "Levels" panel, you can control the visibility, loading, and locking of each sublevel, making it easier to focus on specific parts of your environment.

## Sublevel Structure for Project Levels

To maintain consistency and clarity, all levels in our project will be divided into specific category sublevels. While the exact structure may vary slightly depending on the level's complexity, the principle of separating elements is fundamental.

Below is a table outlining the sublevel structure. This allows for clear organization and parallel development across different levels.

| Level Name (Persistent)      | Category                    | Sublevel Name Example     | Purpose                                                        |
|------------------------------|-----------------------------|---------------------------|----------------------------------------------------------------|
| `L_House_L1`         | **3D Assets**               | `L_House_Decals`          | Various decals (bullet holes, dirt, graffiti).                |
|                              |                             | `L_House_Furniture`       | Furniture and props inside the house.                         |
|                              |                             | `L_House_Model`           | The main geometry of the house (walls, roof, floor).          |
|                              |                             | `L_House_PrimaryAssets`   | Primary and highly important visual assets not in other categories. |
|                              | **Gameplay**               | `L_House_Blueprints`      | Level-specific Blueprints (triggers, interactive doors, NPCs).|
|                              |                             | `L_House_Cinematics`      | Cinematic sequences and story events.                         |
|                              | **Lighting & Post Processing** | `L_House_Audio`        | Ambient sound cues, level-specific audio cues.                |
|                              |                             | `L_House_Lightning`       | Lights (point, directional, rectangular, etc.), light volumes.|
|                              |                             | `L_House_VFX`             | Visual effects (smoke, dust, environmental particles).        |
|                              | **Miscellaneous**          | `L_House_City`            | Parts of the city or external environment (visible, not playable). |
|                              |                             | `L_House_ScaleReference`  | For scale reference during development only (to be removed).  |

