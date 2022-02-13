# Modern Quantum Chemistry with Modern Fortran
Welcome to this tutorial! This tutorial is based on the [excellent C++ tutorial](https://github.com/CrawfordGroup/ProgrammingProjects) by [Prof. T. Daniel Crawford's group](https://crawford.chem.vt.edu/), and its [Python adaptation](https://pycrawfordprogproj.readthedocs.io/en/latest/index.html) by [ajz34](https://github.com/ajz34), which inspired the use of [Jupyter Book](https://jupyterbook.org/intro.html).

# Prerequisites
Although this tutorial will attempt to teach you some quantum chemistry and Fortran, you'll need a basic working knowledge of both, especially the former. 
### Books and courses on quantum chemistry

 1. **The** first book to get would be Szabo and Ostlund's [Modern Quantum Chemistry](https://www.amazon.co.uk/Modern-Quantum-Chemistry-Introduction-Electronic/dp/0486691861/ref=pd_sim_1/257-6651894-9620421?pd_rd_w=rSw1g&pf_rd_p=b1e87cc7-5592-4974-a868-4689b8cff950&pf_rd_r=T6W5KMW8PVAX8H7F4YCV&pd_rd_r=3937198d-695d-4e98-91ce-0abfef567e0b&pd_rd_wg=66b5X&pd_rd_i=0486691861&psc=1), ISBN: 0486691861
 2. The bible (it is about as long) of wavefunction-based quantum chemistry would be Helgaker, Jorgensen and Olsen's [Molecular Electronic-Structure Theory](https://www.amazon.co.uk/Molecular-Electronic-Structure-Theory-Trygve-Helgaker/dp/1118531477/ref=tmm_pap_swatch_0?_encoding=UTF8&qid=1644700035&sr=1-4), ISBN: 9781118531471
 3. [This GitHub repo](https://github.com/hebrewsnabla/awesome-qc-courses) collects many good quantum chemistry courses, of which I would recommend [Prof. Evangelista's course](https://github.com/fevangelista/CHEM532-ElectronicStructure-Notes) most.

### Fortran resources
Contrary to popular belief, Fortran is very much alive and well-loved all around the world, it also has a very active core group of users which makes getting into Fortran today easier than ever. These are some of the books and websites I would recommend:

 1. [Fortran-Lang](https://fortran-lang.org/), the de-facto official page and one-stop shop for everything you need to start coding in Fortran
 2. [Fortran wiki](https://fortranwiki.org/fortran/show/HomePage), similar to above.
 3. If you're more of a book person, Milan Curcic's [Modern Fortran: Building Efficient Parallel Applications](https://www.amazon.co.uk/Modern-FORTRAN-Milan-Curcic/dp/1617295280/ref=sr_1_1?crid=30PSOYG5QWFVZ&keywords=fortran%20milan%20curcic&qid=1644700523&s=books&sprefix=fortran%20milan%20curcic,stripbooks,62&sr=1-1) is one of the most up-to-date textbooks on Fortran, written by someone who knows the language inside-out.
 4. Less of a textbook and more of a documentation of the language, [Modern Fortran Explained: Incorporating Fortran 2018](https://www.amazon.co.uk/Modern-Fortran-Explained-Incorporating-Mathematics-dp-0198811896/dp/0198811896/ref=dp_ob_title_bk) makes for a good reference.
 
 ### Your computing environment
 You need
 
 1. A Linux distribution
 2. A working Fortran compiler (see Fortran resources above), gfortran comes with most Linux distros.
 3. A text editor. If you don't already have a favourite editor, I recommend [Sublime Text](https://www.sublimetext.com/), which has a bunch of cool features like multi-cursor editing, and with the [Fortran package](https://packagecontrol.io/packages/Fortran) also supports Fortran syntax highlighting, with docstring support for intrinsics.

```{admonition} What if I use Windows?
If you're on Windows 10 or 11, you can download the Windows Subsystem for Linux 2 (WSL2), which is a Windows-native virtual machine for a stripped-down version of Ubuntu (as of Windows 11, the performance rivals actual native Ubuntu, and even comes with native GUI support, so it's almost as good as the real thing). Instructions on how to do so can be found on [official Microsoft documentation](https://docs.microsoft.com/en-us/windows/wsl/install). It is also highly recommended that you download the official [Windows Terminal](https://www.microsoft.com/en-gb/p/windows-terminal/9n0dx20hk701#activetab=pivot:overviewtab) app, which makes the command-line interface experience so much better.