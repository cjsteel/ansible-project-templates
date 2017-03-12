ansible-role-freesurfer
=======================

An Ansible role to install and manage ANFI (Analysis of Functional NeuroImages)


Description
-----------

"**FreeSurfer** is a brain imaging software package developed by the Athinoula A. Martinos Center for Biomedical Imaging at Massachusetts General Hospital for analyzing magnetic resonance imaging (MRI) scan data.

It is an important tool in functional brain mapping and facilitates the visualization of the functional regions of the highly folded cerebral cortex.

It contains tools to conduct both volume based and surface based analysis, which primarily use the white matter surface. FreeSurfer includes tools for the reconstruction of topologically correct and geometrically accurate models of both the gray/white and pial surfaces, for measuring cortical thickness, surface area and folding, and for computing inter-subject registration based on the pattern of cortical folds. In addition, an automated labeling of 35 non-cortical regions is included in the package."

Resources
---------

-  http://www.freesurfer.net/ 
-  http://www.freesurfer.net/fswiki/DownloadAndInstall 
-  https://en.wikipedia.org/wiki/FreeSurfer 

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

### roles/freesurfer/defaults/main.yml

```yaml
# file: roles/freesurfer/defaults/main.yml
#
freesurfer_arch : 'amd64'
freesurfer_ver  : 'v6.0.0'
freesurfer_ftp_url: 'ftp://surfer.nmr.mgh.harvard.edu/pub/dist/freesurfer/6.0.0/freesurfer-Linux-centos6_x86_64-stable-pub-v6.0.0.tar.gz'

# FreeSurfer/FS-FAST (and FSL) environment variables

freesurfer_home          : '/usr/local/freesurfer'
freesurfer_fsfast_home   : '/usr/local/freesurfer/fsfast'
freesurfer_output_format : 'nii.gz'
freesurfer_subjects_dir	 : '/usr/local/freesurfer/subjects'
freesurfer_mni_dir		 : '/usr/local/freesurfer/mni'

# testing 
freesurfer_users_test_dir: '~/freesurfer/test'
freesurfer_subject_samples: 'sample-001.mgz'
```

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

* [ ansible-role-acemenu ]( https://github.com/cjsteel/ansible-role-acemenu )
* [ ansible-role-ensure_dirs ]( https://github.com/csteel/ansible-role-ensure_dirs )
* [ ansible-role-skel ]( https://github.com/csteel/ansible-role-skel )

### ensure_dirs

#### roles/ansible-role-freesurfer/meta/main.yml

```yaml
---
# file: roles/ansible-role-freesurfer/meta/main.yml in dependant role
dependencies:

- { role: ensure_dirs, 
        ensure_dirs_on_remote: "{{ freesurfer_remote_directories_description }}",
        ensure_dirs_on_local : "{{ freesurfer_local_directories_description }}"
  }
```

#### roles/ansible-role-freesurfer/defaults/main.yml example

```yaml
freesurfer_remote_directories_description:

  freesurfer_installation_resources_dir:

    state       : "present"					# absent
    path        : "sys/sw"					# relative to Ansible users home
    owner       : "{{ ansible_ssh_user }}"
    group       : "{{ ansible_ssh_user }}"
    mode        : "0644"

freesurfer_local_directories_description:

  freesurfer_installation_resources_dir:

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
         - { role: cjsteel.ansible-role-freesurfer, x: 42 }
```

License
-------

MIT

Author Information
------------------

Christopher Steel
Systems Administrator
McGill Centre for Integrative Neuroscience
Montreal Neurological Institute
McGill University
3801 University Street
Montréal, QC, Canada H3A 2B4
Tel. No. +1 514 398-2494
E-mail: christopherDOTsteel@mcgill.ca
[MCIN](http://mcin-cnim.ca/), [theneuro.ca](http://theneuro.ca)
