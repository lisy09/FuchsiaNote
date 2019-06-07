# Zercon Kernal
## Zercon Kernal Concepts
- `Kernal Objects`
  - accessible directly via system calls are C++ classes which implement the Dispatcher interface
  -  implemented in zircon/kernel/object
- `System Calls`
  - almost via `Handles`
  - Handle
    - userspace: 32bit integer(type zx_handle_t)
  - three broad categories, from an access standpoint
    - Calls which have `no limitations`
      - `zx_clock_get()` and `zx_nanosleep()`
    - Calls which take a `Handle` as the `first parameter`, denoting the Object they act upon, which are the vast majority, for example `zx_channel_write()` and `zx_port_queue()`.
    - Calls which `create new Objects` but do not take a Handle, such as `zx_event_create()` and `zx_channel_create()`. Access to these (and limitations upon them) is controlled by the Job in which the calling Process is contained.
  - provide by `libzircon.so` / virtual Dynamic Shared Object/ vDSO
    - C ELF ABI functions
    - defined by syscalls.abigen and processed by the abigen tool 
