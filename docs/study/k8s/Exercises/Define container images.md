---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Define container images.md'
---
# Define container images
Note Created: 2023-02-26

## Lab 

Create container image file - Dockerfile for sample python application

```python
1 #!/usr/bin/python3
2 ## Import the necessary modules
3 import time
4 import socket
5
6 ## Use an ongoing while loop to generate output
7 while True :
8
9 ## Set the hostname and the current date
10 host = socket.gethostname()
11 date = time.strftime("%Y-%m-%d %H:%M:%S")
12
13 ## Convert the date output to a string
14 now = str(date)
15
16 ## Open the file named date in append mode
17 ## Append the output of hostname and time
18 f = open("date.out", "a" )
19 f.write(now + "\n")
20 f.write(host + "\n")
21 f.close()
22
23 ## Sleep for five seconds then continue the loop
24 time.sleep(5)
```

## Solution

```yaml
FROM python:3
ADD simple.py /
## RUN pip install pystrich
CMD [ "python", "./simple.py" ]
```

## Materials
LFD259 exercise 3.1.7