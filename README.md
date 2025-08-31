This project demonstrates how to deploy a static website to an **AWS EC2 instance** using **Nginx** and **GitHub Actions** for continuous deployment.

---

##  Public Website
The site is live at:  
[http://13.48.133.233](http://13.48.133.233)

---

## Repository Structure
.
├── site/ # Static site files (index.html, etc.)
├── .github/
│ └── workflows/
│ └── deploy.yml # GitHub Actions workflow for deployment
└── README.md

---

## Branching Strategy
- `main` → Production branch (deploys to EC2)  
- `dev` → Development branch (test changes before merging to main)  
- `stg` → Staging branch (optional)  

---

## GitHub Actions Workflow
Located at `.github/workflows/deploy.yml`.  
The workflow is triggered on pushes or pull requests to `main`, `dev`, or `stg`.

**Steps:**
1. Checkout the repository.  
2. Copy static site files from `site/` to the EC2 instance using `scp`.  
3. Restart Nginx on EC2 to serve the updated site.  

---

## GitHub Secrets
The following secrets must be configured in the GitHub repository:  

- `EC2_HOST` → Public IP address of the EC2 instance.  
- `EC2_USER` → EC2 username (for Ubuntu instances, use `ubuntu`).  
- `EC2_SSH_KEY` → Private SSH key for the EC2 instance.  

---

## EC2 Setup
Install, test and reload Nginx:  
   ```bash
     sudo apt update
     sudo apt install nginx -y
     sudo nginx -t
     sudo systemctl restart nginx
   
