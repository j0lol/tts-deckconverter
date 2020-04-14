# Tabletop Simulator TCG Deck Converter

![build](https://github.com/jeandeaual/tts-deckconverter/workflows/build/badge.svg)
![test](https://github.com/jeandeaual/tts-deckconverter/workflows/test/badge.svg)

Generate card decks for [Tabletop Simulator](https://www.tabletopsimulator.com/).

Inspired by [decker](https://github.com/Splizard/decker) and [Frogtown](https://www.frogtown.me/).

## Features

* Generate a Tabletop Simulator deck with thumbnail from an existing website or file.

* Import from the following website:

    * <https://deckstats.net>
    * <https://tappedout.net>
    * <https://deckbox.org>
    * <https://www.mtggoldfish.com>
    * <https://ygoprodeck.com>
    * <https://yugiohtopdecks.com>

* Import from the following files:

    * `*.dec`
    * `*.cod`
    * `*.ydk`
    * `*.ptcgo`

* Available as a command-line application and a GUI (built using [Fyne](https://fyne.io/)).

* Ability to customize the back of the cards.

* No external tool required. You just need to run the provided executable.

* MTG

    * Support for transform and meld cards. Implemented using [states](https://berserk-games.com/knowledgebase/creating-states/) (press 1 or 2 to switch between states).

    * Sideboard and Maybeboard support.

    * Oversized card support (they'll appear twice as big as standard cards).

* Template mode

    By default, each card will have it's own image, retrieved from [Scryfall](https://scryfall.com/), [YGOPRODeck](https://db.ygoprodeck.com/) or <https://pokemontcg.io/>. \
    It's also possible to create a [card sheet template](https://kb.tabletopsimulator.com/custom-content/custom-deck/) (like what [decker](https://github.com/Splizard/decker) is doing). You'll have to upload the template to an image hosting site and update the `FaceURL` values in the deck's JSON file to the URL of the uploaded template.

## Download

The latest version is available [here](https://github.com/jeandeaual/tts-deckconverter/actions?query=workflow%3Abuild).

Click on the topmost job, then download the appropriate package for your machine from the artifact list.

## Building

[Go](https://golang.org/doc/install) 1.13 or newer is required.

### Command-line tool

```sh
$ go build ./cmd/tts-deckconverter
```

This will generate an executable called `tts-deckconverter`.

### GUI

Install the dependencies required by [Fyne](https://fyne.io/), listed [here](https://fyne.io/develop/index#prerequisites).

```sh
$ go build ./cmd/tts-deckconverter-gui
```

This will generate an executable called `tts-deckconverter-gui`.

## Usage

```
$ ./tts-deckconverter -h

Usage: tts-deckconverter TARGET

Flags:
  -back string
    	card back (cannot be used with "-backURL"):
  -backURL string
    	custom URL for the card backs (cannot be used with "-back")
  -chest string
    	save to the Tabletop Simulator chest folder (use "/" for the root folder) (cannot be used with "-output")
  -compact
    	don't indent the resulting JSON file
  -debug
    	enable debug logging
  -mode string
    	available modes: mtg, pkm, ygo
  -option value
    	plugin specific option (can have multiple)
    	mtg:
    		quality (enum): image quality (default: large)
    		rulings (bool): add the rulings to each card description (default: false)
    	pkm:
    		quality (enum): image quality (default: hires)
    	ygo: no option available
  -output string
    	destination folder (defaults to the current folder) (cannot be used with "-chest")
  -template
    	download each images and create a deck template instead of referring to each image individually
  -version
    	display the version information
```

### Samples usages

* Generate `Angelic Arrmy.json` under the TTS Saved Objects folder (`%USERPROFILE%/Documents/My Games/Tabletop Simulator/Saves/Saved Objects` on Windows):

    ```sh
    tts-deckconverter -chest / https://www.mtggoldfish.com/deck/2062036#paper
    ```

* Generate `Test Deck.json` under the `decks` folder:

    ```sh
    $ tts-deckconverter -mode mtg -output decks "Test Deck.txt"
    ```

* Generate `Starter Deck: Codebreaker.json` under the `YGO/Starter` folder in the TTS Saved Objects:

    ```sh
    $ tts-deckconverter -chest /YGO/Starter "Starter Deck: Codebreaker.ydk"
    ```

## Aknowledgements

Icon and card backs created using the [YGO Card Template](https://www.deviantart.com/holycrapwhitedragon/art/Yu-Gi-Oh-Back-Card-Template-695173962) (© 2017 - 2020 [HolyCrapWhiteDragon](https://www.deviantart.com/holycrapwhitedragon)).