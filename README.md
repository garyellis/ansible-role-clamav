clamav
===============
A simple Ansible role to install clamav on ubuntu linux hosts

* installs clamav
* optionallly installs clamav-unofficial-sigs
* runs virus definition updates
* optionally creates cron jobs to update virus def updates and clamscan

Requirements
------------

* Ansible 2+
* root access


Dependencies
------------
None


Role Variables
--------------
The following role variable defaults can be overridden as needed

    # set to true to configure clamav db refresh and scan jobs
    clamav_enable_cron: false
    # job day and hour are configurable. override defaults values as needed
    clamav_db_refresh_hr: 7
    clamav_db_refresh_min: "{{59 |random}}"
    clamav_db_unofficial_refresh_hr: 7
    clamav_db_unofficial_refresh_min: "{{59 |random}}"
    clamav_scan_hr: 8
    clamav_scan_min: "{{59 |random}}"
    # set the nice level on clamav cron jobs
    clamscan_nice: 19



Usage
-----
The following playbook yml installs clamav and schedules jobs to run at default times

    - hosts: all
      user: vagrant
      become: yes
      vars:
        clamav_enable_cron: true
      roles:
        - clamav



License
-------
MIT

Author
------
*Gary Ellis* <gary.luis.ellis@gmail.com>

