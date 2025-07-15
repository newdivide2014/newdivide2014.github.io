# Qt程序在多屏下显示不全的问题


### 问题描述
发布的qt程序在多屏幕机器上显示不全。

反复调试了好久，发现在只有一块显示屏中程序显示正常。但是在同事的外接了一块显示屏下运行程序时，程序总是不在屏幕中间，而是只显示了一半，每次启动程序位置都是有一半不在屏幕内，还需要拖动。对于用户的使用不友好...

原始测试代码段：
```c
int main(int argc, char *argv[])
{
    QApplication a(argc, argv);
    MainWidget w;
    w.move((a.desktop()->width()-w.width())/2,((a.desktop()->height()-w.height())/2));
    w.show();
    return a.exec();
}
```
> 帮助文档内容：
However, for desktops with multiple screens, the size of the desktop is the union of all the screen sizes, so width() and height() should not be used for computing the size of a widget to be placed on one of the screens.

原来这位置是用像素大小来计算的，单屏幕上也并没有什么问题，但是在多屏下就有问题了，因为多屏下的像素是所有屏幕加起来，所以用上面的方法，程序界面位置是不可预料。

### 解决办法

```c
int main(int argc, char *argv[])
{
    QApplication a(argc, argv);
    MainWidget w;
    //程序所在的屏幕编号
    int currentScreen = a.desktop()->screenNumber(&w);
    //程序所在屏幕尺寸
    QRect rect = a.desktop()->screenGeometry(currentScreen);
    //移动到所在屏幕中间
    w.move((rect.width() - w.width()) / 2, (rect.height() - w.height()) / 2);
    w.show();
    return a.exec();
}
```



---

> : 蓝红柿  
> URL: https://newdivide2014.github.io/posts/qt-ui-center-show/  

