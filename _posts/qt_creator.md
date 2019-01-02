---
layout: post
title: "Run LittlevGL PC Simulator from QT-Creator in Windows"
author: "pusillus"
cover: /assets/qt_creator/QT_littlevgl.PNG
image:
  path: /assets/qt_creator/QT_littlevgl.PNG
  height: 717
  width: 1324

  image:
  path: /assets/qt_creator/new_project.PNG
  height: 882
  width: 552
---

This is a step by step tutorial to run littlevgl PC simulator, in Windows 10, from QT-Creator 4.8.0 with Mingw 64 bit compiler.
Refer https://www.qt.io/ to install the open source version of QT environment.


download SDL2 developement libraries for mingw:
https://www.libsdl.org/download-2.0.php

in pc_simulator folder create a subfolder named SDL2, copy sdl header files there.
create SDL2/lib subfolder and copy libraries for i686-w64 from SDL2 package.

* Open QT-Creator
* from 'file' menu select 'new file or project'.
  * in the form select 'non-qt-project' and 'plain C application'. Press 'choose' button.


* in the project management form:
  * location: select project directory location and type a project name (ex. : pc_sim). press 'next' button.
  * build system: select qmake. press 'next' button.
  * kits: select "Mingw 64-bit". press 'next' button.
  * summary: press 'finish' button.
![QT-Creator project set up](/assets/qt_creator/new_project.PNG)

* close project from QT-Creator.

new subfolder is created with pc_sim.pro, pc_sim.pro.user and main.c template.
move pc_sim.pro, pc_sim.pro.user to main directory. remove "pc_sim" subfolder.

from QT-Creator open pc_sim.pro. Edit pc_sim.pro and remove sources:
'''
SOURCES += \
        main.c
'''
save project

in 'projects' pane right click on pc_sim project and select "Add Existing Directory" from menu

from file list, remove folder "lv_examples" and "SDL2". Then add only .c and .h files from folder "lv_examples/demo".

edit pc_sim.pro and add this lines to add SDL2 library and includes to the project:

'''
LIBS += -L$$PWD/SDL2/lib/ -lmingw32 -lSDL2main -lSDL2

INCLUDEPATH += $$PWD/SDL2
DEPENDPATH += $$PWD/SDL2
'''

select 'release' build from left panel icon.

Running demo
![QT-Creator running LittlevGL demo in PC simulator](/assets/qt_creator/QT_littlevgl.PNG)

