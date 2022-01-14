Tags: #obsidian #tools #cheatsheet #macos #user-configuration 

**NOTE:** This is MacOS-specific, though presumably the command key can be replaced with control for other systems.

# Important Shortcuts

Notes:
- New note: ⌘-n
- Open note: ⌘-o

Navigation:
- Go back: ⌘-⌥-left arrow
- Go forward: ⌘-⌥-right arrow
- Graph view: ⌘-g

Searching:
- Search current file (⌘-f)
- Search all files (⌘-Shift-f)

Focus:
- Focus on editor (⌘-Shift-e)
- Toggle sidebar (⌘-Shift-b) \[CUSTOM\]
- Focus on the pane... (match Vim keybindings)
    - Above (⌘-Shift-k) \[CUSTOM\]
    - Below (⌘-Shift-j) \[CUSTOM\]
    - Left (⌘-Shift-l) \[CUSTOM\]
    - Right (⌘-Shift-h) \[CUSTOM\]

Pane manipulation:
- Close active pane (⌘-w)
- Close other panes (⌘-Shift-w) \[CUSTOM\]
- Split panes horizontally (⌘-Shift-s) \[CUSTOM\]
- Split panes vertically (⌘-Shift-|) \[CUSTOM\]

# Configuration
Obsidian stores hotkey configuration within the `.obsidian/hotkeys.json` file in each Vault.  The following patch configures the hotkeys listed as "\[CUSTOM\]" above:

```shell
diff -u -r .obsidian-prekeys/hotkeys.json .obsidian/hotkeys.json
--- .obsidian-prekeys/hotkeys.json	2022-01-03 10:10:22.000000000 -0500
+++ .obsidian/hotkeys.json	2022-01-03 10:11:36.000000000 -0500
@@ -1 +1,74 @@
-{}
\ No newline at end of file
+{
+  "app:toggle-left-sidebar": [
+    {
+      "modifiers": [
+        "Mod",
+        "Shift"
+      ],
+      "key": "B"
+    }
+  ],
+  "editor:focus-top": [
+    {
+      "modifiers": [
+        "Mod",
+        "Shift"
+      ],
+      "key": "K"
+    }
+  ],
+  "editor:focus-bottom": [
+    {
+      "modifiers": [
+        "Mod",
+        "Shift"
+      ],
+      "key": "J"
+    }
+  ],
+  "editor:focus-left": [
+    {
+      "modifiers": [
+        "Mod",
+        "Shift"
+      ],
+      "key": "L"
+    }
+  ],
+  "editor:focus-right": [
+    {
+      "modifiers": [
+        "Mod",
+        "Shift"
+      ],
+      "key": "H"
+    }
+  ],
+  "workspace:close-others": [
+    {
+      "modifiers": [
+        "Mod",
+        "Shift"
+      ],
+      "key": "W"
+    }
+  ],
+  "workspace:split-horizontal": [
+    {
+      "modifiers": [
+        "Mod",
+        "Shift"
+      ],
+      "key": "S"
+    }
+  ],
+  "workspace:split-vertical": [
+    {
+      "modifiers": [
+        "Mod",
+        "Shift"
+      ],
+      "key": "\\"
+    }
+  ]
+}
```