# Video-to-Audio Conversion Microservice

## Overview

Microservice Architecture and System Design with Python & Kubernetes that converts MP4 video files to MP3 audio format. Built with Python, Kubernetes, RabbitMQ, MongoDB, and MySQL, this project demonstrates microservice architecture and distributed system principles.

## Key Features

- **Video to Audio Conversion**: Converts MP4 video files into MP3 audio format efficiently.
- **Scalable Microservices**: Designed for deployment in a Kubernetes environment to ensure high availability and scalability.
- **Asynchronous Processing**: Utilizes RabbitMQ for message queuing, allowing for efficient task processing.
- **Database Management**:
  - **MongoDB** for metadata storage of processed files.
  - **MySQL** for managing user and job-related data.
- **Containerized**: Fully containerized using Docker, ensuring consistency across environments.

---

## Technologies Used

| Component   | Technology       |
|-------------|------------------|
| Language    | Python           |
| Containerization | Docker       |
| Orchestration | Kubernetes     |
| Messaging   | RabbitMQ         |
| Databases   | MongoDB, MySQL   |
| API Framework | Flask/FastAPI  |
| Storage     | Cloud/Local Storage |

### Core Technologies

- **Python**: Backend logic for processing video and audio files.
- **Kubernetes**: Orchestrates containerized applications for scaling and reliability.
- **RabbitMQ**: Message broker for task queue management.
- **MongoDB**: Stores file processing metadata.
- **MySQL**: Relational database for user and job management.

### Auxiliary Tools

- **FFmpeg**: Library for audio and video processing.
- **Docker**: Containerizes services for deployment.

---

## Architecture Overview

### System Flow:
1. **User Interaction**: Users upload MP4 files via the API.
2. **Task Queuing**: The file details are sent to RabbitMQ, which manages task queues.
3. **Processing**:
   - A worker service retrieves tasks from RabbitMQ.
   - The MP4 file is converted to MP3 using a Python-based audio processing library (e.g., FFmpeg).
   - Conversion status and metadata are saved to MongoDB.
4. **Completion Notification**:
   - Users are notified of the task's completion.
   - Converted files are stored and made available for download.

---
## Docker Image
The Docker image for this project is available at:
- [Docker Hub - alexdeliev/auth](https://hub.docker.com/r/alexdeliev/auth)
- [Docker Hub - alexdeliev/gateway](https://hub.docker.com/r/alexdeliev/gateway)
- [Docker Hub - alexdeliev/converter](https://hub.docker.com/r/alexdeliev/converter)
- [Docker Hub - alexdeliev/notification](https://hub.docker.com/r/alexdeliev/notification)

### Deployment:
- Services are containerized using Docker.
- Deployed to Kubernetes for scalability and fault tolerance.
- Configurable via Helm charts and environment variables.

### Prerequisites
- Docker & Kubernetes
- RabbitMQ Server
- MongoDB and MySQL Databases
- FFmpeg Library
- Python 3.12
---

## File Structure
```
src/
├── auth/
│   ├── Dockerfile                    # Docker configuration for the auth service
│   ├── init.sql                      # SQL script to initialize the database
│   ├── manifests/
│   │   ├── auth-deploy.yaml          # Kubernetes deployment configuration for the auth service
│   │   ├── configmap.yaml            # Kubernetes ConfigMap for the auth service
│   │   ├── secret.yaml               # Kubernetes Secret for the auth service
│   │   ├── service.yaml              # Kubernetes Service for the auth service
│   ├── requirements.txt              # Python dependencies for the auth service
│   ├── server.py                     # Main server script for the auth service
│   ├── venv/                         # Virtual environment for the auth service
├── converter/
│   ├── Dockerfile                    # Docker configuration for the converter service
│   ├── manifests/
│   │   ├── configmap.yaml            # Kubernetes ConfigMap for the converter service
│   │   ├── converter-deploy.yaml     # Kubernetes deployment configuration for the converter service
│   │   ├── secret.yaml               # Kubernetes Secret for the converter service
│   ├── requirements.txt              # Python dependencies for the converter service
│   ├── consumer.py                   # Consumer script for the converter service
│   ├── convert/
│   │   ├── __init__.py               # Init file for the convert module
│   │   ├── to_mp3.py                 # Script to convert files to MP3 format
│   ├── venv/                         # Virtual environment for the converter service
├── gateway/
│   ├── Dockerfile                    # Docker configuration for the gateway service
│   ├── manifests/
│   │   ├── configmap.yaml            # Kubernetes ConfigMap for the gateway service
│   │   ├── gateway-deploy.yaml       # Kubernetes deployment configuration for the gateway service
│   │   ├── ingress.yaml              # Kubernetes Ingress configuration for the gateway service
│   │   ├── secret.yaml               # Kubernetes Secret for the gateway service
│   │   ├── service.yaml              # Kubernetes Service for the gateway service
│   ├── requirements.txt              # Python dependencies for the gateway service
│   ├── server.py                     # Main server script for the gateway service
│   ├── storage/
│   │   ├── __init__.py               # Init file for the storage module
│   │   ├── util.py                   # Utility functions for storage
│   ├── venv/                         # Virtual environment for the gateway service
│   ├── auth/
│   │   ├── __init__.py               # Init file for the auth module in the gateway service
│   │   ├── validate.py               # Script to validate authentication
│   ├── auth_svc/
│   │   ├── __init__.py               # Init file for the auth_svc module in the gateway service
│   │   ├── access.py                 # Script to handle access control
├── notification/
│   ├── Dockerfile                    # Docker configuration for the notification service
│   ├── manifests/
│   │   ├── configmap.yaml            # Kubernetes ConfigMap for the notification service
│   │   ├── notification-deploy.yaml  # Kubernetes deployment configuration for the notification service
│   │   ├── secret.yaml               # Kubernetes Secret for the notification service
│   ├── requirements.txt              # Python dependencies for the notification service
│   ├── send/
│   │   ├── __init__.py               # Init file for the send module in the notification service
│   │   ├── email.py                  # Script to send email notifications
│   ├── consumer.py                   # Consumer script for the notification service
│   ├── venv/                         # Virtual environment for the notification service
├── rabbit/
│   ├── manifests/
│   │   ├── configmap.yaml            # Kubernetes ConfigMap for RabbitMQ
│   │   ├── ingress.yaml              # Kubernetes Ingress configuration for RabbitMQ
│   │   ├── pvc.yaml                  # Kubernetes PersistentVolumeClaim for RabbitMQ
│   │   ├── secret.yaml               # Kubernetes Secret for RabbitMQ
│   │   ├── service.yaml              # Kubernetes Service for RabbitMQ
│   │   ├── statefulset.yaml          # Kubernetes StatefulSet configuration for RabbitMQ
```

## Future Enhancements

- Add support for more video and audio formats.
- Implement a notification system for job completion.
- Introduce caching for faster re-processing of files.
- Use Grafana and Prometheus for monitoring and alerting.
- Add user interface UI/UX.
---

## License

This project is licensed under the MIT License. See the `LICENSE` file for more details.

---

## Acknowledgements

Special thanks to the open-source community and the developers behind Python, Kubernetes, RabbitMQ, MongoDB, MySQL, and FFmpeg for their incredible tools and resources.

