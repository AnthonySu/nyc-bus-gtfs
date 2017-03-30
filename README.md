# NYC Bus GTFS downloader

This repo downloads NYC bus GTFS data and loads it into a MySQL database, tracking different versions of the data.

## Requirements
* MySQL
* bash command line environment


## Usage
```
make init DATABASE=name_of_your_database
```

The `name_of_your_database` defaults to `nycbus`.

Download the current GTFS dataset. This places the files in a folder named `gtfs/YYYYMMDD`. The assumption is that you may, in the future, download a newer version of the GTFS.
```
make gtfs
```

Load the downloaded GTFS into the MySQL database
```
make mysql DATABASE=name_of_your_database
```

If a day goes by, or you have older GTFS data to load, use the GTFSVERSION variable:
```
make mysql GTFSVERSION=20170319
```

## Schema

The database will contain tables for each entry file in the GTFS schema. One additional column appears on each, `feed_index`, which is an integer keyed to the `gtfs_feeds` table. The `gtfs_feeds` contains a record of the `feed_start_date`, `feed_end_date` and `feed_download_date`.
