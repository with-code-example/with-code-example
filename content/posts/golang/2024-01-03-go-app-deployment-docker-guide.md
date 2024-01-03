---
title: "Go Application Bootstrapping Guide with Docker"
subtitle: "Preparing Your Go App for Deployment in Docker"
description: "Explore the seamless integration of a Golang stack within Docker containers. Learn to deploy and orchestrate with Docker Compose for an efficient development workflow."
slug: "go-app-deployment-docker-guide"
tags: ["Go", "Docker", "Containerization", "DevOps", "Docker Compose"]
featured_image: https://res.cloudinary.com/harendra21/image/upload/w_1200/golangwithexample/1_jesgUWcmdloZw7Y1MpyjpQ_ixcu2z.webp
thumbnail: https://res.cloudinary.com/harendra21/image/upload/w_400/golangwithexample/1_jesgUWcmdloZw7Y1MpyjpQ_ixcu2z.webp
comments: false
date: 2024-01-03
toc: false
draft: false

---

When developing a web application with Go, whether it's for HTTP or another type of service, deploying it across different stages or environments (local development, production, etc.) is a common consideration. In this article, we will explore integrating a Golang stack inside a Docker container, a widely adopted approach, and using Docker Compose for orchestration.

## Getting Your Go Application Ready

First and foremost, you need a functional Go application. Below is the code for our `main.go` file, along with a brief explanation:

```go
// /src/main.go

package main

import (
	"fmt"
	"net/http"
	"os"
)

func main() {
	var PORT string
	if PORT = os.Getenv("PORT"); PORT == "" {
		PORT = "3001"
	}

	http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
		fmt.Fprintf(w, "Hello World from path: %s\n", r.URL.Path)
	})

	http.ListenAndServe(":"+PORT, nil)
}
```

This code sets up a basic HTTP server that responds with "Hello World" and dynamically assigns a port based on the environment variable.

## Creating Your Dockerfile

![dockerfile](https://res.cloudinary.com/harendra21/image/upload/v1704300713/golangwithexample/w203qkq2umde2wgc0uej_pv9lsg.jpg)

The next step is to create a Dockerfile that defines the environment for building and running your Go application.

```Dockerfile
# /Dockerfile

FROM golang:alpine

ADD ./src /go/src/app
WORKDIR /go/src/app

ENV PORT=3001

CMD ["go", "run", "main.go"]
```

Breaking down the Dockerfile:

- It builds the container from the official Golang image using the Alpine Linux distribution for its lightweight nature.
- Mounts the current directory onto the container's standard Go path.
- Sets the working directory to our app's Go path.
- Defines an environment variable "PORT" with a default value of "3001".
- Specifies the command to build and run our application.

## Building and Running the Container

![Running the Container](https://res.cloudinary.com/harendra21/image/upload/v1704300753/golangwithexample/image-2-1024x629_w2lwzc.png)

Assuming you have the Docker runtime environment installed, follow these steps:

1. Build the Docker image:

   ```bash
   docker build . -t my-golang-app-image
   ```

2. Run a container from the image:

   ```bash
   docker run -p 3030:3001 -it --rm --name my-golang-app-run my-golang-app-image
   ```

Here, we instruct Docker to run a new container, bind the host port 3030 to the container's internal port 3001, display stdout output in the current terminal, remove the container once its process terminates, and assign a custom name to the container.

### Try it!

Visit `localhost:3030` in your browser, and you should see the text "Hello World from path: /". To stop the container, press `Ctrl + C`.

## Docker Compose for Orchestration

![Docker Compose](https://res.cloudinary.com/harendra21/image/upload/v1704300794/golangwithexample/docker-compose-button_zpc6vy.jpg)

Docker Compose allows the integration of multiple containers. While it might be overkill for this exercise, it's valuable knowledge for future scenarios. Create a `docker-compose.yml` file:

```yaml
# /docker-compose.yml

version: '2'
services:
  my-golang-app-run:
    container_name: my-golang-app-run
    build: .
    command: go run main.go
    volumes:
      - ./src:/go/src/app
    working_dir: /go/src/app
    ports:
      - "3030:3000"
    environment:
      PORT: 3001
```

Now, run the following command:

```bash
docker-compose up
```

Visit `localhost:3030` again in your browser to see the same result as before using Docker Compose. To stop the container, press `Ctrl + C`.

## Why Use Docker Locally?

Notice that we never installed Go in our local environment. By only installing Docker, you can avoid cluttering your local environment with various runtimes. This approach is beneficial when working on multiple projects with different runtimes.

## Summary

We've successfully configured a Dockerfile to build images and run containers with the necessary environment for Go applications. Additionally, a Docker Compose definition file allows us to run containers alongside other services seamlessly when needed.

![thank you](https://res.cloudinary.com/harendra21/image/upload/w_500/golangwithexample/blog-2020-04-07-how_to_say_thank_you_in_business_i69dkn.png)