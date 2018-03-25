garmin-connect-export
=====================

Downloads gpx, tcx or original fit files from your Garmin Connect

Description
-----------
This script downloads gpx, tcx or original fit files from your personal Garmin Connect Account. All downloaded data will go into a directory called `YYYY-MM-DD_garmin_connect_export/` in the current working directory. Activity details like activity title or activity description will be persisted using the Activity ID in a separate JSON file called `activities.json`. This JSON can be used to parsing data into additional data sources.

If there is no GPS track data (e.g., due to an indoor treadmill workout), a data file is still saved. If the GPX format is used, activity title and description data are saved. If the original format is used, Garmin may not provide a file at all and an empty file will be created. For activities where a GPX file was uploaded, Garmin may not have a TCX file available for download, so an empty file will be created. Since GPX is the only format Garmin should have for every activity, it is the default and preferred download format.

Hint: If you have many activities, you may find that this script crashes with an "Operation timed out" message. Just run the script again and it will pick up where it left off.

Usage
-----
You will need a little experience running things from the command line to use this script. That said, here are the usage details from the `--help` flag:

```
usage:

    gcexport.py [-h] [--version] [--username [USERNAME]]
                [--password [PASSWORD]] [-c [COUNT]]
                [-f [{gpx,tcx,original}]] [-d [DIRECTORY]] [-u]

optional arguments:

    -h, --help
    
        show this help message and exit
    
    --version
    
        print version and exit
    
    --username [USERNAME]
    
        your Garmin Connect username
        otherwise, you will be prompted
    
    --password [PASSWORD]
    
        your Garmin Connect password
        otherwise, you will be prompted
    
    -c [COUNT], --count [COUNT]
    
        number of recent activities to download
        or 'all' for all
        default: 1
    
    -f [{gpx,tcx,original}], --format [{gpx,tcx,original}]
    
        export format; can be 'gpx', 'tcx', or 'original'
        default: 'gpx'
        
    -d [DIRECTORY], --directory [DIRECTORY]
    
        the directory to export to
        default: './YYYY-MM-DD_garmin_connect_export'
        
    -u, --unzip
    
        if downloading zip files (format: 'original')
        unzipping files and removing zip file
```

Examples
--------
`python gcexport.py --count all`
downloads all of your data to a dated directory.

`python gcexport.py -d ~/MyActivities -c 3 -f original -u --username mygarminusername --password mygarminpassword`
downloads your three most recent activities in the FIT file format (or whatever they were uploaded as) into the `~/MyActivities` directory (unless they already exist).

Security Dislaimer
Using the `--username` and `--password` flags are not recommended because your password will be stored in your command line history. Instead, omit them to be prompted (and note that nothing will be displayed when you type your password).

Python
------
Alternatively, you may run it with `./gcexport.py` if you set the file as executable (i.e., `chmod u+x gcexport.py`). This requires Python. Most Mac and Linux users should already have it. Also, as stated above and already mentioned, you some really basic command line experience might be helpful.

`python /mygarminconnectexportscriptfolder/gcexport.py -d /mygarminconnectexportsfolder -c "mynumberofexports" -f original -u --username "mygarminusername" --password "mygarminpassword"`
executes from command line, downloads the definied number of original FIT files to your destination folder

JSON Data
---------
If you want to see all of the raw data that Garmin Connect hands to this script, just print out the contents of the `json_results` variable. This should be most useful for parsing data into other data sources. But still, some information might be missing, such as "Favorite".  This is only available from the Garmin Connect web interface and not included in data given to this script.
Also, be careful with speed data as it is sometimes measured as a pace (minutes per mile) or as a speed (miles per hour).

Contributions
-------------
Contributions are welcome, particularly if this script stops working with Garmin Connect. You may consider opening a GitHub Issue first. New features, however simple, are encouraged.

Thank You
---------
Thanks for using this script and I hope you find it as useful as I do! :smile:

Golden Cheetah & Garmin Connect
-------------------------------
You are a runner, cyclist or triathlete? You love Golden Cheetah? You track your activities with Garmin devices? You want to download all of them from Garmin Connect? Okay, this got answered already within here.

But now, you want to archive, cloud-backup and import automatically into Golden Cheetah? There are tons of alternatives and workarounds. Here is mine.

[Download, archive, cloud-backup and auto-import your activities.](https://johannesheinrich.de/golden-cheetah-garmin-connect-script/)

DISCLAIMER
----------
No guarantee

This script does NOT guarantee to get all of your data or even download it correctly. Against my Garmin Connect account it works quite fine and smooth, but different Garmin Connect account settings or different data types could potentially cause any kind of problems. Also, important hint now (!), this is NOT an official feature of Garmin Connect, Garmin may very well make changes to their APIs that breaks this script (and they certainly did since this project got created for several times).

Garmin Connect API

This script is for personal use only. It simulates a standard user session (i.e., in the browser), logging in using cookies and an authorization ticket. This makes the script pretty brittle. If you're looking for a more reliable option, particularly if you wish to use this for some production service, Garmin does offer a paid API service.

Security Dislaimer

As already mentioned above, using the `--username` and `--password` flags are not recommended because your password will be stored in your command line history. Instead, omit them to be prompted (and note that nothing will be displayed when you type your password).

License
-------
[MIT](https://github.com/kjkjava/garmin-connect-export/blob/master/LICENSE) &copy; 2015 Kyle Krafka