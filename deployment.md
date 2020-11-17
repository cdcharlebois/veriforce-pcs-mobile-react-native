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

* Begin build on Team Server, noting the application version number (including build number)

* Begin [bundle](https://docs.mendix.com/refguide/native-builder#2-8-generating-only-the-app-bundles) locally

* When the local bundle finishes, move the bundle into the appropriate directory as described [here](https://docs.mendix.com/howto/mobile/native-build-locally#4-bundling-your-mendix-app). 

* Once you have placed the bundles in the right directories, update the _.env_ files with the application version number in the `VERSION_NUMBER` variable.

* Commit your work to the appropriate git branch (_deployment/dev_ or *deployment/beta*)

  > Note that both these branches are currently configured to execute a build on push.

## Release

> Note that at the time of writing, there is a known issue with the OTA update function on AppCenter where Mendix OTA updates are not working. :(

If you want to release an OTA update (just the app bundle without a new build) you can do so via the appcenter codepush API

* Bundle your app as you normally would, and move the bundle to the correct resource directories (as above)

* Run the `appcenter codepush release` command as documented [here](https://docs.microsoft.com/en-us/appcenter/distribution/codepush/cli#releasing-updates-general).

  ```bash
  appcenter codepush release \
    -a "Veriforce/PCS" \
    -c "<path/to/native>/verisource-pcs-mobile-react-native/ios/Bundle" \
    -t "*" \
    -d "Dev" \
    -m \
    --description "Update to PCS Version <application_version>"
  ```

* The next time that a user closes and re-opens the application, they will be presented with a prompt to update the application. 

  > Note that the `-m` option flags this release as mandatory.