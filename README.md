# Install NVIDIA Visual Profiler (nvvp) on macOS (Big Sur, Monterey)
-----------
0. Download nvvp zip file from NVIDIA webpage (https://developer.nvidia.com/nvidia-cuda-toolkit-developer-tools-mac-hosts)
1. Disable gatekeeper for nvvp folder
sudo xattr -rd com.apple.quarantine ./nvvp

2. Install Zulu - 1.8.151 jdk (https://www.azul.com/downloads/zulu-community/?version=java-8-lts&os=macos&architecture=x86-64-bit&package=jdk&show-old-builds=true)
3. Add JAVA_HOME and path (already reflected in .zshrc of this dotfiles)
/Library/Java/JavaVirtualMachines/zulu-8.jdk/Contents/Home

4. Create symlink
sudo ln -s /Library/Java/JavaVirtualMachines/zulu-8.jdk/Contents/Home/jre/lib/server/libjvm.dylib /Library/Java/JavaVirtualMachines/zulu-8.jdk/Contents/Home/lib/libserver.dy

5. Add arguments
In `libnvvp/nvvp.app/Contents/MacOS/nvvp.ini`
-d64
-vmargs
-Xms2g
-Xmx22g
-XX:+UseConcMarkSweepGC
-XX:+CMSIncrementalMode

6. Add on App drawer

Use mac-appify (pip) if possible (Be sure to place nvvp folder on your home directory (`~/`))
```
mkdir -p nvvpMac.app
mkdir -p nvvpMac.app/Contents/MacOS
cp runnvvp.sh nvvpMac.app/Contents/MacOS/executable
mkdir -p nvvpMac.app/Contents/Resources
/usr/bin/sips -s format icns /Users/young/nvvp/libnvvp/nvvp.app/Contents/Resources/visualprofiler.icns --out nvvpMac.app/Contents/Resources/Icon.icns /Users/young/nvvp/libnvvp/nvvp.app/Contents/Resources/visualprofiler.icns /Users/young/.dotfiles/nvvpMac.app/Contents/Resources/Icon.icns
/usr/libexec/PlistBuddy -c 'Add CFBundleName string '\''nvvpMac'\''' -c 'Add CFBundleExecutable string '\''executable'\''' -c 'Add CFBundleIconFile string '\''Icon'\''' nvvpMac.app/Contents/Info.plist
/usr/bin/touch nvvpMac.app nvvpMac.app nvvpMac.app
```

7. `mv nvvpMac.app /Applications/`

