+++
title = "Running Docker Container With Dockerfile."
author = ["Anak Wannaphaschaiyong"]
tags = ["docker", "blog", "container", "dockerfile"]
draft = false
+++

As an example, the goal is to run container that will download things hosted on the web and run some command DURING a docker launches (using ENTRYPOINT to run the command).

<a id="code-snippet--935413320"></a>
```Dockerfile
FROM ubuntu

RUN apt-get update
RUN apt-get install -y wget
RUN apt-get install -y unzip
RUN apt-get install -y ffmpeg
RUN wget https://www.cse.fau.edu/~hari/sequences/vid-clips.zip
RUN unzip vid-clips.zip
ENTRYPOINT ["ffmpeg" -i" clip-crf20.mp4" -c:v" libx264" -crf" 36" -c:a" copy" clip-out.mp4"]
```

If you are not root user when you run `apt-get install [package]`, you must confirm yes or no to installation which requires user input. On the other hand, `-y` will insert `yes` as user input.

In <935413320>, image `ubuntu` (`FROM ubuntu`) run as root, so `-y` is not needed. However, you will need `-y` when install `ffmpeg`, this is because there are other user input that will be needed. I assume `-y` also accept default options. Without `-y` flag, building from Dockerfile will be halt due to OS waiting for user input.

Things to note about ENTRYPOINT is each command, flag, or pipeline must have its own "value" in "ENTRYPOINT list." According above command <935413320>, the command that you intended to run upon start up container launch is `ffmpeg -i clip-crf20.mp4 -c:v libx264 -crf 36 -c:a copy clip-out.mp4`.

```sh
ffmpeg -i clip-crf20.mp4 -c:v libx264 -r 36 -c:a copy clip-out.mp4
```

`-c` is short for `-coden` which stands for `code encode`. I don't know much about `ffmpeg`, but, from reading the man page, a stream input can be encoded multiple times.

-   `-c:v libx264` means libx264 encoder is applied to all video stream input.
-   `-r 36` means frame rate is set to `36` fps.
-   `-c:a copy` means copy all audio stream.

To run docker using Dockerfile, do the following

```sh
cd [path-to-dir-with-dockerfile]
docker build -t [sometags] .
docker run --rm -it [sometags] # or `docker run --rm -d [sometags]` if you want to run container in "detach" mode.
```

Note that it is a good practice to always use tags.

That's it.
Peace.
