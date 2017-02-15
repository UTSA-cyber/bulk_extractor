Build Instructions
==================================

Linux build
-----------------

    git clone --recursive https://github.com/nbeebe/sceadan.git

###### Creating the liblinear dependency package
    
    cd <path_to>/sceadan/liblinear
    libtoolize
    autoheader
    aclocal
    autoconf
    automake -a
    ./configure
    make
    make install
    cd ..
    
###### Building sceadan
    
    cd <path_to>/sceadan
    libtoolize
    autoheader
    aclocal
    autoconf
    automake -a
    ./configure
    make
    make install
		
###### Building bulk_extractor with sceadan as a plugin
    
    git clone --recursive https://github.com/simsong/bulk_extractor.git
    cd bulk_extractor
    libtoolize
    autoheader -f
    aclocal -I m4
    autoconf -f
    libtoolize
    automake --add-missing --copy
    ./configure --with-sceadan=<sceadan directory>
    make
	sudo make install

Windows 64-bit build
-----------------

    git clone --recursive https://github.com/nbeebe/sceadan.git

###### Creating the liblinear dependency package
    
    cd <path_to>/sceadan/liblinear
    libtoolize
    autoheader
    aclocal
    autoconf
    automake -a
    mingw64-configure
    make

###### Building sceadan
    
    cd <path_to>/sceadan
    libtoolize
    autoheader -f
    aclocal -I m4
    autoconf -f
    libtoolize
    automake --add-missing --copy
    mingw64-configure
    make

###### bulk_extractor
    
    git clone --recursive https://github.com/simsong/bulk_extractor.git
    cd bulk_extractor
    libtoolize
    autoheader -f
    aclocal -I m4
    autoconf -f
    libtoolize
    automake --add-missing --copy
    mingw64-configure --with-sceadan=<sceadan directory> --disable-afflib --disable-libewf
    make

Tips for recompiling
---------------------

If you use the make file generated from CONFIGURE\_F20.bash, it will blow away everything with `make distclean` every time you build bulk extractor!

Re-build sceadan the smarter way if making dev changes to it or bulk_extractor:

    cd ../sceadan; make clean; mingw64-configure; make
    cd /home/deflogix/bulk_extractor; make distclean (to clean stuff up)
    cd win64; mingw64-configure --with-sceadan=../../sceadan --disable-afflib --disable-libewf

To test an updated sceadan in bulk extractor, go to the sceadan source dir (sceadan/src/\*.cpp), make a change, and type `make`. It should only rebuild the modified files. However, to relink the new sceadan to bulk extractor, you *need* to delete **bulk_extractor/win64/src/scan_sceadan.o**. Then type `make`. You can also update bulk extractor source files and type `make` in this directory to rebuild bulk extractor with the new changes.

Running bulk extractor
----------------------

The basic syntax for running bulk extractor with sceadan on both Windows and Linux is:

`bulk_extractor -E sceadan -S sceadan_model_file=<model file location> -o <log file location> <disk image location>`

---

For more information on installing packages and building bulk_extractor, read the wiki page here:
https://github.com/simsong/bulk_extractor/wiki/Installing-bulk_extractor

To download the Windows installer and/or other releases of bulk_extractor, visit the downloads page here:
http://digitalcorpora.org/downloads/bulk_extractor

For more information on bulk_extractor, visit: http://www.forensicswiki.org/wiki/Bulk_extractor
