Maven Parents
=============

This repository contains parent POMs for [FIT CTU]’s projects.
All faculty projects should use one of these parents.


root-parent
-----------

This is the root parent with basic plugins and profiles. It automatically checks classpath for duplicate classes with
[duplicate-finder], checks Java code with [checkstyle] \(rules are defined in [checkstyle.xml]), runs integration tests,
collects metrics for code coverage analysis (when **ci** profile enabled), deploys sources and JavaDocs in deploy phase
etc.

It’s preconfigured to deploy artifacts to [the faculty repository](https://repository.fit.cvut.cz/maven)
([more info][wiki-maven-repos]), but it also provides profile _bintray-deploy_ for deploying artifacts to [Bintray] /
[jCenter] \(a [pain-free gateway to Maven Central]) and _sonatype-deploy_ for deploying artifacts to [Sonatype OSS]
\(a painful gateway to Maven Central).

### Properties

*  **java.version** ... Version of JDK to compile sources for (default is 1.7).
*  **slf4j.version** ... Version of [slf4j-api] to use (default is 1.7.12).

### Profiles

*  **ci** ... General profile for [CI] to analyze code coverage (uses [JaCoCo]). It should be activated automatically
   on CI environments.
*  **travis-ci** ... Profile for [Travis] to submit code coverage to [Coveralls]. This profile is for public projects
   only. It’s activated automatically on Travis.
*  **bintray-deploy** ... Profile for deploying artifacts to Bintray.
*  **sonatype-deploy** ... Profile for deploying artifacts to Sonatype OSS.

### Usage

Add this to the top of your POM:

```xml
<parent>
    <groupId>cz.cvut.fit.maven</groupId>
    <artifactId>root-parent</artifactId>
    <version>2.1.5</version>
</parent>
```

If you want to use Travis with Coveralls, put `.travis.yml` to the root of your repository:

```yml
language: java
sudo: false
jdk:
  - openjdk7
  - oraclejdk8
script:
  - 'mvn verify -B'
after_success:
  - 'mvn jacoco:report coveralls:jacoco'
```

[![Maven Central](https://maven-badges.herokuapp.com/maven-central/cz.cvut.fit.maven/root-parent/badge.svg)](https://maven-badges.herokuapp.com/maven-central/cz.cvut.fit.maven/root-parent)
[![Dependency Status](https://www.versioneye.com/user/projects/5621114d36d0ab0019000852/badge.svg?style=flat)](https://www.versioneye.com/user/projects/5621114d36d0ab0019000852)


groovy-parent
-------------
_inherits from root-parent_

Parent for projects that uses Groovy.

### Properties

*  **groovy.version** ... Version of [groovy] to use.
*  **groovy-compiler.version** ... Version of [groovy-eclipse-compiler] to use.
*  **groovy-batch.version** ... Version of [groovy-eclipse-batch] to use.

### Usage

Add this to the top of your POM:

```xml
<parent>
    <groupId>cz.cvut.fit.maven</groupId>
    <artifactId>groovy-parent</artifactId>
    <version>2.1.5</version>
</parent>
```

If you want to use Groovy just in tests, not a production code, then redefine the groovy’s dependency scope:

```xml
<dependencies>
    <dependency>
        <groupId>org.codehaus.groovy</groupId>
        <artifactId>groovy</artifactId>
        <scope>test</scope>
    </dependency>
</dependencies>
```

[![Maven Central](https://maven-badges.herokuapp.com/maven-central/cz.cvut.fit.maven/groovy-parent/badge.svg)](https://maven-badges.herokuapp.com/maven-central/cz.cvut.fit.maven/groovy-parent)
[![Dependency Status](https://www.versioneye.com/user/projects/5621117436d0ab00160009df/badge.svg?style=flat)](https://www.versioneye.com/user/projects/5621117436d0ab00160009df)


groovy-lombok-parent
--------------------
_inherits from groovy-parent_

Parent for projects that uses Groovy (mainly for tests) and [Lombok] annotation processor.

### Properties

*  **lombok.version** ... Version of [lombok] to use.

### Usage

Add this to the top of your POM:

```xml
<parent>
    <groupId>cz.cvut.fit.maven</groupId>
    <artifactId>groovy-lombok-parent</artifactId>
    <version>2.1.5</version>
</parent>
```

[![Maven Central](https://maven-badges.herokuapp.com/maven-central/cz.cvut.fit.maven/groovy-lombok-parent/badge.svg)](https://maven-badges.herokuapp.com/maven-central/cz.cvut.fit.maven/groovy-lombok-parent)
[![Dependency Status](https://www.versioneye.com/user/projects/5621115336d0ab00210009cd/badge.svg?style=flat)](https://www.versioneye.com/user/projects/5621115336d0ab00210009cd)


License
-------

This project is licensed under [MIT license](http://opensource.org/licenses/MIT).


<!-- Links -->

[Bill of Materials]: http://howtodoinjava.com/2014/02/18/maven-bom-bill-of-materials-dependency/
[Bintray]: https://bintray.com/
[duplicate-finder]: https://github.com/ning/maven-duplicate-finder-plugin
[checkstyle]: http://checkstyle.sourceforge.net/
[CI]: http://en.wikipedia.org/wiki/Continuous_integration
[Coveralls]: https://coveralls.io/
[FIT CTU]: http://fit.cvut.cz
[jCenter]: https://bintray.com/bintray/jcenter/
[JaCoCo]: http://www.eclemma.org/jacoco/
[Maven Central]: http://search.maven.org/
[pain-free gateway to Maven Central]: http://blog.bintray.com/2014/02/11/bintray-as-pain-free-gateway-to-maven-central/
[Lombok]: http://projectlombok.org/
[Sonatype OSS]: https://docs.sonatype.org/display/Repository/Sonatype+OSS+Maven+Repository+Usage+Guide
[Travis]: https://travis-ci.org/
[wiki-maven-repos]: https://rozvoj.fit.cvut.cz/Main/Maven-repositare

[checkstyle.xml]: /codequality-resources/src/main/resources/cz/cvut/fit/maven/codequality/checkstyle.xml

[groovy]: http://search.maven.org/#search|gav|1|g%3A%22org.codehaus.groovy%22%20AND%20a%3A%22groovy%22
[groovy-eclipse-batch]: http://search.maven.org/#search|gav|1|g%3A%22org.codehaus.groovy%22%20AND%20a%3A%22groovy-eclipse-batch%22
[groovy-eclipse-compiler]: http://search.maven.org/#search|gav|1|g%3A%22org.codehaus.groovy%22%20AND%20a%3A%22groovy-eclipse-compiler%22
[lombok]: http://search.maven.org/#search|gav|1|g%3A%22org.projectlombok%22%20AND%20a%3A%22lombok%22
[slf4j-api]: http://search.maven.org/#search|gav|1|g%3A%22org.slf4j%22%20AND%20a%3A%22slf4j-api%22
