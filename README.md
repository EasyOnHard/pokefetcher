# Welcome to Pokefetcher!
Pokefetcher is a program that I made because I like pokemon and I use Linux (arch btw), so it was only natural.

# How does it work?
The program is quite simple, as intended. It is a small zsh script file that pulls data from [PokéAPI](https://pokeapi.co), which has LOADS of data to pull from. 

![Example of Pokefetcher in Action](img/Example_v2.1.0.png)

Above: v2.1.0

As of now (v2.1.0), the program can pull Evolution Chains, Types, Variants, and Egg Groups

To use the program, you run `zsh pokefetcher.zsh -p <pokemon> [Flags]`. The flags are as follows:

- -t, --types: Fetch Types
- -f, --forms: Fetch Variants
- -e, --egg-groups: Displays Egg Groups
- -a, --all-pokemon: Fetch both Types and Forms.
- --no-img: No Image
- --shiny: Displays the Image as a Shiny
- --animated-image: Displays the Image as a .gif
- -h, --help: View the Help menu
- -v, --version: Displays Version Number

# Installation
The program is just a Z Shell script, so you can just download it and use it as is, or you can grant it execution privileges, add it to PATH, and run it from anywhere!

I am not a Linux wiz, so I don't want to give an `install.sh` for saftey's sake (for now), but here is what I have done:

`chmod +x pokefetcher`

Add where ever the file is to PATH in `~/.zshrc` or move it to `/bin`. You can add a directory to the PATH by adding  the line `export PATH="$PATH:where/your/script/file/is"`.

And just like that, you should be able to run the file from anywhere! Make sure that it doesn't conflict with any other programs!


If you have questions, run `pokefetcher -h`, examine the script, or [submit an issue](https://github.com/EasyOnHard/pokefetcher/issues/new). I will try to respond when I can.

# Planned Changes
I might add all of these, I may add none, but they are things that I would like to see in the program.

- TLDR (Teal Deer) Page
- Support for more verbose evolution details (level, other requirements)
- ~~--egg-group~~, --stats, and --gender-ratio flags

# Known Issues
Only Kitty and Konsole supports `kitten icat`, which is used to display images. If you do not use these terminals, use the `--no-image` flag.

# Disclaimer
Pokefetcher is an unofficial tool and is not affiliated with, endorsed, or licensed by the **The Pokémon Company**, **Game Freak**, or **Nintendo**. All Pokémon-related content (including images, names, and other trademarks) are the property of their respective owners. This tool is made for personal use only. I do not own or claim to own any Pokémon-related content gathered or distributed by this program.