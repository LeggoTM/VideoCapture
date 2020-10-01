# VideoCapture
Grabs screenshots from a video
You can do like this in Java 
First, you need to add a proper permission to save the file:

`<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>`
And this is the code (running in an Activity):

`private void takeScreenshot() {
    Date now = new Date();
    android.text.format.DateFormat.format("yyyy-MM-dd_hh:mm:ss", now);

    try {
        // image naming and path  to include sd card  appending name you choose for file
        String mPath = Environment.getExternalStorageDirectory().toString() + "/" + now + ".jpg";

        // create bitmap screen capture
        View v1 = getWindow().getDecorView().getRootView();
        v1.setDrawingCacheEnabled(true);
        Bitmap bitmap = Bitmap.createBitmap(v1.getDrawingCache());
        v1.setDrawingCacheEnabled(false);

        File imageFile = new File(mPath);

        FileOutputStream outputStream = new FileOutputStream(imageFile);
        int quality = 100;
        bitmap.compress(Bitmap.CompressFormat.JPEG, quality, outputStream);
        outputStream.flush();
        outputStream.close();

        openScreenshot(imageFile);
    } catch (Throwable e) {
        // Several error may come out with file handling or DOM
        e.printStackTrace();
    }
}`
