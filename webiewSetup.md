### step 1:Start new project and select empty activity

### step-2 :give a name to your project select language as java

### step 3:open manifest folder and click on andriod manifest

note best this code above <application

``` xml
<uses-permission android:name="android.permission.INTERNET"/></uses-permission>
    

```
### step 4: go  to res folder choose layout inside layout folder, inside this folder you can see acticity.xml, just paste this code above </android.support.constraint.ConstraintLayout>

``` xml


<WebView
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:id="@+id/webview"></WebView>


```

### step 5 now delete <android.support.constraint.ConstraintLayout> from activity.xml and change it to relative layout


``` xml
<android.support.constraint.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <WebView
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:id="@+id/webview"></WebView>
</android.support.constraint.ConstraintLayout>


```

change above code into below code


``` xml

<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <WebView
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:id="@+id/webview"></WebView>
</RelativeLayout>


```


### step 6: remove action bar:inside res folder choose values folder and choose themes folder inside themes you can find themes.xml yoy can find code like this in third line

``` xml
    <style name="Theme.MyApplication" parent="Theme.AppCompat.Light.DarkActionBar">


```

change into

``` xml

    <style name="Theme.MyApplication" parent="Theme.AppCompat.Light.NoActionBar">


```

### step 7 :open mainactivity.java and import below packages at top below package name code

``` java

import android.webkit.WebSettings;
import android.webkit.WebView;
import android.webkit.WebViewClient;

```
### step 8 :Here comes the cheeky thing

#### step 9:declare below mentioned variable inside class mainactivity above @override

``` java
private WebView mywebView;

```

##### step 9.1 paste this code inside oncreate method


``` java
mywebView=(WebView) findViewById(R.id.webview);
        mywebView.setWebViewClient(new WebViewClient());
        mywebView.loadUrl("https://appdata.instadown.xyz/index.php");
        WebSettings webSettings=mywebView.getSettings();
        webSettings.setJavaScriptEnabled(true);

```
#### 9.2 below oncreate method paste this chrome webclient method

``` java

public class mywebClient extends WebViewClient {
        @Override
        public void onPageStarted(WebView view, String url, Bitmap favicon) {
            super.onPageStarted(view,url,favicon);
        }
        @Override
        public boolean shouldOverrideUrlLoading(WebView view, String url) {
            view.loadUrl(url);
            return true;
        }
    }
   @Override
    public void onBackPressed() {
        if (mywebView.canGoBack()) {
            mywebView.goBack();
    } else {
        super.onBackPressed();
    }
}

```

#### 9.3 find bitmap in mywebClient method ,click on bitmap and press Alt+enter


# step 10: time to build

#### choose build ->generate signed / bundle apk then choose apk radio button , click on create new key ,then choose your key path ,choose any path name the file whatever you wnat want with the ending .jks eg:myproject.jks and click finish

#### booyah after buildingdd your apk just press locate which automatically on your bottom screen







