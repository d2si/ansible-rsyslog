# Rsyslog Ansible role

[![The MIT License](https://img.shields.io/badge/license-MIT-orange.svg?style=flat-square)](http://opensource.org/licenses/MIT)

This role manages configuration of `rsyslog` client and makes sure that it's installed.

## Requirements & Dependencies

### Ansible
It was tested on the following versions:
 * 1.9

### Operating systems

Currently the module was only tested on Debian.

### Role variables

 * `rsyslog_conf_file`: string, the path to `rsyslog.conf`
 * `rsyslog_d_dir`: string, where are the config files`
 * `rsyslog_user`: the owner group of `rsyslog.conf`
 * `rsyslog_group`: the owner user of `rsyslog.conf`
 * `rsyslog_remote_loggers`: dict of remote centralized logging servers

Optional:
 * `ca_certificate`: string, the root ca certificate to verify server log certificate.

Almost all of them has default values in `defaults/main.yml`.


### Specific variables

Rsyslog support traffic encryption with TLS (SSL). [More info](http://www.rsyslog.com/doc/v8-stable/tutorials/tls_cert_summary.html)

To enable it, `ca_certificate` must be defined, and `ssl` must be set to true for hosts to which you want to encrypt traffic.


*Example*:

```yaml
  vars:
    ca_certificate: "root-ca.pem"
    rsyslog_remote_loggers:
      syslog-ng1:
        remote_host: "securelogserver.example.com"
        remote_port: "10514"
        ssl: true
        filters:
          - "auth.*"
          - "local6.*"
      syslog-ng2:
        remote_host: "logserver.example.com"
        remote_port: "514"
        ssl: false
        filters:
          - "auth.*"
```


### Contribution
If you find a bug, please open an issue on [GitHub](https://github.com/d2si/ansible-rsyslog/issues).

If you want to hack some features into this role, please open an issue and we will talk about that.


### Authors

`ansible-rsyslog` role was written by:
- Laurent Bernaille | [e-mail](mailto:laurent.bernaille@gmail.com) | [Twitter](https://twitter.com/lbernail) | [GitHub](https://github.com/lbernail)
- François Gouteroux | [e-mail](mailto:francois.gouteroux@gmail.com) | [Twitter](https://twitter.com/fgouteroux) | [GitHub](https://github.com/fgouteroux)
