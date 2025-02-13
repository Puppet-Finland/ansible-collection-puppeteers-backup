# Ansible Collection - puppeteers.backup

This Ansible Collection contains code for managing backup configurations.

# Roles

## git_repo_backup

This Ansible role configures
[git-repo-backup](https://github.com/Puppet-Finland/git-repo-backup) tool. It
can be used to back up arbitrary Git repositories via SSH. It creates a
separate user for the backup job and runs it in a Podman container. The role
has been tested on Rocky Linux 9.
