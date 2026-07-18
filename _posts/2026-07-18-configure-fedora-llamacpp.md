---
layout: post
title:  "configure llama.cpp on fedora"
date:   2026-07-05 11:49:00 -0700
tags: [ai]
---

configure llama.cpp on fedora for raedeon 9070XT


dependencies
```text
sudo dnf list installed "vulkan*"
sirecmg@fedora-desktop:~/projects/llama.cpp$ sudo dnf list installed "vulkan*"
Updating and loading repositories:
Repositories loaded.
Installed packages (available for reinstall, available for upgrade)
vulkan-headers.noarch                 1.4.341.0-1.fc44 fedora
vulkan-loader.x86_64                  1.4.341.0-1.fc44 6ecc2dfaa0dc41e5ad51e007707a786b
vulkan-loader-devel.x86_64            1.4.341.0-1.fc44 fedora
vulkan-tools.x86_64                   1.4.341.0-1.fc44 6ecc2dfaa0dc41e5ad51e007707a786b

Available packages (available for reinstall, available for upgrade)
VulkanMemoryAllocator-devel.noarch    3.3.0-4.fc44     fedora
VulkanMemoryAllocator-doc.noarch      3.3.0-4.fc44     fedora
vulkan-loader.i686                    1.4.341.0-1.fc44 fedora
vulkan-loader-devel.i686              1.4.341.0-1.fc44 fedora
vulkan-utility-libraries-devel.i686   1.4.341.0-1.fc44 fedora
vulkan-utility-libraries-devel.x86_64 1.4.341.0-1.fc44 fedora
vulkan-validation-layers.i686         1.4.341.0-2.fc44 fedora
vulkan-validation-layers.x86_64       1.4.341.0-2.fc44 fedora
vulkan-volk-devel.i686                1.4.341.0-1.fc44 fedora
vulkan-volk-devel.x86_64 
```


configure and build
```text
cmake -B build -DGGML_VULKAN=ON -DCMAKE_BUILD_TYPE=Release
cmake --build build --config Release -j$(nproc)
```

start llama.cpp
```text
sirecmg@fedora-desktop:~/projects/llama.cpp$ ./build/bin/llama serve -hf yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF:Q4_K_M --host 0.0.0.0 -ngl 999
```

