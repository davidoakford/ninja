Notes to myself on all the steps to make for a Ninja release.

### Push new release branch:
1. Run afl-fuzz for a day or so and run ninja_test
2. Consider sending a heads-up to the ninja-build mailing list first
3. Make sure branches 'master' and 'release' are synced up locally
4. Update src/version.cc with new version (with ".git"), then
   ```
   git commit -am 'mark this 1.5.0.git'
   ```
5. git checkout release; git merge master
6. Fix version number in src/version.cc (it will likely conflict in the above)
7. Fix version in doc/manual.asciidoc (exists only on release branch)
8. commit, tag, push (don't forget to push --tags)
   ```
   git commit -am v1.5.0; git push origin release
   git tag v1.5.0; git push --tags
   # Push the 1.5.0.git change on master too:
   git checkout master; git push origin master
   ```
9. Construct release notes from prior notes

   credits: `git shortlog -s --no-merges REV..`


### Release on GitHub:
1. Go to [Tags](https://github.com/ninja-build/ninja/tags)
2. Open the newly created tag and select "Create release from tag"
3. Create the release which will trigger a build which automatically attaches
   the binaries

### Make announcement on mailing list:
1. copy old mail

### Update website:
1. Make sure your ninja checkout is on the v1.5.0 tag
2. Clone https://github.com/ninja-build/ninja-build.github.io
3. In that repo, `./update-docs.sh`
4. Update index.html with newest version and link to release notes
5. `git commit -m 'run update-docs.sh, 1.5.0 release'`
6. `git push origin master`
