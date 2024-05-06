Configuration files for use with [Kometa](https://kometa.wiki/) (formerly Plex Meta Manager) to organize and customize Plex collections and other metadata.

## To Run Kometa
1. Once logged into the Windows PC running Plex & Kometa, open Powershell (Windows menu > Powershell)
2. Enter the following command then press Enter to run it:
 
   `cd ~\Kometa; .\kometa-venv\Scripts\activate;`

## Examples of Commands
Once you've started Kometa, you can run it with various commands to process Plex updates.

### Run the entire configuration
This command will run Kometa without any specific instructions — load the entire config and process everything. (This is scheduled to happen every day automatically but can be done manually if desired.)

`python kometa.py -r`

### Only run specific libraries
This command will run all the operations for the library or libraries you specifically name (e.g. Movies or TV Shows only), rather than the *entire* Plex installation. You can provide a single library name or a list of pipe-separated names.

`python kometa.py --run-libraries "Movies"`

`python kometa.py --run-libraries "TV Shows"`

`python kometa.py --run-libraries "Movies|Movies (4K)"`


### Only run specific collections
This command will create and/or update only the collections you specifically list. It will still need to process the whole list of titles, in order to find matching movies.

`python kometa.py --run-collections "Collection Name"`

Replace `Collection Name` with a pipe-separated list of the actual collection names you want to process. This can be any manually-defined or automatically-generated collection.

`python kometa.py --run-collections "Alien"`

or

`python kometa.py --run-collections "Godzilla (Showa)|Godzilla (Heisei)|Godzilla (Millennium)"`

### Only run specific configuration files
There are multiple individual config files for each library:
1. `metadata.yml` to override specific attributes of individual items, like title, description, year, labels, etc
2. `franchises.yml` to automatically create collections based on data from TheMovieDB.org (TMDB)
3. `collections.yml` to create manually-defined collections
    - TMDB has specific rules about what constitutes a collection, which generally do not allow for thematic/universe collections (like "Marvel Cinematic Universe") or loosely-related items
    - "Dumb" collections will just group the assigned items together and typically hide them from being shown as individual movies in the main library
    - "Smart" collections are either *filters* (which automatically update any time a new item matches the conditions, like runtime or year) or *builders* (which use external data like Trakt and update only when Kometa runs)

These files are currently hosted in this GitHub repository but can be downloaded to the Kometa configs folder on the PC and run locally.

To run specific files:

`python kometa.py --run-files "metadata.yml"`

or

`python kometa.py --run-files "franchises.yml"`
