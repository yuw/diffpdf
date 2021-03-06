DiffPDF
===========

DiffPDF is used to compare two PDF files.

By default the comparison is of the words on each pair of pages, but
comparing character by character is also supported (e.g., for
logographic languages). And there's also support for comparing the pages
by appearance (for example, if a diagram is changed or if a paragraph is
reformatted, or a font changed). It is also possible to compare
particular pages or page ranges. For example, if there are two versions
of a PDF file, one with pages 1-12 and the other with pages 1-13 because
of an extra page having been added as page 4, they can be compared by
specifying two page ranges, 1-12 for the first and 1-3, 5-13 for the
second. This will make DiffPDF compare pages in the pairs (1, 1), (2,
2), (3, 3), (4, 5), (5, 6), and so on, to (12, 13).

A couple of example PDF files are provided online so that you can try it
out. PDF files can be loaded from the GUI (by pressing the File #1 and
File #2 buttons), or by specifying them on the command line. More
information is available in the program's tooltips and About box.

(If you want a command line tool for comparing PDFs see
http://www.qtrac.eu/comparepdf.html.)

Home page: http://www.qtrac.eu/diffpdf.html

Windows Users
=============

Download the zip file, e.g., diffpdf-1.9.2.zip (where the number will
vary depending on the version). Navigate to the file in Windows Explorer
and use the context menu to choose the Extract All option. It doesn't
matter what folder you extract to, but best to use one specifically for
DiffPDF. The folder will contain diffpdf.exe and may contain some .dll
files too. If there are .dll files, you must not move diffpdf.exe to any
other folder!

Once unzipped you can double-click diffpdf.exe to run it. You might also
like to add a shortcut to it from the desktop or from the start menu.

Ubuntu Users
============

The following packages are required to compile Ubuntu 14.04 LTS:

* debhelper
* qt4-qmake
* libqt4-dev
* qt4-linguist-tools
* libpoppler-qt4-dev
* libpoppler-cpp-dev
* hardening-wrapper

Compiling and Installing DiffPDF (Mac-specific notes are at the end.)
================================

Prerequisites: A C++ compiler, the Qt 4 libraries (I test with Qt 4.7
and Qt 4.8. Earlier Qt's may work although Qt 4.4 and 4.5 will at least
need a compiler with tr1 support), and the Poppler libraries (at least
0.20.1, including Poppler's Qt 4 headers). Linux and BSD users should be
able to get everything through their package management system---and
some distros already include diffpdf so you don't even have to build it.
Mac OS X users can get a compiler by installing Xcode; you'll need to
get Qt and Poppler separately.

1. Unpack the archive file, diffpdf-XXX.tar.gz

    $ tar xvfz diffpdf-XXX.tar.gz

2. Change directory to diffpdf-XXX

    $ cd diffpdf-XXX

3. Run lrelease; on some sytems this might be called lrelease-qt4

    $ lrelease diffpdf.pro

4. Run qmake; on some systems, run qmake-qt4

    $ qmake

5. Run make

    $ make

6. Copy or soft-link the diffpdf executable to somewhere on your PATH
7. Only the executable is needed; all the files that were unpacked or
   generated can be safely deleted.

That's it!

Running DiffPDF
===============

A pair of tiny example files are available:
http://www.qtrac.eu/boson1.pdf and http://www.qtrac.eu/boson2.pdf. You
can use these to see the difference between text and appearance
comparisons and to get a feel for how DiffPDF works.

If you hit a bug, please report it to mark@qtrac.eu. Be sure to include
"DiffPDF" in the subject line and specify the version you are using
and details of your system, e.g., operating system name and version,
compiler name and version, Qt library version, Poppler library version.

License
=======

This program was written by Mark Summerfield.
Copyright © 2008-13 Qtrac Ltd. All rights reserved.

This program is free software: you can redistribute it and/or modify it
under the terms of the GNU General Public License as published by the
Free Software Foundation, either version 2 of the License, or (at your
option), any later version. This program is distributed in the hope that
it will be useful, but WITHOUT ANY WARRANTY; without even the implied
warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
GNU General Public License (in file gpl-2.0.txt) for more details.


Building on Mac OS X
====================

Here's how to build it:

    $ /usr/bin/ruby -e "$(curl -fsSL https://raw.github.com/gist/323731)"
    $ brew install qt
    $ brew install poppler --with-qt4

    # Dirs must be writeable because macdeployqt modifies copied files
    $ chmod -R u+w /usr/local/Cellar/qt/
    $ chmod -R u+w /usr/local/Cellar/poppler/

    $ curl -O http://www.qtrac.eu/diffpdf-1.5.0.tar.gz
    $ tar xvfz diffpdf-1.5.0.tar.gz
    $ cd diffpdf-1.5.0
    $ lrelease diffpdf.pro
    $ qmake -spec macx-g++
    $ make

Here's how to make a .dmg:

    # Fix references, remove unneeded Frameworks and build DMG
    $ macdeployqt diffpdf.app/
    $ cd diffpdf.app/Contents/Frameworks/
    $ rm -r QtDeclarative.framework/ QtNetwork.framework/
    QtScript.framework/ QtSql.framework/ QtSvg.framework/
    QtXmlPatterns.framework/
    $ cd ../../..
    $ hdiutil create diffpdf-1.5.0.dmg -srcfolder diffpdf.app/

Thanks to Dirk Loss for this information.
