<!-- TITLE: sev::FiberLoop -->
<!-- SUBTITLE: Event loop with support for fibers -->

```c_cpp
#include <libsev/fiber_loop.h>
```

Inherits [sev::EventLoop](/classes/sev/event-loop)
# Functions
## Event queue
* void [fiber](/classes/sev/fiber-loop/fiber)(sev::FiberFunction f)
## Fiber synchronization
* void [yieldAwait](/classes/sev/fiber-loop/yield)()
* void [yieldImmediate](/classes/sev/fiber-loop/yield)()
* void [yieldDeferred](/classes/sev/fiber-loop/yield)()