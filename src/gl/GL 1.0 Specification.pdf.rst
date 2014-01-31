The OpenGLTM Graphics System:
        A Speci cation
         (Version 1.0)

              Mark Segal
              Kurt Akeley
                 Editor:
              Chris Frazier




     Version 1.0 - 1 July 1994
          Copyright c 1992, 1993, 1994 Silicon Graphics, Inc.

        This document contains unpublished information of
                      Silicon Graphics, Inc.
This document is protected by copyright, and contains information propri-
etary to Silicon Graphics, Inc. Any copying, adaptation, distribution, public
performance, or public display of this document without the express written
consent of Silicon Graphics, Inc. is strictly prohibited. The receipt or pos-
session of this document does not convey any rights to reproduce, disclose,
or distribute its contents, or to manufacture, use, or sell anything that it
may describe, in whole or in part.
             U.S. Government Restricted Rights Legend
Use, duplication, or disclosure by the Government is subject to restrictions
set forth in FAR 52.227.19(c)(2) or subparagraph (c)(1)(ii) of the Rights
in Technical Data and Computer Software clause at DFARS 252.227-7013
and/or in similar or successor clauses in the FAR or the DOD or NASA FAR
Supplement. Unpublished rights reserved under the copyright laws of the
United States. Contractor/manufacturer is Silicon Graphics, Inc., 2011 N.
Shoreline Blvd., Mountain View, CA 94039-7311.
          OpenGL is a trademark of Silicon Graphics, Inc.




                       Version 1.0 - 1 July 1994
Contents
1 Introduction                                                                                         1
  1.1    What is the OpenGL Graphics System?           :   :   :   :   :   :   :   :   :   :   :   :   1
  1.2    Programmer's View of OpenGL : : : : :         :   :   :   :   :   :   :   :   :   :   :   :   1
  1.3    Implementor's View of OpenGL : : : : :        :   :   :   :   :   :   :   :   :   :   :   :   2
  1.4    Our View : : : : : : : : : : : : : : : : :    :   :   :   :   :   :   :   :   :   :   :   :   2
2 OpenGL Operation                                                                                     4
  2.1    OpenGL Fundamentals : : : : : : : : : : :             :   :   :   :   :   :   :   :   :   :    4
  2.2    GL State : : : : : : : : : : : : : : : : : : :        :   :   :   :   :   :   :   :   :   :    7
  2.3    GL Command Syntax : : : : : : : : : : : :             :   :   :   :   :   :   :   :   :   :    7
  2.4    Basic GL Operation : : : : : : : : : : : : :          :   :   :   :   :   :   :   :   :   :    9
  2.5    GL Errors : : : : : : : : : : : : : : : : : : :       :   :   :   :   :   :   :   :   :   :   11
  2.6    Begin/End Paradigm : : : : : : : : : : : : :          :   :   :   :   :   :   :   :   :   :   12
         2.6.1 Begin and End Objects : : : : : : :             :   :   :   :   :   :   :   :   :   :   15
         2.6.2 Polygon Edges : : : : : : : : : : : :           :   :   :   :   :   :   :   :   :   :   19
         2.6.3 GL Commands within Begin/End :                  :   :   :   :   :   :   :   :   :   :   20
  2.7    Vertex Speci cation : : : : : : : : : : : : :         :   :   :   :   :   :   :   :   :   :   20
  2.8    Rectangles : : : : : : : : : : : : : : : : : : :      :   :   :   :   :   :   :   :   :   :   22
  2.9    Coordinate Transformations : : : : : : : : :          :   :   :   :   :   :   :   :   :   :   23
         2.9.1 Controlling the Viewport : : : : : :            :   :   :   :   :   :   :   :   :   :   24
         2.9.2 Matrices : : : : : : : : : : : : : : : :        :   :   :   :   :   :   :   :   :   :   25
         2.9.3 Normal Transformation : : : : : : :             :   :   :   :   :   :   :   :   :   :   29
         2.9.4 Generating texture coordinates : : :            :   :   :   :   :   :   :   :   :   :   30
  2.10   Clipping : : : : : : : : : : : : : : : : : : : :      :   :   :   :   :   :   :   :   :   :   32
  2.11   Current Raster Position : : : : : : : : : : :         :   :   :   :   :   :   :   :   :   :   34
  2.12   Colors and Coloring : : : : : : : : : : : : :         :   :   :   :   :   :   :   :   :   :   37
         2.12.1 Lighting : : : : : : : : : : : : : : : :       :   :   :   :   :   :   :   :   :   :   38
         2.12.2 Lighting Parameter Speci cation : :            :   :   :   :   :   :   :   :   :   :   42
                                        i




                                 Version 1.0 - 1 July 1994
ii                                                                           CONTENTS

          2.12.3   ColorMaterial : : : : : : : : : : : : : : : : : : : : : 43
          2.12.4   Lighting State : : : : : : : : : : : : : :    :   :   :   :   :   :   :   :   46
          2.12.5   Color Index Lighting : : : : : : : : : : :    :   :   :   :   :   :   :   :   46
          2.12.6   Clamping or Masking : : : : : : : : : :       :   :   :   :   :   :   :   :   47
          2.12.7   Flatshading : : : : : : : : : : : : : : : :   :   :   :   :   :   :   :   :   48
          2.12.8   Color and Texture Coordinate Clipping         :   :   :   :   :   :   :   :   48
          2.12.9   Final Color Processing : : : : : : : : : :    :   :   :   :   :   :   :   :   49
3 Rasterization                                                                                  50
     3.1 Invariance : : : : : : : : : : : : : : : : : : : : : : : :          :   :   :   :   :   51
     3.2 Antialiasing : : : : : : : : : : : : : : : : : : : : : : :          :   :   :   :   :   51
     3.3 Points : : : : : : : : : : : : : : : : : : : : : : : : : :          :   :   :   :   :   53
          3.3.1 Point Rasterization State : : : : : : : : : : :              :   :   :   :   :   56
     3.4 Line Segments : : : : : : : : : : : : : : : : : : : : :             :   :   :   :   :   56
          3.4.1 Basic Line Segment Rasterization : : : : : : :               :   :   :   :   :   56
          3.4.2 Other Line Segment Features : : : : : : : : :                :   :   :   :   :   59
          3.4.3 Line Rasterization State : : : : : : : : : : : :             :   :   :   :   :   63
     3.5 Polygons : : : : : : : : : : : : : : : : : : : : : : : : :          :   :   :   :   :   63
          3.5.1 Basic Polygon Rasterization : : : : : : : : : :              :   :   :   :   :   63
          3.5.2 Stippling : : : : : : : : : : : : : : : : : : : :            :   :   :   :   :   65
          3.5.3 Antialiasing : : : : : : : : : : : : : : : : : : :           :   :   :   :   :   66
          3.5.4 Options Controlling Polygon Rasterization :                  :   :   :   :   :   66
          3.5.5 Polygon Rasterization State : : : : : : : : : :              :   :   :   :   :   67
     3.6 Pixel Rectangles : : : : : : : : : : : : : : : : : : : :            :   :   :   :   :   67
          3.6.1 Pixel Storage Modes : : : : : : : : : : : : : :              :   :   :   :   :   68
          3.6.2 Pixel Transfer Modes : : : : : : : : : : : : :               :   :   :   :   :   68
          3.6.3 Rasterization of Pixel Rectangles : : : : : : :              :   :   :   :   :   70
     3.7 Bitmaps : : : : : : : : : : : : : : : : : : : : : : : : :           :   :   :   :   :   77
     3.8 Texturing : : : : : : : : : : : : : : : : : : : : : : : :           :   :   :   :   :   79
          3.8.1 Texture Mini cation : : : : : : : : : : : : : :              :   :   :   :   :   83
          3.8.2 Texture Magni cation : : : : : : : : : : : : :               :   :   :   :   :   87
          3.8.3 Texture Environments and Texture Functions                   :   :   :   :   :   87
          3.8.4 Texture Application : : : : : : : : : : : : : :              :   :   :   :   :   88
     3.9 Fog : : : : : : : : : : : : : : : : : : : : : : : : : : : :         :   :   :   :   :   90
     3.10 Antialiasing Application : : : : : : : : : : : : : : : :           :   :   :   :   :   92




                          Version 1.0 - 1 July 1994
CONTENTS                                                                                                                         iii

4 Fragments and the Framebu er                                                                                                   93
  4.1 Per-Fragment Operations : : : : : : :                                 :   :   :   :   :   :   :   :   :   :   :   :   :    94
      4.1.1 Pixel Ownership Test : : : : :                                  :   :   :   :   :   :   :   :   :   :   :   :   :    94
      4.1.2 Scissor test : : : : : : : : : : :                              :   :   :   :   :   :   :   :   :   :   :   :   :    95
      4.1.3 Alpha test : : : : : : : : : : : :                              :   :   :   :   :   :   :   :   :   :   :   :   :    95
      4.1.4 Stencil test : : : : : : : : : : :                              :   :   :   :   :   :   :   :   :   :   :   :   :    96
      4.1.5 Depth bu er test : : : : : : : :                                :   :   :   :   :   :   :   :   :   :   :   :   :    97
      4.1.6 Blending : : : : : : : : : : : : :                              :   :   :   :   :   :   :   :   :   :   :   :   :    98
      4.1.7 Dithering : : : : : : : : : : : :                               :   :   :   :   :   :   :   :   :   :   :   :   :   100
      4.1.8 Logical Operation : : : : : : :                                 :   :   :   :   :   :   :   :   :   :   :   :   :   100
  4.2 Whole Framebu er Operations : : : :                                   :   :   :   :   :   :   :   :   :   :   :   :   :   102
      4.2.1 Selecting a Bu er for Writing :                                 :   :   :   :   :   :   :   :   :   :   :   :   :   102
      4.2.2 Fine Control of Bu er Updates                                   :   :   :   :   :   :   :   :   :   :   :   :   :   103
      4.2.3 Clearing the Bu ers : : : : : :                                 :   :   :   :   :   :   :   :   :   :   :   :   :   104
      4.2.4 The Accumulation Bu er : : :                                    :   :   :   :   :   :   :   :   :   :   :   :   :   105
  4.3 Drawing, Reading, and Copying Pixels                                  :   :   :   :   :   :   :   :   :   :   :   :   :   107
      4.3.1 Writing to the Stencil Bu er :                                  :   :   :   :   :   :   :   :   :   :   :   :   :   107
      4.3.2 Reading Pixels : : : : : : : : :                                :   :   :   :   :   :   :   :   :   :   :   :   :   107
      4.3.3 Copying Pixels : : : : : : : : :                                :   :   :   :   :   :   :   :   :   :   :   :   :   112
      4.3.4 Pixel draw/read state : : : : :                                 :   :   :   :   :   :   :   :   :   :   :   :   :   113
5 Special Functions                                                                                                             114
  5.1   Evaluators : : : : :    :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   114
  5.2   Selection : : : : : :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   120
  5.3   Feedback : : : : :      :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   122
  5.4   Display Lists : : :     :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   125
  5.5   Flush and Finish        :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   129
  5.6   Hints : : : : : : : :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   129
6 State and State Requests                                                                                                      130
A Invariance                                                                                                                    154
  A.1   Repeatability : : : : :         :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   154
  A.2   Multi-pass Algorithms           :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   155
  A.3   Invariance Rules : : :          :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   155
  A.4   What All This Means             :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   :   157
B Corollaries                                                                                                                   158




                                    Version 1.0 - 1 July 1994
iv                                            CONTENTS

     Index of OpenGL Commands                      161




                  Version 1.0 - 1 July 1994
List of Figures
 2.1 Block diagram of the GL. : : : : : : : : : : : : : : : : : : : :               9
 2.2 Creation of a processed vertex from a transformed vertex and
     current values. : : : : : : : : : : : : : : : : : : : : : : : : : :           13
 2.3 Primitive assembly and processing. : : : : : : : : : : : : : : :              15
 2.4 Triangle strips, fans, and independent triangles. : : : : : : : :             17
 2.5 Quadrilateral strips and independent quadrilaterals. : : : : :                18
 2.6 Vertex transformation sequence. : : : : : : : : : : : : : : : :               23
 2.7 Current raster position. : : : : : : : : : : : : : : : : : : : : :            35
 2.8 Processing of colors. : : : : : : : : : : : : : : : : : : : : : : :           37
 2.9 ColorMaterial operation. : : : : : : : : : : : : : : : : : : : : :            43
 3.1    Rasterization. : : : : : : : : : : : : : : : : : : : : : : : : :   :   :   50
 3.2    Rasterization of non-antialiased wide points. : : : : : : : :      :   :   55
 3.3    Rasterization of antialiased wide points. : : : : : : : : : :      :   :   55
 3.4    Visualization of Bresenham's algorithm. : : : : : : : : : :        :   :   57
 3.5    Rasterization of non-antialiased wide lines. : : : : : : : :       :   :   60
 3.6    The region used in rasterizing an antialiased line segment.        :   :   62
 3.7    Operation of DrawPixels. : : : : : : : : : : : : : : : : :         :   :   70
 3.8    Selecting a subimage from an image : : : : : : : : : : : :         :   :   74
 3.9    A bitmap and its associated parameters. : : : : : : : : : :        :   :   78
 3.10   A texture image and the coordinates used to access it. : :         :   :   81
 4.1 Per-fragment operations. : : : : : : : : : : : : : : : : : : :        :   :    94
 4.2 Operation of ReadPixels. : : : : : : : : : : : : : : : : :            :   :   107
 4.3 Operation of CopyPixels. : : : : : : : : : : : : : : : : :            :   :   112
 5.1 Map Evaluation. : : : : : : : : : : : : : : : : : : : : : : :         :   :   116
 5.2 Feedback syntax. : : : : : : : : : : : : : : : : : : : : : : :        :   :   126


                                       v




                                Version 1.0 - 1 July 1994
List of Tables
 2.1   GL command su xes : : : : : : : : : : : : : : : : : : : :       :   :    8
 2.2   GL data types : : : : : : : : : : : : : : : : : : : : : : : :   :   :   10
 2.3   Summary of GL errors : : : : : : : : : : : : : : : : : : : :    :   :   13
 2.4   RGBA color component conversions : : : : : : : : : : : :        :   :   38
 2.5   Summary of lighting parameters. : : : : : : : : : : : : : :     :   :   40
 2.6   Correspondence of lighting parameter symbols to names. :        :   :   44
 2.7   Polygon atshading color selection. : : : : : : : : : : : : :    :   :   48
 3.1   PixelStore parameters pertaining to DrawPixels. : :         :   :   :   68
 3.2   PixelTransfer parameters. : : : : : : : : : : : : : : : :   :   :   :   69
 3.3   PixelMap parameters. : : : : : : : : : : : : : : : : : :    :   :   :   70
 3.4   DrawPixels and ReadPixels types. : : : : : : : : : :        :   :   :   72
 3.5   DrawPixels and ReadPixels formats. : : : : : : : : :        :   :   :   73
 3.6 Correspondence of texture components to extracted R, G, B,
     and A values. : : : : : : : : : : : : : : : : : : : : : : : : : : : 80
 3.7 Texture parameters and their values. : : : : : : : : : : : : : : 83
 3.8 Texture functions. : : : : : : : : : : : : : : : : : : : : : : : : 89
 4.1 Values controlling the source blending function and the source
     blending values they compute : : : : : : : : : : : : : : : : : : 99
 4.2 Values controlling the destination blending function and the
     destination blending values they compute : : : : : : : : : : : 99
 4.3 Arguments to LogicOp and their corresponding operations. : 101
 4.4 Arguments to DrawBu er and the bu ers that they indicate.103
 4.5 PixelStore parameters pertaining to ReadPixels. : : : : : : 108
 4.6 ReadPixels index masks and component conversion formulas.112
 5.1 Values speci ed by the target to Map1. : : : : : : : : : : : : 115
 5.2 Correspondence of feedback type to number of values per vertex.124
                                     vi




                     Version 1.0 - 1 July 1994
LIST OF TABLES                                                                               vii

  6.1    Attribute groups : : : : : : : : : : : : : : : : : : :      :   :   :   :   :   :   134
  6.2    State variable types : : : : : : : : : : : : : : : : :      :   :   :   :   :   :   136
  6.3    GL Internal begin-end state variables (inaccessible)        :   :   :   :   :   :   137
  6.4    Current Values and Associated Data : : : : : : : :          :   :   :   :   :   :   138
  6.5    Transformation state : : : : : : : : : : : : : : : : :      :   :   :   :   :   :   139
  6.6    Coloring : : : : : : : : : : : : : : : : : : : : : : : :    :   :   :   :   :   :   140
  6.7    Lighting (see also Table 2.5 for defaults) : : : : : :      :   :   :   :   :   :   141
  6.8    Rasterization : : : : : : : : : : : : : : : : : : : : :     :   :   :   :   :   :   142
  6.9    Texturing : : : : : : : : : : : : : : : : : : : : : : :     :   :   :   :   :   :   143
  6.10   Pixel Operations : : : : : : : : : : : : : : : : : : :      :   :   :   :   :   :   144
  6.11   Framebu er Control : : : : : : : : : : : : : : : : :        :   :   :   :   :   :   145
  6.12   Pixels : : : : : : : : : : : : : : : : : : : : : : : : :    :   :   :   :   :   :   146
  6.13   Pixels (cont.) : : : : : : : : : : : : : : : : : : : : :    :   :   :   :   :   :   147
  6.14   Evaluators (GetMap takes a map name) : : : : :              :   :   :   :   :   :   148
  6.15   Hints : : : : : : : : : : : : : : : : : : : : : : : : : :   :   :   :   :   :   :   149
  6.16   Implementation Dependent Values : : : : : : : : :           :   :   :   :   :   :   150
  6.17   More Implementation Dependent Values : : : : : :            :   :   :   :   :   :   151
  6.18   Implementation Dependent Pixel Depths : : : : : :           :   :   :   :   :   :   152
  6.19   Miscellaneous : : : : : : : : : : : : : : : : : : : : :     :   :   :   :   :   :   153




                                 Version 1.0 - 1 July 1994
Chapter 1
Introduction
This document describes the OpenGL graphics system: what it is, how it
acts, and what is required to implement it. We assume that the reader has
at least a rudimentary understanding of computer graphics. This means
familiarity with the essentials of computer graphics algorithms as well as
familiarity with basic graphics hardware and associated terms.

1.1 What is the OpenGL Graphics System?
OpenGL (for \Open Graphics Library") is a software interface to graphics
hardware. The interface consists of a set of several hundred procedures and
functions that allow a programmer to specify the objects and operations
involved in producing high-quality graphical images, speci cally color images
of three-dimensional objects.
    Most of OpenGL requires that the graphics hardware contain a frame-
bu er. Many OpenGL calls pertain to drawing objects such as points, lines,
polygons, and bitmaps, but the way that some of this drawing occurs (such
as when antialiasing or texturing is enabled) relies on the existence of a
framebu er. Further, some of OpenGL is speci cally concerned with frame-
bu er manipulation.

1.2 Programmer's View of OpenGL
To the programmer, OpenGL is a set of commands that allow the speci -
cation of geometric objects in two or three dimensions, together with com-
mands that control how these objects are rendered into the framebu er.
                                      1




                               Version 1.0 - 1 July 1994
2                                           CHAPTER 1. INTRODUCTION

For the most part, OpenGL provides an immediate-mode interface, mean-
ing that specifying an object causes it to be drawn.
    A typical program that uses OpenGL begins with calls to open a window
into the framebu er into which the program will draw. Then, calls are made
to allocate a GL context and associate it with the window. Once a GL con-
text is allocated, the programmer is free to issue OpenGL commands. Some
calls are used to draw simple geometric objects (i.e. points, line segments,
and polygons), while others a ect the rendering of these primitives includ-
ing how they are lit or colored and how they are mapped from the user's
two- or three-dimensional model space to the two-dimensional screen. There
are also calls to e ect direct control of the framebu er, such as reading and
writing pixels.

1.3 Implementor's View of OpenGL
To the implementor, OpenGL is a set of commands that a ect the opera-
tion of graphics hardware. If the hardware consists only of an addressable
framebu er, then OpenGL must be implemented almost entirely on the host
CPU. More typically, the graphics hardware may comprise varying degrees
of graphics acceleration, from a raster subsystem capable of rendering two-
dimensional lines and polygons to sophisticated oating-point processors
capable of transforming and computing on geometric data. The OpenGL
implementor's task is to provide the CPU software interface while dividing
the work for each OpenGL command between the CPU and the graphics
hardware. This division must be tailored to the available graphics hardware
to obtain optimum performance in carrying out OpenGL calls.
    OpenGL maintains a considerable amount of state information. This
state controls how objects are drawn into the framebu er. Some of this
state is directly available to the user: he or she can make calls to obtain its
value. Some of it, however, is visible only by the e ect it has on what is
drawn. One of the main goals of this speci cation is to make OpenGL state
information explicit, to elucidate how it changes, and to indicate what its
e ects are.

1.4 Our View
We view OpenGL as a state machine that controls a set of speci c draw-
ing operations. This model should engender a speci cation that satis es




                        Version 1.0 - 1 July 1994
1.4. OUR VIEW                                                          3

the needs of both programmers and implementors. It does not, however,
necessarily provide a model for implementation. An implementation must
produce results conforming to those produced by the speci ed methods, but
there may be ways to carry out a particular computation that are more
e cient than the one speci ed.




                             Version 1.0 - 1 July 1994
Chapter 2
OpenGL Operation
2.1 OpenGL Fundamentals
OpenGL (henceforth, the \GL") is concerned only with rendering into a
framebu er (and reading values stored in that framebu er). There is no
support for other peripherals sometimes associated with graphics hardware,
such as mice and keyboards. Programmers must rely on other mechanisms
to obtain user input.
    The GL draws primitives subject to a number of selectable modes. Each
primitive is a point, line segment, polygon, or pixel rectangle. Each mode
may be changed independently the setting of one does not a ect the settings
of others (although many modes may interact to determine what eventually
ends up in the framebu er). Modes are set, primitives speci ed, and other
GL operations described by sending commands in the form of function or
procedure calls.
    Primitives are de ned by a group of one or more vertices. A vertex
de nes a point, an endpoint of an edge, or a corner of a polygon where
two edges meet. Data (consisting of positional coordinates, colors, normals,
and texture coordinates) are associated with a vertex and each vertex is
processed independently, in order, and in the same way. The only exception
to this rule is if the group of vertices must be clipped so that the indicated
primitive ts within a speci ed region in this case vertex data may be
modi ed and new vertices created. The type of clipping depends on which
primitive the group of vertices represents.
    Commands are always processed in the order in which they are received,
although there may be an indeterminate delay before the e ects of a com-
                                       4




                       Version 1.0 - 1 July 1994
2.1. OPENGL FUNDAMENTALS                                                  5

mand are realized. This means, for example, that one primitive must be
drawn completely before any subsequent one can a ect the framebu er. It
also means that queries and pixel read operations return state consistent
with complete execution of all previously invoked GL commands. In gen-
eral, the e ects of a GL command on either GL modes or the framebu er
must be complete before any subsequent command can have any such e ects.
    In the GL, data binding occurs on call. This means that data passed
to a command are interpreted when that command is received. Even if the
command requires a pointer to data, those data are interpreted when the
call is made, and any subsequent changes to the data have no e ect on the
GL (unless the same pointer is used in a subsequent command).
    The GL provides direct control over the fundamental operations of 3D
and 2D graphics. This includes speci cation of such parameters as trans-
formation matrices, lighting equation coe cients, antialiasing methods, and
pixel update operators. It does not provide a means for describing or mod-
eling complex geometric objects. Another way to describe this situation is
to say that the GL provides mechanisms to describe how complex geometric
objects are to be rendered rather than mechanisms to describe the complex
objects themselves.
    The model for interpretation of GL commands is client-server. That is, a
program (the client) issues commands, and these commands are interpreted
and processed by the GL (the server). The server may or may not operate
on the same computer as the client. In this sense, the GL is \network-
transparent." A server may maintain a number of GL contexts, each of
which is an encapsulation of current GL state. A client may choose to
connect to any one of these contexts.
    The e ects of GL commands on the framebu er are ultimately controlled
by the window system that allocates framebu er resources. It is the window
system that determines which portions of the framebu er the GL may access
at any given time and that communicates to the GL how those portions
are structured. Therefore, there are no GL commands to con gure the
framebu er or initialize the GL. Similarly, display of framebu er contents
on a CRT monitor (including the transformation of individual framebu er
values by such techniques as gamma correction) is not addressed by the GL.
Framebu er con guration occurs outside of the GL in conjunction with the
window system the initialization of a GL context occurs when the window
system allocates a window for GL rendering.
    The GL is designed to be run on a range of graphics platforms with vary-
ing graphics capabilities and performance. To accommodate this variety, we




                               Version 1.0 - 1 July 1994
6                                   CHAPTER 2. OPENGL OPERATION

specify ideal behavior instead of actual behavior for certain GL operations.
In cases where deviation from the ideal is allowed, we also specify the rules
that an implementation must obey if it is to approximate the ideal behavior
usefully. This allowed variation in GL behavior implies that two distinct
GL implementations may not agree pixel for pixel when presented with the
same input even when run on identical framebu er con gurations.
    Finally, command names, constants, and types are pre xed in the GL
(by gl, GL , and GL, respectively in C) to reduce name clashes with other
packages. The pre xes are omitted in this document for clarity.


Floating-Point Computation
The GL must perform a number of oating-point operations during the
course of its operation. We do not specify how oating-point numbers are
to be represented or how operations on them are to be performed. We require
simply that numbers' oating-point parts contain enough bits and that their
exponent elds are large enough so that individual results of oating-point
operations are accurate to about 1 part in 105. The maximum representable
magnitude of a oating-point number used to represent positional or normal
coordinates must be at least 232 the maximum representable magnitude for
colors or texture coordinates must be at least 210. The maximum repre-
sentable magnitude for all other oating-point values must be at least 232.
x 0 = 0 x = 0 for any non-in nite and non-NaN x. 1 x = x 1 = x.
x + 0 = 0 + x = x. 00 = 1. (Occasionally further requirements will be speci-
  ed.) Most single-precision oating-point formats meet these requirements.
    Any representable oating-point value is legal as input to a GL command
that requires oating-point data. The result of providing a value that is not
a oating-point number to such a command is unspeci ed, but must not
lead to GL interruption or termination. In IEEE arithmetic, for example,
providing a negative zero or a denormalized number to a GL command yields
predictable results, while providing a NaN or an in nity yields unspeci ed
results.
    Some calculations require division. In such cases (including implied di-
visions required by vector normalizations), a division by zero produces an
unspeci ed result but must not lead to GL interruption or termination.




                       Version 1.0 - 1 July 1994
2.2. GL STATE                                                                7

2.2 GL State
The GL maintains considerable state. This document enumerates each state
variable and describes how each variable can be changed. For purposes
of discussion, state variables are categorized somewhat arbitrarily by their
function. Although we describe the operations that the GL performs on the
framebu er, the framebu er is not a part of GL state.
    We distinguish two types of state. The rst type of state, called GL
server state, resides in the GL server. The majority of GL state falls into
this category. The second type of state, called GL client state, resides in the
GL client. Unless otherwise speci ed, all state referred to in this document
is GL server state GL client state is speci cally identi ed. Each instance of
a GL context implies one complete set of GL server state each connection
from a client to a server implies a set of both GL client state and GL server
state.
    While an implementation of the GL may be hardware dependent, this
discussion is independent of the speci c hardware on which a GL is imple-
mented. We are therefore concerned with the state of graphics hardware
only when it corresponds precisely to GL state.

2.3 GL Command Syntax
GL commands are functions or procedures. Various groups of commands
perform the same operation but di er in how arguments are supplied to
them. To conveniently accommodate this variation, we adopt a notation for
describing commands and their arguments.
    GL commands are formed from a name followed, depending on the par-
ticular command, by up to 4 characters. The rst character indicates the
number of values of the indicated type that must be presented to the com-
mand. The second character or character pair indicates the speci c type of
the arguments: 8-bit integer, 16-bit integer, 32-bit integer, single-precision
  oating-point, or double-precision oating-point. The nal character, if
present, is v, indicating that the command takes a pointer to an array (a
vector) of values rather than a series of individual arguments. Two speci c
examples come from the Vertex command:
      void   Vertex3f(   float x, float y, float       z)
and




                                Version 1.0 - 1 July 1994
8                                      CHAPTER 2. OPENGL OPERATION

                        Letter Corresponding GL Type
                           b      byte
                           s      short
                           i      int
                           f      float
                           d      double
                          ub      ubyte
                          us      ushort
                          ui      uint

Table 2.1: Correspondence of command su x letters to GL argument types.
Refer to Table 2.2 for de nitions of the GL types.

      void   Vertex2sv(      short   v 2] )
These examples show the ANSI C declarations for these commands. In
general, a command declaration has the form
      rtype Namef 1234gf b s i f d ub us uigf vg
                     ( args ,] T arg1 , : : : , T argN , args]           )

rtype is the return type of the function. The braces (fg) enclose a series
of characters (or character pairs) of which one is selected. indicates no
character. The arguments enclosed in brackets ( args ,] and , args]) may
or may not be present. The N arguments arg1 through argN have type T,
which corresponds to one of the type letters or letter pairs as indicated in
Table 2.1 (if there are no letters, then the arguments' type is given explic-
itly). If the nal character is not v, then N is given by the digit 1, 2, 3, or
4 (if there is no digit, then the number of arguments is xed). If the nal
character is v, then only arg1 is present and it is an array of N values of
the indicated type. Finally, we indicate an unsigned type by the shorthand
of prepending a u to the beginning of the type name (so that, for instance,
unsigned char is abbreviated uchar).
    For example,
    The declarations shown in this document apply to ANSI C. Languages such as C++
and Ada that allow passing of argument type information admit simpler declarations and
fewer entry points.




                          Version 1.0 - 1 July 1994
2.4. BASIC GL OPERATION                                                     9

     void   Normal3ffdg( T arg )
indicates the two declarations
      void Normal3f( float arg1, float arg2, float arg3 )
      void Normal3d( double arg1, double arg2, double arg3 )

while
      void Normal3ffdgv( T arg )

means the two declarations
      void Normal3fv( float arg 3] )
      void Normal3dv( double arg 3] )

    Arguments whose type is xed (i.e. not indicated by a su x on the
command) are of one of 14 types (or pointers to one of these). These types
are summarized in Table 2.2.

2.4 Basic GL Operation
Figure 2.1 shows a schematic diagram of the GL. Commands enter the GL
on the left. Some commands specify geometric objects to be drawn while
others control how the objects are handled by the various stages. Most
commands may be accumulated in a display list for processing by the GL at
a later time. Otherwise, commands are e ectively sent through a processing
pipeline.
    The rst stage provides an e cient means for approximating curve and
surface geometry by evaluating polynomial functions of input values. The
next stage operates on geometric primitives described by vertices: points,
line segments, and polygons. In this stage vertices are transformed and lit,
and primitives are clipped to a viewing volume in preparation for the next
stage, rasterization. The rasterizer produces a series of framebu er addresses
and values using a two-dimensional description of a point, line segment, or
polygon. Each fragment so produced is fed to the next stage that performs
operations on individual fragments before they nally alter the framebu er.
These operations include conditional updates into the framebu er based
on incoming and previously stored depth values (to e ect depth bu ering),
blending of incoming fragment colors with stored colors, as well as masking
and other logical operations on fragment values.




                                Version 1.0 - 1 July 1994
10                                 CHAPTER 2. OPENGL OPERATION




     GL Type Minimum Precision Description
      boolean 1 bit            Boolean
         byte 8 bits           signed 2's complement binary
                               integer
        ubyte 8 bits           unsigned binary integer
        short 16 bits          signed 2's complement binary
                               integer
       ushort 16 bits          unsigned binary integer
         int  32 bits          signed 2's complement binary
                               integer
         uint 32 bits          unsigned binary integer
        sizei 32 bits          Non-negative binary integer size
         enum 32 bits          Enumerated binary integer value
     bitfield 32 bits          Bit eld
        float 32 bits          Floating-point value
       clampf 32 bits          Floating-point value clamped to
                                0 1]
       double 64 bits          Floating-point value
       clampd 64 bits          Floating-point value clamped to
                                0 1]
Table 2.2: GL data types. An implementation may use more bits than
the number indicated in the table to represent one of these types. Correct
interpretation of integer values outside the minimum range is not required,
however.




                      Version 1.0 - 1 July 1994
2.5. GL ERRORS                                                                        11



          Display
           List


                                Per−Vertex
                                Operations                 Per−
                                               Rasteriz−
                    Evaluator                              Fragment     Framebuffer
                                Primitive      ation
                                                           Operations
                                Assembly


                                                Texture
                                                Memory

                                Pixel
                                Operations



   Figure 2.1. Block diagram of the GL.


    Finally, there is a way to bypass the vertex processing portion of the
pipeline to send a block of fragments directly to the individual fragment
operations, eventually causing a block of pixels to be written to the frame-
bu er values may also be read back from the framebu er or copied from
one portion of the framebu er to another. These transfers may include some
type of decoding or encoding.
    This ordering is meant only as a tool for describing the GL, not as a strict
rule of how the GL is implemented, and we present it only as a means to
organize the various operations of the GL. Objects such as curved surfaces,
for instance, may be transformed before they are converted to polygons.

2.5 GL Errors
The GL detects only a subset of those conditions that could be considered
errors. This is because in many cases error checking would adversely impact
the performance of an error-free program.
    The command
      enum GetError( void )

is used to obtain error information. Each detectable error is assigned a
numeric code. When an error is detected, a ag is set and the code is




                                     Version 1.0 - 1 July 1994
12                                   CHAPTER 2. OPENGL OPERATION

recorded. Further errors, if they occur, do not a ect this recorded code.
When GetError is called, the code is returned and the ag is cleared,
so that a further error will again record its code. If a call to GetError
returns NO ERROR, then there has been no detectable error since the last call
to GetError (or since the GL was initialized).
    To allow for distributed implementations, there may be several ag-
code pairs. In this case, after a call to GetError returns a value other
than NO ERROR each subsequent call returns the non-zero code of a distinct
 ag-code pair (in unspeci ed order), until all non-NO ERROR codes have been
returned. When there are no more non-NO ERROR error codes, all ags are
reset. This scheme requires some positive number of pairs of a ag bit and
an integer. The initial state of all ags is cleared and the initial value of all
codes is NO ERROR.
    Table 2.3 summarizes GL errors. Currently, when an error ag is set,
results of GL operation are unde ned only if OUT OF MEMORY has occurred.
In other cases, the command generating the error is ignored so that it has
no e ect on GL state or framebu er contents. If the generating command
returns a value, it returns zero. If the generating command modi es values
through a pointer argument, no change is made to these values. These error
semantics apply only to GL errors, not to system errors such as memory
access errors. This behavior is the current behavior the action of the GL in
the presence of errors is subject to change.
    Two error generation conditions are implicit in the description of every
GL command. First, if a command that requires an enumerated value is
passed an enumerant that is not one of those speci ed as allowable for that
command, the error INVALID ENUM results. This is the case even if the ar-
gument is a pointer to an enumerated value if that value is not allowable
for the given command. Second, if a negative number is provided where an
argument of type sizei is speci ed, the error INVALID VALUE results.

2.6 Begin/End Paradigm
In the GL, most geometric objects are drawn by enclosing a series of coordi-
nate sets that specify vertices and optionally normals, texture coordinates,
and colors between Begin/End pairs. There are ten geometric objects that
are drawn this way: points, line segments, line segment loops, separated
line segments, polygons, triangle strips, triangle fans, separated triangles,
quadrilateral strips, and separated quadrilaterals.




                        Version 1.0 - 1 July 1994
2.6. BEGIN/END PARADIGM                                                    13


   Error                 Description                   O ending com-
                                                       mand ignored?
   INVALID ENUM          enum argument out of range    Yes
   INVALID VALUE         Numeric argument out of Yes
                         range
   INVALID OPERATION     Operation illegal in current Yes
                         state
   STACK OVERFLOW        Command would cause a stack Yes
                         over ow
   STACK UNDERFLOW       Command would cause a stack Yes
                         under ow
   OUT OF MEMORY         Not enough memory left to ex- Unknown
                         ecute command

                     Table 2.3: Summary of GL errors

    Each vertex is speci ed with two, three, or four coordinates. In addition,
a current normal, current texture coordinates, and current color may be used
in processing each vertex. Normals are used by the GL in lighting calcu-
lations the current normal is a three-dimensional vector that may be set
by sending three coordinates that specify it. Texture coordinates determine
how a texture image is mapped onto a primitive.
    A color is associated with each vertex as it is speci ed. This associated
color is either the current color or a color produced by lighting depending on
whether or not lighting is enabled. Texture coordinates are similarly asso-
ciated with each vertex. Figure 2.2 summarizes the association of auxiliary
data with a transformed vertex to produce a processed vertex.
    The current values are part of GL state. Vertices and normals are trans-
formed, colors may be a ected or replaced by lighting, and texture coordi-
nates are transformed and possibly a ected by a texture coordinate genera-
tion function. The processing indicated for each current value is applied for
each vertex that is sent to the GL.
    The methods by which vertices, normals, texture coordinates, and colors
are sent to the GL, as well as how normals are transformed and how vertices
are mapped to the two-dimensional screen, are discussed later.
    Before a color has been assigned to a vertex, the state required by a ver-




                                Version 1.0 - 1 July 1994
14                                           CHAPTER 2. OPENGL OPERATION




                 Vertex
              Coordinates In


                                   vertex / normal             Transformed
                                   transformation
                                                               Coordinates
        Current
        Normal
                                                                                  Processed
                                                                                    Vertex
                                                                                     Out

        Current                              lighting
         Color                                                 Associated
                                                                  Data
                                                               (Color & Texture
                                                                 Coordinates)

        Current
                                                     texture
        Texture           texgen
                                                      matrix
        Coords



     Figure 2.2. Association of current values with a vertex. The heavy lined
     boxes represent GL state.




                           Version 1.0 - 1 July 1994
2.6. BEGIN/END PARADIGM                                                                       15



                                                             Point culling;
                                                             Line Segment
                  Coordinates         Point,                   or Polygon
                                Line Segment, or                Clipping
      Processed
                                    Polygon                                   Rasterization
       Vertices   Associated       (Primitive)
                    Data           Assembly                      Color
                                                              Processing




                                   Begin/End
                                     State



   Figure 2.3. Primitive assembly and processing.


tex is the vertex's coordinates, the current normal, and the current texture
coordinates. Once color has been assigned, however, the current normal
is no longer needed. Because color assignment is done vertex-by-vertex, a
processed vertex comprises the vertex's coordinates, its assigned color, and
its texture coordinates.
    Figure 2.3 shows the sequence of operations that builds a primitive
(point, line segment, or polygon) from a sequence of vertices. After a primi-
tive is formed, it is clipped to a viewing volume. This may alter the primitive
by altering vertex coordinates, texture coordinates, and color. In the case
of a polygon primitive, clipping may insert new vertices into the primitive.
The vertices de ning a primitive to be rasterized have texture coordinates
and color associated with them.

2.6.1 Begin and End Objects
Begin and End require one state variable with eleven values: one value for
each of the ten possible Begin/End objects, and one other value indicating
that no Begin/End object is being processed. The two relevant commands
are
        void       Begin( enum mode )
        void       End( void )




                                               Version 1.0 - 1 July 1994
16                                  CHAPTER 2. OPENGL OPERATION

There is no limit on the number of vertices that may be speci ed between
a Begin and an End.
    Points. A series of individual points may be speci ed by calling Begin
with an argument value of POINTS. No special state need be kept between
Begin and End in this case, since each point is independent of previous
and following points.
    Line Strips. A series of one or more connected line segments is speci ed
by enclosing a series of two or more endpoints within a Begin/End pair
when Begin is called with LINE STRIP. In this case, the rst vertex speci es
the rst segment's start point while the second vertex speci es the rst
segment's endpoint and the second segment's start point. In general, the
ith vertex (for i > 1) speci es the beginning of the ith segment and the end
of the i ; 1st. The last vertex speci es the end of the last segment. If only
one vertex is speci ed between the Begin/End pair, then no primitive is
generated.
    The required state consists of the processed vertex produced from the
last vertex that was sent (so that a line segment can be generated from it
to the current vertex), and a boolean ag indicating if the current vertex is
the rst vertex.
    Line Loops. Line loops, speci ed with the LINE LOOP argument value to
Begin, are the same as line strips except that a nal segment is added from
the nal speci ed vertex to the rst vertex. The additional state consists of
the processed rst vertex.
    Separate Lines. Individual line segments, each speci ed by a pair of
vertices, are generated by surrounding vertex pairs with Begin and End
when the value of the argument to Begin is LINES. In this case, the rst
two vertices between a Begin and End pair de ne the rst segment, with
subsequent pairs of vertices each de ning one more segment. If the number
of speci ed vertices is odd, then the last one is ignored. The state required
is the same as for lines but it is used di erently: a vertex holding the rst
vertex of the current segment, and a boolean ag indicating whether the
current vertex is odd or even (a segment start or end).
    Polygons. A polygon is described by specifying its boundary as a series
of line segments. When Begin is called with POLYGON, the bounding line
segments are speci ed in the same way as line loops. Depending on the
current state of the GL, a polygon may be rendered in one of several ways
such as outlining its border or lling its interior. A polygon described with
fewer than three vertices does not generate a primitive.
    Only convex polygons are guaranteed to be drawn correctly by the GL.




                       Version 1.0 - 1 July 1994
2.6. BEGIN/END PARADIGM                                                               17



   2               4               2                       2
                                              3                                   6
                                                                    4
                                                  4

                                                      5                       5
   1           3          5        1                       1            3

            (a)                         (b)                             (c)

   Figure 2.4. (a) A triangle strip. (b) A triangle fan. (c) Independent triangles.
   The numbers give the sequencing of the vertices between Begin and End.
   Note that the in (a) and (b) triangle edge ordering is determined by the rst
   triangle, while in (c) the order of each triangle's edges is independent of the
   other triangles.


If a speci ed polygon is nonconvex (in particular, if its bounding edges,
when projected onto the window, intersect anywhere other than at common
endpoints), then the rendered polygon need only lie within the convex hull
of the vertices de ning its boundary.
     The state required to support polygons consists of at least two processed
vertices (more than two are never required, although an implementation may
use more) this is because a convex polygon can be rasterized as its vertices
arrive, before all of them have been speci ed. The order of the vertices is sig-
ni cant in lighting and polygon rasterization (see sections 2.12.1 and 3.5.1).
     Triangle strips. A triangle strip is a series of triangles connected along
shared edges. A triangle strip is speci ed by giving a series of de ning ver-
tices between a Begin/End pair when Begin is called with TRIANGLE STRIP.
In this case, the rst three vertices de ne the rst triangle (and their order is
signi cant, just as for polygons). Each subsequent vertex de nes a new tri-
angle using that point along with two vertices from the previous triangle. A
Begin/End pair enclosing fewer than three vertices, when TRIANGLE STRIP
has been supplied to Begin, produces no primitive. See Figure 2.4.
     The state required to support triangle strips consists of a ag indicating
if the rst triangle has been completed, two stored processed vertices, (called
vertex A and vertex B), and a one bit pointer indicating which stored vertex




                                   Version 1.0 - 1 July 1994
18                                   CHAPTER 2. OPENGL OPERATION

will be replaced with the next vertex. After a Begin(TRIANGLE STRIP),
the pointer is initialized to point to vertex A. Each vertex sent between a
Begin/End pair toggles the pointer. Therefore, the rst vertex is stored as
vertex A, the second stored as vertex B, the third stored as vertex A, and
so on. Any vertex after the second one sent forms a triangle from vertex A,
vertex B, and the current vertex (in that order).
    Triangle fans. A triangle fan is the same as a triangle strip with one
exception: each vertex after the rst always replaces vertex B of the two
stored vertices. The vertices of a triangle fan are enclosed between Begin
and End when the value of the argument to Begin is TRIANGLE FAN.
    Separate Triangles. Separate triangles are speci ed by placing ver-
tices between Begin and End when the value of the argument to Begin
is TRIANGLES. In this case, The 3i + 1st, 3i + 2nd, and 3i + 3rd vertices (in
that order) determine a triangle for each i = 0 1 : : : n ; 1, where there are
3n + k vertices between the Begin and End. k is either 0, 1, or 2 if k is not
zero, the nal k vertices are ignored. For each triangle, vertex A is vertex
3i and vertex B is vertex 3i + 1. Otherwise, separate triangles are the same
as a triangle strip.
    The rules given for polygons also apply to each triangle generated from
a triangle strip, triangle fan or from separate triangles.
    Quadrilateral (quad) strips. Quad strips generate a series of edge-
sharing quadrilaterals from vertices appearing between Begin and End,
when Begin is called with QUAD STRIP. If the m vertices between the Begin
and End are v1 : : : vm, where vj is the j th speci ed vertex, then quad i has
vertices (in order) v2i , v2i+1 , v2i+3, and v2i+2 with i = 0 : : : bm=2c. The
state required is thus three processed vertices, to store the last two vertices
of the previous quad along with the third vertex (the rst new vertex) of
the current quad, a ag to indicate when the rst quad has been completed,
and a one-bit counter to count members of a vertex pair. See Figure 2.5.
    A quad strip with fewer than four vertices generates no primitive. If
the number of vertices speci ed for a quadrilateral strip between Begin and
End is odd, the nal vertex is ignored.
    Separate Quadrilaterals Separate quads are just like quad strips ex-
cept that each group of four vertices, the 4j +1st, the 4j +2nd, the 4j +3rd,
and the 4j + 4th, generate a single quad, for j = 0 1 : : : n ; 1. The total
number of vertices between Begin and End is 4n + k, where 0 k 3 if
k is not zero, the nal k vertices are ignored. Separate quads are generated
by calling Begin with the argument value QUADS.
    The rules given for polygons also apply to each quad generated in a quad




                        Version 1.0 - 1 July 1994
2.6. BEGIN/END PARADIGM                                                        19



             2       4        6                 2         3     6   7




             1       3          5               1         4     5   8


                    (a)                                       (b)

   Figure 2.5. (a) A quad strip. (b) Independent quads. The numbers give the
   sequencing of the vertices between Begin and End.


strip or from separate quads.

2.6.2 Polygon Edges
Each edge of each primitive generated from a polygon, triangle strip, triangle
fan, separate triangle set, quadrilateral strip, or separate quadrilateral set,
is agged as either boundary or non-boundary. These classi cations are used
during polygon rasterization some modes a ect the interpretation of poly-
gon boundary edges (see section 3.5.4). By default, all edges are boundary
edges, but the default agging of polygons, separate triangles, or separate
quadrilaterals may be altered by calling
      void   EdgeFlag( boolean ag )
      void   EdgeFlagv( boolean * ag )
to change the value of a ag bit. If ag is zero, then the ag bit is set to
FALSE if ag is non-zero, then the ag bit is set to TRUE,
     When Begin is supplied with one of the argument values POLYGON,
TRIANGLES, or QUADS, each vertex speci ed within a Begin and End pair
begins an edge. If the edge ag bit is TRUE, then each speci ed vertex begins
an edge that is agged as boundary. If the bit is FALSE, then induced edges
are agged as non-boundary.
     The state required for edge agging consists of one current ag bit. Ini-
tially, the bit is TRUE. In addition, each processed vertex of an assembled




                                    Version 1.0 - 1 July 1994
20                                   CHAPTER 2. OPENGL OPERATION

polygonal primitive must be augmented with a bit indicating whether or
not the edge beginning on that vertex is boundary or non-boundary.

2.6.3 GL Commands within Begin/End
The only GL commands that are allowed within any Begin/End pairs are
the commands for specifying vertex coordinates, vertex color, normal coordi-
nates, and texture coordinates (Vertex, Color, Index, Normal, TexCo-
ord), EvalCoord and EvalPoint commands (see section 5.1), commands
for specifying lighting material parameters (Material commands see sec-
tion 2.12.2), display list invocation commands (CallList and CallLists
see section 5.4), and the EdgeFlag command. Executing Begin after Be-
gin has already been executed but before an End is issued generates the
INVALID OPERATION error, as does executing End without a previous corre-
sponding Begin. Executing any other GL command within Begin/End
results in the error INVALID OPERATION.

2.7 Vertex Speci cation
Vertices are speci ed by giving their coordinates in two, three, or four dimen-
sions. This is done using one of several versions of the Vertex command:
      void  Vertexf234gfsifdg( T coords )
      void  Vertexf234gfsifdgv( T coords )
A call to any Vertex command speci es four coordinates: x, y , z , and w.
The x coordinate is the rst coordinate, y is second, z is third, and w is
fourth. A call to Vertex2 sets the x and y coordinates the z coordinate is
implicitly set to zero and the w coordinate to one. Vertex3 sets x, y , and
z to the provided values and w to one. Vertex4 sets all four coordinates,
allowing the speci cation of an arbitrary point in projective three-space.
Invoking a Vertex command outside of a Begin/End pair results in unde-
  ned behavior.
    Current values are used in associating auxiliary data with a vertex as
described in section 2.6. A current value may be changed at any time by
issuing an appropriate command. The commands
      void   TexCoordf1234gfsifdg( T coords )
      void   TexCoordf1234gfsifdgv( T coords )




                        Version 1.0 - 1 July 1994
2.7. VERTEX SPECIFICATION                                                  21

specify the current homogeneous texture coordinates, named s, t, r, and q .
The TexCoord1 family of commands set the s coordinate to the provided
single argument while setting t and r to 0 and q to 1. Similarly, TexCoord2
sets s and t to the speci ed values, r to 0 and q to 1 TexCoord3 sets s, t,
and r, with q set to 1, and TexCoord4 sets all four texture coordinates.
    The current normal is set using
       void Normal3fbsifdg( T coords )
       void Normal3fbsifdgv( T coords )

The current normal is set to the given coordinates whenever one of these
commands is issued. Byte, short, or integer values passed to Normal are
converted to oating-point values as indicated for the corresponding (signed)
type in Table 2.4.
    Finally, there are several ways to set the current color. The GL stores
both a current single-valued color index, and a current four-valued RGBA
color. One or the other of these is signi cant depending as the GL is in color
index mode or RGBA mode. The mode selection is made when the GL is
initialized.
    The command to set RGBA colors is
       void Colorf34gfbsifd ubusuig( T components )
       void Colorf34gfbsifd ubusuigv( T components )

The Color command has two major variants: Color3 and Color4. The
four value versions set all four values. The three value versions set R, G,
and B to the provided values A is set to 1.0. (The conversion of integer
color components (R, G, B, and A) to oating-point values is discussed in
section 2.12.)
    Versions of the Color command that take oating-point values accept
values nominally between 0.0 and 1.0. 0.0 corresponds to the minimum
while 1.0 corresponds to the maximum (machine dependent) value that a
component may take on in the framebu er (see section 2.12 on colors and
coloring). Values outside 0 1] are not clamped.
    The command
       void Indexfsifdg( T index )
       void Indexfsifdgv( T index )

Index updates the current (single-valued) color index. It takes one ar-
gument, the value to which the current color index should be set. Values




                                Version 1.0 - 1 July 1994
22                                  CHAPTER 2. OPENGL OPERATION

outside the (machine-dependent) representable range of color indices are not
clamped.
    The state required to support vertex speci cation consists of four
  oating-point numbers to store the current texture coordinates s, t, r, and
q, three oating-point numbers to store the three coordinates of the current
normal, four oating-point values to store the current RGBA color, and one
  oating-point value to store the current color index. There is no notion of
a current vertex, so no state is devoted to vertex coordinates. The initial
values of s, t, and r of the current texture coordinates are zero the initial
value of q is one. The initial current normal has coordinates (0 0 1). The
initial RGBA color is (R G B A) = (1 1 1 1). The initial color index is 1.

2.8 Rectangles
There is a set of GL commands to support e cient speci cation of rectangles
as two corner vertices.
     void   Rectfsifdg( T x1, T y1, T x2, T y2 )
     void   Rectfsifdgv( T v1 2], T v2 2] )
Each command takes either four arguments organized as two consecutive
pairs of (x y ) coordinates, or two pointers to arrays each of which contains
an x value followed by a y value. The e ect of the Rect command
          Rect (x1 y1 x2 y2)
has exactly the same e ect as the following sequence of commands:
          Begin(POLYGON)
            Vertex2(x1 y1)
            Vertex2(x2 y1)
            Vertex2(x2 y2)
            Vertex2(x1 y2)
          End()
The appropriate Vertex2 command would be invoked depending on which
of the Rect commands is issued.




                       Version 1.0 - 1 July 1994
2.9. COORDINATE TRANSFORMATIONS                                                                       23



                                                                                        Normalized
     Object      Model−View      Eye          Projection      Clip        Perspective     Device
   Coordinates                Coordinates                  Coordinates     Division     Coordinates
                  Matrix                       Matrix




                                                                            Viewport     Window
                                                                         Transformation Coordinates




  Figure 2.6. Vertex transformation sequence.


2.9 Coordinate Transformations
Vertices, normals, and texture coordinates are transformed before their co-
ordinates are used to produce an image in the framebu er. We begin with
a description of how vertex coordinates are transformed and how this trans-
formation is controlled.
    Figure 2.6 diagrams the sequence of transformations that are applied to
vertices. The vertex coordinates that are presented to the GL are termed
object coordinates. The model-view matrix is applied to these coordinates to
yield eye coordinates. Then another matrix, called the projection matrix, is
applied to eye coordinates to yield clip coordinates. A perspective division
is carried out on clip coordinates to yield normalized device coordinates. A
  nal viewport transformation is applied to convert these coordinates into
window coordinates.
    Object coordinates, eye coordinates, and clip coordinates are four-
dimensional, consisting of x, y , z , and w coordinates (in that order). The
model-view and perspective matrices are thus 4 4.
                                                 0 xo 1
                                                 B yo CC and the model-view
   If a vertex in object coordinates is given by B
                                                 @ A                     zo
                                                                         wo




                                            Version 1.0 - 1 July 1994
24                                  CHAPTER 2. OPENGL OPERATION

matrix is M , then the vertex's eye coordinates are found as
                            0 xe 1       0 xo 1
                            BB ye CC     BB yo CC
                             @ A
                              ze     = M  @ A:
                                             zo
                              we             wo
Similarly, if P is the projection matrix, then the vertex's clip coordinates
are                         0x 1 0x 1
                                c             e
                            BB yc CC = P BB ye CC :
                             @ zc A @ ze A
                              wc             we
The vertex's normalized device coordinates are then
                            0 xd 1 0 xc=wc 1
                            @ yd A = @ yc =wc A :
                              zd          zc =wc
2.9.1 Controlling the Viewport
The viewport transformation is determined by the viewport's width and
height in pixels, px and py , respectively, 0and 1its center (ox oy ) (also in
                                                   xw
pixels). The vertex's window coordinates, @ yw A, are given by
                                             zw
                0 xw 1 0           (px=2)xd + ox        1
                @ yw A = @         (py =2)yd + oy       A:
                  zw          (f ; n)=2]zd + (n + f )=2
The factor and o set applied to zd encoded by n and f are set using
     void   DepthRange(      clampd    n, clampd f )
Each of n and f are clamped to lie within 0 1], as are all arguments of type
clampd or clampf. zw is taken to be represented in xed-point with at least
as many bits as there are in the depth bu er of the framebu er. We assume
that the xed-point representation used represents each value k=(2m ; 1),
where k 2 f0 1 : : : 2m ; 1g, as k (e.g. 1.0 is represented in binary as a
string of all ones).
    Viewport transformation parameters are speci ed using




                       Version 1.0 - 1 July 1994
2.9. COORDINATE TRANSFORMATIONS                                                25

      void   Viewport(     int x, int y, sizei     w, sizei h )
where x and y give the x and y window coordinates of the viewport's lower-
left corner and w and h give the viewport's width and height, respectively.
The viewport parameters shown in the above equations are found from these
values as ox = x + w=2 and oy = y + h=2 px = w, py = h.
    Viewport width and height are clamped to implementation-dependent
maximums when speci ed. The maximum width and height may be found
by issuing an appropriate Get command (see Chapter 6). The maximum
viewport dimensions must be greater than or equal to the visible dimensions
of the display being rendered to. INVALID VALUE is generated if either w or h
is negative.
    The state required to implement the viewport transformation is 6 inte-
gers. In the initial state, w and h are set to the width and height, respectively,
of the window into which the GL is to do its rendering. ox and oy are set to
w=2 and h=2, respectively. n and f are set to 0:0 and 1:0, respectively.
2.9.2 Matrices
The projection matrix and model-view matrix are set and modi ed with
a variety of commands. The a ected matrix is determined by the current
matrix mode. The current matrix mode is set with
      void   MatrixMode(       enum   mode )
which takes one of the three pre-de ned constants TEXTURE, MODELVIEW, or
PROJECTION as the argument value. TEXTURE is described later. If the current
matrix mode is MODELVIEW, then matrix operations apply to the model-view
matrix if PROJECTION, then they apply to the projection matrix.
   The two basic commands for a ecting the current matrix are
         LoadMatrixffdg( T m 16] )
      void
         MultMatrixffdg( T m 16] )
      void

LoadMatrix takes a pointer to a 4 4 matrix stored in column-major order
as 16 consecutive oating-point values, i.e. as
                            0 a1 a5 a9 a13 1
                            BB a2 a6 a10 a14 CC :
                             @ a3 a7 a11 a15 A
                              a4 a8 a12 a16




                                 Version 1.0 - 1 July 1994
26                                   CHAPTER 2. OPENGL OPERATION

(This di ers from the standard row-major C ordering for matrix elements. If
the standard ordering is used, all of the subsequent transformation equations
are transposed, and the columns representing vectors become rows.)
    The speci ed matrix replaces the current matrix with the one pointed to.
MultMatrix takes the same type argument as LoadMatrix, but multiplies
the current matrix by the one pointed to and replaces the current matrix
with the product. If C is the current matrix and M is the matrix pointed
to by MultMatrix's argument, then the resulting current matrix, C 0, is
                                 C 0 = C M:

     The command
      void  LoadIdentity( void )
e ectively calls LoadMatrix with the identity matrix:
                           01 0 0 01
                           BB 0 1 0 0 CC
                            @            A:
                                    0 0 1 0
                                    0 0 0 1
    There are a variety of other commands that manipulate matrices. Ro-
tate, Translate, Scale, Frustum, and Ortho manipulate the current ma-
trix. Each computes a matrix and then invokes MultMatrix with this
matrix. In the case of
       void Rotateffdg( T , T x, T y, T z )

  gives an angle of rotation in degrees the coordinates of a vector v are given
by v = (x y z )T . The computed matrix is a counter-clockwise rotation about
the line through the origin with the speci ed axis when that axis is pointing
up (i.e. the right-hand rule determines the sense of the rotation angle). The
matrix is thus                  0           01
                                BB R        0CC
                                 @          0A:
                                    0 0 0 1
Let u = v=jjvjj = ( x y z ) . If
                      0    0     0 T
                                   0 0 ;z0 y0 1
                             S = @ z0 0 ;x0 A
                                     ;y0 x0 0




                        Version 1.0 - 1 July 1994
2.9. COORDINATE TRANSFORMATIONS                                                 27

then
                     R = uuT + cos (I ; uuT ) + sin S:
   The arguments to
       void   Translateffdg( T x, T y, T z )
give the coordinates of a translation vector as (x y z )T . The resulting matrix
is a translation by the speci ed vector:
                                01 0 0 x1
                                BB 0 1 0 y CC
                                 @0 0 1 z A:
                                   0 0 0 1
       void   Scaleffdg( T x, T y, T z )
produces a general scaling along the x-, y -, and z - axes. The corresponding
matrix is                    0x 0 0 01
                             BB 0 y 0 0 CC :
                              @0 0 z 0A
                                0 0 0 1
   For
       void   Frustum(     double l, double r, double          b,   double t,
          double   n, double f )
the coordinates (l b ; n)T and (r t ; n)T specify the points on the near
clipping plane that are mapped to the lower-left and upper-right corners of
the window, respectively (assuming that the eye is located at (0 0 0)T ). f
gives the distance from the eye to the far clipping plane. If either n or f is less
than or equal to zero, the error INVALID VALUE results. The corresponding
matrix is              0 2n 0 r+l
                           r;l          r;l       0 1
                       BB 0 t2;nb tt+;bb          0 C C:
                        B@                        2fn C
                            0 0 ; f ;n ; f ;n A
                                         f +n

                            0 0         ;1 0
       void   Ortho(    double l, double         r,   double   b,   double t,
          double   n, double f )




                                   Version 1.0 - 1 July 1994
28                                  CHAPTER 2. OPENGL OPERATION

describes a matrix that produces parallel projection. (l b ;n)T and (r t ;n)T
specify the points on the near clipping plane that are mapped to the lower-
left and upper-right corners of the window, respectively. f gives the distance
from the eye to the far clipping plane. The corresponding matrix is
                       0 2 0           0      ; rr+;ll 1
                           r;l
                       BB 0 t;2 b 0 ; tt+;bb CC
                        B@                             C:
                            0 0 ; f ;2 n ; ff ;+nn A
                            0 0        0        1
     There is another 4 4 matrix that is applied to texture coordinates. This
matrix is applied as
                      0 m1 m5 m9 m13 1 0 s 1
                      B
                      B m2 m6 m10 m14 C B t C
                      @ m3 m7 m11 m15 CA B@ r CA
                        m4 m8 m12 m16              q
where the left matrix is the current texture matrix. The matrix is applied
to the coordinates resulting from texture coordinate generation (which may
simply be the current texture coordinates), and the resulting transformed co-
ordinates become the texture coordinates associated with a vertex. Setting
the matrix mode to TEXTURE causes the already described matrix operations
to apply to the texture matrix.
    There is a stack of matrices for each of the matrix modes. For MODELVIEW
mode, the stack depth is at least 32 (that is, there is a stack of at least 32
model-view matrices). For the other modes, the depth is at least 2. The
current matrix in any mode is the matrix on the top of the stack for that
mode.
      void PushMatrix( void )

pushes the stack down by one, duplicating the current matrix in both the
top of the stack and the entry below it.
      void PopMatrix( void )

pops the top entry o of the stack, replacing the current matrix with the
matrix that was the second entry in the stack. The pushing or popping takes
place on the stack corresponding to the current matrix mode. Popping a
matrix o a stack with only one entry generates the error STACK UNDERFLOW
pushing a matrix onto a full stack generates STACK OVERFLOW.




                       Version 1.0 - 1 July 1994
2.9. COORDINATE TRANSFORMATIONS                                             29

    The state required to implement transformations consists of a three-
valued integer indicating the current matrix mode, a stack of at least two
4 4 matrices for each of PROJECTION and TEXTURE with associated stack
pointers, and a stack of at least 32 4 4 matrices with an associated stack
pointer for MODELVIEW. Initially, there is only one matrix on each stack, and
all matrices are set to the identity. The initial matrix mode is MODELVIEW.

2.9.3 Normal Transformation
Finally, we consider how the model-view matrix a ects normals. Normals
are of interest only in eye coordinates, so the rules governing their transfor-
mation to other coordinate systems are not examined.
    Normals sent to the GL may or may not have unit length. If normal-
ization is enabled, then normals speci ed with the Normal3 command are
normalized after transformation. Normalization is controlled with
      void   Enable(    enum   target )
and
      void   Disable(   enum   target )
with target equal to NORMALIZE. This requires one bit of state. The initial
state is for normals not to be normalized.
    A normal at a point de nes 0a plane
                                      1 at that point. If the normal is
                                          x
                              B y CC, then for the point to satisfy the
( nx ny nz ) and the point is B
                              @zA
                                          w
plane equation we must have
                                       0x1
                                       B y CC = 0
                        ( nx ny nz q ) B
                                       @zA
                                                  w
whence                                0x1
                        ;( nx ny nz ) @ y A
                   q=                         z          w 6= 0
                                    w




                                  Version 1.0 - 1 July 1994
30                                    CHAPTER 2. OPENGL OPERATION

or q = 0 if w = 0. Therefore, if the model-view matrix is M , then the
transformed plane equation is
              ( nx 0 ny 0 nz 0 q 0 ) = ( nx ny nz q ) M ;1
and the transformed normal is
                                               0 nx0 1
                        q         1            @ ny 0 A :                (2:1)
                          nx0 2 + ny 0 2 + nz 02 nz 0
If normalization is disabled, then the square root in equation 2.1 is replaced
with 1. Otherwise, the square root remains as written.
    Because we specify neither the oating-point format nor the means
for matrix inversion, we cannot specify behavior in the case of a poorly-
conditioned (nearly singular) model-view matrix M . In case of an exactly
singular matrix, the transformed normal is unde ned. If the GL implementa-
tion determines that the model-view matrix is uninvertible, then the entries
in the inverted matrix are arbitrary. In any case, neither normal transfor-
mation nor use of the transformed normal may lead to GL interruption or
termination.

2.9.4 Generating texture coordinates
Texture coordinates associated with a vertex may either be taken from the
current texture coordinates or generated according to a function dependent
on vertex coordinates. The command
     void   TexGenfifdg( enum coord, enum pname, T param )
     void   TexGenfifdgv( enum coord, enum pname, T params )
controls texture coordinate generation. coord must be one of the constants
S, T, R, or Q, indicating that the pertinent coordinate is the s, t, r, or q
coordinate, respectively. In the rst form of the command, params is a
pointer to an array of values that specify texture generation parameters in
the second form, params must be a value specifying a single-valued texture
generation parameter. pname must be one of the three symbolic constants
TEXTURE GEN MODE, OBJECT PLANE, or EYE PLANE. If pname is TEXTURE GEN MODE,
then either params points to or params is an integer that is one of the
symbolic constants OBJECT LINEAR, EYE LINEAR, or SPHERE MAP.




                       Version 1.0 - 1 July 1994
2.9. COORDINATE TRANSFORMATIONS                                             31

    If TEXTURE GEN MODE indicates OBJECT LINEAR, then the generation function
for the coordinate indicated by coord is
                       g = p1xo + p2yo + p3 zo + p4wo :
xo , yo , zo , and wo are the object coordinates of the vertex. p1 : : : p4 are
speci ed by calling TexGen with pname set to OBJECT PLANE in which case
params points to an array containing p1 : : : p4. There is a distinct group of
plane equation coe cients for each texture coordinate coord indicates the
coordinate to which the speci ed coe cients pertain.
   If TEXTURE GEN MODE indicates EYE LINEAR, then the function is
                       g = p01xe + p02ye + p03ze + p04we
where
                  ( p01 p02 p03 p04 ) = ( p1 p2 p3 p4 ) M ;1
xe , ye , ze , and we are the eye coordinates of the vertex. p1 : : : p4 are
set by calling TexGen with pname set to EYE PLANE in correspondence with
setting the coe cients in the OBJECT PLANE case. M is the model-view matrix
in e ect when p1 : : : p4 are speci ed. Computed texture coordinates may
be inaccurate or unde ned if M is poorly conditioned or singular.
     When used with a suitably constructed texture image, calling TexGen
with TEXTURE GEN MODE indicating SPHERE MAP can simulate the re ected im-
age of a spherical environment on a polygon. SPHERE MAP texture coordinates
are generated as follows. Denote the unit vector pointing from the origin to
the vertex (in eye coordinates) by u. Denote the current normal, after trans-
formation to eye coordinates, by n0 . Let r = ( rx ry rz )T , the re ection
vector, be given by
                                r = u ; 2n0n0T u
               q
and let m = 2 rx2 + ry2 + (rz + 1)2 . Then the value assigned to an s coor-
dinate (the rst TexGen argument value is S) is s = rx=m + 21 the value
assigned to a t coordinate is t = ry =m + 21 . Calling TexGen with a co-
ord of either R or Q when pname indicates SPHERE MAP generates the error
INVALID ENUM.
    A texture coordinate generation function is enabled or disabled using
Enable and Disable with an argument of TEXTURE GEN S, TEXTURE GEN T,
TEXTURE GEN R, or TEXTURE GEN Q (each indicates the corresponding texture
coordinate). When enabled, the speci ed texture coordinate is computed




                                Version 1.0 - 1 July 1994
32                                    CHAPTER 2. OPENGL OPERATION

according to the current EYE LINEAR, OBJECT LINEAR or SPHERE MAP speci ca-
tion, depending on the current setting of TEXTURE GEN MODE for that coordi-
nate. When disabled, subsequent vertices will take the indicated texture
coordinate from the current texture coordinates.
    The state required for texture coordinate generation comprises a three-
valued integer for each coordinate indicating coordinate generation mode,
and a bit for each coordinate to indicate whether texture coordinate genera-
tion is enabled or disabled. In addition, four coe cients are required for the
four coordinates for each of EYE LINEAR and OBJECT LINEAR. The initial state
has the texture generation function disabled for all texture coordinates. The
initial values of pi for s are all 0 except p1 which is one for t all the pi are
zero except p2 , which is 1. The values of pi for r and q are all 0. These values
of pi apply for both the EYE LINEAR and OBJECT LINEAR versions. Initially all
texture generation modes are EYE LINEAR.

2.10 Clipping
Primitives are clipped to the clip volume. In clip coordinates, the view
volume is de ned by
                                ;wc     xc wc
                                ;wc     yc wc :
                                ;wc     zc wc
This view volume may be further restricted by as many as n client-de ned
clip planes to generate the clip volume. (n is an implementation dependent
maximum that must be at least 6.) Each client-de ned plane speci es a
half-space. The clip volume is the intersection of all such half-spaces with
the view volume (if there no client-de ned clip planes are enabled, the clip
volume is the view volume).
    A client-de ned clip plane is speci ed with
      void ClipPlane( enum p, double eqn 4] )

The value of the rst argument, p, is a symbolic constant, CLIP PLANEi, where
i is an integer between 0 and n ; 1, indicating one of n client-de ned clip
planes. eqn is an array of four double-precision oating-point values. These
are the coe cients of a plane equation in object coordinates: p1 , p2 , p3 , and
p4 (in that order). The inverse of the current model-view matrix is applied
to these coe cients, at the time they are speci ed, yielding
                ( p01 p02 p03 p04 ) = ( p1 p2 p3 p4 ) M ;1




                        Version 1.0 - 1 July 1994
2.10. CLIPPING                                                                33

(where M is the current model-view matrix the resulting plane equation is
unde ned if M is singular and may be inaccurate if M is poorly-conditioned)
to obtain the plane equation coe cients in eye coordinates. All points with
eye coordinates ( xe ye ze we )T that satisfy
                                            0 xe 1
                                            B ye CC 0
                        ( p01 p02 p03 p04 ) B
                                            @ ze A
                                               we
lie in the half-space de ned by the plane points that do not satisfy this
condition do not lie in the half-space.
    Client-de ned clip planes are enabled with the generic Enable com-
mand and disabled with the Disable command. The value of the argument
to either command is CLIP PLANEi where i is an integer between 0 and n
specifying a value of i enables or disables the plane equation with index i.
The constants obey CLIP PLANEi = CLIP PLANE0 + i.
    If the primitive under consideration is a point, then clipping passes it
unchanged if it lies within the clip volume otherwise, it is discarded. If the
primitive is a line segment, then clipping does nothing to it if it lies entirely
within the clip volume and discards it if it lies entirely outside the volume.
If part of the line segment lies in the volume and part lies outside, then the
line segment is clipped and new vertex coordinates are computed for one or
both vertices. A clipped line segment endpoint lies on both the original line
segment and the boundary of the clip volume.
    This clipping produces a value, 0 t 1, for each clipped vertex. If the
coordinates of a clipped vertex are P and the original vertices' coordinates
are P1 and P2 , then t is given by
                             P = tP1 + (1 ; t)P2:
The value of t is used in color and texture coordinate clipping (sec-
tion 2.12.8).
     If the primitive is a polygon, then it is passed if every one of its edges
lies entirely inside the clip volume and either clipped or discarded otherwise.
Polygon clipping may cause polygon edges to be clipped, but because poly-
gon connectivity must be maintained, these clipped edges are connected by
new edges that lie along the clip volume's boundary. Thus, clipping may
require the introduction of new vertices into a polygon. Edge ags are asso-
ciated with these vertices so that edges introduced by clipping are agged




                                 Version 1.0 - 1 July 1994
34                                   CHAPTER 2. OPENGL OPERATION

as boundary (edge ag TRUE), and so that original edges of the polygon that
become cut o at these vertices retain their original ags.
    If it happens that a polygon intersects an edge of the clip volume's
boundary, then the clipped polygon must include a point on this boundary
edge. This point must lie in the intersection of the boundary edge and
the convex hull of the vertices of the original polygon. We impose this
requirement because the polygon may not be exactly planar.
    A line segment or polygon whose vertices have wc values of di ering signs
may generate multiple connected components after clipping. GL implemen-
tations are not required to handle this situation. That is, only the portion of
the primitive that lies in the region of wc > 0 need be produced by clipping.
    Primitives rendered with clip planes must satisfy a complementarity cri-
terion. Suppose a single clip plane with coe cients ( p01 p02 p03 p04 ) (or a
number of similarly speci ed clip planes) is enabled and a series of primitives
are drawn. Next, suppose that the original clip plane is respeci ed with co-
e cients ( ;p01 ;p02 ;p03 ;p04 ) (and correspondingly for any other clip
planes) and the primitives are drawn again (and the GL is otherwise in the
same state). In this case, primitives must not be missing any pixels, nor
may any pixels be drawn twice in regions where those primitives are cut by
the clip planes.
    Clipping requires at least 6 sets of plane equations (each consisting of
four double-precision oating-point coe cients) and at least 6 corresponding
bits indicating which of these client-de ned plane equations are enabled. In
the initial state, all client-de ned plane equation coe cients are zero and
all planes are disabled.

2.11 Current Raster Position
The current raster position is used by commands that directly a ect pixels in
the framebu er. These commands, which bypass vertex transformation and
primitive assembly, are described in the next chapter. The current raster
position, however, shares some of the characteristics of a vertex.
    The current raster position consists of three window coordinates xw , yw ,
and zw , a clip coordinate wc value, an eye coordinate distance, a valid bit,
and associated data consisting of a color and texture coordinates. It is set
using one of the RasterPos commands:
      void RasterPosf234gfsifdg( T coords )
      void RasterPosf234gfsifdgv( T coords )




                        Version 1.0 - 1 July 1994
2.11. CURRENT RASTER POSITION                                               35

RasterPos4 takes four values indicating x, y, z, and w. RasterPos3 (or
RasterPos2) is analogous, but sets only x, y, and z with w implicitly set
to 1 (or only x and y with z implicitly set to 0 and w implicitly set to 1).
    The coordinates are treated as if they were speci ed in a Vertex com-
mand. The x, y , z , and w coordinates are transformed by the current
model-view and perspective matrices. These coordinates, along with cur-
rent values, are used to generate a color and texture coordinates just as is
done for a vertex. The color and texture coordinates so produced replace the
color and texture coordinates stored in the current raster position's associ-
ated data. The distance from the origin of the eye coordinate system to the
vertex as transformed by only the current model-view matrix replaces the
current raster distance. This distance can be approximated (see section 3.9).
    The transformed coordinates are passed to clipping as if they represented
a point. If the \point" is not culled, then the projection to window coor-
dinates is computed (section 2.9) and saved as the current raster position,
and the valid bit is set. If the \point" is culled, the current raster position
and its associated data become indeterminate and the valid bit is cleared.
Figure 2.7 summarizes the behavior of the current raster position.
    The current raster position requires ve single-precision oating-point
values for its xw , yw , and zw window coordinates, its wc clip coordinate,
and its eye coordinate distance, a single valid bit, a color (RGBA and color
index), and texture coordinates for associated data. In the initial state, the
coordinates and texture coordinates are both (0 0 0 1), the eye coordinate
distance is 0, the valid bit is set, the associated RGBA color is (1 1 1 1)
and the associated color index color is 1. In RGBA mode, the associated
color index always has its initial value in color index mode, the RGBA color
always maintains its initial value.




                                Version 1.0 - 1 July 1994
36                                         CHAPTER 2. OPENGL OPERATION




                       Rasterpos In


                                                           Raster
                          vertex                          Position
                      transformation



                           clip        project
                                                           Valid
         Current
          Color
                            lighting
                                                        Associated
                                                           Data
         Current            TexGen
         Texture                                                     Current
       Coodinatese                                                    Raster
                                                                     Position


     Figure 2.7. The current raster position and how it is set.




                           Version 1.0 - 1 July 1994
2.12. COLORS AND COLORING                                                                    37


        [0,2n−1]        Convert to
     Color                float
     Index
       [0.0,2n−1]

                        Convert to
        [0,2k−1]                             Current   Current
                         [0.0,1.0]
                                             RGBA       Color
     RGBA                                     Color     Index        Color     Mask to
                        Convert to                                   Index     [0.0, 2n−1]
   [−2k−1,2k−1]
                        [−1.0,1.0]

        [0.0,1.0]                                                              Clamp to
                                                                     RGBA      [0.0, 1.0]
                                                 Lighting




                                                          Color
                                                         Clipping
                Color
                Index                RGBA

                 Convert to     Convert to
                fixed−point    fixed−point                                   Flatshade?
                                                         Primitive
                                                         Clipping




   Figure 2.8. Processing of colors. n is the number of bits in a color index
   m is the number of bits an R, G, B, or A component. See Table 2.4 for the
   interpretation of k.


2.12 Colors and Coloring
    Figure 2.8 diagrams the processing of colors before rasterization. In-
coming colors arrive in one of several formats. Table 2.4 summarizes the
conversions that take place on R, G, B, and A components depending on
which version of the Color command was invoked to specify the compo-
nents. As a result of limited precision, some converted values will not be
represented exactly. In color index mode, a single-valued color index is not
mapped.
    Next, lighting, if enabled, produces a color. If lighting is disabled, the
current color is used in further processing. After lighting, RGBA colors
are clamped to the range 0 1]. A color index is converted to xed-point




                                       Version 1.0 - 1 July 1994
38                                   CHAPTER 2. OPENGL OPERATION

        Command Element Type             Conversion Formula
        Colorub Unsigned 8-bit integer        c=(28 ; 1)
         Colorb Signed 8-bit integer      (2c + 1)=(28 ; 1)
        Colorus Unsigned 16-bit integer       c=(216 ; 1)
         Colors Signed 16-bit integer     (2c + 1)=(216 ; 1)
         Colorui Unsigned 32-bit integer      c=(232 ; 1)
         Colori Signed 32-bit integer     (2c + 1)=(232 ; 1)
         Colorf Floating-point                     c
Table 2.4: RGBA Color component conversions. The leftmost column indi-
cates the correspondence between color setting commands and conversions.
c represents the value of the component to be converted.

and then its integer portion is masked (see section 2.12.6). After clamping
or masking, a primitive may be atshaded, indicating that all vertices of
the primitive are to have the same color. Finally, if a primitive is clipped,
then colors (and texture coordinates) must be computed at the vertices
introduced or modi ed by clipping.
2.12.1 Lighting
GL lighting computes a color for each vertex sent to the GL. This is accom-
plished by applying an equation de ned by a client-speci ed lighting model
to a collection of parameters that can include the vertex coordinates, the
coordinates of one or more light sources, the current normal, and parameters
de ning the characteristics of the light sources and a current material. The
following discussion assumes that the GL is in RGBA mode. (Color index
lighting is described in section 2.12.5.)
     Lighting may be in one of two states:
    1. Lighting O . In this state the color assigned to a vertex is the current
       color.
    2. Lighting On. In this state, a vertex's color is found by computing a
       value given the current lighting parameters.
Lighting is turned either on or o using the generic Enable or Disable
commands with the symbolic value LIGHTING.




                        Version 1.0 - 1 July 1994
2.12. COLORS AND COLORING                                                        39

Lighting Operation
A lighting parameter is of one of ve types: color, position, direction, real,
or boolean. A color parameter consists of four oating-point elements, one
for each of R, G, B, and A, in that order. There are no restrictions on
the allowable values for these parameters. A position parameter consists
of four oating-point coordinates (x, y , z , and w) that specify a position
in object coordinates (w may, in some cases, be zero, indicating a point at
in nity in the direction given by x, y , and z ). A direction parameter consists
of three oating-point coordinates (x, y , and z ) that specify a direction in
object coordinates. A real parameter is one oating-point value. The various
values and their types are summarized in Table 2.5. The result of a lighting
computation is unde ned if a value for a parameter is speci ed that is outside
the range given for that parameter in the table.
    There are n light sources, indexed by i = 0 : : : n ; 1. (n is an implemen-
tation dependent maximum that must be at least 8.) Note that the default
values for dcli and scli di er for i = 0 and i > 0.
    Before specifying the way that lighting computes colors, we introduce
operators and notation that simplify the expressions involved. If c1 and
c2 are colors without alpha where c1 = (r1 g1 b1) and c2 = (r2 g2 b2),
then de ne c1 c2 = (r1r2 g1g2 b1b2). Addition of colors is accomplished
by addition of the components. Multiplication of colors by a scalar means
multiplying each component by that scalar. If d1 and d2 are directions, then
de ne
                           d1 d2 = maxfd1 d2 0g:
(Directions are taken to have three coordinates.) If P1 and P2 are (homoge-
neous, with four coordinates) points then let ;;;!  P1P2 be the unit vector that
points from P1 to P2 . Note that if P2 has a zero w coordinate and P1 has
non-zero w coordinate, then ;;;! P1P2 is the unit vector corresponding to the
direction speci ed by the x, y , and z coordinates of P2 if P1 has a zero w
coordinate and P2 has a non-zero w coordinate then ;;;!    P1P2 is the unit vector
that is the negative of that corresponding to the direction speci ed by P1.
If both P1 and P2 have zero w coordinates, then ;;;!     P1P2 is the unit vector
obtained by normalizing the direction corresponding to P2 ; P1.
    If d is an arbitrary direction, then let d^ be the unit vector in d's direction.
Let kP1P2k be the distance between P1 and P2. Finally, let V be the point
corresponding to the vertex being lit, and n be the corresponding normal.
Let Pe be the eyepoint ((0 0 0 1) in eye coordinates).




                                  Version 1.0 - 1 July 1994
40                                  CHAPTER 2. OPENGL OPERATION

 Parameter Type             Default Value          Description
 Material Parameters
    acm        color      (0:2   0:2 0:2   1:0)    ambient color of material
    dcm        color      (0:8   0:8 0:8   1:0)    di use color of material
    scm        color      (0:0   0:0 0:0   1:0)    specular color of material
    ecm        color      (0:0   0:0 0:0   1:0)    emissive color of material
    srm         real               0.0             specular exponent (range:
                                                    0:0 128:0])
     am          real         0:0                  ambient color index
     dm          real         1:0                  di use color index
     sm          real         1:0                  specular color index
 Light Source Parameters
     acli       color (0:0 0:0 0:0 1:0)            ambient intensity of light i
 dcli(i = 0) color (1:0 1:0 1:0 1:0)               di use intensity of light 0
 dcli(i > 0) color (0:0 0:0 0:0 1:0)               di use intensity of light i
 scli(i = 0) color (1:0 1:0 1:0 1:0)               specular intensity of light 0
 scli(i > 0) color (0:0 0:0 0:0 1:0)               specular intensity of light i
     Ppli     position (0:0 0:0 1:0 0:0)           position of light i
     sdli     direction (0:0 0:0 ;1:0)             direction of spotlight for light
                                                   i
     srli       real              0.0              spotlight exponent for light i
                                                   (range: 0:0 128:0])
     crli       real             180.0             spotlight cuto angle for
                                                   light i (range: 0:0 90:0],
                                                   180:0)
     k0i        real              1.0              constant attenuation factor
                                                   for light i (range: 0:0 1))
     k1i        real              0.0              linear attenuation factor for
                                                   light i (range: 0:0 1))
     k2i        real              0.0              quadratic attenuation factor
                                                   for light i (range: 0:0 1))
 Lighting Model Parameters
    acs        color (0:2 0:2 0:2 1:0) ambient color of scene
     vbs     boolean       FALSE       viewer assumed to be at
                                       (0 0 0) in eye coordinates
                                       (TRUE) or (0 0 1) (FALSE)
     tbs     boolean       FALSE       use two-sided lighting mode
Table 2.5: Summary of lighting parameters. The range of individual color
components is (;1 +1).




                       Version 1.0 - 1 July 1994
2.12. COLORS AND COLORING                                               41

   The color c produced by lighting a vertex is given by
             c = ecm
               + acm acs
                 nX
                  ;1
                 +         (atti )(spoti ) acm acli
                     i=0             + (n ;!  VPpli)dcm dcli
                                     + (fi)(n h^ i )srm scm scli ]
where
             (
     fi =        1 n ;!VPpli 6= 0                                     (2.2)
                 0 otherwise,

          8 ;! ;!
          < pli + VPe
     hi = : VP
            ;!               T
                               vbs = TRUE                             (2.3)
            VPpli + ( 0 0 1 ) vbs = FALSE

          8
          < k0i + k1ikVPpli1k + k2ikVPplik2 if Ppli's w 6= 0,
          >
   atti = >                                                   (2.4)
          :              1:0                otherwise,

          8 ;;;!                             ;;;!
          < (PpliV ^sdli)srli crli 6= 180:0 P;;;!
          >                                   pli V ^sdli cos(crli)
  spoti = >
          :       0:0         crli 6= 180:0 PpliV ^sdli < cos(crli)(2.5)
                  1:0         crli = 180:0:
All computations are carried out in eye coordinates.
    The value of A produced by lighting is the alpha value associated with
dcm . Results of lighting are unde ned if the we coordinate (w in eye coor-
dinates) of V is zero.
    Lighting may operate in two-sided mode (tbs = TRUE), in which a front
color is computed with one set of material parameters (the front material)
and a back color is computed with a second set of material parameters (the
back material). This second computation replaces n with ;n. If tbs = FALSE,




                                  Version 1.0 - 1 July 1994
42                                      CHAPTER 2. OPENGL OPERATION

then the back color and front color are both assigned the color computed
using the front material with n.
    The selection between back color and front color depends on the primitive
of which the vertex being lit is a part. If the primitive is a point or a line
segment, the front color is always selected. If it is a polygon, then the
selection is based on the sign of the (clipped or unclipped) polygon's signed
area computed in window coordinates. One way to compute this area is
                                  nX
                         a = 21
                                   ;1
                                        xiw ywi 1 ; xiw 1 ywi             (2:6)
                                  i=0
where xiw and ywi are the x and y window coordinates of the ith vertex of
the n-vertex polygon (vertices are numbered starting at zero for purposes of
this computation) and i 1 is (i + 1) mod n. The interpretation of the sign
of this value is controlled with
       void FrontFace( enum dir )

Setting dir to CCW (corresponding to counter-clockwise orientation of the
projected polygon in window coordinates) indicates that if a 0, then the
color of each vertex of the polygon becomes the back color computed for
that vertex while if a > 0, then the front color is selected. If dir is CW, then
a is replaced by ;a in the above inequalities. This requires one bit of state
initially, it indicates CCW.
2.12.2 Lighting Parameter Speci cation
Lighting parameters are divided into three categories: material parameters,
light source parameters, and lighting model parameters (see Table 2.5). Sets
of lighting parameters are speci ed with
       void Materialfifg( enum face, enum pname, T param )
       void Materialfifgv( enum face, enum pname, T params )
       void Lightfifg( enum light, enum pname, T param )
       void Lightfifgv( enum light, enum pname, T params )
       void LightModelfifg( enum pname, T param )
       void LightModelfifgv( enum pname, T params )

pname is a symbolic constant indicating which parameter is to be set (see
Table 2.6). In the vector versions of the commands, params is a pointer to
a group of values to which to set the indicated parameter. The number of




                        Version 1.0 - 1 July 1994
2.12. COLORS AND COLORING                                                  43

values pointed to depends on the parameter being set. In the non-vector
versions, param is a value to which to set a single-valued parameter. (If
param corresponds to a multi-valued parameter, the error INVALID ENUM re-
sults.) For the Material command, face must be one of FRONT, BACK, or
FRONT AND BACK, indicating that the property name of the front or back ma-
terial, or both, respectively, should be set. In the case of Light, light is a
symbolic constant of the form LIGHTi, indicating that light i is to have the
speci ed parameter set. The constants obey LIGHTi = LIGHT0 + i.
    Table 2.6 gives, for each of the three parameter groups, the correspon-
dence between the pre-de ned constant names and their names in the light-
ing equations, along with the number of values that must be speci ed with
each. Color parameters speci ed with Material and Light are converted
to oating-point values (if speci ed as integers) as indicated in Table 2.4
for signed integers. The error INVALID VALUE occurs if a speci ed lighting
parameter lies outside the allowable range given in Table 2.5. (The sym-
bol \1" indicates the maximum representable magnitude for the indicated
type.)
    The current model-view matrix is applied to the position parameter indi-
cated with Light for a particular light source when that position is speci ed.
These transformed values are the values used in the lighting equation. The
spotlight direction is transformed when it is speci ed into a value of sdli
using the rules given for transforming normals at the end of section 2.9.3.
    An individual light is enabled or disabled by calling Enable or Disable
with the symbolic value LIGHTi (i is in the range 0 to n ; 1, where n is the
implementation-dependent number of lights). If light i is disabled, the ith
term in the lighting equation is e ectively removed from the summation.
2.12.3 ColorMaterial
    It is possible to attach one or more material properties to the current
color, so that they continuously track its component values. This behavior
is enabled and disabled by calling Enable or Disable with the symbolic
value COLOR MATERIAL.
    The command that controls which of these modes is selected is
      void ColorMaterial( enum face, enum mode )

face is one of FRONT, BACK, or FRONT AND BACK, indicating whether the front
material, back material, or both are a ected by the current color. mode
is one of EMISSION, AMBIENT, DIFFUSE, SPECULAR, or AMBIENT AND DIFFUSE and




                                Version 1.0 - 1 July 1994
44                               CHAPTER 2. OPENGL OPERATION




       Parameter            Name                Number of values
       Material Parameters (Material)
         acm               AMBIENT                     4
         dcm               DIFFUSE                     4
       acm dcm       AMBIENT AND DIFFUSE               4
         scm              SPECULAR                     4
         ecm              EMISSION                     4
          srm             SHININESS                    1
       am dm sm         COLOR INDEXES                  3
       Light Source Parameters (Light)
          acli             AMBIENT                     4
          dcli             DIFFUSE                     4
          scli            SPECULAR                     4
          Ppli            POSITION                     4
          sdli         SPOT DIRECTION                  3
          srli          SPOT EXPONENT                  1
          crli           SPOT CUTOFF                   1
          k0        CONSTANT ATTENUATION               1
          k1         LINEAR ATTENUATION                1
          k2        QUADRATIC ATTENUATION              1
       Lighting Model Parameters (LightModel)
          acs        LIGHT MODEL AMBIENT               4
          vbs      LIGHT MODEL LOCAL VIEWER            1
          tbs        LIGHT MODEL TWO SIDE              1

Table 2.6: Correspondence of lighting parameter symbols to names.
AMBIENT AND DIFFUSE is used to set acm and dcm to the same value.




                    Version 1.0 - 1 July 1994
2.12. COLORS AND COLORING                                                                                                    45




                         Current
  Color*()                                                     To subsequent vertex operations
                         Color



                                                          Up while ColorMaterial face is FRONT or FRONT_AND_BACK,
                                                          and ColorMaterial mode is AMBIENT or AMBIENT_AND_DIFFUSE,
                                                          and ColorMaterial is enabled. Down otherwise.

                                                                        Front Ambient
                                                                                                     To lighting equations
  Material*(FRONT,AMBIENT)                                              Color


                                                          Up while ColorMaterial face is FRONT or FRONT_AND_BACK,
                                                          and ColorMaterial mode is DIFFUSE or AMBIENT_AND_DIFFUSE,
                                                          and ColorMaterial is enabled. Down otherwise.

                                                                        Front Diffuse
                                                                                                     To lighting equations
  Material*(FRONT,DIFFUSE)                                              Color


                                                          Up while ColorMaterial face is FRONT or FRONT_AND_BACK,
                                                          and ColorMaterial mode is SPECULAR, and ColorMaterial is
                                                          enabled. Down otherwise.

                                                                        Front Specular
                                                                                                     To lighting equations
  Material*(FRONT,SPECULAR)                                             Color


                                                          Up while ColorMaterial face is FRONT or FRONT_AND_BACK,
                                                          and ColorMaterial mode is EMISSION, and ColorMaterial is
                                                          enabled. Down otherwise.

                                                                        Front Emission
                                                                                                     To lighting equations
  Material*(FRONT,EMISSION)                                             Color




                                   State values flow along this path only when a command is issued

                                   State values flow continuously along this path




  Figure 2.9. ColorMaterial operation. Material properties are continuously
  updated from the current color while ColorMaterial is enabled and has the
  appropriate mode. Only the front material properties are included in this
   gure. The back material properties are treated identically.




                                               Version 1.0 - 1 July 1994
46                                   CHAPTER 2. OPENGL OPERATION

speci es which material property or properties track the current color. If
mode is EMISSION, AMBIENT, DIFFUSE, or SPECULAR, then the value of ecm ,
acm , dcm or scm, respectively, will track the current color. If mode is
AMBIENT AND DIFFUSE, both acm and dcm track the current color. The re-
placements made to material properties are permanent the replaced values
remain until changed by either sending a new color or by setting a new ma-
terial value when ColorMaterial is not currently enabled to override that
particular value. When COLOR MATERIAL is enabled, the indicated parameter
or parameters always track the current color. For instance, calling
      ColorMaterial(FRONT, AMBIENT)
while COLOR MATERIAL is enabled sets the front material acm to the value of
the current color.

2.12.4 Lighting State
The state required for lighting consists of all of the lighting parameters (front
and back material parameters, lighting model parameters, and at least 8 sets
of light parameters), a bit indicating whether a back color distinct from the
front color should be computed, at least 8 bits to indicate which lights are
enabled, a ve-valued variable indicating the current ColorMaterial mode,
a bit indicating whether or not COLOR MATERIAL is enabled, and a single bit
to indicate whether lighting is enabled or disabled. In the initial state, all
lighting parameters have their default values. Back color evaluation does
not take place, ColorMaterial is FRONT AND BACK and AMBIENT AND DIFFUSE,
and both lighting and COLOR MATERIAL are disabled.

2.12.5 Color Index Lighting
A simpli ed lighting computation applies in color index mode that uses
many of the parameters controlling RGBA lighting, but none of the RGBA
material parameters. First, the RGBA di use and specular intensities of
light i (dcli and scli, respectively) determine color index di use and specular
light intensities, dli and sli from
               dli = (:30)R(dcli) + (:59)G(dcli) + (:11)B(dcli)
and
               sli = (:30)R(scli) + (:59)G(scli) + (:11)B(scli):




                        Version 1.0 - 1 July 1994
2.12. COLORS AND COLORING                                                  47

R(x) indicates the R component of the color x and similarly for G(x) and
B (x).
   Next, let
                        X
                        n
                   s=         (atti )(spoti )(sli )(fi )(n h^ i )srm
                        i=0
where atti and spoti are given by equations 2.4 and 2.5, respectively, and fi
and h^ i are given by equations 2.2 and 2.3, respectively. Let s0 = minfs 1g.
Finally, let
                     d = (atti )(spoti )(dli)(n ;!
                         Xn
                                                  VPpli):
                         i=0
Then color index lighting produces a value c, given by
                c = am + d(1 ; s0)(dm ; am) + s0(sm ; am ):
The nal color index is
                                  c0 = minfc smg:
The values am , dm and sm are material properties described in Tables 2.5
and 2.6. Any ambient light intensities are incorporated into am . As with
RGBA lighting, disabled lights cause the corresponding terms from the sum-
mations to be omitted. The interpretation of tbs and the calculation of front
and back colors is carried out as has already been described for RGBA
lighting.
    The values am , dm , and sm are set with Material using prop of
COLOR INDEXES. Their initial values are 0, 1, and 1, respectively. The ad-
ditional state consists of three oating-point values. These values have no
e ect on RGBA lighting.

2.12.6 Clamping or Masking
After lighting, RGBA colors are clamped to the range 0 1]. For a color
index, the index is rst converted to xed-point with an unspeci ed number
of bits to the right of the binary point the nearest xed-point value is
selected. Then, the bits to the right of the binary point are left alone while
the integer portion is masked (bitwise ANDed) with 2n ; 1, where n is the
number of bits in a color in the color index bu er (bu ers are discussed in
chapter 4).




                                    Version 1.0 - 1 July 1994
48                                   CHAPTER 2. OPENGL OPERATION

                   Primitive type of polygon i        Vertex
                   single polygon (i 1)                  1
                   triangle strip                      i+2
                   triangle fan                        i+2
                   independent triangle                 3i
                   quad strip                         2i + 2
                   independent quad                     4i

Table 2.7: Polygon atshading color selection. The color used for atshading
the ith polygon generated by the indicated Begin/End type is the current
color (if lighting is disabled) in e ect when the indicated vertex is speci ed.
If lighting is enabled, the color is produced by lighting the indicated ver-
tex. Vertices are numbered 1 through n, where n is the number of vertices
between the Begin/End pair.

2.12.7 Flatshading
A primitive may be atshaded, meaning that all vertices of the primitive are
assigned the same color. This color is the color of the vertex that spawned
the primitive. For a point, this is the color associated with the point. For a
line segment, it is the color of the second ( nal) vertex of the segment. For
a polygon, the selected color depends on how the polygon was generated.
Table 2.7 summarizes the possibilities.
    Flatshading is controlled by
      void   ShadeModel(      enum   mode )
mode value must be either of the symbolic constants SMOOTH or FLAT. If mode
is SMOOTH (the initial state), vertex colors are treated individually. If mode is
FLAT, atshading is turned on. ShadeModel thus requires one bit of state.


2.12.8 Color and Texture Coordinate Clipping
After lighting, clamping or masking and possible atshading, colors are
clipped. If the color is associated with a vertex that lies within the clip
volume, it is una ected by clipping. If a primitive is clipped, however, the
colors assigned to vertices produced by clipping are clipped colors.




                        Version 1.0 - 1 July 1994
2.12. COLORS AND COLORING                                                 49

   Let the color assigned to the two vertices P1 and P2 of an unclipped
edge be c1 and c2 . The value of t (Section 2.10) for a clipped point P is
used to obtain the color associated with P as
                            c = tc1 + (1 ; t)c2:
(For a color index color, multiplying a color by a scalar means multiplying
the index by the scalar. For an RGBA color, it means multiplying each of R,
G, B, and A by the scalar.) Polygon clipping may create a clipped vertex
along an edge of the clip volume's boundary. This situation is handled by
noting that polygon clipping proceeds by clipping against one plane of the
clip volume's boundary at a time. Color clipping is done in the same way,
so that clipped points always occur at the intersection of polygon edges
(possibly already clipped) with the clip volume's boundary.
    Texture coordinates must also be clipped when a primitive is clipped.
The method is exactly analogous to that used for color clipping.
2.12.9 Final Color Processing
For an RGBA color, each color component (which lies in 0,1]) is converted
(by rounding to nearest) to a xed-point value with m bits. We assume
that the xed-point representation used represents each value k=(2m ; 1),
where k 2 f0 1 : : : 2m ; 1g, as k (e.g. 1.0 is represented in binary as a
string of all ones). m must be at least as large as the number of bits in the
corresponding component of the framebu er. If the framebu er does not
contain an A component, then m must be at least 2 for A. A color index
is converted (by rounding to nearest) to a xed-point value with at least as
many bits as there are in the color index portion of the framebu er.
    Because a number of the form k=(2m ; 1) may not be represented exactly
as a limited-precision oating-point quantity, we place a further requirement
on the xed-point conversion of RGBA components. Suppose that lighting
is disabled, the color associated with a vertex has not been clipped, and one
of Colorub, Colorus, or Colorui was used to specify that color. When
these conditions are satis ed, an RGBA component must convert to a value
that matches the component as speci ed in the Color command: if m is less
than the number of bits b with which the component was speci ed, then the
converted value must equal the most signi cant m bits of the speci ed value
otherwise, the most signi cant b bits of the converted value must equal the
speci ed value.




                               Version 1.0 - 1 July 1994
Chapter 3
Rasterization
Rasterization is the process by which a primitive is converted to a two-
dimensional image. Each point of this image contains such information as
color and depth. Thus, rasterizing a primitive consists of two parts. The
  rst is to determine which squares of an integer grid in window coordinates
are occupied by the primitive. The second is assigning a color and a depth
value to each such square. The results of this process are passed on to the
next stage of the GL (per-fragment operations), which uses the information
to update the appropriate locations in the framebu er. Figure 3.1 diagrams
the rasterization process.
     A grid square along with its parameters of assigned color, z (depth),
and texture coordinates is called a fragment the parameters are collectively
dubbed the fragment's associated data. A fragment is located by its lower-
left corner, which lies on integer grid coordinates. Rasterization operations
also refer to a fragment's center, which is o set by (1=2 1=2) from its lower-
left corner (and so lies on half-integer coordinates).
     Grid squares need not actually be square in the GL. Rasterization rules
are not a ected by the actual aspect ratio of the grid squares. Display of
non-square grids, however, will cause rasterized points and line segments to
appear fatter in one direction than the other. We assume that fragments
are square, since it simpli es antialiasing and texturing.
     Several factors a ect rasterization. Lines and polygons may be stippled.
Points may be given di ering diameters and line segments di ering widths.
A point, line segment, or polygon may be antialiased.
                                      50




                       Version 1.0 - 1 July 1994
3.1. INVARIANCE                                                                     51



                         Point
                      Rasterization



        From
                          Line
      Primitive                                 Texturing         Fog
                      Rasterization
      Assembly                                                          Fragments


                        Polygon
                      Rasterization



                         Pixel
         DrawPixels    Rectangle
                      Rasterization



                        Bitmap
             Bitmap
                      Rasterization




  Figure 3.1. Rasterization.


3.1 Invariance
Consider a primitive p0 obtained by translating a primitive p through an
o set (x y ) in window coordinates, where x and y are integers. As long
as neither p0 nor p is clipped, it must be the case that each fragment f 0
produced from p0 is identical to a corresponding fragment f from p except
that the center of f 0 is o set by (x y ) from the center of f .

3.2 Antialiasing
Antialiasing of a point, line, or polygon is e ected in one of two ways de-
pending on whether the GL is in RGBA or color index mode.
    In RGBA mode, the R, G, and B values of the rasterized fragment are
left una ected, but the A value is multiplied by a oating-point value in
the range 0 1] that describes a fragment's screen pixel coverage. The
per-fragment stage of the GL can be set up to use the A value to blend
the incoming fragment with the corresponding pixel already present in the
framebu er.




                                      Version 1.0 - 1 July 1994
52                                          CHAPTER 3. RASTERIZATION

    In color index mode, the least signi cant b bits (to the left of the binary
point) of the color index are used for antialiasing b = minf4 mg, where
m is the number of bits in the color index portion of the framebu er. The
antialiasing process sets these b bits based on the fragment's coverage value:
the bits are set to zero for no coverage and to all ones for complete coverage.
    The details of how antialiased fragment coverage values are computed
are di cult to specify in general. The reason is that high-quality antialias-
ing may take into account perceptual issues as well as characteristics of the
monitor on which the contents of the framebu er are displayed. Such de-
tails cannot be addressed within the scope of this document. Further, the
coverage value computed for a fragment of some primitive may depend on
the primitive's relationship to a number of grid squares neighboring the one
corresponding to the fragment, and not just on the fragment's grid square.
Another consideration is that accurate calculation of coverage values may
be computationally expensive consequently we allow a given GL implemen-
tation to approximate true coverage values by using a fast but not entirely
accurate coverage computation.
    In light of these considerations, we chose to specify the behavior of exact
antialiasing in the prototypical case that each displayed pixel is a perfect
square of uniform intensity. The square is called a fragment square and has
lower left corner (x y ) and upper right corner (x + 1 y + 1). We recognize
that this simple box lter may not produce the most favorable antialiasing
results, but it provides a simple, well-de ned model.
    A GL implementation may use other methods to perform antialiasing,
subject to the following conditions:
   1. If f1 and f2 are two fragments, and the portion of f1 covered by some
       primitive is a subset of the corresponding portion of f2 covered by
       the primitive, then the coverage computed for f1 must be less than or
       equal to that computed for f2 .
   2. The coverage computation for a fragment f must be local: it may
       depend only on f 's relationship to the boundary of the primitive being
       rasterized. It may not depend on f 's x and y coordinates.
Another property that is desirable, but not required, is:
   3. The sum of the coverage values for all fragments produced by rasteriz-
       ing a particular primitive must be constant, independent of any rigid
       motions in window coordinates, as long as none of those fragments lies
       along window edges.




                        Version 1.0 - 1 July 1994
3.3. POINTS                                                                53

In some implementations, varying degrees of antialiasing quality may be
obtained by providing GL hints (section 5.6), allowing a user to make an
image quality versus speed tradeo .

3.3 Points
The rasterization of points is controlled with
     void   PointSize(    float   size )
size speci es the width or diameter of a point. The default value is 1.0. A
value less than or equal to zero results in the error INVALID VALUE.
    Point antialiasing is enabled or disabled by calling Enable or Disable
with the symbolic constant POINT SMOOTH. The default state is for point an-
tialiasing to be disabled.
     In the default state, a point is rasterized by truncating its xw and yw
coordinates (recall that the subscripts indicate that these are x and y window
coordinates) to integers. This (x y ) address, along with the data associated
with the vertex corresponding to the point, is sent as a single fragment to
the per-fragment stage of the GL.
     The e ect of a point width other than 1:0 depends on the state of
point antialiasing. If antialiasing is disabled, the actual width is deter-
mined by rounding the supplied width to the nearest integer, then clamping
it to the implementation-dependent maximum non-antialiased point width.
Though this implementation-dependent value cannot be queried, it must
be no less than the implementation-dependent maximum antialiased point
width, rounded to the nearest integer value, and in any event no less than
1. If rounding the speci ed width results in the value 0, then it is as if the
value were 1. If the resulting width is odd, then the point
                        (x y ) = (bxw c + 1 byw c + 1 )
                                          2          2
is computed from the vertex's xw and yw , and a square grid of the odd width
centered at (x y ) de nes the centers of the rasterized fragments (recall that
fragment centers lie at half-integer window coordinate values). If the width
is even, then the center point is
                       (x y ) = (bxw + 21 c byw + 12 c)




                                Version 1.0 - 1 July 1994
54                                                 CHAPTER 3. RASTERIZATION




                                             5.5

                                             4.5

                                             3.5

                                             2.5

                                             1.5

                                             0.5

         0.5   1.5   2.5   3.5   4.5   5.5           0.5   1.5   2.5   3.5   4.5   5.5

                Odd Width                                   Even Width

     Figure 3.2. Rasterization of non-antialiased wide points. The crosses show
     fragment centers produced by rasterization for any point that lies within the
     shaded region. The dotted grid lines lie on half-integer coordinates.




                             Version 1.0 - 1 July 1994
3.3. POINTS                                                                         55



                       6.0



                       5.0



                       4.0



                       3.0



                       2.0



                       1.0



                       0.0
                             0.0   1.0     2.0   3.0   4.0   5.0     6.0




   Figure 3.3. Rasterization of antialiased wide points. The black dot indi-
   cates the point to be rasterized. The shaded region has the speci ed width.
   The X marks indicate those fragment centers produced by rasterization. A
   fragment's computed coverage value is based on the portion of the shaded re-
   gion that covers the corresponding fragment square. Solid lines lie on integer
   coordinates.


the rasterized fragment centers are the half-integer window coordinate values
within the square of the even width centered on (x y ). See Figure 3.2.
    All fragments produced in rasterizing a non-antialiased point are as-
signed the same associated data, which are those of the vertex corresponding
to the point.
    If antialiasing is enabled, then point rasterization produces a fragment
for each fragment square that intersects the region lying within the circle
having diameter equal to the current point width and centered at the point's
(xw yw ) (Figure 3.3). The coverage value for each fragment is the window
coordinate area of the intersection of the circular region with the correspond-
ing fragment square (but see section 3.2). This value is saved and used in
the nal step of rasterization (section 3.10). The data associated with each
fragment are otherwise the data associated with the point being rasterized.
   Not all widths need be supported when point antialiasing is on, but
the width 1:0 must be provided. If an unsupported width is requested, the




                                         Version 1.0 - 1 July 1994
56                                          CHAPTER 3. RASTERIZATION

nearest supported width is used instead. The range of supported widths and
the width of evenly-spaced gradations within that range are implementation
dependent. The range and gradations may be obtained using the query
mechanism described in Chapter 6. If, for instance, the width range is from
0.1 to 2.0 and the gradation width is 0.1, then the widths 0:1 0:2 : : : 1:9 2:0
are supported.
3.3.1 Point Rasterization State
The state required to control point rasterization consists of the oating-point
point width and a bit indicating whether or not antialiasing is enabled.

3.4 Line Segments
A line segment results from a line strip Begin/End object, a line loop, or
a series of separate line segments. Line segment rasterization is controlled
by several variables. Line width, which may be set by calling
      void LineWidth( float width )

with an appropriate positive oating-point width, controls the width of ras-
terized line segments. The default width is 1:0. Values less than or equal
to 0:0 generate the error INVALID VALUE. Antialiasing is controlled with En-
able and Disable using the symbolic constant LINE SMOOTH. Finally, line
segments may be stippled. Stippling is controlled by a GL command that
sets a stipple pattern (see below).
3.4.1 Basic Line Segment Rasterization
Line segment rasterization begins by characterizing the segment as either
x-major or y-major. x-major line segments have slope in the closed inter-
val ;1 1] all other line segments are y -major (slope is determined by the
segment's endpoints). We shall specify rasterization only for x-major seg-
ments except in cases where the modi cations for y -major segments are not
self-evident.
    Ideally, the GL uses a \diamond-exit" rule to determine those fragments
that are produced by rasterizing a line segment. For each fragment f with
center at window coordinates xf and yf , de ne a diamond-shaped region
that is the intersection of four half-planes:
                         Rf = Sf 1 \ Sf 2 \ Sf 3 \ Sf 4




                        Version 1.0 - 1 July 1994
3.4. LINE SEGMENTS                                                                57




  Figure 3.4. Visualization of Bresenham's algorithm. A portion of a line
  segment is shown. A diamond shaped region of height 1 is placed around each
  fragment center those regions that the line segment exits cause rasterization
  to produce corresponding fragments.


where
                  Sf 1  = f(x y )jx + y > xf + yf ; 0:5g
                  Sf 2  = f(x y )jx + y xf + yf + 0:5g
                  Sf 3  = f(x y )jx ; y xf ; yf ; 0:5g
                  Sf 4  = f(x y )jx ; y < xf ; yf + 0:5g
    A line segment starting at pa and ending at pb produces those fragments
f for which the segment intersects Rf , except if pb is contained in Rf . See
Figure 3.4.
    When pa and pb lie on fragment centers, this characterization of frag-
ments reduces to Bresenham's algorithm with one modi cation: lines pro-
duced in this description are \half-open," meaning that the nal fragment
(corresponding to pb ) is not drawn. This means that when rasterizing a
series of connected line segments, shared endpoints will be produced only
once rather than twice (as would occur with Bresenham's algorithm).
    Because the initial and nal conditions of the diamond-exit rule may
be di cult to implement, other line segment rasterization algorithms are
allowed, subject to the following rules:




                                 Version 1.0 - 1 July 1994
58                                          CHAPTER 3. RASTERIZATION

   1. The coordinates of a fragment produced by the algorithm may not
      deviate by more than one unit in either x or y window coordinates
      from a corresponding fragment produced by the diamond-exit rule.
   2. The total number of fragments produced by the algorithm may di er
      from that produced by the diamond-exit rule by no more than one.
   3. For an x-major line, no two fragments may be produced that lie in the
      same window-coordinate column (for a y -major line, no two fragments
      may appear in the same row).
   4. If two line segments share a common endpoint, and both segments
      are either x-major (both left-to-right or both right-to-left) or y -major
      (both bottom-to-top or both top-to-bottom), then rasterizing both
      segments may not produce duplicate fragments, nor may any frag-
      ments be omitted so as to interrupt continuity of the connected seg-
      ments.
    Next we must specify how the data associated with each rasterized frag-
ment are obtained. Let the window coordinates of a produced fragment
center be given by pr = (xd yd) and let pa = (xa ya) and pb = (xb yb). Set
                         t = (pr ; pa) (pb ; pa) :
                                    kpb ; pak   2
                                                                           (3:1)
(Note that t = 0 at pa and t = 1 at pb .) The value of an associated datum
f for the fragment, whether it be R, G, B, or A (in RGBA mode) or a color
index (in color index mode), or the s, t, or r texture coordinate (the depth
value, window z , must be found using equation 3.3, below), is found as
                             (1 ; t)fa =wa + tfb =wb
                        f = (1                                          (3:2)
                                ; t) a=wa + t b =wb
where fa and fb are the data associated with the starting and ending end-
points of the segment, respectively wa and wb are the clip w coordinates of
the starting and ending endpoints of the segments, respectively. a = b = 1
for all data except texture coordinates, in which case a = qa and b = qb
(qa and qb are the homogeneous texture coordinates at the starting and end-
ing endpoints of the segment results are unde ned if either of these is less
than or equal to 0). Note that linear interpolation would use
                         f = (1 ; t)fa = a + tfb = b :                    (3:3)




                        Version 1.0 - 1 July 1994
3.4. LINE SEGMENTS                                                           59

The reason that this formula is incorrect (except for the depth value) is
that it interpolates a datum in window space, which may be distorted by
perspective. What is actually desired is to nd the corresponding value when
interpolated in eye space, which equation 3.2 does. A GL implementation
may choose to approximate equation 3.2 with 3.3, but this will normally lead
to unacceptable distortion e ects when interpolating texture coordinates.

3.4.2 Other Line Segment Features
We have just described the rasterization of non-antialiased line segments
of width one using the default line stipple of FFFF16 . We now describe
the rasterization of line segments for general values of the line segment
rasterization parameters.

Line Stipple
The command
      void   LineStipple(    int   factor, ushort pattern )
de nes a line stipple. pattern is an unsigned short integer. The line stipple is
taken from the lowest order 16 bits of pattern. It determines those fragments
that are to be drawn when the line is rasterized. factor is a count that is
used to modify the e ective line stipple by causing each bit in line stipple to
be used factor times. factor is clamped to the range 1 256]. Line stippling
may be enabled or disabled using Enable or Disable with the constant
LINE STIPPLE. When disabled, it is as if the line stipple has its default value.
    Line stippling masks certain fragments that are produced by rasteriza-
tion so that they are not sent to the per-fragment stage of the GL. The
masking is achieved using three parameters: the 16-bit line stipple p, the
line repeat count r, and an integer stipple counter s. Let
                              b = bs=rc mod 16
Then a fragment is produced if the bth bit of p is 1, and not produced
otherwise. The bits of p are numbered with 0 being the least signi cant and
15 being the most signi cant. The initial value of s is zero s is incremented
after production of each fragment of a line segment (fragments are produced
in order, beginning at the starting point and working towards the ending
point). s is reset to 0 whenever a Begin occurs, and before every line




                                Version 1.0 - 1 July 1994
60                                           CHAPTER 3. RASTERIZATION

segment in a group of independent segments (as speci ed when Begin is
invoked with LINES).
    If the line segment has been clipped, then the value of s at the beginning
of the line segment is indeterminate.

Wide Lines
The actual width of non-antialiased lines is determined by rounding
the supplied width to the nearest integer, then clamping it to the
implementation-dependent maximum non-antialiased line width. Though
this implementation-dependent value cannot be queried, it must be no
less than the implementation-dependent maximum antialiased line width,
rounded to the nearest integer value, and in any event no less than 1. If
rounding the speci ed width results in the value 0, then it is as if the value
were 1.
    Non-antialiased line segments of width other than one are rasterized
by o setting them in the minor direction (for an x-major line, the minor
direction is y , and for a y -major line, the minor direction is x) and replicating
fragments in the minor direction (see Figure 3.5). Let w be the width
rounded to the nearest integer (if w = 0, then it is as if w = 1). If the line
segment has endpoints given by (x0 y0 ) and (x1 y1 ) in window coordinates,
the segment with endpoints (x0 y0 ; (w ; 1)=2) and (x1 y1 ; (w ; 1)=2) is
rasterized, but instead of a single fragment, a column of fragments of height
w (a row of fragments of length w for a y -major segment) is produced at
each x (y for y -major) location. The lowest fragment of this column is the
fragment that would be produced by rasterizing the segment of width 1
with the modi ed coordinates. The whole column is not produced if the
stipple bit for the column's x location is zero otherwise, the whole column
is produced.

Antialiasing
Rasterized antialiased line segments produce fragments whose fragment
squares intersect a rectangle centered on the line segment. Two of the edges
are parallel to the speci ed line segment each is at a distance of one-half
the current width from that segment: one above the segment and one below
it. The other two edges pass through the line endpoints and are perpen-
dicular to the direction of the speci ed line segment. Coverage values are
computed for each fragment by computing the area of the intersection of




                         Version 1.0 - 1 July 1994
3.4. LINE SEGMENTS                                                                 61




                  width = 2                             width = 3



  Figure 3.5. Rasterization of non-antialiased wide lines. x-major line segments
  are shown. The heavy line segment is the one speci ed to be rasterized the
  light segment is the o set segment used for rasterization. x marks indicate
  the fragment centers produced by rasterization.




                                 Version 1.0 - 1 July 1994
62                                            CHAPTER 3. RASTERIZATION




     Figure 3.6. The region used in rasterizing and nding corresponding coverage
     values for an antialiased line segment (an x-major line segment is shown).




the rectangle with the fragment square (see Figure 3.6 see also section 3.2).
  Equation 3.2 is used to compute associated data values just as with non-
antialiased lines equation 3.1 is used to nd the value of t for each fragment
whose square is intersected by the line segment's rectangle. Not all widths
need be supported for line segment antialiasing, but width 1:0 antialiased
segments must be provided. As with the point width, a GL implementa-
tion may be queried for the range and number of gradations of available
antialiased line widths.
    For purposes of antialiasing, a stippled line is considered to be a sequence
of contiguous rectangles centered on the line segment. Each rectangle has
width equal to the current line width and length equal to 1 pixel (except the
last, which may be shorter). These rectangles are numbered from 0 to n,
starting with the rectangle incident on the starting endpoint of the segment.
Each of these rectangles is either eliminated or produced according to the
procedure given under Line Stipple, above, where \fragment" is replaced
with \rectangle." Each rectangle so produced is rasterized as if it were an
antialiased polygon, described below (but culling, non-default settings of
PolygonMode, and polygon stippling are not applied).




                          Version 1.0 - 1 July 1994
3.5. POLYGONS                                                                  63

3.4.3 Line Rasterization State
The state required for line rasterization consists of the oating-point line
width, a 16-bit line stipple, the line stipple repeat count, a bit indicating
whether stippling is enabled or disabled, and a bit indicating whether line
antialiasing is on or o . In addition, during rasterization, an integer stipple
counter must be maintained to implement line stippling. The initial value
of the line width is 1:0. The initial value of the line stipple is 0xFFFF (a
stipple of all ones). The initial value of the line stipple repeat count is one.
The initial state of line stippling is disabled. The initial state of line segment
antialiasing is disabled.

3.5 Polygons
A polygon results from a polygon Begin/End object, a triangle resulting
from a triangle strip, triangle fan, or series of separate triangles, or a quadri-
lateral arising from a quadrilateral strip, series of separate quadrilaterals, or
a Rect command. Like points and line segments, polygon rasterization is
controlled by several variables. Polygon antialiasing is controlled with En-
able and Disable with the symbolic constant POLYGON SMOOTH. The analog
to line segment stippling for polygons is polygon stippling, described below.

3.5.1 Basic Polygon Rasterization
The rst step of polygon rasterization is to determine if the polygon is
back facing or front facing. This determination is made by examining the
sign of the area computed by equation 2.6 of section 2.12.1 (including the
possible reversal of this sign as indicated by the last call to FrontFace). If
this sign is positive, the polygon is frontfacing otherwise, it is back facing.
This determination is used in conjunction with the CullFace enable bit and
mode value to decide whether or not a particular polygon is rasterized. The
CullFace mode is set by calling
      void   CullFace(    enum   mode )
mode is a symbolic constant: one of FRONT, BACK or FRONT AND BACK. Culling
is enabled or disabled with Enable or Disable using the symbolic constant
CULL FACE. Front facing polygons are rasterized if either culling is disabled or
the CullFace mode is BACK while back facing polygons are rasterized only if




                                 Version 1.0 - 1 July 1994
64                                             CHAPTER 3. RASTERIZATION

either culling is disabled or the CullFace mode is FRONT. The initial setting
of the CullFace mode is BACK. Initially, culling is disabled.
    The rule for determining which fragments are produced by polygon ras-
terization is called point sampling. The two-dimensional projection obtained
by taking the x and y window coordinates of the polygon's vertices is formed.
Fragment centers that lie inside of this polygon are produced by rasteriza-
tion. Special treatment is given to a fragment whose center lies on a polygon
boundary edge. In such a case we require that if two polygons lie on either
side of a common edge (with identical endpoints) on which a fragment cen-
ter lies, then exactly one of the polygons results in the production of the
fragment during rasterization.
    As for the data associated with each fragment produced by rasterizing a
polygon, we begin by specifying how these values are produced for fragments
in a triangle. De ne barycentric coordinates for a triangle. Barycentric
coordinates are a set of three numbers, a, b, and c, each in the range 0 1],
with a + b + c = 1. These coordinates uniquely specify any point p within
the triangle or on the triangle's boundary as
                              p = apa + bpb + cpc
where pa , pb , and pc are the vertices of the triangle. a, b, and c can be found
as
                    A(ppb pc ) b = A(ppa pc ) c = A(ppapb )
               a = A( papbpc)         A(papb pc )         A(papb pc )
where A(lmn) denotes the area in window coordinates of the triangle with
vertices l, m, and n.
    Denote a datum at pa , pb , or pc as fa , fb , or fc , respectively. Then the
value f of a datum at a fragment produced by rasterizing a triangle is given
by
                        f = aafa=w
                                 =wa + bfb=wb + cfc =wc
                                      + b =w + c =w                          (3:4)
                                a   a      b    b    c   c
where wa, wb and wc are the clip w coordinates of pa, pb , and pc , respectively.
a, b, and c are the barycentric coordinates of the fragment for which the data
are produced. a = b = c = 1 except for texture s, t, and r coordinates,
for which a = qa , b = qb , and c = qc (if any of qa , qb , or qc are less
than or equal to zero, results are unde ned). a, b, and c must correspond
precisely to the exact coordinates of the center of the fragment. Another way
of saying this is that the data associated with a fragment must be sampled
at the fragment's center.




                         Version 1.0 - 1 July 1994
3.5. POLYGONS                                                              65

    Just as with line segment rasterization, equation 3.4 may be approxi-
mated by
                       f = afa = a + bfb= b + cfc = c
this may yield acceptable results for color values (it must be used for depth
values), but will normally lead to unacceptable distortion e ects if used for
texture coordinates.
    For a polygon with more than three edges, we require only that a convex
combination of the values of the datum at the polygon's vertices can be used
to obtain the value assigned to each fragment produced by the rasterization
algorithm. That is, it must be the case that at every fragment
                                      X
                                      n
                                 f=         ai fi
                                      i=1
where n is the number of vertices in Pthe polygon, fi is the value of the f at
vertex i for each i 0 ai 1 and ni=1 ai = 1. The values of the ai may
di er from fragment to fragment, but at vertex i, aj = 0 j 6= i and ai = 1.
    One algorithm that achieves the required behavior is to triangulate a
polygon (without adding any vertices) and then treat each triangle individ-
ually as already discussed. A scan-line rasterizer that linearly interpolates
data along each edge and then linearly interpolates data across each hor-
izontal span from edge to edge also satis es the restrictions (in this case,
the numerator and denominator of equation 3.4 should be iterated indepen-
dently and a division performed for each fragment).

3.5.2 Stippling
Polygon stippling works much the same way as line stippling, masking out
certain fragments produced by rasterization so that they are not sent to the
next stage of the GL. This is the case regardless of the state of polygon
antialiasing. Stippling is controlled with
     void   PolygonStipple(      ubyte   pattern ] )
pattern is a pointer to memory into which a 32 32 pattern is packed.
The pattern is unpacked from memory according to the procedure given
in section 3.6.3 for DrawPixels it is as if the height and width passed to
that command were both equal to 32, the type were BITMAP, and the format
were COLOR INDEX. The unpacked values (before any conversion or arithmetic




                                Version 1.0 - 1 July 1994
66                                         CHAPTER 3. RASTERIZATION

would have been performed) are bitwise ANDed with 1 to obtain a stipple
pattern of zeros and ones.
    If xw and yw are the window coordinates of a rasterized polygon frag-
ment, then that fragment is sent to the next stage of the GL if and only if
the bit of the pattern (xw mod 32 yw mod 32) is 1.
    Polygon stippling may be enabled or disabled with Enable or Disable
using the constant POLYGON STIPPLE. When disabled, it is as if the stipple
pattern were all ones.
3.5.3 Antialiasing
Polygon antialiasing rasterizes a polygon by producing a fragment wherever
the interior of the polygon intersects that fragment's square. A coverage
value is computed at each such fragment, and this value is saved to be applied
as described in section 3.10. An associated datum is assigned to a fragment
by integrating the datum's value over the region of the intersection of the
fragment square with the polygon's interior and dividing this integrated
value by the area of the intersection. For a fragment square lying entirely
within the polygon, the value of a datum at the fragment's center may be
used instead of integrating the value across the fragment.
    Polygon stippling operates in the same way whether polygon antialiasing
is enabled or not. The polygon point sampling rule de ned in section 3.5.1,
however, is not enforced for antialiased polygons.
3.5.4 Options Controlling Polygon Rasterization
The interpretation of polygons for rasterization is controlled using
     void   PolygonMode(       enum   face, enum mode )
face is one of FRONT, BACK, or FRONT AND BACK, indicating that the rasterizing
method described by mode replaces the rasterizing method for front facing
polygons, back facing polygons, or both front and back facing polygons,
respectively. mode is one of the symbolic constants POINT, LINE, or FILL.
Calling PolygonMode with POINT causes certain vertices of a polygon to
be treated, for rasterization purposes, just as if they were enclosed within
a Begin(POINT) and End pair. The vertices selected for this treatment are
those that have been tagged as having a polygon boundary edge beginning
on them (see section 2.6.2). LINE causes edges that are tagged as boundary
to be rasterized as line segments. (The line stipple counter is reset at the




                       Version 1.0 - 1 July 1994
3.6. PIXEL RECTANGLES                                                         67

beginning of the rst rasterized edge of the polygon, but not for subsequent
edges.) FILL is the default mode of polygon rasterization, corresponding to
the description in sections 3.5.1, 3.5.2, and 3.5.3. Note that these modes
a ect only the nal rasterization of polygons: in particular, a polygon's
vertices are lit, and the polygon is clipped and possibly culled before these
modes are applied.
    Polygon antialiasing applies only to the FILL state of PolygonMode.
For POINT or LINE, point antialiasing or line segment antialiasing, respec-
tively, apply.

3.5.5 Polygon Rasterization State
The state required for polygon rasterization consists of a polygon stipple pat-
tern, whether stippling is enabled or disabled, the current state of polygon
antialiasing (enabled or disabled), and the current values of the Polygon-
Mode setting for each of front and back facing polygons. The initial stipple
pattern is all ones initially stippling is disabled. The initial setting of poly-
gon antialiasing is disabled. The initial state for PolygonMode is FILL for
both front and back facing polygons.


3.6 Pixel Rectangles
Rectangles of color, depth, and certain other values may be converted to
fragments using the DrawPixels command. Some of the parameters and
operations governing the operation of DrawPixels are shared by Read-
Pixels (used to obtain pixel values from the framebu er) and CopyPixels
(used to copy pixels from one framebu er location to another) the discus-
sion of ReadPixels and CopyPixels, however, is deferred until Chapter 4
after the framebu er has been discussed in detail. Nevertheless, we note
in this section when parameters and state pertaining to DrawPixels also
pertain to ReadPixels or CopyPixels.
    A number of parameters control the encoding of pixels in client mem-
ory (for reading and writing) and how pixels are processed before being
placed in or after being read from the framebu er (for reading, writing, and
copying). These parameters are set with three commands: PixelStore,
PixelTransfer, and PixelMap.




                                 Version 1.0 - 1 July 1994
68                                          CHAPTER 3. RASTERIZATION

         Parameter Name         Type Initial Value Valid Range
        UNPACK SWAP BYTES      boolean   FALSE     TRUE/FALSE
         UNPACK LSB FIRST      boolean   FALSE     TRUE/FALSE
        UNPACK ROW LENGTH      integer     0           0 1)
         UNPACK SKIP ROWS      integer     0           0 1)
        UNPACK SKIP PIXELS     integer     0           0 1)
         UNPACK ALIGNMENT      integer     4         1,2,4,8
      Table 3.1: PixelStore parameters pertaining to DrawPixels.

3.6.1 Pixel Storage Modes
Pixel storage modes a ect the operation of DrawPixels and ReadPixels
(as well as other commands see sections 3.5.2, 3.7, and 3.8) when one of
these commands is issued. This may di er from the time that the command
is executed if the command is placed in a display list (see section 5.4). Pixel
storage modes are set with
      void   PixelStorefifg(    enum   pname, T param )
pname is a symbolic constant indicating a parameter to be set, and param
is the value to set it to. Table 3.1 summarizes the pixel storage parameters,
their types, their initial values, and their allowable ranges. Setting a param-
eter to a value outside the given range results in the error INVALID VALUE.
    The version of PixelStore that takes a oating-point value may be
used to set any type of parameter if the parameter is boolean, then it
is set to FALSE if the passed value is 0:0 and TRUE otherwise, while if the
parameter is an integer, then the passed value is rounded to the nearest
integer. The integer version of the command may also be used to set any
type of parameter if the parameter is boolean, then it is set to FALSE if the
passed value is 0 and TRUE otherwise, while if the parameter is a oating-
point value, then the passed value is converted to oating-point.

3.6.2 Pixel Transfer Modes
Pixel transfer modes a ect the operation of DrawPixels, ReadPixels, and
CopyPixels at the time when one of these commands is executed (which




                        Version 1.0 - 1 July 1994
3.6. PIXEL RECTANGLES                                                     69


         Parameter Name       Type Initial Value Valid Range
             MAP COLOR       boolean   FALSE     TRUE/FALSE
           MAP STENCIL       boolean   FALSE     TRUE/FALSE
           INDEX SHIFT       integer      0       (;1 1)
           INDEX OFFSET      integer      0       (;1 1)
             RED SCALE          oat     1.0       (;1 1)
           GREEN SCALE          oat     1.0       (;1 1)
            BLUE SCALE          oat     1.0       (;1 1)
           ALPHA SCALE          oat     1.0       (;1 1)
           DEPTH SCALE          oat     1.0       (;1 1)
              RED BIAS          oat     0.0       (;1 1)
            GREEN BIAS          oat     0.0       (;1 1)
             BLUE BIAS          oat     0.0       (;1 1)
            ALPHA BIAS          oat     0.0       (;1 1)
            DEPTH BIAS          oat     0.0       (;1 1)
                  Table 3.2: PixelTransfer parameters.

may di er from the time the command is issued). Some pixel transfer modes
are set with
      void PixelTransferfifg( enum param, T value )

param is a symbolic constant indicating a parameter to be set, and value is
the value to set it to. Table 3.2 summarizes the pixel transfer parameters
that are set with PixelTransfer, their types, their initial values, and their
allowable ranges. Setting a parameter to a value outside the given range
results in the error INVALID VALUE. The same versions of the command exist
as for PixelStore, and the same rules apply to accepting and converting
passed values to set parameters.
    The other pixel transfer modes are the various lookup tables used by
DrawPixels, ReadPixels, and CopyPixels. These are set with
      void PixelMapfui us fgv( enum map, sizei size, T val-
          ues ] )
map is a symbolic map name, indicating the map to set, size indicates the
size of the map, and values is a pointer to an array of size map values.




                               Version 1.0 - 1 July 1994
70                                                    CHAPTER 3. RASTERIZATION

       Map Name                    Address      Value     Init. Size Init. Value
     PIXEL   MAP   I   TO   I      color idx color idx         1           0
     PIXEL   MAP   S   TO   S     stencil idx stencil idx      1           0
     PIXEL   MAP   I   TO   R      color idx      R            1          0.0
     PIXEL   MAP   I   TO   G      color idx      G            1          0.0
     PIXEL   MAP   I   TO   B      color idx      B            1          0.0
     PIXEL   MAP   I   TO   A      color idx      A            1          0.0
     PIXEL   MAP   R   TO   R          R          R            1          0.0
     PIXEL   MAP   G   TO   G          G          G            1          0.0
     PIXEL   MAP   B   TO   B          B          B            1          0.0
     PIXEL   MAP   A   TO   A          A          A            1          0.0
                                Table 3.3: PixelMap parameters.

    The entries of a table may be speci ed using one of three types: single-
precision oating-point, unsigned short integer, or unsigned integer, depend-
ing on which of the three versions of PixelMap is called. A table entry is
converted to the appropriate type when it is speci ed. An entry giving a
color component value is converted according to Table 2.4. An entry giving
a color index value is converted from an unsigned short integer or unsigned
integer to oating-point. An entry giving a stencil index is converted from
single-precision oating-point to an integer by rounding to nearest. The var-
ious tables and their initial sizes and entries are summarized in Table 3.3.
A table that takes an index as an address must have size = 2n or the error
INVALID VALUE results. The maximum allowable size of each table is imple-
mentation dependent, but must be at least 32 (a single maximum applies
to all tables). The error INVALID VALUE is generated if a size larger than the
implemented maximum, or less than zero, is given to PixelMap.

3.6.3 Rasterization of Pixel Rectangles
The process of drawing pixels encoded in host memory is diagrammed in
Figure 3.7. We describe the stages of this process in the order in which they
occur.
   Pixels are drawn using
      void    DrawPixels(              sizei   width, sizei height, enum format,




                                  Version 1.0 - 1 July 1994
3.6. PIXEL RECTANGLES                                                                   71




                                            Index
     byte short int float
        Data Stream                unpack                                    Pixel
                                            RGBA    convert        convert
   (index or component)                                                      Storage
                                            L, Z    to [0,1]      L−>RGBA    Modes




                                              RGBA−>RGBA           scale
                                                 lookup            bias
                        clamp                                                Pixel
      RGBA
                          to                                                 Transfer
        Z
                         [0,1]                                               Modes
    Pixel
    Data                                      index−>RGBA
    Out                                          lookup
                        mask                                        shift
      Index              to                                        offset
      (stencil,       [0.0,2n−1]
      colorindex)
                                              index−>index
                                                 lookup




  Figure 3.7. Operation of DrawPixels. The parameters controlling the stages
  above the dotted line are set with PixelStore while those controlling the
  stages below the line are set with PixelTransfer or PixelMap.




                                            Version 1.0 - 1 July 1994
72                                          CHAPTER 3. RASTERIZATION

                 type                Corresponding Type
            UNSIGNED BYTE           unsigned 8-bit integer
                 BYTE                 signed 8-bit integer
                BITMAP      single bits in unsigned 8-bit integers
           UNSIGNED SHORT          unsigned 16-bit integer
                SHORT                signed 16-bit integer
             UNSIGNED INT          unsigned 32-bit integer
                  INT                    32-bit integer
                FLOAT           single-precision oating-point
              Table 3.4: DrawPixels and ReadPixels types.

         enum   type, void *data )
format is a symbolic constant indicating what the values in memory repre-
sent. width and height are the width and height, respectively, of the pixel
rectangle to be drawn. data is a pointer to the data to be drawn. These data
are signed or unsigned bytes, 16-bit integers, or 32-bit integers, or single-
precision oating-point values, depending on the value of type. The possible
values of type and the types they indicate are given in Table 3.4. If the GL
is in color index mode and format is not one of COLOR INDEX, STENCIL INDEX,
or DEPTH COMPONENT, then the error INVALID OPERATION occurs.

Unpacking
Data are taken from host memory as a sequence of signed or unsigned bytes,
16-bit integers, 32-bit integers, or single-precision oating-point elements.
These elements are grouped into sets of one, two, three, or four values,
depending on the format, to form a group. Table 3.5 summarizes the format
of groups obtained from memory. It also indicates those formats that yield
indices and those that yield components.
    The byte-ordering of the bytes that constitute each element in memory
is whatever is native to the GL client if UNPACK SWAP BYTES is FALSE. If it is
TRUE, then byte-ordering is reversed for each element. In this case, there
is no e ect on a one-byte element, but the constituent bytes of a two-byte
or four-byte element are reversed when those bytes are read to form the
element. If the four bytes making up a four-byte element are stored in order




                        Version 1.0 - 1 July 1994
3.6. PIXEL RECTANGLES                                                        73


        Name             Type          Elements      Target Bu er
    COLOR INDEX          Index       Color Index         Color
   STENCIL INDEX         Index       Stencil value      Stencil
  DEPTH COMPONENT      Component     Depth value        Depth
        RED            Component          R              Color
       GREEN           Component          G              Color
        BLUE           Component          B              Color
       ALPHA           Component          A              Color
        RGB            Components      R, G, B           Color
        RGBA           Components     R, G, B, A         Color
     LUMINANCE         Component Luminance value         Color
  LUMINANCE ALPHA      Components Luminance value, A     Color
Table 3.5: DrawPixels and ReadPixels formats. The third column gives
a description of and the number and order of elements in a group.

in memory as b1, b2, b3, and b4 , then the reverse order is b4, b3, b2, and b1.
     Calling DrawPixels with a type of BITMAP is a special case in which
the data are a series of unsigned bytes. In this case, the only allowable
formats are COLOR INDEX and STENCIL INDEX. (Other formats generate the
error INVALID ENUM.) Each byte is taken as a series of eight bits, each of which
is a single element. The single-bit elements within each byte are ordered from
most signi cant to least signi cant if the value of UNPACK LSB FIRST is FALSE
otherwise, the ordering is from least signi cant to most signi cant.
     The groups in memory are treated as being arranged in a rectangle. This
rectangle consists of a series of rows, with the rst element of the rst group
of the rst row pointed to by the pointer passed to DrawPixels. If the
value of UNPACK ROW LENGTH is not positive, then the number of groups in a
row is width otherwise the number of groups is UNPACK ROW LENGTH. If the
  rst element of a row is at location p in memory, then the location of the
  rst element of the next row is obtained by skipping
                              (
                         k=       nl          s a                         (3:5)
                                  a=s dsnl=ae s < a
elements, where n is the number of elements in a group, l is the number of
groups in the row, a is the value of UNPACK ALIGNMENT, and s is the size, in




                                  Version 1.0 - 1 July 1994
74                                          CHAPTER 3. RASTERIZATION



                                   ROW_LENGTH



                                  subimage

                 SKIP_PIXELS


                               SKIP_ROWS




     Figure 3.8. Selecting a subimage from an image. The indicated param-
     eter names are pre xed by UNPACK for DrawPixels and by PACK for
     ReadPixels.

bytes, of an element. In the case of 1-bit elements, the location of the next
row is obtained by skipping
                                 k = 8a 8nla                            (3:6)
elements. The allowable values of UNPACK ALIGNMENT are 1, 2, 4, or 8 other
values result in the error INVALID VALUE.
    There is a mechanism for selecting a sub-rectangle of groups from a
larger containing rectangle. This mechanism relies on three integer param-
eters: UNPACK ROW LENGTH, UNPACK SKIP ROWS, and UNPACK SKIP PIXELS. Before
obtaining the rst group from memory, the pointer supplied to DrawPixels
is e ectively advanced by (UNPACK SKIP PIXELS)n + (UNPACK SKIP ROWS)k ele-
ments. Then width groups are obtained from contiguous elements in memory
(without advancing the pointer), after which the pointer is advanced by k
elements. height sets of width groups of values are obtained this way. See
Figure 3.8.
Conversion to oating-point
This step applies only to groups of components. It is not performed on
indices. Each element in a group is converted to a oating-point value




                        Version 1.0 - 1 July 1994
3.6. PIXEL RECTANGLES                                                      75

according to the appropriate formula in Table 2.4 (section 2.12) for color
components.

Conversion to RGB
This step is applied only if the format is LUMINANCE or LUMINANCE ALPHA. If
the format is LUMINANCE, then each group of one element is converted to a
group of R, G, and B (three) elements by copying the original single element
into each of the three new elements. If the format is LUMINANCE ALPHA, then
each group of two elements is converted to a group of R, G, B, and A (four)
elements by copying the rst original element into each of the rst three
new elements and copying the second original element to the A (fourth)
new element.

Final Expansion to RGBA
This step is performed only for non-depth component groups. Each group
is converted to a group of 4 elements as follows: if a group does not contain
an A element, then A is added and set to 1.0. If any of R, G, or B is missing
from the group, each missing element is added and assigned a value of 0.0.

Arithmetic on Components
This step applies only to component groups. Each component is multi-
plied by an appropriate signed scale factor: RED SCALE for an R compo-
nent, GREEN SCALE for a G component, BLUE SCALE for a B component, and
ALPHA SCALE for an A component, or DEPTH SCALE for a depth component.
Then the result is added to the the appropriate signed bias: RED BIAS,
GREEN BIAS, BLUE BIAS, ALPHA BIAS, or DEPTH BIAS.


Arithmetic on Indices
This step applies only to indices. If the index is a oating-point value, it is
converted to xed-point, with an unspeci ed number of bits to the right of
the binary point. Indices that are already integers remain so any fraction
bits in the resulting xed-point value are zero.
    The xed-point index is then shifted by jINDEX SHIFTj bits, left if
INDEX SHIFT > 0 and right otherwise. In either case the shift is zero- lled.
Then, the signed integer o set INDEX OFFSET is added to the index.




                                Version 1.0 - 1 July 1994
76                                          CHAPTER 3. RASTERIZATION

RGBA to RGBA Lookup
This step applies only to RGBA component groups, and is skipped if
MAP COLOR is FALSE. First, each component is clamped to the range 0 1].
There is a table associated with each of the R, G, B, and A component
elements: PIXEL MAP R TO R for R, PIXEL MAP G TO G for G, PIXEL MAP B TO B
for B, and PIXEL MAP A TO A for A. Each element is multiplied by an integer
one less than the size of the corresponding table, and, for each element, an
address is found by rounding this value to the nearest integer. For each ele-
ment, the addressed value in the corresponding table replaces the element.
Index Lookup
This step applies only to indices. If the GL is in RGBA mode, then the
integer part of the index is used to reference 4 tables of color components:
PIXEL MAP I TO R, PIXEL MAP I TO G, PIXEL MAP I TO B, and PIXEL MAP I TO A.
Each of these tables must have 2n entries for some integer value of n (n may
be di erent for each table). For each table, the index is rst rounded to the
nearest integer the result is ANDed with 2n ; 1, and the resulting value
used as an address into the table. The indexed value becomes an R, G, B,
or A value, as appropriate. The group of four elements so obtained replaces
the index, changing the group's type to \component."
    If the GL is in color index mode and if MAP COLOR is TRUE, then the index is
looked up in the PIXEL MAP I TO I table (otherwise, the index is not looked
up). Again, the table must have 2n entries for some integer n, and the
integer part of the index is ANDed with 2n ; 1, producing a value. This
value addresses the table, and the value in the table replaces the index.
The oating-point table value is rst rounded to a xed-point value with
unspeci ed precision.
    Finally, if format is STENCIL INDEX and if MAP STENCIL is TRUE, then the
index is looked up as described in the preceding paragraph, but using the
PIXEL MAP S TO S table.

Final Conversion
For a color index, nal conversion consists of masking the bits of the index
to the left of the binary point by 2n ; 1, where n is the number of bits in an
index bu er. For RGBA components, each element is clamped to 0 1]. The
resulting values are converted to xed-point according to the rules given in
section 2.12.9 (Final Color Processing).




                        Version 1.0 - 1 July 1994
3.7. BITMAPS                                                                        77

   For a depth component, an element is rst clamped to 0 1] and then
converted to xed-point as if it were a window z value (see section 2.9.1,
Controlling the Viewport).
   Stencil indices are masked by 2n ; 1, where n is the number of bits in
the stencil bu er.
Conversion to Fragments
The conversion of a group to fragments is controlled with
     void   PixelZoom(       float   zx , float zy )
Let (xrp yrp) be the current raster position (section 2.11). (If the current
raster position is invalid, then DrawPixels is ignored.) If a particular
group (index or components) is the nth in a row and belongs to the mth
row, consider the region in window coordinates bounded by the rectangle
with corners
   (xrp + zx n yrp + zy m)       and     (xrp + zx (n + 1) yrp + zy (m + 1))
(either zx or zy may be negative). Any fragments whose centers lie inside
of this rectangle (or on its bottom or left boundaries) are produced in cor-
respondence with this particular group of elements.
    A fragment arising from a group consisting of color data takes on the
color index or color components of the group the depth and texture coordi-
nates are taken from the current raster position's associated data. A frag-
ment arising from a depth component takes the component's depth value
the color and texture coordinates are given by those associated with the
current raster position. Groups arising from DrawPixels with a format of
STENCIL INDEX are treated specially and are described in section 4.3.1.


3.7 Bitmaps
Bitmaps are rectangles of zeros and ones specifying a particular pattern of
fragments to be produced. Each of these fragments has the same associated
data. These data are those associated with the current raster position.
    Bitmaps are sent using
     void   Bitmap(              w
                         sizei , sizei , floath              xbo ,   float   ybo,
        float   x            y
                 bi , float bi , ubyte data ] )




                                 Version 1.0 - 1 July 1994
78                                                   CHAPTER 3. RASTERIZATION




                        h = 12




                                 ybo = 1.0



                                         xbo = 2.5

                                                      w=8



     Figure 3.9. A bitmap and its associated parameters. xbi and ybi are not
     shown.


w and h comprise the integer width and height of the rectangular bitmap,
respectively. (xbo ybo) gives the oating-point x and y values of the bitmap's
origin. (xbi ybi ) gives the oating-point x and y increments that are added
to the raster position after the bitmap is rasterized. data is a pointer to a
bitmap.
    Like a polygon pattern, a bitmap is unpacked from memory according to
the procedure given in section 3.6.3 for DrawPixels it is as if the width and
height passed to that command were equal to w and h, respectively, the type
were BITMAP, and the format were COLOR INDEX. The unpacked values (before
any conversion or arithmetic would have been performed) are bitwise ANDed
with 1 to obtain a stipple pattern of zeros and ones. See Figure 3.9.
    A bitmap sent using Bitmap is rasterized as follows. First, if the cur-
rent raster position is invalid (the valid bit is reset), the bitmap is ignored.
Otherwise, a rectangular array of fragments is constructed, with lower left
corner at
                     (xll yll) = (bxrp ; xbo c byrp ; ybo c)
and upper right corner at (xll + w yll + h) where w and h are the width




                         Version 1.0 - 1 July 1994
3.8. TEXTURING                                                            79

and height of the bitmap, respectively. Fragments in the array are produced
if the corresponding bit in the bitmap is 1 and not produced otherwise.
The associated data for each fragment are those associated with the current
raster position. Once the fragments have been produced, the current raster
position is updated:
                     (xrp yrp)      (xrp + xbi yrp + ybi ):
The z and w values of the current raster position remain unchanged.

3.8 Texturing
Texturing maps a portion of a speci ed image onto each primitive for which
texturing is enabled. This mapping is accomplished by using the color of an
image at the location indicated by a fragment's (s t) coordinates to modify
the fragment's RGBA color (r is currently ignored). Texturing is speci ed
only for RGBA mode its use in color index mode is unde ned.
    The GL provides a means to specify the details of how texturing of a
primitive is e ected. These details include speci cation of the image to be
texture mapped, the means by which the image is ltered when applied
to the primitive, and the function that determines what RGBA value is
produced given a fragment color and an image value.
    The command
      void TexImage2D( enum target, int level, int compo-
          nents, sizei width, sizei height, int border, enum format,
          enum type, void *data )

is used to specify a texture image. Currently, target must be TEXTURE 2D.
The arguments width, height, format, type, and data correspond precisely to
the corresponding arguments to DrawPixels (refer to section 3.6.3) they
specify the image's width and height, a format of the image data, the type of
those data, and a pointer to the image data in memory. The image is taken
from memory exactly as if these arguments were passed to DrawPixels,
but the process stops just before nal conversion. Each R, G, B, and A
value so extracted is clamped to 0 1]. (The formats STENCIL INDEX and
DEPTH COMPONENT are not allowed.) Components are selected from the R,
G, B, and A values to obtain a texture with components components (the
signi cance of the number of components is described below). Table 3.6
summarizes the mapping of R, G, B, and A values to texture components.




                                 Version 1.0 - 1 July 1994
80                                          CHAPTER 3. RASTERIZATION

           Components       RGBA Values        Texture Components
               1            R                  L
               2            R, A               L, A
               3            R, G, B            C
               4            R, G, B, A         C, A
Table 3.6: Correspondence of texture components to extracted R, G, B, and
A values. See section 3.8.3 for a description of the texture components L,
A, and C .

Specifying a number of components other than 1, 2, 3, or 4 generates the
error INVALID VALUE.
    The image itself (pointed to by data) is a sequence of groups of values.
The rst group is the lower left corner of the texture image. Subsequent
groups ll out rows of width width from left to right height rows are stacked
from bottom to top.
    The level argument to TexImage2D is an integer level-of-detail number.
Levels of detail are discussed below, under Mipmapping. The main texture
image has a level of detail number of 0. If a level-of-detail less than zero or
greater than the base 2 logarithm of the maximum texture width or height
(see below) is speci ed, the error INVALID VALUE is generated.
    The border argument to TexImage2D is a border width. The signi -
cance of borders is described below. The border width a ects the required
dimensions of the texture image: it must be the case that width = 2n + 2b
and height = 2m + 2b. where b is the (non-negative) border width. If width
and height do not satisfy these relationships, then the error INVALID VALUE is
generated. Currently, if b is not either 0 or 1, then the error INVALID VALUE
is generated. The maximum allowable width or height of an image is imple-
mentation dependent, but must be at least 64 (or 64 + 2b with a border of
width b). An excessive width or height, or a width or height less than zero,
generates the INVALID VALUE error.
    Another command,
      void TexImage1D( enum target, int level, int compo-
          nents, sizei width, int border, enum format, enum type,
          void *data )

is used to specify one-dimensional texture images. Currently, target must be




                        Version 1.0 - 1 July 1994
3.8. TEXTURING                                                                81

the texture target TEXTURE 1D. For the purposes of decoding the texture im-
age, TexImage1D is equivalent to calling TexImage2D with correspond-
ing arguments and a height argument of 1, except that the height of the
image is always 1, regardless of the value of border. It must be the case that
width = 2n + 2b for some integer n where b is the value of border, or the
error INVALID VALUE is generated.
    An image with zero height or width (or zero width, for TexImage1D)
indicates the null texture. If the null texture is speci ed for level-of-detail
zero, it is as if texturing were disabled.
    The image indicated to the GL by the image pointer is decoded and
copied into the GL's internal memory. This copying e ectively places the
decoded image inside a border of the maximum allowable width (currently
1) whether or not a border has been speci ed (see Figure 3.10). If no
border or a border smaller than the maximum allowable width has been
speci ed, then the image is still stored as if it were surrounded by a border
of the maximum possible width. Any excess border (which surrounds the
speci ed image, including any border) is assigned unspeci ed values. A
one-dimensional texture has a border only at its left and right ends.
    We shall refer to the (possibly border augmented) decoded image as the
texture array. A two-dimensional texture array has width 2n +2b and height
2m +2b, where b is the maximum allowable border width a one-dimensional
texture array has width 2n + 2b and height 1.
    An element (i j ) of the texture array is called a texel (for a 1-dimensional
texture, j is irrelevant). The texture value used in texturing a fragment is
determined by that fragment's associated (s t) coordinates, but may not
correspond to any actual texel. See Figure 3.10.
    Various parameters control how the texture array is treated when applied
to a fragment. Each parameter is set by calling
      void       TexParameterfifg( enum target, enum pname,
           T param )
      void       TexParameterfifgv( enum target, enum pname,
           T params )

target is the target, either TEXTURE 1D or TEXTURE 2D, pname is a symbolic
constant indicating the parameter to be set the possible constants and cor-
responding parameters are summarized in Table 3.7. In the rst form of the
command, param is a value to which to set a single-valued parameter in the
second form of the command, params is an array of parameters whose type
depends on the parameter being set. If the values for TEXTURE BORDER COLOR




                                 Version 1.0 - 1 July 1994
82                                                       CHAPTER 3. RASTERIZATION




               5.0
                         4
        1.0
                         3

                         2                           α
         t      v    j                                   β
                         1

                         0
        0.0
                     −1
              −1.0
                             −1         0   1    2       3 i 4   5   6   7     8

                     −1.0                                    u                     9.0
                                  0.0                        s               1.0


     Figure 3.10. A texture image and the coordinates used to access it. This is a
     two-dimensional texture with n = 3 and m = 2. A one-dimensional texture
     would consist of a single horizontal strip. and , values used in blending
     adjacent texels to obtain a texture value, are also shown.




                                    Version 1.0 - 1 July 1994
3.8. TEXTURING                                                              83


             Name              Type Legal Values
        TEXTURE WRAP S        integer CLAMP, REPEAT
        TEXTURE WRAP T        integer CLAMP, REPEAT
      TEXTURE MIN FILTER      integer NEAREST,                    LINEAR,
                                        NEAREST MIPMAP NEAREST,
                                        NEAREST MIPMAP LINEAR,
                                        LINEAR MIPMAP NEAREST,
                                        LINEAR MIPMAP LINEAR
      TEXTURE MAG FILTER      integer   NEAREST, LINEAR
     TEXTURE BORDER COLOR     4 oats any 4 values in 0 1]
              Table 3.7: Texture parameters and their values.

are speci ed as integers, the conversion for signed integers from Table 2.4 is
applied to convert the values to oating-point. Each of the four values set
by TEXTURE BORDER COLOR is clamped to lie in 0 1].

Texture Wrap Modes
If TEXTURE WRAP S or TEXTURE WRAP T is set to REPEAT, then the GL ignores
the integer part of s or t coordinates, respectively, using only the fractional
part. (For a number r, the fractional part is r ; brc, regardless of the sign
of r recall that the oor function truncates towards ;1.) CLAMP causes s
or t coordinates to be clamped to the range 0 1]. The initial state is for
both s and t behavior to be that given by REPEAT.

3.8.1 Texture Mini cation
Applying a texture to a primitive implies a mapping from texture image
space to framebu er image space. In general, this mapping involves a recon-
struction of the sampled texture image, followed by a homogeneous warping
implied by the mapping to framebu er space, then a ltering, followed -
nally by a resampling of the ltered, warped, reconstructed image before
applying it to a fragment. In the GL this mapping is approximated by one
of two simple ltering schemes. One of these schemes is selected based on
whether the mapping from texture space to framebu er space is deemed to
magnify or minify the texture image. The choice is governed by a scale fac-




                                Version 1.0 - 1 July 1994
84                                           CHAPTER 3. RASTERIZATION

tor (x y ) and (x y ) log2 (x y )] if (x y ) is less than or equal to some
constant (the selection of the constant is described below in section 3.8.2)
the texture is said to be magni ed if it is greater, the texture is mini ed.
is called the level of detail.
    Let s(x y ) be the function that associates an s texture coordinate with
each set of window coordinates (x y ) that lie within a primitive de ne
t(x y) analogously. Let u(x y ) = 2n s(x y) and v (x y ) = 2mt(x y ) (for a
one-dimensional texture, de ne v (x y ) 0). For a polygon, is given at a
fragment with window coordinates (x y ) by
                     8s                          s               9
                     <                               @u 2 + @v 2 =
               = max : @u      @v
                           2                 2

                        @x   + @x                    @y     @y            (3:7)

where @u=@x indicates the derivative of u with respect to window x, and
similarly for the other derivatives. For a line, the formula is
                   s
               =  @u x + @u y 2 + @v x + @v y 2 l               (3:8)
                  @x       @y          @x     @y
where x = x2 ; x1 and y = y2 ; y1 with (x1 py1) and (x2 y2) being the
segment's window coordinate endpoints and l = x2 + y 2 . For a point,
pixel rectangle, or bitmap,     1.
    While it is generally agreed that equations 3.7 and 3.8 give the best
results when texturing, they are often impractical to implement. Therefore,
an implementation may approximate the ideal with a function f (x y )
subject to these conditions:
     1. f (x y ) is continuous and monotonically increasing in each of j@u=@xj,
        j@u=@yj, j@v=@xj, and j@v=@yj,
     2. Let
           mu = max @x@u @u      and  m    = max @v @v :
                           @y          v         @x @y
       Then maxfmu mv g f (x y ) mu + mv .
    When indicates mini cation, the value assigned to TEXTURE MIN FILTER
is used to determine how the texture value for a fragment is selected. When
TEXTURE MIN FILTER is NEAREST, the texel nearest (in Manhattan distance) to




                         Version 1.0 - 1 July 1994
3.8. TEXTURING                                                              85

that speci ed by (s t) is obtained. This means the texel at location (i j )
becomes the texture value, with i given by
                              (
                          i = b2unc; 1 ss <   1
                                           = 1:                      (3:9)
(Recall that if TEXTURE WRAP S is REPEAT, then 0 s < 1.) Similarly, j is
found as                      (
                          j = b2vmc; 1 tt <   1
                                            = 1:                    (3:10)
For a one-dimensional texture, j is irrelevant the texel at location i becomes
the texture value.
    When TEXTURE MIN FILTER is LINEAR, a 2 2 square of texels is selected.
This square is obtained by rst computing
                (
           i0 = bbuu ; 1=2c mod 2n TEXTURE WRAP S is REPEAT
                     ; 1=2c              TEXTURE WRAP S is CLAMP
and             (
           j0 = bbvv ;
                     ; 1=2c mod 2m TEXTURE WRAP T is REPEAT
                       1=2c              TEXTURE WRAP T is CLAMP:
Then               (
            i1 =       (i0 + 1) mod 2n   TEXTURE WRAP S       is REPEAT
                       i0 + 1            TEXTURE WRAP S       is CLAMP
and                (
           j1 =        (j0 + 1) mod 2m    TEXTURE WRAP T      is REPEAT
                       j0 + 1             TEXTURE WRAP T      is CLAMP:
Let
                    = frac(u ; 1=2) and = frac(v ; 1=2)
where frac(x) denotes the fractional part of x. Let ij be the texel at location
(i j ) in the texture image. Then the texture value, is found as
      = (1 ; )(1 ; ) i0 j0 + (1 ; ) i1 j0 + (1 ; ) i0 j1 + i1 j1 (3:11)
for a two-dimensional texture. For a one-dimensional texture,
                               = (1 ; ) i0 + i1
where i indicates the texel at location i in the one-dimensional texture. If
any of the selected ij (or i ) in the above equations refer to a border texel
with unspeci ed value, then the border color given by the current setting of
TEXTURE BORDER COLOR is used instead of the unspeci ed value or values.




                                  Version 1.0 - 1 July 1994
86                                         CHAPTER 3. RASTERIZATION

Mipmapping
TEXTURE MIN FILTER values NEAREST MIPMAP NEAREST, NEAREST MIPMAP LINEAR,
LINEAR MIPMAP NEAREST, and LINEAR MIPMAP LINEAR each require the use of a
mipmap. A mipmap is an ordered set of arrays representing the same image
each array has a resolution lower than the previous one. If the texture has
dimensions 2n 2m , then there are maxfn mg + 1 mipmap arrays. The
  rst array is the original texture with dimensions 2n 2m . Each subsequent
array has dimensions 2(k;1) 2(l;1) where 2k 2l are the dimensions of the
previous array. This is the case as long as both k > 0 and l > 0. Once either
k = 0 or l = 0, each subsequent array has dimension 1 2(l;1) or 2(k;1) 1,
respectively, until the last array is reached with dimension 1 1.
     Each array in a mipmap is transmitted to the GL using TexImage2D
or TexImage1D the array being set is indicated with the level-of-detail
argument. Level-of-detail numbers proceed from 0 for the original texture
array through p = maxfn mg with each unit increase indicating an array of
half the dimensions of the previous one as already described. If texturing is
enabled (and TEXTURE MIN FILTER is one that requires a mipmap) at the time
a primitive is rasterized and if the set of arrays 0 through p is incomplete,
based on the dimensions of array 0, then it is as if texture mapping were
disabled. The set of arrays 0 through p is incomplete if the numbers of
components in each mipmap array are not the same, or if the border widths
of the mipmap arrays are not the same, or if the dimensions of the mipmap
arrays do not follow the sequence described above. Arrays indexed greater
than p are insigni cant.
     The mipmap is used in conjunction with the level of detail to approx-
imate the application of an appropriately ltered texture to a fragment.
Let p = maxfn mg and let c be the value of at which the transition
from mini cation to magni cation occurs (since this discussion pertains to
mini cation, we are concerned only with values of where > c). For
NEAREST MIPMAP NEAREST, if c <          0:5 then the mipmap array with level-
of-detail of 0 is selected. Otherwise, the dth mipmap array is selected when
d ; 12 <       d + 12 as long as 1 < d < p. If > p + 12 , then the pth mipmap
array is selected. The rules for NEAREST are then applied to the selected
array.
     The same mipmap array selection rules apply for LINEAR MIPMAP NEAREST
as for NEAREST MIPMAP NEAREST, but the rules for LINEAR are applied to the
selected array.
     For NEAREST MIPMAP LINEAR, the level d ; 1 and the level d mipmap arrays




                       Version 1.0 - 1 July 1994
3.8. TEXTURING                                                               87

are selected, where d;1      < d, unless p, in which case the pth mipmap
array is used for both arrays. The rules for NEAREST are then applied to each
of these arrays, yielding two corresponding texture values d;1 and d . The
 nal texture value is then found as
                  = (1 ; frac log2( )]) d;1 + frac log2 ( )] d:
LINEAR MIPMAP LINEAR has the same e ect as NEAREST MIPMAP LINEAR except
that the rules for LINEAR are applied for each of the two mipmap arrays to
generate d;1 and d .
3.8.2 Texture Magni cation
When indicates magni cation, the value assigned to TEXTURE MAG FILTER
determines how the texture value is obtained. There are two possible val-
ues for TEXTURE MAG FILTER: NEAREST and LINEAR. NEAREST behaves exactly as
NEAREST for TEXTURE MIN FILTER (equation 3.9 and 3.10 are used) LINEAR be-
haves exactly as LINEAR for TEXTURE MIN FILTER (equation 3.11 is used). The
level-of-detail 0 texture array is always used for magni cation.
     Finally, there is the choice of c, the mini cation vs. magni cation switch-
over point. If the magni cation lter is given by LINEAR and the mini cation
  lter is given by NEAREST MIPMAP NEAREST or LINEAR MIPMAP NEAREST, then c =
0:5. This is done to ensure that a mini ed texture does not appear \sharper"
than a magni ed texture. Otherwise c = 0.
     The state necessary for texture can be divided into two categories.
First, there are the two sets of mipmap arrays (one-dimensional and two-
dimensional) and their number. Each array has associated with it a width
and height (two-dimensional only), a border width, and a four-valued in-
teger describing the number of components in the image. Each initial
texture array is null (zero width and height, zero border width, 1 com-
ponent). Next, there are the two sets of texture properties each consists
of the selected mini cation and magni cation lters, the wrap modes for
s and t, and the TEXTURE BORDER COLOR. In the initial state, the value as-
signed to TEXTURE MIN FILTER is NEAREST MIPMAP LINEAR, and the value for
TEXTURE MAG FILTER is LINEAR. Both s and t wrap modes are set to REPEAT.
TEXTURE BORDER COLOR is (0,0,0,0).

3.8.3 Texture Environments and Texture Functions
The command




                                Version 1.0 - 1 July 1994
88                                         CHAPTER 3. RASTERIZATION

     void   TexEnvfifg( enum target, enum pname, T param )
     void   TexEnvfifgv( enum target, enum pname, T params )
sets parameters of the texture environment that speci es how texture values
are interpreted when texturing a fragment. target must currently be the sym-
bolic constant TEXTURE ENV. pname is a symbolic constant indicating the pa-
rameter to be set. In the rst form of the command, param is a value to which
to set a single-valued parameter in the second form, params is a pointer to
an array of parameters: either a single symbolic constant or a value or group
of values to which the parameter should be set. The possible environment
parameters are TEXTURE ENV MODE and TEXTURE ENV COLOR. TEXTURE ENV MODE
may be set to one of MODULATE, DECAL, or BLEND TEXTURE ENV COLOR is set to
an RGBA color by providing four single-precision oating-point values in
the range 0 1] (values outside this range are clamped to it). If integers are
provided for TEXTURE ENV COLOR, then they are converted to oating-point as
speci ed in Table 2.4 for signed integers.
    The value of TEXTURE ENV MODE speci es a texture function. The result
of this function depends on the fragment and the texture array value. The
precise form of the function depends on the number of components of the
texture arrays that were last speci ed. In the following table, C is a triple
of color values comprising each of R, G, and B, while A (A) is treated
separately. R, G, B, and A values, after being obtained from a supplied
texture image, are in the range 0 1]. The subscript f indicates a value or
values pertaining to the incoming fragment, t indicates a texture value, and
v indicates the color computed by the texture function. For a one component
image, Lt indicates that single component. For a two component image, Lt
is the rst component, and At is the second. A three component image
has only a color value Ct, while a four component one has a color value Ct
and and alpha value At . The functions for the various combinations are
summarized in Table 3.8.
    The state required for the current texture environment consists of the
three-valued integer indicating the texture function and four oating-point
TEXTURE ENV COLOR values. In the initial state, the texture function is given
by MODULATE and TEXTURE ENV COLOR is (0 0 0 0).

3.8.4 Texture Application
Texturing is enabled or disabled using the generic Enable and Disable com-
mands, respectively, with the symbolic constant TEXTURE 1D or TEXTURE 2D to




                       Version 1.0 - 1 July 1994
3.8. TEXTURING                                                          89




                                Texture Functions
 cpts     MODULATE              DECAL                      BLEND
 1       Cv = LtCf         unde ned         Cv = (1 ; Lt)Cf + LtCc
          Av = Af                                  Av = Af
 2       Cv = LtCf         unde ned         Cv = (1 ; Lt)Cf + LtCc
         Av = AtAf                                Av = At Af
 3       Cv = Ct Cf         Cv = Ct                unde ned
          Av = Af          Av = Af
 4       Cv = Ct Cf Cv = (1 ; At )Cf + AtCt        unde ned
         Av = AtAf         Av = Af
Table 3.8: Texture functions. Multiplication of a color triple by a scalar
means multiplying each of R, G, and B by the scalar multiplying two color
triples means multiplying each component of the second by the correspond-
ing component of the rst. Cc represents the red, green, and blue values
assigned to TEXTURE ENV COLOR. Cf and Cv represent the red, green, and blue
components of the fragment color prior to and after texture application. Af
and Av represent the alpha component of the fragment prior to and after
texture application.




                              Version 1.0 - 1 July 1994
90                                           CHAPTER 3. RASTERIZATION

enable the one-dimensional or two-dimensional texture, respectively. If both
one- and two-dimensional textures are enabled, the two-dimensional texture
is used. If all texturing is disabled, a rasterized fragment is passed on unal-
tered to the next stage of the GL (although its texture coordinates may be
discarded). Otherwise, a texture value is found according to the parameter
values of the currently bound texture image of the appropriate dimension-
ality using the rules given in sections 3.8.1 and 3.8.2. This texture value is
used along with the incoming fragment in computing the texture function
indicated by the currently bound texture environment. The result of this
function replaces the incoming fragment's R, G, B, and A values. These
are the color values passed to subsequent operations. Other data associated
with the incoming fragment remain unchanged, except that the texture co-
ordinates may be discarded.
    The required state is two bits indicating whether each of one- or two-
dimensional texturing is enabled or disabled. In the initial state, all textur-
ing is disabled.

3.9 Fog
If enabled, fog blends a fog color with a rasterized fragment's post-texturing
color using a blending factor f . Fog is enabled and disabled with the Enable
and Disable commands using the symbolic constant FOG.
    This factor f is computed according to one of three equations:
                                f = exp(;d z )                               (3:12)
                              f = exp(;(d z )2) or                           (3:13)
                                   f = ee ;
                                          ;s
                                            z                                (3:14)
(z is the eye-coordinate distance from the eye, (0 0 0 1) in eye coordinates,
to the fragment center). The equation, along with either d or e and s, is
speci ed with
       void Fogfifg( enum pname, T param )
       void Fogfifgv( enum pname, T params )

If pname is FOG MODE, then param must be, or params must point to an integer
that is one of the symbolic constants EXP, EXP2, or LINEAR, in which case
equation 3.12, 3.13, or 3.14, respectively, is selected for the fog calculation (if,




                         Version 1.0 - 1 July 1994
3.9. FOG                                                                    91

when 3.14 is selected, e = s, results are unde ned). If pname is FOG DENSITY,
FOG START,   or FOG END, then param is or params points to a value that is
d, s, or e, respectively. If d, s, or e is speci ed less than zero, the error
INVALID VALUE results.
    An implementation may choose to approximate the eye-coordinate dis-
tance from the eye to each fragment center by jze j. Further, f need not
be computed at each fragment, but may be computed at each vertex and
interpolated as other data are.
    No matter which equation and approximation is used to compute f , the
result is clamped to 0 1] to obtain the nal f .
    f is used di erently depending on whether the GL is in RGBA or color
index mode. In RGBA mode, if Cr represents a rasterized fragment's R, G,
or B value, then the corresponding value produced by fog is
                           C = fCr + (1 ; f )Cf :
(The rasterized fragment's A value is not changed by fog blending.) The R,
G, B, and A values of Cf are speci ed by calling Fog with pname equal to
FOG COLOR in this case params points to four values comprising Cf . If these
are not oating-point values, then they are converted to oating-point using
the conversion given in Table 2.4 for signed integers. Each component of Cf
is clamped to 0 1] when speci ed. If if is a color index, then a single value
speci es if . Its integer part is masked with 2n ; 1, where n is the number
of bits in a color index framebu er.
     In color index mode, the formula for fog blending is
                              I = ir + (1 ; f )if
where ir is the rasterized fragment's color index and if is a single-precision
 oating-point value. (1 ; f )if is rounded to the nearest xed-point value
with the same number of bits to the right of the binary point as ir . In this
case, if is set by calling Fog with pname set to FOG INDEX and param being
or params pointing to the single oating-point value that is if .
    The state required for fog consists of a three valued integer to select the
fog equation, three oating-point values d, e, and s, an RGBA fog color and
a fog color index, and a single bit to indicate whether or not fog is enabled.
In the initial state, fog is disabled, FOG MODE is EXP, d = 1:0, e = 1:0, and
s = 0:0 Cf = (0 0 0 0) and if = 0.




                                Version 1.0 - 1 July 1994
92                                          CHAPTER 3. RASTERIZATION

3.10 Antialiasing Application
Finally, if antialiasing is enabled for the primitive from which a rasterized
fragment was produced, then the computed coverage value is applied to the
fragment. In RGBA mode, the value is multiplied by the fragment's alpha
(A) value to yield a nal alpha value. In color index mode, the value is used
to set the low order bits of the color index value as described in section 3.2.




                        Version 1.0 - 1 July 1994
Chapter 4
Per-Fragment Operations
and the Framebu er
The framebu er consists of a set of pixels arranged as a two-dimensional
array. The height and width of this array may vary from one GL imple-
mentation to another. For purposes of this discussion, each pixel in the
framebu er is simply a set of some number of bits. The number of bits
per pixel may also vary depending on the particular GL implementation or
context.
     Corresponding bits from each pixel in the framebu er are grouped to-
gether into a bitplane each bitplane contains a single bit from each pixel.
These bitplanes are grouped into several logical bu ers. These are the color,
depth, stencil, and accumulation bu ers. The color bu er actually consists
of a number of bu ers: the front left bu er, the front right bu er, the back
left bu er, the back right bu er, and some number of auxiliary bu ers. Typ-
ically the contents of the front bu ers are displayed on a color monitor while
the contents of the back bu ers are invisible. (Monoscopic contexts display
only the front left bu er stereoscopic contexts display both the front left
and the front right bu ers.) The contents of the auxiliary bu ers are never
visible. All color bu ers must have the same number of bitplanes, although
an implementation or context may choose not to provide right bu ers, back
bu ers, or auxiliary bu ers at all. Further, an implementation or context
may not provide depth, stencil, or accumulation bu ers.
     Color bu ers consist of either unsigned integer color indices or R, G,
B, and, optionally, A unsigned integer values. The number of bitplanes
in each of the color bu ers, the depth bu er, the stencil bu er, and the
                                      93




                                Version 1.0 - 1 July 1994
94                CHAPTER 4. FRAGMENTS AND THE FRAMEBUFFER



      Fragment               Pixel                                              Alpha
          +                                          Scissor
                           Ownership                                             Test
                                                      Test                   (RGBA Only)
     Associated              Test
        Data




                                      Depth buffer               Stencil
                                         Test                     Test



                       Framebuffer              Framebuffer


                           Blending                                           Logicop              To
                                                 Dithering
                           (RGBA Only)                                     (colorindex only)   Framebuffer



             Framebuffer                                       Framebuffer



     Figure 4.1. Per-fragment operations.


accumulation bu er is xed and window dependent. If an accumulation
bu er is provided, it must have at least as many bitplanes per R, G, and B
color component as do the color bu ers.
    The initial state of all provided bitplanes is unde ned.

4.1 Per-Fragment Operations
A fragment produced by rasterization with window coordinates of (xw yw )
modi es the pixel in the framebu er at that location based on a number of
parameters and conditions. We describe these modi cations and tests, dia-
grammed in Figure 4.1, in the order in which they are performed. Figure 4.1
diagrams these modi cations and tests.

4.1.1 Pixel Ownership Test
The rst test is to determine if the pixel at location (xw yw ) in the frame-
bu er is currently owned by the GL (more precisely, by this GL context). If




                                 Version 1.0 - 1 July 1994
4.1. PER-FRAGMENT OPERATIONS                                                 95

it is not, the window system decides the fate the incoming fragment. Pos-
sible results are that the fragment is discarded or that some subset of the
subsequent per-fragment operations are applied to the fragment. This test
allows the window system to control the GL's behavior, for instance, when
a GL window is obscured.
4.1.2 Scissor test
The scissor test determines if (xw yw ) lies within the scissor rectangle de ned
by four values. These values are set with
       void    Scissor( int left, int bottom, sizei width,
          sizei height )

If left xw < left + width and bottom yw < bottom + height, then the
scissor test passes. Otherwise, the test fails and the fragment is discarded.
The test is enabled or disabled using Enable or Disable using the con-
stant SCISSOR TEST. When disabled, it is as if the scissor test always passes.
If either width or height is less than zero, then the error INVALID VALUE is
generated. The state required consists of four integer values and a bit
indicating whether the test is enabled or disabled. In the initial state
left = bottom = 0 width and height are determined by the size of the
GL window. Initially, the scissor test is disabled.
4.1.3 Alpha test
This step applies only in RGBA mode. In color index mode, proceed to the
next step. The alpha test discards a fragment conditional on the outcome of
a comparison between the incoming fragment's alpha value and a constant
value. The comparison is enabled or disabled with the generic Enable and
Disable commands using the symbolic constant ALPHA TEST. When disabled,
it is as if the comparison always passes. The test is controlled with
       void AlphaFunc( enum func, clampf ref )

func is a symbolic constant indicating the alpha test function ref is a refer-
ence value. ref is clamped to lie in 0 1], and then converted to a xed-point
value according to the rules given for an A component in section 2.12.9. For
purposes of the alpha test, the fragment's alpha value is also rounded to
the nearest integer. The possible constants specifying the test function are
NEVER, ALWAYS, LESS, LEQUAL, EQUAL, GEQUAL, GREATER, or NOTEQUAL, meaning




                                Version 1.0 - 1 July 1994
96            CHAPTER 4. FRAGMENTS AND THE FRAMEBUFFER

pass the fragment never, always, if the fragment's alpha value is less than,
less than or equal to, equal to, greater than or equal to, greater than, or not
equal to the reference value, respectively.
    The required state consists of the oating-point reference value, an eight-
valued integer indicating the comparison function, and a bit indicating if the
comparison is enabled or disabled. The initial state is for the reference value
to be 0 and the function to be ALWAYS. Initially, the alpha test is disabled.
4.1.4 Stencil test
The stencil test conditionally discards a fragment based on the outcome of a
comparison between the value in the stencil bu er at location (xw yw ) and
a reference value. The test is controlled with
      void StencilFunc( enum func, int ref, uint mask )
      void StencilOp( enum sfail, enum dpfail, enum dppass )

The test is enabled or disabled with the Enable and Disable commands, us-
ing the symbolic constant STENCIL TEST. When disabled, the stencil test and
associated modi cations are not made, and the fragment is always passed.
    ref is an integer reference value that is used in the unsigned stencil com-
parison. It is clamped to the range 0 2s ; 1], where s is the number of bits
in the stencil bu er. func is a symbolic constant that determines the stencil
comparison function the eight symbolic constants are NEVER, ALWAYS, LESS,
LEQUAL, EQUAL, GEQUAL, GREATER, or NOTEQUAL. Accordingly, the stencil test
passes never, always, if the reference value is less than, less than or equal to,
equal to, greater than or equal to, greater than, or not equal to the masked
stored value in the stencil bu er. The s least signi cant bits of mask are
bitwise ANDed with both the reference and the stored stencil value. The
ANDed values are those that participate in the comparison.
    StencilOp takes three arguments that indicate what happens to the
stored stencil value if this or certain subsequent tests fail or pass. sfail
indicates what action is taken if the stencil test fails. The symbolic constants
are KEEP, ZERO, REPLACE, INCR, DECR, and INVERT. These correspond to keeping
the current value, setting it to zero, replacing it with the reference value,
incrementing it, decrementing it, or bitwise inverting it. For purposes of
increment and decrement, the stencil bits are considered as an unsigned
integer values clamp at 0 and the maximum representable value. The same
symbolic values are given to indicate the stencil action if the depth bu er
test (below) fails (dpfail), or if it passes (dppass).




                        Version 1.0 - 1 July 1994
4.1. PER-FRAGMENT OPERATIONS                                                   97

    If the stencil test fails, the incoming fragment is discarded. The state
required consists of the most recent values passed to StencilFunc and Sten-
cilOp, and a bit indicating whether stencil testing is enabled or disabled.
In the initial state, stenciling is disabled, the stencil reference value is zero,
the stencil comparison function is ALWAYS, and the stencil mask is all ones.
Initially, all three stencil operations are KEEP. If there is no stencil bu er, no
stencil modi cation can occur, and it is as if the stencil tests always pass,
regardless of any calls to StencilOp.
4.1.5 Depth bu er test
The depth bu er test discards the incoming fragment if a depth comparison
fails. The comparison is enabled or disabled with the generic Enable and
Disable commands using the symbolic constant DEPTH TEST. When disabled,
the depth comparison and subsequent possible updates to the depth bu er
value are bypassed and the fragment is passed to the next operation. The
stencil value, however, is modi ed as indicated below as if the depth bu er
test passed. If enabled, the comparison takes place and the depth bu er and
stencil value may subsequently be modi ed.
     The comparison is speci ed with
        void DepthFunc( enum func )

This command takes a single symbolic constant: one of NEVER, ALWAYS, LESS,
LEQUAL, EQUAL, GREATER, GEQUAL, NOTEQUAL. Accordingly, the depth bu er test
passes never, always, if the incoming fragment's zw value is less than, less
than or equal to, equal to, greater than, greater than or equal to, or not equal
to the depth value stored at the location given by the incoming fragment's
(xw yw ) coordinates.
     If the depth bu er test fails, the incoming fragment is discarded. The
stencil value at the fragment's (xw yw ) coordinates is updated according to
the function currently in e ect for depth bu er test failure. Otherwise, the
fragment continues to the next operation and the value of the depth bu er
at the fragment's (xw yw ) location is set to the fragment's zw value. In this
case the stencil value is updated according to the function currently in e ect
for depth bu er test success.
     The necessary state is an eight-valued integer and a single bit indicating
whether depth bu ering is enabled or disabled. In the initial state the
function is LESS and the test is disabled.
     If there is no depth bu er, it is as if the depth bu er test always passes.




                                 Version 1.0 - 1 July 1994
98            CHAPTER 4. FRAGMENTS AND THE FRAMEBUFFER

4.1.6 Blending
Blending combines the incoming fragment's R, G, B, and A values with the
R, G, B, and A values stored in the framebu er at the incoming fragment's
(xw yw ) location. This blending is dependent on the incoming fragment's
alpha value and that of the corresponding currently stored pixel. Blending
applies only in RGBA mode in color index mode it is bypassed. Blending
is enabled or disabled using Enable or Disable with the symbolic constant
BLEND. If it is disabled, proceed to the next stage.
    The command that controls blending is
       void BlendFunc( enum src, enum dst )

src indicates how to compute a source blending factor, while dst indicates
how to compute a destination factor. The possible arguments and their
corresponding computed source and destination factors are summarized in
Tables 4.1 and 4.2. In these tables, A is a single alpha value, and C is a
quadruplet of R, G, B, and A values. A subscript of s indicates a value
from an incoming fragment one of d indicates the corresponding current
framebu er value. Division of a quadruplet by a scalar means dividing each
element by that value. Addition or subtraction of quadruplets or triplets
means adding or subtracting them component-wise.
    The computations in Tables 4.1 and 4.2 are e ectively carried out in
  oating-point and yield oating-point blending factors. Destination (frame-
bu er) components referred to in the tables are taken to be xed-point val-
ues represented according to the scheme given in section 2.12.9 (Final Color
Processing), as are source (fragment) components. Any implied conversion
to oating-point must leave 0 and 1 invariant.
    The computed source and destination blending quadruplets are applied
to the source and destination R, G, B, and A values to obtain a new set of
values that are sent to the next operation. Let the source and destination
blending quadruplets be S and D, respectively. Then a quadruplet of values
is computed as
                                  Cs S + CdD
where multiplication of quadruplets means multiplying them component-
wise. Then each value in this quadruplet is clamped to 2n ; 1, where n is
the number of bits allocated to that color component in the framebu er,
and the four values are sent to the next operation.
    The state required is two integers indicating the source and destina-
tion blending functions and a bit indicating whether blending is enabled




                       Version 1.0 - 1 July 1994
4.1. PER-FRAGMENT OPERATIONS                                             99




            Value                   Blend Factors
            ZERO                    (0 0 0 0)
            ONE                     (1 1 1 1)
            DST COLOR               Rd Gd Bd Ad
            ONE MINUS   DST COLOR   (1 1 1 1) ; (Rd Gd Bd Ad )
            SRC ALPHA               (As As As As )
            ONE MINUS   SRC ALPHA   (1 1 1 1) ; (As As As As )
            DST ALPHA               (Ad Ad Ad Ad )
            ONE MINUS   DST ALPHA   (1 1 1 1) ; (Ad Ad Ad Ad)
            SRC ALPHA   SATURATE    (f f f 1)
Table 4.1: Values controlling the source blending function and the source
blending values they compute. f = min(As 1 ; Ad ).




            Value                   Blend factors
            ZERO                    (0 0 0 0)
            ONE                     (1 1 1 1)
            SRC COLOR               Rs Gs Bs As
            ONE MINUS SRC COLOR     (1 1 1 1) ; (Rs Gs Bs As )
            SRC ALPHA               (As As As As )
            ONE MINUS SRC ALPHA     (1 1 1 1) ; (As As As As)
            DST ALPHA               (Ad Ad Ad Ad)
            ONE MINUS DST ALPHA     (1 1 1 1) ; (Ad Ad Ad Ad )
Table 4.2: Values controlling the destination blending function and the des-
tination blending values they compute.




                               Version 1.0 - 1 July 1994
100           CHAPTER 4. FRAGMENTS AND THE FRAMEBUFFER

or disabled. The initial state of the blending functions is ONE for the source
function and ZERO for the destination function initially, blending is disabled.
    Blending occurs once for each color bu er currently enabled for writing
(section 4.2.1) using each bu er's color for Cd . If a color bu er has no A
value, then it is as if the destination A value is 1.

4.1.7 Dithering
Dithering selects between two color values or indices. In RGBA mode, con-
sider the value of any of the color components as a xed-point value with m
bits to the left of the binary point, where m is the number of bits allocated
to that component in the framebu er call each such value c. For each c,
dithering selects a value c1 such that c1 2 fmaxf0 dce; 1g dceg (after this
selection, treat c1 as a xed point value in 0,1] with m bits). This selec-
tion may depend on the xw and yw coordinates of the pixel. In color index
mode, the same rule applies with c being a single color index. c must not be
larger than the maximum value representable in the framebu er for either
the component or the index, as appropriate.
    Many dithering algorithms are possible, but a dithered value produced
by any algorithm must depend only the incoming value and the fragment's x
and y window coordinates. If dithering is disabled, then each color compo-
nent is truncated to a xed-point value with as many bits as there are in the
corresponding component in the framebu er a color index is rounded to the
nearest integer representable in the color index portion of the framebu er.
    Dithering is enabled with Enable and disabled with Disable using the
symbolic constant DITHER. The state required is thus a single bit. Initially,
dithering is enabled. In RGBA mode, this is the last operation, and the
result goes into the framebu er. In color index mode, continue on to the
last operation.

4.1.8 Logical Operation
Finally, a logical operation is applied between the incoming fragment and
the value stored at the corresponding location in the framebu er the result
replaces the current framebu er value. The logical operation is enabled or
disabled with Enable or Disable using the symbolic constant LOGIC OP.
The logical operation is selected by
      void   LogicOp(    enum   op )




                        Version 1.0 - 1 July 1994
4.1. PER-FRAGMENT OPERATIONS                                            101


                       Argument value Operation
                       CLEAR          0
                       AND                 s^d
                       AND REVERSE         s ^ :d
                       COPY                s
                       AND INVERTED        :s ^ d
                       NOOP                d
                       XOR                 s xor d
                       OR                  s_d
                       NOR                 :(s _ d)
                       EQUIV               :(s xor d)
                       INVERT              :d
                       OR REVERSE          s _ :d
                       COPY INVERTED       :s
                       OR INVERTED         :s _ d
                       NAND                :(s ^ d)
                       SET           1
 Table 4.3: Arguments to LogicOp and their corresponding operations.



op is a symbolic constant. The possible constants and the corresponding
logical operations are enumerated in Table 4.3 in this table, s is the value
of the incoming fragment and d is the value stored in the framebu er.
    Note that the SET operation sets all bits of the result to 1. The result
replaces the value in the framebu er at the fragment's (x y ) coordinates.
The numeric values assigned to the symbolic constants are the same as the
those assigned to the corresponding symbolic values in the X window system.
    LogicOp applies only in color index mode in RGBA mode it does not
occur and the previous operation is the last one applied to incoming frag-
ments. LogicOp occurs once for each color bu er selected for writing. The
required state is an integer indicating the logical operation, and a bit to
indicate whether the logical operation is enabled or disabled. The initial
state is for the logic operation to be given by COPY, and it is disabled.




                               Version 1.0 - 1 July 1994
102           CHAPTER 4. FRAGMENTS AND THE FRAMEBUFFER

4.2 Whole Framebu er Operations
The preceding sections described the operations that occur as individual
fragments are sent to the framebu er. This section describes operations
that control or a ect the whole framebu er.
4.2.1 Selecting a Bu er for Writing
The rst such operation is controlling the bu er into which color values are
written. This is accomplished with
      void   DrawBu er(     enum   buf )
buf is a symbolic constant specifying zero, one, two, or four bu ers for writ-
ing. The constants are NONE, FRONT LEFT, FRONT RIGHT, BACK LEFT, BACK RIGHT,
FRONT, BACK, LEFT, RIGHT, FRONT AND BACK, and AUX0 through AUXn, where n +1
is the number of available auxiliary bu ers.
    The constants refer to the four potentially visible bu ers front left,
front right, back left, and back right, and to the auxiliary bu ers. Argu-
ments other than AUXi that omit reference to LEFT or RIGHT refer to both left
and right bu ers. Arguments other than AUXi that omit reference to FRONT
or BACK refer to both front and back bu ers. AUXi enables drawing only to
auxiliary bu er i. Each AUXi adheres to AUXi = AUX0 + i. The constants and
the bu ers they indicate are summarized in Table 4.4. If DrawBu er is
is supplied with a constant (other than NONE) that does not indicate any of
the color bu ers allocated to the GL context, the error INVALID OPERATION
results.
    Indicating a bu er or bu ers using DrawBu er causes subsequent pixel
color value writes to a ect the indicated bu ers. If more than one color
bu er is selected for drawing, blending and logical operations are computed
and applied independently for each bu er. Calling DrawBu er with a
value of NONE inhibits the writing of color values to any bu er.
    Monoscopic contexts include only left bu ers, while stereoscopic contexts
include both left and right bu ers. Likewise, single bu ered contexts include
only front bu ers, while double bu ered contexts include both front and back
bu ers. The type of context is selected at GL initialization.
    The state required to handle bu er selection is a set of up to 4 + n bits.
4 bits indicate if the front left bu er, the front right bu er, the back left
bu er, or the back right bu er, are enabled for color writing. The other n
bits indicate which of the auxiliary bu ers is enabled for color writing. In




                       Version 1.0 - 1 July 1994
4.2. WHOLE FRAMEBUFFER OPERATIONS                                               103


             symbolic         front front back back aux
             constant          left right left right i
             NONE
             FRONT LEFT
             FRONT RIGHT
             BACK LEFT
             BACK RIGHT
             FRONT
             BACK
             LEFT
             RIGHT
             FRONT AND BACK
             AUXi

Table 4.4: Arguments to DrawBu er and the bu ers that they indicate.

the initial state, the front bu er or bu ers are enabled if there are no back
bu ers otherwise, only the back bu er or bu ers are enabled.
4.2.2 Fine Control of Bu er Updates
Four commands are used to mask the writing of bits to each of the logical
framebu ers after all per-fragment operations have been performed. The
commands
     void   IndexMask( uint mask )
     void    ColorMask( boolean r,            boolean       g,   boolean   b,
        boolean   a)
control the color bu er or bu ers (depending on which bu ers are currently
indicated for writing). The least signi cant n bits of mask, where n is the
number of bits in a color index bu er, specify a mask. Where a 1 appears
in this mask, the corresponding bit in the color index bu er (or bu ers) is
written where a 0 appears, the bit is not written. This mask applies only in
color index mode. In RGBA mode, ColorMask is used to mask the writing
of R, G, B and A values to the color bu er or bu ers. r, g, b, and a indicate
whether R, G, B, or A values, respectively, are written or not (a value of
TRUE means that the corresponding value is written). In the initial state, all




                                Version 1.0 - 1 July 1994
104            CHAPTER 4. FRAGMENTS AND THE FRAMEBUFFER

bits (in color index mode) and all color values (in RGBA mode) are enabled
for writing.
    The depth bu er can be enabled or disabled for writing zw values using
      void   DepthMask(     boolean      mask )
If mask is non-zero, the depth bu er is enabled for writing otherwise, it is
disabled. In the initial state, the depth bu er is enabled for writing.
    The command
      void   StencilMask(    uint   mask )
controls the writing of particular bits into the stencil planes. The least
signi cant s bits of mask comprise an integer mask (s is the number of bits
in the stencil bu er), just as for IndexMask. The initial state is for the
stencil plane mask to be all ones.
    The state required for the various masking operations is two integers and
a bit: an integer for color indices, an integer for stencil values, and a bit
for depth values. A set of four bits is also required indicating which color
components of an RGBA value should be written. In the initial state, the
integer masks are all ones as are the bits controlling depth value and RGBA
component writing.

4.2.3 Clearing the Bu ers
The GL provides a means for setting portions of every pixel in a particular
bu er to the same value. The argument to
      void   Clear(   bitfield   buf )
is the bitwise OR of a number of values indicating which bu ers
are to be cleared. The values are COLOR BUFFER BIT, DEPTH BUFFER BIT,
STENCIL BUFFER BIT, and ACCUM BUFFER BIT, indicating the bu ers currently
enabled for color writing, the depth bu er, the stencil bu er, and the accu-
mulation bu er (see below), respectively. The value to which each bu er is
cleared depends on the setting of the clear value for that bu er. If the mask
is not a bitwise OR of the speci ed values, then the error INVALID VALUE is
generated.
      void   ClearColor( clampf r, clampf g, clampf b, clampf a )




                       Version 1.0 - 1 July 1994
4.2. WHOLE FRAMEBUFFER OPERATIONS                                             105

sets the clear value for the color bu ers in RGBA mode. Each of the speci ed
components is clamped to 0 1] and converted to xed-point according to
the rules of section 2.12.9.
       void ClearIndex( float index )

sets the clear color index. index is converted to a xed-point value with
unspeci ed precision to the left of the binary point the integer part of this
value is then masked with 2m ; 1, where m is the number of bits in a color
index value stored in the framebu er.
       void ClearDepth( clampd d )

takes a oating-point value that is clamped to the range 0 1] and con-
verted to xed-point according to the rules for a window z value given in
section 2.9.1. Similarly,
       void ClearStencil( int s )

takes a single integer argument that is the value to which to clear the stencil
bu er. s is masked to the number of bitplanes in the stencil bu er.
       void ClearAccum( float r, float g, float b, float a )

takes four oating-point arguments that are the values, in order, to which
to set the R, G, B, and A values of the accumulation bu er (see the next
section). These values are clamped to the range ;1 1] when they are spec-
i ed.
     When Clear is called, the only per-fragment operations that are applied
(if enabled) are the pixel ownership test, the scissor test, and dithering. The
masking operations described in the last section (4.2.2) are also e ective. If
a bu er is not present, then a Clear directed at that bu er has no e ect.
     The state required for clearing is a clear value for each of the color bu er,
the depth bu er, the stencil bu er, and the accumulation bu er. Initially,
the RGBA color clear value is (0,0,0,0), the clear color index is 0, and the
stencil bu er and accumulation bu er clear values are all 0. The depth
bu er clear value is initially 1.0.
4.2.4 The Accumulation Bu er
Each portion of a pixel in the accumulation bu er consists of four values: one
for each of R, G, B, and A. The accumulation bu er is controlled exclusively
through the use of




                                 Version 1.0 - 1 July 1994
106           CHAPTER 4. FRAGMENTS AND THE FRAMEBUFFER

      void   Accum(    enum   op, float value )

(except for clearing it). op is a symbolic constant indicating an accumula-
tion bu er operation, and value is a oating-point value to be used in that
operation. The possible operations are ACCUM, LOAD, RETURN, MULT, and ADD.
    The accumulation bu er operations apply identically to every pixel, so
we describe the e ect of each operation on an individual pixel. Accumulation
bu er values are taken to be signed values in the range ;1 1]. Using ACCUM
obtains R, G, B, and A components from the bu er currently selected for
reading (section 4.3.2). Each component, considered as a xed-point value
in 0,1] (see section 2.12.9), is converted to oating-point. Each result is then
multiplied by value. The results of this multiplication are then added to the
corresponding color component currently in the accumulation bu er, and
the resulting color value replaces the current accumulation bu er color value.
The LOAD operation has the same e ect as ACCUM, but the computed values
replace the corresponding accumulation bu er components rather than being
added to them.
    The RETURN operation takes each color value from the accumulation
bu er, multiplies each of the R, G, B, and A components by value. The
resulting color value is placed in the bu ers currently enabled for color writ-
ing as if it were a fragment produced from rasterization, except that the only
per-fragment operations applied are the pixel ownership test and, if enabled,
dithering (section 4.1) color masking (section 4.2.2) is also applied.
    The MULT operation multiplies each R, G, B, and A in the accumulation
bu er by value and then returns the scaled color components to their corre-
sponding accumulation bu er locations. ADD is the same as MULT except that
value is added to each of the color components.
    The color components operated on by Accum must be clamped only
if the operation is RETURN. In this case, a value sent to the enabled color
bu ers is rst clamped to 0 1]. Otherwise, results are unde ned if the
result of an operation on a color component is too large (in magnitude) to
be represented by the number of available bits. When the scissor test is
enabled (section 4.1.2), then only those pixels within the current scissor box
are updated by any Accum operation otherwise, all pixels in the window
are updated. If there is no accumulation bu er, or if the GL is in color index
mode, Accum generates the error INVALID OPERATION.
    No state (beyond the accumulation bu er itself) is required for accumu-
lation bu ering.




                        Version 1.0 - 1 July 1994
4.3. DRAWING, READING, AND COPYING PIXELS                                 107

4.3 Drawing, Reading, and Copying Pixels
Pixels may be written to and read from the framebu er using the Draw-
Pixels and ReadPixels commands. CopyPixels can be used to copy a
block of pixels from one portion of the framebu er to another.

4.3.1 Writing to the Stencil Bu er
The operation of DrawPixels was described in section 3.6.3, except if the
format argument was STENCIL INDEX. In this case, all operations described for
DrawPixels take place, but window (x y) coordinates, each with the corre-
sponding stencil index, are produced in lieu of fragments. Each coordinate-
stencil index pair is sent directly to the per-fragment operations, bypassing
the texture, fog, and antialiasing application stages of rasterization. Each
pair is then treated as a fragment for purposes of the pixel ownership and
scissor tests all other per-fragment operations are bypassed. Finally, each
stencil index is written to its indicated location in the framebu er, subject
to the current setting of StencilMask.
    The error INVALID OPERATION results if there is no stencil bu er.

4.3.2 Reading Pixels
The method for reading pixels from the framebu er and placing them in
client memory is diagrammed in Figure 4.2. We describe the stages of the
pixel reading process in the order in which they occur.
    Pixels are read using
     void   ReadPixels(   int x, int y, sizei      width, sizei height,
        enum   format, enum type, void *data )
The arguments after x and y to ReadPixels correspond to those of Draw-
Pixels. The pixel storage modes that apply to ReadPixels are summarized
in Table 4.5.

Obtaining Pixels from the Framebu er
If the format is DEPTH COMPONENT, then values are obtained from the depth
bu er. If there is no depth bu er, the error INVALID OPERATION occurs. If
the format is STENCIL INDEX, then values are taken from the stencil bu er
again, if there is no stencil bu er, the error INVALID OPERATION occurs. For




                               Version 1.0 - 1 July 1994
108                      CHAPTER 4. FRAGMENTS AND THE FRAMEBUFFER




                                                                                    mask
                                                                                     to
                                                     shift         index−>index
            Index                                                                 [0.0,2n−1]
           (stencil,                                 offset           lookup
           colorindex)

                                                                                        Pixel
                                                                   index−>RGBA          Transfer
      Pixels from                                                     lookup            Modes
      Framebuffer


                                                                                   clamp
                                  map                                                to
             RGBA                                    scale         RGBA−>RGBA
                                   to                                               [0,1]
              Z                                      bias             lookup
                                  [0,1]




                                                              convert
                                                     L
                                                                to
          byte short long float                                  L
                                                                                        Pixel
              Data Stream                           RGBA
                                           pack                                         Storage
         (index or component)                            Z                              Modes
               to memory                            Index




  Figure 4.2. Operation of ReadPixels. The parameters controlling the stages
  above the dotted line are set with PixelTransfer or PixelMap while those
  controlling the stages below the line are set with PixelStore.




               Parameter Name                      Type Initial Value Valid Range
               PACK SWAP BYTES                    boolean   FALSE     TRUE/FALSE
                PACK LSB FIRST                    boolean   FALSE     TRUE/FALSE
               PACK ROW LENGTH                    integer      0          0 1)
                PACK SKIP ROWS                    integer      0          0 1)
               PACK SKIP PIXELS                   integer      0          0 1)
                PACK ALIGNMENT                    integer      4        1,2,4,8
          Table 4.5: PixelStore parameters pertaining to ReadPixels.




                                          Version 1.0 - 1 July 1994
4.3. DRAWING, READING, AND COPYING PIXELS                                 109

all other formats, the bu er from which values are obtained is one of the
color bu ers the selection of color bu er is controlled with ReadBu er.
     The command
       void ReadBu er( enum src )

takes a symbolic constant as argument. The possible values are FRONT LEFT,
FRONT RIGHT, BACK LEFT, BACK RIGHT, FRONT, BACK, LEFT, RIGHT, and AUX0
through AUXn. FRONT and LEFT refer to the front left bu er, BACK refers
to the back left bu er, and RIGHT refers to the front right bu er. The other
constants correspond directly to the bu ers that they name. If the requested
bu er is missing, then the error INVALID OPERATION is generated. The ini-
tial setting for ReadBu er is FRONT if there is no back bu er and BACK
otherwise.
     ReadPixels obtains values from the selected bu er from each pixel with
lower left hand corner at (x + i y + j ) for 0 i < width and 0 j <
height this pixel is said to be the ith pixel in the j th row. If any of these
pixels lies outside of the window allocated to the current GL context, the
values obtained for those pixels are unde ned. Results are also unde ned
for individual pixels that are not owned by the current context. Otherwise,
ReadPixels obtains values from the selected bu er, regardless of how those
values were placed there.
     The number of values obtained from the selected bu er depends on the
format. If the format is LUMINANCE, R, G, and B values are obtained, while
if it is LUMINANCE ALPHA, then R, G, B, and A values are obtained. If the
framebu er does not support alpha values then the A that is obtained is
1.0. If the format is one of RED, GREEN, BLUE, ALPHA, RGB, RGBA, LUMINANCE, or
LUMINANCE ALPHA, and the GL is in color index mode, then the color index
is obtained. Otherwise, Table 3.5 gives the type and number of values that
are obtained from the selected bu er for each pixel.
Conversion of RGBA values
This step applies only if the GL is in RGBA mode, and then only if format
is neither STENCIL INDEX nor DEPTH COMPONENT. The error INVALID OPERATION
results (in RGBA mode) if format is COLOR INDEX.
    The R, G, and B (and possibly A) values form a group of elements. Each
element is taken to be a xed-point value in 0,1] with m bits, where m is the
number of bits in the corresponding color component of the selected bu er
(see section 2.12.9).




                                Version 1.0 - 1 July 1994
110           CHAPTER 4. FRAGMENTS AND THE FRAMEBUFFER

Conversion of Depth values
This step applies only if format is DEPTH COMPONENT. An element is taken to
be a xed-point value in 0,1] with m bits, where m is the number of bits in
the depth bu er (see section 2.9.1).

Arithmetic on components
This step applies only to component groups. An R element is multiplied by
RED SCALE, a G element by GREEN SCALE, a B element by BLUE SCALE, and an
A element by ALPHA SCALE a depth component is multiplied by DEPTH SCALE.
Next, RED BIAS, GREEN BIAS, BLUE BIAS, ALPHA BIAS, or DEPTH BIAS is added
to each resulting element, as appropriate.

Arithmetic on Indices
This step applies only to indices. After the index is obtained from the
selected bu er, the corresponding step for DrawPixels is applied to the
integer index (there are no bits to the right of the binary point in this case).

RGBA to RGBA Lookup
This step applies only to RGBA component groups. It is identical to the
corresponding step for DrawPixels.

Index Lookup
This step applies only to indices. If format is one of RED, GREEN, BLUE,
ALPHA, RGB, RGBA, LUMINANCE, or LUMINANCE ALPHA, then the index is used to
reference 4 tables of color components: PIXEL MAP I TO R, PIXEL MAP I TO G,
PIXEL MAP I TO B, and PIXEL MAP I TO A. Each of these tables must have 2n
entries for some integer value of n (n may be di erent for each table). For
each table, the index is rst rounded to the nearest integer this value is
ANDed with 2n ; 1, and the resulting value used as an address into the
table. The indexed value becomes an R, G, B, or A value, as appropriate.
The group of four elements so obtained replaces the index, changing the
group's type to \component."
    If the format is COLOR INDEX and if MAP COLOR is TRUE, then the index is
looked up in the PIXEL MAP I TO I table (otherwise, the index is not looked
up). Again, the table must have 2n entries for some n, and the integer part




                        Version 1.0 - 1 July 1994
4.3. DRAWING, READING, AND COPYING PIXELS                                 111

of the index is ANDed with 2n ; 1, producing a value. This value addresses
the table, and the value in the table replaces the index. The oating-point
table value is rst rounded to a xed-point value with unspeci ed precision.
    Finally, if format is STENCIL INDEX and if MAP STENCIL is TRUE, then the
index is looked up as described in the preceding paragraph, but using the
PIXEL MAP S TO S table.

Conversion to L
This step applies only to RGBA component groups, and only if the format
is either LUMINANCE or LUMINANCE ALPHA. A value L is computed as
                              L = R+G+B
where R, G, and B are the values of the R, G, and B components. The
single computed L component replaces the R, G, and B components in the
group.
Final Conversion
For an index, if the type is not FLOAT, nal conversion consists of masking
the index with the value given Table 4.6 if the type is FLOAT, then the inte-
ger index is converted to single-precision oating-point. For a component,
each component is rst clamped to 0 1]. Then, the appropriate conversion
formula from Table 4.6 is applied to the component.
Placement in Client Memory
Groups of elements are placed in memory just as they are taken from memory
for DrawPixels. That is, the ith group of the j th row (corresponding to
the ith pixel in the j th row) is placed in memory just where the ith group of
the j th row would be taken from for DrawPixels. See Unpacking under
section 3.6.3. The only di erence is that the storage mode parameters whose
names begin with PACK are used instead of those whose names begin with
UNPACK . If the format is RED, GREEN, BLUE, ALPHA, or LUMINANCE, only the
corresponding single element is written. Otherwise the number of elements
to be written is given by Table 3.5.
    In correspondence with DrawPixels, if PACK SWAP BYTES is TRUE, there
is no e ect on a one-byte element, but bytes constituting a two-byte or
four-byte element are reversed (so that they are in an order opposite to the




                                Version 1.0 - 1 July 1994
112           CHAPTER 4. FRAGMENTS AND THE FRAMEBUFFER

                type      Index Mask Component Conversion
           UNSIGNED BYTE     28 ; 1              (28 ; 1)c
                 BYTE        2 ;1
                               7             (2 ; 1)c ; 1]=2
                                               8

               BITMAP            1                   1
          UNSIGNED SHORT     216 ; 1            (216 ; 1)c
                SHORT        215 ; 1        (216 ; 1)c ; 1]=2
           UNSIGNED INT      2 ;1
                              32                (232 ; 1)c
                  INT        231 ; 1        (232 ; 1)c ; 1]=2
                FLOAT         none                   c
Table 4.6: ReadPixels index masks and component conversion formulas. c
represents a component value to be converted.

client's native byte ordering for the indicated type) immediately prior to be-
ing placed in client memory. If PACK SWAP BYTES is FALSE, then no swapping
occurs. If type is BITMAP, then each byte of client memory is eight bits, each
of which is a single element. The single-bit elements within each byte are or-
dered from most signi cant to least signi cant if the value of PACK LSB FIRST
is FALSE otherwise, the ordering is from least signi cant to most signi cant.
The BITMAP type is valid only if format is either COLOR INDEX or STENCIL INDEX
(otherwise, results are unde ned).
4.3.3 Copying Pixels
CopyPixels transfers a rectangle of pixel values from one region of the
framebu er to another. Pixel copying is diagrammed in Figure 4.3.
      void CopyPixels( int x, int y, sizei width, sizei height,
          enum type )

type is a symbolic constant that must be one of COLOR, STENCIL, or DEPTH,
indicating that the values to be transferred are colors, stencil values, or depth
values, respectively. The rst four arguments have the same interpretation
as the corresponding arguments to ReadPixels.
    Values are obtained from the framebu er, converted (if appropriate),
subjected to arithmetic operations, and looked up in tables just as if Read-
Pixels were called with the corresponding arguments. If the type is STENCIL
or DEPTH, then it is as if the format for ReadPixels were STENCIL INDEX




                        Version 1.0 - 1 July 1994
4.3. DRAWING, READING, AND COPYING PIXELS                                              113



                                                              mask
                                                               to
                                shift      index−>index
         Index                                              [0.0,2n−1]
        (stencil,              offset         lookup
        colorindex)                                                      Pixels to
   Pixels from                                                           Framebuffer
   Framebuffer                                               clamp
                      map                                      to
         RGBA                  scale      RGBA−>RGBA
                       to                                     [0,1]
          Z                    bias          lookup
                      [0,1]




   Figure 4.3. Operation of CopyPixels. All parameters a ecting pixel copying
   are set with PixelTransfer or PixelMap.


or DEPTH COMPONENT, respectively. If the type is COLOR, then if the GL is in
RGBA mode, it is as if the format were RGBA, while if the GL is in color
index mode, it is as if the format were COLOR INDEX.
    The groups of elements so obtained are then written to the framebu er
just as if DrawPixels had been given width and height, beginning with
  nal conversion of elements. The e ective format is the same as that already
described.
4.3.4 Pixel draw/read state
The state required for pixel operations consists of the parameters that are
set with PixelStore, PixelTransfer, and PixelMap. This state has been
summarized in Tables 3.1, 3.2, and 3.3. The current setting of ReadBu er,
a twelve-valued integer, is also required, along with the current raster posi-
tion (section 2.11). State set with PixelStore is GL client state.




                                Version 1.0 - 1 July 1994
Chapter 5
Special Functions
This chapter describes additional GL functionality that does not t easily
into any of the preceding chapters. This functionality consists of evalua-
tors (used to model curves and surfaces), selection (used to locate rendered
primitives on the screen), feedback (which returns GL results before raster-
ization), display lists (used to designate a group of GL commands for later
execution by the GL), ushing and nishing (used to synchronize the GL
command stream), and hints.

5.1 Evaluators
Evaluators provide a means to use a polynomial or rational polynomial map-
ping to produce vertex, normal, and texture coordinates, and colors. The
values so produced are sent on to further stages of the GL as if they had
been provided directly by the client. Transformations, lighting, primitive
assembly, rasterization, and per-pixel operations are not a ected by the use
of evaluators.
    Consider the Rk -valued polynomial p(u) de ned by
                                     X
                                     n
                            p(u) =         Bin (u)Ri                   (5:1)
                                     i=0
with Ri 2 Rk and                      !
                       Bin (u) = ni ui(1 ; u)n;i
the ith Bernstein polynomial of degree n (recall that 00
                                                                 ;
                                                            1 and n0     1).
Each Ri is a control point. The relevant command is
                                      114




                       Version 1.0 - 1 July 1994
5.1. EVALUATORS                                                             115


  target                     k Values
  MAP1   VERTEX 3            3 x, y , z vertex coordinates
  MAP1   VERTEX 4            4 x, y , z , w vertex coordinates
  MAP1   INDEX               1   color index
  MAP1   COLOR 4             4   R, G, B, A
  MAP1   NORMAL              3   x, y, z normal coordinates
  MAP1   TEXTURE COORD   1   1   s texture coordinate
  MAP1   TEXTURE COORD   2   2   s, t texture coordinates
  MAP1   TEXTURE COORD   3   3   s, t, r texture coordinates
  MAP1   TEXTURE COORD   4   4   s, t, r, q texture coordinates

Table 5.1: Values speci ed by the target to Map1. Values are given in the
order in which they are taken.

      void  Map1ffdg( enum type, T u1, T u2, int stride, int order,
         T points   )
type is a symbolic constant indicating the range of the de ned polynomial.
Its possible values, along with the evaluations that each indicates, are given
in Table 5.1. order is equal to n +1 The error INVALID VALUE results if order
is less than one or greater than MAX EVAL ORDER. points is a pointer to a set of
n + 1 blocks of storage. Each block begins with k single-precision oating-
point or double-precision oating-point values, respectively. The rest of the
block may be lled with arbitrary data. Table 5.1 indicates how k depends
on type and what the k values represent in each case.
     stride is the number of single- or double-precision values (as appropriate)
in each block of storage. The error INVALID VALUE results if stride is less than
k. The order of the polynomial, order, is also the number of blocks of storage
containing control points.
     u1 and u2 give two oating-point values that de ne the endpoints of the
pre-image of the map. When a value u0 is presented for evaluation, the
formula used is
                              p0(u0) = p( u ; u1 ):
                                            0

                                       u2 ; u1
The error INVALID VALUE results if u1 = u2 .
   Map2 is analogous to Map1, except that it describes bivariate polyno-




                                 Version 1.0 - 1 July 1994
116                                   CHAPTER 5. SPECIAL FUNCTIONS

mials of the form
                                 X
                                 n X
                                   m
                      p(u v) =              Bin (u)Bjm (v )Rij :
                                 i=0 j =0
The form of the Map2 command is
      void     Map2ffdg(     enum target, T u1 , T u2, int ustride,
         int   uorder, T v1, T v2 , int vstride, int vorder, T points )
target is a range type selected from the same group as is used for Map1,
except that the string MAP1 is replaced with MAP2. points is a pointer to
(n + 1)(m + 1) blocks of storage (uorder = n + 1 and vorder = m + 1
the error INVALID VALUE results if either uorderorvorder is less than one or
greater than MAX EVAL ORDER). The values comprising Rij are located
                            (ustride)i + (vstride)j
values (either single- or double-precision oating-point, as appropriate) past
the rst value pointed to by points. u1 , u2 , v1 , and v2 de ne the pre-image
rectangle of the map a domain point (u0 v 0) is evaluated as

                       p0(u0 v0) = p( uu ;; uu1 vv ;; vv1 ):
                                        0         0

                                        2     1   2     1

    The evaluation of a de ned map is enabled or disabled with Enable and
Disable using the constant corresponding to the map as described above.
The error INVALID VALUE results if either ustride or vstride is less than k, or
if u1 is equal to u2 , or if v1 is equal to v2 .
    Figure 5.1 describes map evaluation schematically an evaluation of en-
abled maps is e ected in one of two ways. The rst way is to use
         EvalCoordf12gffdg( T arg )
      void
         EvalCoordf12gffdgv( T arg )
      void

EvalCoord1 causes evaluation of the enabled 1-dimensional maps. The ar-
gument is the value (or a pointer to the value) that is the domain coordinate,
u0. EvalCoord2 causes evaluation of the enabled 2-dimensional maps. The
two values specify the two domain coordinates, u0 and v 0, in that order.
  When one of the EvalCoord commands is issued, all currently enabled
maps of the indicated dimension are evaluated. Then, for each enabled map,




                        Version 1.0 - 1 July 1994
5.1. EVALUATORS                                                                                  117



           Integers                   Reals
                                                                           Vertices
                      k                   [u1,u2]                          Normals
                                                                   ΣBiRi
      EvalMesh                                             [0,1]
                                                    Ax+b
                                                                           Texture Coordinates
      EvalPoint       l                   [v1,v2]
                                                           [0,1]
                                                                           Colors


                          MapGrid                            Map
                                    EvalCoord


   Figure 5.1. Map Evaluation.


it is as if a corresponding GL command were issued with the resulting co-
ordinates, with one important di erence. The di erence is that when an
evaluation is performed, the GL uses evaluated values instead of current
values for those evaluations that are enabled (otherwise, the current val-
ues are used). The order of the e ective commands is immaterial, except
that Vertex (for vertex coordinate evaluation) must be issued last. Use of
evaluators has no e ect on the current color, normal, or texture coordinates.
     No command is e ectively issued if the corresponding map (of the indi-
cated dimension) is not enabled. If more than one evaluation is enabled for a
particular dimension (e.g. MAP1 TEXTURE COORD 1 and MAP1 TEXTURE COORD 2),
then only the result of the evaluation of the map with the highest number
of coordinates is used.
     Finally, if either MAP2 VERTEX 3 or MAP2 VERTEX 4 is enabled, then the nor-
mal to the surface is computed analytically. If automatic normal generation
is enabled, then this computed normal is used as the normal associated with
a generated vertex. Automatic normal generation is controlled with Enable
and Disable with symbolic the constant AUTO NORMAL. If automatic normal
generation is disabled, then a corresponding normal map, if enabled, is used
to produce a normal. If neither automatic normal generation nor a normal
map are enabled, then no normal is sent with a vertex resulting from an
evaluation (the e ect is that the current normal is used).
     For MAP VERTEX 3, let q = p. For MAP VERTEX 4, let q = (x=w y=w z=w),
where (x y z w) = p. Then let
                            m = @@uq @@vq :
Then the generated normal, n, is given by n = m=kmk.




                                      Version 1.0 - 1 July 1994
118                                   CHAPTER 5. SPECIAL FUNCTIONS

     The second way to carry out evaluations is to use a set of commands
that provide for e cient speci cation of a series of evenly spaced values to
be mapped. This method proceeds in two steps. The rst step is to de ne
a grid in the domain. This is done using
      void MapGrid1ffdg( int n, T u01 , T u02 )

for a 1-dimensional map or
      void MapGrid2ffdg( int nu , T u01 , T u02 , int nv , T v10 ,
           T v20 )

for a 2-dimensional map. In the case of MapGrid1 u01 and u02 describe an
interval, while n describes the number of partitions of the interval. The
error INVALID VALUE results if n 0. For MapGrid2, (u01 v10 ) speci es one
two-dimensional point and (u02 v20 ) speci es another. nu gives the number of
partitions between u01 and u02, and nv gives the number of partitions between
v10 and v20 . If either nu 0 or nv 0, then the error INVALID VALUE occurs.
     Once a grid is de ned, an evaluation on a rectangular subset of that grid
may be carried out by calling
      void EvalMesh1( enum mode, int p1 , int p2 )

mode is either POINT or LINE. The e ect is the same as performing the fol-
lowing code fragment, with u0 = (u02 ; u01 )=n:
             Begin(type)
                 for i = p1 to p2 step 1:0
                EvalCoord1(i      *    u0   +   u01)
        End()
where EvalCoord1f or EvalCoord1d is substituted for EvalCoord1 as
appropriate. If mode is POINT, then type is POINTS if mode is LINE, then type
is LINE STRIP. The one requirement is that if either i = 0 or i = n, then the
value computed from i u0 + u01 is precisely u01 or u02 , respectively.
     The corresponding commands for two-dimensional maps are
       void EvalMesh2( enum mode, int p1, int p2 , int q1 ,
          int q2 )

mode must be FILL, LINE, or POINT. When mode is FILL, then these commands
are equivalent to the following, with u0 = (u02 ; u01 )=n and v 0 = (v20 ;
v10 )=m:




                       Version 1.0 - 1 July 1994
5.1. EVALUATORS                                                        119

          for i = q1 to q2 ; 1 step 1:0
             Begin(QUAD STRIP)
                 for j = p1 to p2 step 1:0
                    EvalCoord2(j * u0 + u01 , i * v0 + v10 )
                    EvalCoord2(j * u0 + u01 , (i + 1) * v0 + v10 )
             End()
If mode is LINE, then a call to EvalMesh2 is equivalent to
          for i = q1 to q2 step 1:0
             Begin(LINE STRIP)
             for j = p1 to p2 step 1:0
                 EvalCoord2(j * u0 + u01 , i * v0 + v10 )
             End()
          for i = p1 to p2 step 1:0
             Begin(LINE STRIP)
             for j = q1 to q2 step 1:0
                 EvalCoord2(i * u0 + u01 , j * v0 + v10 )
             End()
If mode is POINT, then a call to EvalMesh2 is equivalent to
          Begin(POINTS)
             for i = q1 to q2 step 1:0
                 for j = p1 to p2 step 1:0
                    EvalCoord2(j * u0 + u01 , i * v0 + v10 )
          End()
Again, in all three cases, there is the requirement that 0 u0 + u01 = u01 ,
n u0 + u01 = u02 , 0 v0 + v10 = v10 , and m v0 + v10 = v20 .
    An evaluation of a single point on the grid may also be carried out:
      void EvalPoint1( int p )

Calling it is equivalent to the command
           EvalCoord1(p * u0 + u01)
with u0 and u01 de ned as above.
      void EvalPoint2( int p, int q )

is equivalent to the command




                              Version 1.0 - 1 July 1994
120                                  CHAPTER 5. SPECIAL FUNCTIONS

          EvalCoord2(p     *    u0   +   u01   ,   q   *   v0   +   v10 )

    The state required for evaluators potentially consists of 9 1-dimensional
map speci cations and 9 2-dimensional map speci cations, as well as cor-
responding ags for each speci cation indicating which are enabled. Each
map speci cation consists of one or two orders, an appropriately sized array
of control points, and a set of two values (for a 1-dimensional map) or four
values (for a 2-dimensional map) to describe the domain. The maximum
possible order, for either u or v , is implementation dependent (one maxi-
mum applies to both u and v ), but must be at least 8. Each control point
consists of between one and four oating-point values (depending on the
type of the map). Initially, all maps have order 1 (making them constant
maps). All vertex coordinate maps produce the coordinates (0 0 0 1) (or
the appropriate subset) all normal coordinate maps produce (0 0 1) RGBA
maps produce (1,1,1,1) color index maps produce 1.0. In the initial state,
all maps are disabled. A ag indicates whether or not automatic normal
generation is enabled for 2-dimensional maps. In the initial state, auto-
matic normal generation is disabled. Also required are two oating-point
values and an integer number of grid divisions for the 1-dimensional grid
speci cation and four oating-point values and two integer grid divisions for
the 2-dimensional grid speci cation. In the initial state, the bounds of the
domain interval for 1-D is 0 and 1:0, respectively for 2-D, they are (0 0)
and (1:0 1:0), respectively. The number of grid divisions is 1 for 1-D and
1 in both directions for 2-D. If any evaluation command is issued when no
vertex map is enabled, nothing happens.

5.2 Selection
Selection is used by a programmer to determine which primitives are drawn
into some region of a window. The region is de ned by the current model-
view and perspective matrices.
    Selection works by returning an array of integer-valued names. This
array represents the current contents of the name stack. This stack is con-
trolled with the commands
      void   InitNames( void )
      void   PopName( void )
      void   PushName( uint name )




                       Version 1.0 - 1 July 1994
5.2. SELECTION                                                             121

      void   LoadName(      uint  name )
InitNames empties (clears) the name stack. PopName pops one name
o the top of the name stack. PushName causes name to be pushed
onto the name stack. LoadName replaces the value on the top of the
stack with name. Loading a name onto an empty stack generates the er-
ror INVALID OPERATION. Popping a name o of an empty stack generates
STACK UNDERFLOW pushing a name onto a full stack generates STACK OVERFLOW.
The maximum allowable depth of the name stack is implementation depen-
dent but must be at least 64.
    In selection mode, no fragments are rendered into the framebu er. The
GL is placed in selection mode with
       int RenderMode( enum mode )

mode is a symbolic constant: one of RENDER, SELECT, or FEEDBACK. RENDER
is the default, corresponding to rendering as described until now. SELECT
speci es selection mode, and FEEDBACK speci es feedback mode (described
below). Use of any of the name stack manipulation commands while the GL
is not in selection mode has no e ect.
    Selection is controlled using
       void SelectBu er( sizei n, uint *bu er )

bu er is a pointer to an array of unsigned integers (called the selection
array) to be potentially lled with names, and n is an integer indicating the
maximum number of values that can be stored in that array. Placing the GL
in selection mode before SelectBu er has been called results in an error of
INVALID OPERATION as does calling SelectBu er while in selection mode.
    In selection mode, if a point, line, polygon, or the valid coordinates pro-
duced by a RasterPos command intersects the clip volume (section 2.10)
then this primitive (or RasterPos command) causes a selection hit. In the
case of polygons, no hit occurs if the polygon would have been culled, but
selection is based on the polygon itself, regardless of the setting of Poly-
gonMode. When in selection mode, whenever a name stack manipulation
command is executed or RenderMode is called and there has been a hit
since the last time the stack was manipulated or RenderMode was called,
then a hit record is written into the selection array.
    A hit record consists of the following items in order: a non-negative
integer giving the number of elements on the name stack at the time of the
hit, a minimum depth value, a maximum depth value, and the name stack




                                Version 1.0 - 1 July 1994
122                                 CHAPTER 5. SPECIAL FUNCTIONS

with the bottommost element rst. The minimum and maximum depth
values are the minimum and maximum taken over all the window coordinate
z values of each (post-clipping) vertex of each primitive that intersects the
clipping volume since the last hit record was written. The minimum and
maximum (each of which lies in the range 0 1]) are each multiplied by 232 ; 1
and rounded to the nearest unsigned integer to obtain the values that are
placed in the hit record.
    Hit records are placed in the selection array by maintaining a pointer
into that array. When selection mode is entered, the pointer is initialized to
the beginning of the array. Each time a hit record is copied, the pointer is
updated to point at the array element after the one into which the topmost
element of the name stack was stored. If copying the hit record into the
selection array would cause the total number of values to exceed n, then as
much of the record as ts in the array is written and an over ow ag is set.
    Selection mode is exited by calling RenderMode with an argument
value other than SELECT. Whenever RenderMode is called in selection
mode, it returns the number of hit records copied into the selection array
and resets the SelectBu er pointer to its last speci ed value. Values are
not guaranteed to be written into the selection array until RenderMode
is called. If the selection array over ow ag was set, then RenderMode
returns ;1 and clears the over ow ag. The name stack is cleared and the
stack pointer reset whenever RenderMode is called.
    The state required for selection consists of the address of the selection
array and its maximum size, the name stack and its associated pointer, a
minimum and maximum depth value, and several ags. One ag indicates
the current RenderMode value. In the initial state, the GL is in the RENDER
mode. Another ag is used to indicate whether or not a hit has occurred
since the last name stack manipulation. This ag is reset upon entering
selection mode and whenever a name stack manipulation takes place. One
  nal ag is required to indicate whether the maximum number of copied
names would have been exceeded. This ag is reset upon entering selection
mode. This ag, the address of the selection array, and its maximum size
are GL client state.

5.3 Feedback
Feedback, like selection, is a GL mode. The mode is selected by calling
RenderMode with FEEDBACK. When the GL is in feedback mode, no frag-




                       Version 1.0 - 1 July 1994
5.3. FEEDBACK                                                             123

ments are written to the framebu er. Instead, information about primitives
that would have been rasterized is fed back to the application using the GL.
   Feedback is controlled using
     void   FeedbackBu er(      sizei n, enum     type, float *bu er )
bu er is a pointer to an array of oating-point values into which feedback in-
formation will be placed, and n is a number indicating the maximum number
of values that can be written to that array. type is a symbolic constant de-
scribing the information to be fed back for each vertex (see Figure 5.2). The
error INVALID OPERATION results if the GL is placed in feedback mode before
a call to FeedbackBu er has been made, or if a call to FeedbackBu er
is made while in feedback mode.
    While in feedback mode, each primitive that would be rasterized (or
bitmap or call to DrawPixels or CopyPixels, if the raster position is
valid) generates a block of values that get copied into the feedback array.
If doing so would cause the number of entries to exceed the maximum, the
block is partially written so as to ll the array (if there is any room left at
all). The rst block of values generated after the GL enters feedback mode
is placed at the beginning of the feedback array, with subsequent blocks
following. Each block begins with a code indicating the primitive type, fol-
lowed by values that describe the primitive's vertices and associated data.
Entries are also written for bitmaps and pixel rectangles. Feedback occurs
after polygon culling (section 3.5.1) and PolygonMode interpretation of
polygons (section 3.5.4) has taken place. It may also occur after polygons
with more than three edges are broken up into triangles (if the GL imple-
mentation renders polygons by performing this decomposition). x, y , and z
coordinates returned by feedback are window coordinates if w is returned,
it is in clip coordinates. In the case of bitmaps and pixel rectangles, the
coordinates returned are those of the current raster position. The texture
coordinates and colors returned are those resulting from the clipping oper-
ations as described in (section 2.12.8).
    The ordering rules for GL command interpretation also apply in feedback
mode. Each command must be fully interpreted and its e ects on both GL
state and the values to be written to the feedback bu er completed before
a subsequent command may be executed.
    The GL is taken out of feedback mode by calling RenderMode with an
argument value other than FEEDBACK. When called while in feedback mode,
RenderMode returns the number of values placed in the feedback array




                                Version 1.0 - 1 July 1994
124                                 CHAPTER 5. SPECIAL FUNCTIONS

              Type         coordinates    color texture total values
               2D          x, y           {     {       2
               3D          x, y , z       {     {       3
            3D COLOR       x, y , z       k     {       3+k
        3D COLOR TEXTURE   x, y , z       k     4       7+k
        4D COLOR TEXTURE   x, y , z , w   k     4       8+k

Table 5.2: Correspondence of feedback type to number of values per vertex.
k is 1 in color index mode and 4 in RGBA mode.
and resets the feedback array pointer to be bu er. The return value never
exceeds the maximum number of values passed to FeedbackBu er.
    If writing a value to the feedback bu er would cause more values to be
written than the speci ed maximum number of values, then the value is not
written and an over ow ag is set. In this case, RenderMode returns ;1
when it is called, after which the over ow ag is reset. While in feedback
mode, values are not guaranteed to be written into the feedback bu er before
RenderMode is called.
   Figure 5.2 gives a grammar for the array produced by feedback. Each
primitive is indicated with a unique identifying value followed by some num-
ber of vertices. A vertex is fed back as some number of oating-point values
determined by the feedback type. Table 5.2 gives the correspondence be-
tween feedback bu er and the number of values returned for each vertex.
      The command
       void   PassThrough(    float   token )
may be used as a marker in feedback mode. token is returned as if it were a
primitive it is indicated with its own unique identifying value. The ordering
of any PassThrough commands with respect to primitive speci cation is
maintained by feedback. PassThrough may not occur between Begin and
End. It has no e ect when the GL is not in feedback mode.
    The state required for feedback is the pointer to the feedback array, the
maximum number of values that may be placed there, and the feedback type.
An over ow ag is required to indicate whether the maximum allowable
number of feedback values has been written initially this ag is cleared.
These state variables are GL client state. Feedback also relies on the same




                       Version 1.0 - 1 July 1994
5.4. DISPLAY LISTS                                                         125

mode ag as selection to indicate whether the GL is in feedback, selection,
or normal rendering mode.

5.4 Display Lists
A display list is simply a group of GL commands and arguments that has
been stored for subsequent execution. The GL may be instructed to process
a particular display list (possibly repeatedly) by providing a number that
uniquely speci es it. Doing so causes the commands within the list to be
executed just as if they were given normally. The only exception pertains
to commands that rely upon client state. When such a command is accu-
mulated into the display list (that is, when issued, not when executed), the
client state in e ect at that time applies to the command. Only server state
is a ected when the command is executed. As always, pointers which are
passed as arguments to commands are dereferenced when the command is
issued.
    A display list is begun by calling
      void   NewList(    uint   n, enum mode )
n is a positive integer to which the display list that follows is assigned, and
mode is a symbolic constant that controls the behavior of the GL during
display list creation. If mode is COMPILE, then commands are not executed
as they are placed in the display list. If mode is COMPILE AND EXECUTE. then
commands are executed as they are encountered, then placed in the display
list. If n = 0, then the error INVALID VALUE is generated.
     After calling NewList all subsequent GL commands are placed in the
display list (in the order the commands are issued) until a call to
      void   EndList(    void   )
occurs, after which the GL returns to its normal command execution state.
It is only when EndList occurs that the speci ed display list is actually asso-
ciated with the index indicated with NewList. The error INVALID OPERATION
is generated if EndList is called without a previous matching NewList, or
if NewList is called a second time before calling EndList.
     Once de ned, a display list is executed by calling
      void   CallList(   uint   n)




                                 Version 1.0 - 1 July 1994
126                                    CHAPTER 5. SPECIAL FUNCTIONS



feedback-list:
      feedback-item feedback-list              pixel-rectangle:
      feedback-item                                     DRAW PIXEL TOKEN    vertex
                                                        COPY PIXEL TOKEN    vertex
feedback-item:                                 passthrough:
      point                                             PASS THROUGH TOKEN    f
      line-segment
      polygon                                  vertex:
      bitmap                                   2D:
      pixel-rectangle                                   ff
      passthrough                              3D:
                                                        fff
point:                                         3D COLOR:
         POINT TOKEN   vertex                           f f f color
line-segment:                                  3D COLOR TEXTURE:
         LINE TOKEN vertex vertex                       f f f color tex
         LINE RESET TOKEN vertex vertex        4D COLOR TEXTURE:
polygon:                                                f f f f color tex
      POLYGON TOKEN n polygon-spec
polygon-spec:                                  color:
      polygon-spec vertex                               ffff
      vertex vertex vertex                              f
bitmap:
      BITMAP TOKEN vertex                      tex:
                                                        ffff

Figure 5.2: Feedback syntax. f is a oating-point number. n is a oating-
point integer giving the number of vertices in a polygon. The symbols
ending with TOKEN are symbolic oating-point constants. The labels under
the \vertex" rule show the di erent data returned for vertices depending
on the feedback type. LINE TOKEN and LINE RESET TOKEN are identical except
that the latter is returned only when the line stipple is reset for that line
segment.




                          Version 1.0 - 1 July 1994
5.4. DISPLAY LISTS                                                          127

n gives the index of the display list to be called. This causes the commands
saved in the display list to be executed, in order, just as if they were issued
without using a display list. If n = 0, then the error INVALID VALUE is
generated.
    The command
      void   CallLists(   sizei   n, enum type, void *lists )
provides an e cient means for executing a number of display lists. n is
an integer indicating the number of display lists to be called, and lists is
a pointer that points to an array of o sets. Each o set is constructed as
determined by lists as follows. First, type may be one of the constants BYTE,
UNSIGNED BYTE, SHORT, UNSIGNED SHORT, INT, UNSIGNED INT, or FLOAT indicating
that the array pointed to by lists is an array of bytes, unsigned bytes, shorts,
unsigned shorts, integers, unsigned integers, or oats, respectively. In this
case each o set is found by simply converting each array element to an
integer ( oating point values are truncated). Further, type may be one of
2 BYTES, 3 BYTES, or 4 BYTES, indicating that the array contains sequences of
2, 3, or 4 unsigned bytes, in which case each integer o set is constructed
according to the following algorithm:
offset 0
for i = 1 to b
     offset offset shifted left 8 bits
     offset offset + byte
     advance to next byte in the array
b is 2, 3, or 4, as indicated by type. If n = 0, CallLists does nothing.
     Each of the n constructed o sets is taken in order and added to a display
list base to obtain a display list number. For each number, the indicated
display list is executed. The base is set by calling
       void ListBase( uint base )

to specify the o set.
     Indicating a display list index that does not correspond to any display
list has no e ect. CallList or CallLists may appear inside a display list. (If
the mode supplied to NewList is COMPILE AND EXECUTE, then the appropriate
lists are executed, but the CallList or CallLists, rather than those lists'
constituent commands, is placed in the list under construction.) To avoid
the possibility of in nite recursion resulting from display lists calling one




                                  Version 1.0 - 1 July 1994
128                                        CHAPTER 5. SPECIAL FUNCTIONS

another, an implementation dependent limit is placed on the nesting level
of display lists during display list execution. This limit must be at least 64.
    Two commands are provided to manage display list indices.
      uint   GenLists(     sizei   s)
returns an integer n such that the indices n : : : n + s ; 1 are previously
unused (i.e. there are s previously unused display list indices starting at n).
GenLists also has the e ect of creating an empty display list for each of
the indices n : : : n + s ; 1, so that these indices all become used. GenLists
returns 0 if there is no group of s contiguous previously unused display list
indices, or if s = 0.
      boolean   IsList(    uint   list )
returns TRUE if list is the index of some display list.
    A contiguous group of display lists may be deleted by calling
      void   DeleteLists(      uint   list, sizei range )
where list is the index of the rst display list to be deleted and range is
the number of display lists to be deleted. All information about the display
lists is lost, and the indices become unused. Indices to which no display list
corresponds are simply ignored. If range = 0, nothing happens.
     Certain commands, when made within a display list, are not compiled
into the display list but are executed immediately. These are: IsList,
GenLists, DeleteLists, FeedbackBu er, SelectBu er, RenderMode,
ReadPixels, PixelStore, Flush, Finish, as well as IsEnabled and all of
the Get commands (see Chapter 6).
     Display lists require one bit of state to indicate whether a GL command
should be executed immediately or placed in a display list. In the initial
state, commands are executed immediately. If the bit indicates display
list creation, an index is required to indicate the current display list being
de ned. Another bit indicates, during display list creation, whether or not
commands should be executed as they are compiled into the display list.
One integer is required for the current ListBase setting its initial value
is zero. Finally, state must be maintained to indicate which integers are
currently in use as display list indices. In the initial state, no indices are in
use.




                          Version 1.0 - 1 July 1994
5.5. FLUSH AND FINISH                                                    129

5.5 Flush and Finish
The command
     void   Flush(   void   )
indicates that all commands that have previously been sent to the GL must
complete in nite time.
    The command
      void Finish( void )

forces all previous GL commands to complete. Finish does not return until
all e ects from previously issued commands on GL client and server state
and the framebu er are fully realized.

5.6 Hints
Certain aspects of GL behavior, when there is room for variation, may be
controlled with hints. A hint is speci ed using
      void Hint( enum target, enum hint )

target is a symbolic constant indicating the behavior to be controlled, and
hint is a symbolic constant indicating what type of behavior is desired.
target may be one of PERSPECTIVE CORRECTION HINT, indicating the desired
quality of parameter interpolation POINT SMOOTH HINT, indicating the desired
sampling quality of points LINE SMOOTH HINT, indicating the desired sampling
quality of lines POLYGON SMOOTH HINT, indicating the desired sampling quality
of polygons and FOG HINT, indicating whether fog calculations are done per
pixel or per vertex. hint must be one of FASTEST, indicating that the most
e cient option should be chosen NICEST, indicating that the highest quality
option should be chosen and DONT CARE, indicating no preference in the
matter.
    The interpretation of hints is implementation dependent. An implemen-
tation may ignore them entirely.




                               Version 1.0 - 1 July 1994
Chapter 6
State and State Requests
The values of most GL state variables can be obtained using a set of Get
commands. There are four commands for obtaining simple state variables:
     void   GetBooleanv( enum value, boolean *data )
     void   GetIntegerv( enum value, int *data )
     void   GetFloatv( enum value, float *data )
     void   GetDoublev( enum value, double *data )
The commands obtain boolean, integer, oating-point, or double-precision
state variables. value is a symbolic constant indicating the state variable to
return, data is a pointer to an array of the indicated type in which to place
the returned data. In addition
     boolean    IsEnabled(    enum   value )
can be used to determine if value is currently enabled (as with Enable) or
disabled.
    If a Get command is issued that returns value types di erent from the
type of the value being obtained, a type conversion is performed. If Get-
Booleanv is called, a oating-point or integer value converts to FALSE if
and only if it is zero (otherwise it converts to TRUE). If GetIntegerv (or
any of the Get commands below) is called, a boolean value is interpreted
as either 1 or 0, and a oating-point value is rounded to the nearest integer,
unless the value is a an RGBA color component, a DepthRange value, a
depth bu er clear value, or a normal coordinate. In these cases, the Get
command converts the oating-point value to an integer according the INT
entry of Table 4.6 a value not in ;1 1] converts to an unde ned value.
                                      130




                       Version 1.0 - 1 July 1994
                                                                         131

If GetFloatv is called, a boolean value is interpreted as either 1:0 or 0:0,
an integer is coerced to oating-point, and a double-precision oating-point
value is converted to single-precision. Analogous conversions are carried
out in the case of GetDoublev. If a value is so large in magnitude that
it cannot be represented with the requested type, then the nearest value
representable using the requested type is returned.
    Other commands exist to obtain state variables that are indexed by a
target. These are
       void GetClipPlane( enum plane, double eqn 4] )
       void GetLightfifgv( enum light, enum value, T data )
       void GetMaterialfifgv( enum face, enum value, T data )
       void GetTexEnvfifgv( enum env, enum value, T data )
       void GetTexGenfifgv( enum coord, enum value, T data )
       void GetTexParameterfifgv( enum target, enum value,
          T data )
       void GetTexLevelParameterfifgv( enum target, int lod,
          enum value, T data )
       void GetPixelMapfui us fgv( enum map, T data )
       void GetMapfifdgv( enum map, enum value, T data )

GetClipPlane always returns four double-precision values in eqn these
are the coe cients of the plane equation of plane in eye coordinates (these
coordinates are those that were computed when the plane was speci ed).
    GetLight places information about value (a symbolic constant) for light
(also a symbolic constant) in data. POSITION or SPOT DIRECTION returns val-
ues in eye coordinates (again, these are the coordinates that were computed
when the position or direction was speci ed).
    GetMaterial, GetTexGen, GetTexEnv, and GetTexParameter
are similar to GetLight, placing information about value for the target indi-
cated by their rst argument into data. The face argument to GetMaterial
must be either FRONT or BACK, indicating the front or back material, respec-
tively. The env argument to GetTexEnv must currently be TEXTURE ENV.
The coord argument to GetTexGen must be one of S, T, R, or Q. For Get-
TexGen, EYE LINEAR coe cients are returned in the eye coordinates that
were computed when the plane was speci ed OBJECT LINEAR coe cients are
returned in object coordinates.
    For GetTexParameter and GetTexLevelParameter, target must
currently be either TEXTURE 1D or TEXTURE 2D, indicating the target from
which information is to be obtained. value is a symbolic value indicating




                               Version 1.0 - 1 July 1994
132                      CHAPTER 6. STATE AND STATE REQUESTS

which texture parameter is to be obtained. The lod argument to Get-
TexLevelParameter determines which level-of-detail's state is returned.
If the lod argument is less than zero or if it is larger than the maximum
allowable level-of-detail then the error INVALID VALUE occurs.
    For GetPixelMap, the map must be a map name from Table 3.3. For
GetMap, map must be one of the map types described in section 5.1, and
value must be one of ORDER, COEFF, or DOMAIN.
    GetTexImage is used to obtain texture images.
      void     GetTexImage(         enum   tex,    int   lod,   enum   format,
         enum   type, void *img )
It is somewhat di erent from the other get commands tex is a symbolic
value indicating which texture is to be obtained. TEXTURE 1D indicates a one-
dimensional texture, while TEXTURE 2D indicates a two-dimensional texture.
lod is a level-of-detail number, format is a pixel format from Table 3.5,
type is a pixel type from Table 3.4, and img is a pointer to a block of
memory. GetTexImage obtains component groups from a texture image
with the indicated level-of-detail (the number of components in a group
is the number of components of the texture the components are assigned
among R, G, B, and A according to Table 3.6) starting with the rst group
in the rst row, and continuing by obtaining groups in order from each
row and proceeding from the rst row to the last. These groups are then
packed and placed in client memory as described in section 4.3.2 under
ReadPixels. The row length and number of rows is determined by the
size of the texture image (including any borders). Calling GetTexImage
with lod less than zero or larger than the maximum allowable causes the
error INVALID VALUE. Calling GetTexImage with format of COLOR INDEX,
STENCIL INDEX, or DEPTH COMPONENT causes the error INVALID ENUM.
    The command
      void    GetPolygonStipple(      void   *pattern )
obtains the polygon stipple. The pattern is packed into memory according
to the procedure given in section 4.3.2 for ReadPixels it is as if the height
and width passed to that command were both equal to 32, the type were
BITMAP, and the format were COLOR INDEX.
    Finally,
      ubyte   *GetString(    enum   name )




                       Version 1.0 - 1 July 1994
                                                                           133

returns a pointer to a static string describing some aspect of the current
GL connection. The possible values for name are VENDOR, RENDERER, VERSION,
and EXTENSIONS. The format of the string pointed to by the value returned
by GetString is implementation dependent.
     The tables on the following pages indicate which state variables are ob-
tained with what commands. State variables that can be obtained using any
of GetBooleanv, GetIntegerv, GetFloatv, or GetDoublev are listed
with just one of these commands { the one that is most appropriate given
the type of the data to be returned. These state variables cannot be ob-
tained using IsEnabled. However, state variables for which IsEnabled is
listed as the query command can also be obtained using GetBooleanv,
GetIntegerv, GetFloatv, and GetDoublev. State variables for which
any other command is listed as the query command can be obtained only
by using that command.
     Unless otherwise indicated, multi-valued state variables return their mul-
tiple values in the same order as they are given as arguments to the com-
mands that set them. For instance, the two DepthRange parameters are
returned in the order n followed by f. Similarly, points for evaluator maps
are returned in the order that they appeared when passed to Map1. Map2
returns Rij in the (uorder)i + j ]th block of values (see page 116 for i, j ,
uorder, and Rij ).
     Besides providing a means to obtain the values of state variables, the
GL also provides a means to save and restore groups of state variables. The
PushAttrib and PopAttrib commands are used for this purpose. The
command
       void PushAttrib( bitfield mask )

takes a bitwise OR of symbolic constants indicating which groups of state
variables to push onto an attribute stack. Each constant refers to a group of
state variables. The classi cation of each variable into a group is indicated
in the following tables of state variables. The command
       void PopAttrib( void )

resets the values of those state variables that were saved with the last
PushAttrib. Those not saved remain unchanged. It is an error to pop
an empty stack or push onto a full one. Table 6.1 shows the attribute
groups with their corresponding symbolic constant names.
     The depth of the attribute stack is implementation dependent but must
be at least 16. The state required is potentially 16 copies of each state




                                Version 1.0 - 1 July 1994
134        CHAPTER 6. STATE AND STATE REQUESTS




         Attribute              Constant
       accum-bu er         ACCUM BUFFER BIT
        color-bu er        COLOR BUFFER BIT
           current             CURRENT BIT
       depth-bu er         DEPTH BUFFER BIT
            enable              ENABLE BIT
              eval               EVAL BIT
               fog                FOG BIT
              hint               HINT BIT
           lighting           LIGHTING BIT
              line               LINE BIT
              list               LIST BIT
             pixel          PIXEL MODE BIT
             point               POINT BIT
          polygon              POLYGON BIT
      polygon-stipple    POLYGON STIPPLE BIT
            scissor            SCISSOR BIT
       stencil-bu er      STENCIL BUFFER BIT
           texture             TEXTURE BIT
         transform           TRANSFORM BIT
          viewport            VIEWPORT BIT
                -           ALL ATTRIB BITS


           Table 6.1: Attribute groups




          Version 1.0 - 1 July 1994
                                                                            135

variable, 16 masks indicating which groups of variables are stored in each
stack entry, and an attribute stack pointer. In the initial state, the attribute
stack is empty.
    In the tables that follow, a type is indicated for each variable. Table 6.2
explains these types. The type actually identi es all state associated with
the indicated description in certain cases only a portion of this state is
returned. This is the case with all matrices, where only the top entry on
the stack is returned with clip planes, where only the selected clip plane is
returned, with parameters describing lights, where only the value pertaining
to the selected light is returned with textures, where only the selected
texture or texture parameter is returned and with evaluator maps, where
only the selected map is returned. Finally, a \{" in the attribute column
indicates that the indicated value is not included in any attribute group
(and thus can not be pushed or popped with PushAttrib or PopAttrib).




                                Version 1.0 - 1 July 1994
136                  CHAPTER 6. STATE AND STATE REQUESTS




      Type code Explanation
          B     Boolean
          C     Color ( oating-point R, G, B, and A values)
         CI     Color index ( oating-point index value)
          T     Texture coordinates ( oating-point s, t, r, q
                values)
          N     Normal coordinates ( oating-point x, y , z
                values)
          V     Vertex, including associated data
          Z     Integer
         Z  +   Non-negative integer
       Zk , Zk k-valued integer (k indicates k is minimum)
          R     Floating-point number
         R+     Non-negative oating-point number
         R  k   k-tuple of oating-point numbers
          P     Position (x, y , z , w oating-point coordinates)
          D     Direction (x, y , z oating-point coordinates)
         M4     4 4 oating-point matrix
           I    Image
          A     Attribute stack entry, including mask
       n type n copies of type type (n indicates n is
                minimum)

                   Table 6.2: State variable types




                    Version 1.0 - 1 July 1994
                                                                                                             Get  Initial
                                                                                              Get value Type Cmnd Value        Description               Sec. Attribute
                                                                                                  {      Z11   {     0    When 6= 0, indicates           2.6.1    {
                                                                                                                          begin/end object
                                                                                                  {       V    {     {    Previous vertex in             2.6.1    {
                                                                                                                             Begin/End line
                                                                                                 {       B       {      {    Indicates if line-vertex    2.6.1    {
                                                                                                                             is the rst
                                                                                                 {       V       {      {    First vertex of a           2.6.1    {
                                                                                                                             Begin/End line loop
                                                                                                 {       Z+      {      {    Line stipple counter         3.4     {
                                                                                                 {      n V      {      {    Vertices inside of          2.6.1    {
                                                                                                                             Begin/End polygon
                                                                                                 {       Z+      {      {    Number of                   2.6.1    {
                                                                                                                             polygon-vertices
                                                                                                 {      2 V      {      {    Previous two vertices       2.6.1    {
                                                                                                                             in a Begin/End
                                                                                                                             triangle strip
                                                                                                 {       Z3      {      {    Number of vertices so       2.6.1    {




Version 1.0 - 1 July 1994
                                                                                                                             far in triangle strip: 0,
                                                                                                                             1, or more
                                                                                                 {       Z2      {      {    Triangle strip A/B          2.6.1    {
                                                                                                                             vertex pointer
                                                                                                 {      3 V      {      {    Vertices of the quad        2.6.1    {
                                                                                                                             under construction
                                                                                                 {       Z4      {      {    Number of vertices so       2.6.1    {
                                                                                                                             far in quad strip: 0, 1,




                            Table 6.3. GL Internal begin-end state variables (inaccessible)
                                                                                                                             2, or more
                                                                                                                                                                          137
                                                                                                                                                                                    138


                                                                                                                      Get       Initial
                                                                                      Get value             Type      Cmnd      Value         Description         Sec. Attribute
                                                                                                                   GetIntegerv,
                                                                                   CURRENT COLOR             C     GetFloatv    1,1,1,1 Current color             2.7 current
                                                                                                                   GetIntegerv,
                                                                                   CURRENT INDEX             CI    GetFloatv       1    Current color index       2.7 current
                                                                               CURRENT TEXTURE COORDS        T      GetFloatv 0,0,0,1 Current texture             2.7 current
                                                                                                                                        coordinates
                                                                                   CURRENT NORMAL            N      GetFloatv 0,0,1 Current normal                2.7     current
                                                                                          {                  C          {          -    Color associated with     2.6        {
                                                                                                                                        last vertex
                                                                                          {                 CI          {          -    Color index associated    2.6       {
                                                                                                                                        with last vertex
                                                                                          {                  T          {          -    Texture coordinates       2.6       {
                                                                                                                                        associated with last
                                                                                                                                        vertex
                                                                               CURRENT RASTER POSITION      R4      GetFloatv 0,0,0,1 Current raster position     2.11    current




Version 1.0 - 1 July 1994
                                                                               CURRENT RASTER DISTANCE      R+      GetFloatv      0    Current raster distance   2.11    current
                                                                                                                   GetIntegerv,
                                                                                CURRENT RASTER COLOR        C      GetFloatv    1,1,1,1 Color associated with     2.11    current
                                                                                                                                        raster position
                                                                                                                   GetIntegerv,
                                                                                CURRENT RASTER INDEX        CI     GetFloatv       1    Color index associated    2.11    current
                                                                                                                                        with raster position
                                                                            CURRENT RASTER TEXTURE COORDS    T      GetFloatv 0,0,0,1 Texture coordinates         2.11    current




                            Table 6.4. Current Values and Associated Data
                                                                                                                                        associated with raster
                                                                                                                                        position
                                                                            CURRENT RASTER POSITION VALID    B     GetBooleanv True Raster position valid         2.11    current
                                                                                                                                        bit
                                                                                      EDGE FLAG              B     GetBooleanv True Edge ag                       2.6.2   current
                                                                                                                                                                                    CHAPTER 6. STATE AND STATE REQUESTS
                                                                                                       Get           Initial
                                                                    Get value            Type          Cmnd          Value            Description         Sec.      Attribute
                                                                MODELVIEW MATRIX       32 M4         GetFloatv      Identity    Model-view matrix         2.9.2         {
                                                                                                                                stack
                                                                PROJECTION MATRIX      2    M4       GetFloatv      Identity    Projection matrix         2.9.2        {
                                                                                                                                stack
                                                                 TEXTURE MATRIX        2     M4      GetFloatv      Identity    Texture matrix stack      2.9.2         {
                                                                    VIEWPORT               4 Z      GetIntegerv     see 2.9.1   Viewport origin &         2.9.1     viewport
                                                                                                                                extent
                                                                   DEPTH RANGE         2 R+          GetFloatv        0,1       Depth range near &        2.9.1     viewport
                                                                                                                                far
                                                              MODELVIEW STACK DEPTH        Z+       GetIntegerv        1        Model-view matrix         2.9.2        {
                                                                                                                                stack pointer
                                                              PROJECTION STACK DEPTH       Z+       GetIntegerv        1        Projection matrix         2.9.2        {
                                                                                                                                stack pointer
                                                               TEXTURE STACK DEPTH         Z+       GetIntegerv        1        Texture matrix stack      2.9.2        {
                                                                                                                                pointer




Version 1.0 - 1 July 1994
                                                                   MATRIX MODE             Z3       GetIntegerv    MODELVIEW    Current matrix mode       2.9.2     transform




                            Table 6.5. Transformation state
                                                                    NORMALIZE              B         IsEnabled       False      Current normal            2.9.3 transform/enable
                                                                                                                                normalization on/o
                                                                   CLIP PLANEi         6     R4     GetClipPlane    0,0,0,0     User clipping plane       2.10     transform
                                                                                                                                coe cients
                                                                   CLIP PLANEi         6        B    IsEnabled       False      xth user clipping plane   2.10 transform/enable
                                                                                                                                enabled
                                                                                                                                                                                   139
                                                                                                                                   140




                                                                          Get       Initial
                                                   Get value    Type      Cmnd      Value         Description   Sec.   Attribute
                                                   FOG COLOR     C      GetFloatv 0,0,0,0 Fog color             3.9       fog
                                                   FOG INDEX     I      GetFloatv      0    Fog index           3.9       fog
                                                  FOG DENSITY    R      GetFloatv     1.0 Exponential fog       3.9       fog
                                                                                            density
                                                   FOG START    R       GetFloatv     0.0 Linear fog start       3.9      fog
                                                     FOG END    R       GetFloatv     1.0 Linear fog end         3.9      fog




Version 1.0 - 1 July 1994
                                                    FOG MODE    Z3     GetIntegerv EXP Fog mode                  3.9      fog




                            Table 6.6. Coloring
                                                       FOG      B       IsEnabled False True if fog enabled      3.9 fog/enable
                                                  SHADE MODEL   Z+     GetIntegerv SMOOTH ShadeModel setting    2.12.7 lighting
                                                                                                                                   CHAPTER 6. STATE AND STATE REQUESTS
                                                                            Get                Initial
                                   Get value               Type             Cmnd               Value                 Description         Sec.     Attribute
                                    LIGHTING                B            IsEnabled              False         True if lighting is       2.12.1 lighting/enable
                                                                                                              enabled
                                 COLOR MATERIAL                B         IsEnabled              False         True if color tracking    2.12.3 lighting/enable
                                                                                                              is enabled
                            COLOR MATERIAL PARAMETER           Z5       GetIntegerv     AMBIENT AND DIFFUSE   Material properties       2.12.3     lighting
                                                                                                              tracking current color
                              COLOR MATERIAL FACE              Z3       GetIntegerv       FRONT AND BACK      Face(s) a ected by        2.12.3     lighting
                                                                                                              color tracking
                                    AMBIENT                2       C    GetMaterialfv     (0.2,0.2,0.2,1.0)   Ambient material color    2.12.1     lighting
                                    DIFFUSE                2       C    GetMaterialfv     (0.8,0.8,0.8,1.0)   Di use material color     2.12.1     lighting
                                   SPECULAR                2       C    GetMaterialfv     (0.0,0.0,0.0,1.0)   Specular material color   2.12.1     lighting
                                   EMISSION                2       C    GetMaterialfv     (0.0,0.0,0.0,1.0)   Emissive mat. color       2.12.1     lighting
                                   SHININESS               2       R    GetMaterialfv            0.0          Specular exponent of      2.12.1     lighting
                                                                                                              material
                               LIGHT MODEL AMBIENT             C         GetFloatv        (0.2,0.2,0.2,1.0)   Ambient scene color       2.12.1     lighting
                            LIGHT MODEL LOCAL VIEWER           B        GetBooleanv             False         Viewer is local           2.12.1     lighting
                               LIGHT MODEL TWO SIDE            B        GetBooleanv             False         Use two-sided lighting    2.12.1     lighting
                                     AMBIENT           8            C    GetLightfv       (0.0,0.0,0.0,1.0)   Ambient intensity of      2.12.1     lighting
                                                                                                              light i
                                    DIFFUSE            8            C    GetLightfv            see 2.5        Di use intensity of       2.12.1     lighting
                                                                                                              light i
                                   SPECULAR            8            C    GetLightfv            see 2.5        Specular intensity of     2.12.1     lighting




Version 1.0 - 1 July 1994
                                                                                                              light i
                                    POSITION            8 P              GetLightfv       (0.0,0.0,1.0,0.0)   Position of light i       2.12.1     lighting
                             CONSTANT ATTENUATION      8 R+              GetLightfv              1.0          Constant atten. factor    2.12.1     lighting
                               LINEAR ATTENUATION      8 R+              GetLightfv              0.0          Linear atten. factor      2.12.1     lighting
                             QUADRATIC ATTENUATION     8 R+              GetLightfv              0.0          Quadratic atten.          2.12.1     lighting
                                                                                                              factor
                                 SPOT DIRECTION        8            D    GetLightfv         (0.0,0.0,-1.0)    Spotlight direction of    2.12.1     lighting
                                                                                                              light i
                                 SPOT EXPONENT         8           R+    GetLightfv              0.0          Spotlight exponent of     2.12.1     lighting
                                                                                                                                                                 141




                                                                                                              light i
                                  SPOT CUTOFF           8 R+             GetLightfv             180.0         Spot. angle of light i    2.12.1     lighting
                                     LIGHTi              8 B             IsEnabled              False         True if light i enabled   2.12.1 lighting/enable
                                 COLOR INDEXES         2 3 R             GetFloatv              0,1,1         am , dm , and sm for      2.12.1     lighting
                                                                                                              color index lighting
                                                                                                                                                                 142




                                                                                           Get         Initial
                                                            Get value         Type         Cmnd        Value         Description        Sec.     Attribute
                                                             POINT SIZE        R+        GetFloatv       1.0 Point size                  3.3       point
                                                           POINT SMOOTH        B         IsEnabled      False  Point antialiasing on     3.3 point/enable
                                                             LINE WIDTH        R+        GetFloatv       1.0 Line width                  3.4        line
                                                            LINE SMOOTH        B         IsEnabled      False  Line antialiasing on      3.4    line/enable
                                                       LINE STIPPLE PATTERN    Z+       GetIntegerv      1's Line stipple               3.4.2       line
                                                        LINE STIPPLE REPEAT    Z+       GetIntegerv       1    Line stipple repeat      3.4.2       line
                                                            LINE STIPPLE       B         IsEnabled      False  Line stipple enable      3.4.2 line/enable
                                                              CULL FACE        B         IsEnabled      False  Polygon culling          3.5.1 polygon/enable
                                                                                                               enabled
                                                         CULL FACE MODE        Z3       GetIntegerv     BACK Cull front/back facing     3.5.1      polygon
                                                                                                               polygons




Version 1.0 - 1 July 1994
                                                           FRONT FACE          Z2       GetIntegerv      CCW   Polygon frontface        3.5.1      polygon
                                                                                                               CW/CCW indicator




                            Table 6.8. Rasterization
                                                        POLYGON SMOOTH         B         IsEnabled      False  Polygon antialiasing     3.5     polygon/enable
                                                                                                               on
                                                          POLYGON MODE        2 Z3      GetIntegerv     FILL Polygon rasterization      3.5.4      polygon
                                                                                                               mode (front & back)
                                                               {               I     GetPolygonStipple 1's Polygon stipple               3.5 polygon-stipple
                                                         POLYGON STIPPLE       B         IsEnabled      False  Polygon stipple enable   3.5.2 polygon/enable
                                                                                                                                                                 CHAPTER 6. STATE AND STATE REQUESTS
                                                                                  Get              Initial
                                                  Get value         Type          Cmnd             Value             Description      Sec.     Attribute
                                                  TEXTURE x          B          IsEnabled          False      True if x-D texturing   3.8.4 texture/enable
                                                                                                              enabled (x is 1D or
                                                                                                              2D)
                                                   TEXTURE          n I        GetTexImage         see 3.8    x-D texture image at    3.8         {
                                                                                                              l.o.d. i
                                                TEXTURE WIDTH       n Z + GetTexLevelParameter       0        x-D texture image i's   3.8         {
                                                                                                              width
                                                TEXTURE HEIGHT      n Z + GetTexLevelParameter       0        x-D texture image i's   3.8         {
                                                                                                              height
                                               TEXTURE BORDER       n Z + GetTexLevelParameter       0        x-D texture image i's   3.8         {
                                                                                                              border width
                                             TEXTURE COMPONENTS     n Z4 GetTexLevelParameter        1        Texture image           3.8         {
                                                                                                              components
                                             TEXTURE BORDER COLOR   2 C      GetTexParameter       0,0,0,0    Texture border color     3.8      texture
                                               TEXTURE MIN FILTER   2 Z6     GetTexParameter       see 3.8    Texture mini cation     3.8.1     texture
                                                                                                              function
                                              TEXTURE MAG FILTER    2 Z2     GetTexParameter       see 3.8    Texture magni cation    3.8.2     texture
                                                                                                              function
                                                TEXTURE WRAP x      2 Z2     GetTexParameter      REPEAT      Texture wrap mode (x    3.8       texture




                      Table 6.9. Texturing
                                                                                                              is S or T)




Version 1.0 - 1 July 1994
                                              TEXTURE ENV MODE       Z3        GetTexEnviv       MODULATE     Texture application     3.8.3     texture
                                                                                                              function
                                              TEXTURE ENV COLOR      C         GetTexEnvfv         0,0,0,0    Texture environment     3.8.3     texture
                                                                                                              color
                                                TEXTURE GEN x       4 B         IsEnabled          False      Texgen enabled (x is    2.9.4 texture/enable
                                                                                                              S, T, R, or Q)
                                                  EYE LINEAR        4 R4       GetTexGenfv        see 2.9.4   Texgen plane equation   2.9.4     texture
                                                                                                              coe cients
                                                OBJECT LINEAR       4 R4       GetTexGenfv        see 2.9.4   Texgen object linear    2.9.4     texture
                                                                                                                                                             143




                                                                                                              coe cients
                                              TEXTURE GEN MODE      4 Z3       GetTexGeniv       EYE LINEAR   Function used for       2.9.4     texture
                                                                                                              texgen
                                                                                                                                                                           144


                                                                                               Get        Initial
                                                                 Get value           Type      Cmnd       Value            Description        Sec.        Attribute
                                                                SCISSOR TEST          B      IsEnabled    False     Scissoring enabled        4.1.2    scissor/enable
                                                                 SCISSOR BOX         4 Z    GetIntegerv see 4.1.2   Scissor box               4.1.2         scissor
                                                                STENCIL TEST          B      IsEnabled    False     Stenciling enabled        4.1.4 stencil-bu er/enable
                                                                STENCIL FUNC          Z8    GetIntegerv ALWAYS      Stencil function          4.1.4     stencil-bu er
                                                             STENCIL VALUE MASK       Z+    GetIntegerv 1's         Stencil mask              4.1.4     stencil-bu er
                                                                 STENCIL REF          Z+    GetIntegerv     0       Stencil reference value   4.1.4     stencil-bu er
                                                                 STENCIL FAIL         Z6    GetIntegerv KEEP        Stencil fail action       4.1.4     stencil-bu er
                                                           STENCIL PASS DEPTH FAIL    Z6    GetIntegerv KEEP        Stencil depth bu er       4.1.4     stencil-bu er
                                                                                                                    fail action
                                                           STENCIL PASS DEPTH PASS    Z6    GetIntegerv    KEEP     Stencil depth bu er       4.1.4     stencil-bu er
                                                                                                                    pass action
                                                                 ALPHA TEST          B       IsEnabled     False    Alpha test enabled        4.1.3   color-bu er/enable
                                                              ALPHA TEST FUNC        Z8     GetIntegerv   ALWAYS    Alpha test function       4.1.3       color-bu er
                                                               ALPHA TEST REF        R+     GetIntegerv     0       Alpha test reference      4.1.3       color-bu er




Version 1.0 - 1 July 1994
                                                                                                                    value
                                                                DEPTH TEST            B      IsEnabled     False    Depth bu er enabled       4.1.5 depth-bu er/enable
                                                                DEPTH FUNC            Z8    GetIntegerv    LESS     Depth bu er test          4.1.5    depth-bu er
                                                                                                                    function




                            Table 6.10. Pixel Operations
                                                                   BLEND              B      IsEnabled     False    Blending enabled          4.1.6   color-bu er/enable
                                                                 BLEND SRC            Z9    GetIntegerv    ONE      Blending source           4.1.6       color-bu er
                                                                                                                    function
                                                                 BLEND DST            Z8    GetIntegerv    ZERO     Blending destination      4.1.6      color-bu er
                                                                                                                    function
                                                                 LOGIC OP             B      IsEnabled     False    Logic op enabled          4.1.8   color-bu er/enable
                                                               LOGIC OP MODE         Z16    GetIntegerv    COPY     Logic op function         4.1.8       color-bu er
                                                                  DITHER              B      IsEnabled     True     Dithering enabled         4.1.7   color-bu er/enable
                                                                                                                                                                           CHAPTER 6. STATE AND STATE REQUESTS
                                                                                             Get       Initial
                                                                 Get value         Type      Cmnd      Value          Description         Sec.     Attribute
                                                                DRAW BUFFER        Z10    GetIntegerv see 4.2.1 Bu ers selected for       4.2.1   color-bu er
                                                                                                                drawing
                                                              INDEX WRITEMASK       Z+    GetIntegerv    1's    Color index writemask     4.2.2   color-bu er
                                                              COLOR WRITEMASK      4 B    GetBooleanv True Color write enables R,         4.2.2   color-bu er
                                                                                                                G, B, or A
                                                              DEPTH WRITEMASK       B     GetBooleanv True Depth bu er enabled            4.2.2 depth-bu er
                                                                                                                for writing
                                                             STENCIL WRITEMASK      Z+    GetIntegerv    1's    Stencil bu er             4.2.2 stencil-bu er
                                                                                                                writemask
                                                             COLOR CLEAR VALUE      C      GetFloatv 0,0,0,0 Color bu er clear            4.2.3   color-bu er
                                                                                                                value (RGBA mode)
                                                             INDEX CLEAR VALUE      CI     GetFloatv      0     Color bu er clear value   4.2.3   color-bu er
                                                                                                                (color index mode)




Version 1.0 - 1 July 1994
                                                             DEPTH CLEAR VALUE      R+    GetIntegerv     1     Depth bu er clear         4.2.3 depth-bu er




                            Table 6.11. Framebu er Control
                                                                                                                value
                                                             STENCIL CLEAR VALUE    Z+    GetIntegerv     0     Stencil clear value       4.2.3 stencil-bu er
                                                              ACCUM CLEAR VALUE    4 R+    GetFloatv      0     Accumulation bu er        4.2.3 accum-bu er
                                                                                                                clear value
                                                                                                                                                                145
                                                                                                                                        146



                                                                            Get      Initial
                                                     Get value        Type  Cmnd     Value      Description            Sec. Attribute
                                                 UNPACK SWAP BYTES     B GetBooleanv False Value of                    4.3      {
                                                                                                  UNPACK SWAP BYTES
                                                  UNPACK LSB FIRST     B   GetBooleanv    False   Value of             4.3      {
                                                                                                  UNPACK LSB FIRST
                                                 UNPACK ROW LENGTH    Z+    GetIntegerv    0      Value of             4.3      {
                                                                                                  UNPACK ROW LENGTH
                                                 UNPACK SKIP ROWS     Z+    GetIntegerv    0      Value of             4.3      {
                                                                                                  UNPACK SKIP ROWS
                                                 UNPACK SKIP PIXELS   Z+    GetIntegerv    0      Value of             4.3      {
                                                                                                  UNPACK SKIP PIXELS
                                                 UNPACK ALIGNMENT     Z+    GetIntegerv    4      Value of             4.3      {
                                                                                                  UNPACK ALIGNMENT
                                                  PACK SWAP BYTES      B   GetBooleanv    False   Value of             4.3      {




Version 1.0 - 1 July 1994
                                                                                                  PACK SWAP BYTES
                                                   PACK LSB FIRST                         False




                            Table 6.12. Pixels
                                                                       B   GetBooleanv            Value of             4.3      {
                                                                                                  PACK LSB FIRST
                                                  PACK ROW LENGTH     Z+    GetIntegerv    0      Value of             4.3      {
                                                                                                  PACK ROW LENGTH
                                                   PACK SKIP ROWS     Z+    GetIntegerv    0      Value of             4.3      {
                                                                                                  PACK SKIP ROWS
                                                  PACK SKIP PIXELS    Z+    GetIntegerv    0      Value of             4.3      {
                                                                                                  PACK SKIP PIXELS
                                                  PACK ALIGNMENT      Z+    GetIntegerv    4      Value of             4.3      {
                                                                                                  PACK ALIGNMENT
                                                                                                                                        CHAPTER 6. STATE AND STATE REQUESTS
                                                                                        Get         Initial
                                                          Get value       Type          Cmnd        Value      Description       Sec. Attribute
                                                          MAP COLOR        B        GetBooleanv     FalseTrue if colors are      4.3    pixel
                                                                                                         mapped
                                                         MAP STENCIL       B       GetBooleanv False True if stencil values      4.3    pixel
                                                                                                         are mapped
                                                          INDEX SHIFT      Z       GetIntegerv     0     Value of INDEX SHIFT 4.3       pixel
                                                         INDEX OFFSET      Z       GetIntegerv     0     Value of INDEX OFFSET 4.3      pixel
                                                            x SCALE        R        GetFloatv      1     Value of x SCALE x is 4.3      pixel
                                                                                                         RED, GREEN, BLUE,
                                                                                                         ALPHA, or DEPTH
                                                            x BIAS         R        GetFloatv      0     Value of x BIAS x is    4.3    pixel
                                                                                                         one of RED, GREEN,
                                                                                                         BLUE, ALPHA, or DEPTH
                                                           ZOOM X          R        GetFloatv     1.0    x zoom factor           4.3    pixel
                                                           ZOOM Y          R        GetFloatv     1.0    y zoom factor           4.3    pixel
                                                              x         8 32     R GetPixelMap    0's    RGBA PixelMap           4.3      {
                                                                                                         translation tables x is




                            Table 6.13. Pixels (cont.)




Version 1.0 - 1 July 1994
                                                                                                         a map name from
                                                                                                         Table 3.3
                                                              x         2 32     Z GetPixelMap    0's    Index PixelMap          4.3      {
                                                                                                         translation tables x is
                                                                                                         a map name from
                                                                                                         Table 3.3
                                                            x SIZE        Z+       GetIntegerv     1     Size of table x         4.3      {
                                                         READ BUFFER      Z3       GetIntegerv see 4.3.2 Read source bu er       4.3    pixel
                                                                                                                                                  147
                                                                                                                                                                             148




                                                                                                                  Get       Initial
                                                                                   Get value             Type     Cmnd      Value         Description      Sec. Attribute
                                                                                    ORDER               9 Z8    GetMapiv       1    1d map order           5.1      {
                                                                                    ORDER             9 2 Z8    GetMapiv      1,1   2d map orders          5.1      {
                                                                                     COEFF            9 8 Rn    GetMapfv    see 5.1 1d control points      5.1      {
                                                                                     COEFF          9 8 8 Rn    GetMapfv    see 5.1 2d control points      5.1      {
                                                                                    DOMAIN             9 2 R    GetMapfv    see 5.1 1d domain endpoints    5.1      {
                                                                                    DOMAIN             9 4 R    GetMapfv    see 5.1 2d domain endpoints    5.1      {
                                                                                    MAP1 x               9 B    IsEnabled    False  1d map enables: x is   5.1 eval/enable
                                                                                                                                    map type
                                                                                     MAP2 x           9 B       IsEnabled    False  2d map enables: x is   5.1 eval/enable
                                                                                                                                    map type




Version 1.0 - 1 July 1994
                                                                                MAP1 GRID DOMAIN       2 R      GetFloatv     0,1 1d grid endpoints        5.1     eval
                                                                                MAP2 GRID DOMAIN       4 R      GetFloatv   0,1 0,1 2d grid endpoints      5.1     eval
                                                                               MAP1 GRID SEGMENTS       Z+      GetFloatv      1    1d grid divisions      5.1     eval
                                                                               MAP2 GRID SEGMENTS     2 Z+      GetFloatv     1,1 2d grid divisions        5.1     eval
                                                                                  AUTO NORMAL           B       IsEnabled    False  True if automatic      5.1     eval
                                                                                                                                    normal generation
                                                                                                                                    enabled




                            Table 6.14. Evaluators (GetMap takes a map name)
                                                                                                                                                                             CHAPTER 6. STATE AND STATE REQUESTS
                                                                                     Get        Initial
                                                        Get value             Type   Cmnd       Value         Description        Sec. Attribute
                                                PERSPECTIVE CORRECTION HINT    Z3 GetIntegerv DONT CARE Perspective correction   5.6    hint
                                                                                                        hint
                                                    POINT SMOOTH HINT          Z3 GetIntegerv DONT CARE Point smooth hint        5.6     hint
                                                     LINE SMOOTH HINT          Z3 GetIntegerv DONT CARE Line smooth hint         5.6     hint
                                                   POLYGON SMOOTH HINT         Z3 GetIntegerv DONT CARE Polygon smooth hint      5.6     hint




                            Table 6.15. Hints
                                                         FOG HINT              Z3 GetIntegerv DONT CARE Fog hint                 5.6     hint




Version 1.0 - 1 July 1994
                                                                                                                                                  149
                                                                                                                 Get      Minimum
                                                                                  Get value            Type      Cmnd     Value            Description      Sec. Attribute
                                                                                                                                                                             150


                                                                                  MAX LIGHTS            Z+    GetIntegerv     8     Maximum number of 2.12.1         {
                                                                                                                                    lights
                                                                               MAX CLIP PLANES          Z+    GetIntegerv     6     Maximum number of       2.10     {
                                                                                                                                    user clipping planes
                                                                          MAX MODELVIEW STACK DEPTH     Z+    GetIntegerv    32     Maximum model-view 2.9.2         {
                                                                                                                                    stack depth
                                                                          MAX PROJECTION STACK DEPTH    Z+    GetIntegerv     2     Maximum projection      2.9.2    {
                                                                                                                                    matrix stack depth
                                                                           MAX TEXTURE STACK DEPTH      Z+    GetIntegerv     2     Maximum number          2.9.2    {
                                                                                                                                    depth of texture
                                                                                                                                    matrix stack
                                                                                 SUBPIXEL BITS          Z+    GetIntegerv     4     Number of bits of         3      {
                                                                                                                                    subpixel precision in x
                                                                                                                                    &y
                                                                               MAX TEXTURE SIZE         Z+    GetIntegerv    64     Maximum height or        3.8     {
                                                                                                                                    width of a texture




Version 1.0 - 1 July 1994
                                                                                                                                    image (w/o borders)
                                                                             MAX PIXEL MAP TABLE        Z+    GetIntegerv    32     Maximum size of a       3.6.2    {
                                                                                                                                    PixelMap translation
                                                                                                                                    table
                                                                            MAX NAME STACK DEPTH        Z+    GetIntegerv    64     Maximum selection        5.2     {
                                                                                                                                    name stack depth
                                                                               MAX LIST NESTING         Z+    GetIntegerv    64     Maximum display list     5.4     {




                            Table 6.16. Implementation Dependent Values
                                                                                                                                    call nesting
                                                                               MAX EVAL ORDER           Z+    GetIntegerv     8     Maximum evaluator        5.1     {
                                                                                                                                    polynomial order
                                                                              MAX VIEWPORT DIMS        2 Z+   GetIntegerv see 2.9.1 Maximum viewport        2.9.1    {
                                                                                                                                    dimensions
                                                                                                                                                                             CHAPTER 6. STATE AND STATE REQUESTS




                                                                            MAX ATTRIB STACK DEPTH      Z+    GetIntegerv    16     Maximum depth of the      6      {
                                                                                                                                    attribute stack
                                                                                                                  Get      Minimum
                                                                                     Get value          Type      Cmnd     Value         Description         Sec. Attribute
                                                                                    AUX BUFFERS          Z+    GetIntegerv     0   Number of auxiliary       4.2.1    {
                                                                                                                                   bu ers
                                                                                     RGBA MODE           B     GetBooleanv     {   True if color bu ers      2.7      {
                                                                                                                                   store rgba
                                                                                    INDEX MODE           B     GetBooleanv     {   True if color bu ers      2.7      {
                                                                                                                                   store indexes
                                                                                   DOUBLEBUFFER          B     GetBooleanv     {   True if front & back      4.2.1    {
                                                                                                                                   bu ers exist
                                                                                      STEREO             B     GetBooleanv     {   True if left & right       6       {
                                                                                                                                   bu ers exist
                                                                                  POINT SIZE RANGE      2 R+    GetFloatv     1,1  Range (lo to hi) of       3.3      {
                                                                                                                                   antialiased point sizes
                                                                               POINT SIZE GRANULARITY    R+     GetFloatv      {   Antialiased point size    3.3      {




Version 1.0 - 1 July 1994
                                                                                                                                   granularity
                                                                                  LINE WIDTH RANGE      2 R+    GetFloatv     1,1  Range (lo to hi) of       3.4      {
                                                                                                                                   antialiased line widths
                                                                               LINE WIDTH GRANULARITY    R+     GetFloatv      {   Antialiased line width    3.4      {
                                                                                                                                   granularity




                            Table 6.17. More Implementation Dependent Values
                                                                                                                                                                              151
                                                                                                           Get      Initial
                                                                                   Get value       Type    Cmnd     Value         Description      Sec. Attribute
                                                                                    RED BITS        Z + GetIntegerv    -    Number of bits per red 4        {
                                                                                                                                                                    152


                                                                                                                            component in color
                                                                                                                            bu ers
                                                                                   GREEN BITS       Z + GetIntegerv    -    Number of bits per      4       {
                                                                                                                            green component in
                                                                                                                            color bu ers
                                                                                   BLUE BITS        Z + GetIntegerv    -    Number of bits per      4       {
                                                                                                                            blue component in
                                                                                                                            color bu ers
                                                                                   ALPHA BITS       Z + GetIntegerv    -    Number of bits per      4       {
                                                                                                                            alpha component in
                                                                                                                            color bu ers
                                                                                   INDEX BITS       Z + GetIntegerv    -    Number of bits per      4       {
                                                                                                                            index in color bu ers
                                                                                   DEPTH BITS       Z + GetIntegerv    -    Number of depth         4       {
                                                                                                                            bu er planes
                                                                                  STENCIL BITS      Z + GetIntegerv    -    Number of stencil       4       {




Version 1.0 - 1 July 1994
                                                                                                                            planes
                                                                                 ACCUM RED BITS     Z + GetIntegerv    -    Number of bits per red 4        {
                                                                                                                            component in the
                                                                                                                            accumulation bu er
                                                                                ACCUM GREEN BITS    Z + GetIntegerv - Number of bits per            4       {
                                                                                                                            green component in
                                                                                                                            the accumulation
                                                                                                                            bu er
                                                                                ACCUM BLUE BITS     Z + GetIntegerv - Number of bits per            4       {




                            Table 6.18. Implementation Dependent Pixel Depths
                                                                                                                            blue component in the
                                                                                                                            accumulation bu er
                                                                                ACCUM ALPHA BITS    Z + GetIntegerv    -    Number of bits per      4       {
                                                                                                                                                                    CHAPTER 6. STATE AND STATE REQUESTS




                                                                                                                            alpha component in
                                                                                                                            the accumulation
                                                                                                                            bu er
                                                                                        Get    Initial
                                                            Get value         Type      Cmnd   Value         Description         Sec. Attribute
                                                            LIST BASE          Z+  GetIntegerv    0    Setting of ListBase       5.4     list
                                                            LIST INDEX         Z+  GetIntegerv    0    number of display list    5.4      {
                                                                                                       under construction 0
                                                                                                       if none
                                                            LIST MODE          Z+  GetIntegerv    0    Mode of display list      5.4      {
                                                                                                       under construction
                                                                                                       unde ned if none
                                                                 {           16 A       {      empty Attribute stack              6       {
                                                        ATTRIB STACK DEPTH     Z+  GetIntegerv    0    Attribute stack pointer    6       {
                                                         NAME STACK DEPTH      Z+  GetIntegerv    0    Name stack depth          5.2      {
                                                           RENDER MODE         Z3  GetIntegerv RENDER RenderMode setting         5.2      {
                                                                 {             Z+       {         {    Selection bu er           5.2      {
                                                                                                       pointer
                                                                {              Z+       {         {    Selection bu er size      5.2      {
                                                                {              Z +                {    Feedback bu er            5.3      {




                            Table 6.19. Miscellaneous
                                                                                        {




Version 1.0 - 1 July 1994
                                                                                                       pointer
                                                                {              Z+       {         {    Feedback bu er size       5.3      {
                                                                {              Z5       {         {    Feedback type             5.3      {
                                                                {             n Z8  GetError      0    Current error code(s)     2.5      {
                                                                {             n B       {       False  True if there is a        2.5      {
                                                                                                       corresponding error
                                                                                                                                                  153
Appendix A
Invariance
The OpenGL speci cation is not pixel exact. It therefore does not guarantee
an exact match between images produced by di erent GL implementations.
However, the speci cation does specify exact matches, in some cases, for
images produced by the same implementation. The purpose of this appendix
is to identify and provide justi cation for those cases that require exact
matches.


A.1 Repeatability
The obvious and most fundamental case is repeated issuance of a series of
GL commands. For any given GL and framebu er state vector, and for
any GL command, the resulting GL and framebu er state must be identical
whenever the command is executed on that initial GL and framebu er state.
    One purpose of repeatability is avoidance of visual artifacts when a
double-bu ered scene is redrawn. If rendering is not repeatable, swapping
between two bu ers rendered with the same command sequence may re-
sult in visible changes in the image. Such false motion is distracting to the
viewer. Another reason for repeatability is testability.
    Repeatability, while important, is a weak requirement. Given only re-
peatability as a requirement, two scenes rendered with one (small) polygon
changed in position might di er at every pixel. Such a di erence, while
within the law of repeatability, is certainly not within its spirit. Additional
invariance rules are desirable to ensure useful operation.
                                       154




                        Version 1.0 - 1 July 1994
A.2. MULTI-PASS ALGORITHMS                                               155

A.2 Multi-pass Algorithms
Invariance is necessary for a whole set of useful multi-pass algorithms. Such
algorithms render multiple times, each time with a di erent GL mode vec-
tor, to eventually produce a result in the framebu er. Examples of these
algorithms include:
       \Erasing" a primitive from the framebu er by redrawing it, either in
       a di erent color or using the XOR logical operation.
       Using stencil operations to compute capping planes.
    On the other hand, invariance rules can greatly increase the complexity
of high-performance implementations of the GL. Even the weak repeatabil-
ity requirement signi cantly constrains a parallel implementation of the GL.
Because GL implementations are required to implement ALL GL capabili-
ties, not just a convenient subset, those that utilize hardware acceleration
are expected to alternate between hardware and software modules based on
the current GL mode vector. A strong invariance requirement forces the
behavior of the hardware and software modules to be identical, something
that may be very di cult to achieve (for example, if the hardware does
  oating-point operations with di erent precision than the software).
    What is desired is a compromise that results in many compliant, high-
performance implementations, and in many software vendors choosing to
port to OpenGL.

A.3 Invariance Rules
For a given instantiation of an OpenGL rendering context:
Rule 1 For any given GL and framebu er state vector, and for any given
GL command, the resulting GL and framebu er state must be identical each
time the command is executed on that initial GL and framebu er state.
Rule 2 Changes to the following state values have no side e ects (the use
of any other state value is not a ected by the change):
Required:
           Framebu er contents (all bitplanes)
           The color bu ers enabled for writing




                               Version 1.0 - 1 July 1994
156                                           APPENDIX A. INVARIANCE

           The values of matrices other than the top-of-stack matrices
           Scissor parameters (other than enable)
           Writemasks (color, index, depth, stencil)
           Clear values (color, index, depth, stencil, accumulation)
           Current values (color, index, normal, texture coords, edge ag)
           Current raster color, index and texture coordinates.
           Material properties (ambient, di use, specular, emission, shini-
           ness)
Strongly suggested:
           Matrix mode
           Matrix stack depths
           Alpha test parameters (other than enable)
           Stencil parameters (other than enable)
           Depth test parameters (other than enable)
           Blend parameters (other than enable)
           Logical operation parameters (other than enable)
           Pixel storage and transfer state
           Evaluator state (except as it a ects the vertex data generated by
           the evaluators)
Corollary 1 Fragment generation is invariant with respect to the state val-
ues marked with in Rule 2.
Corollary 2 The window coordinates (x, y, and z) of generated fragments
are also invariant with respect to
Required:
           Current values (color, color index, normal, texture coords, edge-
            ag)
           Current raster color, color index, and texture coordinates
           Material properties (ambient, di use, specular, emission, shini-
           ness)




                       Version 1.0 - 1 July 1994
A.4. WHAT ALL THIS MEANS                                                     157

Rule 3 The arithmetic of each per-fragment operation is invariant except
with respect to parameters that directly control it (the parameters that control
the alpha test, for instance, are the alpha test enable, the alpha test function,
and the alpha test reference value).
Corollary 3 Images rendered into di erent color bu ers, either simultane-
ously or separately using the same command sequence, are pixel identical.
(Note that this does not hold between X pixmaps and color bu ers, how-
ever.)

A.4 What All This Means
Hardware accelerated GL implementations are expected to default to soft-
ware operation when some GL state vectors are encountered. Even the weak
repeatability requirement means, for example, that OpenGL implementa-
tions cannot apply hysteresis to this swap, but must instead guarantee that
a given mode vector implies that a subsequent command always is executed
in either the hardware or the software machine.
    The stronger invariance rules constrain when the switch from hardware
to software rendering can occur, given that the software and hardware ren-
derers are not pixel identical. For example, the switch can be made when
blending is enabled or disabled, but it should not be made when a change
is made to the blending parameters.
    Because oating point values may be represented using di erent formats
in di erent renderers (hardware and software), many OpenGL state values
may change subtly when renderers are swapped. This is the type of state
value change that Rule 1 seeks to avoid.




   X is a registered trademark of the MIT X Consortium.




                                 Version 1.0 - 1 July 1994
Appendix B
Corollaries
The following observations are derived from the body and the other ap-
pendixes of the speci cation. Absence of an observation from this list in no
way impugns its veracity.
  1. The CURRENT RASTER TEXTURE COORDINATES must be maintained cor-
     rectly at all times, including periods while texture mapping is not
     enabled, and when the GL is in color index mode.
  2. When requested, texture coordinates returned in feedback mode are
     always valid, including periods while texture mapping is not enabled,
     and when the GL is in color index mode.
  3. The error semantics of upward compatible OpenGL revisions may
     change. Otherwise, only additions can be made to upward compat-
     ible revisions.
  4. GL query commands are not required to satisfy the semantics of the
     Flush or the Finish commands. All that is required is that the
     queried state be consistent with complete execution of all previously
     executed GL commands.
  5. Application speci ed point size and line width must be returned as
     speci ed when queried. Implementation dependent clamping a ects
     the values only while they are in use.
  6. Bitmaps and pixel transfers do not cause selection hits.
                                      158




                       Version 1.0 - 1 July 1994
                                                                       159

 7. The mask speci ed as the third argument to StencilFunc a ects the
    operands of the stencil comparison function, but has no direct e ect on
    the update of the stencil bu er. The mask speci ed by StencilMask
    has no e ect on the stencil comparison function it limits the e ect of
    the update of the stencil bu er.
 8. Polygon shading is completed before the polygon mode is interpreted.
    If the shade model is FLAT, all of the points or lines generated by a
    single polygon will have the same color.
 9. A display list is just a group of commands and arguments, so errors
    generated by commands in a display list must be generated when the
    list is executed. If the list is created in COMPILE mode, errors should
    not be generated while the list is being created.
10. RasterPos does not change the current raster index from its default
    value in an RGBA mode GL context. Likewise, RasterPos does not
    change the current raster color from its default value in a color index
    GL context. Both the current raster index and the current raster
    color can be queried, however, regardless of the color mode of the GL
    context.
11. A material property that is attached to the current color via Color-
    Material always takes the value of the current color. Attempts to
    change that material property via Material calls have no e ect.
12. Material and ColorMaterial can be used to modify the RGBA ma-
    terial properties, even in a color index context. Likewise, Material
    can be used to modify the color index material properties, even in an
    RGBA context.
13. Their is no atomicity requirement for OpenGL rendering commands,
    even at the fragment level.
14. Because rasterization of non-antialiased polygons is point sampled,
    polygons that have no area generate no fragments when they are ras-
    terized in FILL mode, and the fragments generated by the rasterization
    of \narrow" polygons may not form a continuous array.
15. OpenGL does not force left- or right-handedness on any of its coor-
    dinates systems. Consider, however, the following conditions: (1) the
    object coordinate system is right-handed (2) the only commands used




                             Version 1.0 - 1 July 1994
160                                         APPENDIX B. COROLLARIES

     to manipulate the model-view matrix are Scale (with positive scaling
     values only), Rotate, and Translate (3) exactly one of either Frus-
     tum or Ortho is used to set the projection matrix (4) the near value
     is less than the far value for DepthRange. If these conditions are all
     satis ed, then the eye coordinate system is right-handed and the clip,
     normalized device, and window coordinate systems are left-handed.
 16. ColorMaterial has no e ect on color index lighting.
 17. (No pixel dropouts or duplicates.) Let two polygons share an identical
     edge (that is, there exist vertices A and B of an edge of one polygon,
     and vertices C and D of an edge of the other polygon, and the coordi-
     nates of vertex A (resp. B) are identical to those of vertex C (resp. D),
     and the state of the the coordinate transfomations is identical when
     A, B, C, and D are speci ed). Then, when the fragments produced
     by rasterization of both polygons are taken together, each fragment
     intersecting the interior of the shared edge is produced exactly once.




                       Version 1.0 - 1 July 1994
Index of GL calls
Accum, 106                                CullFace, 63, 64
AlphaFunc, 95
                                          DeleteLists, 128
Begin, 12, 15, 16, 18{20, 22, 48,         DepthFunc, 97
         56, 59, 60, 63, 66, 118,         DepthMask, 104
         119, 124                         DepthRange, 24, 130, 133, 160
Bitmap, 77, 78                            Disable, 29, 31, 33, 38, 43, 53, 56,
BlendFunc, 98                                     59, 63, 66, 88, 90, 95{98,
CallList, 20, 125, 127                            100, 116, 117
CallLists, 20, 127                        DrawBu er, 102, 103
Clear, 104, 105                           DrawPixels, 65, 67{74, 77{79, 107,
ClearAccum, 105                                   110, 111, 113, 123
ClearColor, 104
ClearDepth, 105                           EdgeFlag, 19, 20
ClearIndex, 105                           EdgeFlagv, 19
ClearStencil, 105                         Enable, 29, 31, 33, 38, 43, 53, 56,
ClipPlane, 32                                     59, 63, 66, 88, 90, 95{98,
Color, 20, 21, 37, 49                             100, 116, 117, 130
Color3, 21                                End, 12, 15{20, 22, 48, 56, 63, 66,
Color4, 21                                        118, 119, 124
Colorb, 38                                EndList, 125
Colorf, 38                                EvalCoord, 20, 116
Colori, 38                                EvalCoord1, 116, 118, 119
ColorMask, 103                            EvalCoord1d, 118
ColorMaterial, 43, 45, 46, 159            EvalCoord1f, 118
Colors, 38                                EvalCoord2, 116, 119, 120
Colorub, 38, 49                           EvalMesh1, 118
Colorui, 38, 49                           EvalMesh2, 118, 119
Colorus, 38, 49                           EvalPoint, 20
CopyPixels, 67{69, 107, 112, 113,         EvalPoint1, 119
         123                              EvalPoint2, 119
                                    161




                             Version 1.0 - 1 July 1994
162                                                                   INDEX

FeedbackBu er, 123, 124, 128               LoadIdentity, 26
Finish, 128, 129, 158                      LoadMatrix, 25, 26
Flush, 128, 129, 158                       LoadName, 121
Fog, 90, 91                                LogicOp, 100, 101
FrontFace, 42, 63
Frustum, 26, 27, 160                       Map1, 115, 116, 133
                                           Map2, 115, 116, 133
GenLists, 128                              MapGrid1, 118
Get, 25, 128, 130                          MapGrid2, 118
GetBooleanv, 130, 133                      Material, 20, 42{44, 47, 159
GetClipPlane, 131                          MatrixMode, 25
GetDoublev, 130, 131, 133                  MultMatrix, 25, 26
GetError, 11, 12
GetFloatv, 130, 131, 133                   NewList, 125, 127
GetIntegerv, 130, 133                      Normal, 20, 21
GetLight, 131                              Normal3, 9, 21, 29
GetMap, 131, 132                           Normal3d, 9
GetMaterial, 131                           Normal3dv, 9
GetPixelMap, 131, 132                      Normal3f, 9
GetPolygonStipple, 132                     Normal3fv, 9
GetString, 132, 133
GetTexEnv, 131                             Ortho, 26, 27, 160
GetTexGen, 131                             PassThrough, 124
GetTexImage, 132                           PixelMap, 67, 69, 71, 108, 113
GetTexLevelParameter, 131, 132             PixelStore, 67{69, 71, 108, 113,
GetTexParameter, 131                               128
Hint, 129                                  PixelTransfer, 67, 69, 71, 108, 113
                                           PixelZoom, 77
Index, 20, 21                              PointSize, 53
IndexMask, 103, 104                        PolygonMode, 62, 66, 121, 123
InitNames, 120, 121                        PolygonStipple, 65
IsEnabled, 128, 130, 133                   PopAttrib, 133, 135
IsList, 128                                PopMatrix, 28
                                           PopName, 120, 121
Light, 42{44                               PushAttrib, 133, 135
LightModel, 42, 44                         PushMatrix, 28
LineStipple, 59                            PushName, 120, 121
LineWidth, 56
ListBase, 127, 128                         RasterPos, 34, 121, 159




                      Version 1.0 - 1 July 1994
INDEX                                                    163

RasterPos2, 35
RasterPos3, 35
RasterPos4, 35
ReadBu er, 109, 113
ReadPixels, 67{69, 72{74, 107{
        109, 112, 128, 132
Rect, 22, 63
RenderMode, 122{124, 128
Rotate, 26, 160
Scale, 26, 27, 160
Scissor, 95
SelectBu er, 121, 122, 128
ShadeModel, 48
StencilFunc, 96, 97, 159
StencilMask, 104, 107, 159
StencilOp, 96, 97
TexCoord, 20
TexCoord1, 21
TexCoord2, 21
TexCoord3, 21
TexCoord4, 21
TexEnv, 88
TexGen, 30, 31
TexImage1D, 80, 81, 86
TexImage2D, 79{81, 86
TexParameter, 81
Translate, 26, 27, 160
Vertex, 7, 20, 35, 117
Vertex2, 20, 22
Vertex2sv, 8
Vertex3, 20
Vertex3f, 7
Vertex4, 20
Viewport, 25




                             Version 1.0 - 1 July 1994
