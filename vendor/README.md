# vendor/

Bundled build-time dependencies that are not reachable from every network.

## EMI (`dev.emi:emi-neoforge:1.1.20+1.21.1`)

- Upstream: https://github.com/emilyploszaj/emi, tag `1.1.20+1.21.1` (commit `a8d798a`)
- Built locally with `RELEASE=1 ./gradlew :neoforge:publishToMavenLocal`
  (without `RELEASE` the artifact version becomes `1.1.20-SNAPSHOT+1.21.1`, which does
  not match the coordinates this project depends on)
- License: MIT — see `EMI-LICENSE.txt`

Why it is here: `maven.terraformersmc.com` is not reachable from some networks, and
EMI is a hard build dependency, so resolution used to fail before compilation started.
`build.gradle` registers this directory as a repository for the `dev.emi` group;
Gradle skips it entirely when the directory is absent, so a plain clone still resolves
EMI from the official source.
