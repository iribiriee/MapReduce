# Distributed Map-Reduce on Kubernetes

## Overview
This repository contains a microservice-based implementation of a distributed **Map-Reduce** framework designed for **Kubernetes**. The system enables scalable, parallel data processing by orchestrating containerized workloads to execute user-provided Python logic.

## System Architecture
The platform utilizes a three-layer microservice architecture to decouple orchestration from execution:

* **Cluster Manager**: An external-facing FastAPI service that serves as the system gateway, handling job submission, status monitoring, and authentication.
* **Job Master**: A dynamically spawned internal engine that coordinates the lifecycle of a specific job, including data splitting and phase transitions.
* **Worker Pods**: Ephemeral Kubernetes Jobs that execute the Map and Reduce functions on assigned data chunks.

## Key Features
* **Fault Tolerance**: Implements "alive" heartbeat pings and watchdog timers to automatically detect and replace failed worker pods.
* **Secure Authentication**: Integrated with Keycloak for Single Sign-On (SSO) and JWT-based identity verification.
* **State Management**: Maintains global job state and task metadata in a persistent PostgreSQL database.
* **Object Storage**: Uses MinIO for high-performance handling of input datasets, intermediate partitions, and final outputs.

## Technology Stack
* **Core**: Python 3.10+, FastAPI, Uvicorn.
* **Orchestration**: Kubernetes Python Client.
* **Storage & State**: PostgreSQL, Redis, MinIO.
* **Security**: Keycloak, PyJWT, Cryptography.

## Deployment
1. **Infrastructure**: Deploy the supporting services (PostgreSQL, MinIO, Keycloak, Redis) using the provided Kubernetes manifests.
2. **Services**: Deploy the Cluster Manager to the cluster.
3. **CLI**: Use the local command-line interface to authenticate and submit Map-Reduce workloads.
