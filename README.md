# Ansible Role: nifi

## Requirements

   - Linux: Java
   - Windows: Java, Nssm, Pscx

## Platform

   - Debian
   - RedHat
   - Windows

## How it works

When user passes a nifi version, say 1.1.2, the role goes to load variables corresponding to the version.
If some nifi version is missing, please issue me or pull a request.)
And download nifi package from apache server to `nifi_download_dir` of the local machine based on these variables.
Then the role unarchives the package to `nifi_install_dir` of remote nodes, and do some configurations.

## Role Main Variables

1. `nifi_version` (default: `1.1.2`): the nifi version you want to install. Only support `1.1.2` for now.
2. `nifi_download_dir` (default: `/tmp/nifi`): the folder to save nifi package in local machine.
3. `nifi_install_dir` (default: `{{ansible_env['HOME']}}`): the path that you want to install the nifi to in remote nodes.
4. `nifi_cluster` (default: `false`): this option active the mode cluster and zookeeper embed for remote node. 
5. `nifi_secure` (default: `none`): options: none, certs, ldap and kerberos.
6. `nifi_auto_keystore` (default: `true`) generate pki for all nodes and init admin certificate.

## Role Other Variables

- nifi_bored_yield_duration: "10 millis"
- nifi_ui_autorefresh_interval: "30 sec"
- nifi_provenance.repository_max_storage_time: "24 hours"
- nifi_provenance.repository_max_storage_size: "1 GB"
- nifi_web_http_port: 8080
- nifi_web_https_port: 9443
- nifi_security_keystore:
- nifi_security_keystoreType: jks
- nifi_security_keystorePasswd:
- nifi_security_keyPasswd:
- nifi_security_truststore:
- nifi_security_truststoreType: jks
- nifi_security_truststorePasswd:
- nifi_security_user_authorizer: file-provider
- nifi_cluster_node_protocol_port: 9999
- nifi_cluster_node_protocol_threads: 10
- nifi_zookeeper_clientPort: 2181
- nifi_kerberos_krb5_file:
- nifi_kerberos_service_principal:
- nifi_kerberos_service_keytab_location:
- nifi_variable_registry_properties:
- nifi_jvm_xms: 512m
- nifi_jvm_xmx: 512m
- nifi_authorizer_dn: "OU=NIFI"
- nifi_authorizer_admin_identity: "CN=admininit, {{ nifi_authorizer_dn }}"
- nifi_authorizer_users_file:
- nifi_ldap_provider_auth_strategy: SIMPLE
- nifi_ldap_provider_manager_dn:
- nifi_ldap_provider_manager_password:
- nifi_ldap_provider_referral_strategy: FOLLOW
- nifi_ldap_provider_url:
- nifi_ldap_provider_search_base:
- nifi_ldap_provider_search_filter:
- nifi_ldap_provider_identity_strategy: USE_USERNAME
- nifi_ldap_provider_tls_keystore:
- nifi_ldap_provider_tls_keystore_password:
- nifi_ldap_provider_tls_keystore_type:
- nifi_ldap_provider_tls_truststore:
- nifi_ldap_provider_tls_password:
- nifi_ldap_provider_tls_client:
- nifi_ldap_provider_tls_type:
- nifi_ldap_provider_tls_protocol:
- nifi_ldap_provider_tls_shutdown:
- nifi_kerberos_provider_realm:


## Dependencies

None.

## Example Playbook

    - hosts: your-servers
      roles:
        - { role: nifi }

    - hosts: your-servers
      roles:
        - { role: nifi, nifi_version: 1.1.2, nifi_download_dir: /tmp }

    - hosts: your-servers
      sudo: yes
      roles:
        - { role: nifi, install_dir: /usr/local }

    - hosts: your-servers
      sudo:
      roles:
        - { role: nifi, nifi_version: 1.1.2, nifi_install_dir: /usr/local }

    - hosts: your-servers
      sudo:
      roles:
        - { role: nifi, nifi_cluster: true }

    - hosts: your-servers
      sudo:
      roles:
        - { role: nifi, nifi_cluster: true, nifi_secure: certs, nifi_auto_keystore: true }

## License

MIT

### Author Information

This role was created by [Sylvain Beynard](https://github.com/sbeyn).

