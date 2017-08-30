<!-- TITLE: Scribbles -->
<!-- SUBTITLE: Simply various thoughts and ideas -->

# Reducing stack space per event loop fiber
* It's possible to split the stack using fibers!
	* https://www.reddit.com/r/programming/comments/zk05a/a_trip_down_the_gcc_split_stack_rabbithole/c65bezg/
	* Out of stack space? Just lambda onto a new fiber and reference your old variables!
		* EventLoop::stackFiber(cb) to stack a temporary fiber (pooled) onto the current one
* For the IO threadpool, use 4kB stack sizes for simplicity
	* Although appears that Win32 rounds up to 64kB minimum
	* https://msdn.microsoft.com/en-us/library/windows/desktop/ms686774(v=vs.85).aspx