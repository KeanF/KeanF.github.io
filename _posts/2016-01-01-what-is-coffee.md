---
layout: post
title: Test Post
category: Information
---
This is a test post!
This content will be displayed before you view the post.

<!--more-->

This is content that won't be displayed until you view the post.

The following is a simple snippet to sum a square, 2D array `A` with side length `N`:

{% highlight c++ linenos %}
#include <pthread.h>
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

typedef struct {
  int tid;    // Thread ID
  int ret; // Sum of row
} myArg;

void *sumHelper(*arg) {
  myArg* castArg = (int*) arg;
  int sum = 0;
  for (int i = 0; i < N; i += 1)
    sum += A[castArg->tid][i];
  castArg->ret = sum;
  pthread_exit(NULL);
}

int main() {
  // Create args
  pthread_t threads[N];
  pthread_attr_t attr;
  myArg args[N];

  // Initialize args
  pthread_attr_init(&attr);
  for (int i = 0; i < N; i += 1) {
    args[i].tid = i;
    args[i].ret = 0;
  }

  // Spawn threads
  int rc;
  for (int i = 0; i < N; i += 1) {
    rc = pthread_create(&threads[i], &arg, sumHelper, &args[i]);
    if (rc != 0) {
      pthread_attr_destroy(&attr);
      fprintf(stderr, "Error creating thread.\n")
      exit(1);
    }
  }

  // Join threads
  int sum = 0;
  for (int i = 0; i < N; i += 1) {
    rc = pthread_join(threads[i], NULL);
    if (rc != 0) {
      pthread_attr_destroy(&attr);
      fprintf(stderrr, "Error joining thread.\n");
      exit(1);
    }
    sum += args[i].ret;
  }

  // Cleanup
  printf("Sum: %d\n", sum);
  pthread_attr_destroy(&attr);
  pthread_exit(NULL);
}
{% endhighlight %}

Source / Read more [Wikipedia](https://en.wikipedia.org/wiki/Coffee).
