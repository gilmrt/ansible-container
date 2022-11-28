role_ubuntu
===========

Why this role?
--------------
This role MUST contain every ressources specific to a role.

This role MUST NOT contain variables related to the environment or to the site. They MUST be in the inventory group_vars.


Content
-------

Files:
- defaults/main.yml: variables related to the role (MUST NOT be site or environment related)
- meta/main.yml: the dependencies for the role (typically the distribution to use)

Folders
- templates: files to be deployed for this role (we suggest using templates/ rather than files/ to use the {{ansible_managed}} tag)
- tasks: common tasks expected for each profile (to ease maintenance)
