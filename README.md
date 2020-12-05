# local-repo-cache
Local repo caching using artifactory

Context:  OEL8 free version relies upon repos that are ever updating.  This makes control of delivery difficult.  The same issue exists with EPEL and EPEL-TESTING.  We want to regularly pull in updates from these upstream repos on a monthly basis.  We also want to retain older package versions should we need to roll back or lock installs to a particular version.  We utilize artifactory as our binary artifact repository.

Task 1)

Create a program using Ruby which will, on a regular (modifiable) basis, pull all content from a defined upstream repo at that point in time and store it in a new local repo with date stamp and repo upstream naming format.  You’ll need to support virtual repositories usage and expect to replace any previously existing repo for the same upstream while not deleting that previously repo (we want to archive it, but not resolve from it).

Task 2)

Create a second script in python that would check an upstream repo (EPEL use case) for newer content and versions and download them to a local repo.  This should result in keeping multiple versions of the same package in the local repo where the upstream only maintains latest.
