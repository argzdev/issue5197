# issue 5197
### Issue link
- https://github.com/firebase/firebase-android-sdk/issues/5197
### Summary
- There's a dependency conflict of okhttp in grpc. This causes failure when using an aggregated query e.g. count()
### Steps to reproduce
- Run app
- Click the test button
# Behavior
- Stack trace throws an error.

```
2023-07-31 21:29:02.142 10184-10184 MainActivity            com.argz.issue5197                   D  Count failed: 
      com.google.firebase.firestore.FirebaseFirestoreException: INTERNAL: error in frame handler
        at com.google.firebase.firestore.util.Util.exceptionFromStatus(Util.java:113)
        at com.google.firebase.firestore.remote.FirestoreChannel.exceptionFromStatus(FirestoreChannel.java:283)
        at com.google.firebase.firestore.remote.FirestoreChannel.access$100(FirestoreChannel.java:43)
        at com.google.firebase.firestore.remote.FirestoreChannel$4.onClose(FirestoreChannel.java:257)
        at io.grpc.internal.DelayedClientCall$DelayedListener$3.run(DelayedClientCall.java:489)
        at io.grpc.internal.DelayedClientCall$DelayedListener.delayOrExecute(DelayedClientCall.java:453)
        at io.grpc.internal.DelayedClientCall$DelayedListener.onClose(DelayedClientCall.java:486)
        at io.grpc.internal.ClientCallImpl.closeObserver(ClientCallImpl.java:576)
        at io.grpc.internal.ClientCallImpl.access$300(ClientCallImpl.java:70)
        at io.grpc.internal.ClientCallImpl$ClientStreamListenerImpl$1StreamClosed.runInternal(ClientCallImpl.java:757)
        at io.grpc.internal.ClientCallImpl$ClientStreamListenerImpl$1StreamClosed.runInContext(ClientCallImpl.java:736)
        at io.grpc.internal.ContextRunnable.run(ContextRunnable.java:37)
        at io.grpc.internal.SerializingExecutor.run(SerializingExecutor.java:133)
        at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:462)
        at java.util.concurrent.FutureTask.run(FutureTask.java:266)
        at java.util.concurrent.ScheduledThreadPoolExecutor$ScheduledFutureTask.run(ScheduledThreadPoolExecutor.java:301)
        at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1167)
        at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:641)
        at com.google.firebase.firestore.util.AsyncQueue$SynchronizedShutdownAwareExecutor$DelayedStartFactory.run(AsyncQueue.java:235)
        at java.lang.Thread.run(Thread.java:923)
      Caused by: io.grpc.StatusException: INTERNAL: error in frame handler
        at io.grpc.Status.asException(Status.java:547)
        at com.google.firebase.firestore.util.Util.exceptionFromStatus(Util.java:111)
        at com.google.firebase.firestore.remote.FirestoreChannel.exceptionFromStatus(FirestoreChannel.java:283) 
        at com.google.firebase.firestore.remote.FirestoreChannel.access$100(FirestoreChannel.java:43) 
        at com.google.firebase.firestore.remote.FirestoreChannel$4.onClose(FirestoreChannel.java:257) 
        at io.grpc.internal.DelayedClientCall$DelayedListener$3.run(DelayedClientCall.java:489) 
        at io.grpc.internal.DelayedClientCall$DelayedListener.delayOrExecute(DelayedClientCall.java:453) 
        at io.grpc.internal.DelayedClientCall$DelayedListener.onClose(DelayedClientCall.java:486) 
        at io.grpc.internal.ClientCallImpl.closeObserver(ClientCallImpl.java:576) 
        at io.grpc.internal.ClientCallImpl.access$300(ClientCallImpl.java:70) 
        at io.grpc.internal.ClientCallImpl$ClientStreamListenerImpl$1StreamClosed.runInternal(ClientCallImpl.java:757) 
        at io.grpc.internal.ClientCallImpl$ClientStreamListenerImpl$1StreamClosed.runInContext(ClientCallImpl.java:736) 
        at io.grpc.internal.ContextRunnable.run(ContextRunnable.java:37) 
        at io.grpc.internal.SerializingExecutor.run(SerializingExecutor.java:133) 
        at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:462) 
        at java.util.concurrent.FutureTask.run(FutureTask.java:266) 
        at java.util.concurrent.ScheduledThreadPoolExecutor$ScheduledFutureTask.run(ScheduledThreadPoolExecutor.java:301) 
        at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1167) 
        at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:641) 
        at com.google.firebase.firestore.util.AsyncQueue$SynchronizedShutdownAwareExecutor$DelayedStartFactory.run(AsyncQueue.java:235) 
        at java.lang.Thread.run(Thread.java:923) 
      Caused by: java.lang.NoSuchMethodError: No interface method getBuffer()Lokio/Buffer; in class Lokio/BufferedSource; or its super classes (declaration of 'okio.BufferedSource' appears in /data/app/~~VVrZq1RCO6t3k_i3oSUNRg==/com.argz.issue5197-djjLy7PA7jr0cloYPQG5JA==/base.apk!classes5.dex)
        at io.grpc.okhttp.OkHttpClientTransport$ClientFrameHandler.data(OkHttpClientTransport.java:1146)
        at io.grpc.okhttp.internal.framed.Http2$Reader.readData(Http2.java:236)
        at io.grpc.okhttp.internal.framed.Http2$Reader.nextFrame(Http2.java:148)
        at io.grpc.okhttp.OkHttpClientTransport$ClientFrameHandler.run(OkHttpClientTransport.java:1105)
        at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1167)
        at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:641)
        at java.lang.Thread.run(Thread.java:923) 
```
