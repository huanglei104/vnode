    手动启动X server : X :dislay ，display是一个任意指定的数字，一个display就代表了一个X server。 display是给x client使用的， 当启动x client的时候 ，需要使用-display参数来指定显示在哪个X上。没有指定display的时候，它的默认值就是0。
如果需要指定X显示在哪个虚拟终端上，使用vtn,n就是虚拟终端的号 ,默认是第一个可用的虚拟终端

X server只能本地的机器上启动，所以并没有hostname参数。hostname参数是给x client需要连接时使用的 client hostname:display.screen  



显卡主要由三类设备组成：GPU, LCDC，硬件视频加速(显示接口HDMI/eDP等)

视频采集卡是输入设备，显卡：输出设备， USB摄像头是输入设备。USB摄像头有视频采集卡的功能，但更专业的场合还是需要用视频采集卡。

硬件加速：将原本由CPU来完成的任务交由其他硬件来完成，减轻CPU的负担。两个必要的条件：硬件本身支持/内核提供相应的接口(DRI)

     渲染(rendering)指将在内存中生成UI所需要的数据，包括2D渲染，3D渲染，图片/视频解码，字体渲染等。 3D渲染和视频解码的数据量和计算量比较大，
所以通常都采用硬件加速。一般的渲染都是指3D渲染。

OpenGL是一套3D渲染的API,之所以能够跨平台，是因为OpenGL仅仅是一套规范。当然，OpenGL也能够处理2D渲染。

     OpenGL只是完成了UI的渲染，但最终还是要显示在一个窗口上，所以OpenGL通过glx(X的一部分)与xerver通信，完成窗口的显示。（xserver是通过用户空间的驱动与kernel通信的，由kernel访问硬件）。
为了实现最优的性能，让3D渲染直接访问硬件，内核就提供了DRI接口(对应用户空间的libdrm)。
     OpenGL可以用软件实现（mesa），也可以硬件实现(驱动中)。 （https://wenku.baidu.com/view/b2c797a30975f46527d3e1a7.html）


xorg.conf配置文件：man xorg.conf
Device section描述一个显卡，Monitor section描述一个显示器，Screen section 绑定一个 Device和 Monitor，InputDevice section描述一个输入设备，ServerLayout section绑定一个 InputDevice 和 
一个 Screen。 ServerLayout section 是最高级的。


Xorg 启动的时候， 需要指定vt参数， 如果没有指定则会使用第一个可用的vt。而启动时的display参数实际是给client用的，可以任意指定(只要没有被使用)，client连接的时候的display参数只要和xorg的一样就能连接上。
(相当于将vt转换成了display)