---
title: My First Post
subtitle:
date: 2023-09-12T14:14:14-07:00
draft: true
author:
  name:
  link:
  email:
  avatar:
description:
keywords:
license:
comment: false
weight: 0
tags:
  - draft
categories:
  - draft
hiddenFromHomePage: false
hiddenFromSearch: false
summary:
resources:
  - name: featured-image
    src: featured-image.jpg
  - name: featured-image-preview
    src: featured-image-preview.jpg
toc: true
math: false
lightgallery: false
password:
message:
repost:
  enable: true
  url:

# See details front matter: https://fixit.lruihao.cn/documentation/content-management/introduction/#front-matter
---
As the title of my homepage suggests, this is a blog inspired by a recent _ah-ha!_ moment. Getting myself prepared for this class (which starts tommorow), I have been taking some prep classes focusing on Linux. When I was about half way through a very good bash scripting class at udemy, the instructor walks students through a bash script that is _less_ than 20 lines of code. And 3 things occured to me all at once:

1.  For < 20 lines of code, this script gets things done, quickly. And well.
2.  In spite of the wonky syntax, I already understood, mostly, what was going on.
3.  By no means an _abstract_ exercise meant to teach syntax, this script (or something very similar) will be something I will likely use in the future--sooner than later.

Wow! So this is where the _revelation_ comes in: I need to build a self-documenting tag-driven journal/adventure/odyssey.....so to speak. And it starts right here, right now with a brief bash script entitled `show-attackers.sh`.

Tanke a look:

Code block (using "boron" theme):
```bash
#!/bin/bash

# Count the number of failed logins by IP address.
# If there are any IPs with over LIMIT , display the count, IP, and location.
LIMIT='10'
LOG_FILE="${1}" # expecting input file of log data as first argument to script execution

# Make sure a file was supplied as an argument.
if [[ ! -e "${LOG_FILE}" ]]
then
  echo "Cannot open log file: ${LOG_FILE}" >&2 # push to standard error stream
  exit 1 # provide non-zero integer to denote failure.
fi

# Display the CSV header.
echo 'Count,IP,Location'

# Loop through the list of failed attempts and corresponding IP addys.
grep Failed syslog-sample | awk '{print $(NF -3)}' | sort | unique -c | sort -nr | while read COUNT IP
do
  # If the number of failed attempts is > the limit, display count, IP, and location.
if [[ "${COUNT}"  -gt "${LIMIT}" ]]
then
  LOCATION=$(geolookup ${IP} | awk -F ', ' '{PRINT $2}')
  echo "${COUNT}, ${IP}, ${LOCATION}"
fi
done
exit 0   # Provide zero exit status denoting success.
```

Quote:

> "Brevity is the soul of wit."  
> \-- _William Shakespeare_

I reckon it is time to get busy. And briefly.

