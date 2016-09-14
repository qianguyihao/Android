



## few 

view控件id的命名：
    


## strings.xml，colors.xml等中id的命名

命名规则：`activity名称_功能模块名称_逻辑名称`。
注：strings.xml中，使用activity名称注释，将文件内容区分开来。

## layout中id的命名规则

命名规则：`view的缩写_模块名称_view的逻辑名称`。

### view的缩写详情如下

| 控件 | 缩写 | 备注 |
|:-------------|:-------------:|:-----:|
| LayoutView | lv | 备注 |
| RelativeView | rv | 备注 |
| TextView | tv |  |
| Button | btn |  |
| ImageButton | imgBtn |  |
| ImageView | imgView 或则 iv |  |
| CheckBox | 缩写 |  |
| RadioButton | anaClk |  |
| DigtalClock | dgtClk |  |
| DatePicker | dtPk |  |
| EditText | edtTxt |  |
| 控件 | 缩写 |  |
| 控件 | 缩写 |  |
| 控件 | 缩写 |  |
| 控件 | 缩写 |  |
| 控件 | 缩写 |  |
| 控件 | 缩写 |  |
| 控件 | 缩写 |  |
| 控件 | 缩写 |  |

        

         

           

        

        

        

         

           

TimePicker         
tmPk
toggleButton       
tglBtn
ProgressBar 
proBar
SeekBar                            
skBar
AutoCompleteTextView
autoTxt
ZoomControls       
zmCtl
VideoView          
vdoVi
WdbView            
webVi
RantingBar         
ratBar
Tab                
tab
Spinner            
spn
Chronometer        
cmt
ScollView          
sclVi
TextSwitch         
txtSwt
ImageSwitch        
imgSwt
listView           
lVi 或则lv
ExpandableList     
epdLt
MapView            
mapVi






activity中的view变量命名：
命名模式为：逻辑名称+view缩写。
建议：如果layout文件很复杂，建议将layout分成多个模块，每个模块定义一个moduleViewHolder，其成员变量包含所属view。





参考链接：
【荐】Android 命名规范 （提高代码可以读性）：http://blog.csdn.net/vipzjyno1/article/details/23542617
Android编码命名规范：http://www.jianshu.com/p/bb4f5033e573
Android 编码规范：http://www.jianshu.com/p/0a984f999592
Android 编码规范文档合辑：https://github.com/oyjt/Android-Code-Style
【荐】Android命名规范：http://cursonjiang.github.io/2015/03/30/Android%E5%91%BD%E5%90%8D%E8%A7%84%E8%8C%83/

