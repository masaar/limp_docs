[Back to Index](/README.md)

# LIMP Docker Image
LIMP had modern approaches in mind with its core design. This includes providing out-of-the-box [`Dockerfile`](https://github.com/masaar/limp/blob/master/Dockerfile) to build [`Docker`](https://www.docker.com) images.

## `Dockerfile` Specs
Current `Dockerfile` is based on `python:3.7` image from [Docker Hub](https://hub.docker.com/) which is based [`Debian Buster`](https://www.debian.org/releases/buster). LIMP `Dockerfile` does the following:
```Dockerfile
# Create new image based on python:3.7 image.
FROM python:3.7
# Change working directory to /usr/src/app.
WORKDIR /usr/src/app
# Expose LIMPd default port 8081.
EXPOSE 8081
# Copy entire LIMP directory contents to image working directory.
COPY . .
# Run LIMP CLI with Install Dependencies Mode.
RUN python limpd.py --install-deps
# Set launch command to 'python limpd.py'. Essentially setting the image purpose is to start LIMPd.
CMD [ "python", "limpd.py" ]
```