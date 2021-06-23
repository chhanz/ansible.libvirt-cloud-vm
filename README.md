# ansible.libvirt-cloud-vm

Role Name
=========

ansible.libvirt-cloud-vm

Requirements
------------

* You must enable virtualization in the BIOS.
* All CPUs must have support for the Intel® 64 or AMD64 CPU extensions, and the AMD-V™ or Intel VT® hardware virtualization extensions enabled.
* Support for the No eXecute flag (NX) is also required. 

Support Operation System
------------

* `RHEL 7` and latest version
* `CentOS 7` and latest version

Role Variables
--------------

* defaults/main.yml
```
## installation 'KVM'
install_libvirt: true
## please choice 'centos' & 'rhel'
provide_os: centos
## default cloud image location
cloud_img_store: /var/lib/libvirt/images

## please import 'rhel-kvm-image'
rhel_cloud_img: /var/lib/libvirt/images/rhel-server-7.7-x86_64-kvm.qcow2

## support os version.
# centos610 : CentOS release 6.10 (Final)
# centos71 : Derived from Red Hat Enterprise Linux 7.1 (Source)
# centos72 : CentOS Linux release 7.2.1511 (Core)
# centos73 : CentOS Linux release 7.3.1611 (Core)
# centos74 : CentOS Linux release 7.4.1708 (Core)
# centos75 : CentOS Linux release 7.5.1804 (Core)
# centos76 : CentOS Linux release 7.6.1810 (Core)
select_version: centos76

## default configure 'KVM' network
kvm_network: default

## default configure 'VM' resource
vm_cpu: 2
# please input 'MiB'
vm_mem: 1024
# please input 'GB'
vm_disk_size: 10
```

Example Playbook
----------------
* Default playbook
```
- hosts: servers
  become: true         ## If it's a user
  roles:
    - { role: ansible.libvirt-cloud-vm }
```
* Example inventory
```
[nodes]

## example inventory

## example deploy 'rhel'
#vm-rhel77-0  ansible_host="hypervisor-ip" provide_os="rhel"
#vm-rhel77-1  ansible_host="hypervisor-ip" provide_os="rhel"
#vm-rhel77-2  ansible_host="hypervisor-ip" provide_os="rhel" vm_disk_size="22"

## example deploy 'centos'
vm-centos-610 ansible_host="hypervisor-ip" provide_os="centos" vm_cpu="1" vm_mem="1024" select_version="centos610"
vm-centos-72  ansible_host="hypervisor-ip" provide_os="centos" vm_cpu="2" vm_mem="1024" select_version="centos72"
vm-centos-71  ansible_host="hypervisor-ip" provide_os="centos" vm_cpu="3" vm_mem="1024" select_version="centos71"
vm-centos-73  ansible_host="hypervisor-ip" provide_os="centos" vm_cpu="1" vm_mem="1024" select_version="centos73"
vm-centos-74  ansible_host="hypervisor-ip" provide_os="centos" vm_cpu="2" vm_mem="2048" select_version="centos74"
vm-centos-75  ansible_host="hypervisor-ip" provide_os="centos" vm_cpu="3" vm_mem="2048" select_version="centos75"
vm-centos-76  ansible_host="hypervisor-ip" provide_os="centos" vm_cpu="4" vm_mem="2048" select_version="centos76" vm_disk_size="15"
```

* Installation 'KVM'   
If you want to install the hypervisor, do the following.
(use tag `install-libvirt`)
    ```
    $ ansible-playbook -i <inventory file> <playbook file> --tags install-libvirt
    ```

* Create vm 'CentOS'   
If you need to create 'centos' vm, do the following command.
(use tag `centos`)

    ```
    $ ansible-playbook -i <inventory file> <playbook file> --tags centos
    ```

* Create vm 'RHEL'   
If you need to create 'rhel' vm, do the following command.
(use tag `rhel`)

    ```
    $ ansible-playbook -i <inventory file> <playbook file> --tags rhel
    ```

* Create vm    
If you need to create a vm, do the following command.
(use tag `create-vm`)   
*** *Important* It must be set to variable.***
    ```
    $ ansible-playbook -i <inventory file> <playbook file> --tags create-vm
    ```
* ***Users and passwords set by default for the VM are as follows.***   
    ```
    id : root
    pw : testtest
    ````

* Destroy vm   
If you need to delete the vm, do the following command.
(use tag `destory-vm`)

    ```
    $ ansible-playbook -i <inventory file> <playbook file> --tags destroy-vm -e ask_remove=yes
    ```

Author Information
------------------

chhanz [han0495@gmail.com](mailto:han0495@gmail.com)
