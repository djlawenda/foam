---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Create Pod with adapter container.md'
---
# Create Pod with adapter container
Note Created: 2023-02-25

## Lab 

Adapter containers standardize and normalize output.  Consider the task of monitoring N different applications.  Each application may be built with a different way of exporting monitoring data. (e.g. JMX, StatsD, application specific statistics) but every monitoring system expects a consistent and uniform data model for the monitoring data it collects.

## Solution

## Materials 
https://kubernetes.io/blog/2015/06/the-distributed-system-toolkit-patterns/#example-3-adapter-containers