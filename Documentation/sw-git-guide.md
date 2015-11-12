# Smartwebs Git Guide

#### Clone the repo
'''
git clone ssh://user@host/path/to/repo.git
'''

#### Create New Feature
'''
git checkout -b some-feature develop
'''

While working on your feature:
'''
git status
git add <some-file>
git commit
'''

Once feature is complete, create a pull request:
```
git push --set-upstream origin some-feature
```

Confirm you are on the some-feature branch, navigate to Github repo, and submit your pull request.

NOTE: Via Github website, navigate to your recently pushed branch. Click on the green 'Compare, review, create a pull request' button. Review your changes, and submit your pull request with a meaningful comment. After peer or departmental review, your sys admin will manage merging an accepted pull request into the ```develop``` branch.

After some-feature pull request has been reviewed, accepted, and merged:
'''
git checkout develop
git pull upstream develop
git branch -d some-feature
'''

#### Create New Release
'''
git checkout -b release-0.1 develop
'''

This branch is a place to clean up the release, test everything, update the documentation, and do any other kind of preparation for the upcoming release.

NOTE: Release branch is feature-frozen, anything not already in ```develop``` will be pushed to next cycle.

#### Finish New Release
```
git checkout master
git merge release-0.1
git push
git checkout develop
git merge release-0.1
git push
git branch -d release-0.1
```

If push to ```master``` has been completed:
```
git tag -a 0.1 -m "Initial public release" master
git push --tags
```

#### Hotfix
```
git checkout -b issue-#001 master
# Fix the bug
git checkout master
git merge issue-#001
git push
```

```
git checkout develop
git merge issue-#001
git push
git branch -d issue-#001
```
