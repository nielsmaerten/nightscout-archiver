# Nightscout Archiver

A simple script that copies your Nightscout records from one Mongo database to another.  

## How do I use this?

1. Fork this repo
2. Open the repo's Action Secrets:  
   https://github.com/[yourGitHubUsername]/nightscout-archiver/settings/secrets/actions
3. Add these 2 secrets:
   - `SOURCE`: The full connectionstring of your main Nightscout MongoDB.  
   This is the same value as MONGODB_URI in your Heroku config settings
   - `DEST`: Connectionstring for the database you want to export your records to

    For example:

    - **SOURCE**: `mongodb+srv://USERNAME:PASSWORD@host.mongodb.net/nightscout?retryWrites=true&w=majority`
    - **DEST**: `mongodb+srv://USERNAME:PASSWORD@host.mongodb.net/?retryWrites=true&w=majority`

**Note:** In 'source', the name of the database (nightscout) is specified after the /, but in 'dest' it is not.

## Running the script

- By default, the script will run every 1st day of the month, you can edit this in the [workflow file](.github/workflows/archive.yml).
- The script can also be run on demand by going to the Actions tab in GitHub > Archive Nightscout > Run Workflow

## Why?

This script could be useful if you're using a free 500MB MongoDB as your main Nightscout database,
but you want to archive your old records into another database instead of deleting them.

I personally transfer my records over to a 'serverless' instance on MongoDB Atlas every month. Nightscout does not (yet) support serverless databases. But once they do, I could theoretically just switch the connectionstring in Heroku and start using that one.

Another scenario would be having a self-hosted MongoDB for archiving purposes, that you don't want to be online 24/7.
