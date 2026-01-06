# AsciiArtify

AsciiArtify is a demonstration project that showcases the design and deployment of an ASCII art generation service using Kubernetes and GitOps practices.

The repository documents the evolution of the project through three stages:
- infrastructure decision-making,
- GitOps Proof of Concept,
- and a deployable MVP managed with ArgoCD.

## Project Structure

- **Concept**  
  Infrastructure decision document comparing local Kubernetes cluster deployment tools and selecting an appropriate solution.  
  👉 [Concept.md](https://github.com/i-stanko/AsciiArtify/blob/main/doc/Concept.md)

- **Proof of Concept (PoC)**  
  Practical setup of a GitOps workflow using ArgoCD on a local Kubernetes cluster.  
  👉 [POC.md](https://github.com/i-stanko/AsciiArtify/blob/main/doc/POC.md)

- **MVP**  
  Description and demo of the AsciiArtify MVP deployed on Kubernetes and managed via ArgoCD.  
  👉 [MVP.md](https://github.com/i-stanko/AsciiArtify/blob/main/doc/MVP.md)

## Technologies Used

- Kubernetes (local cluster)
- Kind
- ArgoCD
- GitOps workflow

## Purpose

This repository is intended for educational and demonstrational purposes, focusing on DevOps practices such as infrastructure evaluation, GitOps-based deployment, and Kubernetes application management.
