# Deployment

Since the Veriforce policy is not to use Github, there are some manual steps involved in the deployment of the native application:

## Summary

* Mendix server model releases as usual
* Bundle the native app code from your local working copy, then
* Push to installed apps via AppCenter CodePush (command line)

## Preparation

* App Center
* `native-builder.exe prepare`

## Build (bundle)

* Commit changes to Team Server, pull any updates
* Begin build on Team Server
* Begin bundle locally

## Release

* AppCenter CodePush (commandline)