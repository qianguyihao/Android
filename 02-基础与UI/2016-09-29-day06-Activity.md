

## Activity之间数据传递

### 方式一：使用Intent 自带的bundle对象

**传递一个字符串：**

（1）在MainActivity.java中发送数据：

```java
Intent intent = new Intent(MainActivity.this, SecondActivity.class);
//在跳转界面的同时，顺便传递数据过去

//传递String型数据
String myName = edtTxt_name.getText().toString();  //姓名
intent.putExtra("name", myName); //方法：public Intent putExtra (String name, String value)

//传递int型数据
int checkId = rg_gender.getCheckedRadioButtonId(); //获取RadioGruop中选中的性别控件id
intent.putExtra("gender", checkId); //方法：public Intent putExtra (String name, int value)

//传递图片
Bitmap bitmap = BitmapFactory.decodeResource(getResources(),r.drawable.logo);
intent.putExtra("bitmap",bitmap); //方法：putExtra(String name,Pacelable value);

startActivity(intent);	
```

14行：Serializable 是java中的序列化。Pacelable 是Android中的序列化。传递bitmap时，会自动被序列化。


（2）在SecondActivity中接收数据：

```java
Intent intent = getIntent();  //Return the intent that started this activity

//获取上一个Activity传递过来的数据
String s = intent.getStringExtra("name");  
int checkId = intent.getIntExtra("gender", 0); //方法：public int getIntExtra (String name, int defaultValue)		
Bitmap bitmap =intent.getParcelableExtra("bitmap");
imageView.setImageBitmap(bitmap);

```


**传递一个对象：**


## 隐式意图

### 显式意图和隐式意图对比

**显式意图：**

- 能从intent上直观得看出跳转到哪一个界面。

- 应用场景：一般是自己内部跳转的时候，用显式意图。效率高。


**隐式意图：**

- 要指定action（动作）、data(数据) 来达到跳转的目的。

- 应用场景：一般是跳转到其他应用中的某个界面，或者自己的应用界面想被其他应用打开。 效率低。


### 启动界面的方式举例


**举例1**：（打开界面的两种方式）

> 现在通过显式意图的方式启动Activity01，通过隐式意图的方式启动Activity02。

（1）清单文件注册：


```xml
        <!-- 显式意图注册 -->
        <activity android:name=".Activity01"></activity>

        
        <!-- 隐式意图注册 -->
        <activity android:name=".Activity02">
            
            <!-- 意图过滤器-->
            <intent-filter>
                <!-- action和 category都必须写上 -->
                <action android:name="com.smyhvae.intentdemo.action.OPEN"/>              
                
                <category android:name="android.intent.category.DEFAULT"/>
            </intent-filter>
            
        </activity>
```


隐式意图的注册过程中：

- `<action>`标签：一般就写`包名 + action + 大写的自定义的动作`，目的就是为了**匹配动作**。

- `<category>`标签：**这个标签一定不能少**。除了主界面是launcher分类之外，其他的界面都是属于default分类。


（2）启动界面：

```java
    //使用显式手法启动 Activity01
    public void click01(View v) {
        Intent intent = new Intent(this, Activity01.class);
        startActivity(intent);
    }

    //使用隐式手法启动Activity02
    public void click02(View v) {
        Intent intent = new Intent();
        //指定跳转到什么动作的界面
        intent.setAction("com.smyhvae.intentdemo.action.OPEN");

        //由于分类是默认的分类，所以可以不用写。
        intent.addCategory("android.intent.category.DEFAULT");

        startActivity(intent);
    }

```


**举例2：跨应启动界面**

> 上面的例1中，IntentDemo分别有三个Activity：默认的MainActivity、 显式注册的Activity01、隐式注册的Activity02。前提是：**只要这些Activity带了`<intent-filter>`标签，就可以被其他应用访问**。所以，MainActivity、Activity02可以被其他应用启动，但是Activity02就不行。

现在我们新建一个应用`IntentDemo2`，在应用`IntentDemo2`中跳转到应用`IntentDemo`中的`Activity02`方式如下。

方式1：

```java
Intent intent = new Intent();
intent.setClassName("com.smyhvae.intentdemo","com.smyhvae.intentdemo.Activity02");
startActivity(intent);
```

方式2：

```java
Intent intent = new Intent();
intent.setAction("com.smyhvae.intentdemo.action.OPENN");
startActivity(intent);
```

备注：如果我们想通过`IntentDemo2`跳转到`IntentDemo`中的`MainActivity`，可以采用方式1，指定具体的包名和类名；但是不能采用方式2，因为很多应用都带有`"android.intent.action.MAIN"`属性，没办法进行准确匹配。










