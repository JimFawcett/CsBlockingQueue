# CsBlockingQueue

https://JimFawcett.github.io/CsBlockingQueue.html

Thread-safe generic blocking queue for inter-thread communication.

## Overview

`BlockingQueue<T>` (namespace `SWTools`) wraps a `System.Collections.Queue` with a `Monitor`-based lock. A consumer thread calling `deQ()` blocks when the queue is empty and wakes automatically when a producer calls `enQ()`.

## Public Interface

```csharp
BlockingQueue<string> bQ = new BlockingQueue<string>();

bQ.enQ(msg);          // enqueue; unblocks any waiting deQ
string msg = bQ.deQ(); // dequeue; blocks until an item is available
int n = bQ.size();    // current number of items
bQ.clear();           // remove all items
```

## Build & Run

Requires the [.NET 10 SDK](https://dotnet.microsoft.com/download).

```
cd CS-BlockingQueue
dotnet run
```

The `Debug` configuration defines `TEST_BLOCKINGQUEUE`, which enables the demo
`Main` in `BlockingQueue.cs`. It launches a child thread that dequeues 20
messages sent by the main thread, then exits on a `"quit"` sentinel.

## Files

| File | Description |
|------|-------------|
| `CS-BlockingQueue/BlockingQueue.cs` | `BlockingQueue<T>` implementation + demo `Main` |
| `CS-BlockingQueue/Program.cs` | Alternate test harness (enabled by `TEST_PROGRAM`) |
| `CS-BlockingQueue/CS-BlockingQueue.csproj` | SDK-style project file targeting `net10.0` |

## Author

Jim Fawcett, Syracuse University
