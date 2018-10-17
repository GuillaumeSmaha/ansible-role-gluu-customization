Ansible Gluu: Customization role
==========

**gluu-customization** is an Ansible role to easily customize files on a Gluu Server by copying XHTML page, images, style resouce or by editing WAR file to update translations for example.


- [Requirements](#requirements)
- [Installation](#installation)
- [Update](#update)
- [Role Variables](#role-variables)
- [Deploying](#deploying)
- [Example Playbook](#example-playbook)
- [Sample projects](#sample-projects)

History
-------

Gluu's open source authentication & API access management server enables organizations to offer single sign-on, strong authentication, and centralize.

Requirements
------------

In order to deploy, you will need:

* Ansible in your deployer machine


Installation
------------

**gluu-customization** is an Ansible role distributed globally using [Ansible Galaxy](https://galaxy.ansible.com/). In order to install **gluu-customization** role you can use the following command.

```
$ ansible-galaxy install GuillaumeSmaha.gluu-customization
```


Update
------

If you want to update the role, you need to pass **--force** parameter when installing. Please, check the following command:

```
$ ansible-galaxy install --force GuillaumeSmaha.gluu-customization
```


Role Variables
--------------


```yaml
vars:

  # Define a custom version of the package to install.
  # To get a list of available package versions visit: https://gluu.org/docs/ce/
  gluu_version: 3.1.4

  # List of files to copy in /etc/gluu/conf inside the Gluu container
  # Can use Jinja template
  # Example:
  # gluu_copy_configuration_files:
  #   - 'template/configuration/auth_multi_ldap.json'
  gluu_copy_configuration_files:

  # List of XHTML page to copy into the directory /etc/gluu/jetty/{{ module }}/custom/pages
  # An optional 'dest' parameter is available
  # Can use Jinja template; so it is possible to use relative path from the 'templates' directory
  # Example:
  # gluu_copy_pages:
  #   oxauth:
  #     - path: 'template/pages/login.xhtml'
  #     - path: 'template/pages/login_template.xhtml'
  #       dest: 'WEB-INF/incl/layout/login-template.xhtml'
  gluu_copy_pages:

  # List of resources for page to copy into the directory /etc/gluu/jetty/{{ module }}/custom/static
  # Can NOT use Jinja template. So you have to specify an absolute path.
  # Example:
  # gluu_copy_resources:
  #   oxauth:
  #     - path: '{{ playbook_dir }}/templates/custom/oxauth/static/logo.svg'
  #       dest: 'img/logo.svg'
  #     - path: '{{ playbook_dir }}/templates/custom/oxauth/static/error.png'
  #       dest: 'img/error.png'
  gluu_copy_resources:


  # List of files to copy into the WAR file.
  # The WAR file will be unzipped, the files will be copied and he archive will be recreated.
  # Can use Jinja template; so it is possible to use relative path from the 'templates' directory
  # Example to customize languages available and translation:
  # gluu_customize_wars:
  #   oxauth:
  #     - path: 'wars/oxauth/messages_fr.properties'
  #       dest: 'WEB-INF/classes/messages_fr.properties'
  #     - path: 'wars/oxauth/messages_en.properties'
  #       dest: 'WEB-INF/classes/messages_en.properties'
  #     - path: 'wars/oxauth/faces-config.xml'
  #       dest: 'WEB-INF/faces-config.xml'
  gluu_customize_wars:
```

Deploying
---------

In order to deploy, you need to perform some steps:

* Create a new `hosts` file. Check [ansible inventory documentation](http://docs.ansible.com/intro_inventory.html) if you need help.
* Create a new playbook for deploying your app, for example, `deploy.yml`
* Set up role variables (see [Role Variables](#role-variables))
* Include the `GuillaumeSmaha.gluu-customization` role as part of a play
* Run the deployment playbook

```ansible-playbook -i hosts deploy.yml```

If everything has been set up properly, this command will install Gluu Cluster Manager on the host.


Example Playbook
----------------

In the folder, example you can check an example project that shows how to deploy.

In order to run it, you will need to have Vagrant and the role installed. Please check https://www.vagrantup.com for more information about Vagrant and our Installation section.

```
$ cd example
$ vagrant plugin install vagrant-lxc
$ vagrant plugin install vagrant-hostmanager
$ vagrant up --provider=lxc
$ ansible-galaxy install GuillaumeSmaha.gluu-setup GuillaumeSmaha.gluu-customization
$ ansible-playbook -i env/ubuntu deploy.yml
$ ansible-playbook -i env/centos deploy.yml
```

Access to Gluu by going to:

https://gluu-customization-ubuntu/

or

https://gluu-customization-centos/


Sample projects
---------------
You can find a full example of a playbook here:

https://github.com/GuillaumeSmaha/ansible-gluu-playbook

