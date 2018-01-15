# flexinvert
    you can visit at http://flexinvert.nilu.no/flexinvert.html
    它的安装主要依赖于netcdf和lapack,而本测试主要用lapack-3.8.0.tar进行安装
## lapack安装步骤
    主要借鉴于http://blog.csdn.net/mlnotes/article/details/9676269
    a.首先cp make.inc.example make.inc
    b.编译blas， 进入BLAS文件夹，执行以下几条命令
        make
    c.编译cblas， 进入CBLAS文件夹
        make
    d.编译lapack以及lapacke
        进入lapacke  make
        进入主目录   make
## flexinvert 安装
    参考自己的Makefile
## FLEXPART
    http://mp.weixin.qq.com/s/lg7ZNBqZXYfKSgCVLUmagw  安装说明
    https://www.flexpart.eu/wiki/FpLimitedareaWrf     官网说明
    
    下载完后解压，你会得到一个存放了.f90文件的源代码文件夹。通常情况下只需要使用makefile编译就好。可是！FLEXPART有几个超级坑爹的地方：
    首先，为了提高运算效率，提前分配好内存空间，FLEXPART中变量的维数并不能通过namelist进行修改，而是直接在编译前通过修改源代码而实现！！所以请打开par_mod.f90文件，并找到126行，修改之后作为输入场的WRF模式维度信息：
    
    其次，要修改的不仅仅是par_mod.f90，还有一个叫做includepar的文件。这个没有后缀名的东西其实是FLEXPART fortran代码的include文件，里面同样包含了变量的维度信息，而且还包含了模式输出的坐标信息。通过修改：
    integer iomode_xycoord_latlon, iomode_xycoord_meters
    parameter (iomode_xycoord_latlon=0, iomode_xycoord_meters=1)
    integer iomode_xycoord
    !parameter (iomode_xycoord=iomode_xycoord_latlon) ! use this for x,y in/out as lat/lon
    !parameter (iomode_xycoord=iomode_xycoord_meters) ! use this for x,y in/out as meters
    
