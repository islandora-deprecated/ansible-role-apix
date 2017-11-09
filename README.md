# Ansible Role: API-X

An Ansible role that installs [API-X](https://github.com/fcrepo4-labs/fcrepo-api-x) in a Karaf container on:

* Centos/RHEL 7.x
* Ubuntu Xenial

## Role Variables

Available variables are listed below, along with default values:

API-X maven repository:
```
apix_feature_repo: mvn:org.fcrepo.apix/fcrepo-api-x-karaf/LATEST/xml/features
```

API-X features to install:
```
apix_feature:
  - fcrepo-api-x
  - fcrepo-indexing-triplestore
  - fcrepo-service-camel
```

Karaf configuration directory:
```
apix_karaf_etc_dir: "{{ karaf_install_symlink }}/etc"
```

API-X configuration settings:
```
apix_config:
  - pid: org.fcrepo.apix.registry.http
    settings:
      timeout.socket.ms: 1000
  - pid: org.fcrepo.camel.indexing.triplestore
    settings:
      input.stream: activemq:topic:fedora
      triplestore.reindex.stream: activemq:queue:triplestore.reindex
      triplestore.baseUrl: http://localhost:8080/bigdata/namespace/kb/sparql
```

## Dependencies

* None
  
## Example Playbook

    - hosts: webservers
      roles:
        - { role: islandora.apix }

## License

MIT