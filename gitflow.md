---
title: GitFlow Workflow and Pull Request
description: 
published: true
date: 2025-06-14T16:08:14.706Z
tags: organization, gitflow, github
editor: markdown
dateCreated: 2025-05-10T15:12:22.508Z
---

To optimize how we manage our work on GitHub and across any Git repository, we will adopt the **GitFlow Workflow**. This robust and widely recognized branching strategy aims to establish a cohesive development process, minimize integration conflicts, and ensure the traceability and stability of the project. With GitFlow, every contribution has a defined place and purpose, facilitating collaboration and the delivery of high-quality software.

---

# Core Branches (Persistent Branches)

GitFlow is built upon the existence of two primary, persistent branches in your repository. Think of them as the "lifelines" of your project, each with a clearly defined responsibility:

1.  ### `main`
    * **Purpose:** This branch always represents the **production-ready code**, meaning it's the most stable version ready for release to users.
    * **Content:** It contains only code that has been thoroughly tested, reviewed, and approved. Direct work on this branch is strictly prohibited.
    * **Integrity:** Every commit on this branch should correspond to a release version or an urgent hotfix for production.
    * **Example:** If you have an application, the code in `main` is what your users are currently interacting with.
    

2.  ### `development`
    * **Purpose:** This is the **primary integration branch** for ongoing development. It's where all new functionalities, bug fixes, and other improvements are first gathered and tested.
    * **Content:** Reflects the current state of work in progress, including partially developed features that aren't yet ready for production.
    * **Interaction:** All other work branches are created from `development` and, once completed, are merged back into it.
    * **Example:** It's the "testing ground" where all new parts of your project are assembled and verified before being considered for a release.
    

---

# Work Branch Flow (User Story & Independent Task Branches)

The core of GitFlow for daily development lies in creating and managing short-lived branches. Following this flow ensures a clean, organized repository with a comprehensible history:

## 1. Create a Work Branch

Whenever you start a new task, whether developing a feature, fixing a bug, or implementing an urgent correction, the first step is to create a new branch from the **`development`** branch.

* **Golden Rule:** **Never work directly on the `main` or `development` branches.**
* **Detailed Naming Convention:** The naming of your branches is crucial for organization and traceability. Strictly follow these patterns:

    * **For User Stories (User Story Task):**
        `T4<MilestoneName>-<MMYY>-US<UserStoryNumber>/TK<TaskNumberInHackNPlan>`
        * **Example:** `T4PP-0625-US01/TK02`
            * `T4`: Project/team identification prefix.
            * `PP`: Milestone Name (e.g., "Pre-Production").
            * `0625`: Month (06) and Year (25).
            * `US01`: User Story Number (e.g., "As a user, I want to register to access the system").
            * `TK02`: Corresponding Task Number in HackNPlan (e.g., "Develop registration form").

    * **For Independent Tasks (Non-User Story Tasks):**
        `T4<MilestoneName>-<MMYY>-IDT<IndependentTaskNumber>/<ShortDescription>`
        * **Example:** `T4PP-0625-IDT05/RefactorAuthModule`
            * `T4`: Project/team identification prefix.
            * `PP`: Milestone Name.
            * `0625`: Month and Year.
            * `IDT05`: Independent Task Number (e.g., a task not directly linked to a specific user story in your project management tool).
            * `RefactorAuthModule`: A concise, descriptive short description of the task (e.g., refactoring an authentication module, updating dependencies, improving CI/CD).

    ```bash
    # Example for a User Story Task
    git checkout -b T4PP-0625-US01/TK02 development

    # Example for an Independent Task
    git checkout -b T4PP-0625-IDT05/RefactorAuthModule development
    ```

## 2. Develop and Commit Regularly

With your new work branch active, you can begin developing the feature or fix.

* **Atomic Commits:** Make small, frequent commits, each representing a complete, logical change. This facilitates code review and problem tracking.
* **Clear Commit Messages:** Your commit messages should be concise but descriptive, explaining what was done and why.
    * **Good Example:** `feat: Add email validation to user registration`
    * **Bad Example:** `update`
* **Local Testing:** Before any push, **always test your changes locally** to ensure they don't introduce new issues or break existing functionalities.

## 3. Merge Back into `development` (Pull Request)

Once your feature or fix is complete, locally tested, and ready to be integrated with the team's work, you should prepare it for merging back into the `development` branch. The preferred method for this is via a **Pull Request (PR)**, which initiates our review process.

* **Create a Pull Request:** Go to GitHub (or your chosen Git platform) and create a Pull Request from your work branch to the `development` branch.
* **Move Task to Testing in HackNPlan:** When you create the PR, remember to update the corresponding task in **HackNPlan** by moving its status to the **"Testing"** column. This signals that the task is now awaiting review.

## 4. Pull Request Review Process

Every Pull Request will undergo a thorough review by **two designated reviewers**: the **Area Lead** and the **Team Lead**. This dual review ensures comprehensive quality control and adherence to best practices.

* **Review and Feedback:** Reviewers will examine the code for quality, adherence to coding standards, potential bugs, and overall design. Feedback will be provided directly within the PR comments.

* **Approval and Automatic Merge:** If both the Area Lead and the Team Lead **approve** the Pull Request, it will be **automatically merged** into the `development` branch. Upon a successful merge, the **remote branch will also be automatically deleted** to maintain repository cleanliness. This streamlines the integration process for approved changes and keeps the remote repository tidy.

* **Rejection and Rework:** If the Pull Request receives feedback or is rejected by either reviewer, the following actions will occur:
    * **All Cases (Minor or Major Feedback):** The corresponding task in **HackNPlan** will **always be moved back to the "In Progress"** column. A clear message will be sent to the developer explaining what needs to be fixed or adjusted, detailing the reasons for the change request.
    * **Minor Changes/Feedback (PR Remains Open):** If the requested changes are minor and do not require a significant re-evaluation of the feature (e.g., small code style fixes, minor logical tweaks), the Pull Request will **remain open**. The developer must implement the requested corrections on the **same branch**, push the updates, and the reviewers will then re-evaluate the existing PR. No new PR is required in this scenario.
    * **Major Rework/Rejection (PR is Closed):** If the feedback indicates fundamental issues, a significant redesign, or a complete misunderstanding of requirements (i.e., a full rejection), the Pull Request will be **closed**. The developer must then address the feedback thoroughly on their existing branch. After completing the rework, the developer will need to **submit another Pull Request from the *same branch*** for re-review, restarting the review process from step 3. The branch itself is **not deleted** in this scenario.

---

## 5. Delete the Local Branch

Since the remote branch is automatically deleted upon a successful merge, your final step will be to remove the local copy of your work branch.

* **Maintain Order:** Deleting the local branch keeps your local repository clean and easy to manage, preventing a build-up of old, unnecessary branches.
* **History Preserved:** Deleting the branch **does not mean losing your work**. All your commits and changes are permanently recorded in the history of the `development` branch (and eventually, `main`). You can always revisit the commit history to see what was done.

    ```bash
    # After the merge (remote branch already deleted), from your development branch:
    git branch -d T4PP-0625-US01/TK02 # Deletes the branch locally
    ```

# Why Deleting Branches is Essential

The practice of deleting branches after merging isn't just about aesthetics; it offers significant practical benefits:

* **Reduces Visual Clutter:** A repository with hundreds of inactive branches becomes confusing and difficult to manage. Deletion helps focus on active and relevant branches.
* **Ensures Clarity and Focus:** It ensures that only branches representing work in progress are visible, making it easier for the team to identify where active development is occurring.
* **Performance:** While marginal, a smaller number of branches can positively impact the performance of some Git operations and visualization tools.
* **History Accountability:** It reinforces the idea that the commit history on `development` (and `main`) is the single source of truth for the project's state, not temporary branches.

---

# Benefits of Adopting the GitFlow Workflow

By consistently adopting GitFlow, our team will reap a series of advantages that will positively impact the entire software development lifecycle:

* **Organization and Clarity:** Each team member knows exactly where to start their work (by creating a branch from `development`) and how to integrate it back, resulting in a well-structured and understandable repository.
* **Reduced Conflicts:** The clear separation between development and production branches, and the creation of isolated branches for each task, significantly minimize merge issues and code conflicts.
* **Efficient Releases:** The ability to create stable versions from the `main` branch without interrupting ongoing development in the `development` branch makes the software release process smoother and more predictable.
* **Improved Collaboration:** With a well-defined process, team members can work independently on their tasks, knowing that their contributions will be integrated in an orderly fashion and without surprises.
* **Superior Traceability:** The commit history becomes a clear narrative of the project's development, making it easy to identify when and why certain changes were made, which is invaluable for debugging and auditing.

---

# How to Create a Pull Request (PR)

Creating a Pull Request is the formal way to propose changes and begin the code review process. Your PR should be clear, concise, and provide all necessary information for reviewers.

Once you have pushed your branch to the remote repository (e.g., `git push origin T4PP-0625-US01/TK02` or using your prefered software), navigate to your repository on GitHub (or your Git platform) and follow these steps to open a new Pull Request.

## Pull Request Template Fields:

Fill out the PR description using the following template fields to ensure all relevant information is provided:

### By:
    
* `[yourDiscordName]`
* _Example: By: yourDiscordName

### **Title:**

* A concise and descriptive summary of the PR's purpose. It should clearly state what the PR is about.

* *Example*: Art: Add Goblin mesh & textures (`US10/TK25`).

### **Description:**
* Explain what was done, why, and any relevant context. Reference your HackNPlan task.
    
* Example: This PR adds the final static mesh and initial PBR textures for the new Goblin enemy, completing `Task TK25`. The mesh is optimized for poly count, and textures are at 2K resolution.

Related HackNPlan Task: `[Link to HackNPlan Task TK25]`

### **Changes Made:**
* A list of specific changes, including affected files or assets.

Example (Art):

* `Content/Characters/Enemies/Goblin/SK_Goblin.uasset`: New skeletal mesh for Goblin.
* `Content/Characters/Enemies/Goblin/T_Goblin_Albedo.uasset`: New Albedo texture.
* `Content/Characters/Enemies/Goblin/T_Goblin_Normal.uasset`: New Normal texture.
* `Content/Characters/Enemies/Goblin/T_Goblin_ORM.uasset`: New ORM texture (Occlusion, Roughness, * Metallic).
* `Content/Blueprints/BP_Enemy_Goblin.uasset`: Updated static mesh component to use new SK_Goblin.

Example (Code):
* `Source/YourProject/Public/PlayerCharacter.h`: Added Dash() function declaration.
* `Source/YourProject/Private/PlayerCharacter.cpp`: Implemented dash logic with a short impulse and cooldown.
* `Content/Blueprints/BP_PlayerCharacter.uasset`: Linked dash input action to C++ function.

### **How to Test:**
* Clear, step-by-step instructions for reviewers to test your changes in Unreal Editor.

Example (Art):
1. Navigate to `Content/Blueprints/BP_Enemy_Goblin.uasset` and open it.
2. Verify that the Static Mesh Component uses SK_Goblin and that the materials display correctly with the new textures.
3. Open `Content/Maps/Level_Swamp.umap` and locate the Goblin test area. Verify the new Goblin mesh appears as expected.

Example (Code):
1. Open `Content/Maps/Level_TestBed.umap`.
2. Click "Play In Editor" (PIE).
3. Press the designated Dash key (e.g., 'Q'). Observe the player character performing a quick dash. Verify cooldown works.

### **Additional Notes:**
* Anything else important (known issues, dependencies, performance thoughts). Not mandatory.

Example (Art): Rigging and animation are not included in this PR and will be handled in a separate task. Textures were compressed with default Unreal settings.

Example (Code): Dash currently consumes no stamina. This will be integrated with the stamina system in a future PR (`US12/TK30`). No special plugins needed.

### **Screenshots or GIFs:**
Visuals are very helpful! Include screenshots or short GIFs showing your changes in action within Unreal Editor. Not mandatory.

Example:
`[Screenshot of Goblin mesh in Unreal's Static Mesh Editor]`
`[GIF of player character performing a dash in PIE]`