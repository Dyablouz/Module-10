# Reflection

## Experiment 1.2: Understanding How It Works

![Execution Result](Experiment1.2.png)

The spawner.spawn() call does not run the async task immediately. It only creates a task and puts it into the executor's ready queue. Because of that, the normal synchronous code after spawner.spawn() continues first, so "Nando's Komputer: hey hey hey" is printed before the executor starts running.

