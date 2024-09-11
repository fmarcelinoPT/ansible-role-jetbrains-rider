# ansible-role-jetbrains-rider

## Role Name

`jetbrains_rider`

This Ansible role is designed to install or uninstall JetBrains Rider, a .NET development IDE, on Linux machines. You can control whether to install or remove JetBrains Rider using a variable.

## Requirements

- Ansible version: 2.9 or higher.
- Root privileges (using `become: yes`), as installation happens in system directories such as `/opt/jetbrains` and symlinks are created in `/usr/local/bin`.
- Internet access on the managed machine to download JetBrains Rider from JetBrains' website.

## Role Variables

### Default Variables (in defaults/main.yml)

|       Variable       |                     Description                     | Default Value                                                                     |
| -------------------- | --------------------------------------------------- | --------------------------------------------------------------------------------- |
| `rider_action`       | Defines whether to `install` or `uninstall` Rider.  | `install`                                                                          |
| `rider_version`      | Version of JetBrains Rider to install.              | `2023.1`                                                                          |
| `rider_install_dir`  | Directory where JetBrains Rider will be installed.  | `/opt/jetbrains`                                                                  |
| `rider_symlink_path` | Path for creating a symlink to rider.sh executable. | `/usr/local/bin/rider`                                                            |
| `rider_download_url` | The URL to download Rider tarball.                  | `https://download.jetbrains.com/rider/JetBrains.Rider-{{ rider_version }}.tar.gz` |

## Action Control

- `rider_action`: Determines whether to install or uninstall JetBrains Rider. Valid values:
  - `install`: Installs the specified version of JetBrains Rider.
  - `uninstall`: Uninstalls JetBrains Rider and removes the associated symlink and installation directory.

## Example of Overriding Variables

You can override these variables in your playbook or via the command line:

```yaml
rider_action: "install"  # Can be 'install' or 'uninstall'
rider_version: "2023.1.4"  # Specify a particular version
rider_install_dir: "/opt/jetbrains"  # Specify custom install path
rider_symlink_path: "/usr/local/bin/rider"  # Path to symlink for Rider
```

## Dependencies

None.

## Example Playbook

Below is an example of how to use the `jetbrains_rider` role in your Ansible playbook.

### Installing JetBrains Rider

```yaml
---
- hosts: dev-machines
  become: yes
  roles:
    - role: jetbrains_rider
      vars:
        rider_action: "install"  # This installs Rider
        rider_version: "2023.1.4"  # Optional: specify the version to install
```

### Uninstalling JetBrains Rider

```yaml
---
- hosts: dev-machines
  become: yes
  roles:
    - role: jetbrains_rider
      vars:
        rider_action: "uninstall"  # This uninstalls Rider
```

## Running the Playbook

To install JetBrains Rider, run:

```bash
ansible-playbook -i inventory playbook.yml --extra-vars "rider_action=install"
```

To uninstall JetBrains Rider, run:

```bash
ansible-playbook -i inventory playbook.yml --extra-vars "rider_action=uninstall"
```

## License

MIT

## Author Information

This role was created at 2024 by [fmarcelinoPT](https://github.com/fmarcelinoPT). Feel free to customize or extend the role to fit your needs.
