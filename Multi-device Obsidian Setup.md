Tags: #obsidian #knowledge-graph #utilities #macos 

Overview on setting up Obsidian on multiple devices such that there is a single source of truth, and one or more (implicitly) read-only viewers.  

For example, where a laptop populates an Obsidian Vault and then synchronizes it to iCloud so that an iOS device sees the same content.  Since the synchronization is one-way (from laptop to iCloud) the iOS device can only read the content from the source of truth - local changes remain local (and possibly overwritten during iCloud synchronization).

# Source of Truth - Laptop
[[Configuring Obsidian|Configure]] [[Obsidian]] as desired.

# Read-only Clients - iOS Devices
[Install Obsidian](https://apps.apple.com/us/app/obsidian-connected-notes/id1557175442) (provided by Dynalist Inc.) from the App Store.

Create a new vault synchronized via iCloud:
- Create new vault
- Enter the `vault` name
- Enable "Store in iCloud"
- Hit "Create"

The vault is empty and will remain so until [[#Synchronize from the Source of Truth|synchronized]] with the source of truth.

Repeat the above steps for each vault.

# Synchronize from the Source of Truth
Setup a `cron` job that synchronizes the vault contents to iCloud on a regular schedule (e.g. once a minute)

On MacOS, Obsidian's iCloud documents are stored beneath `~/Library/Mobile Documents/iCloud~md~obsidian/Documents/<vault>`.

Manual synchronization can be performed via `rsync`:
```shell
# NOTE: be careful to use the trailing slashes in the command!
$ rsync -avz /path/to/source/of/truth/<vault>/ "~/Library/Mobile Documents/iCloud~md~obsidian/Documents/<vault>/"
```

Verify the vault is visible on the client.  Relaunch the application if the contents don't show up.

## Synchronization with cron
Use `cron` to synchronize the laptop's Vault to iCloud, which then synchronizes to the mobile device.

Edit your crontab with `crontab -e` . To synchronize once a minute, forever, add one entry per vault like so:
```
* * * * * rsync -avz /path/to/source/of/truth/<vault>/ "~/Library/Mobile Documents/iCloud~md~obsidian/Documents/<vault>/"
```

Adjust the five asterisks to whichever time specific is desired.  See [`crontab(5)`](rsync -avz /path/to/source/of/truth/<vault>/ ~/Library/Mobile Documents/iCloud~md~obsidian/Documents/<vault>/) for details.