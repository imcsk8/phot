phot
====

Heat templates to test packstack inside openstack instances

Usage:
=====

Packstack review allinone:

    heat  stack-create rhos5-instance-test -f packstack_review.yaml \
      -P 'branch=icehouse' \
      -P 'gerrit_review=git fetch https://review.openstack.org/stackforge/packstack refs/changes/11/109011/4 && git cherry-pick FETCH_HEAD'
      -P 'instance_name=rhos5-mysql' \
      -P 'image=rhos5-test' 
      -e ../your-env.yaml

Create node for RHOSP:

    heat stack-create rhos5-node -f create_rhosp_node.yaml \
      -P 'instance_name=rhel7-node' \
      -P 'image=rhos5-test'
      -e ../your-env.yaml

Create generic node:

    heat  stack-create fedora-20-test -f create_node.yaml
      -P 'instance_name=fedora-20-test' \
      -P 'image=Fedora-20-test' \
      -e ../your-env.yaml


Notes:
=====

For some reason i haven't found the screen command that executes packstack does
not get executed, you have to execute it manually:

    /usr/bin/screen -t packstack -S packstack /usr/bin/packstack -d --allinone


The packstack_review template does not return the floating ip address so you
have to retrieve it manually:

    $ nova list
    +--------------------------------------+-----------------+---------+------------+-------------+-----------------------------------+
    | ID                                   | Name            | Status  | Task State | Power State | Networks                          |
    +--------------------------------------+-----------------+---------+------------+-------------+-----------------------------------+
    | 0b755687-2c20-4319-bc9c-ea7b3ab866dd | juno-test-f20   | SHUTOFF | None       | Shutdown    | testnet=192.168.0.2               |
    | 9a9322a3-3804-4ac7-94f6-d6486728da29 | juno-test-f20-2 | ACTIVE  | None       | Running     | testnet=192.168.0.5, 10.16.18.237 |
    | 09091636-129f-47f7-8397-0ba2c1845850 | rhos5-mysql     | ACTIVE  | None       | Running     | testnet=192.168.0.4, 10.16.18.215 |
    +--------------------------------------+-----------------+---------+------------+-------------+-----------------------------------+

    $ ssh root@10.16.18.215

