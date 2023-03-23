### inside oncreate

``` java

mywebView.setDownloadListener(new DownloadListener() {
            @Override
            public void onDownloadStart(String url, String useragent, String contentdisposition, String mimetype, long contentlength) {
                if(Build.VERSION.SDK_INT >= Build.VERSION_CODES.M)
                {
                    if(checkSelfPermission(android.Manifest.permission.WRITE_EXTERNAL_STORAGE) == PackageManager.PERMISSION_GRANTED)
                    {
                        DowloadDialog(url,useragent,contentdisposition,mimetype);
                    }
                    else
                    {
                        ActivityCompat.requestPermissions(MainActivity.this,new String[]{Manifest.permission.WRITE_EXTERNAL_STORAGE},1);
                    }
                }
                else
                {
                    DowloadDialog(url,useragent,contentdisposition,mimetype);
                }
            }


        });



```


### above webview

``` java

private void DowloadDialog(final String url, final String UserAgent, String contentdisposition, String mimetype) {

        final  String filename = URLUtil.guessFileName(url,contentdisposition,mimetype);
        final AlertDialog.Builder builder = new AlertDialog.Builder(this);
        builder.setTitle("Downloading...")
                .setMessage("Do you want to Download "+ ' '+" "+filename+" "+' ')
                .setPositiveButton("Yes", new DialogInterface.OnClickListener() {
                    @Override
                    public void onClick(DialogInterface dialogInterface, int i) {
                        DownloadManager.Request request = new DownloadManager.Request(Uri.parse(url));
                        String cookie = CookieManager.getInstance().getCookie(url);
                        request.addRequestHeader("Cookie",cookie);
                        request.addRequestHeader("User-Agent",UserAgent);
                        request.allowScanningByMediaScanner();
                        request.setNotificationVisibility(DownloadManager.Request.VISIBILITY_VISIBLE_NOTIFY_COMPLETED);
                        DownloadManager manager = (DownloadManager)getSystemService(DOWNLOAD_SERVICE);
                        request.setDestinationInExternalPublicDir(Environment.DIRECTORY_DOWNLOADS,filename);
                        manager.enqueue(request);
                    }
                })
                .setNegativeButton("No", new DialogInterface.OnClickListener() {
                    @Override
                    public void onClick(DialogInterface dialogInterface, int i) {
                        dialogInterface.cancel();
                    }
                })
                .show();

    }


```