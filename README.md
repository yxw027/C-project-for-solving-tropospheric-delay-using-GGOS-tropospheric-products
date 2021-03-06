# C project for solving tropospheric delay using GGOS tropospheric products
 项目作者：田睿 本科毕业于北京航空航天大学，现在读研，GNSS领域入门两年。
 请注意！
 该项目原始路径为：E:\Thesis\RTKLIB_Workspace\WorkSpace\For_Thesis\For_Thesis
 项目名称为For_Thesis(即上传的文件夹中包含的内容)
 在笔者Win10系统、VS2017上成功运行，亲测可用！！！
 请务必仔细阅读此文件！！！
  ==============程序主要功能==============
  本程序的主要功能是基于GGOS对流层产品进行对流层延迟解算，还可用于rtklib开源项目的二次开发及改进。 总之，该程序的目的是方便其他使用rtklib开源项目的GNSS研究者，提高其科研效率。
  ==============程序基本信息==============
  本程序基于rtklib2.4.3 b33版本进行二次开发，采用C语言编写，并在Win10、Visual Studio 2017平台上完成开发及调试，项目路径为： ‪E:\Thesis\RTKLIB_Workspace\WorkSpace\For_Thesis\For_Thesis 相比于原项目，主要改动点为：
  1.增加了Demo_Tropo.c文件（最主要的改进）。
  2.增加了测试用的main.cpp文件，作为程序入口，应注意！主程序文件必须为cpp文件，不能使用c文件。
  3.在rtklib.h 文件中增加了部分函数的声明。
  4.在Windows系统下，采用VS2017编译rtklib项目会遇到各种问题。对此，对原项目进行了必要的改动， 如增加了unistd.h文件、去掉main函数的rnx2rtkp.c文件等，具体编译方法详见后文。
  5.增加了数据文件orography_ell.txt等，应注意！数据文件必须放在项目目录内，因为主程序中使用的是相对路径。
  ==============Windows下采用Visual Studio IDE的项目编译方法==============
  Windows下常用的C/C++ IDE即Visual Studio，功能丰富全面，适合GNSS研究者使用。 当然，对计算机比较精通的研究者可以采用linux系统，不使用IDE，采用cmake等工具进行编译。事实上，这样做更适合rtklib的二次开发。 然而，对于刚接触GNSS领域的硕/博研究生而言，学习linux系统及cmake等编译工具，无疑会大大拉长学习周期， 耽误宝贵的科研时间，降低科研效率。对此，笔者深有体会！因此，笔者坚持在windows系统下用Visual Studio IDE开发此项目， 遇到的编译问题很多，可参考如下博客解决：
  https://blog.csdn.net/wuwuku123/article/details/100030177
  https://blog.csdn.net/sd28you28/article/details/82911273
  https://blog.csdn.net/zhangtao_heu/article/details/79536427
  https://blog.csdn.net/qq_35363018/article/details/101317869
  https://blog.csdn.net/baixia3551/article/details/101085788?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-4.nonecase&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-4.nonecase https://blog.csdn.net/WalterBrien/article/details/80754215
  此外，笔者在编译过程中还遇到一些没有解决的问题，在此总结发布以飨读者：
  要通过Project——Manage NuGet Packages添加pthread、dirent等
  一定记得切换为64位 注意预编译器添加的是WIN32而非Win32！！！
  预编译器中记得添加
  WIN32
  _DEBUG _CONSOLE
  _CRT_SECURE_NO_WARNINGS
  _WINSOCK_DEPRECATED_NO_WARNINGS
  ENAGLO
  DLL
  主程序必须是.cpp文件！！！
  记得添加unistd.h文件 经上述操作后仍出现：
  unresolved external symbol showmsg等错误
  经测试，发现下述方法可行： 将RTKLIB-rtklib_2.4.3\app\rnx2rtkp文件夹下的rnx2rtkp.c文件放到项目的src文件夹下并加入到工程，并去掉其中的主程序（也可以把这个当做主程序）。
  ==============数据源==============
  所用数据均可在网站https://vmf.geo.tuwien.ac.at/上下载。 应注意！VMFG_FC产品必须注册账户后才能获取，注册方法即通过英文邮件向相关管理人员提出申请，管理人员会通过邮件提供给你一个账户。 ==============开发参考==============
  参考了官方的matlab程序vmf1_grid.m及vmf1_ht.m
  参考了如下文献：
  《GGOS对流层延迟产品精度分析及在PPP中的应用》
  《不同全球对流层天顶延迟产品在中国区域的比较》
  《Troposphere mapping functions for GPS and VLBI from ECMWF operational analysis data》
  《Implementation and testing of the gridded Vienna Mapping Function 1 (VMF1)》
  《Generation and Assessment of VMF1-Type Grids Using North-American Numerical Weather Models》
  《Discussion and recommendations about the height correction for a priori zenith hydrostatic delays derived from ECMWF data》
  还有一些官方网站上提供的资料（请参见官网）
  ==============关于程序结果的一点讨论==============
  经测试，本项目运行结果与官方matlab程序有一定出入，差距在厘米级。 经检查，笔者自认为这并非是编程的问题，而是必然存在的数值计算误差，因为C程序与matlab程序的数值精度不同。 笔者测试的结果是本程序更接近IGS发布的天顶对流层延迟数据。 也可采用C与matlab联合编程应用GGOS产品，但运行较慢，且移植性不好。 如有发现程序中问题的，欢迎在GitHub库上及时发布新版本。
  ==============重要声明==============
  鉴于笔者入门不久，水平有限，有所疏漏在所难免。 该项目仅供研究者参考，并非TU Wien发布的官方代码，可能存在笔者尚未发现的未知错误。 如各位研究者发现问题，欢迎在GitHub上发布修正版本。非常欢迎各位研究者对本项目查漏补缺，系统测试！ 在该项目尚未成熟之前，建议各位研究者审慎地考虑在科研中到底是应用本项目，还是使用C与matlab联合编程，后者虽慢，但毕竟是官方反复验证过的matlab代码。 当然，该项目注释详尽，参考价值较高，可作为学习GGOS产品应用的重要参考！ 在此开源发布，权作抛砖引玉，期冀各位研究者对其进一步改进与完善！
