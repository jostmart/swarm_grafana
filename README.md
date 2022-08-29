Grafana Swarm
=========

Quick hack to deploy Grafana in Docker Swarm.


Example Playbook
----------------



    # Tasks that only need to be executed on a single swarm node

    - name: Deploy containers on swarm
      hosts: docker_swarm_deploytarget
      become: yes

      # These tasks, is added in order to pull a local Grafana build.
      tasks:
        - name: Log into private registry and force re-authorization
          community.general.docker_login:
            registry_url: "registry.foobar.local"
            username: "grafana_pull_account"
            password: "{{ grafana_registry_access_token }}"
            reauthorize: yes

        - name: Pull an image
          community.docker.docker_image:
            name: "{{ grafana_image }}"
            source: pull
            force_source: yes

      roles:
         - { role: swarm_grafana }

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
