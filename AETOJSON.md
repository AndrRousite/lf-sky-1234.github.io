### AE制作json文件格式动画以及lottie开源库的使用 

[install]:img/20170223094951571.png
[run]:img/20170223095115165.png
[success]:img/20170223095315657.png
[do]:img/20170223100258029.png
[render]:img/20170223100639141.png
[publish]:img/20170223101422113.png


手机应用上有很多地方需要用到动画的地方，比如启动页面欢迎界面等，有些动画比如简单的伸缩旋转等我们可以用属性动画来制作，但是涉及到一些复杂的不规则的动画我们要实现起来就很麻烦，但是利用lottie加载json格式文件就简单的很多了。json格式文件的动画是利用AE工具制作然后通过插件bodymovin转换成json格式。
先附上资源，亲测可用。

AE工具：http://pan.baidu.com/s/1hsJrKCs，里面有AE cc 2015，据说只有cc2015才可以用bodymovin插件。还有一个Adobe_pojie.exe文件，它是破解工具，找到相应版本，然后将安装文件里面的dll文件替换即可。还有一个文件夹是ExManCmd_win，它是安装插件bodymovin所需要的（已经将bodymovin文件放在里面，不需要从github上下载https://github.com/bodymovin/bodymovin）。

Lottie开源库：https://github.com/airbnb/lottie-android。

1.   安装AE

2.   安装bodymovin插件

管理员权限运行cmd  

cd到ExManCmd_win文件夹位置
![upload][install]  

输入“ ExManCmd.exe /install bodymovin.zxp”回车就完成了
![upload][run]


可以打开AE看到如图所示有bodymovin表示安装插件成功：
![upload][success]

3.   制作动画并转换成json格式文件

具体AE制作动画就不介绍了，我制作了一个简单的动画：  
![upload][do]

制作完成了之后点击 窗口--->扩展-->bodymovin 出现弹窗：  
![upload][render]

可以点击右侧更改导出文件路径，点击RENDER生成json格式文件。

4.    通过lottie开源库加载动画

将生成的json格式文件放入assets目录中，  
通过xml ：  
[html] view plain copy  
在CODE上查看代码片派生到我的代码片

    <?xml version="1.0" encoding="utf-8"?>  
    <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"  
        xmlns:app="http://schemas.android.com/apk/res-auto"  
        android:orientation="vertical"  
        android:layout_width="match_parent"  
        android:layout_height="match_parent">  
    <com.airbnb.lottie.LottieAnimationView  
        android:layout_width="wrap_content"  
        android:layout_height="wrap_content"  
        app:lottie_fileName="data.json"  
        app:lottie_autoPlay="true"  
        app:lottie_loop="true"  
        />  
    </LinearLayout>  

通过代码：   
[java] view plain copy  
在CODE上查看代码片派生到我的代码片

    LottieAnimationView animationView = (LottieAnimationView) findViewById(R.id.animation_view);  
    animationView.setAnimation("data.json");  
    animationView.loop(true);  

 生成的动画效果：
![upload][publish] 

