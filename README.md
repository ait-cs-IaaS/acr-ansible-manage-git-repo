# Ansible-Role: acr-ansible-manage-git-repo

AIT-CyberRange: Simple local git repo management. 


## Requirements

- git

## Role Variables

```yaml
# git_actions:
#   - clone
#   - pull
#   - checkout
#   - push
# git_dest_dir
# git_repo
# git_branch
# git_owner
# git_group
```

## Example Playbook

```yaml
- name: Get data repo via git
  hosts: localhost
  gather_facts: false
  pre_tasks:
    - name: Get the current active branch of the main project repo
      ansible.builtin.command: 
        cmd: git rev-parse --abbrev-ref HEAD
      args:
        chdir: "{{ local_ansible_dir }}"
      register: current_branch
  roles:
    - role: manage-git-repo
      vars:
        git_repo: "{{ git_data_repo }}"
        git_branch: "{{ current_branch.stdout }}"
        git_dest_dir: "{{ local_ansible_dir }}/data/"
        git_main_project_dir: "{{ local_ansible_dir }}"
        git_actions:
          - clone
```

## License

GPL-3.0

## Author

- Lenhard Reuter