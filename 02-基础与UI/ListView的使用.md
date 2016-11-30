









## ListView的模板写法


**ListView模板写法的完整代码：**

- [android代码优化----ListView中自定义adapter的封装（ListView的模板写法）](http://www.cnblogs.com/smyhvae/p/4477079.html)

以后每写一个ListView，就这么做：直接导入**ViewHolder.java**和**ListViewAdapter**，然后写一个自定义adapter继承自ListViewAdapter就行了。

<br>


## ListView中动态显示和隐藏Header&Footer

备注：本段内容在如下链接中可查看更完整的介绍：

如果需要动态的显示和隐藏footer的话，按照惯例，误以为直接通过setVisibility中的View.GONE就可以实现。但是在实际使用中发现并不是这样的。

例如，先加载footer布局：

```java
private View mFooter;

mFooter = LayoutInflater.from(this).inflate(R.layout.footer, null);  //加载footer的布局
mListView.addFooterView(mFooter);

```

如果想动态隐藏这个footer，惯性思维是直接设置footer为gone：（其实这样做是不对的）

```java
mFooter.setVisibility(View.GONE);  //隐藏footer
```

实际上，直接设置GONE后，虽然元素是隐藏了，但是还是占用着那个区域，此时和View.INVISIBILE效果一样。

**footer的正确使用方法如下：**

**1、方法一：**


（1）布局文件：在footer布局文件的最外层再套一层LinearLayout/RelativeLayout，我们称为footerParent。

layout_footer_listview.xml:（完整版代码）

```xml
<?xml version="1.0" encoding="utf-8"?>

<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/mFooterparent"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:background="#FFFFFF"
    android:gravity="center"
    android:orientation="vertical"
    >

    <LinearLayout
        android:id="@+id/mFooter"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:gravity="center">

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="40dp"
            android:layout_centerVertical="true"
            android:layout_marginLeft="10dp"
            android:gravity="center"
            android:text="查看更多"
            android:textColor="#ff0000"
            android:textSize="20sp"/>
    </LinearLayout>
</LinearLayout>

```


（2）加载footer和footerParent的布局：

```java
private View mFooter; //footer
private View mFooterParent;  //footer的最外面再套一层LinearLayout

mFooterParent = LayoutInflater.from(getActivity()).inflate(R.layout.footerparent_listview, null);//加载footerParent布局
mFooter = mFooterParent.findViewById(R.id.footer);
listView.addFooterView(mFooterParent);  //把footerParent放到ListView当中

mFooterParent.setOnClickListener(MainActivity.this); //绑定监听事件，点击查看全部列表
```

（3）设置footer为gone：(不是设置footerParent为gone)

```java
mFooter.setVisibility(View.GONE);
```


<br>

**2、方法二：**或者直接在代码中为footer添加footerParent也可以，如下：


```java
private View mFooter; //footer
mFooter = LayoutInflater.from(getActivity()).inflate(R.layout.footer_listview, null);//加载footer布局

LinearLayout mFooterParent = new LinearLayout(context);  
mFooterParent.addView(mFooter);//在footer的最外面再套一层LinearLayout（即footerParent）
listView.addFooterView(mFooterParent);//把footerParent放到ListView当中

```

当需要隐藏footer的时候，设置footer为gone：（不是设置footerParent为gone）

```java
mFooter.setVisibility(View.GONE);
```

参考连接：

[如何实现可动态调整隐藏header的listview ](http://blog.sina.com.cn/s/blog_70b9730f01014sgm.html)

[sandroid ListView 设置header和footer的问题](http://my.oschina.net/mugg/blog/157866)















（1）

