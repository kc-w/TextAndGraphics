# TextAndGraphics
仿新闻页面文字图片混排页面。只需要简单传值即可动态生成TextView和ImageView,图片可以点击进入查看放大缩小，支持网络图片、本地图片
#使用方式


public class MainActivity extends AppCompatActivity {

    private ScrollView sv_main;
    private String[] mData;//图文列表的数据
    private TextAndGraphicsView mTextAndGraphicsView;//图文控件
    
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        parseData();//解析数据
        initView();//初始化ui
    }

    private void parseData() {
        //根据分割线来把文字和图片地址存入数组中
        mData = DataUtil.getData().split(DataUtil.SPLIT_TAG);
    }

    private void initView() {
        sv_main = (ScrollView) findViewById(R.id.sv_main);
        //只需要把控件，放到ScrollView里面即可
        mTextAndGraphicsView = new TextAndGraphicsView(this,mData);
        sv_main.addView(mTextAndGraphicsView);
    }
}



//主页布局
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/activity_main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context="com.linchuan.textandgraphics.MainActivity">

    <ScrollView
        android:id="@+id/sv_main"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical"
        android:scrollbars="none"/>
</RelativeLayout>

//图文数据的格式
String content = 
 "[#TEXT#]这里是第一段文字"
+"[#SPLIT#]"
+"[#IMAGE_NET#]http://www.picture.com"
+"[#SPLIT#]"
+"[#TEXT#]这里是第二段文字"
+"[#SPLIT#]"
+"[#IMAGE_LOCAL#]file:///android_asset/local_picture2.png";