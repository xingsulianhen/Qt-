# 如何使用Qt Advanced Docking System

## 通过Github将库clone至本地
github网址
https://github.com/githubuser0xFFFF/Qt-Advanced-Docking-System

https方式:
https://github.com/githubuser0xFFFF/Qt-Advanced-Docking-System.git

ssh方式:
git@github.com:githubuser0xFFFF/Qt-Advanced-Docking-System.git

![下载QADS](1.png "下载QADS")

## Mingw方式

### 通过库导入

#### 通过QtCreator编译
1. 打开工程

![打开cmakeList](2.png "打开cmakeList")

![打开cmakeList](3.png "打开cmakeList")

2. 工程配置,只勾选debug和miniRelease两种即可，调试用Debug，发布用MiniRelease，后面的路径默认即可

![工程配置](4.png "工程配置")

3. Debug模式编译

![Debug模式编译](5.png "Debug模式编译")

4. 编译成功

![Debug编译成功](6.png "Debug编译成功")

生成的文件在.\Github\Qt-Advanced-Docking-System\build\Desktop_Qt_6_5_3_MinGW_64_bit-Debug\x64中

一个是bin文件夹下的DLL

![Debug DLL](7.png "Debug DLL")

一个是lib文件夹下的a文件

![Debug a](8.png "Debug a")

5. MiniRelease模式编译

![MiniRelease模式编译](9.png "MiniRelease模式编译")

6. 生成的文件在.\Github\Qt-Advanced-Docking-System\build\Desktop_Qt_6_5_3_MinGW_64_bit-MinSizeRel\x64中

一个是bin文件夹下的DLL

![MiniRelease DLL](10.png "MiniRelease DLL")

一个是lib文件夹下的a文件

![MiniRelease a](11.png "MiniRelease a")

7. 新建文件夹QADS，将src文件夹以及上面生成的库文件复制进去,将debug和MiniRelease的库文件都放入Mingw文件夹中

![生成QADS文件夹](12.png "生成QADS文件夹")

生成的QADS文件夹如下

![生成QADS文件夹](13.png "生成QADS文件夹")

其中Mingw文件夹如下

![生成QADS文件夹](14.png "生成QADS文件夹")

#### 导入库文件

1. 新建cmake工程

![新建cmake工程](16.png "新建cmake工程")

![新建cmake工程](17.png "新建cmake工程")

选择cmake构建

![选择cmake构建](18.png "选择cmake构建")

选择Mingw环境

![选择Mingw环境](19.png "选择Mingw环境")

一路next，新建工程完成

![新建工程完成](20.png "新建工程完成")

![新建工程完成](21.png "新建工程完成")

2. 将之前生成的QADS文件夹复制过来

![QADS文件夹](22.png "QADS文件夹")

3. 修改CMakeList文件，导入QADS库

导入头文件目录以及库文件目录
	```
	set(INC_DIR "${CMAKE_CURRENT_SOURCE_DIR}/QADS/src")
	set(LINK_DIR "${CMAKE_CURRENT_SOURCE_DIR}/QADS/Mingw")
	include_directories(${INC_DIR})
	link_directories(${LINK_DIR})
	```

![导入QADS库](23.png "导入QADS库")

导入目标文件

	```
	target_link_libraries(untitled PRIVATE libqt6advanceddockingd.dll.a libqt6advanceddocking.dll.a)
	```
![导入QADS库](24.png "导入QADS库")

#### 简单使用QADS

1. 在ui文件中添加一个QWidget作为基本容器

![添加QWidget](25.png "添加QWidget")

2. 在MainWindow.cpp中添加头文件
	```C++
	#include <QVBoxLayout>
	#include <QPlainTextEdit>
	#include "QADS/src/DockManager.h"
	```
	
![添加头文件](26.png "添加头文件")

3. 添加两个QPlainText部件
	```C++
	// 创建QAds容器
    QVBoxLayout* Layout = new QVBoxLayout(ui->widget);
    Layout->setContentsMargins(QMargins(0, 0, 0, 0));
    ads::CDockManager *m_DockManager = new ads::CDockManager(ui->widget);
    Layout->addWidget(m_DockManager);
    
    // 创建窗口1
    QPlainTextEdit *log1 = new QPlainTextEdit(this);
    ads::CDockWidget *logDockWidget1 = new ads::CDockWidget(tr("data1"));
    logDockWidget1->setWidget(log1);
    m_DockManager->addDockWidget(ads::TopDockWidgetArea, logDockWidget1);
    
    // 创建窗口2
    QPlainTextEdit *log2 = new QPlainTextEdit(this);
    ads::CDockWidget *logDockWidget2 = new ads::CDockWidget(tr("data2"));
    logDockWidget2->setWidget(log2);
    m_DockManager->addDockWidget(ads::BottomDockWidgetArea, logDockWidget2);
	```

![添加代码](27.png "添加代码")

4. 编译运行

![编译运行](28.png "编译运行")

![运行效果](29.png "运行效果")



