# Framework

## Core Libraries
### libzircon
- defines the Zircon system ABI
### libzx
- libzircon defines C types and function calls acting on those objects. libzx is a light C++ wrapper around those

### FBL
-  Fuchsia Base Library
- `system/ulib/fbl` which is usable from both kernel and userspace.
- `kernel/lib/fbl` which is usable only from the kernel.
- FBL provides:
  - utility code
    - basic algorithms (zircon/system/ulib/fbl/include/fbl/algorithm.h)
    - atomics
    - alloc checking new (zircon/system/ulib/fbl/include/fbl/alloc_checker.h)
- allocators
  - slab allocation (slab_allocator.h)
  - slab malloc (slab_malloc.h)
- arrays
  - fixed sized arrays (array.h)
  - fixed sized arrays, which stack allocates small arrays (inline_array.h)
- inline containers
  - doubly linked list (intrusive_double_list.h)
  - hash table (intrusive_hash_table.h)
  - singly linked list (intrusive_single_list.h)
  - wavl trees (intrusive_wavl_tree.h)
- smart pointers
  - intrusive refcounted mixin (ref_counted.h)
  - intrusive refcounting pointer (ref_ptr.h)
  - unique pointer (unique_ptr.h)
- raii utilities
  - auto call to run code upon leaving scope (auto_call.h)
  - AutoLock (auto_lock.h)
### FXL
FXL is a platform-independent library containing basic C++ building blocks

## Application model
### FIDL / Fuchsia Interface Definition Language
- the IPC system for Fuchsia

## Sandboxing

## Modules
- A `Module` is a component which displays UI and runs as part of a `Story`.
- Environment
  - A module is given access to two services provided by the modular framework in its incoming namespace:
    - `fuchsia.modular.ComponentContext` which gives the agent access to functionality which is shared across components run under the modular framework (e.g. modules, shells, agents).
    - `fuchsia.modular.ModuleContext` which gives modules access to module specific functionality, like adding other modules to its story and creating entities.
  - A module is expected to provide three services to the modular framework in its outgoing namespace:
    - `fuchsia.ui.app.ViewProvider` which is used to display the module's UI.
    - `fuchsia.modular.Lifecycle` which allows the framework to signal the module to terminate gracefully.
    - `fuchsia.modular.IntentHandler` which allows the framework to send intents to the module.
## Agents
- An Agent is a `singleton-per-session component` which runs outside of the scope of a Story without any graphical UI.
