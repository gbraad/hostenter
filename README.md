Hostenter container
===================

Exploring the host VM (e.g. MobyLinuxVM)


Use privileged Alpine chroot
```bash
$ docker run --net=host --ipc=host --uts=host --pid=host -it --security-opt=seccomp=unconfined --privileged --rm -v /:/host alpine /bin/sh
$ chroot /host
```

Use privileged nsenter
```Dockerfile
FROM alpine
MAINTAINER Gerard Braad <me@gbraad.nl>
RUN apk update && \
    apk add util-linux && \
    rm -rf /var/cache/apk/*
ENTRYPOINT ["nsenter", "--target", "1", "--mount", "--uts", "--ipc", "--net", "--pid"]
```

```powershell
PS> docker build -t hostenter .
PS> docker run -it --privileged --pid=host hostenter /bin/sh
···
