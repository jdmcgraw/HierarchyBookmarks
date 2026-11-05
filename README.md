# Hierarchy Bookmarks

A Unity Editor tool for bookmarking GameObjects, per scene.

- **Alt+Click** an object in the Hierarchy to toggle its bookmark (a marker icon is drawn on bookmarked rows).
- **GameObject > Toggle Hierarchy Bookmark** does the same for the current selection.
- **Tools > Hierarchy Bookmarks** opens a window listing the active scene's bookmarks in a reorderable list, with an optional *Show Hierarchy Paths* toggle.
- Bookmark changes are undoable.

Bookmarks are stored in `EditorPrefs` on the machine you are using. They are **not** part of this repository and do not travel with a clone.

The script contains version-gated code paths (`#if UNITY_2021_2_OR_NEWER`, `UNITY_6000_3_OR_NEWER`, `UNITY_6000_6_OR_NEWER`) so a single file covers the old IMGUI Hierarchy and the new UI Toolkit based one. `package.json` declares Unity 2021.3 as the minimum.

## Layout

```
package.json                 UPM manifest
Editor/
  HierarchyBookmarks.cs      the whole tool (editor-only: lives under an `Editor` folder)
```

Every file and folder has a committed `.meta`. Keep it that way: Unity ignores files without a `.meta` inside packages installed from git, and a stable GUID keeps the script's identity the same in every project.

## Use it in a project

### Option A: editable clone in `Packages/` (use this when you want to change the tool)

From the Unity project root:

```bash
git clone https://github.com/jdmcgraw/HierarchyBookmarks.git Packages/com.jdmcgraw.hierarchybookmarks
```

Unity picks up anything in `Packages/` as an embedded package, so no `manifest.json` edit is needed. If the host project is itself a git repo, either add `Packages/com.jdmcgraw.hierarchybookmarks/` to its `.gitignore` or add it as a submodule instead of cloning.

### Option B: read-only dependency via Package Manager

*Window > Package Manager > + > Install package from git URL…*

```
https://github.com/jdmcgraw/HierarchyBookmarks.git
```

The code is installed into `Library/PackageCache` and cannot be edited there. Because this repository is private, the machine must have git credentials that work non-interactively (e.g. Git Credential Manager already signed in).

## Syncing changes

Edit the tool in whichever project you are in, then:

```bash
cd Packages/com.jdmcgraw.hierarchybookmarks
git add -A
git commit -m "Describe the change"
git push
```

In every other project that has an Option A clone: `git pull` inside that folder. Projects using Option B update from Package Manager.
