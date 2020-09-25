# Eclipse SWT： Shell - Style和模态设置

## 在Dialog中的修改方法：

Dialog打开后的显示方式主要跟Dialog的parant Shell的style的设置有关，但style的设置参数仅仅是HINT，也就是说这些个设置不一定有效（上下文设置/操作系统）。
在Dialog的构造方法中重写：setShellStyle(SWT.DIALOG_TRIM | SWT.MODELESS); 可以修改shell的style。	

## 在Shell初始化时修改方法

参考：https://www.cnblogs.com/pfxiong/articles/3581224.html
Shell dialogShell = new Shell(topShell, SWT.DIALOG_TRIM | SWT.PRIMARY_MODAL);

## Shell有3种模态模式：

PRIMARY_MODAL, 仅针对于父窗口Dialog（Shell）。
APPLICATION_MODAL, 针对当前Display的所有Shell窗口。
SYSTEM_MODAL, 不但包含APPLICATION_MODAL的当前Display，还包括其他应用程序窗口。
  并且，该帮助文档中，还提到，如果当前系统不支持某一种模特style参数，并且在你的代码里已经显式指定了某一style参数，那么SWT系统将自动“升级”或“降级”到系统支持的模态style;。
  功能范围顺序为：PRIMARY_MODAL < APPLICATION_MODAL  < SYSTEM_MODAL
   升级， PRIMARY_MODAL ---> APPLICATION_MODAL
   降级， SYSTEM_MODAL   --->  APPLICATION_MODAL
Shell有1种非模态模式：
MODELESS， 和上面提到的三种模态模式（PRIMARY_MODAL， APPLICATION_MODAL， SYSTEM_MODAL）是相互排斥的，不能同时使用。
注意：非模态模式，表示该Shell窗口不会阻止其他Shell内的操作。反之，模态模式则或多或少的阻止一些Shell窗口。

## SWT的style介绍：

参考：http://blog.sina.com.cn/s/blog_67532a0d010110cn.html

BORDER——当只有BORDER的时候，窗口是一个只有细细白色边框的空白窗口，没有title那一圈蓝色的边框，也没有最大化，最小化，关闭。不能resize，不能移动。在任务栏里右键没有反应。
TITLE 窗口包含标题栏
CLOSE——当只有CLOSE的时候，窗口会出现蓝色的边框，并且有title，title上显示的是setText的内容，没有title就算setText指定了内容也无法显示。没有最大化，最小化，可以移动。任务栏里右键可以关闭和移动。不能resize。
MAX——当只有MAX的时候，窗口会出现蓝色的title边框，并且有最大化，最小化和关闭的按钮，但是最小化的按钮不起作用，关闭的按钮有作用。可以移动，不能resize，任务栏里右键可以移动关闭和最大化/还原。
MIN——当只有MIN的时候，情况跟只有MAX差不多，只是最大化的按钮不起作用。
RESIZE——当只有RESIZE存在的时候，窗口没有title，只有BORDER，不能关闭，移动和最大最小化。

SHELL_TRIM——是TITLE，CLOSE，MIN，MAX，RESIZE的组合。
DIALOG_TRIM——是TITLE，CLOSE，BORDER的组合

NO_TRIM——当有NO_TRIM存在的情况下，其他的任何Style都不起作用。窗口是没有边框，连BORDER那样细小的白色边框也没有，没有title的蓝色边框，不能移动，resize和关闭。
ON_TOP——当只有ON_TOP存在的时候，窗口始终在最前端，没有title，窗口只有一圈黑色的细小边框。
TOOL——当只有TOOL存在的时候，窗口外观和ON_TOP一样。只是在任务栏中并没有窗口的存在。API中的解释是，TOOL窗口是被用来作为一个工具栏使用的。

MODELESS——当只有MODELESS存在的时候，窗口外观和APPLICATION_MODAL一样，API中没有任何说明，只知道这个参数value是0。
APPLICATION_MODAL——当只有APPLICATION_MODAL存在时，窗口外观和ON_TOP，TOOL一样，只是不是始终在最前端，也在任务栏里有窗口。API中说 used by Dialog。
PRIMARY_MODAL——当只有PRIMARY_MODAL存在的时候，窗口的外观和APPLICATION_MODAL一样，API中也说used by Dialog。
SYSTEM_MODAL——和PRIMARY_MODAL一样。
注意，APPLICATION_MODAL、MODELESS、PRIMARY_MODAL、SYSTEM_MODAL只能指定一种。

> **官方 org.eclipse.swt.widgets.Shell**
> Instances of this class represent the "windows" which the desktop or "window manager" is managing. 
> Instances that do not have a parent (that is, they are built using the constructor, which takes a Display as the argument) are described as top level shells. 
> Instances that do have a parent are described as secondary or dialog shells. 
>
> Instances are always displayed in one of the maximized, minimized or normal states: 
> • When an instance is marked as maximized, the window manager will typically resize it to fill the entire visible area of the display, and the instance is usually put in a state where it can not be resized (even if it has style RESIZE) until it is no longer maximized. 
> • When an instance is in the normal state (neither maximized or minimized), its appearance is controlled by the style constants which were specified when it was created and the restrictions of the window manager (see below). 
> • When an instance has been marked as minimized, its contents (client area) will usually not be visible, and depending on the window manager, it may be "iconified" (that is, replaced on the desktop by a small simplified representation of itself), relocated to a distinguished area of the screen, or hidden. Combinations of these changes are also possible. 
>
>
> The modality of an instance may be specified using style bits. The modality style bits are used to determine whether input is blocked for other shells on the display. 
> The PRIMARY_MODAL style allows an instance to block input to its parent. 
> The APPLICATION_MODAL style allows an instance to block input to every other shell in the display. 
> The SYSTEM_MODAL style allows an instance to block input to all shells, including shells belonging to different applications. 
>
> Note: The styles supported by this class are treated as HINTs, since the window manager for the desktop on which the instance is visible has ultimate control over the appearance and behavior of decorations and modality. For example, some window managers only support resizable windows and will always assume the RESIZE style, even if it is not set. In addition, if a modality style is not supported, it is "upgraded" to a more restrictive modality style that is supported. For example, if PRIMARY_MODAL is not supported, it would be upgraded to APPLICATION_MODAL. A modality style may also be "downgraded" to a less restrictive style. For example, most operating systems no longer support SYSTEM_MODAL because it can freeze up the desktop, so this is typically downgraded to APPLICATION_MODAL. 
> Styles:BORDER, CLOSE, MIN, MAX, NO_MOVE, NO_TRIM, RESIZE, TITLE, ON_TOP, TOOL, SHEET, APPLICATION_MODAL, MODELESS, PRIMARY_MODAL, SYSTEM_MODAL
> Events:Activate, Close, Deactivate, Deiconify, 
> IconifyClass SWT provides two "convenience constants" for the most commonly required style combinations: 
> 	SHELL_TRIM: the result of combining the constants which are required to produce a typical application top level shell: (that is, CLOSE | TITLE | MIN | MAX | RESIZE) 
> 	DIALOG_TRIM: the result of combining the constants which are required to produce a typical application dialog shell: (that is, TITLE | CLOSE | BORDER) 
>
> Note: Only one of the styles APPLICATION_MODAL, MODELESS, PRIMARY_MODAL and SYSTEM_MODAL may be specified. 
>
> IMPORTANT: This class is not intended to be subclassed. 
> See Also:DecorationsSWTShell snippetsSWT Example: ControlExampleSample code and further information@noextendThis class is not intended to be subclassed by clients.