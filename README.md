# CsBlockingQueue

https://JimFawcett.github.io/CsBlockingQueue.html

Thread-safe generic queue that blocks the dequeuing thread when empty.

## Concept

`BlockingQueue<T>` (namespace `SWTools`) coordinates two threads via a shared queue:
- **enQ(T msg)** — enqueues an item and pulses any waiting thread.
- **deQ()** — blocks the caller (using `Monitor.Wait`) until an item is available, then dequeues and returns it.
- **size()** — returns the current number of elements.
- **clear()** — removes all elements.

Synchronization uses a `lock` + `Monitor.Pulse` / `Monitor.Wait`, which is equivalent to a condition variable with a mutex.

## Usage

```csharp
BlockingQueue<string> bQ = new BlockingQueue<string>();
bQ.enQ("hello");
string msg = bQ.deQ();  // blocks if queue is empty
```

## Demo

`Program.cs` (enabled with `TEST_PROGRAM`) spawns a child thread that loops on `deQ()`, while the main thread enqueues 20 messages followed by `"quit"`.

## Build

SDK-style project targeting **net8.0**:

```
dotnet build CS-BlockingQueue/CS-BlockingQueue.csproj
dotnet run --project CS-BlockingQueue/CS-BlockingQueue.csproj
```

## Files

| File | Purpose |
|---|---|
| `CS-BlockingQueue/BlockingQueue.cs` | `BlockingQueue<T>` implementation (namespace `SWTools`) |
| `CS-BlockingQueue/Program.cs` | Test harness (conditional on `TEST_PROGRAM`) |
| `CS-BlockingQueue.sln` | Visual Studio solution |
