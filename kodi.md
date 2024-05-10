# Kodi

## Show UTF-8 characters in UI

In the 'Interface' settings, change the fonts for the skin from 'Default' to
'Arial based.'

## Databases

### Addons

The Addons#.db database contains the information on all Kodi addons such as
skins, scraper, video-addons etc.

`addonlinkrepo`

Links the Add-on to the Repository:

| Column Name | Data Type | Description                 |
| ----------- | --------- | --------------------------- |
| idRepo      | integer   | Foreign key to repo table   |
| idAddon     | integer   | Foreign key to addons table |

`addons`

Details relating to the add-on:

| Column Name | Data Type | Description                    |
| ----------- | --------- | ------------------------------ |
| id          | integer   | Primary Key                    |
| metadata    | blob      |                                |
| addonID     | text      | ID of the Add-on               |
| version     | text      | Add-on version                 |
| name        | text      | Add-on friendly name           |
| summary     | text      | Short friendly description     |
| new         | s text    | Notes                          |
| description | text      | Extended description of add-on |

`installed`

Add-ons that have been installed, showing status and usage details:

| Column Name    | Data Type | Description                                                 |
| -------------- | --------- | ----------------------------------------------------------- |
| id             | integer   | Primary Key                                                 |
| addonID        | text      | Foreign key to addons table                                 |
| enabled        | boolean   | 0/1 - No / Yes                                              |
| installDate    | text      | Date add-on was installed                                   |
| lastUpdated    | text      | Date add-on was last updated                                |
| lastUsed       | text      | Date add-o was last used                                    |
| origin         | text      | Originating Repository\*                                    |
| disabledReason | Integer   | NONE = 0, USER = 1, INCOMPATIBLE = 2, PERMANENT_FAILURE = 3 |

- \* A hash (if it's b6a50484-93a0-4afb-a01c-8d17e059feda) means ORIGIN_SYSTEM
  blank means MANUAL (or from ZIP) install anything else is installed from a
  REPOSITORY.

`package`

Details of downloaded zip files for installation. Can be used to roll-back to
previous versions. Does not include add-ons installed using 'Install via zip
file' method.

| Column Name | Data Type | Description                      |
| ----------- | --------- | -------------------------------- |
| id          | integer   | Primary Key                      |
| addonID     | text      | Foreign key to addons table      |
| filename    | text      | Path and name of add-on zip file |
| hash        | text      | Hash security check of zip file  |

`repo`

Details related to the Repository

| Column Name | Data Type | Description                                  |
| ----------- | --------- | -------------------------------------------- |
| id          | integer   | Primary Key                                  |
| addonID     | text      | Foreign key to addons table                  |
| checksum    | text      | Hash of the repository                       |
| lastcheck   | text      | Last time Repository was checked for updates |
| version     | text      | Installed version of the repository          |
| nextcheck   | text      | Next scheduled check for updates             |

`update_rules`

How non-official repositories are updated

| Column Name | Data Type | Description                                                 |
| ----------- | --------- | ----------------------------------------------------------- |
| id          | integer   | Primary Key                                                 |
| addonID     | text      | Foreign key to addons table                                 |
| updateRule  | Integer   | Any = 0, User Disabled Auto Update = 1, Pin Old Version = 2 |

`version`

Database details

| Column Name    | Data Type | Description                                  |
| -------------- | --------- | -------------------------------------------- |
| idVersion      | integer   | Database version                             |
| iCompressCount | integer   | Number of times database has been compressed |

### EPG

The EPG#.db database file contains the listings for the Electronic Program Guide
for Live-TV

`epg`

Lists the channel names and source of the EPG information

| Column Name  | Data Type   | Description           |
| ------------ | ----------- | --------------------- |
| idEpg        | integer     | Primary Key           |
| sName        | varchar(64) | Channel Name          |
| sScraperName | varchar(32) | Source of Information |

`epgtags`

This table stores the downloaded EPG data

| Column Name         | Data Type    | Description                                       |
| ------------------- | ------------ | ------------------------------------------------- |
| idBroadcast         | integer      | Primary Key                                       |
| idBroadcastUid      | integer      |                                                   |
| idEpg               | integer      |                                                   |
| sTitle              | varchar(128) | Program Name                                      |
| sPlotOutline        | text         | Short program description                         |
| sPlot               | text         | Long program description                          |
| sOriginalTitle      | varchar(128) | Original program title                            |
| sCast               | varchar(255) | Cast in program                                   |
| sDirector           | varchar(255) | Director of program                               |
| sWriter             | varchar(255) | Writer of program                                 |
| iYear               | integer      | Release year of program                           |
| sIMDBNumber         | varchar(50)  | IMDB title ID                                     |
| sIconPath           | varchar(255) | Path to channel icon                              |
| iStartTime          | integer      | Program start time in seconds from 1 January 1970 |
| iEndTime            | integer      | Program end time in seconds from 1 January 1970   |
| iGenreType          | Integer      |                                                   |
| iGenreSubType       | integer      |                                                   |
| sGenre              | varchar(128) |                                                   |
| sFirstAired         | varchar(32)  | First time aired                                  |
| iParentalRating     | Integer      | Parental rating                                   |
| iStarRating         | Integer      | Star rating                                       |
| iSeriesId           | Integer      |                                                   |
| iEpisodeId          | Integer      |                                                   |
| iEpisodePart        | Integer      |                                                   |
| sEpisodeName        | varchar(128) |                                                   |
| iFlag               | s Integer    |                                                   |
| sSeriesLink         | varchar(255) |                                                   |
| sParentalRatingCode | varchar(64)  |                                                   |

`lastepgscan`

This table holds information detailing EPG updates

| Column Name | Data Type   | Description                                         |
| ----------- | ----------- | --------------------------------------------------- |
| idEpg       | integer     | Primary Key                                         |
| sLastScan   | varchar(20) | yyy-mm-dd hh:mm:ss of last EPG scan for new content |

`savedsearches`

This table holds information for saved PVR guide (EPG) searches, which is a new
feature added in v20. [1]

| Column Name              | Data Type    | Description |
| ------------------------ | ------------ | ----------- |
| idSearch                 | integer      | Primary Key |
| sTitle                   | varchar(255) |             |
| idLastExecutedDateTime   | varchar(20)  |             |
| sSearchTerm              | varchar(255) |             |
| bSearchInDescription     | bool         |             |
| iGenreType               | Integer      |             |
| sStartDateTime           | varchar(20)  |             |
| sEndDateTime             | varchar(20)  |             |
| bIsCasaeSensitive        | bool         |             |
| iMinimumDuration         | integer      |             |
| iMaximumDuration         | integer      |             |
| bIsRadio                 | bool         |             |
| iClientId                | integer      |             |
| iChallenUid              | integer      |             |
| bIncludeUnknownGenre     | s bool       |             |
| bRemoveDuplicate         | s bool       |             |
| bIgnoreFinishedBroadcast | s bool       |             |
| bIgnoreFutureBroadcast   | s bool       |             |
| bFreeToAirOnly           | bool         |             |
| bIgnorePresentTimer      | s bool       |             |
| bIgnorePresentRecording  | s bool       |             |
| iChannelGroup            | Integer      |             |

`version`

Database details

| Column Name    | Data Type | Description                                  |
| -------------- | --------- | -------------------------------------------- |
| idVersion      | integer   | Database version                             |
| iCompressCount | integer   | Number of times database has been compressed |

### MyMusic

This database contains all information concerning music files that has been
added to the Music Library. It is used in the Music portion of Kodi.

Views

Views are standard queries, often long or complicated queries saved in the
database for convenience. The views below allow you to easily access all the
information about songs and albums in the Music Library, across all the linking
tables.

`albumartistview`

This table combines album with each album artist.

| Column Name            | Data Type    | Description                          |
| ---------------------- | ------------ | ------------------------------------ |
| idAlbum                | integer      | ID from album table                  |
| idArtist               | integer      | ID from artist table                 |
| idRole                 | integer      | 0 (fake role ID field)               |
| strRole                | text         | "AlbumArtist" (fake role desc field) |
| strArtist              | varchar(256) | Artist name                          |
| strSortName            | text         | See: Sort Name                       |
| strMusicBrainzArtistID | text         | Musicbrainz artist ID                |
| iOrder                 | integer      | Order artist appears in credits      |

`albumview`

A view of the album table with some additional fields aggregated from the songs
of that album.

| Column Name           | Data Type    | Description                                                        |
| --------------------- | ------------ | ------------------------------------------------------------------ |
| idAlbum               | integer      | ID from Album Table                                                |
| strAlbum              | varchar(256) | Album Name                                                         |
| strMusicBrainzAlbumID | text         | MusicBrainz album ID                                               |
| strReleaseGroupMBID   | text         | The ID that groups variations of the same release                  |
| strArtist             | s text       | Album artist(s) description (not always a concatenation of names)  |
| strArtistSort         | text         | See: Sort Name                                                     |
| strGenre              | s text       | Album genres (denormalised concatenation of values in genre table) |
| strReleaseDate        | text         | Release date of album (re-releases)                                |
| strOrigReleaseDate    | text         | Original release date of album                                     |
| bBoxedSet             | integer      | 0 = Not part of a Box Set, 1 = Part of a Box Set                   |
| strMood               | s text       | Album moods                                                        |
| strStyle              | s text       | Album styles                                                       |
| strTheme              | s text       | Album themes                                                       |
| strReview             | text         | Album review                                                       |
| strLabel              | text         | Album recording label                                              |
| strType               | text         | Album Type e.g. "Soundtrack / Live"                                |
| strReleaseStatu       | s text       | See: MusicBrainz Release Status                                    |
| strImage              | text         | URLs for available remote album images                             |
| fRating               | float        | Album rating                                                       |
| iUserrating           | integer      | Album user rating (out of 10)                                      |
| iVote                 | s integer    | Votes (for album rating)                                           |
| bCompilation          | integer      | Compilation flag                                                   |
| bScrapedMBID          | integer      | Indicates if mbid(s) have been fetched by scraping or from tags    |
| lastScraped           | varchar(20)  | Date & time of last scrape                                         |
| dateAdded             | text         | Music file timestamp of newest song on album                       |
| dateNew               | text         | Music file timestamp of newest song on album                       |
| dateModified          | text         | Music file timestamp of newest song on album                       |
| iTimesPlayed          | integer      | Average of number of times songs on album are played               |
| strReleaseType        | text         | Internal type - "album" or "single"                                |
| iDiscTotal            | integer      | Number of discs in the Release                                     |
| lastPlayed            | text         | Last date any song on album was played                             |
| iAlbumDuration        | integer      | Duration of all songs from that album currently in the library     |

`artistview`

A view of the artist table with an additional field aggregated from the songs by
that artist.

| Column Name            | Data Type    | Description                                                     |
| ---------------------- | ------------ | --------------------------------------------------------------- |
| idArtist               | integer      | ID from artist table                                            |
| strArtist              | varchar(256) | Artist name                                                     |
| strSortName            | text         | See: Sort Name                                                  |
| strMusicBrainzArtistID | text         | Musicbrainz artist ID                                           |
| strType                | text         | Type of performer                                               |
| strGender              | text         | Male or Female artist                                           |
| strDisambiguation      | text         | See: Disambiguation Comment                                     |
| strBorn                | text         | Artist birthday (and place)                                     |
| strFormed              | text         | Band formation information                                      |
| strGenre               | s text       | Artist genres (just text, no link to genre table)               |
| strMood                | s text       | Artist moods                                                    |
| strStyle               | s text       | Artist styles                                                   |
| strInstrument          | s text       | Artist instruments                                              |
| strBiography           | text         | Artist biography                                                |
| strDied                | text         | Date artist died (and place)                                    |
| strDisbanded           | text         | Band disbanded information                                      |
| strYearsActive         | text         | Years artist is active                                          |
| strImage               | text         | URLs of available artist images                                 |
| bScrapedMBID           | integer      | Indicates if mbid(s) have been fetched by scraping or from tags |
| lastScraped            | varchar(20)  | Date & time of last scrape                                      |
| dateAdded              | text         | Music file timestamp of newest song by artist                   |
| dateNew                | text         | Music file timestamp of newest song on album                    |
| dateModified           | text         | Music file timestamp of newest song on album                    |

`songartistview`

A view that joins song to artist and artist role.

| Column Name            | Data Type    | Description                          |
| ---------------------- | ------------ | ------------------------------------ |
| idSong                 | integer      | ID from song table                   |
| idArtist               | integer      | ID from artist table                 |
| idRole                 | integer      | ID from role table                   |
| strRole                | text         | Description of role                  |
| strArtist              | varchar(256) | Artist name                          |
| strSortName            | text         | See: Sort Name                       |
| strMusicBrainzArtistID | text         | Musicbrainz artist ID Hash           |
| iOrder                 | integer      | Order artist appears in song credits |

`songview`

A view that joins song to album and path.

| Column Name           | Data Type    | Description                                                                |
| --------------------- | ------------ | -------------------------------------------------------------------------- |
| idSong                | integer      | ID from song table                                                         |
| strArtist             | s text       | Song artist(s) description (not always a concatenation of names)           |
| strArtistSort         | text         | See: Sort Name                                                             |
| strGenre              | s text       | Song Genres (denormalised concatenation of values in genre table)          |
| strTitle              | varchar(512) | Song title                                                                 |
| iTrack                | integer      | Song track number                                                          |
| iDuration             | integer      | Song duration in seconds                                                   |
| strReleaseDate        | text         | Release date of album (re-releases)                                        |
| strOrigReleaseDate    | text         | Original release date of album                                             |
| strDiscSubtitle       | text         | Name of disc used in box sets                                              |
| strFileName           | text         | Name of music file                                                         |
| strMusicBrainzTrackID | text         | Musicbrainz track ID                                                       |
| iTimesPlayed          | integer      | Play count                                                                 |
| iStartOffset          | integer      | Start position (in seconds) when song from cuesheet                        |
| iEndOffset            | integer      | End position (in seconds) when song from cuesheet                          |
| lastplayed            | varchar(20)  | Date & time last played                                                    |
| rating                | float        | Song rating                                                                |
| userrating            | integer      | Song rated by user (out of 10)                                             |
| vote                  | s integer    | Votes for song rating                                                      |
| comment               | text         | Song description or comment                                                |
| idAlbum               | integer      | ID from album table                                                        |
| strAlbum              | varchar(256) | Album title                                                                |
| strPath               | varchar(512) | Full path for music file                                                   |
| strReleaseStatu       | s text       | See: MusicBrainz Release Status                                            |
| bCompilation          | integer      | Compilation flag (song is on a compilation album)                          |
| bBoxedSet             | integer      | 0 = Not part of a Box Set, 1 = Part of a Box Set                           |
| strAlbumArtist        | s text       | Album artist(s) description (not always a concatenation of names)          |
| strAlbumArtistSort    | text         | See: Sort Name                                                             |
| strAlbumReleaseType   | text         | Internal type - "album" or "single"                                        |
| mood                  | text         | Song mood                                                                  |
| strReplayGain         | text         | Contains album gain, album peak, track gain, track peak data in one string |
| iBPM                  | Integer      | Beats per Minute of song.                                                  |
| iBitRate              | integer      | Bit rate of recording                                                      |
| iSampleRate           | integer      | Sample rate of recording                                                   |
| iChannel              | s integer    | Number of audio channels in the recording                                  |
| iAlbumDuration        | integer      | Duration of all songs from that album currently in the library             |
| iDiscTotal            | integer      | Total No of discs in the box set                                           |
| dateAdded             | text         | Music file timestamp                                                       |
| dateNew               | text         | Music file timestamp of newest song on album                               |
| dateModified          | text         | Music file timestamp of newest song on album                               |

#### Tables

`album`

An album. This equates to what Musicbrainz call a "release" and represents the
unique release (i.e. issuing) of an item on a specific date with specific
release information such as the country, label, etc. Hence album title and
artist do not have to be unique as long as we have the release ID (Musicbrainz
album ID), Kodi can handle different versions of the same album e.g. original
release and then a later remaster (both same title and artist).

| Column Name                 | Data Type    | Description                                                                  | MusicFileTag \*\*                  | NFO (xml) Tag                                           |
| --------------------------- | ------------ | ---------------------------------------------------------------------------- | ---------------------------------- | ------------------------------------------------------- |
| idAlbum                     | integer      | ID from Album Table                                                          |                                    |
| strAlbum                    | varchar(256) | Album Name                                                                   | ALBUM                              | <title></title>                                         |
| strMusicBrainzAlbumID       | text         | MusicBrainz album ID                                                         | MUSICBRAINZ_ALBUMID                | <musicBrainzAlbumID></musicBrainzAlbumID>               |
| strReleaseGroupMBID         | text         | The ID that groups variations of the same release                            | MusicBrainz Release Group Id       | <musicbrainzreleasegroupid></musicbrainzreleasegroupid> |
| strArtistDisp               | text         | Album artist(s) description (not always a concatenation of names)            | ALBUMARTIST,ALBUMARTIST            | S <artistdesc></artistdesc>                             |
| strArtistSort               | text         | See: Sort Name                                                               | ARTISTSORT                         |
| strGenre                    | s text       | Album genres (denormalised concatenation of values in genre table)           | GENRE                              | <genre></genre> ^^                                      |
| strReleaseDate              | text         | Release date of album (re-releases)                                          |                                    |
| strOrigReleaseDate          | text         | Original release date of album                                               |                                    |
| bBoxedSet                   | integer      | 0 = Not part of a Box Set, 1 = Part of a Box Set                             |                                    |
| bCompilation                | integer      | Compilation flag                                                             | COMPILATION                        | <compilation></compilation>                             |
| strMood                     | s text       | Album mood                                                                   | s <mood></mood> ^^                 |
| strStyle                    | s text       | Album style                                                                  | s <style></style> ^^               |
| strTheme                    | s text       | Album theme                                                                  | s <theme></theme> ^^               |
| strReview                   | text         | Album review                                                                 | <review></review>                  |
| strImage                    | text         | URLs for available remote album image                                        | s <thumb preview="path"></thumb>   |
| strLabel                    | text         | Album recording label                                                        | LABEL                              | <label></label>                                         |
| strType                     | text         | Album Type e.g. "Soundtrack / Live"                                          | RELEASETYPE                        | <type></type>                                           |
| strReleaseStatu             | s text       | See: MusicBrainz Release Statu                                               | s                                  |
| fRating                     | float        | Album rating                                                                 | <rating max="10"></rating>         |
| iVote                       | s integer    | Votes (for album rating)                                                     | <votes></votes>                    |
| iUserrating                 | integer      | Album user rating (out of 10)                                                | <userrating max="10"></userrating> |
| lastScraped                 | text         | Date/time data scraped from online sources or NFO file                       | s                                  |
| bScrapedMBID                | integer      | Indicates if mbid(s) have been fetched by scraping or from tag               | s                                  |
| strReleaseType              | text         | Internal type - "album" or "single"                                          | <releasetype></releasetype>        |
| iDiscTotal                  | integer      | Number of discs in the Release                                               |                                    |
| iAlbumDuration              | integer      | Duration of all songs from that album currently in the library               |                                    |
| idInfoSetting               | integer      | Indicates which scraper setting was used for that item. 0 = default scraper. |
| Linked to infosetting table |              |
| dateAdded                   | text         | Music file timestamp                                                         |                                    |
| dateNew                     | text         | Music file timestamp of newest song on album                                 |                                    |
| dateModified                | text         | Music file timestamp of newest song on album                                 |

| Notes |                                                                                                 |
| ----- | ----------------------------------------------------------------------------------------------- |
| \*\*  | MusicFileTag column shows related Vorbis/Flac tags. Click on column heading for other tag types |
| ^^    | Multiple entries of the XML tag are allowed                                                     |

`album_artist`

This table links albums to the Source folder

| Column Name | Data Type | Description                       |
| ----------- | --------- | --------------------------------- |
| idArtist    | integer   | Foreign key to artist table       |
| idAlbum     | integer   | Foreign key to album table        |
| iOrder      | integer   | Order of artist names for credits |
| strArtist   | text      | Artist name (denormalised)        |

`album_source`

This table links artists and albums

| Column Name | Data Type | Description                 |
| ----------- | --------- | --------------------------- |
| idSource    | integer   | Foreign key to source table |
| idAlbum     | integer   | Foreign key to album table  |

`art`

The current artwork for artists and albums

| Column Name | Data Type | Description                                                         | NFO (xml) Tag                                                                          |
| ----------- | --------- | ------------------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| art_id      | integer   | Primary Key                                                         |                                                                                        |
| media_id    | integer   | Foreign key to album or artist table                                |                                                                                        |
| media_type  | text      | Used in combination with media_id- "album" or "artist"              |                                                                                        |
| type        | text      | art type e.g. "thumb", "fanart" etc.                                | <fanart></fanart>OR<thumb></thumb>                                                     |
| url         | text      | URL of image (can be remote, local or music file with art embedded) | <thumb aspect="poster" preview=""></thumb>,<fanart><thumb preview=""></thumb></fanart> |

`artist`

An artist is generally a musician, group of musicians, or other music
professional (like a producer or engineer). E.g. Bob Dylan, Pink Floyd, London
Symphony Orchestra, Andrew Collins (producer).

| Column Name                 | Data Type    | Description                                                                  | MusicFileTag \*\*                             | NFO (xml) Tag                               |
| --------------------------- | ------------ | ---------------------------------------------------------------------------- | --------------------------------------------- | ------------------------------------------- |
| idArtist                    | integer      | ID from artist table                                                         |                                               |
| strArtist                   | varchar(256) | Artist name                                                                  | ARTIST, ARTISTS, ALBUMARTIST and ALBUMARTISTS | <name></name>                               |
| strMusicBrainzArtistID      | text         | Musicbrainz artist ID                                                        | MUSICBRAINZ_ARTISTID                          | <musicBrainzArtistID></musicBrainzArtistID> |
| strSortName                 | text         | See: Sort Name                                                               | ALBUMARTISTSORT                               |
| strType                     | text         | Type of performer                                                            | <type></type>                                 |
| strGender                   | text         | Male or Female artist                                                        | <gender></gender>                             |
| strDisambiguation           | text         | See: Disambiguation Comment                                                  | <disambiguation></disambiguation>             |
| strBorn                     | text         | Artist birthday (and place)                                                  | <born></born>                                 |
| strFormed                   | text         | Band formation information                                                   | <formed></formed>                             |
| strGenre                    | s text       | Artist genres (just text, no link to genre table)                            | <genre></genre> ^^                            |
| strMood                     | s text       | Artist mood                                                                  | s <mood></mood> ^^                            |
| strStyle                    | s text       | Artist style                                                                 | s <style></style> ^^                          |
| strInstrument               | s text       | Artist instrument                                                            | s <instruments></instruments> ^^              |
| strBiography                | text         | Artist biography                                                             | <biography></biography>                       |
| strDied                     | text         | Date artist died (and place)                                                 | <died></died>                                 |
| strDisbanded                | text         | Band disbanded information                                                   | <disbanded></disbanded>                       |
| strYearsActive              | text         | Years artist is active                                                       | <yearsactive></yearsactive> ^^                |
| strImage                    | text         | URLs of available artist image                                               | s <thumb preview=" "></thumb> ^^              |
| lastScraped                 | varchar(20)  | Date last scraped metadata                                                   |                                               |
| bScrapedMBID                | integer      | Indicates if mbid(s) have been fetched by scraping or from tag               | s                                             |
| idInfoSetting               | integer      | Indicates which scraper setting was used for that item. 0 = default scraper. |
| Linked to infosetting table |              |
| dateAdded                   | text         | Music file timestamp                                                         |                                               |
| dateNew                     | text         | Music file timestamp of newest song on album                                 |                                               |
| dateModified                | text         | Music file timestamp of newest song on album                                 |

| Notes |                                                                                         |
| ----- | --------------------------------------------------------------------------------------- |
| \*\*  | MusicFileTag column shows Vorbis/Flac tags. Click on column heading for other tag types |
| ^^    | Multiple entries of the tag are allowed                                                 |

`audiobook`

For use with Audiobooks. Holds Resume Point information only.

| Column Name | Data Type    | Description                  |
| ----------- | ------------ | ---------------------------- |
| idBook      | integer      | Id of Resume Point           |
| strBook     | varchar(256) | Title link to album table    |
| strAuthor   | text         | Author link to artist table  |
| bookmark    | integer      | Resume Point (millisec)      |
| file        | text         | Path to audiobook            |
| dateAdded   | varchar(20)  | Date & Time bookmark created |

`audiobook`

For use with Audiobooks. Holds Resume Point information only.

| Column Name | Data Type    | Description                  |
| ----------- | ------------ | ---------------------------- |
| idBook      | integer      | Id of Resume Point           |
| strBook     | varchar(256) | Title link to album table    |
| strAuthor   | text         | Author link to artist table  |
| bookmark    | integer      | Resume Point (millisec)      |
| file        | text         | Path to audiobook            |
| dateAdded   | varchar(20)  | Date & Time bookmark created |

`discography`

The discography of an artist. This is returned when additional information for
an artist is scraped from online sources or NFO files. It has no relationship
with the albums actually in the user's music collection, it is just details
about the artist.

| Column Name         | Data Type | Description                                       | NFO (xml) Tag                  |
| ------------------- | --------- | ------------------------------------------------- | ------------------------------ |
| idArtist            | integer   | Foreign key to artist table                       |                                |
| strAlbum            | text      | Album title                                       | <album><title></title></album> |
| strYear             | text      | Year album released                               | <album><year></year></album>   |
| strReleaseGroupMBID | text      | The ID that groups variations of the same release |                                |

`genre`

A music genre. This is a lookup table that enumerates the song genre values read
from the genre tags embedded in music files e.g. "Progressive Rock", "Baroque"
etc. But could contain anything that has been given as a "genre", and is not
strictly limited to music genres.

| Column Name | Data Type    | Description | MusicFileTag \*\* | NFO (xml) Tag      |
| ----------- | ------------ | ----------- | ----------------- | ------------------ |
| idGenre     | integer      | Primary Key |                   |
| strGenre    | varchar(256) | Genre Name  | GENRE             | <genre></genre> ^^ |

| Notes |                                                                                         |
| ----- | --------------------------------------------------------------------------------------- |
| \*\*  | MusicFileTag column shows Vorbis/Flac tags. Click on column heading for other tag types |
| ^^    | Multiple entries of the tag are allowed                                                 |

`infosetting`

As scrapers and scraper settings can be changed per individual Album and Artist,
this table details the settings of additional scrapers used. If only the default
scraper for Album and Artist are used, there are no entries here.

| Column Name    | Data Type | Description      |
| -------------- | --------- | ---------------- |
| idSetting      | integer   | Primary Key      |
| strScraperPath | text      | Scraper details  |
| strSetting     | s text    | Scraper settings |

`path`

The path of a folder containing music that has been scanned into the music
library. This holds hash values of name, size, and timestamp for each folder and
sub folder that is used to determine if the contents have changed and therefore
the music files need rescanning as part of library update.

| Column Name | Data Type    | Description |
| ----------- | ------------ | ----------- |
| idPath      | integer      | Primary Key |
| strPath     | varchar(512) | Media path  |
| strHash     | text         | Hash value  |

`removed_link`

| Column Name | Data Type | Description |
| ----------- | --------- | ----------- |
| idArtist    | integer   |             |
| idMedia     | integer   |             |
| idRole      | integer   |             |

`role`

An artist role, a way that an artist has contributed to or been involved with a
song. This could be by being in the song artist credits ("artist"), as a
musician ("Guitar", "Orchestra" or "vocals" etc.), as composer, conductor,
lyricist etc. or involved in some other way as music professional e.g. producer,
engineer, mixer etc. This is a lookup table that enumerates the various roles
that have been read from tags embedded in music files.

| Column Name | Data Type | Description         | MusicFileTag \*\*                                                                                         |
| ----------- | --------- | ------------------- | --------------------------------------------------------------------------------------------------------- |
| idrole      | integer   | Primary Key         |                                                                                                           |
| strRole     | text      | Description of role | ARTIST, ARRANGER, COMPOSER, CONDUCTOR, DJMIXER, ENGINEER, LYRICIST, MIXER,PRODUCER, REMIXER and PERFORMER |

| Notes |                                                                                         |
| ----- | --------------------------------------------------------------------------------------- |
| \*\*  | MusicFileTag column shows Vorbis/Flac tags. Click on column heading for other tag types |

`song`

A song. It is the way that the individual track(s) from a music file are held in
the music library. Generally a music file contains just one song, however it may
contain more and have an associated cuesheet (separately or embedded) that
identifies the individual tracks. A song may be from an album (the release of
several tracks as one product so includes EPs etc. ), or a single. Singles from
an artist (no album title given in the embedded tags) are internally linked with
a fake album in the album table.

The music library can contain songs with the same title, artist credits, track
number and album as long as they come from separate music files. Unexpectedly
Musicbrainz Track ID is not unique on an album, recordings are sometimes
repeated e.g. "[silence]" or on a disc set.

| Column Name           | Data Type    | Description                                                                | MusicFileTag \*\*          | XML Tags                  |
| --------------------- | ------------ | -------------------------------------------------------------------------- | -------------------------- | ------------------------- |
| idSong                | integer      | ID from song table                                                         |                            |                           |
| idAlbum               | integer      | ID from album table                                                        |                            |                           |
| idPath                | integer      | Foreign key to path table                                                  |                            |                           |
| strArtistDisp         | text         | Album artist(s) description (not always a concatenation of names)          | ALBUMARTIST,ALBUMARTISTS   | <artistdesc></artistdesc> |
| strArtistSort         | text         | See: Sort Name                                                             | ALBUMARTISTSORT            |                           |
| strGenre              | s text       | Song Genres (denormalised concatenation of values in genre table)          | GENRE                      |                           |
| strTitle              | varchar(512) | Song title                                                                 | TITLE                      |                           |
| iTrack                | integer      | Song disc (upper 4 bytes) and track number (lower 4 bytes)                 | TRACKNUMBER and DISCNUMBER |                           |
| iDuration             | integer      | Song duration in second                                                    | s                          |                           |
| strReleaseDate        | text         | Release date of album (re-releases)                                        |                            |                           |
| strOrigReleaseDate    | text         | Original release date of album                                             |                            |                           |
| strDiscSubtitle       | text         | Name of disc used in box set                                               | s                          |                           |
| strFileName           | text         | Name of music file                                                         |                            |                           |
| strMusicBrainzTrackID | text         | Musicbrainz track ID                                                       | MUSICBRAINZ_TRACKID        |                           |
| iTimesPlayed          | integer      | Play count                                                                 |                            |                           |
| iStartOffset          | integer      | Start position (in seconds) when song from cuesheet                        |                            |                           |
| iEndOffset            | integer      | End position (in seconds) when song from cuesheet                          |                            |                           |
| lastplayed            | varchar(20)  | Date & time last played                                                    |                            |                           |
| rating                | float        | Song rating                                                                |                            |                           |
| vote                  | s integer    | Votes for song rating                                                      |                            |                           |
| userrating            | integer      | Song rated by user (out of 10)                                             | RATING                     |                           |
| comment               | text         | Song description or comment                                                | COMMENT                    |                           |
| mood                  | text         | Song mood                                                                  | MOOD                       |                           |
| iBPM                  | Integer      | Beats per Minute of song.                                                  |                            |                           |
| iBitRate              | integer      | Bit rate of recording                                                      |                            |                           |
| iSampleRate           | integer      | Sample rate of recording                                                   |                            |                           |
| iChannel              | s integer    | Number of audio channels in the recording                                  |                            |                           |
| strReplayGain         | text         | Contains album gain, album peak, track gain, track peak data in one string |                            |                           |
| dateAdded             | text         | Music file timestamp                                                       |                            |
| dateNew               | text         | Music file timestamp of newest song on album                               |                            |                           |
| dateModified          | text         | Music file timestamp of newest song on album                               |                            |                           |

| Notes |                                                                                         |
| ----- | --------------------------------------------------------------------------------------- |
| \*\*  | MusicFileTag column shows Vorbis/Flac tags. Click on column heading for other tag types |

`song_artist`

This table links songs to artists and the roles they contributed.

| Column Name | Data Type | Description                   |
| ----------- | --------- | ----------------------------- |
| idArtist    | integer   | Foreign key to artist table   |
| idSong      | integer   | Foreign key to song table     |
| idRole      | integer   | Foreign key to role table     |
| iOrder      | integer   | Order in artist credits       |
| strArtist   | text      | Name of artist (denormalised) |

`song_genre`

This table links the songs with their genres.

| Column Name | Data Type | Description                                     |
| ----------- | --------- | ----------------------------------------------- |
| idGenre     | integer   | Foreign key to genre table                      |
| idSong      | integer   | Foreign key to song table                       |
| iOrder      | integer   | Genre order when concatenating to single string |

`source`

List of Sources

| Column Name  | Data Type | Description                              |
| ------------ | --------- | ---------------------------------------- |
| idSource     | integer   | Primary Key                              |
| strName      | text      | Folder name                              |
| strMultipath | text      | Path or multipath:// of source folder(s) |

`source_path`

A source can be multi-path (made as a collection of separate folders). The
source_path table holds the separate paths per individual source

| Column Name | Data Type    | Description                                 |
| ----------- | ------------ | ------------------------------------------- |
| idSource    | integer      | Primary Key and Foreign key to source table |
| idPath      | integer      |
| strPath     | varchar(512) | Path to source folder                       |

`version`

Database version

| Column Name    | Data Type | Description                                  |
| -------------- | --------- | -------------------------------------------- |
| idVersion      | integer   | Version of the music database                |
| iCompressCount | integer   | Number of times database has been compressed |

`versiontagscan`

Used to hold minimal scanning process related data

| Column Name        | Data Type   | Description                                                                                                                                                               |
| ------------------ | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| idVersion          | integer     | Keeps track of what version of db tag processing was used to populate the db                                                                                              |
| iNeedsScan         | integer     | Is set per Kodi release to indicate the minimum db version needed before a forced rescan on tags is necessary. Used when newer versions have related tag scanning changes |
| lastscanned        | varchar(20) | Date & Time last scan was run. Useful because when rescanning the ids change and add-ons can check if their own data is still valid or a resync is required.              |
| lastcleaned        | varchar(20) |                                                                                                                                                                           |
| artistlinksupdated | varchar(20) |                                                                                                                                                                           |
| genresupdated      | varchar(20) |                                                                                                                                                                           |

### MyVideos

This database contains all information concerning TV shows, movies, and music
videos. It is used in the Videos portion of Kodi.

#### Views

Views are standard queries, often long or complicated queries saved in the
database for convenience. The views below allow you to easily access all the
information about each of the main media types in the Video Library, across all
the linking tables.

`episodeview`

A view that joins episode to file and tvshow (through tvshowlinkepisode) and
path.

| Column Name        | Data Type       | Description                           |
| ------------------ | --------------- | ------------------------------------- |
| idEpisode          | integer         | Primary Key                           |
| idFile             | integer         | Foreign key to the files table        |
| c00                | text            | Episode Title                         |
| c01                | text            | Plot Summary                          |
| c02                | text            | Not Used                              |
| c03                | text            | Link to Rating Table                  |
| c04                | text            | Writer                                |
| c05                | text            | First Aired                           |
| c06                | text            | Thumbnail URL                         |
| c07                | text            | Thumbnail URL Spoof                   |
| c08                | text            | Not Used                              |
| c09                | text            | Runtime                               |
| c10                | text            | Director                              |
| c11                | text            | Production Code                       |
| c12                | varchar(24)     | Season Number                         |
| c13                | tvarchar(24)ext | Episode Number                        |
| c14                | text            | Original Title                        |
| c15                | text            | Season formatted for sorting          |
| c16                | text            | Episode formatted for sorting         |
| c17                | varchar(24)     | Bookmark                              |
| c18                | text            | Path to episode file                  |
| c19                | text            | Link to Path Table                    |
| c20                | text            | Link to UniqueID Table                |
| c21                | text            | Not used                              |
| c22                | text            | Not used                              |
| c23                | text            | Not used                              |
| idShow             | integer         | Foreign key to the tvshow table       |
| userrating         | integer         | User Rating                           |
| idSeason           | integer         | Foreign key to the seasons table      |
| strFilename        | text            | Full name of file including extension |
| strPath            | text            | Path to playable file                 |
| playCount          | integer         | # of Times Played                     |
| lastPlayed         | text            | Date & Time Last Played               |
| dateAdded          | text            | Date & Time Added to Library          |
| strTitle           | text            | Name of program                       |
| genre              | text            | Genre                                 |
| studio             | text            | Studio                                |
| premiered          | text            | Premiered Date                        |
| mpaa               | text            | MPAA Rating                           |
| resumeTimeInSecond | s double        | Resume Point                          |
| totalTimeInSecond  | s double        | Length of video                       |
| playerState        | text            |                                       |
| rating             | float           | Rating                                |
| vote               | s integer       | Votes for rating                      |
| rating_type        | text            | Type of rating                        |
| uniqueid_value     | text            |                                       |
| uniqueid_type      | text            |                                       |

`movieview`

A view that joins movie to file and path.

| Column Name        | Data Type | Description                           |
| ------------------ | --------- | ------------------------------------- |
| idMovie            | integer   | Primary Key                           |
| idFile             | integer   | Foreign Key to files table            |
| c00                | text      | Local Movie Title                     |
| c01                | text      | Movie Plot                            |
| c02                | text      | Movie Plot Outline                    |
| c03                | text      | Movie Tagline                         |
| c04                | text      | Not Used                              |
| c05                | text      | Link to Rating Table                  |
| c06                | text      | Writers                               |
| c07                | text      | Not Used                              |
| c08                | text      | Image URL                             |
| c09                | text      | Link to uniqueid Table                |
| c10                | text      | Title formatted for sorting           |
| c11                | text      | Runtime                               |
| c12                | text      | MPAA Rating                           |
| c13                | text      | IMDB Top 250 Ranking                  |
| c14                | text      | Genre                                 |
| c15                | text      | Director                              |
| c16                | text      | Original Movie Title                  |
| c17                | text      | Thumb URL Spoof]                      |
| c18                | text      | Studio                                |
| c19                | text      | Trailer URL                           |
| c20                | text      | Fanart URLs                           |
| c21                | text      | Country                               |
| c22                | text      | Path to playable file                 |
| c23                | text      | Link to path table for Source folder  |
| idSet              | integer   | Foreign Key to sets table             |
| userrating         | integer   | Rating applied by user                |
| premiered          | text      | Date movie premiered                  |
| strSet             | text      | Movie Set                             |
| strSetOverview     | text      | Movie Set plot                        |
| strFilename        | text      | Full name of file including extension |
| strPath            | text      | Path to playable file                 |
| playCount          | integer   | # of Times Played                     |
| lastPlayed         | text      | Date & Time Last Played               |
| dateAdded          | text      | Date & Time Added to Library          |
| resumeTimeInSecond | s double  | Resume Point                          |
| totalTimeInSecond  | s double  | Length of video                       |
| playerState        | text      |                                       |
| rating             | float     | Rating                                |
| vote               | s integer | Votes for rating                      |
| rating_type        | text      | Type of rating                        |
| uniqueid_value     | text      |                                       |
| uniqueid_type      | text      |                                       |

`musicvideoview`

A view that joins musicvideo to file and path.

| Column Name        | Data Type | Description                           |
| ------------------ | --------- | ------------------------------------- |
| idMVideo           | integer   | Primary Key                           |
| idFile             | integer   | Foreign Key to files table            |
| c00                | text      | Title                                 |
| c01                | text      | Thumb URL                             |
| c02                | text      | Thumb URL spoof                       |
| c03                | text      | Not Used                              |
| c04                | text      | Run time                              |
| c05                | text      | Director                              |
| c06                | text      | Studios                               |
| c07                | text      | Not Used                              |
| c08                | text      | Plot                                  |
| c09                | text      | Album                                 |
| c10                | text      | Artist                                |
| c11                | text      | Genre                                 |
| c12                | text      | Track                                 |
| c13                | text      | Path to playable file                 |
| c14                | text      | Link to path table for Source folder  |
| c15                | text      | Not Used                              |
| c16                | text      | Not Used                              |
| c17                | text      | Not Used                              |
| c18                | text      | Not Used                              |
| c19                | text      | Not Used                              |
| c20                | text      | Not Used                              |
| c21                | text      | Not Used                              |
| c22                | text      | Not Used                              |
| c23                | text      | Not Used                              |
| userrating         | integer   | User Rating                           |
| premiered          | text      | Premier of Music Video                |
| strFileName        | text      | Full name of file including extension |
| strPath            | text      | Path URL                              |
| playCount          | integer   | # of Times Played                     |
| lastPlayed         | text      | Date & Time Last Played               |
| dateAdded          | text      | Date & Time Added to Library          |
| resumeTimeInSecond | s double  | Time in seconds of bookmark location  |
| totalTimeInSecond  | s double  | Time in seconds of the video          |
| playerState        | text      |                                       |

`season_view`

A view that joins seasons to the tvshow.

| Column Name | Data Type | Description                      |
| ----------- | --------- | -------------------------------- |
| idSeason    | integer   | Primary Key                      |
| idShow      | integer   | Foreign key to the tv show table |
| Season      | integer   | Season number                    |
| name        | text      | User modified Season name        |
| userrating  | integer   | User rating for season           |
| strPath     | text      | Path to tv show                  |
| showTitle   | text      | TV Show name                     |
| Plot        | text      | TV Show plot                     |
| premiered   | text      | TV Show premiered date           |
| genre       | text      | genre                            |
| studio      | text      | Studio                           |
| mpaa        | text      | Certification                    |
| episode     | s text    | Season episode count             |
| playCount   |           |
| aired       |           |

`tvshowview`

View that joins tvshow to path. Also produces information about total number of
episodes as well as number of watched and unwatched episodes.

| Column Name    | Data Type | Description                               |
| -------------- | --------- | ----------------------------------------- |
| idShow         | integer   | Primary Key                               |
| c00            | text      | Show Title                                |
| c01            | text      | Show Plot Summary                         |
| c02            | text      | Status                                    |
| c03            | text      | Votes                                     |
| c04            | text      | Rating                                    |
| c05            | text      | First Aired                               |
| c06            | text      | Thumbnail URL                             |
| c07            | text      | [unknown - Spoof Thumbnail URL?]          |
| c08            | text      | Genre                                     |
| c09            | text      | Original Title                            |
| c10            | text      | Episode Guide URL                         |
| c11            | text      | Fan Art URL                               |
| c12            | text      | SeriesId (when using thetvdb.com scraper) |
| c13            | text      | Content Rating                            |
| c14            | text      | Network                                   |
| c15            | text      | Title formatted for sorting               |
| c16            | text      | Trailer                                   |
| c17            | text      | Not Used                                  |
| c18            | text      | Not Used                                  |
| c19            | text      | Not Used                                  |
| c20            | text      | [unknown]                                 |
| c21            | text      | [unknown]                                 |
| c22            | text      | [unknown]                                 |
| c23            | text      | [unknown]                                 |
| userrating     | integer   | User Rating                               |
| duration       | integer   | Total duration                            |
| idParentPath   | integer   |                                           |
| strPath        | text      | Path URL                                  |
| dateAdded      | text      | Date & Time Added to Library              |
| lastPlayed     | text      | Date & Time Last Played                   |
| totalCount     | integer   | # of Episodes                             |
| watchedcount   | integer   | # of Times Played                         |
| totalSeason    | s integer | # of Seasons                              |
| rating         | float     | Rating                                    |
| vote           | s integer | Votes for rating                          |
| rating_type    | text      | Type of rating                            |
| uniqueid_value | text      |                                           |
| uniqueid_type  | text      |                                           |

`tvshowcounts`

This table stores the TV Show watched count, total seasons, last played and date
added data

| Column Name  | Data Type | Description             |
| ------------ | --------- | ----------------------- |
| idShow       | integer   | Primary Key             |
| lastPlayed   | text      | Date & Time Last Played |
| totalCount   | integer   | # of Episodes           |
| watchedcount | integer   | # of Times Played       |
| totalSeason  | s integer | # of Seasons            |
| dateAdded    | text      | Date Added              |

`tvshowlinkpath_minview`

Joins TV Show to Path

| Column Name | Data Type | Description               |
| ----------- | --------- | ------------------------- |
| idShow      | integer   | Primary Key               |
| idPath      |           | Foreign key to path table |

Tables

The information in the Video Library is organized into the following tables.
Several large tables (such as episode, movie, settings, and tvshow) contain the
bulk of the information, while most of the others are used to link a long string
to a common ID key.

`actor`

This table stores actor, artist, director, and writer information.

| Column Name | Data Type | Description                                    |
| ----------- | --------- | ---------------------------------------------- |
| actor_id    | integer   | Primary Key                                    |
| name        | integer   | Name of the actor, artist, director, or writer |
| art_url     | s text    | Image URL                                      |

`actor_link`

This table links actors to Movies, TV Shows, Episodes, Music Videos and stores
role information.

| Column Name | Data Type | Description                                                                |
| ----------- | --------- | -------------------------------------------------------------------------- |
| actor_id    | integer   | Foreign key to actors table                                                |
| media_id    | integer   | Foreign key to episode table, tv show table, movie table,music video table |
| media_type  | text      | Movie, TV Show, Episode, Music Video                                       |
| role        | text      | Role the actor played                                                      |
| cast_order  | integer   | Order actors will be displayed                                             |

`art`

This table stores URLs for video art metadata.

| Column Name | Data Type | Description                                                                                             |
| ----------- | --------- | ------------------------------------------------------------------------------------------------------- |
| art_id      | integer   | Primary Key                                                                                             |
| media_id    | integer   | The id of the media this piece of art is for                                                            |
| media_type  | text      | The type of media this art applies to - movie, set, tvshow, season, episode, musicvideo or actor        |
| type        | text      | The image type - poster, fanart, thumb, banner, landscape, clearlogo, clearart, characterart or discart |
| url         | text      | Image URL                                                                                               |

`bookmark`

This table stores bookmarks, which are timestamps representing the point in a
video where a user stopped playback, an explicit bookmark requested by the user,
or an automatically generated episode bookmark.

| Column Name       | Data Type | Description                                        |
| ----------------- | --------- | -------------------------------------------------- |
| idBookmark        | integer   | Primary Key                                        |
| idFile            | integer   | Foreign key to files table                         |
| timeInSecond      | s double  | Time in seconds of bookmark location               |
| totalTimeInSecond | s double  | Time in seconds of the video                       |
| thumbNailImage    | text      | Thumbnail for bookmark                             |
| player            | text      | Player used to store bookmark                      |
| playerState       | text      | Player's internal state in XML                     |
| type              | integer   | Type of bookmark (0=standard, 1=resume, 2=episode) |

`country`

This table lists countries.

| Column Name | Data Type | Description  |
| ----------- | --------- | ------------ |
| country_id  | integer   | Primary Key  |
| name        | text      | Country Name |

`country link`

This table links countries to movies.

| Column Name | Data Type | Description                  |
| ----------- | --------- | ---------------------------- |
| country_id  | integer   | Foreign key to country table |
| media_id    | integer   | Foreign key to movie table   |
| media_type  | text      | Media Class                  |

`director_link`

This table links directors to Movies, TV show episodes and Music Videos

| Column Name | Data Type | Description                                                 |
| ----------- | --------- | ----------------------------------------------------------- |
| actor_id    | integer   | Foreign key to actors table                                 |
| media_id    | integer   | Foreign key to episode table, movie table,music video table |
| media_type  | text      | Movie, Music Video, Episode                                 |

`episode`

This table stores television episode information. Information concerning the
series is stored in tvshow. To link an episode to its parent series, use
tvshowlinkepisode.

| Column Name | Data Type   | Description                      | TV Episode                        |
| ----------- | ----------- | -------------------------------- | --------------------------------- |
| idEpisode   | integer     | Primary Key                      |                                   |
| idFile      | integer     | Foreign key to the files table   |                                   |
| c00         | text        | Episode Title                    | <title></title>                   |
| c01         | text        | Plot Summary                     | <plot></plot>                     |
| c02         | text        | Not Used                         |                                   |
| c03         | text        | Link to Rating Table             |                                   |
| c04         | text        | Writer                           | <credits></credits>               |
| c05         | text        | First Aired                      | <premiered></premiered>           |
| c06         | text        | Thumbnail URL                    | <thumb></thumb>                   |
| c07         | text        | Thumbnail URL Spoof              |                                   |
| c08         | text        | Not Used                         |                                   |
| c09         | text        | Runtime                          | <runtime></runtime>               |
| c10         | text        | Director                         | <director></director>             |
| c11         | text        | Production Code                  |                                   |
| c12         | varchar(24) | Season Number                    | <season></season>                 |
| c13         | varchar(24) | Episode Number                   | <episode></episode>               |
| c14         | text        | Original Title                   | <originaltitle></originaltitle>   |
| c15         | text        | Season Number- Specials Sorting  | <displayseason></displayseason>   |
| c16         | text        | Episode Number- Specials Sorting | <displayepisode></displayepisode> |
| c17         | varchar(24) | Bookmark                         |                                   |
| c18         | text        | Path to episode file             |                                   |
| c19         | text        | Link to Path Table               |                                   |
| c20         | text        | Link to UniqueID Table           |                                   |
| c21         | text        | Not used                         |                                   |
| c22         | text        | Not used                         |                                   |
| c23         | text        | Not used                         |                                   |
| idShow      | integer     | Foreign key to the tvshow table  |                                   |
| userrating  | integer     | User Rating                      | <userrating></userrating>         |
| idSeason    | integer     | Foreign key to the seasons table |                                   |

`files`

This table stores filenames and links the path.

| Column Name | Data Type | Description                           | Movies, TV Shows, TV Episodes, Music Videos |
| ----------- | --------- | ------------------------------------- | ------------------------------------------- |
| idFile      | integer   | Primary Key                           |                                             |
| idPath      | integer   | Foreign key to path table             |                                             |
| strFilename | text      | Full name of file including extension |                                             |
| playCount   | integer   | # of Times Played                     | <playcount></playcount>                     |
| lastPlayed  | text      | Date & Time Last Played               | <lastplayed></lastplayed>                   |
| dateAdded   | text      | Date & Time Added to Library          | <dateadded></dateadded>                     |

`genre`

This table stores genre information. For convenience the contents are duplicated
in movie and tvshow, so a join isn't necessary.

| Column Name | Data Type | Description | Movies, TV Shows, TV Episodes, Music Videos |
| ----------- | --------- | ----------- | ------------------------------------------- |
| genre_id    | integer   | Primary Key |                                             |
| name        | text      | Genre label | <genre></genre>                             |

`genre_link`

This table links genres to movies. (The contents are also stored in movies.c14,
though.)

| Column Name | Data Type | Description                                                  |
| ----------- | --------- | ------------------------------------------------------------ |
| genre_id    | integer   | Foreign key to genre table                                   |
| media_id    | integer   | Foreign key to movie table, tv show table, music video table |
| media_type  | text      | Movie, Music Video, TV Show                                  |

`movie`

This table stores movie information.

| Column Name | Data Type | Description                          | Movies                                        |
| ----------- | --------- | ------------------------------------ | --------------------------------------------- |
| idMovie     | integer   | Primary Key                          |                                               |
| idFile      | integer   | Foreign Key to files table           |                                               |
| c00         | text      | Local Movie Title                    | <title></title>                               |
| c01         | text      | Movie Plot                           | <plot></plot>                                 |
| c02         | text      | Movie Plot Outline                   | <outline></outline>                           |
| c03         | text      | Movie Tagline                        | <tagline></tagline>                           |
| c04         | text      | Not Used                             |                                               |
| c05         | text      | Link to Rating Table                 |                                               |
| c06         | text      | Writer                               | s <credits></credits>                         |
| c07         | text      | Not Used                             |                                               |
| c08         | text      | Image URL                            | <thumb aspect="poster" preview=""></thumb>    |
| c09         | text      | Link to uniqueid Table               |                                               |
| c10         | text      | Title formatted for sorting          | <sorttitle></sorttitle>                       |
| c11         | text      | Runtime                              | <runtime></runtime> \*\*                      |
| c12         | text      | MPAA Rating                          | <mpaa></mpaa>                                 |
| c13         | text      | IMDB Top 250 Ranking                 | <top250></top250>                             |
| c14         | text      | Genre                                | <genre></genre>                               |
| c15         | text      | Director                             | <director></director>                         |
| c16         | text      | Original Movie Title                 | <originaltitle></originaltitle>               |
| c17         | text      | Thumb URL Spoof                      |                                               |
| c18         | text      | Studio                               | <studio></studio>                             |
| c19         | text      | Trailer URL                          | <trailer></trailer>                           |
| c20         | text      | Fanart URL                           | s <fanart><thumb preview=""></thumb></fanart> |
| c21         | text      | Country                              | <country></country>                           |
| c22         | text      | Path to playable file                |                                               |
| c23         | text      | Link to path table for Source folder |                                               |
| idSet       | integer   | Foreign Key to sets table            |                                               |
| userrating  | integer   | Rating applied by user               | <userrating></userrating>                     |
| premiered   | text      | Date movie premiered                 | <premiered></premiered>                       |

| Notes |                     |
| ----- | ------------------- |
| \*\*  | Overwritten on Play |

`movielinktvshow`

This table links movies to TV shows.

| Column Name | Data Type | Description                 |
| ----------- | --------- | --------------------------- |
| idMovie     | integer   | Foreign key to movie table  |
| idShow      | integer   | Foreign key to tvshow table |

`musicvideo`

| Column Name | Data Type | Description                          | Music Videos                        |
| ----------- | --------- | ------------------------------------ | ----------------------------------- |
| idMVideo    | integer   | Primary Key                          |                                     |
| idFile      | integer   | Foreign Key to files table           |                                     |
| c00         | text      | Title                                | <title></title>                     |
| c01         | text      | Thumb URL                            | <thumb preview=""></thumb>          |
| c02         | text      | Thumb URL spoof                      |                                     |
| c03         | text      | Not Used                             |                                     |
| c04         | text      | Run time                             | <runtime></runtime>                 |
| c05         | text      | Director                             | <director></director>               |
| c06         | text      | Studio                               | s <studio></studio>                 |
| c07         | text      | Not Used                             |                                     |
| c08         | text      | Plot                                 | <plot></plot>                       |
| c09         | text      | Album                                | <album></album>                     |
| c10         | text      | Artist                               | <artist></artist>                   |
| c11         | text      | Genre                                | <genre></genre>                     |
| c12         | text      | Track                                |                                     |
| c13         | text      | Path to playable file                | <filenameandpath></filenameandpath> |
| c14         | text      | Link to path table for Source folder | <basepath></basepath>               |
| c15         | text      | Not Used                             |                                     |
| c16         | text      | Not Used                             |                                     |
| c17         | text      | Not Used                             |                                     |
| c18         | text      | Not Used                             |                                     |
| c19         | text      | Not Used                             |                                     |
| c20         | text      | Not Used                             |                                     |
| c21         | text      | Not Used                             |                                     |
| c22         | text      | Not Used                             |                                     |
| c23         | text      | Not Used                             |                                     |
| userrating  | integer   | Rating applied by user               | <userrating></userrating>           |
| premiered   | text      | Date movie premiered                 | <premiered></premiered>             |

`path`

This table stores path information.

| Column Name   | Data Type | Description                                                                  |
| ------------- | --------- | ---------------------------------------------------------------------------- |
| idPath        | integer   | Primary Key                                                                  |
| strPath       | text      | Path URL                                                                     |
| strContent    | text      | Type of content (tvshows, movies, etc...)                                    |
| strScraper    | text      | addon ID                                                                     |
| strHash       | text      | Hash                                                                         |
| scanRecursive | integer   | Recursive scan setting                                                       |
| useFolderName | s bool    | User folder names setting                                                    |
| strSetting    | s text    | Custom settings used by scraper                                              |
| noUpdate      | bool      | Exclude path from library update                                             |
| exclude       | bool      |                                                                              |
| allAudio      | bool      | Skip filename matching for external audio tracks (0 = Disabled, 1 = Enabled) |
| dateAdded     | text      |                                                                              |
| idParentPath  | integer   |                                                                              |

`rating`

This table stores the ratings for TV Shows, Episodes and Movies

| Column Name | Data Type | Description                                               |
| ----------- | --------- | --------------------------------------------------------- |
| rating_id   | integer   | Primary Key                                               |
| media_id    | integer   | Foreign key to episode table, tv show table, movie table, |
| media_type  | text      | Movies, TV Show, TV Episode                               |
| rating_type | text      | default                                                   |
| rating      | float     | rating from scraper site                                  |
| vote        | s integer | votes from scraper site                                   |

`seasons`

This table stores the links between tv show and seasons.

| Column Name | Data Type | Description                 | TV Show           |
| ----------- | --------- | --------------------------- | ----------------- |
| idSeason    | integer   | Primary Key                 |                   |
| idShow      | integer   | Foreign key to tvshow table |                   |
| season      | integer   | Season number               | <season></season> |
| name        | text      | Season Name                 |                   |
| userrating  | integer   | Season level User Rating    |                   |

`sets`

This table stores the id and name for movie sets. Sets are linked to movies in
the movie table (idSet column).

| Column Name | Data Type | Description                |
| ----------- | --------- | -------------------------- |
| idSet       | integer   | Primary Key                |
| strSet      | text      | The name of the set        |
| strOverview | text      | The description of the set |

`settings`

This table stores settings for individual files.

| Column Name         | Data Type | Description                   |
| ------------------- | --------- | ----------------------------- |
| idFile              | integer   | Foreign Key to files table    |
| Deinterlace         | bool      | Deinterlace                   |
| ViewMode            | integer   | ViewMode                      |
| ZoomAmount          | float     | ZoomAmount                    |
| PixelRatio          | float     | PixelRatio                    |
| VerticalShift       | float     |                               |
| AudioStream         | integer   | Selected audio stream         |
| SubtitleStream      | integer   | Selected subtitle stream      |
| SubtitleDelay       | float     | Amount of delay for subtitles |
| SubtitleOn          | bool      | Enable subtitles              |
| Brightne            | ss float  | Brightness                    |
| Contrast            | float     | Contrast                      |
| Gamma               | float     | Gamma                         |
| VolumeAmplification | float     | VolumeAmplification           |
| AudioDelay          | float     | AudioDelay                    |
| ResumeTime          | integer   | ResumeTime                    |
| Sharpne             | ss float  | Sharpness                     |
| NoiseReduction      | float     | Noise Reduction               |
| NonLinStretch       | bool      | Non Linear Stretch            |
| PostProce           | ss bool   | Post Processing               |
| ScalingMethod       | integer   | Scaling                       |
| DeinterlaceMode     | integer   | Deinterlace mode              |
| StereoMode          | integer   | Stereo Mode                   |
| StereoInvert        | bool      | Stereo Inversion              |
| VideoStream         | integer   | VideoStream                   |
| TonemapMethod       | integer   |                               |
| TonemapParam        | float     |                               |
| Orientation         | integer   |                               |
| CenterMixLevel      | integer   |                               |

`stacktimes`

This table stores playing times for files (used for playing multi-file videos).

| Column Name | Data Type | Description                |
| ----------- | --------- | -------------------------- |
| idFile      | integer   | Foreign key to files table |
| time        | s text    | Times                      |

`streamdetails`

This table contains information regarding codecs used, aspect ratios etc

| Column Name         | Data Type | Description                                            |
| ------------------- | --------- | ------------------------------------------------------ |
| idFile              | integer   | Foreign Key to files table                             |
| iStreamType         | integer   | 0 = video, 1 = audio, 2 = subtitle                     |
| strVideoCodec       | text      | Video codex (xvid etc)                                 |
| fVideoAspect        | float     | Aspect ratio                                           |
| iVideoWidth         | integer   | Width of the video                                     |
| iVideoHeight        | integer   | Height of the video                                    |
| iVideoDuration      | integer   | Actual runtime in sec                                  |
| strStereoMode       | text      | Stereo Mode                                            |
| strAudioCodec       | text      | Audio codec (aac, mp3 etc)                             |
| iAudioChannel       | s integer | Number of audio channels (2 for stereo, 6 for 5.1 etc) |
| strAudioLanguage    | text      | Language of the audio track                            |
| strSubtitleLanguage | text      | Language of the subtitle                               |
| strVideoLanguage    | text      | Language of the Video                                  |
| strHdrType          | text      | hdr type of the video                                  |

| Notes | -                                          |
| ----- | ------------------------------------------ |
| \*\*  | Settings Will be overwritten on first play |

`studio`

This table stores studio information.

| Column Name | Data Type | Description  | Movies, TV Shows, TV Episodes, Music Videos |
| ----------- | --------- | ------------ | ------------------------------------------- |
| studio_id   | integer   | Primary Key  |                                             |
| name        | text      | Studio Label | <studio></studio>                           |

`studio link`

This table links studios to movies, music videos and TV shows

| Column Name | Data Type | Description                                                  |
| ----------- | --------- | ------------------------------------------------------------ |
| studio_id   | integer   | Foreign key to studio table                                  |
| media_id    | integer   | Foreign key to movie table, tv show table, music video table |
| media_type  | text      | Movie, Music Video, TV Show                                  |

`tag`

This stores tags.

| Column Name | Data Type | Description | Movies, TV Shows, Music Videos |
| ----------- | --------- | ----------- | ------------------------------ |
| tag_id      | integer   | Primary Key |                                |
| name        | integer   | Tag         | <tag></tag>                    |

`tag_link`

This table links tags to various media.

| Column Name | Data Type | Description                  |
| ----------- | --------- | ---------------------------- |
| tag_id      | integer   | Foreign key to tag table     |
| media_id    | integer   | Foreign key to a media table |
| media_type  | text      | Media type for link          |

`tvshow`

This table stores information about a television series. Information concerning
the shows episodes is stored in episode. To link a TV show to its episodes, use
tvshowlinkepisode.

| Column Name | Data Type | Description                                    | TV Show                                                             |
| ----------- | --------- | ---------------------------------------------- | ------------------------------------------------------------------- |
| idShow      | integer   | Primary Key                                    |                                                                     |
| c00         | text      | Show Title                                     | <showtitle></showtitle>                                             |
| c01         | text      | Show Plot Summary                              | <plot></plot>                                                       |
| c02         | text      | Status                                         | <status></status>                                                   |
| c03         | text      | Unknown                                        |                                                                     |
| c04         | text      | Link to Rating Table                           |                                                                     |
| c05         | text      | First Aired                                    | <premiered></premiered>                                             |
| c06         | text      | Thumbnail URL                                  | <thumb aspect="" type="" season=""></thumb>                         |
| c07         | text      | [unknown - Spoof Thumbnail URL?]               |                                                                     |
| c08         | text      | Genre                                          | <genre></genre>                                                     |
| c09         | text      | Original Title                                 | <originaltitle></originaltitle>                                     |
| c10         | text      | Episode Guide URL                              | <episodeguide><url cache=""></url></episodeguide>                   |
| c11         | text      | Fan Art URL                                    | <fanart url=""><thumb dim="" colors="" preview=""></thumb></fanart> |
| c12         | text      | Unique ID issued by Kodi based on Scraper ID's |                                                                     |
| c13         | text      | Content Rating                                 | <mpaa></mpaa>                                                       |
| c14         | text      | Studio                                         | <studio></studio>                                                   |
| c15         | text      | Title formatted for sorting                    | <sorttitle></sorttitle>                                             |
| c16         | text      | Trailer                                        | <trailer></trailer>                                                 |
| c17         | text      | Not Used                                       |                                                                     |
| c18         | text      | Not Used                                       |                                                                     |
| c19         | text      | Not Used                                       |                                                                     |
| c20         | text      | [unknown]                                      |                                                                     |
| c21         | text      | [unknown]                                      |                                                                     |
| c22         | text      | [unknown]                                      |                                                                     |
| c23         | text      | [unknown]                                      |                                                                     |
| userrating  | integer   | Rating applied by user                         | <userrating></userrating>                                           |
| duration    | integer   | Length of Episodes                             | <runtime></runtime>                                                 |

`tvshowlinkpath`

This table links a TV show to its path.

| Column Name | Data Type | Description                 |
| ----------- | --------- | --------------------------- |
| idShow      | integer   | Foreign key to tvshow table |
| idPath      | integer   | Foreign key to path table   |

`uniqueid`

This table holds the UniqueID's for Movies, TV shows and Episodes. Normally the
UniqueID's are the ID's used at the scraper sites. For user created nfo files
for say, home movies, the ID's are user nominated. Music Videos do not require a
UniqueID.

| Column Name | Data Type | Description                  | Movies, TV Shows, TV Episodes                                       |
| ----------- | --------- | ---------------------------- | ------------------------------------------------------------------- |
| uniqueid    | integer   | Primary Key                  |                                                                     |
| media_id    | integer   | Foreign key to a media table |                                                                     |
| media_type  | text      | Media type for link          | <movie></movie>,<tvshow></tvshow>,<episodedetails></episodedetails> |
| value       | text      | ID at scraper site           | <id></id>                                                           |
| type        | text      | Scraper site                 |                                                                     |

`version`

This table stores database information.

| Column Name     | Data Type | Description                                  |
| --------------- | --------- | -------------------------------------------- |
| idVersion       | integer   | Version of database                          |
| idCompressCount | integer   | Number of times database has been compressed |

`writer_link`

This table links writers stored in the actors table to movies and episodes.

| Column Name | Data Type | Description                  |
| ----------- | --------- | ---------------------------- |
| actor_id    | integer   | Foreign key to actors table  |
| media_id    | integer   | Foreign key to a media table |
| media_type  | text      | Media type for link          |

### Textures

The Textures#.db database file contains the information for all Kodi Artwork

`path`

This table holds information on the type and location of Artwork

| Column Name | Data Type | Description                             |
| ----------- | --------- | --------------------------------------- |
| id          | integer   | Primary Key                             |
| url         | text      | Path to folder containing playable file |
| type        | text      | Artwork type (poster, fanart etc)       |
| texture     | text      | Path to original artwork                |

`sizes`

This table holds information regarding the size and usage of the Artwork

| Column Name | Data Type | Description |
| ----------- | --------- | ----------- |
| idtexture   | integer   | Primary Key |
| size        | integer   |             |
| width       | integer   | Width px    |
| height      | integer   | Height px   |
| usecount    | integer   |             |
| lastusetime | text      |             |

`texture`

This table links the cached file to the correct title and stores file hash
information

| Column Name   | Data Type | Description                               |
| ------------- | --------- | ----------------------------------------- |
| id            | integer   | Primary Key                               |
| url           | text      | Path to original artwork                  |
| cachedurl     | text      | Name of cached file                       |
| imagehash     | text      | Hash of image                             |
| lasthashcheck | text      | Last time artwork was checked for changes |

`version`

Database details

| Column Name    | Data Type | Description      |
| -------------- | --------- | ---------------- |
| idVersion      | integer   | Database version |
| iCompressCount | integer   |                  |

## TV

The TV#.db database file contains the information for Live-TV channels.

`channelgroups`

Holds the information related to the Channel Groups

| Column Name  | Data Type       | Description                     |
| ------------ | --------------- | ------------------------------- |
| idGroup      | integer         | Primary Key                     |
| blsRadio     | bool            | Is Radio Group- Y/N             |
| iGroupType   | integer         |                                 |
| sName        | varchar(64)     | Name of Channel Group           |
| iLastWatched | integer         | Last time Channel Group watched |
| blsHidden    | bool            | Hidden group? Y/N               |
| iPosition    | integer         |                                 |
| iLastOpened  | bigint unsigned | Epoch time                      |

`channels`

Holds the information related to each TV Channel

| Column Name        | Data Type    | Description                                |
| ------------------ | ------------ | ------------------------------------------ |
| idChannel          | integer      | Primary Key                                |
| iUniqueId          | integer      |                                            |
| bIsRadio           | bool         | Is Radio Channel- Y/N                      |
| bIsHidden          | bool         | Hidden Channel? Y/N                        |
| bIsUserSetIcon     | bool         | Has user set channel icon                  |
| bIsUerSetName      | bool         | Has user set channel name                  |
| bIsLocked          | bool         | Locked channel? Y/N                        |
| sIconPath          | varchar(255) | Path to channel logo icon                  |
| sChannelName       | varchar(64)  | Friendly name of channel                   |
| bIsVirtual         | bool         | Virtual channel? Y/N                       |
| bEPGEnabled        | bool         | Receive EPG? Y/N                           |
| sEPGScraper        | varchar(32)  | Source of EPG data                         |
| iLastWatched       | integer      | Last time channel watched using Epoch Time |
| iClientId          | integer      |                                            |
| idEPG              | integer      |                                            |
| bHasArchive        | bool         | Set true if this channel supports archive  |
| iClientProviderUid | integer      |                                            |
| bIsUserSetHidden   | bool         |                                            |

`clients`

| Column Name | Data Type | Description |
| ----------- | --------- | ----------- |
| idClient    | integer   |             |
| iPriority   | integer   |             |

`map_channelgroups_channels`

Links Channels to Channel Groups

| Column Name             | Data Type | Description                           |
| ----------------------- | --------- | ------------------------------------- |
| idChannel               | integer   | Channel number from channels table    |
| idGroup                 | integer   | Group number from channelgroups table |
| iChannelNumber          | integer   | Channel number                        |
| iSubChannelNumber       | integer   | Sub-channel number                    |
| iOrder                  | integer   |                                       |
| iClientChannelNumber    | integer   |                                       |
| iClientSubChannelNumber | integer   |                                       |

`providers`

Information of channel providers

| Column Name | Data Type     |
| ----------- | ------------- |
| idProvider  | integer       |
| iUniqueId   | integer       |
| iClientId   | integer       |
| sName       | varchar(64)   |
| iType       | integer       |
| sIconPath   | varchar(255)  |
| sCountrie   | s varchar(64) |
| sLanguage   | s varchar(64) |

`timers`

| Column Name        | Data Type    |
| ------------------ | ------------ |
| iClientIndex       | integer      |
| iParentClientIndex | integer      |
| iClientID          | integer      |
| iTimerType         | integer      |
| iState             | integer      |
| sTitle             | varchar(255) |
| iClientChannelUid  | integer      |
| sSeriesLink        | varchar(255) |
| sStartTime         | varchar(20)  |
| bStartAnyTime      | bool         |
| sEndTime           | varchar(20)  |
| bEndAnyTime        | bool         |
| sFirstDay          | varchar(20)  |
| iWeekday           | s integer    |
| iEpgUID            | integer      |
| iMarginStart       | integer      |
| iMarginEnd         | integer      |
| sEpgSearchString   | varchar(255) |
| bFullTextEpgSearch | bool         |
| iPreventDuplicate  | s integer    |
| iPrority           | integer      |
| iLifetime          | integer      |
| iMaxRecording      | s integer    |
| iRecordingGroup    | integer      |

`version`

Database details

| Column Name    | Data Type | Description      |
| -------------- | --------- | ---------------- |
| idVersion      | integer   | Database version |
| iCompressCount | integer   |                  |

### ViewModes

Kodi stores the selected view type for every path in every skin. This enables
different view types for different parts of the library. This database contains
the last set view and sorting method for each path while navigating Kodi.

`version`

Database details

| Column Name    | Data Type | Description      |
| -------------- | --------- | ---------------- |
| idVersion      | integer   | Database version |
| iCompressCount | integer   |                  |

`view`

This table stores details on the saved view mode for all known paths.

| Column Name   | Data Type | Description                          |
| ------------- | --------- | ------------------------------------ |
| idView        | integer   | Primary Key                          |
| window        | integer   | Window GUI ID                        |
| path          | text      | Path to trigger the view on          |
| viewMode      | integer   | View Mode                            |
| sortMethod    | integer   | ID of sort method                    |
| sortOrder     | integer   | Sort order (ascending or descending) |
| sortAttribute | s integer |                                      |
| skin          | text      | Skin settings apply to               |
