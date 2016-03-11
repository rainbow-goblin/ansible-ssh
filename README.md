ssh
===

Universal configuration of SSH daemon and client through a set of variables.


Example
-------

```
---

# Example of how to use the role
- hosts: myhost
  vars:
    # Disable root login (PermitRootLogin = no)
    sshd_config:
      ChallengeResponseAuthentication: 'no'
      GSSAPIAuthentication: 'yes'
      GSSAPICleanupCredentials: 'yes'
      PasswordAuthentication: 'yes'
      PermitRootLogin: 'no'
      Protocol: 2
      Subsystem: sftp /usr/libexec/openssh/sftp-server
      SyslogFacility: AUTHPRIV
      UsePAM: 'yes'
  roles:
    - ssh
```


Role variables
--------------

List of variables used by the role:

```
# Defaults for client
ssh_config:
  '*':
    ForwardX11Trusted: 'no'
    GSSAPIAuthentication: 'no'
    Protocol: 2
    ServerAliveInterval: 10
    SendEnv:
      - LANG LC_CTYPE LC_NUMERIC LC_TIME LC_COLLATE LC_MONETARY LC_MESSAGES
      - LC_IDENTIFICATION LC_ALL
      - LC_PAPER LC_NAME LC_ADDRESS LC_TELEPHONE LC_MEASUREMENT

# Defaults for server
sshd_config:
  Port: 22
  Protocol: 2
  UsePrivilegeSeparation: 'yes'
  ChallengeResponseAuthentication: 'no'
  GSSAPIAuthentication: 'no'
  GSSAPICleanupCredentials: 'yes'
  PasswordAuthentication: 'no'
  ClientAliveInterval: 0
  AcceptEnv: 'LANG LC_*'
  Subsystem: 'sftp internal-sftp'
  SyslogFacility: 'AUTHPRIV'
  LogLevel: 'INFO'
  LoginGraceTime: '20000'
  PermitRootLogin: 'yes'
  StrictModes: 'yes'
  RSAAuthentication: 'yes'
  PubkeyAuthentication: 'yes'
  AuthorizedKeysFile: '%h/.ssh/authorized_keys'
  IgnoreRhosts: 'yes'
  AllowTcpForwarding: 'no'
  X11Forwarding: 'no'
  HostbasedAuthentication: 'no'
  PermitEmptyPasswords: 'no'
  PrintMotd: 'no'
  PrintLastLog: 'yes'
  TCPKeepAlive: 'yes'
  UsePAM: 'yes'
  UseDNS: 'no'
  AllowUsers: 'root'
```

The server and client configuration is using exact keys as they are in the
original configuration file. If the key is a list (e.g. `SendEnv`), multiple
lines with the key will be generated.

If the `ssh_banner` is set to non-zero lenght string, the file specified in the
`ssh_banner_location` will be created and populated with the string. It also
requires to set `Banner` key with the value of the `ssh_banner_location` variable
in the `sshd_config` variable.


License
-------

MIT


Author
------

Jiri Tyr
