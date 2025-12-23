# SDK BOM (Bill of Materials)

[![Maven Central](https://img.shields.io/badge/Maven-Central-blue.svg)](https://search.maven.org/artifact/com.slytechs.sdk/sdk-bom) [![License](https://img.shields.io/badge/License-Apache%20v2-green.svg)](https://claude.ai/chat/LICENSE)

Centralized dependency management for the Sly Technologies Network SDK.

------

## Do You Need the BOM?

**Most users don't.** If you just want to capture and analyze packets:

```xml
<dependency>
    <groupId>com.slytechs.sdk</groupId>
    <artifactId>jnetpcap-sdk</artifactId>
    <version>3.0.0</version>
</dependency>
```

Done. The starter pulls all dependencies with correct versions.

------

## When to Use the BOM

The BOM is useful when you need:

- **Cherry-pick modules** - Only include specific modules, not the full starter
- **Multi-module projects** - Define version once in parent, children inherit
- **Mix commercial + public** - Ensure version consistency across modules
- **Override versions** - Test with newer/older module versions

------

## Usage Patterns

### Pattern 1: Cherry-Pick Modules

```xml
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>com.slytechs.sdk</groupId>
            <artifactId>sdk-bom</artifactId>
            <version>3.0.0</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>

<dependencies>
    <!-- Now omit versions - BOM manages them -->
    <dependency>
        <groupId>com.slytechs.sdk</groupId>
        <artifactId>jnetpcap-api</artifactId>
    </dependency>
    <dependency>
        <groupId>com.slytechs.sdk</groupId>
        <artifactId>sdk-protocol-telco</artifactId>
    </dependency>
</dependencies>
```

### Pattern 2: Multi-Module Parent POM

In your parent POM:

```xml
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>com.slytechs.sdk</groupId>
            <artifactId>sdk-bom</artifactId>
            <version>3.0.0</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```

In child modules:

```xml
<dependencies>
    <dependency>
        <groupId>com.slytechs.sdk</groupId>
        <artifactId>jnetpcap-api</artifactId>
        <!-- Version inherited from parent -->
    </dependency>
</dependencies>
```

### Pattern 3: Version Override

With BOM imported, you can still override specific versions:

```xml
<dependency>
    <groupId>com.slytechs.sdk</groupId>
    <artifactId>sdk-protocol-tcpip</artifactId>
    <version>3.1.0</version> <!-- Override BOM's version -->
</dependency>
```

### Pattern 4: Gradle

```groovy
dependencies {
    implementation platform('com.slytechs.sdk:sdk-bom:3.0.0')
    implementation 'com.slytechs.sdk:jnetpcap-api'
    implementation 'com.slytechs.sdk:sdk-protocol-tcpip'
}
```

------

## Managed Modules

### Public Modules (Maven Central)

**SDK Core**

| Module              | Description                           |
| ------------------- | ------------------------------------- |
| `sdk-common`        | Memory management, buffers, utilities |
| `sdk-protocol-core` | Protocol dissection framework         |

**Protocol Packs**

| Module               | Description                                   |
| -------------------- | --------------------------------------------- |
| `sdk-protocol-tcpip` | Ethernet, IPv4/6, TCP, UDP, VLAN, MPLS, IPsec |
| `sdk-protocol-web`   | HTTP, TLS, DNS, QUIC, WebSocket               |
| `sdk-protocol-infra` | BGP, OSPF, STP, VRRP, LACP, LLDP              |

**jNetPcap**

| Module              | Description                               |
| ------------------- | ----------------------------------------- |
| `jnetpcap-bindings` | Low-level libpcap FFM bindings            |
| `jnetpcap-api`      | High-level capture and analysis API       |
| `jnetpcap-sdk`      | Starter - pulls all jNetPcap dependencies |

**jNetWorks Core**

| Module           | Description                                       |
| ---------------- | ------------------------------------------------- |
| `jnetworks-api`  | High-level jNetWorks API                          |
| `jnetworks-pcap` | PCAP file read/write support                      |
| `jnetworks-sdk`  | Starter - pulls all public jNetWorks dependencies |

### Commercial Modules (maven.slytechs.com)

**jNetWorks Hardware**

| Module               | License    |
| -------------------- | ---------- |
| `jnetdpdk-bindings`  | Commercial |
| `jnetworks-dpdk`     | Commercial |
| `jnetntapi-bindings` | Commercial |
| `jnetworks-ntapi`    | Commercial |
| `jnetafxdp-bindings` | Commercial |
| `jnetworks-afxdp`    | Commercial |

### Commercial Repository Access

Defined by the BOM or use manually

```xml
<repositories>
    <repository>
        <id>slytechs-enterprise</id>
        <url>https://maven.slytechs.com/enterprise</url>
    </repository>
</repositories>
```

------

## Managed Plugin Versions

The BOM also manages common plugin versions:

| Plugin                | Version |
| --------------------- | ------- |
| maven-compiler-plugin | 3.12.1  |
| maven-surefire-plugin | 3.2.5   |
| maven-jar-plugin      | 3.3.0   |
| maven-source-plugin   | 3.3.0   |
| maven-javadoc-plugin  | 3.6.3   |

------

## Managed Test Dependencies

| Dependency           | Version |
| -------------------- | ------- |
| junit-jupiter        | 5.10.2  |
| junit-platform-suite | 1.10.2  |

------

## Summary

| Approach             | Lines | Use Case                     |
| -------------------- | ----- | ---------------------------- |
| Starter with version | 5     | 90% of users                 |
| BOM import           | 15+   | Cherry-picking, multi-module |
| BOM as parent        | 8     | Internal SDK modules         |

**When in doubt, use the starter.**

------

## License

Licensed under Apache License v2.0. See [LICENSE](https://claude.ai/chat/LICENSE) for details.

------

**Sly Technologies Inc.** - High-performance network analysis solutions

Website: [www.slytechs.com](https://www.slytechs.com/)
