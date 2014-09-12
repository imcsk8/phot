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

For some reason i haven't found the screen command that executes packstack does not
get executed, you have to execute it manually:

    /usr/bin/screen -t packstack -S packstack /usr/bin/packstack -d --allinone



