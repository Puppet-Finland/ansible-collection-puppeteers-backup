# Ansible Collection - puppeteers.backup

This Ansible Collection contains code for managing backup configurations.

# Roles

## git_repo_backup

This Ansible role configures
[git-repo-backup](https://github.com/Puppet-Finland/git-repo-backup) tool. It
can be used to back up arbitrary Git repositories via SSH. Right now Bitbucket
and GitHub are explicitly supported by having their SSH host keys in the role
defaults. This role creates a separate user for the backup job and runs it in
a Podman container. The role has been tested on Rocky Linux 9.

Several parameters are required to use this role:

```
puppeteers_backup_git_repo_backup_config:
  org1:
    repos:
      - "repo1"
      - "repo2"
    ssh_key: "my_first_key"
  org2:
    repos:
      - "repo3"
      - "repo4"
    ssh_key: "my_second_key"

puppeteers_backup_git_repo_backup_script_repo: 'https://github.com/Puppet-Finland/git-repo-backup.git'
puppeteers_backup_git_repo_backup_ssh_keys:
    my_first_key: <a SSH private key to use to back up Git repositories for org1>
    my_other_key: <a SSH private key to use to back up Git repositories for org2>
```

In most case all the other parameters can be left at their defaults values (see
[roles/git_repo_backup/defaults/main.yml](roles/git_repo_backup/defaults/main.yml)).

## rsnapshot_marker

This is a simple role that updates a file on the host. That file, by default
/etc/.rsnapshot-marker is supposed to get copied by rsnapshot. Then, at the
rsnapshot server end, the age of all the various backed up marker files can be
used to determine if any rsnapshot backups have failed, e.g. by Prometheus
Textfile Collector. See
[roles/rsnapshot_marker/defaults/main.yml](roles/rsnapshot_marker/defaults/main.yml)
for details about the parameters.
