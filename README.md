# Gaussian Splatting for NeRF

This project implements Gaussian Splatting for 3D scene reconstruction, designed to work as part of a larger Neural Radiance Fields (NeRF) pipeline. It provides functionality for training Gaussian models, rendering scenes, and serving results through a web interface.

## System Overview

The Gaussian Splatting system consists of several key components:

1. **Job Dispatcher**: Manages the queue of training jobs and dispatches them to available GPUs.
2. **Training Pipeline**: Implements the core Gaussian Splatting algorithm for learning 3D scene representations.
3. **Rendering Engine**: Renders the learned 3D scenes from various viewpoints.
4. **File Server**: Provides HTTP access to the generated outputs.
5. **Utility Functions**: Includes various helper functions for data conversion, output generation, and more.

## Key Features

- Multi-GPU support for concurrent job processing
- RabbitMQ integration for job queueing and management
- Dynamic configuration of training parameters
- Output generation in multiple formats (PLY, SPLAT, video)
- Web server for accessing rendered results

## Getting Started

### Prerequisites

- CUDA-capable 11.7 GPU(s)
- NVCC for Pytorch Extension compilation [READ THIS](https://github.com/NeRF-or-Nothing/nerf-worker/wiki/NVCC-notes)
- Python 3.7+
- PyTorch
- RabbitMQ
- Flask

### Installation

#### As a service (Docker) **PREFERRED**
Refer to the backend setup [instructions](https://github.com/NeRF-or-Nothing/backend/README.md)

If you wish to manually build the container
1. Build the image
  ```
  docker build -t nerf-worker  
  ```
2. Start the image
  ```
  docker run nerf-worker
  ```

#### Locally
1. Clone this repository
2. Install the required Python packages:
   ```
   pip install -r requirements.txt
   ```
3. Set up RabbitMQ and configure the connection details in the `.env` file

### Usage

1. Start the job dispatcher:
   ```
   python dispatcher.py
   ```
2. Start the file server:
   ```
   python fileserver.py
   ```
3. Submit jobs to the `nerf-in` queue in RabbitMQ

## Configuration

The system can be configured through various parameters in the `train.py` file and environment variables. Key configuration options include:

- Number of training iterations
- Output types (PLY, SPLAT, video)
- GPU allocation strategy
- RabbitMQ connection details

## Contributing

Contributions to improve the Gaussian Splatting system are welcome. Please submit pull requests or open issues for any bugs or feature requests.

## License

This project is licensed under [LICENSE NAME] - see the LICENSE.md file for details.

## Acknowledgments

- [INRIA](https://www.inria.fr/en) GRAPHDECO research group for the original Gaussian Splatting implementation
- [Spring '24 Team] for adapting and extending the system

For more detailed information on specific components and processes, please refer to the wiki pages.
