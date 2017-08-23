<!-- TITLE: libsev -->
<!-- SUBTITLE: Simple Event Loop -->

# Overview
[Repository](https://github.com/libsev/libsev)

# About libsev
Libsev is a library to make lots of code run at the same time in a very specific way, focused on simplicity of use and performance.

The library provides support for
* Single threaded event loops
* Thread pooled event loops
* Event callbacks
* Win32 message loops
* Asynchronous IO streams (IO completion ports)
* Timers
* Fibers
* Human input devices (game controllers)
* ...

# Usage
## Create a main event loop
```c_cpp
#include <stream>
#include <libsev/EventLoop.h>

void f(EventLoop *el)
{
  // Do something
  std::cout << "Hello world\n";
  
  // Stop event loop
  el->stop();
}

int main()
{
  // Create main event loop
  EventLoop *el = new EventLoop();
  
  // Push function call onto queue
  el->push(f);
  
  // Run event loop synchronously on main thread
  el->runSync();
  
  // Clean up
  delete el;
  el = NULL;
}
```
