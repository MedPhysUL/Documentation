# HOWTO - Valeria

## Introduction

VALERIA makes innovation accessible to the University Laval community by providing powerful and secure tools for data collection, sharing, transfer, processing, and storage. This tutorial aims at providing a simple guide to use the computational resources offered by Valeria.

## Prerequisites

1. Subscribe and connect to Valeria. See [Getting Started](https://doc.s3.valeria.science/fr/index.html).
2. A linux machine with [Apptainer](https://apptainer.org/docs/admin/main/installation.html) and [Docker](https://www.docker.com/get-started) installed. Use [wsl](https://learn.microsoft.com/en-us/windows/wsl/install) on Windows ;)

## 1. Converting a Docker image to a Singularity/Apptainer image

1. Open your terminal or command prompt.

2. Run the following command to build your Docker image:

   ```bash
   docker build . -t myproject.
   ```

3. Now, let's save the Docker image as a `.tar` file on your Desktop using the following command:

   ```bash
   docker save myproject -o myproject.tar
   ```

4. You can now remove the Docker image if you want:

   ```bash
   docker image rm myproject
   ```

5. The apptainer `.sif` file can now be built using the docker `.tar` file.

   ```bash
   apptainer build --fakeroot myproject.sif docker-archive://myproject.tar
   ```

6. You can now remove the Docker `.tar` file. 

   ```bash
   rm myproject.tar
   ```

## 2. Creating a job.sh file

1. Open an empty `.txt` file.

2. Specify your specific computational resources requirements and the way to launch your application. This file is used to start your program on the Valeria server.

   ```bash
   #!/bin/bash
   #SBATCH --job-name=myproject
   #SBATCH --partition=gpu
   #SBATCH --cpus-per-task=50
   #SBATCH --time=2-00:00:00
   #SBATCH --mem=32G
   #SBATCH --gres=gpu:1
   #SBATCH --mail-type=ALL
   #SBATCH --mail-user=username@ulaval.ca
   
   module load apptainer
   
   apptainer run --nv --bind /home/ulaval.ca/username/myproject/experiments/:/workspace/experiments myproject.sif main.py
   ```

3. Save your `.txt` file as a `.sh` file

## 3. Sending files to Valeria

1. Activate the [Ulaval VPN](https://www.dti.ulaval.ca/page-guide-anyconnect-windows).

2. Open a command prompt and access Valeria server using ssh. 

   ```bash
   ssh username@login.valeria.science
   ```

3. Open a second command prompt and send your `.sif` file using scp.

   ```bash
   scp myproject.sif username@login.valeria.science:/home/ulaval.ca/username/myproject
   ```

4. Do the same for the `.sh` file:

   ```bash
   scp job.sh username@login.valeria.science:/home/ulaval.ca/username/myproject
   ```

## 4. Launching a job

1. On the Valeria server you accessed using ssh, type:

   ```bash
   sbatch job.sh
   ```

2. Your job is launched!

## Conclusion

Congratulations! You have learned the basics of using Valeria's computational ressources. Valeria has many more features and capabilities, so feel free to explore the official Valeria [documentation](https://doc.s3.valeria.science/fr/index.html) and [examples](https://git.valeria.science/valeria/val-exemples) to learn more about advanced usage.
