# SDK Bill of Materials (BOM)

[![Java](https://img.shields.io/badge/Java-22%2B-orange.svg)](https://openjdk.java.net/projects/jdk/22/) [![Maven Central](https://img.shields.io/badge/Maven-Central-blue.svg)](https://search.maven.org/artifact/com.slytechs.sdk/sdk-bom) [![License](https://img.shields.io/badge/License-Sly%20Technologies-green.svg)](https://claude.ai/chat/LICENSE)

Centralized dependency management for the Sly Technologies Network Analysis SDK. Import this BOM to automatically manage versions across all SDK modules.

## Overview

The SDK BOM (Bill of Materials) provides a single point of version management for all Sly Technologies SDK modules. By importing the BOM, you can declare SDK dependencies without specifying versions, ensuring compatibility across all modules.

## Quick Start

### Maven

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
    <!-- Use SDK starters for simplest setup -->
    <dependency>
        <groupId>com.slytechs.sdk</groupId>
        <artifactId>jnetpcap-sdk</artifactId>
    </dependency>
</dependencies>
```

### Gradle

```groovy
dependencies {
    implementation platform('com.slytechs.sdk:sdk-bom:3.0.0')
    
    // Use SDK starters for simplest setup
    implementation 'com.slytechs.sdk:jnetpcap-sdk'
}
```

## Licensing

### Open Source (Apache v2)

The following modules are licensed under Apache License v2.0 and free for any use:

- All `sdk-*` modules (common, protocol-core, protocol-tcpip, protocol-web, protocol-infra)
- `jnetpcap-bindings`, `jnetpcap-api`, `jnetpcap-sdk`
- `jnetworks-api`, `jnetworks-pcap`, `jnetworks-sdk`

### Commercial License

The following modules require a commercial license from Sly Technologies:

- `jnetworks-dpdk`, `jnetworks-ntapi`, `jnetworks-afxdp`
- All `jnet*-bindings` (DPDK, NTAPI, AF_XDP)

Contact [sales@slytechs.com](mailto:sales@slytechs.com) for licensing inquiries.

## Managed Modules

### SDK Starters (Public - Maven Central, Apache v2)

Convenience modules that pull all required dependencies for common use cases. Free for non-commercial use.

| Module          | Description                                                  |
| --------------- | ------------------------------------------------------------ |
| `jnetpcap-sdk`  | jNetPcap starter - pulls all libpcap-based capture dependencies |
| `jnetworks-sdk` | jNetWorks starter - pulls all jNetWorks pcap dependencies    |

### Core SDK Modules (Public - Maven Central, Apache v2)

| Module              | Description                                               |
| ------------------- | --------------------------------------------------------- |
| `sdk-common`        | Core memory management, utilities, Panama FFM integration |
| `sdk-protocol-core` | Protocol dissection framework and packet descriptors      |

### Protocol Packs (Public - Maven Central, Apache v2)

| Module               | Description                                                 |
| -------------------- | ----------------------------------------------------------- |
| `sdk-protocol-tcpip` | TCP/IP stack (Ethernet, IPv4/IPv6, TCP, UDP, ICMP, ARP)     |
| `sdk-protocol-web`   | Web protocols (HTTP, TLS, DNS, QUIC, WebSocket)             |
| `sdk-protocol-infra` | Infrastructure protocols (BGP, OSPF, STP, VRRP, LACP, LLDP) |

### jNetPcap Modules (Public - Maven Central, Apache v2)

| Module              | Description                                |
| ------------------- | ------------------------------------------ |
| `jnetpcap-bindings` | Libpcap native bindings via Panama FFM     |
| `jnetpcap-api`      | High-level packet capture and analysis API |

### jNetWorks Core Modules (Public - Maven Central, Apache v2)

| Module           | Description                   |
| ---------------- | ----------------------------- |
| `jnetworks-api`  | jNetWorks high-level API      |
| `jnetworks-pcap` | Libpcap backend for jNetWorks |

### jNetWorks Hardware Backends (Private Repository - Commercial License)

High-performance capture backends supporting up to 800Gbps with hardware acceleration.

| Module            | Description                         |
| ----------------- | ----------------------------------- |
| `jnetworks-dpdk`  | DPDK backend (100Gbps+)             |
| `jnetworks-ntapi` | Napatech SmartNIC backend (800Gbps) |
| `jnetworks-afxdp` | AF_XDP zero-copy backend            |

### Native Bindings (Private Repository)

Low-level Panama FFM bindings. Available for direct use if needed.

| Module               | Description                                   |
| -------------------- | --------------------------------------------- |
| `jnetdpdk-bindings`  | DPDK native bindings via Panama FFM           |
| `jnetntapi-bindings` | Napatech NTAPI native bindings via Panama FFM |
| `jnetafxdp-bindings` | AF_XDP native bindings via Panama FFM         |

## Repository Access

The BOM automatically configures access to the Sly Technologies private Maven repository for enterprise modules:

```xml
<repositories>
    <repository>
        <id>slytechs-nexus</id>
        <url>https://maven.slytechs.com/repository/releases/</url>
    </repository>
</repositories>
```

For private module access, configure credentials in your `~/.m2/settings.xml`:

```xml
<servers>
    <server>
        <id>slytechs-nexus</id>
        <username>your-username</username>
        <password>your-token</password>
    </server>
</servers>
```

## Managed Plugin Versions

The BOM also manages build plugin versions for consistent builds:

| Plugin                  | Version |
| ----------------------- | ------- |
| `maven-compiler-plugin` | 3.12.1  |
| `maven-surefire-plugin` | 3.2.5   |
| `maven-jar-plugin`      | 3.3.0   |

## Managed Test Dependencies

| Dependency             | Version |
| ---------------------- | ------- |
| `junit-jupiter`        | 5.10.2  |
| `junit-platform-suite` | 1.10.2  |

## Requirements

- **Java 22+** - Required for Panama FFM support
- **Maven 3.8+** or **Gradle 8.0+**

## Common Usage Patterns

### Quick Start with jNetPcap (Recommended)

```xml
<dependencies>
    <dependency>
        <groupId>com.slytechs.sdk</groupId>
        <artifactId>jnetpcap-sdk</artifactId>
    </dependency>
</dependencies>
```

### Quick Start with jNetWorks (Recommended)

```xml
<dependencies>
    <dependency>
        <groupId>com.slytechs.sdk</groupId>
        <artifactId>jnetworks-sdk</artifactId>
    </dependency>
</dependencies>
```

### Protocol Analysis Only

```xml
<dependencies>
    <!-- Pick the protocol packs you need -->
    <dependency>
        <groupId>com.slytechs.sdk</groupId>
        <artifactId>sdk-protocol-tcpip</artifactId>
    </dependency>
    <dependency>
        <groupId>com.slytechs.sdk</groupId>
        <artifactId>sdk-protocol-web</artifactId>
    </dependency>
    <dependency>
        <groupId>com.slytechs.sdk</groupId>
        <artifactId>sdk-protocol-infra</artifactId>
    </dependency>
</dependencies>
```

### High-Performance with jNetWorks + DPDK (Commercial)

```xml
<dependencies>
    <dependency>
        <groupId>com.slytechs.sdk</groupId>
        <artifactId>jnetworks-api</artifactId>
    </dependency>
    <dependency>
        <groupId>com.slytechs.sdk</groupId>
        <artifactId>jnetworks-dpdk</artifactId>
    </dependency>
</dependencies>
```

### Hardware-Accelerated with Napatech (Commercial)

```xml
<dependencies>
    <dependency>
        <groupId>com.slytechs.sdk</groupId>
        <artifactId>jnetworks-api</artifactId>
    </dependency>
    <dependency>
        <groupId>com.slytechs.sdk</groupId>
        <artifactId>jnetworks-ntapi</artifactId>
    </dependency>
</dependencies>
```

## Version History

| Version | Release Date | Notes                                            |
| ------- | ------------ | ------------------------------------------------ |
| 3.0.0   | 2025         | Major refactor: Panama FFM, new module structure |
| 2.x     | 2024         | Legacy JNI-based releases                        |

## License

Licensed under the Sly Technologies License. See [LICENSE](https://claude.ai/chat/LICENSE) for details.

## Related Projects

- [jnetpcap-api](https://github.com/slytechs-repos/jnetpcap-api) - High-level packet capture API
- [sdk-common](https://github.com/slytechs-repos/sdk-common) - Core utilities and memory management
- [sdk-protocol-core](https://github.com/slytechs-repos/sdk-protocol-core) - Protocol dissection framework

------

**Sly Technologies Inc.** - High-performance network analysis solutions

Website: [www.slytechs.com](https://www.slytechs.com/)
