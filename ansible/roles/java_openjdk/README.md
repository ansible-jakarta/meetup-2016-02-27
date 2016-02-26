# shared/java_openjdk #

Installs OpenJDK Java.

- Supports versions: 6, 7, 8.
- Supports modes: jdk, jre-headless, jre.
- Supports installation from ppa:openjdk-r/ppa (required to install version 8).

## Requirements ##

This role requires Ansible 2.0 or higher.

## Role Variables ##

    - name: java_openjdk_version
      desc: Version of OpenJDK Java to install
      default: 8
    - name: java_openjdk_package
      desc: Whether to install 'jdk', 'jre' or 'jre-headless'
      default: jre-headless
    - name: java_openjdk_use_ppa
      desc: Use the OpenJDK-R Java PPA repository
      default: true

## Dependencies ##

None.

## Example Playbook ##

Install OpenJDK Java 8 (headless, JRE-only, from PPA):

    - hosts: all
      roles:
        - role: shared/java_openjdk

Install OpenJDK Java 7 (complete, JRE-only, from PPA):

    - hosts: all
      roles:
        - role: shared/java_openjdk
          java_openjdk_version: 7
          java_openjdk_package: jre

Install OpenJDK Java 7 (JDK, from default source):

    - hosts: all
      roles:
        - role: shared/java_openjdk
          java_openjdk_version: 7
          java_openjdk_package: jdk
          java_openjdk_use_ppa: false

License
-------

BSD

Author Information
------------------

Based on java role by Kevin Brebanov
