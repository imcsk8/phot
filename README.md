phot
====

Heat templates to test packstack inside openstack instances

Usage:
====

Packstack review allinone:

heat  stack-create rhos5-instance-test -f packstack_review.yaml -P 'branch=master' -P 'gerrit_review=git fetch https://review.openstack.org/stackforge/packstack refs/changes/11/109011/4 && git cherry-pick FETCH_HEAD'_
