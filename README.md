<p align="center"><img src="https://raw.githubusercontent.com/SlimefunNewHorizons/SefiLib/main/banner.svg" alt="SefiLib for DrakesCraft" width="100%"></p>

# SefiLib for DrakesCraft

> ### 🏰 ¡Únete a la Comunidad Oficial de DrakesCraft!
> 
> * 🎮 **IP del Servidor**: `play.drakescraft.net` *(Java 1.21.11 & Bedrock)*
> * 💬 **Discord Oficial**: [discord.gg/drakescraft](https://discord.gg/rv3vtXZTk7)
> * 🌐 **Web & Guía**: [drakescraft.net](https://drakescraft.net) — 🛒 **Tienda**: [tienda.drakescraft.net](https://tienda.drakescraft.net)
> 
> *¡Juega con este addon y más de 80 expansiones optimizadas en vivo en nuestra network de supervivencia técnica!*

---

Compatibility port of SefiLib for Java 21, Paper/Purpur 1.21.11 and the repackaged DrakesCraft Slimefun core.

The port updates modern Bukkit attributes, item flags and particle names. Telemetry and runtime update checks are disabled; reviewed artifacts are built and deployed centrally.

```bash
mvn -DskipTests install
```

Artifact: `com.github.drakescraft_labs:SefiLib:0.3.0-Drake-1.21.11`.

The original project by Sefiraat and its GPL-3.0 license are preserved.

---

## Using maven.drakescraft.cl

Release and snapshot builds of this project are published at **https://maven.drakescraft.cl** (a static Maven repository served from GitHub Pages; sources in [SlimefunNewHorizons/maven-repo](https://github.com/SlimefunNewHorizons/maven-repo)). The full matrix lives in [`docs/COMPATIBILITY.md`](https://github.com/SlimefunNewHorizons/maven-repo/blob/main/docs/COMPATIBILITY.md).

> **Warning:** the 1.21.11 and 26.x lines are **not binary-interchangeable** (different Java release, Paper API, and Java packages). Pick one line per server/addon and recompile your addon against the matching line.

| Artifact (`com.github.drakescraft_labs`) | Version | Minecraft | Java | Source branch |
|---|---|---|---|---|
| `slimefun-core` | `11.0-Drake-1.21.11-SNAPSHOT` | 1.21.11 | 21 | `main` of Slimefun4-Drake |
| `slimefun-core` | `11.0-Universal-26.x-SNAPSHOT` | 26.2 | 25 | `port-26x` of Slimefun4-Drake |
| `dough-core` | `1.3.1-DRAKE-v11-SNAPSHOT` | 1.21.11 | 21 | `main` of dough-core |
| `dough-core` | `1.3.1-Universal-26.x-SNAPSHOT` | 26.2 | 25 | `port-26x` of dough-core |
| `SefiLib` | `0.3.0-Drake-1.21.11` | 1.21.11 | 21 | `main` of SefiLib |
| `SefiLib` | `0.3.1-Universal-26.x-SNAPSHOT` | 26.2 | 25 | `port-26x` of SefiLib |

### Maven

```xml
<repositories>
  <repository>
    <id>drakescraft-labs</id>
    <url>https://maven.drakescraft.cl/</url>
    <snapshots><enabled>true</enabled></snapshots>
  </repository>
</repositories>

<dependencies>
  <!-- 26.2 line (Java 25) -->
  <dependency>
    <groupId>com.github.drakescraft_labs</groupId>
    <artifactId>slimefun-core</artifactId>
    <version>11.0-Universal-26.x-SNAPSHOT</version>
    <scope>provided</scope>
  </dependency>
  <dependency>
    <groupId>com.github.drakescraft_labs</groupId>
    <artifactId>dough-core</artifactId>
    <version>1.3.1-Universal-26.x-SNAPSHOT</version>
  </dependency>
  <dependency>
    <groupId>com.github.drakescraft_labs</groupId>
    <artifactId>SefiLib</artifactId>
    <version>0.3.1-Universal-26.x-SNAPSHOT</version>
  </dependency>
</dependencies>
```

For the **1.21.11 line (Java 21)** use instead `slimefun-core:11.0-Drake-1.21.11-SNAPSHOT`, `dough-core:1.3.1-DRAKE-v11-SNAPSHOT` and `SefiLib:0.3.0-Drake-1.21.11`.

### Gradle (Kotlin DSL)

```kotlin
repositories {
    maven("https://maven.drakescraft.cl/")
}

dependencies {
    // 26.2 line (Java 25)
    compileOnly("com.github.drakescraft_labs:slimefun-core:11.0-Universal-26.x-SNAPSHOT")
    implementation("com.github.drakescraft_labs:dough-core:1.3.1-Universal-26.x-SNAPSHOT")
    implementation("com.github.drakescraft_labs:SefiLib:0.3.1-Universal-26.x-SNAPSHOT")

    // 1.21.11 line (Java 21) -- do not mix with the lines above
    // compileOnly("com.github.drakescraft_labs:slimefun-core:11.0-Drake-1.21.11-SNAPSHOT")
    // implementation("com.github.drakescraft_labs:dough-core:1.3.1-DRAKE-v11-SNAPSHOT")
    // implementation("com.github.drakescraft_labs:SefiLib:0.3.0-Drake-1.21.11")
}
```

### Fallback: GitHub Packages

If `maven.drakescraft.cl` is unreachable, the same builds are mirrored in GitHub Packages under `SlimefunNewHorizons` (repositories `Slimefun4-Drake`, `dough-core`, `SefiLib`). Differences from the main repository:

- GitHub Packages **requires authentication even for public packages**: use a personal access token (classic) with at least `read:packages`. Never commit it; read it from an environment variable.
- GitHub Packages rejects uppercase artifact ids, so `SefiLib` is published there as **`sefilib`** (same version strings).
- The mirror carries the jars only (generated minimal POMs for the 1.21.11 line); transitive dependencies still resolve from `https://maven.drakescraft.cl/`, so keep both repositories declared.

`~/.m2/settings.xml` (placeholders only):

```xml
<settings>
  <servers>
    <server>
      <id>github-slimefun</id>
      <username>YOUR_GITHUB_USERNAME</username>
      <password>${env.GITHUB_TOKEN}</password> <!-- token with read:packages -->
    </server>
  </servers>
</settings>
```

and in your `pom.xml` (one `<repository>` per mirrored repo you need; the `id` must match the `<server>` id):

```xml
<repository>
  <id>github-slimefun</id>
  <url>https://maven.pkg.github.com/SlimefunNewHorizons/SefiLib</url>
  <snapshots><enabled>true</enabled></snapshots>
</repository>
```

Package pages: `slimefun-core` and `drakes-slimefun-labs` (parent POM) under [Slimefun4-Drake](https://github.com/SlimefunNewHorizons/Slimefun4-Drake/packages), `dough-core` under [dough-core](https://github.com/SlimefunNewHorizons/dough-core/packages), `sefilib` under [SefiLib](https://github.com/SlimefunNewHorizons/SefiLib/packages).

## 📄 License & Upstream Attribution

This project is a sovereign fork maintained by [**JackStar6677-1**](https://github.com/JackStar6677-1) under [**DrakesCraft Labs**](https://github.com/SlimefunNewHorizons).

- **Original Project:** Created by the upstream authors and the open-source community.
- **DrakesCraft Optimizations:** Modernized for Paper/Purpur 1.21.11+, Java 21, high concurrency, asynchronous safety, and exploit/duplication prevention.
- **License:** Distributed under the original **GNU General Public License v3.0 (GPLv3)** (or original upstream license). See the [LICENSE](LICENSE) file for complete terms.
