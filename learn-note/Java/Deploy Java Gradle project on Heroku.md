---
tags: 
  - gradle
  - java
  - heroku
---



## gradle.build file 

``` groovy
buildscript {
    repositories {
        mavenCentral()
    }
    dependencies {
        classpath  'org.springframework.boot:spring-boot-gradle-plugin:2.5.0'
    }
}


plugins {
    id 'org.springframework.boot' version '2.5.0'
    id 'io.spring.dependency-management' version '1.0.11.RELEASE'
    id 'java'
    id 'idea'
}

group = 'com.lunatech'
version = '0.0.1-SNAPSHOT'

sourceCompatibility = '1.8'


repositories {
    mavenCentral()
}

dependencies {
    implementation platform('software.amazon.awssdk:bom:2.16.86')
    implementation 'org.springframework.boot:spring-boot-starter'
    implementation 'org.springframework.boot:spring-boot-starter-web'
    testImplementation 'org.springframework.boot:spring-boot-starter-test'
    implementation 'com.squareup.okhttp3:okhttp:4.9.1'
    implementation("com.slack.api:bolt:1.8.0")
    implementation("com.slack.api:bolt-servlet:1.8.0")
    implementation("com.slack.api:bolt-jetty:1.8.0")
// https://mvnrepository.com/artifact/software.amazon.awssdk/protocol-core
    implementation group: 'software.amazon.awssdk', name: 'protocol-core', version: '2.16.86'
// https://mvnrepository.com/artifact/software.amazon.awssdk/dynamodb
    implementation group: 'software.amazon.awssdk', name: 'dynamodb', version: '2.16.86'
// https://mvnrepository.com/artifact/software.amazon.awssdk/dynamodb-enhanced
    implementation group: 'software.amazon.awssdk', name: 'dynamodb-enhanced', version: '2.16.86'
    implementation group: 'org.slf4j', name: 'slf4j-api', version: '1.7.30'
    // https://mvnrepository.com/artifact/org.projectlombok/lombok
    compileOnly 'org.projectlombok:lombok:1.18.20'
    annotationProcessor 'org.projectlombok:lombok:1.18.20'
    testCompileOnly 'org.projectlombok:lombok:1.18.20'
    testAnnotationProcessor 'org.projectlombok:lombok:1.18.20'

}


jar {
    distributionBaseName = 'demo'
    archiveVersion = '0.1.0'
}

task stage{
    dependsOn build
}
```

## Profile 

An extra file called Procfile should be added in the project root directory

```bash
web: java -Dserver.port=$PORT $JAVA_OPTS -jar build/libs/ToggleElf-0.0.1-SNAPSHOT.jar

```

Pay attention the file name and dirctory should match the one in local project, or although it can build successfully, it still cannot be accessed.


```
./gradlew stage
heroku local 
```

If nothing goes wrong, the gradle can successfully  build on local

---

```bash
heroku login
```

```bash
git commit -am "make first commit"```

```bash
git push heroku main
```

```bash
heroku ps:scale web=1
```

if success:
![a5ce361a7b79302cc3840dcde5674206.png](../_resources/a5ce361a7b79302cc3840dcde5674206.png)