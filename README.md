# Install NVIDIA Visual Profiler (nvvp) on macOS (Big Sur, Monterey)
-----------
0. Download nvvp zip file from NVIDIA webpage [LINK](https://developer.nvidia.com/nvidia-cuda-toolkit-developer-tools-mac-hosts)
1. Disable gatekeeper for nvvp folder

```
sudo xattr -rd com.apple.quarantine ./nvvp
```

2. Install Zulu - 1.8.141 jdk [LINK](https://www.azul.com/downloads/zulu-community/?version=java-8-lts&os=macos&architecture=x86-64-bit&package=jdk&show-old-builds=true)
3. Add JAVA_HOME and PATH - Add below on `.zshrc`
```
export JAVA_HOME=/Library/Java/JavaVirtualMachines/zulu-8.jdk/Contents/Home
export PATH=${PATH}:$JAVA_HOME/bin
```

4. Create symlink
```
sudo ln -s /Library/Java/JavaVirtualMachines/zulu-8.jdk/Contents/Home/jre/lib/server/libjvm.dylib /Library/Java/JavaVirtualMachines/zulu-8.jdk/Contents/Home/lib/libserver.dy
```

5. Add arguments

On `libnvvp/nvvp.app/Contents/MacOS/nvvp.ini`, add 

```
-d64
-vmargs
-Xms2g
-Xmx22g
-XX:+UseConcMarkSweepGC
-XX:+CMSIncrementalMode
```

6. Install [mac-appify](https://pypi.org/project/mac-appify/) 
7. `appify run_nvvp.sh nvvpMac.app $HOME/nvvp/libnvvp/nvvp.app/Contents/Resources/visualprofiler.icns`
- This will generate `nvvpMac.app`. 
- `run_nvvp.sh` is included in this repo.

8. Add on App drawer

