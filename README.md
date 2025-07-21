# Central

Central repository for [XDEV's GitHub packages](https://github.com/orgs/xdev-software/packages?repo_name=central)

## How to use it?

> [!NOTE]
> Related [GitHub documentation](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-apache-maven-registry#authenticating-with-a-personal-access-token)

``~/.m2/settings.xml``
```xml
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0
                      http://maven.apache.org/xsd/settings-1.0.0.xsd">

  <activeProfiles>
    <activeProfile>github-xdev</activeProfile>
  </activeProfiles>

  <profiles>
    <profile>
      <id>github-xdev</id>
      <repositories>
        <repository>
          <id>central</id>
          <url>https://repo.maven.apache.org/maven2</url>
        </repository>
        <repository>
          <id>github</id>
          <url>https://maven.pkg.github.com/xdev-software/central</url>
          <snapshots>
            <enabled>true</enabled>
          </snapshots>
        </repository>
      </repositories>
    </profile>
  </profiles>

  <servers>
    <server>
      <id>github-xdev</id>
      <username>USERNAME</username>
      <password>TOKEN</password>
    </server>
  </servers>
</settings>
```

## FAQ

#### Why not publish into each corresponding repo?

Because we currently have around 50 individual repos that would all require you to add them to your ``settings.xml``.
This is impossible to manage and also massively degrades performance.

#### Snapshots?

Can be published into the repo but will be automatically deleted after a few days.

[![Snapshot Cleanup](https://github.com/xdev-software/central/actions/workflows/snapshot-cleanup.yml/badge.svg)](https://github.com/xdev-software/central/actions/workflows/snapshot-cleanup.yml)
