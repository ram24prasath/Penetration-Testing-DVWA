# Installing DVWA through docker

  DVWA application can be installed through various methods. I have chosen to install DVWA in kali linux through Docker.

  Pre-requisite to installing DVWA is having docker and docker-compose.

  ## Installing Docker in Kali linux.

  Installing docker from debian in kali linux through the following set of commands.

  ```
  sudo apt update -y

  sudo apt install docker.io docker-compose
  ```

  You can now get started with using docker, with sudo. If you want to add yourself to the docker group to use docker without sudo, an additional step is needed:

  ```
  sudo usermod -aG docker $USER
  ```

  Reboot the linux

  ```
  sudo reboot
  ```

  To check docker is up and running:

  ```
  docker version

  docker-compose version
  ```

---

  ## Installing DVWA

  Step 1:

  Run `docker version` and `docker-compose` to see if you have Docker and Docker Compose properly installed. You should be able to see their versions in the output.

  ![image](https://github.com/user-attachments/assets/3b42cbd6-a198-4ad5-b2ff-53d1b78ba326)

  ![image](https://github.com/user-attachments/assets/12563119-1dc0-4b94-95e4-b5f3309a887d)


  Step 2:

  Clone DVWA git repository from `git clone https://github.com/digininja/DVWA.git`.

  Step 3: 

  Open terminal and navigate to the DVWA folder.

  ![image](https://github.com/user-attachments/assets/0f91554d-1823-4830-8b7c-2f61ebbb3700)


  Step 4:

  Run `docker-compose up -d`.

  DVWA is now available at `http://localhost:4280`.

  ![image](https://github.com/user-attachments/assets/63317b56-9c12-45be-9a46-a6a6224af4db)
