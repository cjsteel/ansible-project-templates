
ansible-role-{{ short_role_name }}
=======================

An Ansible role to install and manage ANFI (Analysis of Functional NeuroImages)


Description
-----------

"**{{ short_role_name }}** is a brain imaging software package developed by ...


Resources
---------

-  http://www.{{ short_role_name }}.net/ 
-  http://www.{{ short_role_name }}.net/fswiki/DownloadAndInstall 
-  https://en.wikipedia.org/wiki/{{ short_role_name }} 



Requirements
------------

### Ubuntu 16.04

```shell
sudo apt-get install libjpeg62
```


Options
-------

- Matlab (only needed to run FS-FAST, the fMRI analysis stream)



Issues
------

On Ubuntu platforms, you may encounter the error "freeview.bin: error while loading shared libraries: libjpeg.so.62: cannot open shared object file: No such file or directory." Freeview will work fine if you install libjpeg62-dev and run: 

```shell
sudo apt-get install libjpeg62-dev
```


Role Variables
--------------

### roles/{{ short_role_name }}/defaults/main.yml

```yaml
# file: roles/{{ short_role_name }}/defaults/main.yml
#
{{ short_role_name }}_arch : 'amd64'
{{ short_role_name }}_ver  : 'v6.0.0'
{{ short_role_name }}_ftp_url: 'ftp://surfer.nmr.mgh.harvard.edu/pub/dist/{{ short_role_name }}/6.0.0/{{ short_role_name }}-Linux-centos6_x86_64-stable-pub-v6.0.0.tar.gz'

# {{ short_role_name }}/FS-FAST (and FSL) environment variables

{{ short_role_name }}_home          : '/usr/local/{{ short_role_name }}'
{{ short_role_name }}_fsfast_home   : '/usr/local/{{ short_role_name }}/fsfast'
{{ short_role_name }}_output_format : 'nii.gz'
{{ short_role_name }}_subjects_dir	 : '/usr/local/{{ short_role_name }}/subjects'
{{ short_role_name }}_mni_dir		 : '/usr/local/{{ short_role_name }}/mni'

# testing 
{{ short_role_name }}_users_test_dir: '~/{{ short_role_name }}/test'
{{ short_role_name }}_subject_samples: 'sample-001.mgz'
```


Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

* [ ansible-role-acemenu ]( https://github.com/cjsteel/ansible-role-acemenu )
* [ ansible-role-ensure_dirs ]( https://github.com/csteel/ansible-role-ensure_dirs )
* [ ansible-role-skel ]( https://github.com/csteel/ansible-role-skel )

### ensure_dirs

#### roles/ansible-role-{{ short_role_name }}/meta/main.yml

```yaml
---
# file: roles/ansible-role-{{ short_role_name }}/meta/main.yml in dependant role
dependencies:

- { role: ensure_dirs, 
        ensure_dirs_on_remote: "{{ {{ short_role_name }}_remote_directories_description }}",
        ensure_dirs_on_local : "{{ {{ short_role_name }}_local_directories_description }}"
  }
```

#### roles/ansible-role-{{ short_role_name }}/defaults/main.yml example

```yaml
{{ short_role_name }}_remote_directories_description:

  {{ short_role_name }}_installation_resources_dir:

    state       : "present"					# absent
    path        : "sys/sw"					# relative to Ansible users home
    owner       : "{{ ansible_ssh_user }}"
    group       : "{{ ansible_ssh_user }}"
    mode        : "0644"

{{ short_role_name }}_local_directories_description:

  {{ short_role_name }}_installation_resources_dir:

    state       : "present"					# absent
    path        : "sys/sw/" 				# relative to Ansible users home dir
    owner       : "{{ ansible_ssh_user }}"
    group       : "{{ ansible_ssh_user }}"
    mode        : "0644"
```


Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
    - hosts: servers
      roles:
         - { role: cjsteel.ansible-role-{{ short_role_name }}, x: 42 }
```



## License

Various, MIT



## Author Information

Christopher Steel on behalf of ACElabs  
Systems Administrator  
McGill Centre for Integrative Neuroscience  
Montreal Neurological Institute  
E-mail: christopherDOTsteel@mcgill.ca  
[mcin-cnim.ca](http://mcin-cnim.ca/)    
[theneuro.ca](http://www.mcgill.ca/neuro/)   

## Open Science



The Neuro has adopted the principles of Open Science. We are inspired by the likes of the Allen Institute for Brain Science, the National Institutes of Health's Human Connectome project, and the Human Genome project. For additional information please see [open science at the neuro]( https://www.mcgill.ca/neuro/open-science-0).





![MCIN](imgs/mcin-logo-brain-140x116.png)          ![neuro](imgs/neuro-logo-160x116.png)  