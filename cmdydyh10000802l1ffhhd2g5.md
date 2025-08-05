---
title: "Moving Git history"
datePublished: Tue Aug 05 2025 10:17:53 GMT+0000 (Coordinated Universal Time)
cuid: cmdydyh10000802l1ffhhd2g5
slug: moving-git-history
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/RGJlwpeAIBg/upload/51e30e07e0355def915031d3c6a48c10.jpeg
tags: commit, git, history, save

---

I needed to move some files between two repositories. I could have just copied the files over but I wanted to maintain the commit history.

Enter the [git-filter-repo](https://github.com/newren/git-filter-repo) utility that’s based on the native [git-filter-branch](https://git-scm.com/docs/git-filter-branch) command. It does a lot of things but for my use case I only filtered for the folder I need moved.

Here’s what I did:

### Prepare your source repository

```bash
# RE-Clone the source repository (local version will be altered)
git clone /path/to/source-repo source-repo-filtered 
cd source-repo-filtered 

# Extract only the directory you want (keeps full history)
git filter-repo --path directory-to-move/

# Optional: Remove the directory prefix if you want it at the root
git filter-repo --path-rename directory-to-move/:
```

> filtering will remove all other git objects

### Prepare the destination repository

```bash
# Clone or navigate to your destination repository
git clone /path/to/destination-repo destination-repo
cd destination-repo

# Add the local filtered repository as a remote
git remote add source-filtered /path/to/source-repo-filtered

# Fetch the filtered history
git fetch source-filtered
```

### Merge into the destination repository

```bash
# Create a new branch for the merge
git checkout -b merge-directory

# Merge the filtered history (allows unrelated histories)
git merge source-filtered/main --allow-unrelated-histories

# If you want the directory in a specific location, you might need additional renaming
# For example, to put it in a subdirectory:
git filter-repo --path-rename :new-location/
```

> review the branch before you merge

### Clean up the destination repository

```bash
# Remove the temporary remote
git remote remove source-filtered

# Clean up the filtered repository clone
rm -rf /path/to/source-repo-filtered

# Clone the source repository again
git clone /path/to/source-repo source-repo-filtered 
cd source-repo-filtered 

# Delete a moved folder
git filter-repo --path directory-moved/ --invert-paths

# update the remote
git push --force
```

## References:

* [https://github.com/newren/git-filter-repo](https://github.com/newren/git-filter-repo)
    
* [https://git-scm.com/docs/git-filter-branch](https://git-scm.com/docs/git-filter-branch)