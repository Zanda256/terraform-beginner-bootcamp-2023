# Terraform Beginner Bootcamp 2023

## Semantic Versioning :mage:

This project is going to use semantic versioning for its tagging.
[semver.org](https://semver.org/)

The general format: 
 **MAJOR.MINOR.PATCH**, e.g `1.0.1` increment the:

- __MAJOR__ version when you make incompatible API changes
- __MINOR__ version when you add functionality in a backward compatible manner
- __PATCH__ version when you make backward compatible bug fixes

## Install terraform

### Consideration with the Terraform CLI changes
The terraform installation instructions have changed and needed user input to complete. We wanted a fully automated process.
[install terraform CLI](https://developer.hashicorp.com/terraform/install)

### Refactoring into Bash Scripts
The new installation steps were alot of code and we decided to create a [bash script](./bin/install_terraform_cli) to install terraform.

### gitpod lifecycle issues
Changed .gitpod.yml tasks to use before as opposed to init because of the gitpod life cycle.
Read more [here](https://www.gitpod.io/docs/configure/workspaces/tasks)

References
https://en.wikipedia.org/wiki/Shebang_(Unix)#:~:text=In%20computing%2C%20a%20shebang%20is,the%20beginning%20of%20a%20script.


**My Notes**
The command wget -O - https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg works interactively because of the privilege escalation (sudo) and direct file redirection. When this is placed in a script, it may encounter issues or prompts due to permission conflicts during file creation or overwriting.

To automate this process fully, you can rewrite the command using sudo tee as it avoids redirection issues caused by sudo. Here's how it works:

Adjusted Command for Automation
bash
Copy code
wget -O - https://apt.releases.hashicorp.com/gpg | sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg > /dev/null
Explanation:
wget -O -:
Downloads the GPG key from the HashiCorp URL and outputs it to standard output.
sudo tee:
Writes the output of wget directly to /usr/share/keyrings/hashicorp-archive-keyring.gpg with elevated permissions.
> /dev/null:
Prevents tee from also outputting the content to the terminal, keeping the script clean.
Why Use tee Instead of Direct sudo gpg?
Using sudo tee ensures that the redirection (>) happens with proper permissions. Without this, the sudo command only applies to gpg and not to the redirection operation, causing permission issues.

https://phoenixnap.com/kb/linux-tee
https://www.tecmint.com/tee-command-examples/
https://www.putorius.net/linux-tee-command-usage-examples.html
https://www.linuxfordevices.com/tutorials/linux/tee-command


__source command__
https://phoenixnap.com/kb/linux-source-command
https://ss64.com/bash/source.html
https://www.namehero.com/blog/how-to-use-the-bash-source-command-and-why/
