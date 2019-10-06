# Document-Scanner-API
Document Scanner API - Android Studio

The Document Scanner Library is built with the OpenCV. On importing the library module to your required creation in Android Studio will allow the user to
  - Select exact edges of the picture
  - Crop the Edges with the selected border
  - Change the perspective transformation of the cropped image

# Importing to your Project 
- Android Studio 3.5
- Compile SDK Version 28 

Add the dependecy to your project through Project Structure.
```	
Files => Project Structure => Dependecy => App => Module Dependency
```	

```	    
compile project(':scanlibrary')
```
For the user to start scanning, Start Scan library. The app will go to the library. Add the function/ code snippet given to the **MainActivity.java** file.

```	
public void openCamera(View v){
        int REQUEST_CODE = 99;
        int preference = ScanConstants.OPEN_CAMERA;
        Intent intent = new Intent(this, ScanActivity.class);
        intent.putExtra(ScanConstants.OPEN_INTENT_PREFERENCE, preference);
        startActivityForResult(intent, REQUEST_CODE);
    }

    public void  openGallery(View v){
        int REQUEST_CODE = 99;
        int preference = ScanConstants.OPEN_MEDIA;
        Intent intent = new Intent(this, ScanActivity.class);
        intent.putExtra(ScanConstants.OPEN_INTENT_PREFERENCE, preference);
        startActivityForResult(intent, REQUEST_CODE);
    }
```	
    
When the scanning action is completed the app is returned from instance of scanlibrary to main app, to retrieve the scanned image and to get the next screen of getiing the result scan.
```	
    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        super.onActivityResult(requestCode, resultCode, data);

        if (requestCode == 99 && resultCode == Activity.RESULT_OK) {
            Uri uri = data.getExtras().getParcelable(ScanConstants.SCANNED_RESULT);
            Bitmap bitmap = null;
            try {
                bitmap = MediaStore.Images.Media.getBitmap(getContentResolver(), uri);
                getContentResolver().delete(uri, null, null);
                ImageView scannedImageView;
               // scannedImageView.setImageBitmap(bitmap);
            } catch (IOException e) {
                e.printStackTrace();
            }
        }


    }
```	

