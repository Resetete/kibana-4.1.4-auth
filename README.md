# Kibana 4.1.4 with Authentication

This is a fork of [elastic/kibana](https://github.com/elastic/kibana) with an authentication page. For introductions of Kibana, please refer to the original repository.

Kibana and Elasticsearch's lacking of the ability of authentication has post great danger to sensitive data. This fork adds a login page for kibana to eliminate unauthorized requests.

Current release: 0.0.1-beta2. [中文简介](http://blog.lotuslab.org/post/139361133998/%E6%89%93%E9%80%A0%E5%AE%89%E5%85%A8%E7%9A%84elk).


## Authentication

To use the authentication feature, the following entries must be configured in `kibana.yml`:
```yml
# account for kibana, which should only has the accessibility of the .kibana index
# to add authorization to Elasticsearch, see Security Warning section
kibana_elasticsearch_username: username
kibana_elasticsearch_password: password
# LDAP API for authentication
# this API should accept url parameters name and password
# you can customize this easily in src/server/routes/auth/login.js
ldap_api: "localhost/ldap.php"

# session settings
# session secret, used to generate session ID
session_secret: "keyboard cat"
# session max age, default is one week
session_cookie_max_age: 604800
```

## Security Warning

Please be reminded that, this login page only protects your kibana web client, people are still able to access your elasticsearch without control via kibana proxy: `localhost:5601/elasticsearch`. If you want to protect your Elasticsearch, please have a look at [search-guard](https://github.com/dotSlashLu/search-guard) which is a plugin for Elasticsearch providing fine-grained ACL control.

## Roadmap

Though users and/or groups to indices ACLs can be controlled by search-guard, but they are still listed on the kibana page, clicking the index as an unauthorized user would lead to an error. This might be improved by removing unauthorized indecies from kibana in future release.
