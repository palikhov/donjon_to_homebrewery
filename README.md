[![Python 3.8](https://img.shields.io/badge/python-3.8-blue.svg)](https://www.python.org/downloads/release/python-360/)
[![Homebrewery v3](https://img.shields.io/badge/homebrewery-v3-blue.svg)](https://homebrewery.naturalcrit.com/)
[![Tests](https://github.com/telboy007/donjon_to_homebrewery/actions/workflows/build.yml/badge.svg)](https://github.com/telboy007/donjon_to_homebrewery/actions/workflows/build.yml)

# donjon_to_homebrewery
Converts [donjon](https://donjon.bin.sh) random dungeons into nice homebrewery v3 formatted text to copy and paste.  It will add page markers to break up room locations, but some minor edits may still be required to the final document.

This tool has been tested with:
1. AD&D
1. D&D 4e
1. D&D 5e

NOTE: don't forget to grab both maps (gm and player) from donjon as well as the json! :)

## Features
* Uses AI to enhance the dungeon flavour text and suggest a boss and lair details
* Adds any monster stat blocks that exist in the SRD to the document and lists the ones it had to skip
* Collects all the monsters and magical items into easy to use reference tables with sourcebook page number
* Provides total XP and a breakdown of combat encounter difficulty types
* Tries to add page breaks to reduce amount of manual editing needed
* Captures all the settings used to generate this dungeon on donjon.bin.sh for prosperity
* Ability to customise certain parts of room locations so important details aren't missed

## Using GitHub Actions

NOTE: filename, gm map and player map are all required fields when using the github action.

1. Via the Actions tab click on `Generate Homebrewery Text`
1. Click `Run Workflow`
1. Enter google drive download link for donjon json file (required)**
1. Provide GM and Player map hosted URLs (required)*
1. Click `Run Workflow`
1. After it completes click on your job (it gets a green tick)
1. Scroll to the bottom to find the Hombrewery.txt file under `Aftifacts`

*if using imgur.com, you will probably need to put `.png` on the end of the url!

**IMPORTANT: Creating download link for google drive

1. Make the json file shareable with anyone with the link with viewer rights (make sure viewers can download files via settings)
1. Copy link which will look like: https://drive.google.com/file/d/111111AAAAAAAABBBBBBBBBBB/view?usp=sharing
1. 111111AAAAAAAABBBBBBBBBBB is the file ID (your file ID will be different)
1. Create this link: https://docs.google.com/uc?export=download&id=111111AAAAAAAABBBBBBBBBBB
1. Enter this URL in the github action workflow filename field

## Using locally

NOTE: You will need to provide your own ChatGPT API token for the AI enhancement to work, if you don't want to then use the `--testmode` CLI flag to disable it.  Add a `.env` file in your local copy of this repo and add your API token like this `CHATGPT_TOKEN="your-token-here"`.

To install:
1. Clone repo
1. cd into repo
1. `pip install pipenv`
1. `pipenv shell` (NOTE: you may need to install pyenv to install python 3.8)

To run:
1. Copy json from donjon into repo folder
1. Supplied help text explains arguments needed to run the command
```
positional arguments:
  filename

optional arguments:
  -h, --help            show this help message and exit
  -gm GM_MAP, --gm_map GM_MAP
                        URL for the GM map image
  -p PLAYER_MAP, --player_map PLAYER_MAP
                        URL for the Player map image
  -t, --testmode        Disable AI enhancements
```
1. If you have the GM and Player maps, host them on an image hosting site and add the urls as arguments
1. `python convert_donjon_to_homebrewery.py your_filename.json -gm https://imgur.something.png -p https://imgur.something.png`

You can now copy and paste the contents of homebrewery.txt into your [homebrewery](https://homebrewery.naturalcrit.com/) document.

## Examples

1. You can see an example based on the included example.json [here](https://homebrewery.naturalcrit.com/share/PHjB9LurqAWm), this document hasn't been changed in any way since being generated by `DtH` to give you an idea of edits you will need to make to the final homebrewery document.
1. An example of what it could look like after some editing and tidying up can be seen [here](https://homebrewery.naturalcrit.com/share/my8Mqp3hmad1).

## Customising room locations

You can change the formatting of traps, hidden treasure and treasure in room locations so that important information is highlighted and not missed.

In the repo you will find a folder called templates, pick one of the css files and copy the contents into the style tab on homebrewery.

Feel free to create your own, if you don't mind sharing you can add them via a pull request!

## Troubleshooting:
1. Make sure all the URLs are as stated above; google drive links have been changed into the download version, and any imgur urls have the `.png` added to the end
1. Raise an issue via Issues tab with as much detail as possible, also please provide the json / json file that is causing problems.
