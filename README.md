# Hierarchy Bookmarks

A Unity Editor tool for bookmarking GameObjects, per scene.

- **Alt+Click** an object in the Hierarchy to toggle its bookmark (a marker icon is drawn on bookmarked rows).
- **GameObject > Toggle Hierarchy Bookmark** does the same for the current selection.
- **Tools > Hierarchy Bookmarks** opens a window listing the active scene's bookmarks in a reorderable list, with an optional *Show Hierarchy Paths* toggle.
- Bookmark changes are undoable.

Bookmarks are stored in `EditorPrefs` on the machine you are using. They are **not** part of this repository and do not travel with a clone.

The script contains version-gated code paths (`#if UNITY_2021_2_OR_NEWER`, `UNITY_6000_3_OR_NEWER`, `UNITY_6000_6_OR_NEWER`) so a single file covers the old IMGUI Hierarchy and the new UI Toolkit based one. `package.json` declares Unity 2021.3 as the minimum.

## Install

### Package Manager (for using the tool)

*Window > Package Manager > + > Install package from git URL…*

```
https://github.com/jdmcgraw/HierarchyBookmarks.git
```

Package Manager can check this URL for newer commits and offer an **Update**. To stay on a fixed release instead, append a git tag or commit hash: `https://github.com/jdmcgraw/HierarchyBookmarks.git#<tag>`. The code is installed into `Library/PackageCache` and cannot be edited there.

### Editable clone (for changing the tool)

From the Unity project root:

```bash
git clone https://github.com/jdmcgraw/HierarchyBookmarks.git Packages/com.jdmcgraw.hierarchybookmarks
```

Unity treats anything in `Packages/` as an embedded package, so no `manifest.json` edit is needed. Edit in place, then commit and push from that folder; run `git pull` in the clones in your other projects. If the host project is itself a git repo, add the folder to its `.gitignore` or use a submodule.

## Layout

```
package.json                 UPM manifest
Editor/
  HierarchyBookmarks.cs      the whole tool (editor-only: lives under an `Editor` folder)
```

Every file and folder has a committed `.meta`. Keep it that way: Unity ignores files without a `.meta` inside packages installed from git, and a stable GUID keeps the script's identity the same in every project.

## License

MIT. See [LICENSE](LICENSE).
