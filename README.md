# Image Picker Android

This library built to give to other developers an easy way to implement the image picker in Android
application with latest Android technologies.
Support me and I will appreciate if you provide me your feedback(s).

The library contain:

- Picker for single image from gallery
- Picker for multiple images from gallery (up to 9 images)
- Take single image from camera (handled permission)
- Video Picker
- Support for the base64 value and scale (resize) are only for image
- All the previous features supported on Jetpack Compose

### Versioning

Gradle Version 8.0.2 <br />
Kotlin Version 1.8.22 <br />
JDK Version 17 <br />
Minimum SDK 24 <br />
Target SDK 33 <br />

## IMPORTANT NOTE

THE NEXT BETA RELEASES MAYBE CONTAIN MAJOR/MINOR CHANGES

## Configuration

[![](https://jitpack.io/v/NicosNicolaou16/ImagePickerAndroid.svg)](https://jitpack.io/#NicosNicolaou16/ImagePickerAndroid)

### Standard Configuration

### Step 1

```Groovy
implementation 'com.github.NicosNicolaou16:ImagePickerAndroid:1.0.0'
```

```Groovy
allprojects {
    repositories {
        maven { url "https://jitpack.io" }
    }
}
```

### Step 2 - Get Instance

```Kotlin
class MainActivity : AppCompatActivity(), ImagePickerInterface {
    //...
    private var imagePicker: ImagePicker? = null

    //...
    fun initImagePicker() {
        //Builder
        //Note: fragmentActivity or fragment are mandatory one of them
        imagePicker = ImagePicker(
            fragmentActivity = this, //activity instance - private
            fragment = this, // fragment instance - private
            coroutineScope = lifecycleScope, // mandatory - coroutine scope from activity or fragment - private
            scaleBitmapModelForSingleImage = ScaleBitmapModel(
                height = 100,
                width = 100
            ), // optional, change the scale for image, by default is null
            scaleBitmapModelForMultipleImages = ScaleBitmapModel(
                height = 100,
                width = 100
            ), // optional, change the scale for image, by default is null
            scaleBitmapModelForCameraImage = ScaleBitmapModel(
                height = 100,
                width = 100
            ), // optional, change the scale for image, by default is null
            enabledBase64ValueForSingleImage = true, // optional, by default is false - private
            enabledBase64ValueForMultipleImages = true, // optional, by default is false - private
            enabledBase64ValueForCameraImage = true, // optional, by default is false - private
            imagePickerInterface = this // call back interface
        )
        //...other image picker initialization method(s)
    }
    //...
}
```

### Step 3 - Initialize the methods for Image Pickers (choose the preferred method(s))

```Kotlin
imagePicker?.initPickSingleImageFromGalleryResultLauncher()

imagePicker?.initPickMultipleImagesFromGalleryResultLauncher()

imagePicker?.initTakePhotoWithCameraResultLauncher()

imagePicker?.initPickSingleVideoFromGalleryResultLauncher()
```

### Step 4 Call from Click Listeners (choose the preferred method(s))

```Kotlin
imagePicker?.pickSingleImageFromGallery()

imagePicker?.pickMultipleImagesFromGallery()

imagePicker?.takeSinglePhotoWithCamera()

imagePicker?.pickSingleVideoFromGallery()
```

### Step 5 - Callbacks (Optionals)

```Kotlin
class MainActivity : AppCompatActivity(), ImagePickerInterface {
    //...
    override fun onGallerySingleImage(bitmap: Bitmap?, uri: Uri?) {
        super.onGalleryImage(bitmap, uri)
        //...your code here
    }

    override fun onCameraImage(bitmap: Bitmap?) {
        super.onCameraImage(bitmap)
        //...your code here
    }

    override fun onMultipleGalleryImages(
        bitmapList: MutableList<Bitmap>?,
        uriList: MutableList<Uri>?
    ) {
        super.onMultipleGalleryImages(bitmapList, uriList)
        //...your code here
    }

    override fun onGallerySingleImageWithBase64Value(
        bitmap: Bitmap?,
        uri: Uri?,
        base64AsString: String?
    ) {
        super.onGalleryImage(bitmap, uri, base64AsString)
        //...your code here
    }

    override fun onCameraImageWithBase64Value(bitmap: Bitmap?, base64AsString: String?) {
        super.onCameraImage(bitmap, base64AsString)
        //...your code here
    }

    override fun onMultipleGalleryImagesWithBase64Value(
        bitmapList: MutableList<Bitmap>?,
        uriList: MutableList<Uri>?,
        base64AsStringList: MutableList<String>?
    ) {
        super.onMultipleGalleryImages(bitmapList, uriList, base64AsStringList)
        //...your code here
    }

    override fun onGallerySingleVideo(uri: Uri?) {
        super.onGallerySingleVideo(uri)
        //...your code here
    }
}
```

### Compose Configuration

### Step 1 - Initialize

```Kotlin
PickSingleImage(scaleBitmapModel = null, listener = { bitmap, uri ->
    if (bitmap != null) {
        //handle the bitmap
    }
})

PickSingleImageWithBase64Value(scaleBitmapModel = null, listener = { bitmap, uri, base64 ->
    if (bitmap != null) {
        //handle the bitmap
    }
})

PickMultipleImages(scaleBitmapModel = null,
    listener = { bitmapList, uriList ->
        if (bitmapList != null) {
            //handle the bitmapList
        }
    })

PickMultipleImagesWithBase64Values(
    scaleBitmapModel = null,
    listener = { bitmapList, uriList, base64List ->
        if (bitmapList != null) {
            //handle the bitmapList
        }
    })

TakeCameraImage(scaleBitmapModel = null, listener = { bitmap, uri ->
    if (bitmap != null) {
        //handle the bitmap
    }
})

TakeCameraImageWithBase64Value(scaleBitmapModel = null, listener = { bitmap, uri, base64 ->
    if (bitmap != null) {
        //handle the bitmap
    }
})

PickVideo(listener = { uri ->
    if (uri != null) {
        //handle the uri
    }
})
```

### Step 2 Call from Click Listeners (choose the preferred method(s))

```Kotlin
pickSingleImage()

pickSingleImageWithBase64Value()

pickMultipleImages()

pickMultipleImagesWithBase64Value()

takeCameraImage()

takeCameraImageWithBase64Value()

pickVideo()
```