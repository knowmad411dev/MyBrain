---
tags:
- docker
---
## **Docker Installation & Hello World!

[![Cover image for Day 2: Docker Installation & Hello World!](https://media2.dev.to/dynamic/image/width=1000,height=420,fit=cover,gravity=auto,format=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2F2nriyj9jrz7cori2vnfj.png)](https://media2.dev.to/dynamic/image/width=1000,height=420,fit=cover,gravity=auto,format=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2F2nriyj9jrz7cori2vnfj.png)

This is a crosspost from [adventofdocker.com](https://adventofdocker.com/posts/day-2-installation-hello-world/)

Today we are going to start with the installation of Docker and run our first container! This blog post should take you about 10 minutes.

Docker is available for all major platforms, Windows, Mac, and Linux. It even works on Raspberry Pi! Here's an overview of the supported operating systems:

| Platform | x86\_64 / amd64 | arm64 / aarch64 | arm (32-bit) | ppc64le | s390x |
| --- | --- | --- | --- | --- | --- |
| Debian | ✅ | ✅ | ✅ | ✅ |  |
| Fedora | ✅ | ✅ |  | ✅ |  |
| Raspberry Pi OS |  |  | ✅ |  |  |
| RHEL | ✅ | ✅ |  |  | ✅ |
| SLES |  |  |  |  | ✅ |
| Ubuntu | ✅ | ✅ | ✅ | ✅ |  |
| Binaries | ✅ | ✅ | ✅ |  |  |

The easiest way to get started is to download the Docker Desktop application from the [official website](https://www.docker.com/products/docker-desktop/). Docker Desktop includes everything you need to get started with Docker and even comes with a graphical user interface.

I can't explain it better than the official documentation, so please refer to the official documentation for installation instructions:

-   [Windows](https://docs.docker.com/desktop/setup/install/windows-install/)
-   [Mac](https://docs.docker.com/desktop/setup/install/mac-install/)
-   [Linux](https://docs.docker.com/desktop/setup/install/linux-install/)

Once you have Docker Desktop installed, you can verify the installation by running the following command in your terminal:

You should get a bunch of information about your Docker installation, this is how it looks on my machine:

[![docker info output](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fe7vpuy356jg7rxux9ept.png)](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fe7vpuy356jg7rxux9ept.png)

To make sure that the installation was successful, we are going to run our first container.

For that, again open your terminal and run the following command:

[![docker run output](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fomnag08z8z7zdpy5oip5.png)](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fomnag08z8z7zdpy5oip5.png)

If you see the output above, your Docker installation was successful! 🎉

If not, please comment under this post or reach out to me via mail ([jonas@sliplane.io](mailto:jonas@sliplane.io)) and I will help you out!

## [](https://dev.to/code42cate/day-2-docker-installation-hello-world-50n#whats-next)What's next?

Tomorrow we are going to learn how to build our first container! If you want to get a head start, run `docker help` and have a look at the different commands that Docker offers.

Until tomorrow, happy coding! 🚀

Jonas

[[Docker]]