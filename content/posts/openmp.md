---
title: "OpenMP: A step into code parallelisation"
date: "2026-11-17"
draft: false
description: "You'll learn to use OpenMP and how it allows you to optimize your code with the concept of parallel programming."
showToc: true
tags: ["parallelisation", "openmp", "programming", "scripting"]
---

![OpenMP](/openmp/openmp-banner.webp)


## Introduction

Traditionally, there existed various forms of proprietary vendor-specific multi-threading APIs that aimed to achieve shared-memory parralel programming via complex low-level programming. This forced every program to be written with these complex low-level components.

Hence, various vendors: *(SiliconGraphics, IBM, DEC, Intel etc.)* came together to establish a common API for shared-memory parallelisation. OpenMP allowed developers to use simple compiler directives (pragmas) to scale applications portably across multi-core systems.

At the end of this blog you'll be able to write programs using openMP to make them more efficient using the concept of shared-memory parallel programming.

## The Fork-Join Concurrency Model

This model is the basis of what OpenMP does and how it is used to parallelize code.

The act of forking in computing means to make a copy of something. In this case, we'll be making a copy of our code and then using that copy to do a task on some piece of data.

We can fork many times for different pieces of data as we need.

A simple analogy to understand this concept is

- Imagine a long stream of a river that is flowing continuously.
- A farmer splits a segment of this stream and redirects it to turn a turbine.
- This turbine does some work using the stream, and then the stream returns back to the river.

In the above example, the splitting of the river was forking. The split stream doing work on the turbine was the forked thread doing its work, and the stream returning to the river demonstrates how every forked thread joins back to the main stream after it has done its work.

The diagram looks something like below:

![Fork Join Model](https://parallelcomputingsite.wordpress.com/wp-content/uploads/2017/04/fork_join_model.png)

*Image Source: [here](https://parallelcomputingsite.wordpress.com/2017/04/17/fork-join-in-open-mp/)*

## The Concept of Shared Memory

Now that we've understood the fork-join model, we must understand yet another concept of shared memory access.

The basis of this concept says that the memory is unified. When many threads are forked to do some task on different pieces of data, they are all accessing the same memory.

This means that two threads can be working on the same piece of data at the same time, and if thread A updates the data, thread B immediately sees this change.

However, this simultaneous memory access leads to a problem called "Race Condition", as we'll see in the next section of this post.

## The Problem of Race Conditions

A race condition occurs when a forked thread To access a piece of data at the same time, another forked thread is either updating it or reading it.

This causes thread A to read an updated value or an old value depending on when it accessed that value.

The main thing about race conditions is that the problems they cause can be random. It can either be data corruption, a miscalculation from the data, or an error that could occur later on due to wrong data.

This is because each thread can either finish their task faster than others or later than others. Hence, the problem can vary in each run of the program.

The solution to this problem will be discussed later on once we've looked at OpenMP's compiler directives.

---

## Integrating OpenMP into Programs

Finally! Lets start integrating OpenMP into our code!

However... Before we do that, I'd like for you to know what compiler directives are as they are the basis of how we tell OpenMP what to do.

### Compiler Directives

These are special lines in our code that the compiler processes during the time of code compilation, and it then compiles the final machine binary according to such instructions. These usually start with `#` and since I'll be using `C++` for the demonstration of OpenMP, here is an example below of a compiler directive you've already used!

🥁 *Drum Roll...* It is... {{< spoiler >}}# include{{</ spoiler >}}

The above directive essentially makes the compiler move every definition and function into the main file itself, and then it compiles the main binary using that (the actual code file is never touched).

In a similar way another directive such as `# define` exists. Whenever you define a macro using this directive and use it somewhere, the compiler directly takes the value from this macro and pastes it where it is being used like a hardcoded value.

These two are the most commonly used compiler directives in C / C++.

### Including OpenMP in to our Code

OpenMP is super easily to incoporate into our program:

#### 1. Include the OpenMP header file:

```cpp
#include <openmp.h> // <= HERE

// Rest Code here
```

#### 2. Compile the program with OpenMP support

```sh
g++ -fopenmp file.cpp
```

## OpenMP directives

Now that we're all set up, let's start writing our first simple program with OpenMP!

I'll explain the code as we go.

All of our OpenMP directives start with `# pragma` directive. This basically tells the compiler to look at the line of code typed after this block.

In our case, we'll be passing openMP commmands.

### 1. The Loop Directive

The most iterative code we write in C / C++ is with the help of a for loop.

The issue is that a for loop waits for the prior iteration to proceed. When maybe we can save that time by parallelizing it!

Normally, that would take significant changes to the code. However, OpenMP has a directive that automatically does all of the splitting and everything for us.

Let's have a look at the example below:

```cpp
#pragma omp parallel for
for (int i = 0; i < 1000; i++) {
    // Each thread handles a chunk of these iterations simultaneously
    process_data(i);
}
```

Here the "`omp parallel for`" is the compiler directive.

Here, because the CPU cores vary from system to system, mostly for a large number of iterations, OpenMP groups the number of iterations by dividing the number of total iterations by the total number of threads to equally split them per thread.

So in the above case, assuming a system with 4 CPU threads, OpenMP splits the threads into the following groups:

- Core 0: `0 - 249`
- Core 1: `250 - 499`
- Core 2: `500 - 749`
- Core 3: `750 - 999`

Each core runs its own assigned block as a normal, continuous sequence in its local cache, hence making it fast.

### 2. The Critical Directive

With the above example, say if we were calculating a sum and all the threads calculate the sum into the same variable, a race condition occurs.

To deal with that, we use the omp critical directive:

```cpp
int total_sum = 0;

#pragma omp parallel for
for (int i = 0; i < 100; i++) {
    int val = compute(i);
    
    #pragma omp critical
    {
        // Only one thread enters here at a time to safely update total_sum
        total_sum += val;
    }
}
```

Here the critical directive only lets one thread work on the variable at a time. This makes sure that threads don't overwrite each other's content.

### 3. The Reduction Directive

While using the critical directive eliminates the race condition problem, it creates another: the slowdown.

Having to wait for one thread to complete its task on the variable slows things down because other threads are waiting to modify the variable when it is being written on by the other.

Hence, the reduction directive solves this. Have a look at the example below:

```cpp
int sum = 0;

#pragma omp parallel for reduction(+:sum)
for (int i = 0; i < 100; i++) {
    sum += i; // No critical block needed; OpenMP handles it behind the scenes
}
```

Unlike the critical directive, this gives each thread its own copy of the sum variable. They each perform their task, and then OpenMP safely merges them in the end.

This results in a much faster and safer result calculation.

### 4. The Single Block

While parrelizing your code yields significant improvements to efficiency, we sometimes need for a piece of code to be handled by only one thread. For example, printing a message to the console.

For that we use the single directive. Have a look at the example below:

```cpp
#pragma omp parallel
 {
    // Every thread runs this
    do_background_work();

    #pragma omp single
    {
        // Only one thread prints this out
        cout << "All background threads have started." << endl;
    }
}
```

The print message is only printed once after all the tasks have completed.

### 5. Variable Scoping: Shared vs Private

By default, every variable available in the scope where the parallel directive is being used is shared. Meaning all threads access the same variable and write to the same variable.

However, sometimes we want each thread to have its own private copy of some data. What this means is that whatever changes it makes to that variable strictly stay with that thread.

Let's have a look at the example below:

```cpp
int x = 10;

#pragma omp parallel private(x)
{
    // Here, 'x' is uninitialized garbage for each thread (or 0 depending on type), 
    // completely independent of the x = 10 outside.
    cout << "Thread " << omp_get_thread_num() << " sees x = " << x << endl;
}
```

The output on my computer was:

```sh
Thread 0 sees x = 0
Thread 1 sees x = 0
Thread 3 sees x = 0
Thread 2 sees x = 0
```

We initialize each value of this variable per thread and process it accordingly.

### 6. The "nowait" Directive

Assume that we have two loops that are each to do their own work.

Traditionally, using the for directive will get things done for loop A and then loop B.

However, loop B will only start its work once the loop A finishes its task. This can lead to unnecessary slowdown. So to allow loop B to work, loop A sets the "`nowait`" directive.

Look at the example below to understand:

```cpp
#pragma omp parallel
{
    #pragma omp for nowait
    for (int i = 0; i < 100; i++) { do_work_a(i); }

    // Threads don't wait here; they immediately jump to work B
    #pragma omp for
    for (int j = 0; j < 100; j++) { do_work_b(j); }
}
```

### 7. The List Goes On...

There are many more directives in OpenMP. However, the ones listed are enough to get you started with OpenMP and to write code in parallel! If you want to learn about OpenMP in more detail, I'll share a link to a YouTube playlist in the summary at the end of the blog.

## OpenMP Functions

OpenMP has various functions that allow us to change the behaviour of how OpenMP does its work or that allow us to manually control parallelisation.

### 1. Setting Number of Threads Explicitly

Say a system has 16 CPU threads in total. However, we would like our work to only be split across 4 threads. We can easily limit the number of threads using: `omp_set_num_threads(int)`.

Look at the example below:

```cpp
#include <iostream>
#include <omp.h>

int main() {
    // Explicitly set OpenMP to use 4 threads
    omp_set_num_threads(4);

    #pragma omp parallel
    {
        int thread_id = omp_get_thread_num();
        cout << "Hello from thread " << thread_id << endl;
    }

    return 0;
}
```

This limits the code inside parallel block to only 4 threads!

> Note: You can also use `export OMP_NUM_THREADS=4` to set the number of threads in your shell.

### 2. Getting Total Number of Threads in a Block

We can use `omp_get_num_threads()` to get total number of threads in the active block.

For example:

```cpp
#include <iostream>
#include <omp.h>

using namespace std;

int main() {
    // Explicitly request 4 threads
    omp_set_num_threads(4);

    #pragma omp parallel
    {
        // This will print 4 because we forced it above
        cout << "Active threads in team: " << omp_get_num_threads() << endl;
    }

    return 0;
}
```

### 3. Getting A Specific thread's ID

If you'd like to know about a specific thread's ID, you can use: `omp_get_thread_num()`. This ID ranges from 0 to n-1, where n is the total number of threads.

For Example:
```cpp
#include <iostream>
#include <omp.h>

using namespace std;

int main() {
    #pragma omp parallel
    {
        int thread_id = omp_get_thread_num();
        
        if (thread_id == 0) {
            cout << "Hello from the master thread (0)!\n";
        } else {
            cout << "Hello from worker thread " << thread_id << "\n";
        }
    }

    return 0;
}
```
### 4. Getting Maximum Number of Threads

Returns the maximum number of threads OpenMP would use if a parallel region were created right now. This depends on the system hardware or if the threads were set via a environment variable.

```cpp
#include <iostream>
#include <omp.h>

using namespace std;

int main() {
    // Called outside any parallel region
    int max_threads = omp_get_max_threads();
    cout << "Maximum available threads on this system: " << max_threads << endl;

    return 0;
}
```

### 5. Calculating Time Elapsed for a Task

Let's say you want to measure how much time a task took. You can easily do so with: `omp_get_wtime()`. It returns a high-resolution wall-clock timer in seconds. It is usually used for benchmarking purposes since C / C++'s own timer.h isn't accurate enough.

Here is an example of it being used:

```cpp
#include <iostream>
#include <omp.h>

using namespace std;

int main() {
    double start_time = omp_get_wtime();

    // Simulate heavy workload
    #pragma omp parallel for
    for (int i = 0; i < 1000000; i++) {
        volatile double x = i * 0.5; // dummy work
    }

    double end_time = omp_get_wtime();
    
    cout << "Loop took " << (end_time - start_time) << " seconds to execute.\n";

    return 0;
}
```

The output of this code on my system was:

```sh
Loop took 0.00350171 seconds to execute.
```

It may differ from yours depending on the number of CPU threads and their speed.

---

## Summary

You should now be able to write simple parallelized programs using OpenMP by using the concepts taught in this post.

While I certainly did not cover the details in depth about OpenMP, the main aim of this post was to get you started with basic concepts.

If you'd like to learn more about OpenMP in detail, you can check out this playlist: **[here](https://www.youtube.com/watch?v=nE-xN4Bf8XI&list=PLLX-Q6B8xqZ8n8bwjGdzBJ25X2utwnoEG)**.

**Happy Coding!** 💻