# StackCheck

Full DevSecOps Deployment Pipeline  
GitHub → Jenkins → Docker → Ansible → Azure VM  
Built for automated deployment with clean configuration and zero unnecessary tooling.

---

## What It Does

StackCheck deploys a static HTML application through a complete CI CD pipeline:

- Dockerized build using Jenkins  
- Artifact push to Docker Hub  
- Ansible deployment to Azure VM  
- Static content hosted on hardened NGINX instance  
- Live site served on a preconfigured virtual machine

---

## Features

- Clean Ansible playbook for fast deployment  
- Auto redeploy pipeline triggered by GitHub commits  
- Docker containers used for isolated and repeatable builds  
- Logs stored locally on the target VM post deployment

---

## Tech Stack

- Jenkins for CI  
- Docker for containerization  
- Ansible for deployment and system configuration  
- Azure VM for hosting  
- Bash scripting and system services for orchestration

---

## Usage

```bash
# Clone the repository
git clone https://github.com/dzigibro/stackcheck.git && cd stackcheck

# Configure Jenkinsfile and Ansible inventory if needed
# Ensure your Docker Hub credentials and Jenkins SSH keys are in place

# Trigger a Jenkins build to deploy

Planned Features

These features were considered during development but may never be implemented
They are left here for future laughs or possible inspiration

    Terraform based infrastructure provisioning

    Full OS level hardening including user lockdown and SSH tuning

    Fail2Ban integration and basic IDS alerts

    Automatic rollback on failed deployments

    Self destruct mode if Jenkins detects drift




##Author Notes

I built StackCheck to compress real world DevSecOps deployment into one pipeline without bloat
It is minimal focused and deploys in under five minutes
Use it as a base tweak it fork it or break it

– https://github.com/dzigibro
