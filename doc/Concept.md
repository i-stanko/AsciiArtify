# Concept: Local Kubernetes Cluster Deployment Tools

## Introduction
The purpose of this document is to compare three tools for deploying local Kubernetes clusters: `minikube`, `kind` (Kubernetes IN Docker), and `k3d`. Each tool provides different capabilities and trade-offs that can affect its suitability for the "AsciiArtify" startup during the Proof of Concept (PoC) stage. This document presents an overview of the selected tools and provides a recommendation based on their analysis.

## Tools

### Minikube
- **Description:** Minikube is a tool that allows running a local Kubernetes cluster on a single machine. It is commonly used for local development and testing.
- **Key Features:**
    - Supported Operating Systems: Windows, macOS, Linux
    - Architecture: Single-node Kubernetes cluster running inside a virtual machine or container runtime
    - Automation: Command-line interface (CLI) for cluster lifecycle management
    - Additional Features: Built-in add-ons such as DNS, storage provisioning, and Kubernetes Dashboard
- **Advantages:**
  - Simple setup and usage
  - Well-documented with strong community support
  - Built-in add-ons for common Kubernetes components
- **Disadvantages:**
  - Primarily focused on single-node clusters
  - Virtual machine-based setup may consume more resources

### Kind (Kubernetes IN Docker)
- **Description:** Kind is a tool for running local Kubernetes clusters using container-based nodes. It is designed primarily for testing Kubernetes itself but is also suitable for local development.
- **Key Features:**
    - Supported Operating Systems: Windows, macOS, Linux
    - Architecture: Multi-node Kubernetes clusters running as containers
    - Automation: Easily scriptable cluster creation and teardown
    - Additional Features: Well-suited for CI/CD workflows and reproducible test environments
- **Advantages:**
  - Lightweight and fast cluster startup
  - Supports multi-node cluster configurations
  - Good integration with container-based workflows
- **Disadvantages:**
  - Limited built-in tooling for monitoring and cluster management
  - Requires a container runtime

### K3d
- **Description:** K3d is a tool for running lightweight Kubernetes clusters based on K3s inside container environments. It is designed for fast cluster creation and local testing.
- **Key Features:**
    - Supported Operating Systems: Windows, macOS, Linux
    - Architecture: Kubernetes clusters running in containers using K3s
    - Automation: Simple and efficient CLI for cluster management
    - Additional Features: Built-in load balancer support, local registry integration
- **Advantages:**
    - Very fast cluster provisioning
    - Low resource consumption
    - Additional features useful for local development scenarios
- **Disadvantages:**
    - Relies on a container runtime
    - Uses K3s, which may differ from upstream Kubernetes behavior

## Risk Analysis: Docker Licensing

When considering the use of Docker-based tooling in the "AsciiArtify" project, it is important to take into account potential risks related to Docker Desktop licensing rather than the Docker engine itself.

The Docker engine is open-source and licensed under the Apache 2.0 license. However, Docker Desktop, which is commonly used for local development on macOS and Windows, is distributed under a separate commercial license that may impose restrictions for certain types of usage, including larger organizations or commercial environments.

The main risk factors to consider include:

- **Docker Desktop Licensing:** Docker Desktop requires a paid subscription for use in medium and large commercial organizations. While this may not be an immediate blocker for a PoC, it can become a constraint as the project grows or if contributors are subject to licensing requirements.

- **Dependency on a Specific Toolchain:** Relying on Docker Desktop for local Kubernetes tooling creates a dependency on a specific vendor-provided solution. This can limit flexibility when switching environments or adopting alternative container runtimes.

Considering these risks, it is reasonable to evaluate alternative container runtimes that provide similar functionality without additional licensing constraints.

### Exploring Podman as an Alternative

`Podman` is an open-source container management tool that can be used as an alternative to Docker for local development.

**Advantages:**
- **Open-source Licensing:** Podman is fully open-source and does not require a commercial license for usage.
- **Docker CLI Compatibility:** Podman provides a Docker-compatible command-line interface, which allows reuse of existing workflows and scripts with minimal changes.
- **Daemonless Architecture:** Containers are run without a central daemon, reducing the attack surface and simplifying process isolation.
- **Rootless Containers:** Supports running containers without root privileges, improving local security.

**Disadvantages:**
- **Ecosystem Differences:** Podman has a smaller ecosystem compared to Docker, and some tools or workflows may require additional configuration.
- **Tool Compatibility:** Not all Kubernetes-related tools fully support Podman in the same way they support Docker.
- **Adoption Curve:** Teams familiar with Docker may require time to adapt to Podman-specific behaviors.

The choice between Docker and Podman should be based on the project's local development requirements, contributor environments, and long-term maintainability considerations.

## Comparison table
This table compares the main characteristics of the selected tools for deploying local Kubernetes clusters.

| Tool     | Supported OS          | Architecture                                   | Automation Support | Additional Features                                         | Advantages                                              | Disadvantages                                             |
|----------|-----------------------|------------------------------------------------|--------------------|-------------------------------------------------------------|---------------------------------------------------------|-----------------------------------------------------------|
| Minikube | Windows, macOS, Linux | Single-node Kubernetes cluster (VM or container-based) | CLI-based          | Built-in add-ons (DNS, storage, dashboard)                  | Easy to use, good documentation, strong community       | Primarily single-node, higher resource usage with VM      |
| Kind     | Windows, macOS, Linux | Multi-node clusters running as containers      | Scriptable via CLI | Designed for testing, good CI/CD integration                | Fast startup, lightweight, reproducible environments   | Limited built-in management and monitoring features       |
| K3d      | Windows, macOS, Linux | Kubernetes clusters based on K3s running in containers | CLI-based          | Load balancer support, local registry integration            | Very fast provisioning, low resource consumption        | Uses K3s instead of upstream Kubernetes                   |

## Demonstration

To demonstrate the selected tool, a simple "Hello World" application was deployed to a local Kubernetes cluster using `kind`.

A local cluster was created, a basic Pod manifest was applied, and the running container was accessed to verify the output. This demonstration shows the simplicity and reliability of using Kind for deploying and testing workloads in a local Kubernetes environment.

The full demonstration was recorded using `asciinema` and is available below.

[![asciicast](https://asciinema.org/a/766091.svg)](https://asciinema.org/a/766091)

## Conclusion

After conducting a comparative analysis of local Kubernetes cluster deployment tools - `minikube`, `kind`, and `k3d` - the following conclusions can be drawn for the AsciiArtify Proof of Concept (PoC):

- `Minikube` is a well-known and easy-to-use tool for local Kubernetes development. It is suitable for individual development and learning purposes, but its single-node focus and higher resource usage may be limiting for certain PoC scenarios.

- `Kind` provides a lightweight and flexible solution by running Kubernetes clusters inside containers. It offers fast cluster startup, reproducibility, and good integration with container-based workflows, making it well-suited for local PoC environments.

- `K3d` enables rapid creation of lightweight Kubernetes clusters based on K3s. While it offers fast provisioning and useful features, it differs from upstream Kubernetes behavior, which may be a consideration depending on the use case.

Based on the evaluation, `kind` is selected as the recommended tool for deploying a local Kubernetes cluster for the AsciiArtify PoC due to its balance of simplicity, flexibility, and alignment with upstream Kubernetes.

## References
- Minikube: https://minikube.sigs.k8s.io/docs/
- Kind: https://kind.sigs.k8s.io/
- K3d: https://k3d.io/
- Podman: https://podman.io/docs
