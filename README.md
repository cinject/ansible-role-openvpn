# Ansible Role: OpenVPN

**This role does not generate certificates and keys, but only copies them and starts services.**
Default location ca, key and etc files {{ fetch_private_dir }}/openvpn/{{ obj.name }}


## Requirements

None.

## Example Playbook

```yaml
- hosts: all
  vars:
    fetch_private_dir: ./.private/{{ inventory_hostname }}
  
    openvpn_conf: 
      - name: server    # => obj.name
        server: 10.8.1.0 255.255.255.0 
        ca: ca.crt
        cert: server.crt
        key: server.key
        dh: dh.pem
        ta: ta.key
        extra_params: |
          push "redirect-gateway def1"
          push "dhcp-option DNS 8.8.8.8"
          push "dhcp-option DNS 8.8.4.4"
  roles:
    - cinject.openvpn
```

## Default vars

```yaml
openvpn_conf_server_template: server.conf.j2
openvpn_conf_client_template: client.conf.j2
openvpn_path: /etc/openvpn
openvpn_conf: []
```

## License

MIT / BSD