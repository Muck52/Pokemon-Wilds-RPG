# Editing maps with Porymap (Windows, beginner guide)

Porymap is a free click-and-drag map editor built for this kind of project.
You edit maps on your PC, send the changes to GitHub, and Claude rebuilds
the ROM (`release/pokemon-wilds.gba`) in a cloud session.

You do **not** need WSL, a compiler, or the command line for this.

---

## One-time setup (about 15 minutes)

### 1. Install GitHub Desktop
1. Download it from <https://desktop.github.com> and install it.
2. Sign in with your GitHub account (the one that owns `Muck52/Pokemon-Wilds-RPG`).

### 2. Download (clone) the project to your PC
1. In GitHub Desktop: **File → Clone repository…**
2. Pick **Muck52/Pokemon-Wilds-RPG** from the list.
3. For **Local path**, choose a short folder that is **not** inside OneDrive,
   for example `C:\romhack\Pokemon-Wilds-RPG`.
   (OneDrive syncing can lock files and corrupt saves.)
4. Click **Clone**. It's a large project, so this can take a few minutes.

### 3. Switch to the working branch
At the top of GitHub Desktop, click **Current branch** and choose
**build-setup**. This is the branch where your ROM lives.

### 4. Install Porymap
1. Go to <https://github.com/huderlem/porymap/releases>.
2. Under the newest release, open **Assets** and download the **Windows**
   `.zip` file.
3. Unzip it somewhere permanent (e.g. `C:\romhack\porymap`).
4. Double-click `porymap.exe`. If Windows SmartScreen warns you, click
   **More info → Run anyway**.

### 5. Open the project in Porymap
1. **File → Open Project…** and select your project folder
   (`C:\romhack\Pokemon-Wilds-RPG`).
2. If Porymap asks which base game the project uses, choose **pokeemerald**.
3. The map list on the left now shows every map in the game (about 900).
   A good one to start with is **LittlerootTown**, the first town.

---

## Using Porymap

The tabs at the top of the editor each do one job:

| Tab | What you do there |
|---|---|
| **Map** | Paint the ground: grass, trees, water, houses, paths. Click a tile in the palette on the right, then click or drag on the map. Right-click on the map to copy an existing tile. |
| **Events** | Place and drag **things**: people/NPCs, item balls, signs, warps (doors), and triggers. Drag an existing one to move it. Use the **+** button to add a new one, then pick its sprite in the panel on the right. |
| **Header** | Map music, weather, whether you can bike or run. |
| **Connections** | Which maps join at the edges (e.g. Littleroot → Route 101). |
| **Wild Pokémon** | Which Pokémon appear in the grass/water and how often. |

**Save often:** **File → Save All** (Ctrl+S).

Tips:
- Undo is **Ctrl+Z**.
- Duplicating an NPC (select it, then Ctrl+D or the duplicate button) is the
  easiest way to make "copies" of something already on the map.
- What a person *says or does* is set by their **Script** field in the
  Events tab. Ask Claude to write or change those scripts for you.

---

## Sending your changes so Claude can rebuild the ROM

1. **Before you start editing each time:** in GitHub Desktop click
   **Fetch origin**, then **Pull origin** if it appears. This picks up the
   latest ROM and any changes Claude made.
2. Edit and save in Porymap.
3. Back in GitHub Desktop you'll see your changed files listed on the left.
   Type a short summary at the bottom left (e.g. "Add NPCs to Littleroot")
   and click **Commit to build-setup**.
4. Click **Push origin**.
5. In a Claude Code session, say something like:
   *"I pushed map changes to build-setup. Please rebuild the ROM."*
6. When Claude has pushed the new ROM, **Fetch/Pull** in GitHub Desktop.
   The new `release\pokemon-wilds.gba` is in your project folder, ready
   for mGBA.

---

## If something goes wrong

- **Porymap shows an error opening the project:** make sure you picked the
  top project folder (the one that contains `Makefile` and the `data`
  folder), and that you're on the `build-setup` branch.
- **GitHub Desktop says there's a conflict:** don't try to fix it by hand.
  Tell Claude what the message says.
- **You broke a map and want to undo everything since your last commit:**
  in GitHub Desktop, right-click the changed file → **Discard changes**.
