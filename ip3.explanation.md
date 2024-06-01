## Vagrant file: VM setup
This setup uses Vagrant to create and configure three VMs, each running a part of the application stack. Ansible is employed to provision these VMs, ensuring Docker is installed, repositories are cloned, and the necessary containers are up and running. The use of static IP addresses and port forwarding ensures seamless communication and access to services both internally (between VMs) and externally (from the host machine).



Getting these VMs to communicate was quite a hustle, although the app runs and is accessible from the localhosts port 3000, it appears that the backend VM is not writing data on the mongodb. Both Mongodb and the backend vm connect but for some reason data is not exchanged (when you try to add a product, the page just goes blank and refreshing leads to homepage without any product added). I am suspecting either an issue with how i am configuring the docker volumes or the networks. For now i will stop chasing this bug, an easy fix is to use a single vm running the 3 containers but then I will miss the point of ansible. So for the sake of playing around with ansible, this state remains.  Below is a rationale of my approach in setting the vms, details can be foun at /Vagrant File

- `Base OS`: Using geerlingguy/ubuntu2004 ensures a consistent environment across all VMs.
  
- `Private Network`: Each VM is assigned a static IP within a private network to ensure stable communication between them.
  
- `Port Forwarding`: Ports are forwarded to allow access to the services running inside the VMs from the host machine.
- 
    -MongoDB: Port 27017 for database access.
  
    -Backend: Port 5000 for the backend service.
  
    -Client: Port 3000 for the client application.
  
- `Ansible Provisioner`: Ansible is used for provisioning to automate the setup process and ensure idempotency.




## Provisioning with Ansible playbook



*Rationale:*

`Package Cache Update:`

- Ensures that all package lists are updated to the latest versions.
    
`Ping Role:`

- Verifies connectivity to all hosts, ensuring that Ansible can manage the VMs.
    
`Install Docker:`

- Installs Docker on all VMs to support containerized applications.
    
`Clone YOLO Git Repository:`

- Clones the necessary application code to all VMs for building the Docker images.
    
`Pull and Run Containers:`

- MongoDB: Pulls and runs the MongoDB container on the mongodb VM.
    
- Backend: Pulls and runs the backend application container on the backend VM.
    
- Client: Pulls and runs the client application container on the client VM.

*Role Descriptions*

- `ping_role`: Ensures all VMs are reachable.
    
- `docker_role`: Handles Docker installation.
    
- `clone_yolo_git`: Clones the YOLO application repository to the VMs.
    
- `run_mongodb_container`: Pulls the MongoDB Docker image and runs the container.
    
- `run_backend_container`: Builds and runs the backend Docker container, linking it to MongoDB.
    
- `run_client_container`: Builds and runs the client Docker container, linking it to the backend.




