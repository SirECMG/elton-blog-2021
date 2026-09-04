---
layout: post
title:  "configure excalidraw using podman on fedora"
date:   2026-07-18 1:57:00 -0700
tags: [productivity]
---

the following commands install excalidraw in local network

```text
podman pull docker.io/excalidraw/excalidraw:latest```


```text
podman run -d --name excalidraw -p 8999:89 docker.io/excalidraw/excalidraw:latest
```

```text
podman build -t excalidraw/excalidraw .
  
  podman pull excalidraw/excalidraw
  
  podman pull docker.io/excalidraw/excalidraw:latest
  
  podman run -d --name excalidraw -p 8999:80 docker.io/excalidraw/excalidraw:latest
```


> [host]:[container]
this is the convention the right hand side is not arbitrary as app depends on it
8999:80
