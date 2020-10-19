# autorebuild-template

This template can help you track a upstream repo from github.  
When upstream pulish a new release, auto update version & download source archive.  
They will push to your repo, then you can trigger your copr rebuild by github webhook.

# Reborned

> Use Makefile instead of rpkg to make srpm, so we don’t have to put the tarball in the repository anymore.

# Speicial Thanks
- [pozetroninc/github-action-get-latest-release](https://github.com/pozetroninc/github-action-get-latest-release)
