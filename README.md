# local-repo-cache
Local repo caching using artifactory

**********

THIS PROJECT IS ABANDONED DUE TO THE FREE VERSION OF ARTIFACTORY NOT BEING COMPATIBLE WITH EXISTING SERVICES ON MY DEV BOX.

Yes, I'm bing lazy in not wanting to troubleshoot someone else's Java just to be able to do a demo project. It's an awesome idea, but the up-front hassles of trying to get the open-source version of artifactory configured on a machine with other needed services running isn't worth my time. I may revist it later if I get another dedicated system to develop with.

**********

Context:  OEL8 free version relies upon repos that are ever updating.  This makes control of delivery difficult.  The same issue exists with EPEL and EPEL-TESTING.  We want to regularly pull in updates from these upstream repos on a monthly basis.  We also want to retain older package versions should we need to roll back or lock installs to a particular version.  We utilize artifactory as our binary artifact repository.

Task 0)

In order to write-test-write any of this, a working version of artifactory and mariadb has to be installed on the dev system. This is a non-trivial task. The artifactory software used is the open source version, and requires tomcat, which threatens to clobber the existing web server on my system. The configuration for a minimal system is pretty complex, and overengineered.

Artifactory supports multiple source repos and a virtual repo combining elements cherry picked from other repos. Great idea, but I'm not liking the Swiss army knife configs. 

Task 1)

Create a program using Ruby which will, on a regular (modifiable) basis, pull all content from a defined upstream repo at that point in time and store it in a new local repo with date stamp and repo upstream naming format.  You’ll need to support virtual repositories usage and expect to replace any previously existing repo for the same upstream while not deleting that previously repo (we want to archive it, but not resolve from it).

Task 2)

Create a second script in python that would check an upstream repo (EPEL use case) for newer content and versions and download them to a local repo.  This should result in keeping multiple versions of the same package in the local repo where the upstream only maintains latest.
