# Reflection

## Experiment 1.2: Understanding How It Works

![Execution Result](Experiment1.2.png)

The spawner.spawn() call does not run the async task immediately. It only creates a task and puts it into the executor's ready queue. Because of that, the normal synchronous code after spawner.spawn() continues first, so "Nando's Komputer: hey hey hey" is printed before the executor starts running.

## Experiment 1.3: Multiple Spawn and Removing Drop

![Execution Result](Experiment1.3.png)

In this experiment, there are three async tasks. Each task prints a "howdy" message, waits for TimerFuture for about two seconds, and then prints a "done" message.

The "Nando's Komputer: hey hey hey" line appears first because it is normal synchronous code that runs before executor.run() starts polling the queued async tasks. Calling spawner.spawn() only puts each task into the ready queue; it does not execute the task immediately.

After executor.run() starts, the executor polls the queued tasks one by one. Each task prints its "howdy" message, creates a timer, and returns Poll::Pending. When the timers finish, their wakers put the tasks back into the queue so the executor can poll them again and print the "done" messages.
