
# FAQ
## How to add custom page list?

 1. Get list of facebook URLs for specific client.

 **example**
 ```
 For client:
 https://noise.apps.socialbakers.com/tritone/252434

 Add pages:
 http://www.facebook.com/corinthians/
 http://www.facebook.com/santosfc
 http://www.facebook.com/PontePretaOficial/
 ```

 1. Using http://datamining.ccl/page-info/ get respective list of page IDs.

 ```
 132769576762243
 101402899928278
 156238824423790
 ```

 1. Open production MySQL database and insert pairs [account_id, page_id] to 'account_has_page' table.

 ```sql
 insert into account_has_page values
  (253427, 132769576762243),
  (253427, 101402899928278),
  (253427, 156238824423790);
 ```

## How to create and use custom styles (custom skin)?

 1. Creta new folder named with accountId in `public/sass/custom-styles/[accountId]`

 1. Copy/paste there main sass file, e.g. `public/sass/custom-styles/test/style.sass`

 1. In the new custom style.sass, to change some of the styles:
  * create custom version of some of the imported files in the same folder (typically constants.sass)
  * make changes in that custom file
  * change the import command to import this custom version of file

 1. Gruntfile changes:
  * add new path in sass.custom.files definition
  * add new path in postcss.custom.src definition

 1. Generate new styles using grunt task `grunt custom-styles`

 1. Upload the file in Amazon S3 storage, bucket `sbks-noise-prediction`
  * rename generated CSS file to skin-01.css
  * path `noiseprediction/custom-skins/[accountId]/skin-01.css`

 1. MySQL changes:
  * in table `account` change for row with specific accountId flag `skin_active` to 1
