---
title: "An Introduction to Multithreading"
date: "2026-04-20"
draft: false
description: "In this guide we'll cover the fundamentals of multithreading and discover how it is used for various purposes in coding."
showToc: true
tags: ["python", "multithreading"]
---

![SSH Screenshot](https://miro.medium.com/1*ckEihMg7ZxrzQsL89JGGLA.jpeg)

## Introduction
Multithreading refers to a concept that allows many instructions in our code to be executed concurrently, meaning they execute in the same period of time. These codes run inside a smaller execution unit called threads. While in normal procedural programming, the code ran line by line, with multithreading, you can allow various snippets to run side-by-side, thus achieving efficiency.

## Uses of Multithreading in Python Today
With the growing influence of AI in various workspaces, Python has become very popular for its simplicity. The use of multithreading is vital for I/O based tasks (Input / Output). For example, fetching data through multiple API's at the same time. Though, this concept also exists in various other languages.

---

## Demonstration of Multithreading

I will be showing various examples of how multithreading helps us achieve maximum efficiency with a few code examples, as I'll share below.

### Without Multithreading

Let's take the following code as an example:

```py
# Example of Procedual Programming

def say_hello():
    print("Hello!")

def ask_status():
    print("How are you?")

def say_bye():
    print("Bye!")

say_hello()
ask_status()
say_bye()
```

The output will be as follows

```
Hello!
How are you?
Bye!
```

The output shows that each line executes one-by-one.

In the next following example, let's add delay to each action so that each action performs after a specific period of time:

```python
# Example of Procedual Programming with Delays

import time

def say_hello():
    time.sleep(5)
    print("Hello!")

def ask_status():
    time.sleep(2)
    print("How are you?")

def say_bye():
    time.sleep(3)
    print("Bye!")

say_hello()
ask_status()
say_bye()
```

The program remains mostly unchanged. However, we have imported the time module, and we take a specific amount of time per action before they are completed.

With the above change, each output line appears after a specific amount of time as follows:

```sh
# After 5 Seconds:
Hello!

# After 2 Seconds:
How are you?

# After 3 Seconds:
Bye!
```

In the above example, we've used simple examples with fixed intervals. However, with actual codes, some operations may take longer to finish or finish earlier than others. Hence, we can help these tasks complete concurrently.

### With Multithreading
In Python with the `threading` module, we can allow each function to run in its individual thread.

Let's look at the below example:

```python
# Example of Multithreading
import time

# Import the threading module
import threading

def say_hello():
    time.sleep(5)
    print("Hello!")

def ask_status():
    time.sleep(2)
    print("How are you?")

def say_bye():
    time.sleep(3)
    print("Bye!")

# Create a Thread, and pass the say_hello function as the target for the Thread constructor.
task1 = threading.Thread(target=say_hello)

# Start the Thread
task1.start()

# The control is immidiately transfered here, while the task1 runs in the background

# Same Repeats for the remaining tasks.
task2 = threading.Thread(target=ask_status)
task2.start()

task3 = threading.Thread(target=say_bye)
task3.start()
```

The output now changes, as shown below:

```sh
How are you?
Bye!
Hello!
```

It can be seen that the order of the output is no longer in the same order. However, if we take a look back at our code, we can see that the function `ask_status` takes the least amount of time to complete, while the function `say_hello` takes the most amount of time to complete. Hence, it can be seen that the control is immediately transferred forward to the next line after the thread is started so that the code can continue to execute while the thread completes its task in the background.

---

## Performing an Action After the Completion of All Threads
Let's say we want to print a message to mark the completion of all the tasks. Let's have a look at the code snippet below:

```python
# Example of Performing an Action after Completion of All Tasks

import time
import threading

def say_hello():
    time.sleep(5)
    print("Hello!")

def ask_status():
    time.sleep(2)
    print("How are you?")

def say_bye():
    time.sleep(3)
    print("Bye!")

task1 = threading.Thread(target=say_hello)
task1.start()

task2 = threading.Thread(target=ask_status)
task2.start()

task3 = threading.Thread(target=say_bye)
task3.start()

print("All statements have been said.")
```

The output we get from the above code snippet is:

```python
All statements have been said.
How are you?
Bye!
Hello!
```

It can be seen that the last statement was printed first, before all the tasks were complete. The intended purpose of this snippet was to print the completion message after all the tasks were done. While the functions running simultaneously and allowing other code snippets to execute is a great pro of multithreading, in this scenario it breaks the whole functionality of the program. However, there is a solution for this issue.

Let's look at the code snippet below:

```python
import time
import threading

def say_hello():
    time.sleep(5)
    print("Hello!")

def ask_status():
    time.sleep(2)
    print("How are you?")

def say_bye():
    time.sleep(3)
    print("Bye!")

task1 = threading.Thread(target=say_hello)
task1.start()

task2 = threading.Thread(target=ask_status)
task2.start()

task3 = threading.Thread(target=say_bye)
task3.start()

# Join method waits for the thread to complete it's task beforee continuing with the excecution of code below
task1.join()
task2.join()
task3.join()

print("All statements have been said.")
```

By using the join method on each thread, we wait for those threads to finish before executing the next lines of code.

The output is now as expected:

```sh
How are you?
Bye!
Hello!
All statements have been said.
```

---

## Passing Arguments to Functions
Let's say our functions require a parameter passed to them. For example, the say_hello function:

```python
import time

def say_hello(name):
    time.sleep(5)
    print(f"Hello! {name}")

say_hello("Example")
```

The output will be as follows:

```sh
Hello! Example
```

To pass a parameter, while the function is being run in a thread, it is done as follows:

```python
# Example of Parameter Passing
import time
import threading

def say_hello(name):

    time.sleep(5)
    print(f"Hello! {name}")

def ask_status():
    time.sleep(2)
    print("How are you?")

def say_bye():
    time.sleep(3)
    print("Bye!")

# Pass a Tuple into the Args parameter of the Thread's Constructor
# Note we must end the tuple with a comma.
task1 = threading.Thread(target=say_hello, args=("Example",))
task1.start()

task2 = threading.Thread(target=ask_status)
task2.start()

task3 = threading.Thread(target=say_bye)
task3.start()
```

---

# Summary

Multithreading is a concept that allows your program to "multitask." It allows snippets of code or methods to run independently of the code so that they perform the tasks simultaneously, achieving speed and maximum efficiency.