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
## Create the main event loop
Create the main event loop and launch the first function
```c_cpp
#include <stream>
#include <libsev/EventLoop.h>

void f(sev::EventLoop *el)
{
  // Do something
  std::cout << "Hello world\n";
  
  // Stop event loop
  el->stop();
}

int main()
{
  // Create main event loop
  sev::EventLoop *el = new sev::EventLoop();
  
  // Push function call onto queue
  el->immediate([el]() -> {
    f(el);
  });
  
  // Run event loop synchronously on main thread
  el->runSync();
  
  // Clean up
  delete el;
  el = NULL;
}
```
Or in one line using the shorthand version
```c_cpp
#include <stream>
#include <memory>
#include <libsev/EventLoop.h>

void f(EventLoop *el)
{
  // ...
}

int main()
{
  // Create event loop, run synchronously, and call function
  std::make_unique<sev::EventLoop>()->runSync([el]() -> {
    f(el);
  });
}
```
## Order of operations
All events are processed in the order that they are pushed onto the event loop queue. In other words, it's a fifo queue. When using a single threaded event loop, it is guaranteed that all (except fiber) events previously onto the event loop have finished running synchronously when an event runs, and it is similarly guaranteed that the currently running event finishes running before any pushed events start running. The `EventLoop::immediate(...)` function returns immediately.

```c_cpp
#include <stream>
#include <libsev/EventLoop.h>

void f(sev::EventLoop *el)
{
  std::cout << "1\n";
  el->immediate([el]() -> {
    std::cout << "3\n";
    el->immediate[el]()-> {
      std::cout << "6\n";
    };
    std::cout << "4\n";
  });
  el->immediate([el]() -> {
    std::cout << "5\n";
  });
  std::cout << "2\n";
}
```
Output

```text
1
2
3
4
5
6
```

## Thread messaging
A practical application of using event loops is the ability to easily message accross threads without worrying too much about synchronisation.