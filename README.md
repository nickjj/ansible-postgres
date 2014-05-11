## What is ansible-postgres?

It is an [ansible](http://www.ansible.com/home) role to install postgres 9.3.

### What problem does it solve and why is it useful?

Often times you just want a single database server without any fuss or headaches. The only thing you need to supply to this role is the username/password it should use for the postgres user account and you're on your way.

It will continue to be updated to provide the latest stable version of postgres.

## Role variables

```
---
postgres_user: deploy
postgres_password: pleasedonthackme
```

## Example playbook

For the sake of this example let's say you have a group called **database** and you have a typical `site.yml` file.

To use this role edit your `site.yml` file to look something like this:

```
---
- name: ensure database servers are configured
- hosts: database

  roles:
    - { role: nickjj.postgres, tags: postgres }
```

Let's say you want to edit the credentials, you can do this by opening or creating `group_vars/app.yml` which is located relative to your `inventory` directory and then making it look something like this:

```
---
postgres_user: hulk
postgres_password: notverysecure

```

#### More secure passwords

If you plan to publish your inventory somewhere and you do not want plain text passwords to be checked in then you must remove the password out of this file. You can use ansible's `lookup` module to have the password stored locally outside of version control and then load it into your inventory. Here is an example:

```
postgres_password: "{{ lookup('password', '/path/to/secrets/' + 'database_password') }}"
```

In the above case `database_password` would be a text file containing your password. You can encrypt this file on your local file system if you want but that is outside of the scope of this documentation.

## Installation

`$ ansible-galaxy install nickjj.postgres`

## Requirements

Tested on ubuntu 12.04 LTS but it should work on other versions that are similar.

## License

MIT