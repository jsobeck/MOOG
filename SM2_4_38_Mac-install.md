# How to install sm2_4_38 on Mac High Sierra OS
- Use specialized version of gcc (install via brew install gcc command; gcc base install location: /usr/local/Cellar/gcc/)
- Download and install X11/X11R6 libraries and associated materials (Xcode,...)
- Make sure all $PATH specifications are correct and include directories such /usr/local,...
- With aprropriate permissions, download the gzipped tarfile for SM (filename: sm2_4_38.tar.gz)
- Move tarfile to /usr/local directory
- Unzip and untar file
- Execute set_opts code (chmod/sudo for necessary permissions)
- Open sm2_4_38/Makefile in a text editor and alter the C compiler/flag information as follows:

  `CC = /usr/local/Cellar/gcc/8.2.0/bin/gcc-8 -fopenmp -Wall -DmacOSX -DNEED_SWAP -I/usr/X11/include`
  
  (note above depends on currently installed gcc version)
- Open sm2_4_38/src/Makefile in a text editor and verify that the X11 library is given as follows:

  `XLIB11 = -L/usr/X11R6/lib -lX11`
  
- Open src/readcol.c in a text editor and modify the file in the following way:
  above the line where #include <studio.h> is written, insert 
  
      #undef _POSIX_C_SOURCE
      #define _POSIX_C_SOURCE 200112L
      
- Open src/devices/ttyopen.c in a text editor and alter the file in the following way:   
  above the line where #include <studio.h> is written, insert

      #undef _POSIX_C_SOURCE
      #define _POSIX_C_SOURCE 200112L
      
- Run `$make` and `$make install` (sudo permissions enabled)
- Compilation should occur with no fatal errors
(for the recommendation to do text additions to the files readcol.c and ttyopen.c, a h/t is given to jtmyles [bi-jmyles.blogspot.com])
