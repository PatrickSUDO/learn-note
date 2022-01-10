---
tags: 
  - java
  - environment
---



# Java Environment Management

## Delete specific version of JDK:

```bash
java -version
```

```bash
cd /Library/Java/JavaVirtualMachines
```

```bash
ls
```

```bash
##for example:
sudo rm -rf jdk-10.0.1.jdk
sudo rm -rf jdk-9.0.1.jdk
sudo rm -rf jdk1.8.0_111.jdk
sudo rm -rf jdk1.7.0_79.jdk
```



## Delete Open JDK

```bash
/usr/libexec/java_home -V
```

take user1 as example:

```bash
cd /Users/user1/Library/Java/
```

```bash
sudo rm -fr JavaVirtualMachines/*
```

