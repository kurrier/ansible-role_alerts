Ansible Role: alerts
=========

Alert Control and Mangement Role

Requirements
------------

Slack or E-Mail account

Role Variables
--------------

vars/main.yml - Contains default variables [empty by default]

* msg_function_alert: [true/false] - enable/disable alerting functions

## Message Setup: ##
* msg_subject: main subject category of alert
* msg_alert_title: specific alert title
* msg_alert_url: url to where alert originated, if any
* msg_alert_txt: alert message information [for slack]
* msg_alert_body: alert message information [for email]
* msg_alert_lvl: alert level
* msg_job_time: time of alert in epoch time
* msg_job_uuid: unique job id

## Message Display: ##
* msg_footer: application/service message originated
* msg_footer_icon: url to icon's service

## Alert Control: ##
* msg_slack_info: [true/false]
* msg_slack_notice: [true/false]
* msg_slack_warn: [true/false]
* msg_slack_crit: [true/false]
* msg_mail_info: [true/false]
* msg_mail_notice: [true/false]
* msg_mail_warn: [true/false]
* msg_mail_crit: [true/false]

## Basic Setup: ##
Can be setup as global vars

* ansible_slack_token: slack token
* ansible_slack_channel: slack channel

* ansible_mail_host: localhost
* ansible_mail_from: from email host
* ansible_mail_to: to email host

Alert Levels
------------
* 1 - Critical
* 2 - Warning
* 3 - Notice
* 4 - Information

Dependencies
------------

None - can easily be called from other roles/tasks with set_fact.

Example Playbook
----------------

Example:

    - hosts: localhost
      vars:
        msg_function_alert: true
        msg_slack_notice: true
        msg_subject: "Ansible Alert Test"
        msg_alert_title: "Test Completed"
        msg_alert_txt: "sent alert using new ansible role."
        msg_alert_url: ""
        msg_alert_body: "{{ msg_alert_txt }}"
        msg_alert_lvl: 3

        msg_job_time: "{{ lookup('pipe', 'date +%s') }}"
        msg_job_uuid: "12345678"
        
        msg_footer: "RedHat"
        msg_footer_icon: "redhat.png"

      roles:
         - { role: alerts, when msg_alert_txt is defined }

Test
----------------

ansible-playbook tests/test.yml -i tests/inventory


Plans
----------------
- Full Headless support through Docker, then can be called through cron/bash jobs
- Add plans for API notification support

License
-------

Licensed under GPLv3 License. See LICENSE for details.

Author Information
------------------

Nick Lalumiere
