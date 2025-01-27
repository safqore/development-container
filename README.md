# Development Container

This development container aims to set up a development environment quickly and reliably for developers.

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