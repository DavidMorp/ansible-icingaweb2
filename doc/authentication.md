# Authentication

creates `authentication.ini`

```
icingaweb_auth_backend: "{{ icingaweb_resources.db.icingaweb }}"

icingaweb_authentication:
  auth_db:
    backend: db
    resource: icingaweb

  auth_ldap:
    resource: ldap
    user_class: inetOrgPerson
    user_name_attribute: uid
    backend:  ldap
    base_dn: dc=ldap,dc=cm,dc=local
    domain: ldap.cm.local

  azure_users:
    backend: "msldap"
    resource: "azure_ad"
    # login per full email:
    #   userPrincipalName
    # login per user (emailname without domain part)
    #   sAMAccountName
    user_name_attribute: "userPrincipalName"
    filter: "(|(memberOf=CN=svc_icinga_viewer,DC=foo,DC=bar)(memberOf=CN=svc_icinga_admin,DC=foo,DC=bar))"

icingaweb_groups:
  ldap_groups:
    backend: "ldap" # msldap
    resource: "ldap"
    user_backend: "auth_ldap"
    base_dn: "dc=ldap,dc=icinga,dc=local"
    group_class: "*"
    group_name_attribute: "gid"
    group_member_attribute: "memberUid"
```
