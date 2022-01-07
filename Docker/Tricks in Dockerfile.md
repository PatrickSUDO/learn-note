---
tags: 
  - docker
---



---

### Clean rededundent state file in linux to minize image size

```bash
  rm -rf /var/lib/apt/lists/* && \
  apt-get autoclean && \
  apt-get --purge -y autoremove
```

