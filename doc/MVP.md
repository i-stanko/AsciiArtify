# MVP for AsciiArtify Project

## Description
The MVP (Minimum Viable Product) for AsciiArtify represents the initial version of the product with core functionality required to validate the idea and demonstrate end-to-end deployment using GitOps practices. AsciiArtify is a service that converts images into ASCII art and is deployed on Kubernetes using ArgoCD.

## Functionalities of the MVP

1. Image Upload: Users can upload an image file to the AsciiArtify application.
2. ASCII Art Conversion: The application converts the uploaded image into ASCII art.
3. Display ASCII Art: The converted ASCII art is displayed to the user.
4. Download ASCII Art: Users can download the generated ASCII art as a text file.
5. GitOps Deployment: Application updates are automatically deployed to the Kubernetes cluster using ArgoCD by tracking changes in the Git repository.

## Deployment Overview

The MVP is deployed to a Kubernetes cluster using ArgoCD. An ArgoCD Application is configured to monitor the application repository and automatically synchronize changes to the cluster. This setup demonstrates a complete GitOps workflow, where Git serves as the single source of truth for application state.

## Future Enhancements

The MVP focuses on core functionality and deployment automation. Possible future improvements include:

- Improved image processing algorithms for higher-quality ASCII art output.
- Additional configuration options for ASCII art generation.
- Enhanced observability and monitoring for the deployed application.
- Performance optimizations for handling larger images.
- Extended deployment strategies (e.g., canary or blue-green deployments).

## Demo

The repository contains a demo showcasing the MVP deployed on Kubernetes and managed by ArgoCD. The demo demonstrates how changes in the Git repository are automatically synchronized and deployed to the cluster.

![demo](https://github.com/i-stanko/AsciiArtify/raw/main/assets/peek-mvp.gif)
