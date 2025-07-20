# Development Container

This development container aims to set up a development environment quickly and reliably for developers, supporting both Windows (with WSL) and Mac (with Apple Silicon).

## Setup for Windows Users (WSL)

### Steps

1. Open Command Prompt as Administrator:
    - Right-click the Start Menu and select Command Prompt (Admin).

2. If Ubuntu is already installed, start it using:
    - `wsl -d Ubuntu`

3. If WSL is not installed, run the WSL Installation Command:
    - `wsl --install`

4. Set default version to 2:
    - `wsl --set-default-version 2`

5. Configure WSL memory and processors:
    - Open a text editor and create a new file named `.wslconfig` in your Windows user profile directory (e.g., `C:\Users\<YourUsername>\.wslconfig`).
    - Add the following configuration:
      ```
      [wsl2]
      # Enables cgroup v2 and unified cgroup hierarchy
      kernelCommandLine=cgroup_no_v1=all systemd.unified_cgroup_hierarchy=1 

      # Limits VM memory in WSL 2 to 4 GB
      memory=4GB 
      
      # Specifies the number of virtual processors
      processors=2
      ```
    - Save the file and restart WSL by running the following command in PowerShell or Command Prompt:
      ```sh
      wsl --shutdown
      ```

6. If WSL is already installed, check for updates:
    - `wsl --update`

7. Install Ubuntu using WSL:
    - `wsl --install -d Ubuntu`

8. Open Ubuntu terminal and set up your username and password:
    - Follow the prompts to create a new user account and set a password. This user will have sudo privileges.

9. Update package lists:
    - `sudo apt update`

10. Upgrade packages:
    - `sudo apt upgrade -y`
    - `sudo apt full-upgrade -y`
    - `sudo apt autoremove -y`

11. Install Ansible:
    - `sudo apt install ansible -y`

12. Set up Git:
    - `git config --global user.name "Your Name"`
    - `git config --global user.email "your.email@example.com"`
    - `git config --global init.defaultBranch main`
    - `gh auth login`
    - `gh auth setup-git`

13. Clone the repository:
    - `git clone https://github.com/safqore/development-container.git`

14. Navigate to the cloned repository:
    - `cd development-container`

15. Run the Ansible playbook to set up the development environment:
    - `sudo ansible-playbook playbook.yaml`

## Setup for Mac Users (Apple Silicon)

### Prerequisites

1. **Install UTM on your Mac:**
   - Download from the [UTM website](https://mac.getutm.app/) or the Mac App Store

2. **Set up Ubuntu VM in UTM:**
   - Follow the tutorial at: https://youtu.be/nUhQy5PDj2A?si=AYFn03zAZU9wcNF0 and instructions at: https://docs.getutm.app/guides/ubuntu/
   - **IMPORTANT:** Do NOT tick "Enable hardware OpenGL acceleration" when setting up the VM
   - Recommended settings:
     - Allocate at least 4GB RAM
     - Assign at least 2 CPU cores
     - Provide 20GB+ storage

### Steps

1. **Start your Ubuntu VM in UTM** and open the terminal.

2. **Update package lists:**
   - `sudo apt update`

3. **Upgrade packages:**
   - `sudo apt upgrade -y`
   - `sudo apt full-upgrade -y`
   - `sudo apt autoremove -y`

4. **Install Ansible:**
   - `sudo apt install software-properties-common -y`
   - `sudo add-apt-repository --yes --update ppa:ansible/ansible`
   - `sudo apt install ansible -y`

5. **Install GitHub CLI:**
   ```bash
   sudo apt install curl -y
   curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg
   echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null
   sudo apt update
   sudo apt install gh -y
   ```

6. **Set up Git:**
   - `git config --global user.name "Your Name"`
   - `git config --global user.email "your.email@example.com"`
   - `git config --global init.defaultBranch main`
   - `gh auth login`
   - `gh auth setup-git`

7. **Clone the repository:**
   - `git clone https://github.com/safqore/development-container.git`

8. **Navigate to the cloned repository:**
   - `cd development-container`

9. **Run the Ansible playbook to set up the development environment:**
   - `sudo ansible-playbook playbook.yaml`

### Notes for Mac Users

- The playbook will automatically detect your ARM64 architecture and install appropriate versions of software
- Cursor IDE will be installed as an AppImage if available for ARM64, or you may need to install it manually
- All other development tools (VSCode, Miniconda, PostgreSQL, DBeaver, Node.js, Node-RED) will be installed automatically