Here's the updated README incorporating the details for accessing the OLLAMA server and the Open Web UI via localhost URLs and including a curl command to test the OLLAMA server by sending a question:

---

# Getting Started with OLLAMA and Open Web UI

This guide provides instructions on how to set up and run the OLLAMA service along with an Open Web UI using Docker Compose. This setup is suitable for beginners and covers everything from cloning the repository to running and testing the services.

## Prerequisites

Before you begin, ensure you have the following installed on your system:
- **Git**: [Install Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) for your operating system.
- **Docker**: [Install Docker](https://docs.docker.com/get-docker/) for your operating system.
- **Docker Compose**: [Install Docker Compose](https://docs.docker.com/compose/install/) if it's not included in your Docker installation.

## Cloning the Repository

To get started, clone the repository containing the Docker Compose setup:

```bash
git clone https://github.com/avianinc/basic_llm_setup.git
cd basic_llm_setup
```

This command downloads the project files into a directory named `basic_llm_setup` and changes into that directory.

## Project Structure

Ensure your project directory contains the following:
```
basic_llm_setup/
|-- docker-compose.yml
```

- **docker-compose.yml**: This file contains the Docker Compose configuration for running your services.

## Configuration Details

### Docker Compose File

The `docker-compose.yml` file defines two main services:

1. **OLLAMA**:
   - **Image**: Uses the latest OLLAMA image.
   - **Ports**: Maps port 11434 on the host to port 11434 in the container.
   - **Volumes**: Uses a local volume `ollama` to store persistent data.
   - **Networks**: Uses a custom network `app-network`.

2. **Open Web UI**:
   - **Image**: Uses the `dyrnq/open-webui` image.
   - **Ports**: Maps port 3000 on the host to port 8080 in the container.
   - **Volumes**: Uses a local volume `open-webui` for backend data storage.
   - **Extra Hosts**: Maps `host.docker.internal` to `host-gateway` for network access.

### Networks

- **app-network**: A custom bridge network that allows containers to communicate internally.

### Volumes

- **ollama**: Stores persistent data for the OLLAMA service.
- **open-webui**: Stores data for the Open Web UI backend.

## Accessing the Services

After starting the services, you can access them through the following URLs in your web browser:

- **OLLAMA Server**: [http://localhost:11434](http://localhost:11434)
- **Open Web UI**: [http://localhost:3000](http://localhost:3000)

## Running the Services

To start the services, run:

```bash
docker compose up
```

This command builds (if necessary), (re)creates, starts, and attaches to containers for a service. When you run this command, Docker will pull the necessary images, set up the defined networks and volumes, and start the services as configured.

## Testing the OLLAMA Server

To test the OLLAMA server, you can use the following `curl` command from your command line to ask a question: (must download via containter command line or web-ui first...)

```bash
curl http://localhost:11434/api/generate -d '{
  "model": "llama2",
  "prompt": "Why is the sky blue?",
  "context": [],
  "stream": true
}'
```

This command sends a request to the OLLAMA server to generate a response based on the prompt "Why is the sky blue?".

## Stopping the Services

To stop and remove all running services, use the following command:

```bash
docker compose down
```

This command stops all running containers and removes the containers, networks, and volumes created by `docker compose up`.

## Troubleshooting

If you encounter issues with the services, check the logs using:

```bash
docker compose logs
```

This command displays log output from all services. It's useful for diagnosing problems and ensuring that all services are running as expected.

## Conclusion

This guide should help you get started with running the OLLAMA and Open Web UI services using Docker Compose. If you have any questions or run into problems, consulting the Docker and Docker Compose documentation can provide additional guidance and troubleshooting tips.