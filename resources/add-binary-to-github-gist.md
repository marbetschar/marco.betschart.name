---
description: >-
  A neat little trick to keep binaries around which might disappear otherwise -
  or simply to add pictures to your Gists
---

# Add Binary to GitHub Gist

## How to add a binary file to a GitHub Gist

First make sure `git` is installed on the local machine and then:

1. Create a new [Gist](https://gist.github.com)
2.  Clone to your local machine (replace `<hash>` with your Gist's hash):

    ```
    git clone git@gist.github.com:<hash>.git gist
    ```
3.  Add and commit the binary:

    ```
    cd gist
    git add VCForPython27.msi
    git commit -m "Added VCForPython27.msi binary"
    ```
4.  Push changes to GitHub:

    ```
    git push origin
    ```

### Acknowledgements

Credit [goes to Mark](https://remarkablemark.org/blog/2016/06/16/how-to-add-image-to-gist/) for this great trick!
