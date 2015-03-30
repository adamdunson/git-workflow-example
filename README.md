# Git Workflow Example

This repository is an example of the following workflow:

1. Master is in a state you would like to deploy. Make a version branch off master called something like "v_2_6".
2. Change the capistrano deploy file to point to a tag called "v2.6", rather than a branch, and commit it. Tag that commit on that branch with "v2.6".
3. Merge the "v_2_6" branch into master with a PR,  _without_ deleting the branch.
4. Deploy the changes to staging, and production if all looks good.
5. Oh no! We discover a new bug in a serializer on staging/production.
6. We make a branch off of "v_2_6", called "v_2_6_serializer_fix".
7. We fix the bug on the "v_2_6_serializer_fix" branch, and make a PR into "v_2_6".
8. Assuming the PR is approved, we merge it in, and delete "v_2_6_serializer_fix"
9. We change capistrano to deploy a tag called "v2.6.1", and commit this on "v_2_6"
10. We tag this commit "v2.6.1" and push up all tags.
11. Make a PR to Merge "v_2_6" into master again, merge _without_ deleting the branch, thus preserving the latest bugfix on master.
12. Deploy the changes to staging, and production if all looks good.
13. Repeat steps 5-12 as necessary, bumping the minor version each time.
14. When master is in a state where we are ready to launch the next build, make a new branch like "v_2_7" off of master, repeat the process.
