<h1>
  <span class="headline">Running Your First Docker Container</span>
  <span class="subhead">Creating Custom Docker Images with Dockerfiles</span>
</h1>

**Learning objective:** By the end of this lesson, students will be able to create a Dockerfile to build a custom Docker image.

<br>

<img src="./assets/docker-icon-lg.png" alt="Docker Logo" style="width:400px;"/>

<br>
[source](https://www.loft.sh/blog/11-of-the-best-open-source-kubernetes-tools-2021-edition)

## Introduction to Dockerfiles

So far, we’ve worked with existing images to run containers, but creating a custom image for our application requires a **Dockerfile**.

According to [Docker’s documentation](https://docs.docker.com/engine/reference/builder/#:~:text=A%20Dockerfile%20is%20a%20text,command%2Dline%20instructions%20in%20succession.), a **Dockerfile** is a text file containing instructions for Docker to follow when building an image. Each instruction in the Dockerfile represents a step in setting up the application environment, from defining the OS to specifying how the application will run in the container.

With a Dockerfile, you can:

- Select the base OS or runtime (ex: Alpine, Ubuntu, Node.js).

- Install dependencies.

- Copy source code files into the container.

- Specify commands to start your application when the container runs.

The result is a fully customizable image that’s purpose-built for your application—commonly referred to as [“dockerizing”](https://www.memecreator.org/static/images/memes/5099940.jpg) your app.

### Naming and Format

A Dockerfile must be named `Dockerfile` without any file extensions and is case-sensitive. This standardized naming is essential for Docker to recognize and build it correctly.

### Sample Dockerfile

Let’s look at an example of a Dockerfile and break down what each line does:

```plaintext
FROM tomcat:8.0-alpine

LABEL maintainer="tristan.hall@generalassemb.ly"

ADD JavaWebApp.war /usr/local/tomcat/webapps/

EXPOSE 8080

CMD ["catalina.sh", "run"]
```

### Dockerfile Instructions

| Instruction  | Description                                                                                                                                                                                                                                                                                     |
| ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **`FROM`**   | The `FROM` instruction specifies the base image on which to build your image. In this example, we’re using `tomcat:8.0-alpine`, a lightweight version of the Tomcat server. Every Dockerfile must start with a `FROM` instruction.                                                              |
| **`LABEL`**  | `LABEL` allows you to add metadata to the image, like the author's name or email. The format is `LABEL key="value"`, making it easy to document or add custom information to the image.                                                                                                         |
| **`ADD`**    | `ADD` copies files, directories, or remote URLs into the image’s filesystem. Here, `JavaWebApp.war` is copied into the default Tomcat webapps directory. <br> - **`COPY` vs. `ADD`**: While both copy files, `ADD` can also retrieve files from a URL, whereas `COPY` only handles local files. |
| **`EXPOSE`** | This instruction tells Docker that the container listens on a specific network port—in this case, port `8080`. Exposing ports allows Docker to manage incoming network connections to the container.                                                                                            |
| **`CMD`**    | The `CMD` instruction specifies the command that will run when the container starts. Here, it launches Tomcat with `catalina.sh run`. Each Dockerfile can only have one `CMD`; if multiple `CMD` instructions are present, only the last one will execute.                                      |

> **Note:** The `CMD` instruction runs commands in the container, not during the build. If you need commands executed as part of the build, use `RUN`.

### Additional Dockerfile Instructions

Docker provides many other instructions for fine-tuning how your image is built and how the application runs. Some commonly used instructions include:

| Instruction | Description                                                                                                           |
| ----------- | --------------------------------------------------------------------------------------------------------------------- |
| **`RUN`**   | Executes commands in the shell during the image build, allowing you to install packages or perform other setup tasks. |
| **`COPY`**  | Similar to `ADD`, but limited to copying local files and directories into the image’s filesystem.                     |
| **`ENV`**   | Sets environment variables within the container, which can be accessed by applications running inside the container.  |

We’ll explore additional instructions as needed.

Here is the official [Docker Reference Guide](https://docs.docker.com/reference/dockerfile/) on Dockerfile instructions.

## Building your Image

Once you’ve created your **Dockerfile**, you’re ready to build a custom Docker image tailored to your application.

To build the image using the Dockerfile you created, run the following command in your terminal:

```bash
docker build -t <your-image-name> .
```

Replace `<your-image-name>` with a name of your choice for the new image. The `.` at the end specifies that the Dockerfile is located in the current directory.

After building, you can verify your new image by running:

```bash
docker images
```

Once your custom image is ready, you can use it to run a container as usual with:

```bash
docker run <your-image-name>
```
