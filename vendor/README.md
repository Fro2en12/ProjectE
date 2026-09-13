# vendor/

本地内置的构建依赖，**jar 不入 git**（见仓库根目录 `.gitignore` 里的 `vendor/maven/`）。
这里只保存说明与许可文本。

## EMI (`dev.emi:emi-neoforge:1.1.20+1.21.1`)

`maven.terraformersmc.com` 在部分网络下不可达，而 EMI 是硬性构建依赖，解析失败会让编译
根本跑不起来。`build.gradle` 因此把 `vendor/maven` 声明为 `dev.emi` 组的仓库；该目录
不存在时 Gradle 会直接跳过，所以普通 clone 依旧从官方源解析，不受影响。

jar 需要在本机自行放置：

1. `git clone --depth 1 -b "1.1.20+1.21.1" https://github.com/emilyploszaj/emi.git`
   （注意：构建时不设 `RELEASE=1` 的话，产物版本号会变成 `1.1.20-SNAPSHOT+1.21.1`，
   与本项目依赖的坐标对不上）
2. `RELEASE=1 ./gradlew :neoforge:publishToMavenLocal`
3. 把 `~/.m2/repository/dev/emi/emi-neoforge/1.1.20+1.21.1/` 下的
   `emi-neoforge-1.1.20+1.21.1-api.jar`、`emi-neoforge-1.1.20+1.21.1.jar`、
   `emi-neoforge-1.1.20+1.21.1.pom` 复制到
   `vendor/maven/dev/emi/emi-neoforge/1.1.20+1.21.1/`

- 上游：https://github.com/emilyploszaj/emi （tag `1.1.20+1.21.1`，commit `a8d798a`）
- 许可：MIT，见 `EMI-LICENSE.txt`
