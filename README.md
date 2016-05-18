# ~~Official~~ Jenkins Docker image

This is a fork enabling SSH authentication with keys inside Jenkins jobs.

For official and original instructions: see https://github.com/jenkinsci/docker.
For usage, see below.

# Usage

The simplest way is to use [whilp/ssh-agent](https://github.com/whilp/ssh-agent) with this image.

Considering SSH identities are found in '~/.ssh/'.

Start a shared ssh-agent:
```console
docker run -d --name=ssh-agent whilp/ssh-agent:latest
```

Add an identity to this shared ssh-agent:
```console
docker run --rm -it --volumes-from=ssh-agent -v ~/.ssh:/ssh whilp/ssh-agent:latest ssh-add /ssh/<key>
```

Start Jenkins
```console
docker run -d --name jenkins --volumes-from=ssh-agent -e SSH_AUTH_SOCK=/root/.ssh/socket -v ~/.ssh:/ssh -p 8080:8080 debovema/jenkins-docker-with-ssh:latest
```

