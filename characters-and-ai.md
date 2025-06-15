---
title: Characters and AI
description: 
published: true
date: 2025-06-14T12:21:50.480Z
tags: characters, ai
editor: markdown
dateCreated: 2025-05-10T14:57:41.376Z
---

This section delves into the mechanical attributes of the game's characters, as well as the design of NPCs and their AI behaviors.

# **Main Characters**

## **Leo**
**Gameplay Role**
- Primary focus on stealth mechanics and physical interaction with the environment.
- Can crouch, climb, vault over obstacles, and use cover to avoid detection.
- Equipped with basic tools like a lockpick, throwable distractions (e.g., coins), and a stun device for incapacitating guards.

**Animations**
- Fluid, parkour-inspired movements for climbing and sneaking.
- Tense idle animations when hiding or observing enemies.
- Quick and reactive animations during chases or combat scenarios.

---

## **Vinny**
**Gameplay Role**
- Operates as the team's hacker, controlling a digital avatar within the mainframe-like 2D environment.
- Navigates the 2D circuit-like layout to access "nodes" representing cameras, unlock "gates" (doors), disable "alarm modules," and gather intel on enemy positions.
- Provides critical support to Leo by manipulating the digital world in real-time, directly influencing the 3D environment's systems and flow.

**Animations**
- Features agile movements appropriate for a 2D digital avatar, such as quick zips along data pathways, "phasing" through certain obstacles, and distinct animations for interacting with digital nodes (e.g., a glow or particle effect when a hack is successful).
- Animations emphasize his digital presence and direct interaction with the abstract mainframe elements.

---

# **Non-Playable Characters (NPCs)**

## **Security Guards**
**Physical Description**
- Varied physiques, but all wear professional high-tech uniforms, including helmets and visors with integrated HUDs.
- Their gear includes utility belts, flashlights, and tasers.

**AI Behavior**
- Patrol set paths but can dynamically adjust based on player actions (e.g., noises, footprints, or suspicious objects).
- Collaborative behavior when investigating, with guards calling for backup or spreading out to search.
- Alert states:
    - **Normal:** Patrolling.
    - **Suspicious:** Investigating noise or movement.
    - **Alert:** Actively pursuing Leo.

**Animations**
- Realistic walking and searching motions.
- Reactive animations for spotting the player, using communication devices, or drawing weapons.

---

## **Neotech Employees**
**Physical Description**
- Formal attire that reflects their roles, from lab coats to suits.
- Some may carry personal items like ID badges, tablets, or coffee mugs.

**AI Behavior**
- Passive NPCs who react to unusual activity but are not actively hostile.
- May alert guards if they notice suspicious activity.

**Animations**
- Idle behaviors like typing, talking, or walking between rooms.

---

## **Digital Defense Systems (2D Enemies for Vinny)**
**Physical Description**
- Appear as abstract, geometric shapes or entities composed of glowing lines, pixels, and circuit patterns, reflecting their function. Examples include:
    - **"Watchdog" Programs:** Small, fast-moving, orb-like entities that patrol data streams.
    - **"Firewall Guardians":** Larger, block-like entities that serve as mobile barriers, often with pulsating energy.
    - **"Glitch Sprites":** Erratic, visually distorted entities that disrupt Vinny's movement or interface.

**AI Behavior**
- **Patrol Routes:** Digital enemies follow predefined paths within the circuit layout.
- **Detection:** They have a "digital line-of-sight" or "data footprint" detection, triggering alerts if Vinny's avatar enters their area.
- **Interruption:** Upon detection, they may attempt to slow Vinny, drain his "data integrity" (a health/resource mechanic), or trigger sub-routines that alert other systems.
- **Adaptive Patterns:** More advanced digital enemies might adapt their patrol patterns based on Vinny's common routes or successful hacks.
- **Response Protocols:** When alerted, they might call in other digital threats or increase the complexity of nearby interactive nodes.

**Animations**
- Smooth, synthetic movements for patrolling entities.
- Quick, sharp visual distortions or "pixel bursts" when detecting Vinny.
- Unique visual effects for attacking or disrupting Vinny's avatar, such as a temporary scramble effect or a draining animation.
- Transformation animations for more complex entities that might change their form based on their alert state.

---

# **Environment-Specific NPCs**

## **Café Customers**
- Relaxed attire, reflecting a casual atmosphere.
- Idle animations include sipping coffee, chatting, or reading.

## **Warehouse Workers**
- Work uniforms with protective gear like gloves and helmets.
- Perform routine tasks like moving crates or operating forklifts.

## **Neotech Specialists**
- Appear in high-security zones with more advanced attire, including lab coats or augmented reality glasses.
- Engage in technical tasks or monitor security systems.

---

# **AI Behavior Design**

## **Awareness System**
- AI reacts to sound, line-of-sight, and environmental triggers (for 3D Operative).
- Digital AI reacts to Vinny's digital presence, data signatures, and interactions within the mainframe (for 2D Oracle).
- Guards have cone-shaped vision fields that can be altered based on environmental lighting.

## **Cooperation**
- Guards work together, communicating via radios to strategize and flank the player.
- In high-security areas, guards may deploy drones or other automated systems.
- Digital defense systems can alert each other and coordinate to shut down compromised network segments or trap Vinny.

## **Player-Induced Suspicion (Vinny's Actions)**
- Excessive or repetitive use of Vinny's digital distractions (e.g., flickering lights, triggering minor alarms, manipulating environmental elements in rapid succession) within a single mission will gradually increase the suspicion level of nearby NPCs. If suspicion becomes too high, it could lead to guards actively investigating the source or initiating a lockdown.

## **Persistent Alertness**
- If Leo is detected and escapes, enemies in the affected area will remain in an **Alert** state. While they will cease active pursuit after a period of no detection, their patrol patterns might become more erratic or focused on the last known location. Leo can still re-engage stealth, but the increased alertness makes subsequent detection more likely and consequences more severe.


---

# **Character and AI Animation Techniques**

## **Blending and Layering**
- Smooth transitions between stealth, idle, and action animations for fluid gameplay (for 3D Operative).
- Seamless digital transitions and reactive effects for Vinny's avatar and 2D enemies.

## **Dynamic Reactions**
- Contextual animations, such as a guard checking a noise or reacting to a disabled camera.
- Digital enemies will have contextual reactions to Vinny's hacks or evasions, such as "rebuilding" animations for firewalls or "error" visual effects.

## **Attention to Detail**
- Subtle environmental interactions, such as a guard leaning on a desk or an NPC checking their watch, to make the world feel alive.
