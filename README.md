# pokesprite

Inspired by [msikma/pokesprite](https://github.com/msikma/pokesprite), this repo
is a simplified version that generates a spritesheet and stylesheet that are
meant to be used for [PokedexTracker](https://pokedextracker.com).

I mainly added various sprites from gen 8 and 9, including various fan-made sprites
in order to make (almost?) everything fit in a 32x32 grid like how it was in
the 3ds gens, removed all shiny sprites and various variants and also some
small changes like making the sprite names 4 digits.

---------------------------

Credits for the small sprites:

[Ezerart](https://www.deviantart.com/ezerart/art/Pokemon-Gen-9-Icon-sprites-3DS-Style-944211258): Most Gen 9 sprites

[Larryturbo](https://www.deviantart.com/larryturbo/art/Gen-8-Galar-Menu-Box-Sprites-32x32-16-819999589): Most Gen 8 

GhostaboArt: electrode-h, wooper-paldea

MrGalleom: Arcanine-h, Slowbro-g, Slowking-g, Glastrier, Spectrier, Zarude, Melmetal, Kleavor

Pikafan200, multidiegodani and MBCmechachu: Other hisuian sprites

---------------------------

It currently consists of 6 scripts:

- `rename` - This renames icons from
  [msikma/pokesprite](https://github.com/msikma/pokesprite) to names that can be
  used by the other scripts. Only use this one if you're copying sprites from
  that repo. Read the comment at the top of the file for more info.
- `chop` - This takes in a JSON file explaining the details of an existing
  spritesheet, and it chops it up into individual images.
- `scale` - This takes any images in the `images` directory that are greater
  than the threshold (default 100px) in either dimension (height or width) and
  either scales it by the provided factor (default 0.5) or to the set dimensions
  passed in. This script will modify the images in place.
- `trim` - This takes all images in the `images` directory and trims any excess
  transparency from it. This is so that we can center the sprites based on
  content (non-transparent pixels) and control the padding through CSS.
- `spritesheet` - This takes all the images in the `images` directory and
  stitches them together into a single image.
- `scss` - This uses the images in the `images` directory to generate a `.scss`
  file that lists classes with the correct positions so the spritesheet can be
  used.
- `copy` - This takes the final outputs (the spritesheet and the `.scss` file)
  and copies them into their appropriate location in
  [pokedextracker/pokedextracker.com](https://github.com/pokedextracker/pokedextracker.com).
  It assumes that this repo and that repo are both cloned in the same parent
  directory. If that is not the case, this script will err.

To run any of them, it's a simple `task` command:

```sh
task rename
task chop -- data.json
task scale
task trim
task spritesheet
task scss
task copy
```

## Setup

### Task

Instead of `make`, this project uses [`task`](https://taskfile.dev/#/). It seems
to be a bit cleaner for some specific things that we want to do.

You can find instructions on how to install it
[here](https://taskfile.dev/#/installation).

### Go

To have everything working as expected, you need to have a module-aware version
of Go installed (v1.11 or greater) and `pngcrush`.

To install Go, you can do it any way you prefer. We recommend using
[`goenv`](https://github.com/syndbg/goenv) so that you can use the correct
version of Go for different projects depending on `.go-version` files. In its
current state, the v2 beta of `goenv` can't be installed through `brew`
normally, so you need to fetch from `HEAD` using the following command:

```sh
brew install --HEAD goenv
```

**Note**: If you already have a v1 version of `goenv` installed, you need to
uninstall it first.

Once installed, you can go into this projects directory and run the following to
install the correct version of Go:

```sh
goenv install
```

### `pngcrush`

`pngcrush` is required for the `spritesheet` command. To install it, you can
just run the following command:

```sh
task setup
```
