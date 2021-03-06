#多达288中动态效果的侧滑菜单开源库,满足您项目的各种需求
##演示:
##首先是实现效果的总览:
![这里写图片描述](http://img.blog.csdn.net/20160809092650976)
![这里写图片描述](http://img.blog.csdn.net/20160809092700538)
##然后是单独效果的演示:
###位移动画演示:
![这里写图片描述](http://img.blog.csdn.net/20160809093204682)
###缩放动画演示:
![这里写图片描述](http://img.blog.csdn.net/20160809093452510)
###透明度动画演示:
![这里写图片描述](http://img.blog.csdn.net/20160809093611636)
###旋转动画演示:
![这里写图片描述](http://img.blog.csdn.net/20160809094242759)
###全局图片沉浸演示:
![这里写图片描述](http://img.blog.csdn.net/20160809094336154)
###模糊背景演示:
![这里写图片描述](http://img.blog.csdn.net/20160809094426264)
###动态模糊演示:
![这里写图片描述](http://img.blog.csdn.net/20160809094536763)
###反向动态模糊演示
![这里写图片描述](http://img.blog.csdn.net/20160809094648671)
##单一的动画就演示完了,下面演示几组组合动画
![这里写图片描述](http://img.blog.csdn.net/20160809094750719)
![这里写图片描述](http://img.blog.csdn.net/20160809094842236)
###好了,就演示这么多了,因为组合动画太多了,演示不完的
###简单计算一下:
```
(位移动画(3种)*缩放动画(2种)*透明动画(2种)*旋转动画(6种),图片背景效果(4种)=288(种),另外包括缩放,透明度,3D旋转,动态模糊都能设置范围,所以可定制的效果就更多了.

```
###接下来就该介绍一下使用方法:
###用于测试的`Demo`上演示了很多效果,同时动态的显示了当前效果要进行的代码设置方法,同时还包含一些小提示,建议您先下个`Demo`先看看.[Demo下载](http://www.brioal.cn/apks/SwipeMenuDemo.apk)
###`xml`布局文件中的使用方法:
```
<?xml version="1.0" encoding="utf-8"?>
<com.brioal.swipemenu.view.SwipeMenu
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/main_swipemenu"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context="com.brioal.swipemenudemo.MainActivity">

    <include layout="@layout/left_menu"/>

    <include layout="@layout/right_content"/>

</com.brioal.swipemenu.view.SwipeMenu>

```
###布局文件非常简单,包含两个`xml`布局,上边的是菜单布局,下边的是内容布局
###如果是最简单的使用那么这样设置已经足够了,默认的是固定不动的滑动方式
###如果要对滑动的参数和效果进行定制,那么可以看一下资源文件中的设置(都有注释,理解起来不难)
```
<declare-styleable name="SwipeMenu">
        <!--动画的代码-->
        <attr name="sm_type" format="integer"/>
        <!--滑出菜单的范围-->
        <attr name="sm_dragoffset" format="dimension"/>
        <!--滑出菜单距边界的值-->
        <attr name="sm_menuoffset" format="dimension"/>
        <!--滑动开始的缩放值-->
        <attr name="sm_startscale" format="float"/>
        <!--滑动开始的alpha值-->
        <attr name="sm_startalpha" format="float"/>
        <!--滑动开始的3D旋转角度-->
        <attr name="sm_start3dangle" format="integer"/>
    </declare-styleable>
```
###关于动画代码这里解释一下
###为了方便定制动画效果,用一个4位数字来表示不同的动画组合,个位代表的旋转动画效果序号,十位代表透明度动画效果,千位代表缩放动画效果,万位代表位移动画效果,各个位置的起始都是1,有几种动画效果上限就是多少.比如位移动画有三种,则万位的范围就为1~3,其他依次类推.
####注:因为背景,模糊效果会引入多余的组件,所以只在需要的时候添加进去,故不包含在动画代码中,设置方式下面再说.
###再贴一个`xml`属性与代码的实现表格
|代码实现|xml实现|功能|
|--|--|--|
|`setStyleCode(int type)`|sm_type`|设置动画效果代码|
|`setMenuOffset(int menuOffset)`|`sm_menuoffset`|设置拉出菜单距离右边界的距离|
|`setDragWipeOffset(int dragWipeOffset)`|`sm_dragoffset`|设置触发滑动的范围,为0则是全屏|
|`setStartScale(float minScale)`|`sm_startscale`|设置起始缩放|
|`setStartAlpha(float startAlpha)`|`sm_startalpha`|设置起始透明度|
|`setStart3DAngle(int start3DAngle)`|`sm_start3dangle`|设置起始3D旋转角度|
|`setFullColor(Activity activity, int headColor)`|无|设置全局颜色|
|`setBackImage(Activity activity, int backBitmap, int headColor)`|无|设置全局图片背景并沉浸|
|`setBlur(Activity activity, int backBitmap, int headColor, float blur)`|无|设置全局模糊背景并指定模糊程度|
|`setChangedBlur(Activity activity, int backBitmap, int headColor)`|无|设置全局动态模糊(范围默认0~25f)|
|`setReverseChangedBlur(Activity activity, int backBitmap, int headColor)`|无|设置反向动态模糊背景(范围默认0~25f)|
|`setChangedBlur(Activity activity, int backBitmap, int headColor, float startBlur, float endBlur)`|无|设置指定范围的动态模糊|
|`setOnMenuShowingListener(onSwipeProgressListener listener)`|无|设置滑动监听,回调获取菜单隐藏到显示的进度,范围(0~1.0f)|
|`changeAllColor(int color)`|无|改变全局颜色(需要先设置全局颜色)|
|`isMenuShowing()`|无|当前菜单是否显示|
|`showMenu()`|无|显示菜单|
|`hideMenu()`|无|隐藏菜单|
##提供的方法就这么多,也不难理解,这里再说一点注意事项
###1.默认是不设置全局背景或者颜色的,所以如果需要全局颜色沉浸和背景沉浸请做相关设置.两种沉浸都兼容到4.4
###2.全局颜色支持动态更换,全局图片背景不支持,当时想的是应该没有这种需求,当然如果有的话可以跟我反馈我会添加.
###3.旋转动画其实就一个3D旋转效果比较好,其他的都是瞎添的,如果要用的话建议和透明度动画一起使用,可防止卡顿(单独用中心旋转卡顿明显,毕竟绘图的代价摆在那)
##为了方便同学们对效果进行设置,我在演示`Demo`中添加了参数设置显示的效果,就在`RecyclerView`的第一个`Item`,并且是可以动态更改的,当前的效果需要如何设置参数全部在上面显示出来了.
##另外用`RecyclerView`来显示提示的另一个目的是演示滑动冲突的处理,默认的是菜单和内容都是可以处理横向纵向的滑动操作的,只有当滑动在靠近菜单内容交集点的时候才会触发滑动.当然也可以设置全屏滑动和设置触发的范围,具体方法查看上面表格内的方法,这里就不重复了.
##使用介绍就到这里了,下面介绍如何添加依赖库:
##`Android Studio`的话跟其他库一样,在你们`App`的`build.gradle`内的`dependencies`下添加
```
compile 'com.brioal:SwipeMenu:1.0'
```
##或者可以下载`Demo`提取`module`添加
###`Demo`代码已上传`Github`,地址:[SwipeMenuDemo](https://github.com/Brioal/SwipeMenuDemo)
##另外说一点其他的,本人开学大四,喜欢`Android`开发,目前还没有确定的工作,如果您有推荐可以进入我的另外一个博客查看简历:[Brioal`s Blog](http://www.brioal.cn/wordpress/)
##如果觉得我写的东西多多少少有一点可取之处,可以**去`[Github](https://github.com/Brioal/SwipeMenuDemo)`上点个赞**,多的话也能写到简历装一下是吧~~麻烦了
##大部分大学应该是不开`Android`开发的,在这里与所有自学`Android`的同学们共勉~自学不容易啊!!
##另外我建了个qq群,方便交流,欢迎各种大神,新手老手加入,群号码:`375276053`
##差点忘了,本库用到的一些代码片段来自网络,贴一下地址,感谢大神的代码:
###[沉浸状态栏](https://github.com/laobie/StatusBarUtil)
###[教你一分钟实现动态模糊效果](http://mp.weixin.qq.com/s?__biz=MzA5MzI3NjE2MA==&mid=2650236619&idx=1&sn=7f4f97babcad9f62607e544efaf2d86e&scene=23&srcid=0809CmU7E9JVZ0ZIyCvG4nLh#rd)
