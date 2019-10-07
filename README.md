# Document-Scanner-API
Document Scanner API - Android Studio

The Document Scanner Library is built with the OpenCV. On importing the library module to your required creation in Android Studio will allow the user to
  - Select exact edges of the picture
  - Crop the Edges with the selected border
  - Change the perspective transformation of the cropped image

**Updated OpenCV Framework** [openCV](https://opencv.org/releases/) / [Git repo](https://github.com/opencv/opencv/tree/4.1.1)

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


# Required Library Dependency
On building the app the error of 'android support' pops up in some cases.

**error: package android.support.v4.content does not exist**

- Add the library dependency android support v4 through project structure
or just add the below snippet in build.gradle(Module:app) file 

```

dependencies {
    //
    // IDE setting pulls in the specific version of v4 support you have installed:
    //
    //compile 'com.android.support:support-v4:21.0.3'

    //
    // generic directive pulls in any available version of v4 support:
    //
    compile 'com.android.support:support-v4:+'
}

```


# Screenshot
<div align="center">
<a href="https://raw.githubusercontent.com/JagadishSivakumar/Document-Scanner-API/master/scanlibrary/ScanDemoExample/screenshots/design.png" />
<img width="23%" height="400px" src="https://raw.githubusercontent.com/JagadishSivakumar/Document-Scanner-API/master/scanlibrary/ScanDemoExample/screenshots/design.png" alt="Scan Input" title="Scan Input"></img>

<a href="https://raw.githubusercontent.com/JagadishSivakumar/Document-Scanner-API/master/scanlibrary/ScanDemoExample/screenshots/click.png" />
<img width="23%" src="https://raw.githubusercontent.com/JagadishSivakumar/Document-Scanner-API/master/scanlibrary/ScanDemoExample/screenshots/click.png" alt="Scan Input" title="Scan Input"></img>

<a href="https://raw.githubusercontent.com/JagadishSivakumar/Document-Scanner-API/master/scanlibrary/ScanDemoExample/screenshots/crop.png" />
<img width="23%" src="https://raw.githubusercontent.com/JagadishSivakumar/Document-Scanner-API/master/scanlibrary/ScanDemoExample/screenshots/crop.png" alt="Scan Input" title="Scan Input"></img>

<a href="https://raw.githubusercontent.com/JagadishSivakumar/Document-Scanner-API/master/scanlibrary/ScanDemoExample/screenshots/options.png" />
<img width="23%" src="https://raw.githubusercontent.com/JagadishSivakumar/Document-Scanner-API/master/scanlibrary/ScanDemoExample/screenshots/options.png" alt="Scan Input" title="Scan Input"></img>

<a href="https://raw.githubusercontent.com/JagadishSivakumar/Document-Scanner-API/master/scanlibrary/ScanDemoExample/screenshots/blacknwhite.png" />
<img width="23%" style="float:left;" src="https://raw.githubusercontent.com/JagadishSivakumar/Document-Scanner-API/master/scanlibrary/ScanDemoExample/screenshots/blacknwhite.png" alt="Scan Input" title="Scan Input"></img>
</div>


# License

	Copyright (c) 2019 Jagadish Sivakumar
	
	
	The DocumentScanner app was built with the scanlibrary module dependency which
	was developed by Jhansi Karee with tweaks and enhancements to the design and
	MainActivity execution.
	
	Permission is hereby granted, free of charge, to any person obtaining a copy
	of this software and associated documentation files (the "Software"), to deal
	in the Software without restriction, including without limitation the rights
	to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
	copies of the Software, and to permit persons to whom the Software is
	furnished to do so, subject to the following conditions:

	The above copyright notice and this permission notice shall be included in all
	copies or substantial portions of the Software.

	THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
	IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
	FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
	AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
	LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
	OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
	SOFTWARE.


