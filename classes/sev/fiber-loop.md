<!-- TITLE: sev::FiberLoop -->
<!-- SUBTITLE: Event loop with support for fibers -->

```c_cpp
#include <libsev/fiber_loop.h>
```

Inherits [sev::EventLoop](/classes/sev/event-loop)
# Functions
## Event queue
* void [fiberImmediate](/classes/sev/fiber-loop/fiber)(sev::FiberFunction f)
* void [fiberDeferred](/classes/sev/fiber-loop/fiber)(sev::FiberFunction f)
## Fiber synchronization
* void [yieldAwait](/classes/sev/fiber-loop/yield)(int nb = 1)
* void [yieldImmediate](/classes/sev/fiber-loop/yield)()
* void [yieldDeferred](/classes/sev/fiber-loop/yield)()
* void [respond](/classes/sev/fiber-loop/respond)(int nb = 1)
# Usage
```c_cpp
void f(sev::FiberEvent *fe)
{
  sev::FiberLoop *fl = fe->eventLoop();
  int res1, res2, res3;
  fl->fiber([fe, &res1](sev::FiberEvent *fe1) {
    res1 = 1;
    fe->respond(); // IMPL NOTE: In case multithreaded fiber loop, this may be called before yieldAwait; FiberEvent will contain a signed counter to decide on the await
  });
  fl->fiber([fe, &res2](sev::FiberEvent *fe2) {
    res2 = 2;
    fe->respond();
  });
  other->immediate([fe, &res2](sev::FiberEvent *fe2) { // NOTE: Also possible to use other event loops for responding
    res3 = 3;
    fe->respond(1); // Can also use different response counts
  });
  fl->yieldAwait(3); // Continue once number of responses received
}
```
