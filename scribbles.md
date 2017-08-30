<!-- TITLE: Scribbles -->
<!-- SUBTITLE: Simply various thoughts and ideas -->

* It's possible to split the stack using fibers!
	* https://www.reddit.com/r/programming/comments/zk05a/a_trip_down_the_gcc_split_stack_rabbithole/c65bezg/
	* Out of stack space? Just lambda onto a new fiber and reference your old variables!
		* EventLoop::stackFiber(cb) to stack a temporary fiber (pooled) onto the current one
* For the IO threadpool, use 4kB stack sizes for simplicity
	* Although appears that Win32 rounds up to 64kB minimum
	* https://msdn.microsoft.com/en-us/library/windows/desktop/ms686774(v=vs.85).aspx
* Half float support
	* Neat
	* http://half.sourceforge.net/
* WinRT
	* https://msdn.microsoft.com/en-us/magazine/dn342867.aspx
	* https://msdn.microsoft.com/en-us/library/hh438466.aspx?ranMID=24542&ranEAID=TnL5HPStwNw&ranSiteID=TnL5HPStwNw-nAzPqQl7W78N8KEGQUOOUQ&tduid=(92d5d6a02dd15b087fb9854d4ffb7e4f)(256380)(2459594)(TnL5HPStwNw-nAzPqQl7W78N8KEGQUOOUQ)()