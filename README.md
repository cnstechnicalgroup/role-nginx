Role: cns.nginx
========

This role installs and configures a single nginx site.

Requirements
------------

Nothing, it runs out of the box.

Role Variables
--------------

In the current version, you can specify the following variables:

| Name                  | Default |                                                              |
|-----------------------|---------|--------------------------------------------------------------|
| web_root              |   ---   | Main root for prestashop install.                            |
| site_public_url       |   ---   | Site URL. The primary site URL.                              |
| cdn_endpoint          |   ---   | Primary CDN end-point.                                       |
| rewrite_rules         |   ---   | List containing custom nginx rewrite rules. (see below)      |


Rewrite rules variable format
-----------------------------
```yaml

# This list contains custom rewrite rules
# Single quote any rule that contains double quotes

rewrite_rules:
  - '"^/c/([0-9]+)(\-[_a-zA-Z0-9-]*)/(.*)\.jpg$" {{ cdn_endpoint }}/img/c/$1$2.jpg last;'
  - '"^/c/([_a-zA-Z-]+)/(.*)\.jpg$" {{ cdn_endpoint }}/img/c/$1.jpg last;'
  - ^/page-not-found$ /index.php?controller=404 last;
  - ^/address$ /index.php?controller=address last;
```

Dependencies
------------

This package has no dependencies.

License
-------

GPLv2

Author Information
------------------

Created by Sam Morrison
https://www.twitter.com/samcns

Examples
--------

```yaml
---
- name: common role test
  hosts: all
  roles:
    - cns.nginx
```
