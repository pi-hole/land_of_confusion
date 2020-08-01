# Build configuration files for CI/CD

## Travis-CI

Travis-CI can source [shared build configurations](https://docs.travis-ci.com/user/build-config-imports/).

**Please remember to tag versions for [`<path>@<ref>`](https://docs.travis-ci.com/user/build-config-imports/#importing-specific-versions-of-configs) notation.**

Pull Requests can `import` any reference.
>The format of the import source is `<account>/<repository>:<path>@<ref>` in which `<ref>` can be any valid Git reference, such as a commit sha, branch name, or tag name.

*Usage example:*  

```yml
import: pi-hole/.github:/build-configs/core.yml@v1.0.0
```

Imports can be conditional. As an example, Pi-hole Core can import a stable configuration for master releases, using different configurations for pull requests and branches.

```yml
import:
  - source: pi-hole/.github:/build-configs/core.yml@main
    if: branch = master
  - source: pi-hole/.github:/build-configs/core.yml@latest
    if: branch != master
```

This format will allow for the `main` tag to float to updated yml without having to push changes to the actual master branch. *No more :WAIT: hotfix releases.*
