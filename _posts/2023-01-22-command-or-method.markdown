---
layout: post
title:  "When to send a command or call a method?"
date:   2023-01-22 17:00:00 +0100
categories: api design
---
A command and a method have a common semantic:  
Based on the input data, execute some logic and return a result.  
But there are fundamental semantics differences between the two:  
A method implies that the behaviour is local and immediate: the logic is executed locally and start immediately.  
The method logic can fail, but calling a method never fails (yes, in practice calling a method can fail, but let's not take these sort edge case for our API design).  
A command doesn't imply that. A command can be serialised (or not), and run locally, or remotely, right now, or later.  

# About RPC:

This is why I think RPC is not a good thing.  
I believe this semantic difference is a good thing to keep.  
RPC try to blur the boundaries and destroy this healthy semantic.  
Yes, it may have worked previously for 
Calling an RPC method can fail if the remote is not available, and a method doesn't convey this semantic.  
Because the execution of a RPC method may be remote, calling it may fails, is not local, and is not immediate.  
We lost all the semantics of the method, therefore it should be a command.
