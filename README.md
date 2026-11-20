# vCheck for macOS

vCheck is an RVTools report analyzer for VMware estates. This repository holds
the releases of its Mac app and nothing else: the installed app reads its
updates from here.

## Installing

1. Download `vCheck-<version>.dmg` from the [latest release](https://github.com/azizo/vcheck-app/releases/latest).
2. Open it and drag vCheck to Applications.
3. Open vCheck and enter your licence key.

## What it needs

- macOS 26 or later, on a Mac with Apple Silicon.
- A licence key. If you have none, ask the person who gave you vCheck.

## Moving from the earlier install

If vCheck was installed on this Mac with the install script (the copy that
runs in Docker and opens at `http://localhost:8080`), remove it and install
the app instead. The two keep their data separately, so take your data with
you first.

1. **Keep your data.** In the old copy press ⌘K, open **My Profile**, and
   under **Your Data** choose **Prepare export**. Download the file.

2. **Remove Colima's virtual machine.** This comes first: on a Mac without
   Homebrew the next step deletes the `colima` command itself.

   ```bash
   colima delete --data
   ```

   If it answers `unknown flag: --data`, it is an older Colima: run
   `colima delete` instead.

3. **Remove vCheck.** Answer `y` when asked. A message that Docker cannot be
   reached is expected, since the virtual machine is already gone.

   ```bash
   vcheck uninstall
   ```

4. **Remove Docker**, if it came from Homebrew:

   ```bash
   brew uninstall colima docker docker-compose docker-buildx
   ```

5. **Install the app** as described above and enter your licence key. Then
   press ⌘K, open **My Profile**, and under **Your Data** import the file
   from step 1.

If you use Colima or Docker for anything else, skip steps 2 and 4: step 2
deletes every container in Colima, not only vCheck's. `vcheck uninstall` on
its own removes vCheck and leaves both in place.

One line is left behind in `~/.zprofile`, `~/.zshrc` and `~/.bash_profile`,
under a `# vCheck` comment: `export PATH="$HOME/.vcheck/bin:$PATH"`. It does
no harm and can be deleted by hand.

## Updates

An installed copy looks for a newer version by itself, downloads it in the
background and shows **Relaunch to update**. Nothing needs to be downloaded
from here again.

© 2026 Aziz Ozsoy
