+++
title = "What Is X Where X Is Docker's Image?"
author = ["Anak Wannaphaschaiyong"]
tags = ["docker", "blog", "docker-image"]
draft = false
+++

-   Edit log
    -   <span class="timestamp-wrapper"><span class="timestamp">[2022-07-25 Mon]</span></span>

I was following "What's A Docker Image Anyway?"&nbsp;[^fn:1], but found that its content is no longer true, there are new changes to metadata of docker image, so I write this blog to reflect the changes that I observed at the time of writing.

```sh
docker -v
```

|                         |               |
|-------------------------|---------------|
| Docker version 20.10.17 | build 100c701 |

I write the following Dockerfile.

```Dockerfile
FROM ubuntu

RUN echo hihi
RUN touch /hi
RUN rm /hi
CMD ["echo", "hello"]
```

I build container from Dockerfile above as followed

```sh
docker build -t scratch/example1
```

This can be validated by running the following.

```sh
docker history scratch/example1
```

| IMAGE        | CREATED | CREATED | BY      | SIZE    | COMMENT |       |                      |                        |          |    |                        |
|--------------|---------|---------|---------|---------|---------|-------|----------------------|------------------------|----------|----|------------------------|
| fe1071a1af53 | 30      | hours   | ago     | CMD     | echo    | hello | 0B                   | buildkit.dockerfile.v0 |          |    |                        |
| 30           | hours   | ago     | RUN     | /bin/sh | -c      | rm    | /hi                  | #                      | buildkit | 0B | buildkit.dockerfile.v0 |
| 30           | hours   | ago     | RUN     | /bin/sh | -c      | touch | /hi                  | #                      | buildkit | 0B | buildkit.dockerfile.v0 |
| 30           | hours   | ago     | RUN     | /bin/sh | -c      | echo  | hihi                 | #                      | buildkit | 0B | buildkit.dockerfile.v0 |
| 5            | months  | ago     | /bin/sh | -c      | #(nop)  | CMD   | bash                 | 0B                     |          |    |                        |
| 5            | months  | ago     | /bin/sh | -c      | #(nop)  | ADD   | <3ccf747d646089ed7>… | 72.8MB                 |          |    |                        |

To inspect what is going on underneath `docker build`, I save created image into tar file as followed&nbsp;[^fn:2].

```sh
docker save --output scratch_example1 scratch/example1
```

`scratch-example1.tar` contains the following

```tar
 drwxr-xr-x       0/0             0 167845793a0de123dc4c161f88156bc5f251e60b980a4c05c2d4614ba3f92b0f/
 -rw-r--r--       0/0             3 167845793a0de123dc4c161f88156bc5f251e60b980a4c05c2d4614ba3f92b0f/VERSION
 -rw-r--r--       0/0           477 167845793a0de123dc4c161f88156bc5f251e60b980a4c05c2d4614ba3f92b0f/json
 -rw-r--r--       0/0          1536 167845793a0de123dc4c161f88156bc5f251e60b980a4c05c2d4614ba3f92b0f/layer.tar
 drwxr-xr-x       0/0             0 1fdea14b213c2f3f88f5a2eb66244810fceea42d7c1228fbbda7d686c8589d41/
 -rw-r--r--       0/0             3 1fdea14b213c2f3f88f5a2eb66244810fceea42d7c1228fbbda7d686c8589d41/VERSION
 -rw-r--r--       0/0           876 1fdea14b213c2f3f88f5a2eb66244810fceea42d7c1228fbbda7d686c8589d41/json
 -rw-r--r--       0/0          1536 1fdea14b213c2f3f88f5a2eb66244810fceea42d7c1228fbbda7d686c8589d41/layer.tar
 drwxr-xr-x       0/0             0 5fe796f180a876bb11d1a67d07372506b71b6a525d50f3fb90bb372595100380/
 -rw-r--r--       0/0             3 5fe796f180a876bb11d1a67d07372506b71b6a525d50f3fb90bb372595100380/VERSION
 -rw-r--r--       0/0           477 5fe796f180a876bb11d1a67d07372506b71b6a525d50f3fb90bb372595100380/json
 -rw-r--r--       0/0          1024 5fe796f180a876bb11d1a67d07372506b71b6a525d50f3fb90bb372595100380/layer.tar
 drwxr-xr-x       0/0             0 d85e86bc213d877934da6a64515dfaa38bdf4c979ce33e7dbcb0b58fd8d00bbd/
 -rw-r--r--       0/0             3 d85e86bc213d877934da6a64515dfaa38bdf4c979ce33e7dbcb0b58fd8d00bbd/VERSION
 -rw-r--r--       0/0           401 d85e86bc213d877934da6a64515dfaa38bdf4c979ce33e7dbcb0b58fd8d00bbd/json
 -rw-r--r--       0/0       75153920 d85e86bc213d877934da6a64515dfaa38bdf4c979ce33e7dbcb0b58fd8d00bbd/layer.tar
 -rw-r--r--       0/0          1362 fe1071a1af5308e79164f7533e0a4b910d15f278dfdaa6245fc6ffddfb8e119c.json
 -rw-r--r--       0/0           513 manifest.json
 -rw-r--r--       0/0            99 repositories
```

Metadata of images layers are contained in `manifest.json`.

<a id="code-snippet--4098582197"></a>
```json
[
  {
    "Config": "fe1071a1af5308e79164f7533e0a4b910d15f278dfdaa6245fc6ffddfb8e119c.json",
    "RepoTags": [
      "scratch/example1:latest"
    ],
    "Layers": [
      "d85e86bc213d877934da6a64515dfaa38bdf4c979ce33e7dbcb0b58fd8d00bbd/layer.tar",
      "5fe796f180a876bb11d1a67d07372506b71b6a525d50f3fb90bb372595100380/layer.tar",
      "167845793a0de123dc4c161f88156bc5f251e60b980a4c05c2d4614ba3f92b0f/layer.tar",
      "1fdea14b213c2f3f88f5a2eb66244810fceea42d7c1228fbbda7d686c8589d41/layer.tar"
    ]
  }
]
```

Inspecting `[hash]/layer.json`, it is clear that `[hash]/layer.json` contains meta data of layers which are created by command in Dockerfile e.g. RUN, CMD, etc. `[hash]/layer.json` has id and parent. Example of `[hash]/layer.json` is shown in <233064065>

<a id="code-snippet--233064065"></a>
```json
{
  "id": "167845793a0de123dc4c161f88156bc5f251e60b980a4c05c2d4614ba3f92b0f",
  "parent": "5fe796f180a876bb11d1a67d07372506b71b6a525d50f3fb90bb372595100380",
  "created": "1970-01-01T00:00:00Z",
  "container_config": {
    "Hostname": "",
    "Domainname": "",
    "User": "",
    "AttachStdin": false,
    "AttachStdout": false,
    "AttachStderr": false,
    "Tty": false,
    "OpenStdin": false,
    "StdinOnce": false,
    "Env": null,
    "Cmd": null,
    "Image": "",
    "Volumes": null,
    "WorkingDir": "",
    "Entrypoint": null,
    "OnBuild": null,
    "Labels": null
  },
  "os": "linux"
}
```

New layer builds on top of previous layer where new layer contain a diff to the previous layer (Docker uses copy-on-write filesystem)&nbsp;[^fn:3]. From youngest layer to oldest layer depth (top to bottom), we get the following <4880184960> which align with content of `manifest.json` in <4098582197>.

<a id="code-snippet--4880184960"></a>
```org
1fd...
57e...
167...
d85...
```

`[hash].json` contains meetadata of `Dockerfile`, see <291829122>

<a id="code-snippet--291829122"></a>
```json
{
  "architecture": "amd64",
  "config": {
    "Env": [
      "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
    ],
    "Cmd": [
      "echo",
      "hello"
    ],
    "ArgsEscaped": true,
    "OnBuild": null
  },
  "created": "2022-07-24T19:35:13.8021321Z",
  "history": [
    {
      "created": "2022-02-02T02:14:45.667699167Z",
      "created_by": "/bin/sh -c #(nop) ADD file:3ccf747d646089ed7fbb43c40c45dd43e86f0674115f856efada93c7e4a63624 in / "
    },
    {
      "created": "2022-02-02T02:14:46.177066251Z",
      "created_by": "/bin/sh -c #(nop)  CMD [\"bash\"]",
      "empty_layer": true
    },
    {
      "created": "2022-07-24T19:35:10.4043161Z",
      "created_by": "RUN /bin/sh -c echo hihi # buildkit",
      "comment": "buildkit.dockerfile.v0"
    },
    {
      "created": "2022-07-24T19:35:12.1260549Z",
      "created_by": "RUN /bin/sh -c touch /hi # buildkit",
      "comment": "buildkit.dockerfile.v0"
    },
    {
      "created": "2022-07-24T19:35:13.8021321Z",
      "created_by": "RUN /bin/sh -c rm /hi # buildkit",
      "comment": "buildkit.dockerfile.v0"
    },
    {
      "created": "2022-07-24T19:35:13.8021321Z",
      "created_by": "CMD [\"echo\" \"hello\"]",
      "comment": "buildkit.dockerfile.v0",
      "empty_layer": true
    }
  ],
  "os": "linux",
  "rootfs": {
    "type": "layers",
    "diff_ids": [
      "sha256:36ffdceb4c77bf34325fb695e64ea447f688797f2f1e3af224c29593310578d2",
      "sha256:5f70bf18a086007016e948b04aed3b82103a36bea41755b6cddfaf10ace3c6ef",
      "sha256:04dc7596c93f628a30235c38a4a33cf35eab61b48b6cccda83b83ae8646021e1",
      "sha256:2c751040e46bbe19f7caf612d68652d5b5772dc3bca11d93f86fa888087217d2"
    ]
  }
}
```


## docker images {#docker-images}

Docker image contains information on what changed to the images it's based on. Each image has a parent unless the image is "scratch" image&nbsp;[^fn:4].

-   container images compose of base OS + application + user libraries.
-   base OS is not a full-blown OS.
-   images contains binaries and data in a read-only files system.
    -   a read-write layer is added when the contianer runs.

[how to create docket images?]

[^fn:1]: [What's A Docker Image Anyway](https://vsupalov.com/whats-a-docker-image/)
[^fn:2]: Alternatively, you can use `dive`. In [dive github readme](https://github.com/wagoodman/dive), dive is described as "A tool for exploring a docker image, layer contents, and discovering ways to shrink the size of your Docker/OCI image."
[^fn:3]: As of <span class="timestamp-wrapper"><span class="timestamp">[2022-07-25 Mon]</span></span>, I am not sure if new layer still only contain diff. I add a footnote to be precise on information that I am not 100 percent certain.
[^fn:4]: [What Are Docker Image Layers?](https://vsupalov.com/docker-image-layers/#:~:text=Each%20layer%2C%20is%20a%20complete,%2Dfriendly%20name%3Atag%20pair).
