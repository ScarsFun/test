---
layout: post
title: "Running LittlevGL PC Simulator from QT-Creator in Windows"
author: "ScarsFun"
cover: /assets/qt_creator/QT_littlevgl.PNG
image:
  path: /assets/qt_creator/QT_littlevgl.PNG
  height: 300
  width: 300

---
#Running LittlevGL PC Simulator from QT-Creator in Windows
Qt-Creator is a powerful tool and is easy manage non Qt project too.
With the latest release Qt 5.12.0, GCC x64 compiler for windows is supported.
This is a step by step tutorial to run littlevgl PC simulator, in Windows 10, from Qt-Creator 4.8.0 with Mingw 64 bit compiler.

##Requirements
* Qt-Creator and Mingw-64bit environment. Refer to https://www.qt.io/ to install the open source version of QT environment.
* SDL2 developement libraries for mingw: https://www.libsdl.org/download-2.0.php
* LittlevGL PC Simulator: https://littlevgl.com/pc-simulator

in pc_simulator folder create a subfolder named SDL2, copy sdl header files there.
create SDL2/lib subfolder and copy libraries for i686-w64 from SDL2 package.

* Open Qt-Creator
* from 'file' menu select 'new file or project'.
  * in the form select 'non-qt-project' and 'plain C application'. Press 'choose' button.

![QT-Creator project set up](/assets/qt_creator/new_project.PNG)

* in the project management form:
  * location: select project directory location and type a project name (ex. : pc_sim). press 'next' button.
  * build system: select qmake. press 'next' button.
  * kits: select "Mingw 64-bit". press 'next' button.
  * summary: press 'finish' button.

![QT-Creator plain C app](/assets/qt_creator/plain_c_app.PNG)

A new subfolder is created with pc_sim.pro, pc_sim.pro.user and main.c template.

* close project from QT-Creator.
* move pc_sim.pro, pc_sim.pro.user to main directory. remove "pc_sim" subfolder.

* from QT-Creator: open project pc_sim.pro. Edit file pc_sim.pro and remove this two lines:
  ```
  SOURCES += \
        main.c
  ```

![QT-Creator remove template source](/assets/qt_creator/remove_souces.PNG)
* save project

* in 'projects' pane: right click on pc_sim project and select "Add Existing Directory" from menu. All sources files and includes should be already selected by default.
  * from file list: deselect folder "lv_examples" and "SDL2". Then add only .c and .h files from folder "lv_examples/demo".

 ![QT-Creator remove template source](/assets/qt_creator/file_select.PNG)
* edit pc_sim.pro and add this lines to add SDL2 library and includes to the project:
  ```
  LIBS += -L$$PWD/SDL2/lib/ -lmingw32 -lSDL2main -lSDL2

  INCLUDEPATH += $$PWD/SDL2
  DEPENDPATH += $$PWD/SDL2
  ```

![QT-Creator add libraries path](/assets/qt_creator/add_SDL_path.PNG)
* Save project.
* select 'release' build from left panel icon.

![QT-Creator manage kit](/assets/qt_creator/release.png)
* Run demo

![QT-Creator running LittlevGL demo in PC simulator](/assets/qt_creator/QT_littlevgl.PNG)

