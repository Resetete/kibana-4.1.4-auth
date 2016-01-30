# Kibana 4.1.4 with Authentication

This is a fork of [elastic/kibana](https://github.com/elastic/kibana) with an authentication page. For introductions of Kibana, please refer to the original repository.

Kibana and Elasticsearch's lack of the ability of authentication has post great danger to sensitive data. This fork adds a login page for kibana to eliminate unauthorized requests.

Please be reminded that, this login page only protects your kibana web client, people are still able to access your elasticsearch without control via kibana proxy: `localhost:5601/elasticsearch`. If you want to protect your elasticsearch, please have a look at [search-guard](https://github.com/dotSlashLu/search-guard) which is a plugin for elasticsearch providing fine-grained acl control.

## Authentication

To use the authentication feature, the following entries must be configured in the `kibana.yml`:
```yml
# account for kibana, which should only has the accessibility of the .kibana index
kibana_elasticsearch_username: username
kibana_elasticsearch_password: password
# ldap API for authentication
# this API should accept url parameters name and password
# you can customize this easily in src/server/routes/auth/login.js
ldap_api: "localhost/ldap.php"
```

## Roadmap
Though users and/or groups to lists ACLs can be controlled by search-guard, but they are still listed on the kibana page, clicking the index as an unauthorized user would lead to an error. This might be improved by removing unauthorized indecies from kibana in future release.