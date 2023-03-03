# m2eclipse-ajdt
M2E Configurer for AJDT

This plugin provides support for Eclipse build procedure in maven projects that use `aspectj:compile`.
Without this plugin you may see warnings such as "`Plugin execution not covered by lifecycle configuration: org.codehaus.mojo:aspectj-maven-plugin ...`"

This plugin supports multiple different forked versions of `aspectj-maven-plugin`. Following `groupId` values for this plugin are recognized:
 * `dev.aspectj`
 * `com.nickwongdev`
 * `org.codehaus.mojo`
 * `com.github.m50d`
 * `se.haleby.aspectj`
 * `io.starter`

I need this plugin for work stuff and plan to maintain its compatiblity with Eclipse (mostly packaging related updates). Any updates for this plugin are expected to happen when somehing breaks my use-case. I welcome any patches and pull requests.

If you find this plugin useful, you are free to use and distribute it according to the original license.

## Build
Use Java version 17 to build this plugin (if you use other version, build will fail because MANIFEST.MF has required version set to JavaSE-17)
```sh
mvn clean package
# or use specific java installation
JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64 mvn clean package
```
This build produces Eclipse update site to folder `org.maven.ide.eclipse.ajdt.site/target/site`. You can simply copy everything in that directory and host it with
any http server you want and then install the artifacts from that site with Eclipse.

## Tests
Execute integration tests with following command.
```sh
mvn clean integration-test
```
Integration test will launch eclipse instance and this process takes a while but should complete successfully.

## Release process
Create new release by executing:
```sh
# Prepare release
mvn release:prepare -DreleaseVersion=0.14.5 -Dtag=m2eclipse-ajdt-0.14.5 -DdevelopmentVersion=0.14.6-SNAPSHOT

# Perform release
mvn release:perform -Dgoals="clean install"
```

`release:perform` does not work yet (unresolved javadoc issues).

## Installation
You can install this m2e connector to eclipse by selecting Help -> Install new software... -> Add

Eclipse update site URLs:

| Eclipse version | Update site URL  |
| --------------- | ---------------- |
| 2019-06         | https://repo.t5.fi/public/eclipse/m2eclipse-ajdt/eclipse-2019-06/ |
| 2020-12         | https://repo.t5.fi/public/eclipse/m2eclipse-ajdt/eclipse-2020-12/ |
| 2022-12         | https://repo.t5.fi/public/eclipse/m2eclipse-ajdt/eclipse-2022-12/ |

These update sites are provided on best-effort basis but availability is generally good.
