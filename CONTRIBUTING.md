## Understanding Patches
Patches to Paper are very simple, but center around the directories 'Cheetah-API' and 'Cheetah-Server'

Assuming you already have forked the repository:

1. Pull the latest changes from the main repository
2. Type `./cheetah patch` in git bash to apply the changes from upstream
3. cd into `Cheetah-Server` for server changes, and `Cheetah-API` for API changes

## Adding Patches
Adding patches to Paper is very simple:

1. Modify `Cheetah-Server` and/or `Cheetah-API` with the appropriate changes
2. Type `git add .` to add your changes
3. Run `git commit` with the desired patch message
4. Run `./cheetah rebuild` in the main directory to convert your commit into a new patch
5. PR your patches back to this repository

Your commit will be converted into a patch that you can then PR into Paper

## Help! I can't find the file I'm looking for!
By default, Paper (and upstream) only import files that we make changes to.
If you would like to make changes to a file that isn't present in Paper-Server's source directory, you
just need to add it to our import script to be ran during the patch process.

1. Save (rebuild) any patches you are in the middle of working on!
2. Identify the names of the files you want to import.
   - A complete list of all possible file names can be found at ```./work/Minecraft/$MCVER/net/minecraft/server```
3. Open the file at `./scripts/importmcdev.sh` and add the name of your file to the script.
4. Re-patch the server `./cheetah patch`
5. Edit away!

This change is temporary! DO NOT COMMIT CHANGES TO THIS FILE!
Once you have made your changes to the new file, and rebuilt patches, you may undo your changes to importmcdev.sh

Any file modified in a patch file gets automatically imported, so you only need this temporarily
to import it to create the first patch.

To undo your changes to the file, type `git checkout scripts/importmcdev.sh`

## Merging upstream
Using the lumi script, make sure to stash or commit all local changes first (and run `lumi rb`, `lumi patch`).
Follow this with `lumi up up` and `lumi patch`. If there aren't any merge conflicts, you're done - else, fix them ;)

## Editing patches
### Method 1
In case you need something more complex or want more control, this step-by-step instruction does
exactly what the above slightly automated system does.

1. If you have changes you are working on type `git stash` to store them for later.
   - Later you can type `git stash pop` to get them back.
2. Type `git rebase -i upstream/upstream`
   - It should show something like [this](https://gist.github.com/zachbr/21e92993cb99f62ffd7905d7b02f3159).
3. Replace `pick` with `edit` for the commit/patch you want to modify, and "save" the changes.
   - Only do this for one commit at a time.
4. Make the changes you want to make to the patch.
5. Type `git add .` to add your changes.
6. Type `git commit --amend` to commit.
   - **MAKE SURE TO ADD `--amend`** or else a new patch will be created.
   - You can also modify the commit message here.
7. Type `git rebase --continue` to finish rebasing.
8. Type `./cheetah rebuild` in the main directory.
   - This will modify the appropriate patches based on your commits.
9. PR your modifications back to this project.

## Method 2 (sometimes easier)
If you are simply editing a more recent commit or your change is small, simply making the change at HEAD and then moving the commit after you have tested it may be easier.

This method has the benefit of being able to compile to test your change without messing with your API HEAD.

1. Make your change while at HEAD
2. Make a temporary commit. You don't need to make a message for this.
3. Type `git rebase -i upstream/upstream`, move (cut) your temporary commit and move it under the line of the patch you wish to modify.
4. Change the `pick` with `f` (fixup) or `s` (squash) if you need to edit the commit message 
5. Type `./cheetah rebuild` in the main directory
   - This will modify the appropriate patches based on your commits
6. PR your modifications to github