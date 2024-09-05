# ansible-role-jetbrains-rider

## Role Name

`jetbrains_rider`

This Ansible role installs or updates JetBrains Rider, a powerful IDE for .NET development, on a Linux machine. It manages the download, extraction, symlink creation, and version updates of Rider.

## How it works

1. **Ensure the installation directory exists**: If `/opt/jetbrains` does not exist, it is created.
1. **Download Rider**: The `get_url` task fetches the Rider tarball if the version is not already installed.
1. **Extract Rider**: The tarball is extracted into the installation directory.
1. **Symlink creation**: A symlink to the Rider executable is created in `/usr/local/bin`.
1. **Cleanup old versions**: Finds all Rider installations and removes older versions while keeping the current one.

## Requirements

- Ansible 2.9 or higher.
- The managed node should have internet access to download Rider from JetBrains.
- Root privileges (using become: yes) to install Rider in system directories such as /opt and create symlinks in /usr/local/bin.

## Role Variables

### Default Variables (in defaults/main.yml)

|       Variable       |                     Description                     | Default Value                                                                     |
| -------------------- | --------------------------------------------------- | --------------------------------------------------------------------------------- |
| `rider_version`      | Version of JetBrains Rider to install.              | `2023.1`                                                                          |
| `rider_install_dir`  | Directory where JetBrains Rider will be installed.  | `/opt/jetbrains`                                                                  |
| `rider_symlink_path` | Path for creating a symlink to rider.sh executable. | `/usr/local/bin/rider`                                                            |
| `rider_download_url` | The URL to download Rider tarball.                  | `https://download.jetbrains.com/rider/JetBrains.Rider-{{ rider_version }}.tar.gz` |

## Additional Variables

- You can override the default variables as needed to install a different version of Rider or specify a different installation directory or symlink path.

## Dependencies

None.

## Example Playbook

Below is an example of how to use the `jetbrains_rider` role in your Ansible playbook:

```yaml
---
- hosts: dev-machines
  become: yes
  roles:
    - role: jetbrains_rider
      vars:
        rider_version: "2023.1.4"  # Specify the version you want to install
```

In this example:

- The role is applied to the `dev-machines` host group.
- The `rider_version` variable is overridden to install a specific version (`2023.1.4`) of JetBrains Rider.

## Running the Playbook

Run the playbook with the following command:

```bash
ansible-playbook -i inventory playbook.yml
```

This will install or update JetBrains Rider on the specified hosts.

## License

MIT

## Author Information

This role was created by **Filipe Marcelino**.
