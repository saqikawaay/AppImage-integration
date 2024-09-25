# Integrating Obsidian AppImage on Pop!_OS

This guide explains how to integrate the Obsidian AppImage on Pop!_OS (or any other Debian-based Linux distribution) so that it appears in your application launcher with an icon.

## Step 1: Move the AppImage to a Standard Directory

It's common practice to store AppImages in `~/Applications` or `/opt`. If your AppImage is already in `~/Applications`, you can proceed.

Example location:
```
~/Applications/Obsidian-1.6.7.AppImage
```

## Step 2: Retrieve the Icon

AppImages often come with embedded icons that you can extract and use for desktop integration.

1. **Extract the AppImage contents**:
   
   Open a terminal and navigate to the directory where your AppImage is stored:
   ```bash
   cd ~/Applications
   ```

2. **Extract the contents**:
   
   Run the following command to extract the files:
   ```bash
   ./Obsidian-1.6.7.AppImage --appimage-extract
   ```
   
   This will create a directory named `squashfs-root` that contains the contents of the AppImage.

3. **Find the icon**:
   
   Icons are usually found in `usr/share/icons/` or `usr/share/pixmaps/`. To find the icon file, use the following command:
   ```bash
   find squashfs-root -name "*.png"
   ```
   or
   ```bash
   find squashfs-root -name "*.svg"
   ```

4. **Copy the icon**:
   
   Once you've located the icon, copy it to a standard icon directory such as `~/.local/share/icons/`:
   ```bash
   cp <path-to-icon> ~/.local/share/icons/
   ```

## Step 3: Create a `.desktop` File for Application Integration

To make the AppImage appear in your application launcher (such as GNOME's or Pop!_OS's launcher), you need to create a `.desktop` file.

1. **Create a `.desktop` file**:
   
   Use the following command to create a `.desktop` file:
   ```bash
   nano ~/.local/share/applications/obsidian.desktop
   ```

2. **Add the following content**:
   
   ```ini
   [Desktop Entry]
   Name=Obsidian
   Exec=/home/<your-username>/Applications/Obsidian-1.6.7.AppImage
   Icon=/home/<your-username>/.local/share/icons/<obsidian-icon>.png
   Type=Application
   Categories=Utility;Application;
   ```

   Replace `<your-username>` with your actual username and `<obsidian-icon>` with the name of the icon you extracted in Step 2.

3. **Save and close the file**.

## Step 4: Make the AppImage Executable

Ensure that the AppImage is executable:
```bash
chmod +x ~/Applications/Obsidian-1.6.7.AppImage
```

## Step 5: Refresh the Desktop Database

Finally, refresh the desktop application database so that the launcher detects your new `.desktop` entry:
```bash
update-desktop-database ~/.local/share/applications/
```

## Conclusion

Once these steps are completed, you should be able to find Obsidian in your application launcher, complete with the correct icon. Enjoy using Obsidian on Pop!_OS!
