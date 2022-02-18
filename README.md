# Telepathy

Welcome to Telepathy, an OSINT toolkit for scraping Telegram data to help investigate shady goings on.

## Installation

1. Install from source

```
git clone https://github.com/jordanwildon/Telepathy.git
cd Telepathy
pip install -r requirements.txt
```

2. Register for and obtain your Telegram API details from [my.telegram.org][1].

3. Navigate to the installation directory and run setup.py, this will walk you through the Telegram API login and prepare the toolkit with your details.

```
python3 setup.py
```

## Usage

Upon installation completion, you will be able to launch telepathy.py. On first use of any of the modules, Telepathy will ask you for an authorization code that will be sent to your Telegram account.

_telepathy.py_

A launcher to select which module you would like to use.

_archiver.py_

This module batch archives the entirety of the chats you specify in _to_archive.csv_ (this filename must be exactly correct and have only one column with "To" as the header). A chat name is everything after t.me/ in the chat's sharelink or the @name as seen in chats.

<img width="494" alt="chatname" src="https://user-images.githubusercontent.com/88871159/151660067-160848bc-7e4e-487c-94c5-4985fe639892.png">

Messages saved by archiver.py are archived in both .CSV and .JSON formats and media content (photos, videos and documents) is saved to the directory Telepathy is installed in. For the module to work, the chat has to either be public, or your Telegram account needs to be a member. The module can also be set to run on a cron job to regularly archive target chats. Please use responsibly.

The 1.1 version of the module includes the ability to toggle media archiving, printing messages to the terminal, and archiving messages only after a specific date. Telepathy now manages files in a more organized manner.

<img width="702" alt="Screenshot 2022-02-13 at 14 39 05" src="https://user-images.githubusercontent.com/88871159/153755736-e89deba0-34c8-4865-a9a3-cfa04489bc6b.png">

_members.py_

This module scrapes the memberlist of a group your Telegram account is a member of. This works best with aged accounts and once the Telegram client has 'seen' members before. The module will still operate without these conditions, but 'invisible' members might not be saved to the memberlist.

_forwards.py_

This module scrapes the names of chats that have had messages forwarded into your target groups and automatically save these in an edgelist named _edgelist.csv_. It can then scrape forwards from all the discovered channels for a larger network map, which is saved as _net.csv_. This second feature takes a long time to run, but is worthwhile for a broader analysis. This edglist can then be used with software such as Gephi to visualize the network you have discovered.

_userlookup.py_

This module gives the user the ability to input a Telegram user ID and lookup basic information about the associated account.

## Advanced tools
Telepathy installs with a user analysis tool that analyzes the post frequency of users based on archived chats. The tool works by gathering all CSV archives in the "./telepathy/advanced/analysis_dropbox" folder. Simply drop a selection of group archives into this folder and it will calculate the number of unique active posters and how often they have posted. If used in combination with specific date archiving, this can also work to calculate how many users were active within a certain timeframe——for example within the last week.

Usage: 
```
cd ./advanced/analysis_dropbox
python3 user_analysis.py > analysis.csv
```

nb. when a user joins a group, it is considered a post in the above analysis. This is a tiny bug with Telepathy and will eventually be fixed but has been currently left in as it's still considered a signal of activity.

## A note on how Telegram works

Telegram chats are organised into two [key types][2]: channels and megagroups/supergroups. Each module works slightly differently depending on the chat type. For example, subscribers of Channels can't be scraped with the _members.py_ module. Channels can have seemingly unlimited subscribers, megagroups can have up to 200,000 members.

## Upcoming changes
Telepathy is still in the development stage with this version serving as an early release. Some bugs may still be present and some features are yet to be added. In some environments (particularly Window), Telepathy struggles to effectively manage files and can sometimes produce errors. Fixes for these errors should come soon. 

Upcoming features include:
  - ~~Adding message views to the archiver module.~~
  - ~~Expanding the time specifications for the archive module to include be able to set a specific period (including end date).~~
  - Giving the archiver module the ability to archive comments on channel posts.
  - May integrate location analysis tools.

## Feedback

Please send feedback to @[jordanwildon][3] on Twitter

## Usage terms

You may use Telepathy however you like, but your usecase is your responsibility. Be safe and respectful.

## Credits

All tools created by Jordan Wildon (@[jordanwildon][3]) with some suggestions, improvements and bug-busting contributed by Alex Newhouse (@[AlexBNewhouse][4]).

Where possible, credit for the use of this tool in published research is desired, but not required.

[1]: <https://my.telegram.org/auth?to=apps> "Telegram API"
[2]: <https://core.telegram.org/api/channel> "Telegram chat types"
[3]: <https://www.twitter.com/jordanwildon> "@jordanwildon"
[4]: <https://www.twitter.com/AlexBNewhouse> "@AlexBNewhouse"
