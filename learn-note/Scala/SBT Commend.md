---
tags: 
  - scala
---



### Set correct scala format

```bash
sbt scalafmt
```


### Starts your application in a forked JVM (something like "hot-deployment")
https://github.com/spray/sbt-revolver
```bash
# Caan run sbt first than reStart
sbt reStart
```

### Clear all the target things in SBT project

```bash
find . -type d -name 'target' -exec rm -r {} +
```