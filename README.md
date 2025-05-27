# custom-runner-test

This repository demonstrates how to build and run a custom GitHub Actions runner using Docker on Apple Silicon (M-series) machines.

## Overview

The custom runner is a lightweight Docker container that connects to GitHub and polls for workflow jobs. It uses the official GitHub Actions runner binary (Linux ARM64) and requires no inbound network traffic — all communication is initiated from the container to GitHub, using long polling (HTTP 403 responses are expected during idle periods).

## Security and Resource Use

To avoid unintended usage and limit exposure:

- **The runner is only active on the `main` branch.**
- **It is not left running continuously**, except during specific demonstrations.
- This prevents misuse (e.g., unauthorized compute workloads like cryptocurrency mining) and keeps the setup secure and cost-effective.

## Running in Other Environments

While this example uses a standalone Docker container, the same concept can be extended to other environments:

- You can deploy runners in orchestration platforms like **Kubernetes** or **OpenShift**, where each runner is a containerized workload.
- These runners can be managed as **long-running pods** or integrated into **autoscaling systems**.

In OpenShift, for example:
- A `Deployment` or `DeploymentConfig` can define a runner pod template.
- You could configure **Horizontal Pod Autoscalers (HPAs)** or **KEDA (Kubernetes-based Event Driven Autoscaling)** to dynamically scale runners based on queue depth, CPU usage, or webhook triggers from GitHub.
- This allows you to provision runners **on demand** rather than keeping them always running — improving both scalability and security posture.

## Notes

- Environment variables (`REPO_URL` and `RUNNER_TOKEN`) are provided via an `.env` file.
- This setup is intended for development, testing, and educational purposes — not for production use.

