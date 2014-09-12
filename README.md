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

Notes:
=====

For some reason i haven't fixed i the screen command that executes packstack does not
get executed, you have to execute it manually.

