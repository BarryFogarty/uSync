uSync 3
=
uSync lets you serialize the settings and configuration elements of an Umbraco site, to and from the database, 
making it easier to have multiple developers working on a project and working towards simpler deployment of changes.

For uSync 3 we have decoupled the de/serialization of Umbraco objects from the disk and tracking parts giving us 
much more flexibility when it comes to what we can do with uSync

uSync.Core
-
this is the core of uSync - it contains everything to serialize and de-serialize elements of Umbraco, the serizlizers 
in the core, allow you to take a database element and give it a generic xml representation, and to take xml and push
it into Umbraco.

One of the keys to uSync is how it makes the exported data generic allowing you to move it between installations; usync
converts internal id's to strings and transferable GUID values so when you get to another install everything is still
linked. 

Also for speed the serialization in core come with change detection allowing for you to only import changes when things
are actually different - this makes a significant difference to the speed at which a site can be imported, and is 
especially important if you are using usync as part of a site's start-up process.

uSync.BackOffice
-

Backoffice replicates the functionality of the traditional uSync package using the core as the engine for change. 

by using the core, we have been able to make the back office elements of uSync much more robust and flexible. Changes 
are now tracked better, renames and deletes can be followed across installations more reliably, and we can report what
changes are going to happen before imports are ran. 

BackOffice also uses implements a Type handler so it can be extended to sync other things - by implementing ISyncHanlder interface
you can have your items synced at the same time as uSync performs it's own synchronisation. 

uSync.ContentEdition
-
Content Syncing, using the Core, content edition is now two additional Sync Handlers for uSync BackOffice. when you install the content Edition dll, the back office picks this up, and run media and content handlers after all the other items are installed. 

Media is also extracted from the site, and stored in a _uSyncMedia under each media node, this means you can move the uSync folder and get all the media too *although things like image croppers directly inside content don't get picked up, so you might want to copy media over aswell :(*
uSync.Snapshots
-

Snapshots allows you to take snapshots of you're site and create point in time changesets. 

each changeset contains the changes that have occured on you're site since the last time you took a snapshot, these changesets,
can then be deployed to a site, and uSync will combine them and bring all the changes through - giving you a much more incremental
way of managing changes on you're site.

Snapshots will (soon) come with a command line interface that will allow you to create changes programatically and potentially
use the changesets as part of a deployment process.

