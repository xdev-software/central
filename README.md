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

#### Are the artifacts cryptographically signed?

_Last updated: 2025-09_

Yes, all artifacts should be signed with
```
-----BEGIN PGP PUBLIC KEY BLOCK-----

mDMEYanFmRYJKwYBBAHaRw8BAQdAwe6KCL97lXybaEP0YmvILxEra1NKqUy6MPyJ
1YslrwK0JVhERVYgU29mdHdhcmUgPGluZm9AeGRldi1zb2Z0d2FyZS5kZT6IkAQT
FggAOAIbAwULCQgHAgYVCgkICwIEFgIDAQIeAQIXgBYhBByUKHSrxufW8XAY4hTr
jkjDgOqqBQJlX1QbAAoJEBTrjkjDgOqqKrwBAJ+eAxW+JyUiD1ctvAeYllJlbUk0
d5O4DG93rrJNRnQNAQCEeDefKB1u/L3LuB9WSCHF7ferP+JZW2OMUHJq/QksB7g4
BGGpxZkSCisGAQQBl1UBBQEBB0B4U6R9YDwjffS8fShj23blN4dV5lwKBEpKcpON
I/yHTwMBCAeIfgQYFggAJgIbDBYhBByUKHSrxufW8XAY4hTrjkjDgOqqBQJlX1Yl
BQkJlH6MAAoJEBTrjkjDgOqql1oA/jMFKPwyPK3AwatXa4pHEksSWIMRgvfn/wQ5
myqQxdxKAP9Mm50oVv6ONXkVpxf6zG47HnUZEdKFvNT6HRH4LMiWBQ==
=h0V/
-----END PGP PUBLIC KEY BLOCK-----
```

Also available at [keyserver.ubuntu.com](https://keyserver.ubuntu.com/pks/lookup?search=1c942874abc6e7d6f17018e214eb8e48c380eaaa&fingerprint=on&op=index).

For example you can check the key used for signing artifacts using the [pgpverify-maven-plugin](https://github.com/s4u/pgpverify-maven-plugin):<br/>
`mvn org.simplify4u.plugins:pgpverify-maven-plugin:show -Dartifact=software.xdev:<artifactId>:1.2.3`

Older releases (before 2022) might use different keys.
