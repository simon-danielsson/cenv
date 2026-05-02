<h2 align="center">cenv</h2>
  
<p align="center">
    <img src="https://img.shields.io/badge/license-MIT-green?style=flat-square" alt="MIT License" />
  <img src="https://img.shields.io/github/last-commit/simon-danielsson/cenv/main?style=flat-square&color=blue" alt="Last commit" />
</p>
  
<p align="center">
  <a href="#info">Info</a> •
  <a href="#install">Install</a> •
  <a href="#usage">Usage</a> •
  <a href="#license">License</a>
</p>  
  
---
<div id="info"></div>

## Info
  
cenv assumes that everything required to build and maintain a C project should live within the codebase itself. It is an *opinionated* development environment built for developing small to medium sized C projects.
  
Prerequisites:  
- git  
- curl  
- a C compiler  
  
> [!IMPORTANT]  
> 1. No support for Windows. Only unix systems.
> 2. Since cenv is heavily opinionated and built for my own specific workflow, I can't
> guarantee that this will function properly on your computer (or be enjoyable
> to use.)
  
cenv relies on [nob.h](https://github.com/tsoding/nob.h) (a header-only
build-system) for compilation.  
  
---
<div id="install"></div>

## Install
  
[cenv-init.sh](./cenv-init.sh) is what you will be using to build new cenv projects - add it as an alias in your `.bashrc`:  
  
``` bash
# ~/.bashrc

# cinit script
alias cinit="$HOME/path/to/cenv-init.sh"

# this function lets you launch cenv from anywhere
# within your cenv project folder (assuming you have
# a .gitignore in its root)
cenv() {
    local dir="$(pwd)"
    while [[ "$dir" != "/" ]]; do
        if [[ -f "$dir/cenv" ]]; then
            (cd "$dir" && ./cenv "$@")
            return
        fi
        dir="$(dirname "$dir")"
    done
    echo "cenv: no project root found" >&2
    return 1
}
```
  
---
<div id="usage"></div>
  
## Usage
  
Run cinit in your destination folder with the project name as an argument, then run the help command to get started:  
  
``` bash
cinit my_project
cd my_project
cenv help
```
   
When you run `cenv help` you will see the following commands:
  
``` terminal
cenv debug
│ compile into and run from './build/debug' with debug options
╰ default command
cenv release
╰ compile into and run from './build/release' with optimizations
cenv test
│ compile into and run from './build/tests' directory with debug options
╰ the source folder used for this command is './tests'

cenv doc
│ auto-generate docs from './src' and open in browser
╰ this command is still in the experimental stage
cenv tidy
╰ clean up log, debug and object files
cenv help
╰ display help
```
  
---
<div id="license"></div>

## License
  
This project is licensed under the [MIT License](https://github.com/simon-danielsson/cenv/blob/main/LICENSE).  
 
