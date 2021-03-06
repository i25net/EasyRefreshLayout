# EasyRefreshLayout
Inherited This library allows you to easily achieve the drop-down refresh and upload more 

## Recommended 
* Recommended in conjunction with [BaseRecyclerViewAdapterHelper](http://www.recyclerview.org)


# How to use

## Step one
* You need to add jitpack repository infomaition to build.gradle in your project.

``` 
// Top-level build file where you can add configuration options common to all sub-projects/modules.

buildscript {
    repositories {
        jcenter()
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:2.2.0'

        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
    }
}

allprojects {
    repositories {
        jcenter()
        maven { url "https://jitpack.io" }

    }
}

task clean(type: Delete) {
    delete rootProject.buildDir
}

```
## step two
* You need to add library dependencies infomation to build.gradle in your module. 

``` 
 compile 'com.github.anzaizai:EasyRefreshLayout:1.0.8'
```
* last releases version is 1.0.9 can be use

## step three

* Use EasyRefreshLayout as the top-level root layout the needs to be added pull-down refresh or pull-up loading more the funcation views.

###such as:

```

    <com.ajguan.library.EasyRefreshLayout
        android:id="@+id/easylayout"
        android:layout_width="match_parent"
        android:layout_height="match_parent">

        <android.support.v7.widget.RecyclerView
            android:id="@+id/recyclerview"
            android:layout_width="match_parent"
            android:layout_height="match_parent" />
    </com.ajguan.library.EasyRefreshLayout>
    
```
* add pull-down refresh funcation

```
 easyRefreshLayout.setRefreshListener(new EasyRefreshLayout.OnRefreshListener() {
            @Override
            public void onRefreshing() {
                new Handler().postDelayed(new Runnable() {
                    @Override
                    public void run() {
                        easyRefreshLayout.refreshComplete();
                        Toast.makeText(getApplicationContext(), "refresh success", Toast.LENGTH_SHORT).show();                    }
                },3000);

            }
        });
```

* add pull-up loading funcation 

```
easyRefreshLayout.initLoadMore(
                new EasyRefreshLayout.LoadMoreEvent() {
                    @Override
                    public void onLoadMore() {
                        new Handler().postDelayed(new Runnable() {
                            @Override
                            public void run() {
                                final List<String> list = new ArrayList<>();
                                for (int i = 0; i < 5; i++) {
                                    list.add("EasyRefreshLayout new index :" + i);
                                }
                                easyRefreshLayout.loadMoreComplete(new EasyRefreshLayout.Event() {
                                    @Override
                                    public void complete() {
                                        adapter.getData().addAll(list);
                                        adapter.notifyDataSetChanged();
                                    }
                                }, 1000);
                            }
                        }, 2000);
                    }   
                }
        );
```

* if you need only pull-down refresh funcation

```
easyRefreshLayout.setEnableLoadMore(false);

```

* if you need only pull-up loading funcation

```
easyRefreshLayout.setEnablePullToRefresh(false);
```
## step four 

### Customizable pull-down refresh head view 

* You only need to create a view to implement the RefreshVIew interface
* Set the custom view to Easy RefreshLayout

```
easyRefreshLayout.setRefreshHeadView(customizabaleView);

```

### Customizable pull-up load footer view 

* You only need to create a view to implement the ILoadMoreView interface
* Set the custom view to Easy RefreshLayout

```
easyRefreshLayout.setLoadMoreView(customizabaleView);

```

for more information on how to use it，see demo on github [https://github.com/anzaizai/EasyRefreshLayout](https://github.com/anzaizai/EasyRefreshLayout)

# References

* Part of the content from the blog [http://www.2cto.com/kf/201606/518620.html](http://www.2cto.com/kf/201606/518620.html)

## Very grateful to the contribution of bloggers

