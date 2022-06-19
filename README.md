# codecio.github.io_source
This repository contains the source to build and publish codecio.github.io

## Test and build

Install project tooling:

    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    brew install hugo
    git clone --recurse-submodules https://github.com/codecio/codecio.github.io_source.git
    cd codecio.github.io_source.git

Draft new content and posts and preview locally. Once happy commit and let the pipeline handle the deployment.

    hugo server -D

## Acknowledgements

* [Hugo Quick Start](https://gohugo.io/getting-started/quick-start/)
* [Hugo Themes - hello-friend-ng by Djordje Atlialp](https://github.com/rhazdon/hugo-theme-hello-friend-ng/)
* [Create a website with hugo and gh](https://www.mytechramblings.com/posts/create-a-website-with-hugo-and-gh/)
* [GitHub Actions for Hugo](https://github.com/marketplace/actions/hugo-setup)
