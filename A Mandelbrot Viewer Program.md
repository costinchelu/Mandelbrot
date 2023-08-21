## A Mandelbrot Viewer Program

------

| ![img](https://math.hws.edu/eck/js/mandelbrot/java/mandelbrot1.jpeg) | This page discusses a Java program for exploring the Mandelbrot set. The program and its source code are available for [download](https://math.hws.edu/eck/js/mandelbrot/java/MB-java.html#download). A somewhat less capable JavaScript version of the program, which can be used in a Web browser, can be found athttp://math.hws.edu/eck/js/mandelbrot/MB.htmlYou can also browse a [collection of examples](https://math.hws.edu/eck/js/mandelbrot/java/MandelbrotSettings/index.html), with links to settings files that can be loaded into either the Java or the JavaScript version of the program.The Mandelbrot set itself is a well-known mathematical object; see the [Wikipedia entry](http://en.wikipedia.org/wiki/Mandelbrot_Set) for more information, if you need it. |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
|                                                              |                                                              |

------

### About the Program:

Visualizations of the Mandelbrot Set can be computed as follows: Take a point **(a,b)** in the xy-plane. Set **(x,y) = (a,b)**. Perform the computation **(x,y)= (a2 - b2 + a, 2xy + b)** repeatedly until one of two things happen; either (1) the point (x,y) is more than 2 units distant from (0,0); or (2) the number of times that you have performed the computation is equal to some set upper limit. The number of times that you perform the computation is called the number of **iterations**, and the upper limit on the number of iterations is referred to as **MaxIterations** in the program. In the case (1), the starting point **(a,b)** is **definitely not** in the Mandelbrot Set; in the case (2), the starting point **(a,b)** is **possibly** in the Mandlebrot Set (but increasing the maximum number of iterations might show that **(a,b)** is actually not in the set). This sort of computation can't *prove* that a point is in the Mandelbrot Set, since that would require doing an infinite number of iterations and checking that **(x,y)** *never* moves more than two units away from (0,0).

In the program, each pixel in an image is colored as follows: The image represents a rectangle in the xy-plane bounded by *xmin* on the left, *xmax* on the right, *ymin* on the bottom, and *ymax* on the top. Take **(a,b)** to be the point in the center of the pixel, and use **(a,b)** as the starting point in the computation described in the previous paragraph. If case (1) applies, then the pixel is assigned a color that depends on the number of iterations that were done. The colors that are used for such points are referred to as the "palette"; you can modify the palette using the "Show Palette Editor" and "Apply Default Palette" commands in the "Control" menu. If the case (2) applies, the pixel is assigned a color that represents a point that is possibly in the Mandelbrot Set; by default, this color is black, but the color can be set with the "Mandelbrot Color" submenu of the "Control" menu. Note that increasing the MaxIteration count can convert pixels from case (2) to case (1) -- that is, it can fill in black areas with color as more points are proven to be not in the Mandelbrot Set.

The "interesting" regions of the xy-plane are those along the boundary of the Mandelbrot Set, between black and colored areas. The object of the program is to find an interesting region and to make its structure visible -- and beautiful -- with well-chosen colors. You can zoom in on a point along the boundary, and you will always find more structure. To zoom in, click-and-drag the mouse to enclose a rectangular reqion. When you release the mouse, the inside of the rectangle will be expanded to fill the entire image. (The mouse can also be used for other functions; see the "Help..." command in the "Tools" menu for more information.) As you zoom in, you will have to increase MaxIterations, and you will want to use the Palette Editor to adjust the colors.

After computing the image as described here, the program will make a second pass in which it computes iteration counts at additional points. The data from these additional points is averaged in with the data from the first pass. This can give a smoother, more attractive image. You can turn off this behavior, if you want, using the "Enable Subpixel Sampling" command in the "Control" menu.

If you zoom in very far, the program will switch over to "High Precision" calculation. The numbers that are ordinarily used have only about 18 digits of accuracy. You can easily zoom in to the point where more digits are required. High precision computation allows any number of digits, but it takes much longer than normal precision (mostly because the normal precision numbers are implemented very efficiently in the hardware).

The program has a "File" menu that can be used to save the images created by the program. It can also save and load "Mandelbrot Settings" files, which are small files that contain specifications of all the data needed to reconstruct an image.

The program also has the ability to distribute its computation over a group of networked computers; more information about this can be found below.

------

### Downloads and Links:

- [**xMandelbrot.jar**](https://math.hws.edu/eck/js/mandelbrot/java/xMandelbrot.jar) --- Download the compiled program. (Alternatively, you can download the source code and compile it yourself.) If Java is properly installed on your computer, you should be able to run this by double-clicking. You can also run the program from the command line with the command: java -jar xMandelbrot.jar
- [**Source Code**](https://math.hws.edu/eck/js/mandelbrot/java/xMandelbrotSource-1-2.zip) --- Download the source code for the program, as a .zip archive. See the [README](https://math.hws.edu/eck/js/mandelbrot/java/xMandelbrotSource-1-2/README.txt) file from the download for more information.
- [**Browse the source online**](https://math.hws.edu/eck/js/mandelbrot/java/xMandelbrotSource-1-2/) --- The actual source code files can be found in the directories [edu/hws/eck/umb](https://math.hws.edu/eck/js/mandelbrot/java/xMandelbrotSource-1-2/edu/hws/eck/umb), [edu/hws/eck/umb/comp](https://math.hws.edu/eck/js/mandelbrot/java/xMandelbrotSource-1-2/edu/hws/eck/umb/comp), [edu/hws/eck/umb/palette](https://math.hws.edu/eck/js/mandelbrot/java/xMandelbrotSource-1-2/edu/hws/eck/umb/palette), and [edu/hws/eck/umb/util](https://math.hws.edu/eck/js/mandelbrot/java/xMandelbrotSource-1-2/edu/hws/eck/umb/util).
- [**MandelbrotCL.jar**](https://math.hws.edu/eck/js/mandelbrot/java/MandelbrotCL.jar) --- A command-line version of the program, which can be used to create images from settings files, without a graphical user interface. Documentation can be found below. The source code for this program is included in the above source code links.
- [**MBNetServe.jar**](https://math.hws.edu/eck/js/mandelbrot/java/MBNetServe.jar) --- A server program that can be used to distribute the computation over a network. Documentation can be found below. The source code for this program is included in the above source code links.

------

### Documentation for MandelbrotCL.jar:

MandelbrotCL.jar is a simple command-line utility for making Mandelbrot images. This program can read Mandelbrot "settings" files, which are created by xMandelbrot.jar, and can create the images that are specified by those files. I use this utility, for example, to create small "thumbnail" images from a group of settings files. The syntax for using this command is:



```
           java -jar MandelbrotCL.jar  [options]  filenames...
```

where "filenames..." represents one or more settings file names and the "[options]" can include any or all (or none) of the following:

- **-size WWWxHHH** --- where WWW and HHH are positive integers, specifies the size of the image. If no size is specified, 800x600 is used.
- **-format XXX** --- use XXX as the format for the image. PNG is the default. JPEG is also definitely supported. Other formats might be supported as well.
- **-onepass** --- turn subpixel sampling off. If this option is omitted, subpixel sampling is used. (This is an option in the Control menu of xMandelbrot.jar; subpixel sampling can produce smoother, more attractive images in many cases.)
- **-net XXX** --- add one or more network workers. The format for XXX is a list of one or more hosts, separated by commas. Each host can be specified as a host name or IP address optionally followed by a colon and a port number. The port number is only necessary if different from the default, 17071. No spaces are allowed in the list of computers. A copy of MBNetServe.jar should already be running on each of the specified computers.

For example, to make small JPEG images for two files named mbdata1.xml and mbdata2.xml:

```
        java -jar MandelbrotCL.jar -size 160x120 -format jpeg mbdata1.xml mbdata2.xml
```

By the way, if you are working with very large images, you might need to tell the java virtual machine to use more memory than it ordinarily would. You can do this with the "-Xms" option to the java command. For example:

```
       java -jar -Xms2000m MandelbrotCL.jar -size 3300x2550 -format jpeg settings.xml
```

------

### Documentation for MBNetServe.jar:

It can take a long time to compute some Mandelbrot images. This is especially true for high precision computation, which is used when you zoom in so far that the standard Java real number implementation does not have enough significant digits to represent the numbers involved. The networking option is for people who want to speed up these long computations and who have access to several networked computers.

To distribute Mandelbrot computations over a network, you must run MBNetServe.jar on each computer EXCEPT the one where you will run xMandlebrot.jar (or MandelbrotCL.jar). Once that is done, you can use the "Configure Multiprocessing..." command in the "Control" menu of xMandelbrot to configure that program to use the network. (For MandelbrotCL, use the "-net" option.) You will need to know something about networking in order to use this option. Most important, you will need to know the host names or IP addresses of the computers where the server is running.

To run MBNetServe.jar on the computers that you want to use as computation servers, use the following command in the directory that contains the program:

```
                java -jar MBNetServe.jar [options]
```

where the "[options]" can include:

- **-processcount XXX** --- use XXX processes instead of the default number. Enter 0 for XXX to use one process for each available processor. The default is to use one less than this (if the number of processors is greater than one).
- **-timeout XXX** --- exit after XXX minutes of inactivity. The default is 30 minutes. Use 0 for XXX to mean that there is no timeout. You can also stop the server by pressing Control-C in the window where the program is running.
- **-once** --- accept one connection, and exit when that connection is closed. The default is to open a new listener after the connection is closed and wait for another connection.
- **-quiet** --- suppress all output.
- **-port XXX** --- listen on port number XXX instead of on the default port (17071). (Ordinarily, you will NOT need this option; just use the default.)

For example:

```
                java -jar MBNetServe.jar -processcount 0
```

To use the network in xMandelbrot, choose the "Configure Multiprocessing..." command from the "Control" menu. In the dialog box, check the option labeled "Enable Networking". Then, use the "Add Network Host" button to add each computer where MBNetServe is running. When you click this button, a small dialog will open where you can type in the host name of a computer that is running the server. (You can also enter an IP address, instead of a host name.) After adding the hosts, click the "Apply Config Now" button -- the network is not activated until you press this button. You should see "Connecting" next to each host name in the list. In a few seconds, this should change to "Connected." If it changes to "Connection Failed", or if it continues to say "Connected" for some time, then there is something wrong -- check that the server is running and that the host names or IP addresses are correct. Even if some listed connections are not working, the program will still use those that are connected. (Note that the list of hosts that you have entered will be saved for the next time you run the program, but networking will not automatically be turned on when the program runs; you will have to enable it by hand each time you run the program.)

Note: If your server computers are Linux or Mac OS computers that are configured to accept ssh connections, you can start up the server program remotely, using the ssh command, instead of logging on to each individual computer to start the program. If the computer's name is, for example, cslab1.hws.edu, you could use a command such as:

```
              ssh -f cslab1.hws.edu java -jar MBNetServe.jar -quiet -processcount 0
```

The "-f" option means that the command will be run in the background (after asking for your password, if required) so that you can continue to use the same command-line window to give other commands. This assumes that you have an account on cslab1.hws.edu with the same user name as on the computer where you give this command. It also assumes that MBNetServe.jar is in your home directory on cslab1.hws.edu. MBNetServe will shut itself down after 30 minutes of inactivity, so you don't have to worry about shutting it down. However, if you do want to shut down the server remotely, you can do so by using a special "-shutdown" option on the MBNetServe program. For example, if you are finished with the server that was started with the above command, you can use:

```
            java -jar MBNetServe.jar -shutdown cslab1.hws.edu
```

to shut down the server. (This command will NOT work if the server is still being used by xMandelbrot or MandelbrotCL.)

------

[*David Eck*](http://math.hws.edu/eck/index.html)