# omnis-conference
A conference management application centered around the needs of the annual Euromnis conference. 

# Dependencies

[Omnis Studio 8.1](https://www.omnis.net) or later

ArtsMan's [TMobjs](http://www2.artsman.com/omnis/Software/TMObjs257.zip) xcomp

The [omnis-infra](https://github.com/PISL/omnis-infra) library.

A PostgreSQL installation with two databases named conference and stb.  The first holds the data for the conference application and can be created from the included [conference.sql](db/conference.sql) file which contains data from the EurOmnis management database but with personal information obfuscated. This script also includes creation statements for the minimum required postgres roles, _developer, regular and console.

The second database, stb, holds the Omnis string table entries for the application and can be created from the SQL script included with the [omnis-stbeditor](https://github.com/PISL/omnis-stbeditor) repository.

NB.  The above databases come from a PostgreSQL 11 instance.

# Installation

Clone the [omnis-infra](https://github.com/PISL/omnis-infra) repository.

Clone this repository.

Copy the infra and conference libraries to your desired location (or [import from JSON](src)).

Copy the [CONFERENCE.libini](lib/CONFERENCE.libini) file to the same location as the CONFERENCE library.

Create the conference database from the [SQL script](db/conference.sql).

`psql -h dbServer -p port -d dbToConnectTo -U userName -a -f /path/to/conference.sql`

Create the stb database from its [SQL script](https://github.com/PISL/omnis-stbeditor/blob/master/db/stb.sql).

`psql -h dbServer -p port -d dbToConnectTo -U userName -a -f /path/to/stb.sql` 

The SQLite [initialisation database](lib/CONFERENCE.libini) is set up to expect the application databases to be running on localhost port 5432.  If this differs from your installation, you will need to open the file with an SQLite DB tool or an Omnis SQL Browser session and edit the appropriate rows:

```
update inidb set db_value = 'YourPgServer' where db_key = 'Host';
update inidb set db_value = portnumber where db_key = 'port'
```

## Usage

Open infra.lbs

If you have installed the stb database, open infra.tkSuper and set a Postgres user name and password for the local variables lcUserName and lcPassword in the $buildStringTable method.

Open CONFERENCE.lbs

## Acknowledgements

With thanks to [Arts Management Systems Ltd](https://www.artsman.com) for the TMobjs external component and for their charting tool, [Marquee](https://github.com/artsman/MarqueeCharts), used in the Dashboard.

## Contributing

We would welcome contributions to the application.  Please fork the repository and submit pull requests in the usual manner.