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
    - Calls which have no limitations
      - 