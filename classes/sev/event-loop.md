<!-- TITLE: sev::EventLoop -->
<!-- SUBTITLE: Event Loop -->

```c_cpp
#include <libsev/event_loop.h>
```

Inherits [sev::EventLoopBase](/classes/sev/event-loop-base)
# Functions
## Loop control
* void [run](/classes/sev/event-loop/run)()
* void [run](/classes/sev/event-loop/run)(sev::EventFunction f)
* void [run](/classes/sev/event-loop/run)(std::function\<void(sev::EventLoop \*el)\> f)
* void [runSync](/classes/sev/event-loop/run)()
* void [runSync](/classes/sev/event-loop/run)(sev::EventFunction f)
* void [runSync](/classes/sev/event-loop/run)(std::function\<void(sev::EventLoop \*el)\> f)
* void [stop](/classes/sev/event-loop/stop)()
* void [join](/classes/sev/event-loop/join)(bool empty)
## Event queue
* void [immediate](/classes/sev/event-loop/immediate)(sev::EventFunction f)
* void [deferred](/classes/sev/event-loop/deferred)(sev::EventFunction f) // push function into deferred queue
## Queue control
* void [advance](/classes/sev/event-loop/advance)() // flushes deferred queue into immediate queue
* void [clear](/classes/sev/event-loop/clear)()