# refactor: ping tutorial using tokio Issue #5554
> https://github.com/libp2p/rust-libp2p/issues/5554

## Description
By identifying the missing examples and tests for solving #4449 I identified 
that the ping tutorial still uses async-std and there is an already refactored 
tokio ping example. Upon opening, there are some slight differences that might 
require review.

## Motivation
The tokio runtime is much more well established and better maintained. Users 
should be able to use other runtimes or bring their own.[1]

Examples and tests where considered in #4449 but not this tutorial.

## Current Implementation
Both runtimes are being mixed.[1]

## Differences between the ping example and the ping tutorial

### Cargo.toml 

* libp2p missing features from tutorial in the example: "tls", "dns" "websocket", and "macros"
* using latest version of the dependencies (should we use specific versions?)

### src/main.rs 

* SwarmBuilder tcp config does not implement tcp but noise instead
* Ping timeout in the tutorial is 30 seconds while in the example is Duration::from_secs(u64::MAX)

## Change checklist
- [x] I have performed a self-review of my own code
- [x] I have made corresponding changes to the documentation
- [ ] I have added tests that prove my fix is effective or that my feature works
- [ ] A changelog entry has been made in the appropriate crates


## References
1. Prefer tokio runtime everywhere #4449, @thomaseizinger, https://github.com/libp2p/rust-libp2p/issues/4389, 2023-09-04. 

