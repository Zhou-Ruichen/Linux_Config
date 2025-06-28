# Precision-7920-Tower 服务器配置备份

本仓库包含了用于保障课题组服务器 `Precision-7920-Tower` 安全、稳定、友好运行的核心配置文件和自定义脚本。

## 仓库结构

- `README.md`: 本说明文件。
- `sshd_config/`: 存放SSH服务相关的配置。
  - `sshd_config.secure.example`: 一个加固后的SSH服务核心配置参考。
  - `ssh_banner.txt`: 用户登录前显示的警告横幅。
- `systemd/`: 存放Systemd服务相关的覆盖配置。
  - `override.conf`: 用于修改SSH服务监听端口的Systemd Socket覆盖文件。
- `motd/`: 存放登录欢迎信息 (Message of the Day) 相关的脚本。
  - `99-welcome-message`: 动态MOTD脚本，用于显示实时系统状态和警告。
  - `motd-help`: 自定义帮助命令脚本，提供详细的服务器使用指南。
- `fail2ban/`: 存放Fail2Ban相关的配置。
  - `jail.local.example`: Fail2Ban的本地配置文件，用于设置白名单等。

## 部署方法

1.  **SSH配置**:
    - 将 `sshd_config.secure.example` 的内容参考并合并到服务器的 `/etc/ssh/sshd_config` 中。
    - 将 `ssh_banner.txt` 拷贝到服务器的 `/etc/ssh/ssh_banner.txt`。

2.  **Systemd端口配置**:
    - 在服务器上创建目录 `sudo mkdir -p /etc/systemd/system/ssh.socket.d/`。
    - 将 `override.conf` 拷贝到该目录下。

3.  **MOTD配置**:
    - 将 `99-welcome-message` 拷贝到服务器的 `/etc/update-motd.d/` 目录，并确保其有可执行权限 (`sudo chmod +x`)。
    - 将 `motd-help` 拷贝到服务器的 `/usr/local/bin/` 目录，并确保其有可执行权限 (`sudo chmod +x`)。

4.  **Fail2Ban配置**:
    - 将 `jail.local.example` 的内容参考并合并到服务器的 `/etc/fail2ban/jail.local` 中。

配置完成后，请根据需要重启相关服务 (`sshd`, `ssh.socket`, `fail2ban`)。
