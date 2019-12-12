# 2019-12-12

### LinearLayout

자식뷰의 배치를 조정하는 ViewComponent

- Orientation 속성

  ![image](https://user-images.githubusercontent.com/52770718/70694289-9975dd80-1d02-11ea-84a9-4bae45835cb4.png)

  **자식 뷰들을 세로로 배치할것인지? 가로로 배치할 것인지?**

  **기본 설정은 가로로 설정되어있음**

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
      xmlns:app="http://schemas.android.com/apk/res-auto"
      xmlns:tools="http://schemas.android.com/tools"
      android:orientation="vertical"
      android:layout_width="match_parent"
      android:layout_height="match_parent"
      tools:context=".MainActivity">
  <!--자식 뷰를 세로로 배치-->
      <TextView
          android:layout_width="100dp"
          android:layout_height="100dp"
          android:background="@color/colorPrimaryDark"/>
      <TextView
          android:layout_width="100dp"
          android:layout_height="100dp"
          android:background="@color/colorPrimary"
          />
      <TextView
          android:layout_width="100dp"
          android:layout_height="100dp"
          android:background="@color/colorAccent"
          />
  </LinearLayout>
  ```

  

- Weight 속성

  ![image](https://user-images.githubusercontent.com/52770718/70694385-cde99980-1d02-11ea-9347-6d038227fceb.png)

  **자식 뷰의 크기를 가중치에 의해서 결정**

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
      android:orientation="horizontal" android:layout_width="match_parent"
      android:layout_height="match_parent">
      <TextView
          android:layout_width="0dp"
          android:layout_weight="2"
          android:layout_height="100dp"
          android:background="@color/colorAccent"
          />
      <TextView
          android:layout_width="0dp"
          android:layout_weight="2"
          android:layout_height="100dp"
          android:background="@color/colorPrimary"
          />
      <TextView
          android:layout_width="0dp"
          android:layout_weight="2"
          android:layout_height="100dp"
          android:background="@color/colorPrimaryDark"
          />
  </LinearLayout>
  ```

  

- Gravity 

  ![image](https://user-images.githubusercontent.com/52770718/70694421-e78ae100-1d02-11ea-950d-9fe9266d86e8.png)

  **자식뷰를 부모의 어떤 방향으로 치우치게 배치할 것인지 결정**

  **Top,Bottom,Center**

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
      android:orientation="vertical" android:layout_width="match_parent"
      android:layout_height="match_parent"
      android:gravity="center_vertical">
  
      <TextView
          android:layout_width="100dp"
          android:layout_height="100dp"
          android:background="@color/colorPrimaryDark"/>
  </LinearLayout>
  ```

### RelativeLayout

**자식뷰의 배치를 조정하는 ViewComponent**

- RelativeLayout 스스로 기준이 됨

  ![image](https://user-images.githubusercontent.com/52770718/70695161-73e9d380-1d04-11ea-8605-5b4809445ad9.png)

  **alignParent~  사용**

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
      xmlns:app="http://schemas.android.com/apk/res-auto"
      xmlns:tools="http://schemas.android.com/tools"
      android:layout_width="match_parent"
      android:layout_height="match_parent"
      tools:context=".MainActivity">
  
      <TextView
          android:layout_width="100dp"
          android:layout_height="100dp"
          android:layout_alignParentRight="true"
          android:background="@color/colorPrimaryDark"/>
      <TextView
          android:layout_width="100dp"
          android:layout_height="100dp"
          android:layout_alignParentBottom="true"
          android:background="@color/colorPrimaryDark"/>
  
      <TextView
          android:layout_width="100dp"
          android:layout_height="100dp"
          android:layout_alignParentTop="true"
          android:background="@color/colorPrimaryDark"/>
      <TextView
          android:layout_width="100dp"
          android:layout_height="100dp"
          android:layout_alignParentRight="true"
          android:layout_alignParentBottom="true"
          android:background="@color/colorPrimaryDark"/>
  
      <TextView
          android:layout_width="100dp"
          android:layout_height="100dp"
          android:layout_centerInParent="true"
          android:background="@color/colorPrimaryDark"/>
  </RelativeLayout>
  ```

  

- RelativeLayout이 새로운기준을 정해서 사용 

  ![image](https://user-images.githubusercontent.com/52770718/70695210-8cf28480-1d04-11ea-9a0f-e68fd06b94c5.png)

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
      android:orientation="vertical" android:layout_width="match_parent"
      android:layout_height="match_parent">
  
      <TextView
          android:id="@+id/gijun"
          android:layout_width="100dp"
          android:layout_height="100dp"
          android:background="@color/colorPrimaryDark"
          android:layout_centerInParent="true"/>
      <TextView
          android:layout_toRightOf="@+id/gijun"
          android:layout_width="100dp"
          android:layout_height="100dp"
          android:background="@color/colorAccent"/>
      <TextView
          android:layout_width="100dp"
          android:layout_height="100dp"
          android:background="@color/colorAccent"
          android:layout_toLeftOf="@+id/gijun"/>
      <TextView
          android:layout_width="100dp"
          android:layout_height="100dp"
          android:background="@color/colorAccent"
          android:layout_above="@+id/gijun"/>
      <TextView
          android:layout_width="100dp"
          android:layout_height="100dp"
          android:background="@color/colorAccent"
          android:layout_below="@+id/gijun"/>
      <TextView
          android:layout_width="100dp"
          android:layout_height="100dp"
          android:layout_centerInParent="true"
          android:background="@color/colorAccent"
          android:layout_above="@+id/gijun"/>
  </RelativeLayout>
  ```

  

### FrameLayout

**뷰컴포넌트들을 겹처 보이고 싶을때**

```xml
<?xml version="1.0" encoding="utf-8"?>
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:background="@color/colorAccent"/>
    <LinearLayout
        android:layout_width="300dp"
        android:layout_height="300dp"
        android:background="@color/colorPrimaryDark"/>
    <LinearLayout
        android:layout_width="200dp"
        android:layout_height="200dp"
        android:background="@color/colorPrimary"/>

</FrameLayout>
```



- gravity 속성

  ![image](https://user-images.githubusercontent.com/52770718/70701276-6e45bb00-1d0f-11ea-80d5-a1de2e1e0467.png)

```xml
<?xml version="1.0" encoding="utf-8"?>
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical" android:layout_width="match_parent"
    android:layout_height="match_parent">

    <TextView
        android:layout_width="100dp"
        android:layout_height="100dp"
        android:layout_gravity="left|top"
        android:background="@color/colorPrimary"></TextView>
    <TextView
        android:layout_width="100dp"
        android:layout_height="100dp"
        android:background="@color/colorPrimary"
        android:layout_gravity="center|top"></TextView>
    <TextView
        android:layout_width="100dp"
        android:layout_height="100dp"
        android:background="@color/colorPrimary"
        android:layout_gravity="right|top"></TextView>
    <TextView
        android:layout_width="100dp"
        android:layout_height="100dp"
        android:background="@color/colorPrimary"
        android:layout_gravity="center|left"></TextView>
    <TextView
        android:layout_width="100dp"
        android:layout_height="100dp"
        android:background="@color/colorPrimary"
        android:layout_gravity="center"></TextView>
    <TextView
        android:layout_width="100dp"
        android:layout_height="100dp"
        android:background="@color/colorPrimary"
        android:layout_gravity="center|right"></TextView>
    <TextView
        android:layout_width="100dp"
        android:layout_height="100dp"
        android:background="@color/colorPrimary"
        android:layout_gravity="bottom|left"></TextView>
    <TextView
        android:layout_width="100dp"
        android:layout_height="100dp"
        android:background="@color/colorPrimary"
        android:layout_gravity="bottom|center"></TextView>
    <TextView
        android:layout_width="100dp"
        android:layout_height="100dp"
        android:background="@color/colorPrimary"
        android:layout_gravity="right|bottom"></TextView>
</FrameLayout>
```

