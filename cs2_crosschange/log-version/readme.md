建议使用.txt打开

这个项目来源于我自己在打游戏的困难，不想依赖cs2的code来进行记录我的准心
但是我很长一段时间没有头绪

但是有一天我突然想到了一个办法
（如果你会使用 MySQL也许会有更好的办法）
1、维护准心库
获得数据并保存：
设定一些快捷键来进行后台操作，并且保证此操作不会修改cs2内存和内部文件（如果你想VAC的话）
数据是一堆文本：可以有控制台输出，那么流程就是：
copyq处理剪切板生成文本文件>>py脚本执行该文本文件>>autohotkey设置Windows全局快捷键>>生成“数据库文件”但实际上是一个指令库文本文件
2、调用准心库
每次打开游戏前保证自己使用的是最新的指令库文本文件



具体看还可以改进的部分：
>copyq脚本优化；
>py脚本的自动执行和异常识别；
>ahk的异常弹窗和终止处理
>关于多个快捷键的合并使用顺序，可以减少快捷键位
>指令集合循环的其他写法（已经极限卡字符数了）

======================================================================
作者尽力了，做了3天做的，虽然技术力不高，但很多东西之前没学过，做到在哪一步学到哪一步，周末到了姐姐搬进的新房子喝搬屋酒

1、关于字符串输入问题：剪切板
1.1关于copyq和ditto以及copyq脚本：
JS，但是特殊版本，有点难受
可以用py脚本进行交互，但我没学会
1.2关于其中的bug
对于保留的条目，再进行复制是无法直接激活从而快捷键选中

2、关于bind不能进行嵌套：并加载第一级别cfg，保留第二级别cfg提醒

3、关于alias无法加载超过512个字符的问题{由于简单的准心参数不是指令，所以无法定义别名去减少字符数解决}：
下面是关于准心设置的全部参数
cl_crosshair_drawoutline;
cl_crosshair_dynamic_maxdist_splitratio;
cl_crosshair_dynamic_splitalpha_innermod;
cl_crosshair_dynamic_splitalpha_outermod;
cl_crosshair_dynamic_splitdist;
cl_crosshair_friendly_warning;
cl_crosshair_outlinethickness;
cl_crosshair_sniper_show_normal_inaccuracy;
cl_crosshair_sniper_width;
cl_crosshair_t;
cl_crosshairalpha;
cl_crosshaircolor;
cl_crosshaircolor_b;
cl_crosshaircolor_g;
cl_crosshaircolor_r;
cl_crosshairdot;
cl_crosshairgap;
cl_crosshairgap_useweaponvalue;
cl_crosshairsize;
cl_crosshairstyle;
cl_crosshairthickness;
cl_crosshairusealpha;
进行以下处理{
3.1预设定：
cl_crosshair_drawoutline = false; （看个人：是否保存带黑边准心）
cl_crosshair_t = false; （看个人：是否保存T准心）
cl_crosshair_dynamic_maxdist_splitratio;(看个人：是否保存动态准心)
cl_crosshair_dynamic_splitalpha_innermod;
cl_crosshair_dynamic_splitalpha_outermod;
cl_crosshairusealpha = true;（不能保存无显示准心）
cl_crosshairalpha = 255;
cl_crosshaircolor = 4;（默认初始黄色，可修改颜色但不多余使用此参数）
cl_crosshair_sniper_show_normal_inaccuracy;（不修改狙击准心）
cl_crosshair_sniper_width;
}
3.2由于没有完全设置准心参数可能会导致半修改，那么此时所谓的准心代码就对不上号，加上准心代码太长实在不适合做别名，因此别名的方式为：（单字母字符+当前时间进行简单函数运算值），虽然只能保证一般不会重复（怕重复可以自己写一个哈希函数），但在并非恶意脚本大量操作的情况下，应该问题不大


