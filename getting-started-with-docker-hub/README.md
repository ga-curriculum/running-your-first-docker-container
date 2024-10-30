<h1>
  <span class="headline">Running Your First Docker Container</span>
  <span class="subhead">Getting Started with Docker Hub</span>
</h1>

**Learning objective:** By the end of this lesson, students will be able to access Docker Hub to pull images and run their first container.

## What is Docker Hub?

Docker Hub is a cloud-based repository where developers can find and share container images, which serve as templates for creating containers. It hosts both public images, freely accessible to everyone, and private images restricted to specific users or organizations.

Additionally, Docker Hub fosters a community of developers who contribute to and maintain these images, making it a valuable resource for discovering pre-built images for common applications and frameworks.

Before running a container, users often need to pull an image from Docker Hub.

<div class="activity guided-walkthrough">
  <h2 class="title">Run the <code>hello-world</code> Docker Image</h2>
  <span class="minutes">5 min</span>
</div>

The `hello-world` Docker image is a simple, introductory tool for new users to verify that Docker is installed and working correctly. By running it, you can quickly confirm that Docker’s client-server setup, image downloading, and container launching processes are all functioning as expected.

When you execute `docker run hello-world`, Docker will:

- Download the small `hello-world` image from **Docker Hub**.
- Create and start a container that runs a short program displaying a message in the terminal.

### Running Your First Docker Command

1. First, launch your terminal application.

2. Ensure that the **Docker daemon** is running. You may need to start **Docker Desktop** if it isn’t already running.

In the terminal, type the following command:

```bash
docker run hello-world
```

### What Happens?

#### First Run

If this is the first time you’re running the `hello-world` image, Docker will check if it’s available locally. If not, it will pull the image from **Docker Hub**, create a container, and execute it.

You might have even seen an error message initially that looks like this:

```text
Unable to find image 'hello-world:latest' locally
```

<br>

Followed by:

```text
Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.
```

#### Subsequent Runs

If the image is already downloaded, Docker will use the cached image, so you won’t see the “Unable to find image” message.

### Run the Command Again

Run the same command a second time. Notice anything different from the first run?

The second time you will not see the message `Unable to find image 'hello-world:latest' locally`. The image has been cached and is now available locally for future use.
