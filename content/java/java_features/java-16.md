### Java 16

#### New features

- [Text Blocks](#text-blocks)
- [Records](#records)
- [Sealed class](#sealed-class)
- [Stream API](#stream-api)
- [Pattern matching](#pattern-matching)
- [Strong Encapsulation](#strong-encapsulation)
- [Unix Domain Socket Channels](#unix-domain-socket-channels)
- [ZGC Improvements](#zgc-imrpovements)
- [Alpine Linux Support](#alpine-linux-support)
- [Tooling and JVM Diagnostics Improvements](#tooling-and-jvm-diagnostics-improvements)


### Text blocks
- became stable

### Records
- Records – Final (BIG ONE)

### Sealed class
- Secon preview only (not final yet)

### Stream API
- toList()
- mapMulti

### Pattern Matching
- instanceOf - This feature is now a part of standard delivery

### Strong Encapsulation
This is very important.
- Illegal access to sun.* APIs is blocked by default
- Breaks old libraries using reflection hacks
- Better security

### Unix Domain Socket Channels
***What it is***

Support for Unix domain sockets (local IPC).

Benefits
- Faster than TCP loopback
- Lower latency
- More secure local communication

Typical usage
- Microservices on same machine
- Databases
- High-performance servers

### ZGC Improvements
***Enhancements***
- Reduced memory fooprint
- Better performance on large heaps
- Lower pause times

***Who benefits***
- Large-scale server apps
- Cloud workloads

### Alpine Linux Support

***What it is***

Official JDK builds for Alpine Linux (musl libc).

***Why it matters***

- Smaller Docker images
- Faster container startup
- Cloud-native deployments

### Tooling and JVM Diagnostics Improvements
- Better crash reporting
- Improved JVM logging
- Clearer error messages for illegal access