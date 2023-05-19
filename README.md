# Image Picker Android

# Configuration

# Step 1

```Groovy
allprojects {
    repositories {
        maven { url "https://jitpack.io" }
    }
}
```

# Step 2 - Initialize the methods for Image Pickers

```Kotlin
initPickAnImageFromGalleryResultLauncher(
    fragmentActivity = this,
    imagePickerInterface = this
)

initPickMultipleImagesFromGalleryResultLauncher(
    fragmentActivity = this,
    coroutineScope = lifecycleScope,
    imagePickerInterface = this
)

initTakePhotoWithCameraResultLauncher(
    fragmentActivity = this,
    imagePickerInterface = this
)
```

# Step 3 - Call the interface (Optional)

```Kotlin
override fun onGalleryImage(bitmap: Bitmap?, uri: Uri?) {
    super.onGalleryImage(bitmap, uri)
}

override fun onCameraImage(bitmap: Bitmap?, uri: Uri?) {
    super.onCameraImage(bitmap, uri)
}

override fun onMultipleGalleryImages(
    bitmapList: MutableList<Bitmap>?,
    uriList: MutableList<Uri>?
) {
    lifecycleScope.launch(Dispatchers.Main) {}
    super.onMultipleGalleryImages(bitmapList, uriList)
}
```