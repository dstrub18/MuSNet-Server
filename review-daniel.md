# Review on MuSnet Server

## Overall
- Super fun idea
- Love the combination of domains: Networking + Audio
- If it works, then great


## Improvements
I think the main issue I have is that I can only know if works by the time it runs.
Running it requires docker working correctly, and then it's about going through each use case 1 by 1.
I don't know what these use cases are, so I'd never really know when I'm done. :(

So here's my suggestions on how I'd approach a refactor.

### More build profiles
- This is a heavily multithreaded service.
- I find it notoriously difficult to reason about multithreaded code.
- A build with thread sanitizer would help a lot here.
- It also operates a lot on raw packets, offset juggling, pointer arithmetic. I never get that right the first time around.
- A build with Address Sanitizer would help.

The executable with these build profiles is gonna be slower, but you wouldn't ship that build in a production environment anyways.

A build system helps with making different build configurations (You probably know that already).
I used meson here because I like it the most. Choose what you like best. :)

### Refactoring for injection and testing
This could be a great exercise in refactoring for testability.

Let's take TcpResponse as an example:
- The constructor could take `std::functions` which have the same signature as `send`, `close` etc .
- This way the production TcpResponse takes the system functions, a test could have a different one.

### Memory profiling
- Check out heaptrack! It could be a great use case for detecting temporary allocations.

### Flags in general
- Profiling could be behind a build flag.
- Verboseness and DEBUG on the other hand shouldn't
- Investigate https://en.wikipedia.org/wiki/Syslog. This will give you a configurable log level.

### Diagnostics
- Provide errno on perror, if function sets it
