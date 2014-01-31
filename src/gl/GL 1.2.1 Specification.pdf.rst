The OpenGL Graphics System:
                   R


       A Speci cation
       Version 1.2.1

                Mark Segal
                Kurt Akeley
  Editor version 1.1: Chris Frazier
 Editor versions 1.2, 1.2.1: Jon Leech




    Version 1.2.1 - April 1, 1999
             Copyright c 1992-1999 Silicon Graphics, Inc.

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
set forth in FAR 52.227.19c2 or subparagraph c1ii of the Rights
in Technical Data and Computer Software clause at DFARS 252.227-7013
and or in similar or successor clauses in the FAR or the DOD or NASA FAR
Supplement. Unpublished rights reserved under the copyright laws of the
United States. Contractor manufacturer is Silicon Graphics, Inc., 2011 N.
Shoreline Blvd., Mountain View, CA 94039-7311.
    OpenGL is a registered trademark of Silicon Graphics, Inc.
       Unix is a registered trademark of The Open Group.
    The "X" device and X Windows System are trademarks of
                         The Open Group.




                               Version 1.2.1 - April 1, 1999
Contents
1 Introduction                                                                                        1
  1.1   Formatting of Optional Features . . . .       .   .   .   .   .   .   .   .   .   .   .   .    1
  1.2   What is the OpenGL Graphics System?           .   .   .   .   .   .   .   .   .   .   .   .    1
  1.3   Programmer's View of OpenGL . . . . .         .   .   .   .   .   .   .   .   .   .   .   .    2
  1.4   Implementor's View of OpenGL . . . . .        .   .   .   .   .   .   .   .   .   .   .   .    2
  1.5   Our View . . . . . . . . . . . . . . . . .    .   .   .   .   .   .   .   .   .   .   .   .    3
2 OpenGL Operation                                                                                    4
  2.1 OpenGL Fundamentals . . . . . . . . . . .               .   .   .   .   .   .   .   .   .   .    4
       2.1.1 Floating-Point Computation . . . .               .   .   .   .   .   .   .   .   .   .    6
  2.2 GL State . . . . . . . . . . . . . . . . . . .          .   .   .   .   .   .   .   .   .   .    6
  2.3 GL Command Syntax . . . . . . . . . . . .               .   .   .   .   .   .   .   .   .   .    7
  2.4 Basic GL Operation . . . . . . . . . . . . .            .   .   .   .   .   .   .   .   .   .    9
  2.5 GL Errors . . . . . . . . . . . . . . . . . . .         .   .   .   .   .   .   .   .   .   .   11
  2.6 Begin End Paradigm . . . . . . . . . . . . .            .   .   .   .   .   .   .   .   .   .   12
       2.6.1 Begin and End Objects . . . . . . .              .   .   .   .   .   .   .   .   .   .   15
       2.6.2 Polygon Edges . . . . . . . . . . . .            .   .   .   .   .   .   .   .   .   .   18
       2.6.3 GL Commands within Begin End .                   .   .   .   .   .   .   .   .   .   .   19
  2.7 Vertex Speci cation . . . . . . . . . . . . .           .   .   .   .   .   .   .   .   .   .   19
  2.8 Vertex Arrays . . . . . . . . . . . . . . . . .         .   .   .   .   .   .   .   .   .   .   21
  2.9 Rectangles . . . . . . . . . . . . . . . . . . .        .   .   .   .   .   .   .   .   .   .   28
  2.10 Coordinate Transformations . . . . . . . . .           .   .   .   .   .   .   .   .   .   .   28
       2.10.1 Controlling the Viewport . . . . . .            .   .   .   .   .   .   .   .   .   .   30
       2.10.2 Matrices . . . . . . . . . . . . . . . .        .   .   .   .   .   .   .   .   .   .   31
       2.10.3 Normal Transformation . . . . . . .             .   .   .   .   .   .   .   .   .   .   34
       2.10.4 Generating Texture Coordinates . .              .   .   .   .   .   .   .   .   .   .   36
  2.11 Clipping . . . . . . . . . . . . . . . . . . . .       .   .   .   .   .   .   .   .   .   .   38
  2.12 Current Raster Position . . . . . . . . . . .          .   .   .   .   .   .   .   .   .   .   40
  2.13 Colors and Coloring . . . . . . . . . . . . .          .   .   .   .   .   .   .   .   .   .   43
                                      i



                               Version 1.2.1 - April 1, 1999
ii                                                                            CONTENTS

          2.13.1   Lighting . . . . . . . . . . . . . . . . . .   .   .   .   .   .   .   .   .    44
          2.13.2   Lighting Parameter Speci cation . . . .        .   .   .   .   .   .   .   .    49
          2.13.3   ColorMaterial . . . . . . . . . . . . .        .   .   .   .   .   .   .   .    51
          2.13.4   Lighting State . . . . . . . . . . . . . .     .   .   .   .   .   .   .   .    53
          2.13.5   Color Index Lighting . . . . . . . . . . .     .   .   .   .   .   .   .   .    53
          2.13.6   Clamping or Masking . . . . . . . . . .        .   .   .   .   .   .   .   .    54
          2.13.7   Flatshading . . . . . . . . . . . . . . . .    .   .   .   .   .   .   .   .    54
          2.13.8   Color and Texture Coordinate Clipping          .   .   .   .   .   .   .   .    55
          2.13.9   Final Color Processing . . . . . . . . . .     .   .   .   .   .   .   .   .    56
3 Rasterization                                                                                   57
     3.1 Invariance . . . . . . . . . . . . . . . . . . . . . . . . . . .                 .   .    59
     3.2 Antialiasing . . . . . . . . . . . . . . . . . . . . . . . . . .                 .   .    59
     3.3 Points . . . . . . . . . . . . . . . . . . . . . . . . . . . . .                 .   .    60
         3.3.1 Point Rasterization State . . . . . . . . . . . . . .                      .   .    62
     3.4 Line Segments . . . . . . . . . . . . . . . . . . . . . . . .                    .   .    62
         3.4.1 Basic Line Segment Rasterization . . . . . . . . . .                       .   .    64
         3.4.2 Other Line Segment Features . . . . . . . . . . . .                        .   .    66
         3.4.3 Line Rasterization State . . . . . . . . . . . . . . .                     .   .    69
     3.5 Polygons . . . . . . . . . . . . . . . . . . . . . . . . . . . .                 .   .    70
         3.5.1 Basic Polygon Rasterization . . . . . . . . . . . . .                      .   .    70
         3.5.2 Stippling . . . . . . . . . . . . . . . . . . . . . . .                    .   .    72
         3.5.3 Antialiasing . . . . . . . . . . . . . . . . . . . . . .                   .   .    72
         3.5.4 Options Controlling Polygon Rasterization . . . .                          .   .    73
         3.5.5 Depth O set . . . . . . . . . . . . . . . . . . . . .                      .   .    73
         3.5.6 Polygon Rasterization State . . . . . . . . . . . . .                      .   .    75
     3.6 Pixel Rectangles . . . . . . . . . . . . . . . . . . . . . . .                   .   .    75
         3.6.1 Pixel Storage Modes . . . . . . . . . . . . . . . . .                      .   .    75
         3.6.2 The Imaging Subset . . . . . . . . . . . . . . . . .                       .   .    76
         3.6.3 Pixel Transfer Modes . . . . . . . . . . . . . . . .                       .   .    78
         3.6.4 Rasterization of Pixel Rectangles . . . . . . . . . .                      .   .    88
         3.6.5 Pixel Transfer Operations . . . . . . . . . . . . . .                      .   .   100
     3.7 Bitmaps . . . . . . . . . . . . . . . . . . . . . . . . . . . .                  .   .   110
     3.8 Texturing . . . . . . . . . . . . . . . . . . . . . . . . . . .                  .   .   111
         3.8.1 Texture Image Speci cation . . . . . . . . . . . . .                       .   .   112
         3.8.2 Alternate Texture Image Speci cation Commands                              .   .   118
         3.8.3 Texture Parameters . . . . . . . . . . . . . . . . .                       .   .   123
         3.8.4 Texture Wrap Modes . . . . . . . . . . . . . . . . .                       .   .   124
         3.8.5 Texture Mini cation . . . . . . . . . . . . . . . . .                      .   .   125
         3.8.6 Texture Magni cation . . . . . . . . . . . . . . . .                       .   .   131




                       Version 1.2.1 - April 1, 1999
CONTENTS                                                                                                                           iii

       3.8.7 Texture State and Proxy State . . . . . . . .                                                    .   .   .   .   .   131
       3.8.8 Texture Objects . . . . . . . . . . . . . . . .                                                  .   .   .   .   .   132
       3.8.9 Texture Environments and Texture Functions                                                       .   .   .   .   .   135
       3.8.10 Texture Application . . . . . . . . . . . . . .                                                 .   .   .   .   .   138
  3.9 Color Sum . . . . . . . . . . . . . . . . . . . . . . . .                                               .   .   .   .   .   138
  3.10 Fog . . . . . . . . . . . . . . . . . . . . . . . . . . . .                                            .   .   .   .   .   138
  3.11 Antialiasing Application . . . . . . . . . . . . . . . .                                               .   .   .   .   .   140
4 Per-Fragment Operations and the Framebu er                                                                                      141
  4.1 Per-Fragment Operations . . . . . . .                                   .   .   .   .   .   .   .   .   .   .   .   .   .   142
      4.1.1 Pixel Ownership Test . . . . .                                    .   .   .   .   .   .   .   .   .   .   .   .   .   142
      4.1.2 Scissor test . . . . . . . . . . .                                .   .   .   .   .   .   .   .   .   .   .   .   .   143
      4.1.3 Alpha test . . . . . . . . . . . .                                .   .   .   .   .   .   .   .   .   .   .   .   .   143
      4.1.4 Stencil test . . . . . . . . . . .                                .   .   .   .   .   .   .   .   .   .   .   .   .   144
      4.1.5 Depth bu er test . . . . . . . .                                  .   .   .   .   .   .   .   .   .   .   .   .   .   145
      4.1.6 Blending . . . . . . . . . . . . .                                .   .   .   .   .   .   .   .   .   .   .   .   .   146
      4.1.7 Dithering . . . . . . . . . . . .                                 .   .   .   .   .   .   .   .   .   .   .   .   .   149
      4.1.8 Logical Operation . . . . . . .                                   .   .   .   .   .   .   .   .   .   .   .   .   .   150
  4.2 Whole Framebu er Operations . . . .                                     .   .   .   .   .   .   .   .   .   .   .   .   .   150
      4.2.1 Selecting a Bu er for Writing .                                   .   .   .   .   .   .   .   .   .   .   .   .   .   150
      4.2.2 Fine Control of Bu er Updates                                     .   .   .   .   .   .   .   .   .   .   .   .   .   152
      4.2.3 Clearing the Bu ers . . . . . .                                   .   .   .   .   .   .   .   .   .   .   .   .   .   153
      4.2.4 The Accumulation Bu er . . .                                      .   .   .   .   .   .   .   .   .   .   .   .   .   155
  4.3 Drawing, Reading, and Copying Pixels                                    .   .   .   .   .   .   .   .   .   .   .   .   .   156
      4.3.1 Writing to the Stencil Bu er .                                    .   .   .   .   .   .   .   .   .   .   .   .   .   156
      4.3.2 Reading Pixels . . . . . . . . .                                  .   .   .   .   .   .   .   .   .   .   .   .   .   156
      4.3.3 Copying Pixels . . . . . . . . .                                  .   .   .   .   .   .   .   .   .   .   .   .   .   162
      4.3.4 Pixel Draw Read state . . . . .                                   .   .   .   .   .   .   .   .   .   .   .   .   .   162
5 Special Functions                                                                                                               164
  5.1   Evaluators . . . .    .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   164
  5.2   Selection . . . . .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   170
  5.3   Feedback . . . .      .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   173
  5.4   Display Lists . .     .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   175
  5.5   Flush and Finish      .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   179
  5.6   Hints . . . . . . .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   179
6 State and State Requests                                                                                                        181
  6.1 Querying GL State . . . . . . . . . . . . . . . . . . . . . . . . 181
      6.1.1 Simple Queries . . . . . . . . . . . . . . . . . . . . . . 181




                                      Version 1.2.1 - April 1, 1999
iv                                                                                                       CONTENTS

         6.1.2 Data Conversions . . . . . .                      .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   182
         6.1.3 Enumerated Queries . . . .                        .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   182
         6.1.4 Texture Queries . . . . . .                       .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   184
         6.1.5 Stipple Query . . . . . . . .                     .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   185
         6.1.6 Color Matrix Query . . . .                        .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   185
         6.1.7 Color Table Query . . . . .                       .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   185
         6.1.8 Convolution Query . . . . .                       .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   186
         6.1.9 Histogram Query . . . . . .                       .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   187
         6.1.10 Minmax Query . . . . . . .                       .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   188
         6.1.11 Pointer and String Queries                       .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   189
         6.1.12 Saving and Restoring State                       .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   189
     6.2 State Tables . . . . . . . . . . . . .                  .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   193
A Invariance                                                                                                                 218
     A.1   Repeatability . . . . .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   218
     A.2   Multi-pass Algorithms     .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   219
     A.3   Invariance Rules . . .    .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   219
     A.4   What All This Means       .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   221
B Corollaries                                                                                                                222
C Version 1.1                                                                                                                225
     C.1 Vertex Array . . . . . . . . .              .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   225
     C.2 Polygon O set . . . . . . . .               .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   226
     C.3 Logical Operation . . . . . .               .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   226
     C.4 Texture Image Formats . . .                 .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   226
     C.5 Texture Replace Environment                 .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   226
     C.6 Texture Proxies . . . . . . . .             .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   227
     C.7 Copy Texture and Subtexture                 .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   227
     C.8 Texture Objects . . . . . . .               .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   227
     C.9 Other Changes . . . . . . . .               .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   227
     C.10 Acknowledgements . . . . . .               .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   228
D Version 1.2                                                                                                                230
     D.1   Three-Dimensional Texturing . . . .                       .   .   .   .   .   .   .   .   .   .   .   .   .   .   230
     D.2   BGRA Pixel Formats . . . . . . . .                        .   .   .   .   .   .   .   .   .   .   .   .   .   .   230
     D.3   Packed Pixel Formats . . . . . . . .                      .   .   .   .   .   .   .   .   .   .   .   .   .   .   230
     D.4   Normal Rescaling . . . . . . . . . . .                    .   .   .   .   .   .   .   .   .   .   .   .   .   .   231
     D.5   Separate Specular Color . . . . . . .                     .   .   .   .   .   .   .   .   .   .   .   .   .   .   231
     D.6   Texture Coordinate Edge Clamping                          .   .   .   .   .   .   .   .   .   .   .   .   .   .   231




                      Version 1.2.1 - April 1, 1999
CONTENTS                                                                                                    v

  D.7 Texture Level of Detail Control . .     .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   232
  D.8 Vertex Array Draw Element Range         .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   232
  D.9 Imaging Subset . . . . . . . . . . .    .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   232
       D.9.1 Color Tables . . . . . . . .     .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   232
       D.9.2 Convolution . . . . . . . . .    .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   233
       D.9.3 Color Matrix . . . . . . . .     .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   233
       D.9.4 Pixel Pipeline Statistics . .    .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   234
       D.9.5 Constant Blend Color . . .       .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   234
       D.9.6 New Blending Equations . .       .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   234
  D.10 Acknowledgements . . . . . . . . .     .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   234
E Version 1.2.1                                                                                           238
F ARB Extensions                                                                                          239
  F.1 Naming Conventions . . . . . . . . . . . . . . . . . . . . . . . 239
  F.2 Multitexture . . . . . . . . . . . . . . . . . . . . . . . . . . . 240
      F.2.1 Dependencies . . . . . . . . . . . . . . . . . . . . . . . 240
      F.2.2 Issues . . . . . . . . . . . . . . . . . . . . . . . . . . . 240
      F.2.3 Changes to Section 2.6 Begin End Paradigm . . . . 240
      F.2.4 Changes to Section 2.7 Vertex Speci cation . . . . . 241
      F.2.5 Changes to Section 2.8 Vertex Arrays . . . . . . . . 243
      F.2.6 Changes to Section 2.10.2 Matrices . . . . . . . . . . 244
      F.2.7 Changes to Section 2.10.4 Generating Texture Coor-
             dinates . . . . . . . . . . . . . . . . . . . . . . . . . . 245
      F.2.8 Changes to Section 2.12 Current Raster Position . . 246
      F.2.9 Changes to Section 3.8 Texturing . . . . . . . . . . . 246
      F.2.10 Changes to Section 3.8.5 Texture Mini cation . . . . 248
      F.2.11 Changes to Section 3.8.8 Texture Objects . . . . . . 248
      F.2.12 Changes to Section 3.8.10 Texture Application . . . 249
      F.2.13 Changes to Section 5.1 Evaluators . . . . . . . . . . 249
      F.2.14 Changes to Section 5.3 Feedback . . . . . . . . . . . 249
      F.2.15 Changes to Section 6.1.2 Data Conversions . . . . . 251
      F.2.16 Changes to Section 6.1.12 Saving and Restoring State251
  Index of OpenGL Commands                                                                                256




                              Version 1.2.1 - April 1, 1999
List of Figures
 2.1 Block diagram of the GL. . . . . . . . . . . . . . . . . . . . .                9
 2.2 Creation of a processed vertex from a transformed vertex and
      current values. . . . . . . . . . . . . . . . . . . . . . . . . . .           13
 2.3 Primitive assembly and processing. . . . . . . . . . . . . . . .               13
 2.4 Triangle strips, fans, and independent triangles. . . . . . . . .              16
 2.5 Quadrilateral strips and independent quadrilaterals. . . . . .                 17
 2.6 Vertex transformation sequence. . . . . . . . . . . . . . . . .                28
 2.7 Current raster position. . . . . . . . . . . . . . . . . . . . . .             41
 2.8 Processing of RGBA colors. . . . . . . . . . . . . . . . . . . .               43
 2.9 Processing of color indices. . . . . . . . . . . . . . . . . . . .             43
 2.10 ColorMaterial operation. . . . . . . . . . . . . . . . . . . . . .            51
 3.1    Rasterization. . . . . . . . . . . . . . . . . . . . . . . . . .   .   .    57
 3.2    Rasterization of non-antialiased wide points. . . . . . . . .      .   .    61
 3.3    Rasterization of antialiased wide points. . . . . . . . . . .      .   .    61
 3.4    Visualization of Bresenham's algorithm. . . . . . . . . . .        .   .    64
 3.5    Rasterization of non-antialiased wide lines. . . . . . . . .       .   .    67
 3.6    The region used in rasterizing an antialiased line segment.        .   .    69
 3.7    Operation of DrawPixels. . . . . . . . . . . . . . . . . .         .   .    88
 3.8    Selecting a subimage from an image . . . . . . . . . . . .         .   .    93
 3.9    A bitmap and its associated parameters. . . . . . . . . . .        .   .   110
 3.10   A texture image and the coordinates used to access it. . .         .   .   118
 4.1 Per-fragment operations. . . . . . . . . . . . . . . . . . . . . . 142
 4.2 Operation of ReadPixels. . . . . . . . . . . . . . . . . . . . 156
 4.3 Operation of CopyPixels. . . . . . . . . . . . . . . . . . . . 162
 5.1 Map Evaluation. . . . . . . . . . . . . . . . . . . . . . . . . . 166
 5.2 Feedback syntax. . . . . . . . . . . . . . . . . . . . . . . . . . 176
                                       vi



                    Version 1.2.1 - April 1, 1999
LIST OF FIGURES                                                           vii

  F.1 Creation of a processed vertex from a transformed vertex and
      current values. . . . . . . . . . . . . . . . . . . . . . . . . . . 241
  F.2 Current raster position. . . . . . . . . . . . . . . . . . . . . . 246
  F.3 Multitexture pipeline. . . . . . . . . . . . . . . . . . . . . . . 249




                              Version 1.2.1 - April 1, 1999
List of Tables
 2.1   GL command su xes . . . . . . . . . . . . . . . . . . . . .        .     8
 2.2   GL data types . . . . . . . . . . . . . . . . . . . . . . . . .    .    10
 2.3   Summary of GL errors . . . . . . . . . . . . . . . . . . . . .     .    13
 2.4   Vertex array sizes values per vertex and data types . . . .      .    22
 2.5   Variables that direct the execution of InterleavedArrays.          .    26
 2.6   Component conversions . . . . . . . . . . . . . . . . . . . .      .    44
 2.7   Summary of lighting parameters. . . . . . . . . . . . . . . .      .    46
 2.8   Correspondence of lighting parameter symbols to names. . .         .    50
 2.9   Polygon atshading color selection. . . . . . . . . . . . . . .     .    55
 3.1 PixelStore parameters pertaining to one or more of Draw-
      Pixels, TexImage1D, TexImage2D, and TexImage3D. .                        76
 3.2 PixelTransfer parameters. . . . . . . . . . . . . . . . . . . .           78
 3.3 PixelMap parameters. . . . . . . . . . . . . . . . . . . . . .            79
 3.4 Color table names. . . . . . . . . . . . . . . . . . . . . . . . .        80
 3.5 DrawPixels and ReadPixels types . . . . . . . . . . . . . .               91
 3.6 DrawPixels and ReadPixels formats. . . . . . . . . . . . .                92
 3.7 Swap Bytes Bit ordering. . . . . . . . . . . . . . . . . . . . .          92
 3.8 Packed pixel formats. . . . . . . . . . . . . . . . . . . . . . . .       94
 3.9 UNSIGNED BYTE formats. Bit numbers are indicated for each
      component. . . . . . . . . . . . . . . . . . . . . . . . . . . . .       95
 3.10 UNSIGNED SHORT formats . . . . . . . . . . . . . . . . . . . . .         96
 3.11 UNSIGNED INT formats . . . . . . . . . . . . . . . . . . . . . . .       97
 3.12 Packed pixel eld assignments . . . . . . . . . . . . . . . . . .         98
 3.13 Color table lookup. . . . . . . . . . . . . . . . . . . . . . . . .     103
 3.14 Computation of ltered color components. . . . . . . . . . . .           104
 3.15 Conversion from RGBA pixel components to internal texture,
      table, or lter components. . . . . . . . . . . . . . . . . . . .        114
 3.16 Correspondence of sized internal formats to base internal for-
      mats. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .   115
                                     viii



                   Version 1.2.1 - April 1, 1999
LIST OF TABLES                                                                             ix

  3.17 Texture parameters and their values. . . . . . . . . . . . . . . 124
  3.18 Replace and modulate texture functions. . . . . . . . . . . . . 136
  3.19 Decal and blend texture functions. . . . . . . . . . . . . . . . 137
  4.1 Values controlling the source blending function and the source
      blending values they compute. f = minAs ; 1 , Ad . . . . . . 148
  4.2 Values controlling the destination blending function and the
      destination blending values they compute. . . . . . . . . . . 148
  4.3 Arguments to LogicOp and their corresponding operations. . 151
  4.4 Arguments to DrawBu er and the bu ers that they indicate.152
  4.5 PixelStore parameters pertaining to ReadPixels,
      GetTexImage1D, GetTexImage2D, GetTexImage3D,
      GetColorTable, GetConvolutionFilter, GetSeparable-
      Filter, GetHistogram, and GetMinmax. . . . . . . . . . . 158
  4.6 ReadPixels index masks. . . . . . . . . . . . . . . . . . . . . 160
  4.7 ReadPixels GL Data Types and Reversed component con-
      version formulas. . . . . . . . . . . . . . . . . . . . . . . . . . 161
  5.1 Values speci ed by the target to Map1. . . . . . . . . . . . . 165
  5.2 Correspondence of feedback type to number of values per vertex.174
  6.1    Texture, table, and lter return values. . . . . . . . .      .   .   .   .   .   185
  6.2    Attribute groups . . . . . . . . . . . . . . . . . . . .     .   .   .   .   .   191
  6.3    State variable types . . . . . . . . . . . . . . . . . .     .   .   .   .   .   192
  6.4    GL Internal begin-end state variables inaccessible .       .   .   .   .   .   194
  6.5    Current Values and Associated Data . . . . . . . . .         .   .   .   .   .   195
  6.6    Vertex Array Data . . . . . . . . . . . . . . . . . . .      .   .   .   .   .   196
  6.7    Transformation state . . . . . . . . . . . . . . . . . .     .   .   .   .   .   197
  6.8    Coloring . . . . . . . . . . . . . . . . . . . . . . . . .   .   .   .   .   .   198
  6.9    Lighting see also Table 2.7 for defaults . . . . . . .     .   .   .   .   .   199
  6.10   Lighting cont. . . . . . . . . . . . . . . . . . . . . .   .   .   .   .   .   200
  6.11   Rasterization . . . . . . . . . . . . . . . . . . . . . .    .   .   .   .   .   201
  6.12   Texture Objects . . . . . . . . . . . . . . . . . . . .      .   .   .   .   .   202
  6.13   Texture Objects cont. . . . . . . . . . . . . . . . .      .   .   .   .   .   203
  6.14   Texture Environment and Generation . . . . . . . .           .   .   .   .   .   204
  6.15   Pixel Operations . . . . . . . . . . . . . . . . . . . .     .   .   .   .   .   205
  6.16   Framebu er Control . . . . . . . . . . . . . . . . . .       .   .   .   .   .   206
  6.17   Pixels . . . . . . . . . . . . . . . . . . . . . . . . . .   .   .   .   .   .   207
  6.18   Pixels cont. . . . . . . . . . . . . . . . . . . . . . .   .   .   .   .   .   208
  6.19   Pixels cont. . . . . . . . . . . . . . . . . . . . . . .   .   .   .   .   .   209




                                 Version 1.2.1 - April 1, 1999
x                                                                    LIST OF TABLES

    6.20   Pixels cont. . . . . . . . . . . . . . . . .    .   .   .   .   .   .   .   .   .   .   .   210
    6.21   Pixels cont. . . . . . . . . . . . . . . . .    .   .   .   .   .   .   .   .   .   .   .   211
    6.22   Evaluators GetMap takes a map name              .   .   .   .   .   .   .   .   .   .   .   212
    6.23   Hints . . . . . . . . . . . . . . . . . . . . .   .   .   .   .   .   .   .   .   .   .   .   213
    6.24   Implementation Dependent Values . . . .           .   .   .   .   .   .   .   .   .   .   .   214
    6.25   More Implementation Dependent Values .            .   .   .   .   .   .   .   .   .   .   .   215
    6.26   Implementation Dependent Pixel Depths .           .   .   .   .   .   .   .   .   .   .   .   216
    6.27   Miscellaneous . . . . . . . . . . . . . . . .     .   .   .   .   .   .   .   .   .   .   .   217
    F.1    Changes to State Tables . . . . . . . . . . . . . . . . . . . . .                             252
    F.2    Changes to State Tables cont. . . . . . . . . . . . . . . . . .                             253
    F.3    New State Introduced by Multitexture . . . . . . . . . . . . .                                254
    F.4    New Implementation-Dependent Values Introduced by Mul-
           titexture . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .                         255




                       Version 1.2.1 - April 1, 1999
Chapter 1
Introduction
This document describes the OpenGL graphics system: what it is, how it
acts, and what is required to implement it. We assume that the reader has
at least a rudimentary understanding of computer graphics. This means
familiarity with the essentials of computer graphics algorithms as well as
familiarity with basic graphics hardware and associated terms.

1.1 Formatting of Optional Features
Starting with version 1.2 of OpenGL, some features in the speci cation are
considered optional; an OpenGL implementation may or may not choose to
provide them see section 3.6.2.
   Portions of the speci cation which are optional are so labelled where
they are de ned. Additionally, those portions are typeset in gray, and state
table entries which are optional are typeset against a gray background .

1.2 What is the OpenGL Graphics System?
OpenGL for Open Graphics Library" is a software interface to graphics
hardware. The interface consists of a set of several hundred procedures and
functions that allow a programmer to specify the objects and operations
involved in producing high-quality graphical images, speci cally color images
of three-dimensional objects.
    Most of OpenGL requires that the graphics hardware contain a frame-
bu er. Many OpenGL calls pertain to drawing objects such as points, lines,
polygons, and bitmaps, but the way that some of this drawing occurs such
as when antialiasing or texturing is enabled relies on the existence of a
                                      1



                               Version 1.2.1 - April 1, 1999
2                                            CHAPTER 1. INTRODUCTION

framebu er. Further, some of OpenGL is speci cally concerned with frame-
bu er manipulation.

1.3 Programmer's View of OpenGL
To the programmer, OpenGL is a set of commands that allow the speci -
cation of geometric objects in two or three dimensions, together with com-
mands that control how these objects are rendered into the framebu er.
For the most part, OpenGL provides an immediate-mode interface, mean-
ing that specifying an object causes it to be drawn.
    A typical program that uses OpenGL begins with calls to open a window
into the framebu er into which the program will draw. Then, calls are made
to allocate a GL context and associate it with the window. Once a GL con-
text is allocated, the programmer is free to issue OpenGL commands. Some
calls are used to draw simple geometric objects i.e. points, line segments,
and polygons, while others a ect the rendering of these primitives includ-
ing how they are lit or colored and how they are mapped from the user's
two- or three-dimensional model space to the two-dimensional screen. There
are also calls to e ect direct control of the framebu er, such as reading and
writing pixels.

1.4 Implementor's View of OpenGL
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




                     Version 1.2.1 - April 1, 1999
1.5. OUR VIEW                                                            3

information explicit, to elucidate how it changes, and to indicate what its
e ects are.

1.5 Our View
We view OpenGL as a state machine that controls a set of speci c draw-
ing operations. This model should engender a speci cation that satis es
the needs of both programmers and implementors. It does not, however,
necessarily provide a model for implementation. An implementation must
produce results conforming to those produced by the speci ed methods, but
there may be ways to carry out a particular computation that are more
e cient than the one speci ed.




                              Version 1.2.1 - April 1, 1999
Chapter 2
OpenGL Operation
2.1 OpenGL Fundamentals
OpenGL henceforth, the GL" is concerned only with rendering into a
framebu er and reading values stored in that framebu er. There is no
support for other peripherals sometimes associated with graphics hardware,
such as mice and keyboards. Programmers must rely on other mechanisms
to obtain user input.
    The GL draws primitives subject to a number of selectable modes. Each
primitive is a point, line segment, polygon, or pixel rectangle. Each mode
may be changed independently; the setting of one does not a ect the settings
of others although many modes may interact to determine what eventually
ends up in the framebu er. Modes are set, primitives speci ed, and other
GL operations described by sending commands in the form of function or
procedure calls.
    Primitives are de ned by a group of one or more vertices. A vertex
de nes a point, an endpoint of an edge, or a corner of a polygon where
two edges meet. Data consisting of positional coordinates, colors, normals,
and texture coordinates are associated with a vertex and each vertex is
processed independently, in order, and in the same way. The only exception
to this rule is if the group of vertices must be clipped so that the indicated
primitive ts within a speci ed region; in this case vertex data may be
modi ed and new vertices created. The type of clipping depends on which
primitive the group of vertices represents.
    Commands are always processed in the order in which they are received,
although there may be an indeterminate delay before the e ects of a com-
mand are realized. This means, for example, that one primitive must be
                                        4



                    Version 1.2.1 - April 1, 1999
2.1. OPENGL FUNDAMENTALS                                                  5

drawn completely before any subsequent one can a ect the framebu er. It
also means that queries and pixel read operations return state consistent
with complete execution of all previously invoked GL commands. In gen-
eral, the e ects of a GL command on either GL modes or the framebu er
must be complete before any subsequent command can have any such e ects.
    In the GL, data binding occurs on call. This means that data passed
to a command are interpreted when that command is received. Even if the
command requires a pointer to data, those data are interpreted when the
call is made, and any subsequent changes to the data have no e ect on the
GL unless the same pointer is used in a subsequent command.
    The GL provides direct control over the fundamental operations of 3D
and 2D graphics. This includes speci cation of such parameters as trans-
formation matrices, lighting equation coe cients, antialiasing methods, and
pixel update operators. It does not provide a means for describing or mod-
eling complex geometric objects. Another way to describe this situation is
to say that the GL provides mechanisms to describe how complex geometric
objects are to be rendered rather than mechanisms to describe the complex
objects themselves.
    The model for interpretation of GL commands is client-server. That is, a
program the client issues commands, and these commands are interpreted
and processed by the GL the server. The server may or may not operate
on the same computer as the client. In this sense, the GL is network-
transparent." A server may maintain a number of GL contexts, each of which
is an encapsulation of current GL state. A client may choose to connect to
any one of these contexts. Issuing GL commands when the program is not
connected to a context results in unde ned behavior.
    The e ects of GL commands on the framebu er are ultimately controlled
by the window system that allocates framebu er resources. It is the window
system that determines which portions of the framebu er the GL may access
at any given time and that communicates to the GL how those portions
are structured. Therefore, there are no GL commands to con gure the
framebu er or initialize the GL. Similarly, display of framebu er contents
on a CRT monitor including the transformation of individual framebu er
values by such techniques as gamma correction is not addressed by the GL.
Framebu er con guration occurs outside of the GL in conjunction with the
window system; the initialization of a GL context occurs when the window
system allocates a window for GL rendering.
    The GL is designed to be run on a range of graphics platforms with vary-
ing graphics capabilities and performance. To accommodate this variety, we
specify ideal behavior instead of actual behavior for certain GL operations.




                               Version 1.2.1 - April 1, 1999
6                                    CHAPTER 2. OPENGL OPERATION

In cases where deviation from the ideal is allowed, we also specify the rules
that an implementation must obey if it is to approximate the ideal behavior
usefully. This allowed variation in GL behavior implies that two distinct
GL implementations may not agree pixel for pixel when presented with the
same input even when run on identical framebu er con gurations.
    Finally, command names, constants, and types are pre xed in the GL
by gl, GL , and GL, respectively in C to reduce name clashes with other
packages. The pre xes are omitted in this document for clarity.
2.1.1 Floating-Point Computation
The GL must perform a number of oating-point operations during the
course of its operation. We do not specify how oating-point numbers are
to be represented or how operations on them are to be performed. We require
simply that numbers' oating-point parts contain enough bits and that their
exponent elds are large enough so that individual results of oating-point
operations are accurate to about 1 part in 105 . The maximum representable
magnitude of a oating-point number used to represent positional or normal
coordinates must be at least 232 ; the maximum representable magnitude for
colors or texture coordinates must be at least 210 . The maximum repre-
sentable magnitude for all other oating-point values must be at least 232 .
x  0 = 0  x = 0 for any non-in nite and non-NaN x. 1  x = x  1 = x.
x + 0 = 0 + x = x. 00 = 1. Occasionally further requirements will be speci-
  ed. Most single-precision oating-point formats meet these requirements.
    Any representable oating-point value is legal as input to a GL command
that requires oating-point data. The result of providing a value that is not
a oating-point number to such a command is unspeci ed, but must not
lead to GL interruption or termination. In IEEE arithmetic, for example,
providing a negative zero or a denormalized number to a GL command yields
predictable results, while providing a NaN or an in nity yields unspeci ed
results.
    Some calculations require division. In such cases including implied di-
visions required by vector normalizations, a division by zero produces an
unspeci ed result but must not lead to GL interruption or termination.

2.2 GL State
The GL maintains considerable state. This document enumerates each state
variable and describes how each variable can be changed. For purposes
of discussion, state variables are categorized somewhat arbitrarily by their




                    Version 1.2.1 - April 1, 1999
2.3. GL COMMAND SYNTAX                                                            7

function. Although we describe the operations that the GL performs on the
framebu er, the framebu er is not a part of GL state.
    We distinguish two types of state. The rst type of state, called GL
server state, resides in the GL server. The majority of GL state falls into
this category. The second type of state, called GL client state, resides in the
GL client. Unless otherwise speci ed, all state referred to in this document
is GL server state; GL client state is speci cally identi ed. Each instance of
a GL context implies one complete set of GL server state; each connection
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
present, is v, indicating that the command takes a pointer to an array a
vector of values rather than a series of individual arguments. Two speci c
examples come from the Vertex command:
      void    Vertex3f float x, float y, float z ;
and
      void    Vertex2sv short v 2 ;
   These examples show the ANSI C declarations for these commands. In
general, a command declaration has the form1
  1 The   declarations shown in this document apply to ANSI C. Languages such as C++




                                   Version 1.2.1 - April 1, 1999
8                                       CHAPTER 2. OPENGL OPERATION

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

       rtype Namef 1234gf b s i f d ub us uigf vg
                           args , T arg1 , : : : , T argN , args ;

rtype is the return type of the function. The braces fg enclose a series
of characters or character pairs of which one is selected. indicates no
character. The arguments enclosed in brackets  args , and , args  may
or may not be present. The N arguments arg1 through argN have type T,
which corresponds to one of the type letters or letter pairs as indicated in
Table 2.1 if there are no letters, then the arguments' type is given explic-
itly. If the nal character is not v, then N is given by the digit 1, 2, 3, or
4 if there is no digit, then the number of arguments is xed. If the nal
character is v, then only arg1 is present and it is an array of N values of
the indicated type. Finally, we indicate an unsigned type by the shorthand
of prepending a u to the beginning of the type name so that, for instance,
unsigned char is abbreviated uchar.
    For example,
        void   Normal3ffdg T arg ;
indicates the two declarations
        void   Normal3f float arg1, float arg2, float arg3 ;
        void   Normal3d double arg1, double arg2, double arg3 ;
while
and Ada that allow passing of argument type information admit simpler declarations and
fewer entry points.




                       Version 1.2.1 - April 1, 1999
2.4. BASIC GL OPERATION                                                       9

      void   Normal3ffdgv T arg ;
means the two declarations
      void   Normal3fv float arg 3 ;
      void   Normal3dv double arg 3 ;
    Arguments whose type is xed i.e. not indicated by a su x on the
command are of one of 14 types or pointers to one of these. These types
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
on incoming and previously stored depth values to e ect depth bu ering,
blending of incoming fragment colors with stored colors, as well as masking
and other logical operations on fragment values.
    Finally, there is a way to bypass the vertex processing portion of the
pipeline to send a block of fragments directly to the individual fragment
operations, eventually causing a block of pixels to be written to the frame-
bu er; values may also be read back from the framebu er or copied from
one portion of the framebu er to another. These transfers may include some
type of decoding or encoding.
    This ordering is meant only as a tool for describing the GL, not as a strict
rule of how the GL is implemented, and we present it only as a means to




                                Version 1.2.1 - April 1, 1999
10                                   CHAPTER 2. OPENGL OPERATION




 GL Type Minimum Number of Bits Description
  boolean         1             Boolean
     byte         8             signed 2's complement binary inte-
                                ger
    ubyte         8             unsigned binary integer
    short         16            signed 2's complement binary inte-
                                ger
   ushort         16            unsigned binary integer
      int         32            signed 2's complement binary inte-
                                ger
     uint         32            unsigned binary integer
    sizei         32            Non-negative binary integer size
     enum         32            Enumerated binary integer value
 bitfield         32            Bit eld
    float         32            Floating-point value
   clampf         32            Floating-point value clamped to
                                 0; 1
   double         64            Floating-point value
   clampd         64            Floating-point value clamped to
                                 0; 1
Table 2.2: GL data types. GL types are not C types. Thus, for example,
GL type int is referred to as GLint outside this document, and is not
necessarily equivalent to the C type int. An implementation may use more
bits than the number indicated in the table to represent a GL type. Correct
interpretation of integer values outside the minimum range is not required,
however.




                    Version 1.2.1 - April 1, 1999
2.5. GL ERRORS                                                                        11


         Display
          List


                               Per−Vertex
                               Operations                  Per−
                                               Rasteriz−
                   Evaluator                               Fragment     Framebuffer
                               Primitive       ation
                                                           Operations
                               Assembly



                                               Texture
                                               Memory

                               Pixel
                               Operations



  Figure 2.1. Block diagram of the GL.


organize the various operations of the GL. Objects such as curved surfaces,
for instance, may be transformed before they are converted to polygons.

2.5 GL Errors
The GL detects only a subset of those conditions that could be considered
errors. This is because in many cases error checking would adversely impact
the performance of an error-free program.
    The command
     enum   GetError void ;
is used to obtain error information. Each detectable error is assigned a
numeric code. When an error is detected, a ag is set and the code is
recorded. Further errors, if they occur, do not a ect this recorded code.
When GetError is called, the code is returned and the ag is cleared,
so that a further error will again record its code. If a call to GetError
returns NO ERROR, then there has been no detectable error since the last call
to GetError or since the GL was initialized.
    To allow for distributed implementations, there may be several ag-
code pairs. In this case, after a call to GetError returns a value other
than NO ERROR each subsequent call returns the non-zero code of a distinct
  ag-code pair in unspeci ed order, until all non-NO ERROR codes have been




                                    Version 1.2.1 - April 1, 1999
12                                    CHAPTER 2. OPENGL OPERATION

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
access errors. This behavior is the current behavior; the action of the GL in
the presence of errors is subject to change.
    Three error generation conditions are implicit in the description of every
GL command. First, if a command that requires an enumerated value is
passed a symbolic constant that is not one of those speci ed as allowable for
that command, the error INVALID ENUM results. This is the case even if the
argument is a pointer to a symbolic constant if that value is not allowable
for the given command. Second, if a negative number is provided where an
argument of type sizei is speci ed, the error INVALID VALUE results. Finally,
if memory is exhausted as a side e ect of the execution of a command, the
error OUT OF MEMORY may be generated. Otherwise errors are generated only
for conditions that are explicitly described in this speci cation.

2.6 Begin End Paradigm
In the GL, most geometric objects are drawn by enclosing a series of coordi-
nate sets that specify vertices and optionally normals, texture coordinates,
and colors between Begin End pairs. There are ten geometric objects that
are drawn this way: points, line segments, line segment loops, separated
line segments, polygons, triangle strips, triangle fans, separated triangles,
quadrilateral strips, and separated quadrilaterals.
    Each vertex is speci ed with two, three, or four coordinates. In addi-
tion, a current normal, current texture coordinates, and current color may
be used in processing each vertex. Normals are used by the GL in light-
ing calculations; the current normal is a three-dimensional vector that may
be set by sending three coordinates that specify it. Texture coordinates
determine how a texture image is mapped onto a primitive.
    Primary and secondary colors are associated with each vertex see sec-




                     Version 1.2.1 - April 1, 1999
2.6. BEGIN END PARADIGM                                                    13

   Error                 Description                     O ending com-
                                                         mand ignored?
   INVALID ENUM          enum argument out of range      Yes
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
   TABLE TOO LARGE       The speci ed table is too large Yes

                     Table 2.3: Summary of GL errors

tion 3.9. These associated colors are either based on the current color
or produced by lighting, depending on whether or not lighting is enabled.
Texture coordinates are similarly associated with each vertex. Figure 2.2
summarizes the association of auxiliary data with a transformed vertex to
produce a processed vertex.
    The current values are part of GL state. Vertices and normals are trans-
formed, colors may be a ected or replaced by lighting, and texture coordi-
nates are transformed and possibly a ected by a texture coordinate genera-
tion function. The processing indicated for each current value is applied for
each vertex that is sent to the GL.
    The methods by which vertices, normals, texture coordinates, and colors
are sent to the GL, as well as how normals are transformed and how vertices
are mapped to the two-dimensional screen, are discussed later.
    Before colors have been assigned to a vertex, the state required by a
vertex is the vertex's coordinates, the current normal, the current edge ag
see section 2.6.2, the current material properties see section 2.13.2, and
the current texture coordinates. Because color assignment is done vertex-
by-vertex, a processed vertex comprises the vertex's coordinates, its edge
  ag, its assigned colors, and its texture coordinates.
    Figure 2.3 shows the sequence of operations that builds a primitive
point, line segment, or polygon from a sequence of vertices. After a primi-




                               Version 1.2.1 - April 1, 1999
14                                                 CHAPTER 2. OPENGL OPERATION


                    Vertex
                 Coordinates In


                                          vertex / normal                           Transformed
                                          transformation
                                                                                    Coordinates
        Current
        Normal
                                                                                                     Processed
                                                                                                       Vertex
                                                                                                        Out

        Current                                     lighting                           Associated
       Color and                                                                          Data
       Materials                                                                    (Colors, Edge Flag,
                                                                                       and Texture
                                                                                       Coordinates)

        Current
                                                            texture
        Texture                  texgen
                                                             matrix
        Coords


        Current
       Edge Flag



     Figure 2.2. Association of current values with a vertex. The heavy lined
     boxes represent GL state.



                                                                      Point culling;
                                                                      Line Segment
                 Coordinates         Point,                             or Polygon
                               Line Segment, or                          Clipping
     Processed
                                   Polygon                                                          Rasterization
      Vertices   Associated       (Primitive)
                   Data           Assembly                                Color
                                                                       Processing




                                  Begin/End
                                    State




     Figure 2.3. Primitive assembly and processing.




                               Version 1.2.1 - April 1, 1999
2.6. BEGIN END PARADIGM                                                     15

tive is formed, it is clipped to a viewing volume. This may alter the primitive
by altering vertex coordinates, texture coordinates, and colors. In the case
of a polygon primitive, clipping may insert new vertices into the primitive.
The vertices de ning a primitive to be rasterized have texture coordinates
and colors associated with them.
2.6.1 Begin and End Objects
Begin and End require one state variable with eleven values: one value for
each of the ten possible Begin End objects, and one other value indicating
that no Begin End object is being processed. The two relevant commands
are
      void   Begin enum mode ;
      void   End void ;
There is no limit on the number of vertices that may be speci ed between
a Begin and an End.
    Points. A series of individual points may be speci ed by calling Begin
with an argument value of POINTS. No special state need be kept between
Begin and End in this case, since each point is independent of previous
and following points.
    Line Strips. A series of one or more connected line segments is speci ed
by enclosing a series of two or more endpoints within a Begin End pair
when Begin is called with LINE STRIP. In this case, the rst vertex speci es
the rst segment's start point while the second vertex speci es the rst
segment's endpoint and the second segment's start point. In general, the
ith vertex for i 1 speci es the beginning of the ith segment and the end
of the i , 1st. The last vertex speci es the end of the last segment. If only
one vertex is speci ed between the Begin End pair, then no primitive is
generated.
    The required state consists of the processed vertex produced from the
last vertex that was sent so that a line segment can be generated from it
to the current vertex, and a boolean ag indicating if the current vertex is
the rst vertex.
    Line Loops. Line loops, speci ed with the LINE LOOP argument value to
Begin, are the same as line strips except that a nal segment is added from
the nal speci ed vertex to the rst vertex. The additional state consists of
the processed rst vertex.
    Separate Lines. Individual line segments, each speci ed by a pair of
vertices, are generated by surrounding vertex pairs with Begin and End




                                Version 1.2.1 - April 1, 1999
16                                    CHAPTER 2. OPENGL OPERATION

when the value of the argument to Begin is LINES. In this case, the rst
two vertices between a Begin and End pair de ne the rst segment, with
subsequent pairs of vertices each de ning one more segment. If the number
of speci ed vertices is odd, then the last one is ignored. The state required
is the same as for lines but it is used di erently: a vertex holding the rst
vertex of the current segment, and a boolean ag indicating whether the
current vertex is odd or even a segment start or end.
     Polygons. A polygon is described by specifying its boundary as a series
of line segments. When Begin is called with POLYGON, the bounding line
segments are speci ed in the same way as line loops. Depending on the
current state of the GL, a polygon may be rendered in one of several ways
such as outlining its border or lling its interior. A polygon described with
fewer than three vertices does not generate a primitive.
     Only convex polygons are guaranteed to be drawn correctly by the GL.
If a speci ed polygon is nonconvex when projected onto the window, then
the rendered polygon need only lie within the convex hull of the projected
vertices de ning its boundary.
     The state required to support polygons consists of at least two processed
vertices more than two are never required, although an implementation may
use more; this is because a convex polygon can be rasterized as its vertices
arrive, before all of them have been speci ed. The order of the vertices is sig-
ni cant in lighting and polygon rasterization see sections 2.13.1 and 3.5.1.
     Triangle strips. A triangle strip is a series of triangles connected along
shared edges. A triangle strip is speci ed by giving a series of de ning ver-
tices between a Begin End pair when Begin is called with TRIANGLE STRIP.
In this case, the rst three vertices de ne the rst triangle and their order is
signi cant, just as for polygons. Each subsequent vertex de nes a new tri-
angle using that point along with two vertices from the previous triangle. A
Begin End pair enclosing fewer than three vertices, when TRIANGLE STRIP
has been supplied to Begin, produces no primitive. See Figure 2.4.
     The state required to support triangle strips consists of a ag indicating
if the rst triangle has been completed, two stored processed vertices, called
vertex A and vertex B, and a one bit pointer indicating which stored vertex
will be replaced with the next vertex. After a BeginTRIANGLE STRIP,
the pointer is initialized to point to vertex A. Each vertex sent between a
Begin End pair toggles the pointer. Therefore, the rst vertex is stored as
vertex A, the second stored as vertex B, the third stored as vertex A, and
so on. Any vertex after the second one sent forms a triangle from vertex A,
vertex B, and the current vertex in that order.
     Triangle fans. A triangle fan is the same as a triangle strip with one




                     Version 1.2.1 - April 1, 1999
2.6. BEGIN END PARADIGM                                                               17


   2               4               2                        2
                                              3                                   6
                                                                    4
                                                  4

                                                      5                       5
   1           3          5        1                        1           3

            (a)                         (b)                             (c)

   Figure 2.4. a A triangle strip. b A triangle fan. c Independent triangles.
   The numbers give the sequencing of the vertices between Begin and End.
   Note that in a and b triangle edge ordering is determined by the rst
   triangle, while in c the order of each triangle's edges is independent of the
   other triangles.


exception: each vertex after the rst always replaces vertex B of the two
stored vertices. The vertices of a triangle fan are enclosed between Begin
and End when the value of the argument to Begin is TRIANGLE FAN.
    Separate Triangles. Separate triangles are speci ed by placing ver-
tices between Begin and End when the value of the argument to Begin
is TRIANGLES. In this case, The 3i + 1st, 3i + 2nd, and 3i + 3rd vertices in
that order determine a triangle for each i = 0; 1; : : : ; n , 1, where there are
3n + k vertices between the Begin and End. k is either 0, 1, or 2; if k is not
zero, the nal k vertices are ignored. For each triangle, vertex A is vertex
3i and vertex B is vertex 3i + 1. Otherwise, separate triangles are the same
as a triangle strip.
    The rules given for polygons also apply to each triangle generated from
a triangle strip, triangle fan or from separate triangles.
    Quadrilateral quad strips. Quad strips generate a series of edge-
sharing quadrilaterals from vertices appearing between Begin and End,
when Begin is called with QUAD STRIP. If the m vertices between the Begin
and End are v1 ; : : : ; vm , where vj is the j th speci ed vertex, then quad i has
vertices in order v2i , v2i+1 , v2i+3 , and v2i+2 with i = 0; : : : ; bm=2c. The
state required is thus three processed vertices, to store the last two vertices
of the previous quad along with the third vertex the rst new vertex of
the current quad, a ag to indicate when the rst quad has been completed,
and a one-bit counter to count members of a vertex pair. See Figure 2.5.




                                   Version 1.2.1 - April 1, 1999
18                                      CHAPTER 2. OPENGL OPERATION


             2         4         6              2      3     6     7




              1        3          5             1      4     5     8


                      (a)                                  (b)

     Figure 2.5. a A quad strip. b Independent quads. The numbers give the
     sequencing of the vertices between Begin and End.


    A quad strip with fewer than four vertices generates no primitive. If
the number of vertices speci ed for a quadrilateral strip between Begin and
End is odd, the nal vertex is ignored.
    Separate Quadrilaterals Separate quads are just like quad strips ex-
cept that each group of four vertices, the 4j +1st, the 4j +2nd, the 4j +3rd,
and the 4j + 4th, generate a single quad, for j = 0; 1; : : : ; n , 1. The total
number of vertices between Begin and End is 4n + k, where 0  k  3; if
k is not zero, the nal k vertices are ignored. Separate quads are generated
by calling Begin with the argument value QUADS.
    The rules given for polygons also apply to each quad generated in a quad
strip or from separate quads.
2.6.2 Polygon Edges
Each edge of each primitive generated from a polygon, triangle strip, trian-
gle fan, separate triangle set, quadrilateral strip, or separate quadrilateral
set, is agged as either boundary or non-boundary. These classi cations
are used during polygon rasterization; some modes a ect the interpreta-
tion of polygon boundary edges see section 3.5.4. By default, all edges are
boundary edges, but the agging of polygons, separate triangles, or separate
quadrilaterals may be altered by calling
      void EdgeFlag boolean ag ;
      void EdgeFlagv boolean * ag ;

to change the value of a ag bit. If ag is zero, then the ag bit is set to
FALSE; if ag is non-zero, then the ag bit is set to TRUE.




                       Version 1.2.1 - April 1, 1999
2.7. VERTEX SPECIFICATION                                                   19

    When Begin is supplied with one of the argument values POLYGON,
TRIANGLES  , or QUADS, each vertex speci ed within a Begin and End pair
begins an edge. If the edge ag bit is TRUE, then each speci ed vertex begins
an edge that is agged as boundary. If the bit is FALSE, then induced edges
are agged as non-boundary.
    The state required for edge agging consists of one current ag bit. Ini-
tially, the bit is TRUE. In addition, each processed vertex of an assembled
polygonal primitive must be augmented with a bit indicating whether or
not the edge beginning on that vertex is boundary or non-boundary.
2.6.3 GL Commands within Begin End
The only GL commands that are allowed within any Begin End pairs are
the commands for specifying vertex coordinates, vertex color, normal coor-
dinates, and texture coordinates Vertex, Color, Index, Normal, Tex-
Coord, the ArrayElement command see section 2.8, the EvalCoord
and EvalPoint commands see section 5.1, commands for specifying light-
ing material parameters Material commands; see section 2.13.2, display
list invocation commands CallList and CallLists; see section 5.4, and
the EdgeFlag command. Executing any other GL command between the
execution of Begin and the corresponding execution of End results in the
error INVALID OPERATION. Executing Begin after Begin has already been
executed but before an End is executed generates the INVALID OPERATION
error, as does executing End without a previous corresponding Begin.
    Execution of the commands EnableClientState, Dis-
ableClientState, PushClientAttrib, PopClientAttrib, EdgeFlag-
Pointer, TexCoordPointer, ColorPointer, IndexPointer, Normal-
Pointer, VertexPointer, InterleavedArrays, and PixelStore, is not
allowed within any Begin End pair, but an error may or may not be gen-
erated if such execution occurs. If an error is not generated, GL operation
is unde ned. These commands are described in sections 2.8, 3.6.1, and
Chapter 6.

2.7 Vertex Speci cation
Vertices are speci ed by giving their coordinates in two, three, or four dimen-
sions. This is done using one of several versions of the Vertex command:
     void   Vertexf234gfsifdg T coords ;
     void   Vertexf234gfsifdgv T coords ;




                                Version 1.2.1 - April 1, 1999
20                                   CHAPTER 2. OPENGL OPERATION

A call to any Vertex command speci es four coordinates: x, y, z , and w.
The x coordinate is the rst coordinate, y is second, z is third, and w is
fourth. A call to Vertex2 sets the x and y coordinates; the z coordinate is
implicitly set to zero and the w coordinate to one. Vertex3 sets x, y, and
z to the provided values and w to one. Vertex4 sets all four coordinates,
allowing the speci cation of an arbitrary point in projective three-space.
Invoking a Vertex command outside of a Begin End pair results in unde-
  ned behavior.
    Current values are used in associating auxiliary data with a vertex as
described in section 2.6. A current value may be changed at any time by
issuing an appropriate command. The commands
     void   TexCoordf1234gfsifdg T coords ;
     void   TexCoordf1234gfsifdgv T coords ;
specify the current homogeneous texture coordinates, named s, t, r, and q.
The TexCoord1 family of commands set the s coordinate to the provided
single argument while setting t and r to 0 and q to 1. Similarly, TexCoord2
sets s and t to the speci ed values, r to 0 and q to 1; TexCoord3 sets s, t,
and r, with q set to 1, and TexCoord4 sets all four texture coordinates.
    The current normal is set using
       void Normal3fbsifdg T coords ;
       void Normal3fbsifdgv T coords ;

Byte, short, or integer values passed to Normal are converted to oating-
point values as indicated for the corresponding signed type in Table 2.6.
    Finally, there are several ways to set the current color. The GL stores
both a current single-valued color index, and a current four-valued RGBA
color. One or the other of these is signi cant depending as the GL is in color
index mode or RGBA mode. The mode selection is made when the GL is
initialized.
    The command to set RGBA colors is
     void Colorf34gfbsifd ubusuig T components ;
     void Colorf34gfbsifd ubusuigv T components ;
The Color command has two major variants: Color3 and Color4. The
four value versions set all four values. The three value versions set R, G,
and B to the provided values; A is set to 1.0. The conversion of integer
color components R, G, B, and A to oating-point values is discussed in
section 2.13.




                    Version 1.2.1 - April 1, 1999
2.8. VERTEX ARRAYS                                                           21

    Versions of the Color command that take oating-point values accept
values nominally between 0.0 and 1.0. 0.0 corresponds to the minimum
while 1.0 corresponds to the maximum machine dependent value that a
component may take on in the framebu er see section 2.13 on colors and
coloring. Values outside 0; 1 are not clamped.
    The command
      void   Indexfsifd ubg T index ;
      void   Indexfsifd ubgv T index ;
updates the current single-valued color index. It takes one argument, the
value to which the current color index should be set. Values outside the
machine-dependent representable range of color indices are not clamped.
    The state required to support vertex speci cation consists of four
 oating-point numbers to store the current texture coordinates s, t, r, and
q, three oating-point numbers to store the three coordinates of the current
normal, four oating-point values to store the current RGBA color, and
one oating-point value to store the current color index. There is no notion
of a current vertex, so no state is devoted to vertex coordinates. The initial
values of s, t, and r of the current texture coordinates are zero; the initial
value of q is one. The initial current normal has coordinates 0; 0; 1. The
initial RGBA color is R; G; B; A = 1; 1; 1; 1. The initial color index is 1.

2.8 Vertex Arrays
The vertex speci cation commands described in section 2.7 accept data in
almost any format, but their use requires many command executions to spec-
ify even simple geometry. Vertex data may also be placed into arrays that
are stored in the client's address space. Blocks of data in these arrays may
then be used to specify multiple geometric primitives through the execution
of a single GL command. The client may specify up to six arrays: one each
to store edge ags, texture coordinates, colors, color indices, normals, and
vertices. The commands
      void   EdgeFlagPointer sizei stride, void *pointer ;
      void   TexCoordPointer int size, enum type, sizei stride,
         void   *pointer ;
      void   ColorPointer int size, enum type, sizei stride,
         void   *pointer ;




                                Version 1.2.1 - April 1, 1999
22                                    CHAPTER 2. OPENGL OPERATION

     Command                  Sizes
                             Types
     VertexPointer            2,3,4
                             short, int, float, double
     NormalPointer              3
                             byte, short, int, float, double
     ColorPointer              3,4
                             byte, ubyte, short, ushort, int,
                             uint, float, double
     IndexPointer       1    ubyte, short, int, float, double
     TexCoordPointer 1,2,3,4 short, int, float, double
     EdgeFlagPointer    1    boolean

     Table 2.4: Vertex array sizes values per vertex and data types.

      void  IndexPointer enum type, sizei stride,
         void   *pointer ;
      void  NormalPointer enum type, sizei stride,
         void   *pointer ;
      void  VertexPointer int size, enum type, sizei stride,
         void   *pointer ;
describe the locations and organizations of these arrays. For each com-
mand, type speci es the data type of the values stored in the array. Because
edge ags are always type boolean, EdgeFlagPointer has no type argu-
ment. size, when present, indicates the number of values per vertex that
are stored in the array. Because normals are always speci ed with three
values, NormalPointer has no size argument. Likewise, because color in-
dices and edge ags are always speci ed with a single value, IndexPointer
and EdgeFlagPointer also have no size argument. Table 2.4 indicates
the allowable values for size and type when present. For type the values
BYTE, SHORT, INT, FLOAT, and DOUBLE indicate types byte, short, int, float,
and double, respectively; and the values UNSIGNED BYTE, UNSIGNED SHORT, and
UNSIGNED INT indicate types ubyte, ushort, and uint, respectively. The er-
ror INVALID VALUE is generated if size is speci ed with a value other than
that indicated in the table.
    The one, two, three, or four values in an array that correspond to a single
vertex comprise an array element. The values within each array element are
stored sequentially in memory. If stride is speci ed as zero, then array
elements are stored sequentially as well. Otherwise pointers to the ith and
i + 1st elements of an array di er by stride basic machine units typically




                     Version 1.2.1 - April 1, 1999
2.8. VERTEX ARRAYS                                                          23

unsigned bytes, the pointer to the i + 1st element being greater. For each
command, pointer speci es the location in memory of the rst value of the
 rst element of the array being speci ed.
    An individual array is enabled or disabled by calling one of
     void   EnableClientState enum array ;
     void   DisableClientState enum array ;
with array set to EDGE FLAG ARRAY, TEXTURE COORD ARRAY, COLOR ARRAY,
            ,
INDEX ARRAY NORMAL ARRAY   , or VERTEX ARRAY, for the edge ag, texture coor-
dinate, color, color index, normal, or vertex array, respectively.
   The ith element of every enabled array is transferred to the GL by calling
     void   ArrayElement int i ;
For each enabled array, it is as though the corresponding command from sec-
tion 2.7 or section 2.6.2 were called with a pointer to element i. For the ver-
tex array, the corresponding command is Vertex size type v, where size is
one of 2,3,4 , and type is one of s,i,f,d , corresponding to array types short,
int, float, and double respectively. The corresponding commands for
the edge ag, texture coordinate, color, color index, and normal arrays are
EdgeFlagv, TexCoord size type v, Color size type v, Index type v,
and Normal type v, respectively. If the vertex array is enabled, it is as
though Vertex size type v is executed last, after the executions of the
other corresponding commands.
    Changes made to array data between the execution of Begin and the
corresponding execution of End may a ect calls to ArrayElement that are
made within the same Begin End period in non-sequential ways. That is,
a call to ArrayElement that precedes a change to array data may access
the changed data, and a call that follows a change to array data may access
original data.
    The command
     void   DrawArrays enum mode, int rst, sizei count ;
constructs a sequence of geometric primitives using elements first through
first+count,1 of each enabled array. mode speci es what kind of primitives
are constructed; it accepts the same token values as the mode parameter of
the Begin command. The e ect of
          DrawArrays mode; first; count;




                                Version 1.2.1 - April 1, 1999
24                                    CHAPTER 2. OPENGL OPERATION

is the same as the e ect of the command sequence
          if mode or count is invalid 
             generate appropriate error
          else   f
             int i;
              Begin mode
                       ;
             for i=0; i         count ;   i++
                ArrayElementfirst+ i;
              End;
          g
with one exception: the current edge ag, texture coordinates, color, color
index, and normal coordinates are each indeterminate after the execution of
DrawArrays, if the corresponding array is enabled. Current values corre-
sponding to disabled arrays are not modi ed by the execution of DrawAr-
rays.
   The command
     void     DrawElements enum mode, sizei count, enum type,
        void    *indices ;
constructs a sequence of geometric primitives using the count elements
whose indices are stored in indices. type must be one of UNSIGNED BYTE,
UNSIGNED SHORT, or UNSIGNED INT, indicating that the values in indices are
indices of GL type ubyte, ushort, or uint respectively. mode speci es
what kind of primitives are constructed; it accepts the same token values as
the mode parameter of the Begin command. The e ect of
          DrawElements mode; count; type; indices;
is the same as the e ect of the command sequence
          if   mode; count; or type is invalid 
              generate appropriate error
          else   f
             int i;
              Begin mode
                       ;
             for i=0; i         count ;   i++
                ArrayElementindices i ;
              End;
          g




                     Version 1.2.1 - April 1, 1999
2.8. VERTEX ARRAYS                                                          25

with one exception: the current edge ag, texture coordinates, color, color
index, and normal coordinates are each indeterminate after the execution
of DrawElements, if the corresponding array is enabled. Current val-
ues corresponding to disabled arrays are not modi ed by the execution of
DrawElements.
   The command
     void   DrawRangeElements enum mode, uint start,
        uint   end, sizei count, enum type, void *indices ;
is a restricted form of DrawElements. mode, count, type, and indices
match the corresponding arguments to DrawElements, with the additional
constraint that all values in the array indices must lie between start and end
inclusive.
    Implementations denote recommended maximum amounts of vertex and
index data, which may be queried by calling GetIntegerv with the symbolic
constants MAX ELEMENTS VERTICES and MAX ELEMENTS INDICES. If end,start+1
is greater than the value of MAX ELEMENTS VERTICES, or if count is greater than
the value of MAX ELEMENTS INDICES, then the call may operate at reduced per-
formance. There is no requirement that all vertices in the range start; end
be referenced. However, the implementation may partially process unused
vertices, reducing performance from what could be achieved with an optimal
index set.
    The error INVALID VALUE is generated if end start. Invalid mode, count,
or type parameters generate the same errors as would the corresponding
call to DrawElements. It is an error for indices to lie outside the range
 start; end , but implementations may not check for this. Such indices will
cause implementation-dependent behavior.
    The command
     void   InterleavedArrays enum format, sizei stride,
        void   *pointer ;
e ciently initializes the six arrays and their enables to one of 14 con gura-
tions. format must be one of 14 symbolic constants: V2F, V3F, C4UB V2F,
C4UB V3F, C3F V3F, N3F V3F, C4F N3F V3F, T2F V3F, T4F V4F, T2F C4UB V3F,
T2F C3F V3F, T2F N3F V3F, T2F C4F N3F V3F, or T4F C4F N3F V4F.
    The e ect of
          InterleavedArraysformat; stride; pointer;
   is the same as the e ect of the command sequence




                                Version 1.2.1 - April 1, 1999
26                                          CHAPTER 2. OPENGL OPERATION


 format              et          ec          en      st sc sv             tc
 V2F               False        False       False                2
 V3F               False        False       False                3
 C4UB V2F          False        True        False            4   2   UNSIGNED BYTE
 C4UB V3F          False        True        False            4   3   UNSIGNED BYTE
 C3F V3F           False        True        False            3   3      FLOAT
 N3F V3F           False        False       True                 3
 C4F N3F V3F       False        True        True             4   3      FLOAT
 T2F V3F           True         False       False        2       3
 T4F V4F           True         False       False        4       4
 T2F C4UB V3F      True         True        False        2   4   3   UNSIGNED BYTE
 T2F C3F V3F       True         True        False        2   3   3      FLOAT
 T2F N3F V3F       True         False       True         2       3
 T2F C4F N3F V3F   True         True        True         2   4   3      FLOAT
 T4F C4F N3F V4F   True         True        True         4   4   4      FLOAT

 format            pc pn              pv             s
 V2F                                    0           2f
 V3F                                    0           3f
 C4UB V2F           0                  c c + 2f
 C4UB V3F           0                  c c + 3f
 C3F V3F            0                 3f    6f
 N3F V3F                    0         3f    6f
 C4F N3F V3F        0      4f         7f   10f
 T2F V3F                              2f    5f
 T4F V4F                              4f    8f
 T2F C4UB V3F      2f             c + 2f c + 5f
 T2F C3F V3F       2f                5f     8f
 T2F N3F V3F          2f             5f     8f
 T2F C4F N3F V3F   2f 6f             9f    12f
 T4F C4F N3F V4F   4f 8f            11f    15f
Table 2.5: Variables that direct the execution of InterleavedArrays. f
is sizeofFLOAT. c is 4 times sizeofUNSIGNED BYTE, rounded up to
the nearest multiple of f . All pointer arithmetic is performed in units of
sizeofUNSIGNED BYTE.




                    Version 1.2.1 - April 1, 1999
2.8. VERTEX ARRAYS                                                                       27

          if   format or stride is invalid
              generate appropriate error
          else   f
             int str;
              set et ; ec ; en ; st ; sc; sv ; tc ; pc ; pn ; pv ; and s as a function
                 of Table 2.5 and the value of format.
              str = stride;
              if str is zero
                 str = s;
              DisableClientStateEDGE FLAG ARRAY;
              DisableClientStateINDEX ARRAY;
                  e f
              if  t 
                 EnableClientStateTEXTURE COORD ARRAY;
                 TexCoordPointerst , FLOAT, str, pointer;
              g else f
                 DisableClientStateTEXTURE COORD ARRAY;
              g
              if ec  f
                 EnableClientStateCOLOR ARRAY;
                 ColorPointersc, tc, str, pointer + pc;
              g else f
                 DisableClientStateCOLOR ARRAY;
              g
              if en  f
                 EnableClientStateNORMAL ARRAY;
                 NormalPointerFLOAT, str, pointer + pn;
              g else f
                 DisableClientStateNORMAL ARRAY;
              g
              EnableClientStateVERTEX ARRAY;
              VertexPointersv , FLOAT, str, pointer + pv ;
          g

   The client state required to implement vertex arrays consists of six
boolean values, six memory pointers, six integer stride values, ve symbolic
constants representing array types, and three integers representing values
per element. In the initial state the boolean values are each disabled, the
memory pointers are each null, the strides are each zero, the array types are
each FLOAT, and the integers representing values per element are each four.




                                      Version 1.2.1 - April 1, 1999
28                                    CHAPTER 2. OPENGL OPERATION

2.9 Rectangles
There is a set of GL commands to support e cient speci cation of rectangles
as two corner vertices.
     void   Rectfsifdg T x1, T y1, T x2, T y2 ;
     void   Rectfsifdgv T v1 2 , T v2 2 ;
Each command takes either four arguments organized as two consecutive
pairs of x; y coordinates, or two pointers to arrays each of which contains
an x value followed by a y value. The e ect of the Rect command
          Rect x1; y1; x2 ; y2 ;
is exactly the same as the following sequence of commands:
         BeginPOLYGON;
            Vertex2x1 ; y1;
            Vertex2x2 ; y1;
            Vertex2x2 ; y2;
            Vertex2x1 ; y2;
         End;
The appropriate Vertex2 command would be invoked depending on which
of the Rect commands is issued.

2.10 Coordinate Transformations
Vertices, normals, and texture coordinates are transformed before their
coordinates are used to produce an image in the framebu er. We begin
with a description of how vertex coordinates are transformed and how this
transformation is controlled.
    Figure 2.6 diagrams the sequence of transformations that are applied to
vertices. The vertex coordinates that are presented to the GL are termed
object coordinates. The model-view matrix is applied to these coordinates to
yield eye coordinates. Then another matrix, called the projection matrix, is
applied to eye coordinates to yield clip coordinates. A perspective division
is carried out on clip coordinates to yield normalized device coordinates. A
  nal viewport transformation is applied to convert these coordinates into
window coordinates.




                     Version 1.2.1 - April 1, 1999
2.10. COORDINATE TRANSFORMATIONS                                                                         29


                                                                                           Normalized
     Object      Model−View      Eye          Projection         Clip      Perspective       Device
   Coordinates                Coordinates                   Coordinates     Division       Coordinates
                  Matrix                        Matrix




                                                                             Viewport        Window
                                                                          Transformation
                                                                                           Coordinates




  Figure 2.6. Vertex transformation sequence.


   Object coordinates, eye coordinates, and clip coordinates are four-
dimensional, consisting of x, y, z , and w coordinates in that order. The
model-view and perspective matrices are thus 4 0 4. 1
                                                                          xo
                                                 B yo CC and the model-view
   If a vertex in object coordinates is given by B
                                                 @ zo A
                                                                          wo
matrix is M , then the vertex's eye coordinates are found as
                                    0 xe 1        0 xo 1
                                    BB ye CC = M BB yo CC :
                                     @ A
                                       ze         @ A       zo
                                       we                   wo
Similarly, if P is the projection matrix, then the vertex's clip coordinates
are                         0 1 0 1     xc                  xe
                                    BB yc CC = P BB ye CC :
                                     @ zc A @ ze A
                                       wc                  we
The vertex's normalized device coordinates are then
                                   0 xd 1 0 xc=wc 1
                                   @ yd A = @ yc=wc A :
                                       zd                zc =wc




                                            Version 1.2.1 - April 1, 1999
30                                    CHAPTER 2. OPENGL OPERATION

2.10.1 Controlling the Viewport
The viewport transformation is determined by the viewport's width and
height in pixels, px and py , respectively, 0and 1its center ox ; oy  also in
                                                     xw
pixels. The vertex's window coordinates, @ yw A, are given by
                                                     zw
                  0 xw 1 0           px =2xd + ox       1
                  @ yw A = @         py =2yd + oy       A:
                     zw         f , n=2 zd + n + f =2
The factor and o set applied to zd encoded by n and f are set using
      void   DepthRange clampd n, clampd f ;
Each of n and f are clamped to lie within 0; 1 , as are all arguments of type
clampd or clampf. zw is taken to be represented in xed-point with at least
as many bits as there are in the depth bu er of the framebu er. We assume
that the xed-point representation used represents each value k=2m , 1,
where k 2 f0; 1; : : : ; 2m , 1g, as k e.g. 1.0 is represented in binary as a
string of all ones.
    Viewport transformation parameters are speci ed using
      void   Viewport int x, int y, sizei w, sizei h ;
where x and y give the x and y window coordinates of the viewport's lower-
left corner and w and h give the viewport's width and height, respectively.
The viewport parameters shown in the above equations are found from these
values as ox = x + w=2 and oy = y + h=2; px = w, py = h.
    Viewport width and height are clamped to implementation-dependent
maximums when speci ed. The maximum width and height may be found
by issuing an appropriate Get command see Chapter 6. The maximum
viewport dimensions must be greater than or equal to the visible dimensions
of the display being rendered to. INVALID VALUE is generated if either w or h
is negative.
    The state required to implement the viewport transformation is 6 inte-
gers. In the initial state, w and h are set to the width and height, respectively,
of the window into which the GL is to do its rendering. ox and oy are set to
w=2 and h=2, respectively. n and f are set to 0:0 and 1:0, respectively.




                     Version 1.2.1 - April 1, 1999
2.10. COORDINATE TRANSFORMATIONS                                          31

2.10.2 Matrices
The projection matrix and model-view matrix are set and modi ed with
a variety of commands. The a ected matrix is determined by the current
matrix mode. The current matrix mode is set with
     void   MatrixMode enum mode ;
which takes one of the pre-de ned constants TEXTURE, MODELVIEW, COLOR,
or PROJECTION as the argument value. TEXTURE is described later in sec-
tion 2.10.2, and COLORis described in section 3.6.3. If the current matrix
mode is MODELVIEW, then matrix operations apply to the model-view matrix;
if PROJECTION, then they apply to the projection matrix.
    The two basic commands for a ecting the current matrix are
     void   LoadMatrixffdg T m 16 ;
     void   MultMatrixffdg T m 16 ;
LoadMatrix takes a pointer to a 4  4 matrix stored in column-major order
as 16 consecutive oating-point values, i.e. as
                          0 a1 a5 a9 a13 1
                          BB a2 a6 a10 a14 CC :
                           @ a3 a7 a11 a15 A
                             a4 a8 a12 a16
This di ers from the standard row-major C ordering for matrix elements. If
the standard ordering is used, all of the subsequent transformation equations
are transposed, and the columns representing vectors become rows.
    The speci ed matrix replaces the current matrix with the one pointed to.
MultMatrix takes the same type argument as LoadMatrix, but multiplies
the current matrix by the one pointed to and replaces the current matrix
with the product. If C is the current matrix and M is the matrix pointed
to by MultMatrix's argument, then the resulting current matrix, C 0 , is
                                C 0 = C  M:
   The command
     void   LoadIdentity void ;




                               Version 1.2.1 - April 1, 1999
32                                    CHAPTER 2. OPENGL OPERATION

e ectively calls LoadMatrix with the identity matrix:
                              01 0 0 01
                              BB 0 1 0 0 CC :
                               @0 0 1 0A
                                 0 0 0 1
    There are a variety of other commands that manipulate matrices. Ro-
tate, Translate, Scale, Frustum, and Ortho manipulate the current ma-
trix. Each computes a matrix and then invokes MultMatrix with this
matrix. In the case of
      void   Rotateffdg T , T x, T y, T z ;
 gives an angle of rotation in degrees; the coordinates of a vector v are given
by v = x y z T . The computed matrix is a counter-clockwise rotation about
the line through the origin with the speci ed axis when that axis is pointing
up i.e. the right-hand rule determines the sense of the rotation angle. The
matrix is thus
                              0            01
                              BB R         0CC
                               @           0A:
                                 0 0 0 1
Let u = v=jjvjj =  x0 y0 z 0 T . If
                                0 0 ,z 0 y 0 1
                          S = @ z0 0 ,x0 A
                                  ,y0 x0 0
then
                     R = uuT + cos I , uuT  + sin S:
    The arguments to
      void   Translateffdg T x, T y, T z ;
give the coordinates of a translation vector as x y z T . The resulting matrix
is a translation by the speci ed vector:
                              01 0 0 x1
                              BB 0 1 0 y CC :
                               @0 0 1 z A
                                 0 0 0 1




                     Version 1.2.1 - April 1, 1999
2.10. COORDINATE TRANSFORMATIONS                                               33

      void   Scaleffdg T x, T y, T z ;
produces a general scaling along the x-, y-, and z - axes. The corresponding
matrix is                    0x 0 0 01
                             BB 0 y 0 0 CC :
                              @0 0 z 0A
                                0 0 0 1
   For
      void   Frustum double l, double r, double b, double t,
         double n, double f ;

the coordinates l b , nT and r t , nT specify the points on the near
clipping plane that are mapped to the lower-left and upper-right corners of
the window, respectively assuming that the eye is located at 0 0 0T . f
gives the distance from the eye to the far clipping plane. If either n or f is
less than or equal to zero, l is equal to r, b is equal to t, or n is equal to f ,
the error INVALID VALUE results. The corresponding matrix is
                       0 2n 0 r+l                 0 1
                          r ,l          r,l
                       BB 0 t2,nb tt+,bb               C
                        B@ 0 0 , f +n , 20fn CCA :
                                         f ,n     f ,n
                           0 0          ,1        0
      void   Ortho
                  double l, double r, double b, double t,
         double n, double f ;

describes a matrix that produces parallel projection. l b ,nT and r t ,nT
specify the points on the near clipping plane that are mapped to the lower-
left and upper-right corners of the window, respectively. f gives the distance
from the eye to the far clipping plane. If l is equal to r, b is equal to t, or n
is equal to f , the error INVALID VALUE results. The corresponding matrix is
                         0 2 0          0      , rr+,ll 1
                            r ,l
                         BB 0 t,2 b 0 , tt+,bb CC
                          B@ 0 0 , 2 , f +n CA :
                                        f ,n     f ,n
                             0 0        0        1
    There is another 4  4 matrix that is applied to texture coordinates. This
matrix is applied as




                                 Version 1.2.1 - April 1, 1999
34                                             CHAPTER 2. OPENGL OPERATION

                      0 m1 m5 m9 m13 1 0 s 1
                      B
                      B m m m m CB t C
                      @ m23 m67 m1011 m1415 CA B@ r CA ;
                         m4 m8 m12 m16               q
where the left matrix is the current texture matrix. The matrix is applied
to the coordinates resulting from texture coordinate generation which may
simply be the current texture coordinates, and the resulting transformed co-
ordinates become the texture coordinates associated with a vertex. Setting
the matrix mode to TEXTURE causes the already described matrix operations
to apply to the texture matrix.
    There is a stack of matrices for each of the matrix modes. For MODELVIEW
mode, the stack depth is at least 32 that is, there is a stack of at least 32
model-view matrices. For the other modes, the depth is at least 2. The
current matrix in any mode is the matrix on the top of the stack for that
mode.
      void PushMatrix void ;

pushes the stack down by one, duplicating the current matrix in both the
top of the stack and the entry below it.
      void PopMatrix void ;

pops the top entry o of the stack, replacing the current matrix with the
matrix that was the second entry in the stack. The pushing or popping takes
place on the stack corresponding to the current matrix mode. Popping a
matrix o a stack with only one entry generates the error STACK UNDERFLOW;
pushing a matrix onto a full stack generates STACK OVERFLOW.
    The state required to implement transformations consists of a four-
valued integer indicating the current matrix mode, a stack of at least two
4  4 matrices for each of COLOR, PROJECTION, and TEXTURE with associated
stack pointers, and a stack of at least 32 4  4 matrices with an associated
stack pointer for MODELVIEW. Initially, there is only one matrix on each stack,
and all matrices are set to the identity. The initial matrix mode is MODELVIEW.
2.10.3 Normal Transformation
Finally, we consider how the model-view matrix and transformation state
a ect normals. Before use in lighting, normals are transformed to eye co-
ordinates by a matrix derived from the model-view matrix. Rescaling and
normalization operations are performed on the transformed normals to make




                     Version 1.2.1 - April 1, 1999
2.10. COORDINATE TRANSFORMATIONS                                          35

them unit length prior to use in lighting. Rescaling and normalization are
controlled by
      void   Enable enum target ;
and
      void   Disable enum target ;
with target equal to RESCALE NORMAL or NORMALIZE. This requires two bits of
state. The initial state is for normals not to be rescaled or normalized.
    If the model-view matrix is M , then the normal is transformed to eye
coordinates by:
                  nx 0 ny 0 nz 0 q0  =  nx ny nz q   M ,1
          0x1
          B y CC are the associated vertex coordinates, then
where, if B
          @ Az
             w          8
                            0;       0 x 1 w = 0;
                    q = , nx ny nz @ y A                              2.1
                       :               z ; w=6 0
                                w
   Implementations may choose instead to transform  nx ny nz  to eye
coordinates using
                 nx0 ny 0 nz 0  =  nx ny nz   Mu ,1
where Mu is the upper leftmost 3x3 matrix taken from M .
   Rescale multiplies the transformed normals by a scale factor
                     nx 00 ny 00 nz 00  = f  nx0 ny 0 nz 0 
If rescaling is disabled, then f = 1. If rescaling is enabled, then f is com-
puted as mij denotes the matrix element in row i and column j of M ,1 ,
numbering the topmost row of the matrix as row 1 and the leftmost column
as column 1
                           f=p 2 1 2
                                  m31 + m32 + m33 2




                                 Version 1.2.1 - April 1, 1999
36                                   CHAPTER 2. OPENGL OPERATION

    Note that if the normals sent to GL were unit length and the model-view
matrix uniformly scales space, then rescale makes the transformed normals
unit length.
    Alternatively, an implementation may chose f as
                          f=q 2 1 2
                                 nx0 + ny 0 + nz 0 2
recomputing f for each normal. This makes all non-zero length normals
unit length regardless of their input length and the nature of the model-
view matrix.
    After rescaling, the nal transformed normal used in lighting, nf , is
computed as
                         nf = m  nx00 ny 00 nz 00 

If normalization is disabled, then m = 1. Otherwise
                         m= q 2 1 2
                                 nx00 + ny 00 + nz 002
    Because we specify neither the oating-point format nor the means
for matrix inversion, we cannot specify behavior in the case of a poorly-
conditioned nearly singular model-view matrix M . In case of an exactly
singular matrix, the transformed normal is unde ned. If the GL implementa-
tion determines that the model-view matrix is uninvertible, then the entries
in the inverted matrix are arbitrary. In any case, neither normal transfor-
mation nor use of the transformed normal may lead to GL interruption or
termination.
2.10.4 Generating Texture Coordinates
Texture coordinates associated with a vertex may either be taken from the
current texture coordinates or generated according to a function dependent
on vertex coordinates. The command
     void   TexGenfifdg enum coord, enum pname, T param ;
     void   TexGenfifdgv enum coord, enum pname, T params ;
controls texture coordinate generation. coord must be one of the constants
S, T, R, or Q, indicating that the pertinent coordinate is the s, t, r , or q




                    Version 1.2.1 - April 1, 1999
2.10. COORDINATE TRANSFORMATIONS                                                37

coordinate, respectively. In the rst form of the command, param is a sym-
bolic constant specifying a single-valued texture generation parameter; in the
second form, params is a pointer to an array of values that specify texture
generation parameters. pname must be one of the three symbolic constants
TEXTURE GEN MODE, OBJECT PLANE, or EYE PLANE. If pname is TEXTURE GEN MODE,
then either params points to or param is an integer that is one of the symbolic
constants OBJECT LINEAR, EYE LINEAR, or SPHERE MAP.
    If TEXTURE GEN MODE indicates OBJECT LINEAR, then the generation function
for the coordinate indicated by coord is
                        g = p1xo + p2 yo + p3 zo + p4 wo :
xo , yo, zo , and wo are the object coordinates of the vertex. p1 ; : : : ; p4 are
speci ed by calling TexGen with pname set to OBJECT PLANE in which case
params points to an array containing p1 ; : : : ; p4 . There is a distinct group of
plane equation coe cients for each texture coordinate; coord indicates the
coordinate to which the speci ed coe cients pertain.
   If TEXTURE GEN MODE indicates EYE LINEAR, then the function is
                        g = p01 xe + p02 ye + p03 ze + p04 we
where
                 p01 p02 p03 p04  =  p1 p2 p3 p4  M ,1
xe , ye, ze, and we are the eye coordinates of the vertex. p1 ; : : : ; p4 are
set by calling TexGen with pname set to EYE PLANE in correspondence with
setting the coe cients in the OBJECT PLANE case. M is the model-view matrix
in e ect when p1 ; : : : ; p4 are speci ed. Computed texture coordinates may
be inaccurate or unde ned if M is poorly conditioned or singular.
     When used with a suitably constructed texture image, calling TexGen
with TEXTURE GEN MODE indicating SPHERE MAP can simulate the re ected im-
age of a spherical environment on a polygon. SPHERE MAP texture coordinates
are generated as follows. Denote the unit vector pointing from the origin to
the vertex in eye coordinates by u. Denote the current normal, after trans-
formation to eye coordinates, by n0 . Let r =  rx ry rz T , the re ection
vector, be given by
                                 r = u , 2n0 T ,n0 u ;
               q
and let m = 2 rx2 + ry2 + rz + 12 . Then the value assigned to an s coor-
dinate the rst TexGen argument value is S is s = rx =m + 12 ; the value




                                  Version 1.2.1 - April 1, 1999
38                                    CHAPTER 2. OPENGL OPERATION

assigned to a t coordinate is t = ry =m + 21 . Calling TexGen with a co-
ord of either R or Q when pname indicates SPHERE MAP generates the error
INVALID ENUM.
    A texture coordinate generation function is enabled or disabled using
Enable and Disable with an argument of TEXTURE GEN S, TEXTURE GEN T,
TEXTURE GEN R, or TEXTURE GEN Q each indicates the corresponding texture
coordinate. When enabled, the speci ed texture coordinate is computed
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
initial values of pi for s are all 0 except p1 which is one; for t all the pi are
zero except p2 , which is 1. The values of pi for r and q are all 0. These values
of pi apply for both the EYE LINEAR and OBJECT LINEAR versions. Initially all
texture generation modes are EYE LINEAR.

2.11 Clipping
Primitives are clipped to the clip volume. In clip coordinates, the view
volume is de ned by
                                ,wc  xc  wc
                                ,wc  yc  wc :
                                ,wc  zc  wc
This view volume may be further restricted by as many as n client-de ned
clip planes to generate the clip volume. n is an implementation dependent
maximum that must be at least 6. Each client-de ned plane speci es a
half-space. The clip volume is the intersection of all such half-spaces with
the view volume if there no client-de ned clip planes are enabled, the clip
volume is the view volume.
    A client-de ned clip plane is speci ed with

      void   ClipPlane enum p, double eqn 4 ;




                     Version 1.2.1 - April 1, 1999
2.11. CLIPPING                                                                39

The value of the rst argument, p, is a symbolic constant, CLIP PLANEi, where
i is an integer between 0 and n , 1, indicating one of n client-de ned clip
planes. eqn is an array of four double-precision oating-point values. These
are the coe cients of a plane equation in object coordinates: p1 , p2 , p3 , and
p4 in that order. The inverse of the current model-view matrix is applied
to these coe cients, at the time they are speci ed, yielding
                 p01 p02 p03 p04  =  p1 p2 p3 p4  M ,1
where M is the current model-view matrix; the resulting plane equation is
unde ned if M is singular and may be inaccurate if M is poorly-conditioned
to obtain the plane equation coe cients in eye coordinates. All points with
eye coordinates  xe ye ze we T that satisfy
                                            0 xe 1
                                            B ye CC  0
                         p01 p02 p03 p04  B
                                            @ ze A
                                               we
lie in the half-space de ned by the plane; points that do not satisfy this
condition do not lie in the half-space.
    Client-de ned clip planes are enabled with the generic Enable com-
mand and disabled with the Disable command. The value of the argument
to either command is CLIP PLANEi where i is an integer between 0 and n;
specifying a value of i enables or disables the plane equation with index i.
The constants obey CLIP PLANEi = CLIP PLANE0 + i.
    If the primitive under consideration is a point, then clipping passes it
unchanged if it lies within the clip volume; otherwise, it is discarded. If the
primitive is a line segment, then clipping does nothing to it if it lies entirely
within the clip volume and discards it if it lies entirely outside the volume.
If part of the line segment lies in the volume and part lies outside, then the
line segment is clipped and new vertex coordinates are computed for one or
both vertices. A clipped line segment endpoint lies on both the original line
segment and the boundary of the clip volume.
    This clipping produces a value, 0  t  1, for each clipped vertex. If the
coordinates of a clipped vertex are P and the original vertices' coordinates
are P1 and P2 , then t is given by
                             P = tP1 + 1 , tP2 :
The value of t is used in color and texture coordinate clipping sec-
tion 2.13.8.




                                 Version 1.2.1 - April 1, 1999
40                                    CHAPTER 2. OPENGL OPERATION

     If the primitive is a polygon, then it is passed if every one of its edges
lies entirely inside the clip volume and either clipped or discarded otherwise.
Polygon clipping may cause polygon edges to be clipped, but because poly-
gon connectivity must be maintained, these clipped edges are connected by
new edges that lie along the clip volume's boundary. Thus, clipping may
require the introduction of new vertices into a polygon. Edge ags are asso-
ciated with these vertices so that edges introduced by clipping are agged
as boundary edge ag TRUE, and so that original edges of the polygon that
become cut o at these vertices retain their original ags.
     If it happens that a polygon intersects an edge of the clip volume's
boundary, then the clipped polygon must include a point on this boundary
edge. This point must lie in the intersection of the boundary edge and
the convex hull of the vertices of the original polygon. We impose this
requirement because the polygon may not be exactly planar.
     A line segment or polygon whose vertices have wc values of di ering signs
may generate multiple connected components after clipping. GL implemen-
tations are not required to handle this situation. That is, only the portion of
the primitive that lies in the region of wc 0 need be produced by clipping.
     Primitives rendered with clip planes must satisfy a complementarity cri-
terion. Suppose a single clip plane with coe cients  p01 p02 p03 p04  or a
number of similarly speci ed clip planes is enabled and a series of primitives
are drawn. Next, suppose that the original clip plane is respeci ed with co-
e cients  ,p01 ,p02 ,p03 ,p04  and correspondingly for any other clip
planes and the primitives are drawn again and the GL is otherwise in the
same state. In this case, primitives must not be missing any pixels, nor
may any pixels be drawn twice in regions where those primitives are cut by
the clip planes.
     The state required for clipping is at least 6 sets of plane equations each
consisting of four double-precision oating-point coe cients and at least 6
corresponding bits indicating which of these client-de ned plane equations
are enabled. In the initial state, all client-de ned plane equation coe cients
are zero and all planes are disabled.

2.12 Current Raster Position
The current raster position is used by commands that directly a ect pixels in
the framebu er. These commands, which bypass vertex transformation and
primitive assembly, are described in the next chapter. The current raster
position, however, shares some of the characteristics of a vertex.




                     Version 1.2.1 - April 1, 1999
2.13. COLORS AND COLORING                                                   41

    The state required for the current raster position consists of three window
coordinates xw , yw , and zw , a clip coordinate wc value, an eye coordinate
distance, a valid bit, and associated data consisting of a color and texture
coordinates. It is set using one of the RasterPos commands:


     void   RasterPosf234gfsifdg T coords ;
     void   RasterPosf234gfsifdgv T coords ;

RasterPos4 takes four values indicating x, y, z, and w. RasterPos3 or
RasterPos2 is analogous, but sets only x, y, and z with w implicitly set
to 1 or only x and y with z implicitly set to 0 and w implicitly set to 1.
    The coordinates are treated as if they were speci ed in a Vertex com-
mand. The x, y, z , and w coordinates are transformed by the current
model-view and perspective matrices. These coordinates, along with cur-
rent values, are used to generate a color and texture coordinates just as is
done for a vertex. The color and texture coordinates so produced replace
the color and texture coordinates stored in the current raster position's as-
sociated data. The distance from the origin of the eye coordinate system
to the vertex as transformed by only the current model-view matrix re-
places the current raster distance. This distance can be approximated see
section 3.10.
    The transformed coordinates are passed to clipping as if they represented
a point. If the point" is not culled, then the projection to window coor-
dinates is computed section 2.10 and saved as the current raster position,
and the valid bit is set. If the point" is culled, the current raster position
and its associated data become indeterminate and the valid bit is cleared.
Figure 2.7 summarizes the behavior of the current raster position.
    The current raster position requires ve single-precision oating-point
values for its xw , yw , and zw window coordinates, its wc clip coordinate,
and its eye coordinate distance, a single valid bit, a color RGBA and color
index, and texture coordinates for associated data. In the initial state, the
coordinates and texture coordinates are both 0; 0; 0; 1, the eye coordinate
distance is 0, the valid bit is set, the associated RGBA color is 1; 1; 1; 1
and the associated color index color is 1. In RGBA mode, the associated
color index always has its initial value; in color index mode, the RGBA color
always maintains its initial value.




                                Version 1.2.1 - April 1, 1999
42                                             CHAPTER 2. OPENGL OPERATION



                                                                            Valid
       Rasterpos In                    Clip            Project
                                                                              Raster
                               Vertex/Normal                                 Position
         Current               Transformation
         Normal

                                                                              Raster
        Current                             Lighting                         Distance
        Color &
        Materials
                                                                            Associated
                                                          Texture              Data
         Current                   Texgen                  Matrix
         Texture                                                                         Current
       Coordinates                                                                        Raster
                                                                                         Position



     Figure 2.7. The current raster position and how it is set.




                      Convert to
       [0,2k−1]
                       [0.0,1.0]               Current
                                               RGBA                                     Clamp to
                                                Color            Lighting               [0.0, 1.0]
                      Convert to
     [−2k,2k−1]
                      [−1.0,1.0]
          float
                                                           Color
                                                          Clipping


                                Convert to                                     Flatshade?
                               fixed−point
                                                          Primitive
                                                          Clipping



     Figure 2.8. Processing of RGBA colors. The heavy dotted lines indicate
     both primary and secondary vertex colors, which are processed in the same
     fashion. See Table 2.6 for the interpretation of k.




                          Version 1.2.1 - April 1, 1999
2.13. COLORS AND COLORING                                                              43


                Convert to
   [0,2n−1]                       Current
                  float
                                   Color                                 Mask to
      float                        Index        Lighting                 [0.0, 2n−1]



                                             Color
                                            Clipping


                     Convert to                                   Flatshade?
                    fixed−point
                                            Primitive
                                            Clipping


  Figure 2.9. Processing of color indices. n is the number of bits in a color
  index.



2.13 Colors and Coloring
Figures 2.8 and 2.9 diagram the processing of RGBA colors and color in-
dices before rasterization. Incoming colors arrive in one of several formats.
Table 2.6 summarizes the conversions that take place on R, G, B, and A com-
ponents depending on which version of the Color command was invoked to
specify the components. As a result of limited precision, some converted
values will not be represented exactly. In color index mode, a single-valued
color index is not mapped.
    Next, lighting, if enabled, produces either a color index or primary and
secondary colors. If lighting is disabled, the current color index or color
is used in further processing the current color is the primary color, and
the secondary color is 0; 0; 0; 0. After lighting, RGBA colors are clamped
to the range 0; 1 . A color index is converted to xed-point and then its
integer portion is masked see section 2.13.6. After clamping or masking,
a primitive may be atshaded, indicating that all vertices of the primitive
are to have the same color. Finally, if a primitive is clipped, then colors
and texture coordinates must be computed at the vertices introduced or
modi ed by clipping.




                                  Version 1.2.1 - April 1, 1999
44                                     CHAPTER 2. OPENGL OPERATION

                         GL Type     Conversion
                         ubyte        c=28 , 1
                         byte     2c + 1=28 , 1
                         ushort      c=216 , 1
                         short   2c + 1=216 , 1
                         uint        c=232 , 1
                         int     2c + 1=232 , 1
                           oat            c
                         double           c
Table 2.6: Component conversions. Color, normal, and depth components,
c, are converted to an internal oating-point representation, f , using the
equations in this table. All arithmetic is done in the internal oating point
format. These conversions apply to components speci ed as parameters to
GL commands and to components in pixel data. The equations remain the
same even if the implemented ranges of the GL data types are greater than
the minimum required ranges. Refer to table 2.2


2.13.1 Lighting
GL lighting computes colors for each vertex sent to the GL. This is accom-
plished by applying an equation de ned by a client-speci ed lighting model
to a collection of parameters that can include the vertex coordinates, the
coordinates of one or more light sources, the current normal, and parameters
de ning the characteristics of the light sources and a current material. The
following discussion assumes that the GL is in RGBA mode. Color index
lighting is described in section 2.13.5.
    Lighting may be in one of two states:

     1. Lighting O . In this state, the current color is assigned to the vertex
        primary color. The secondary color is 0; 0; 0; 0.

     2. Lighting On. In this state, the vertex primary and secondary colors
        are computed from the current lighting parameters.

Lighting is turned on or o using the generic Enable or Disable commands
with the symbolic value LIGHTING.




                      Version 1.2.1 - April 1, 1999
2.13. COLORS AND COLORING                                                         45

Lighting Operation
A lighting parameter is of one of ve types: color, position, direction, real,
or boolean. A color parameter consists of four oating-point values, one
for each of R, G, B, and A, in that order. There are no restrictions on the
allowable values for these parameters. A position parameter consists of four
  oating-point coordinates x, y, z , and w that specify a position in object
coordinates w may be zero, indicating a point at in nity in the direction
given by x, y, and z . A direction parameter consists of three oating-point
coordinates x, y, and z  that specify a direction in object coordinates. A
real parameter is one oating-point value. The various values and their
types are summarized in Table 2.7. The result of a lighting computation is
unde ned if a value for a parameter is speci ed that is outside the range
given for that parameter in the table.
    There are n light sources, indexed by i = 0; : : : ; n , 1. n is an implemen-
tation dependent maximum that must be at least 8. Note that the default
values for dcli and scli di er for i = 0 and i 0.
    Before specifying the way that lighting computes colors, we introduce
operators and notation that simplify the expressions involved. If c1 and
c2 are colors without alpha where c1 = r1 ; g1 ; b1  and c2 = r2 ; g2 ; b2 ,
then de ne c1  c2 = r1 r2 ; g1 g2 ; b1 b2 . Addition of colors is accomplished
by addition of the components. Multiplication of colors by a scalar means
multiplying each component by that scalar. If d1 and d2 are directions, then
de ne
                           d1 d2 = maxfd1  d2; 0g:
Directions are taken to have three coordinates.   ,,,If!P1 and P2 are homoge-
neous, with four coordinates points then let P1 P2 be the unit vector that
points from P1 to P2 . Note that ,,, !if P2 has a zero w coordinate and P1 has
non-zero w coordinate, then P1 P2 is the unit vector corresponding to the
direction speci ed by the x, y, and z coordinates of ,P,,    2 ; if P1 has a zero w
coordinate and P2 has a non-zero w coordinate then P1 P!2 is the unit vector
that is the negative of that corresponding to the direction
                                                          ,,,!       speci ed by P1 .
If both P1 and P2 have zero w coordinates, then P            P
                                                            1 2 the unit vector
                                                                  is
obtained by normalizing the direction corresponding to P2 , P1 .
    If d is an arbitrary direction, then let d^ be the unit vector in d's direction.
Let kP1 P2 k be the distance between P1 and P2 . Finally, let V be the point
corresponding to the vertex being lit, and n be the corresponding normal.
Let Pe be the eyepoint 0; 0; 0; 1 in eye coordinates.
    Lighting produces two colors at a vertex: a primary color cpri and a
secondary color csec. The values of cpri and csec depend on the light model




                                  Version 1.2.1 - April 1, 1999
46                                   CHAPTER 2. OPENGL OPERATION

 Parameter     Type         Default Value           Description
 Material Parameters
    acm        color       0:2; 0:2; 0:2; 1:0     ambient color of material
    dcm        color       0:8; 0:8; 0:8; 1:0     di use color of material
    scm        color       0:0; 0:0; 0:0; 1:0     specular color of material
    ecm        color       0:0; 0:0; 0:0; 1:0     emissive color of material
    srm         real               0.0              specular exponent range:
                                                     0:0; 128:0 
     am          real          0:0                  ambient color index
     dm          real          1:0                  di use color index
     sm          real          1:0                  specular color index
 Light Source Parameters
     acli       color 0:0; 0:0; 0:0; 1:0          ambient intensity of light i
 dclii = 0 color 1:0; 1:0; 1:0; 1:0             di use intensity of light 0
 dclii 0 color 0:0; 0:0; 0:0; 1:0               di use intensity of light i
 sclii = 0 color 1:0; 1:0; 1:0; 1:0             specular intensity of light 0
 sclii 0 color 0:0; 0:0; 0:0; 1:0               specular intensity of light i
     Ppli     position 0:0; 0:0; 1:0; 0:0         position of light i
     sdli     direction 0:0; 0:0; ,1:0            direction of spotlight for light
                                                    i
     srli        real              0.0              spotlight exponent for light i
                                                    range: 0:0; 128:0 
     crli        real            180.0              spotlight cuto angle for
                                                    light i range: 0:0; 90:0 ,
                                                    180:0
     k0i         real              1.0              constant attenuation factor
                                                    for light i range: 0:0; 1
     k1i         real              0.0              linear attenuation factor for
                                                    light i range: 0:0; 1
     k2i         real              0.0              quadratic attenuation factor
                                                    for light i range: 0:0; 1
 Lighting Model Parameters
    acs        color 0:2; 0:2; 0:2; 1:0 ambient color of scene
     vbs     boolean        FALSE         viewer assumed to be at
                                          0; 0; 0 in eye coordinates
                                          TRUE or 0; 0; 1 FALSE
     ces       enum      SINGLE COLOR     controls computation of col-
                                          ors
     tbs     boolean        FALSE         use two-sided lighting mode
Table 2.7: Summary of lighting parameters. The range of individual color
components is ,1; +1.



                    Version 1.2.1 - April 1, 1999
2.13. COLORS AND COLORING                                                       47

color control, ces . If ces = SINGLE COLOR, then the equations to compute cpri
and csec are

             cpri = ecm
                  + acm  acs
                    nX
                     ,1
                   +    atti spoti  acm  acli
                    i=0           + n ,     ,!plidcm  dcli
                                            VP
                                  + fi n h^ i srm scm  scli
             csec = 0; 0; 0; 0
   If ces = SEPARATE SPECULAR COLOR, then

              cpri = ecm
                   + acm  acs
                     nX
                      ,1
                    +           atti spoti  acm  acli
                          i=0             + n ,     ,!plidcm  dcli
                                                    VP
                         nX,1
              csec =            atti spoti fi n h^ i srm scm  scli
                         i=0

   where
              
     fi =         1; n ,  ,!pli 6= 0;
                         VP                                                   2.2
                  0; otherwise,

          ,,! ,,!
     hi = VP
           ,,!pli
           VP
                  + VPe ;
                  +  0  0 1 
                                   vbs = TRUE;
                               T ; v = FALSE;                                 2.3
              pli                   bs


              8                   1
             k0   + k 1   k VP     k + k 2  k VP     k 2 ; if Ppli 's w 6= 0,
    atti =      i       i      pli        i      pli                          2.4
           :                    1:0;                       otherwise.




                                     Version 1.2.1 - April 1, 1999
48                                                  CHAPTER 2. OPENGL OPERATION
             8 ,,,!
               Ppli V ^sdli srli ; crli 6= 180:0; ,,,
                                                    P,,, !
                                                      pliV ^sdli  coscrli ;
     spoti =
             :        0:0;           crli =6 180:0; Ppli!V ^sdli coscrli ;2.5
                      1:0;           crli = 180:0:
                                                                            2.6

All computations are carried out in eye coordinates.
    The value of A produced by lighting is the alpha value associated with
dcm. A is always associated with the primary color cpri; the alpha compo-
nent of csec is 0. Results of lighting are unde ned if the we coordinate w
in eye coordinates of V is zero.
    Lighting may operate in two-sided mode tbs = TRUE, in which a front
color is computed with one set of material parameters the front material
and a back color is computed with a second set of material parameters the
back material. This second computation replaces n with ,n. If tbs = FALSE,
then the back color and front color are both assigned the color computed
using the front material with n.
    The selection between back color and front color depends on the primitive
of which the vertex being lit is a part. If the primitive is a point or a line
segment, the front color is always selected. If it is a polygon, then the
selection is based on the sign of the clipped or unclipped polygon's signed
area computed in window coordinates. One way to compute this area is
                                    nX
                                     ,1
                           a = 21         xiw ywi1 , xiw1 ywi             2.7
                                    i=0

where xiw and ywi are the x and y window coordinates of the ith vertex of
the n-vertex polygon vertices are numbered starting at zero for purposes of
this computation and i  1 is i + 1 mod n. The interpretation of the sign
of this value is controlled with

        void   FrontFace enum dir ;
Setting dir to CCW corresponding to counter-clockwise orientation of the
projected polygon in window coordinates indicates that if a  0, then the
color of each vertex of the polygon becomes the back color computed for
that vertex while if a 0, then the front color is selected. If dir is CW, then
a is replaced by ,a in the above inequalities. This requires one bit of state;
initially, it indicates CCW.




                       Version 1.2.1 - April 1, 1999
2.13. COLORS AND COLORING                                                  49

2.13.2 Lighting Parameter Speci cation
Lighting parameters are divided into three categories: material parameters,
light source parameters, and lighting model parameters see Table 2.7. Sets
of lighting parameters are speci ed with

     void   Materialfifg enum face, enum pname, T param ;
     void   Materialfifgv enum face, enum pname, T params ;
     void   Lightfifg enum light, enum pname, T param ;
     void   Lightfifgv enum light, enum pname, T params ;
     void   LightModelfifg enum pname, T param ;
     void   LightModelfifgv enum pname, T params ;
pname is a symbolic constant indicating which parameter is to be set see
Table 2.8. In the vector versions of the commands, params is a pointer to
a group of values to which to set the indicated parameter. The number of
values pointed to depends on the parameter being set. In the non-vector
versions, param is a value to which to set a single-valued parameter. If
param corresponds to a multi-valued parameter, the error INVALID ENUM re-
sults. For the Material command, face must be one of FRONT, BACK, or
FRONT AND BACK, indicating that the property name of the front or back ma-
terial, or both, respectively, should be set. In the case of Light, light is a
symbolic constant of the form LIGHTi, indicating that light i is to have the
speci ed parameter set. The constants obey LIGHTi = LIGHT0 + i.
    Table 2.8 gives, for each of the three parameter groups, the correspon-
dence between the pre-de ned constant names and their names in the light-
ing equations, along with the number of values that must be speci ed with
each. Color parameters speci ed with Material and Light are converted
to oating-point values if speci ed as integers as indicated in Table 2.6
for signed integers. The error INVALID VALUE occurs if a speci ed lighting
parameter lies outside the allowable range given in Table 2.7. The sym-
bol 1" indicates the maximum representable magnitude for the indicated
type.
    The current model-view matrix is applied to the position parameter indi-
cated with Light for a particular light source when that position is speci ed.
These transformed values are the values used in the lighting equation.
    The spotlight direction is transformed when it is speci ed using only the
upper leftmost 3x3 portion of the model-view matrix. That is, if Mu is the
upper left 3x3 matrix taken from the current model-view matrix M , then




                               Version 1.2.1 - April 1, 1999
50                                    CHAPTER 2. OPENGL OPERATION




      Parameter             Name                     Number of values
      Material Parameters Material
         acm                     AMBIENT                    4
         dcm                     DIFFUSE                    4
       acm; dcm          AMBIENT AND DIFFUSE                4
         scm                    SPECULAR                    4
         ecm                    EMISSION                    4
          srm                   SHININESS                   1
      am ; dm ; sm           COLOR INDEXES                  3
      Light Source Parameters Light
         acli                    AMBIENT                    4
         dcli                    DIFFUSE                    4
         scli                   SPECULAR                    4
         Ppli                   POSITION                    4
         sdli               SPOT DIRECTION                  3
          srli               SPOT EXPONENT                  1
          crli                SPOT CUTOFF                   1
          k0             CONSTANT ATTENUATION               1
          k1              LINEAR ATTENUATION                1
          k2            QUADRATIC ATTENUATION               1
      Lighting Model Parameters LightModel
          acs            LIGHT MODEL AMBIENT                4
          vbs         LIGHT MODEL LOCAL VIEWER              1
          tbs            LIGHT MODEL TWO SIDE               1
          ces         LIGHT MODEL COLOR CONTROL             1

Table 2.8: Correspondence of lighting parameter symbols to names.
AMBIENT AND DIFFUSE is used to set acm and dcm to the same value.




                     Version 1.2.1 - April 1, 1999
2.13. COLORS AND COLORING                                                  51

the spotlight direction             0 dx 1
                                    @ dy A
                                      dz
is transformed to          0 d0 1       0 dx 1
                              x
                           @ d0y A = Mu @ dy A :
                              d0z             dz
   An individual light is enabled or disabled by calling Enable or Disable
with the symbolic value LIGHTi i is in the range 0 to n , 1, where n is the
implementation-dependent number of lights. If light i is disabled, the ith
term in the lighting equation is e ectively removed from the summation.

2.13.3 ColorMaterial
It is possible to attach one or more material properties to the current color,
so that they continuously track its component values. This behavior is
enabled and disabled by calling Enable or Disable with the symbolic value
COLOR MATERIAL.
     The command that controls which of these modes is selected is
     void   ColorMaterial enum face, enum mode ;
face is one of FRONT, BACK, or FRONT AND BACK, indicating whether the front
material, back material, or both are a ected by the current color. mode
is one of EMISSION, AMBIENT, DIFFUSE, SPECULAR, or AMBIENT AND DIFFUSE and
speci es which material property or properties track the current color. If
mode is EMISSION, AMBIENT, DIFFUSE, or SPECULAR, then the value of ecm ,
acm, dcm or scm , respectively, will track the current color. If mode is
AMBIENT AND DIFFUSE, both acm and dcm track the current color. The re-
placements made to material properties are permanent; the replaced values
remain until changed by either sending a new color or by setting a new ma-
terial value when ColorMaterial is not currently enabled to override that
particular value. When COLOR MATERIAL is enabled, the indicated parameter
or parameters always track the current color. For instance, calling
     ColorMaterialFRONT, AMBIENT
while COLOR MATERIAL is enabled sets the front material acm to the value of
the current color.




                                Version 1.2.1 - April 1, 1999
52                                                       CHAPTER 2. OPENGL OPERATION




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




     Figure 2.10. ColorMaterial operation. Material properties are continuously
     updated from the current color while ColorMaterial is enabled and has the
     appropriate mode. Only the front material properties are included in this
      gure. The back material properties are treated identically, except that face
     must be BACK or FRONT AND BACK.




                                 Version 1.2.1 - April 1, 1999
2.13. COLORS AND COLORING                                                     53

2.13.4 Lighting State
The state required for lighting consists of all of the lighting parameters front
and back material parameters, lighting model parameters, and at least 8 sets
of light parameters, a bit indicating whether a back color distinct from the
front color should be computed, at least 8 bits to indicate which lights are
enabled, a ve-valued variable indicating the current ColorMaterial mode,
a bit indicating whether or not COLOR MATERIAL is enabled, and a single bit
to indicate whether lighting is enabled or disabled. In the initial state, all
lighting parameters have their default values. Back color evaluation does
not take place, ColorMaterial is FRONT AND BACK and AMBIENT AND DIFFUSE,
and both lighting and COLOR MATERIAL are disabled.
2.13.5 Color Index Lighting
A simpli ed lighting computation applies in color index mode that uses
many of the parameters controlling RGBA lighting, but none of the RGBA
material parameters. First, the RGBA di use and specular intensities of
light i dcli and scli , respectively determine color index di use and specular
light intensities, dli and sli from
                dli = :30Rdcli  + :59Gdcli  + :11B dcli 
and
                 sli = :30Rscli  + :59Gscli  + :11B scli :
Rx indicates the R component of the color x and similarly for Gx and
B x.
    Next, let
                           Xn
                     s = atti spotisli fin h^ i srm
                        i=0
where atti and spoti are given by equations 2.4 and 2.5, respectively, and fi
and h^ i are given by equations 2.2 and 2.3, respectively. Let s0 = minfs; 1g.
Finally, let
                         Xn
                     d = attispoti dli n ,  ,!pli:
                                                  VP
                         i=0
Then color index lighting produces a value c, given by
               c = am + d1 , s0 dm , am + s0sm , am :
The nal color index is
                             c0 = minfc; sm g:




                                 Version 1.2.1 - April 1, 1999
54                                    CHAPTER 2. OPENGL OPERATION

The values am , dm and sm are material properties described in Tables 2.7
and 2.8. Any ambient light intensities are incorporated into am . As with
RGBA lighting, disabled lights cause the corresponding terms from the sum-
mations to be omitted. The interpretation of tbs and the calculation of front
and back colors is carried out as has already been described for RGBA
lighting.
    The values am , dm , and sm are set with Material using a pname of
COLOR INDEXES. Their initial values are 0, 1, and 1, respectively. The ad-
ditional state consists of three oating-point values. These values have no
e ect on RGBA lighting.

2.13.6 Clamping or Masking
After lighting whether enabled or not, all components of both primary and
secondary colors are clamped to the range 0; 1 .
    For a color index, the index is rst converted to xed-point with an
unspeci ed number of bits to the right of the binary point; the nearest
 xed-point value is selected. Then, the bits to the right of the binary point
are left alone while the integer portion is masked bitwise ANDed with
2n , 1, where n is the number of bits in a color in the color index bu er
bu ers are discussed in chapter 4.

2.13.7 Flatshading
A primitive may be atshaded, meaning that all vertices of the primitive are
assigned the same color index or the same primary and secondary colors.
These colors are the colors of the vertex that spawned the primitive. For a
point, these are the colors associated with the point. For a line segment, they
are the colors of the second  nal vertex of the segment. For a polygon, they
come from a selected vertex depending on how the polygon was generated.
Table 2.9 summarizes the possibilities.
    Flatshading is controlled by

      void   ShadeModel enum mode ;
mode value must be either of the symbolic constants SMOOTH or FLAT. If mode
is SMOOTH the initial state, vertex colors are treated individually. If mode is
FLAT, atshading is turned on. ShadeModel thus requires one bit of state.




                     Version 1.2.1 - April 1, 1999
2.13. COLORS AND COLORING                                                   55

                  Primitive type of polygon i          Vertex
                  single polygon i  1                  1
                  triangle strip                        i+2
                  triangle fan                          i+2
                  independent triangle                   3i
                  quad strip                           2i + 2
                  independent quad                       4i

Table 2.9: Polygon atshading color selection. The colors used for atshad-
ing the ith polygon generated by the indicated Begin End type are derived
from the current color if lighting is disabled in e ect when the indicated
vertex is speci ed. If lighting is enabled, the colors are produced by lighting
the indicated vertex. Vertices are numbered 1 through n, where n is the
number of vertices between the Begin End pair.

2.13.8 Color and Texture Coordinate Clipping
After lighting, clamping or masking and possible atshading, colors are
clipped. Those colors associated with a vertex that lies within the clip
volume are una ected by clipping. If a primitive is clipped, however, the
colors assigned to vertices produced by clipping are clipped colors.
    Let the colors assigned to the two vertices P1 and P2 of an unclipped
edge be c1 and c2 . The value of t section 2.11 for a clipped point P is
used to obtain the color associated with P as

                             c = tc1 + 1 , tc2 :
For a color index color, multiplying a color by a scalar means multiplying
the index by the scalar. For an RGBA color, it means multiplying each of R,
G, B, and A by the scalar. Both primary and secondary colors are treated
in the same fashion. Polygon clipping may create a clipped vertex along an
edge of the clip volume's boundary. This situation is handled by noting that
polygon clipping proceeds by clipping against one plane of the clip volume's
boundary at a time. Color clipping is done in the same way, so that clipped
points always occur at the intersection of polygon edges possibly already
clipped with the clip volume's boundary.
    Texture coordinates must also be clipped when a primitive is clipped.
The method is exactly analogous to that used for color clipping.




                                Version 1.2.1 - April 1, 1999
56                                   CHAPTER 2. OPENGL OPERATION

2.13.9 Final Color Processing
For an RGBA color, each color component which lies in 0; 1  is converted
by rounding to nearest to a xed-point value with m bits. We assume
that the xed-point representation used represents each value k=2m , 1,
where k 2 f0; 1; : : : ; 2m , 1g, as k e.g. 1.0 is represented in binary as a
string of all ones. m must be at least as large as the number of bits in the
corresponding component of the framebu er. m must be at least 2 for A if
the framebu er does not contain an A component, or if there is only 1 bit
of A in the framebu er. A color index is converted by rounding to nearest
to a xed-point value with at least as many bits as there are in the color
index portion of the framebu er.
    Because a number of the form k=2m , 1 may not be represented exactly
as a limited-precision oating-point quantity, we place a further requirement
on the xed-point conversion of RGBA components. Suppose that lighting
is disabled, the color associated with a vertex has not been clipped, and one
of Colorub, Colorus, or Colorui was used to specify that color. When
these conditions are satis ed, an RGBA component must convert to a value
that matches the component as speci ed in the Color command: if m is less
than the number of bits b with which the component was speci ed, then the
converted value must equal the most signi cant m bits of the speci ed value;
otherwise, the most signi cant b bits of the converted value must equal the
speci ed value.




                    Version 1.2.1 - April 1, 1999
Chapter 3
Rasterization
Rasterization is the process by which a primitive is converted to a two-
dimensional image. Each point of this image contains such information as
color and depth. Thus, rasterizing a primitive consists of two parts. The
  rst is to determine which squares of an integer grid in window coordinates
are occupied by the primitive. The second is assigning a color and a depth
value to each such square. The results of this process are passed on to the
next stage of the GL per-fragment operations, which uses the information
to update the appropriate locations in the framebu er. Figure 3.1 diagrams
the rasterization process.
     A grid square along with its parameters of assigned color, z depth,
and texture coordinates is called a fragment; the parameters are collectively
dubbed the fragment's associated data. A fragment is located by its lower-
left corner, which lies on integer grid coordinates. Rasterization operations
also refer to a fragment's center, which is o set by 1=2; 1=2 from its lower-
left corner and so lies on half-integer coordinates.
     Grid squares need not actually be square in the GL. Rasterization rules
are not a ected by the actual aspect ratio of the grid squares. Display of
non-square grids, however, will cause rasterized points and line segments to
appear fatter in one direction than the other. We assume that fragments
are square, since it simpli es antialiasing and texturing.
     Several factors a ect rasterization. Lines and polygons may be stippled.
Points may be given di ering diameters and line segments di ering widths.
A point, line segment, or polygon may be antialiased.
                                      57



                                Version 1.2.1 - April 1, 1999
58                                             CHAPTER 3. RASTERIZATION




                              Point
                           Rasterization



          From
                               Line
        Primitive                                       Texturing
                           Rasterization
        Assembly


                             Polygon
                           Rasterization

                                                        Color Sum
                              Pixel
           DrawPixels       Rectangle
                           Rasterization



                             Bitmap
               Bitmap                                     Fog
                           Rasterization
                                                                    Fragments



     Figure 3.1. Rasterization.




                        Version 1.2.1 - April 1, 1999
3.1. INVARIANCE                                                             59

3.1 Invariance
Consider a primitive p0 obtained by translating a primitive p through an
o set x; y in window coordinates, where x and y are integers. As long
as neither p0 nor p is clipped, it must be the case that each fragment f 0
produced from p0 is identical to a corresponding fragment f from p except
that the center of f 0 is o set by x; y from the center of f .

3.2 Antialiasing
Antialiasing of a point, line, or polygon is e ected in one of two ways de-
pending on whether the GL is in RGBA or color index mode.
    In RGBA mode, the R, G, and B values of the rasterized fragment are
left una ected, but the A value is multiplied by a oating-point value in
the range 0; 1 that describes a fragment's screen pixel coverage. The
per-fragment stage of the GL can be set up to use the A value to blend
the incoming fragment with the corresponding pixel already present in the
framebu er.
    In color index mode, the least signi cant b bits to the left of the binary
point of the color index are used for antialiasing; b = minf4; mg, where
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
be computationally expensive; consequently we allow a given GL implemen-
tation to approximate true coverage values by using a fast but not entirely
accurate coverage computation.
    In light of these considerations, we chose to specify the behavior of exact
antialiasing in the prototypical case that each displayed pixel is a perfect
square of uniform intensity. The square is called a fragment square and has
lower left corner x; y and upper right corner x + 1; y + 1. We recognize




                                Version 1.2.1 - April 1, 1999
60                                           CHAPTER 3. RASTERIZATION

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
In some implementations, varying degrees of antialiasing quality may be
obtained by providing GL hints section 5.6, allowing a user to make an
image quality versus speed tradeo .

3.3 Points
The rasterization of points is controlled with
       void   PointSize float size ;
size speci es the width or diameter of a point. The default value is 1.0. A
value less than or equal to zero results in the error INVALID VALUE.
    Point antialiasing is enabled or disabled by calling Enable or Disable
with the symbolic constant POINT SMOOTH. The default state is for point an-
tialiasing to be disabled.
    In the default state, a point is rasterized by truncating its xw and yw
coordinates recall that the subscripts indicate that these are x and y window
coordinates to integers. This x; y address, along with data derived from
the data associated with the vertex corresponding to the point, is sent as a
single fragment to the per-fragment stage of the GL.




                      Version 1.2.1 - April 1, 1999
3.3. POINTS                                                                   61

    The e ect of a point width other than 1:0 depends on the state of point
antialiasing. If antialiasing is disabled, the actual width is determined by
rounding the supplied width to the nearest integer, then clamping it to
the implementation-dependent maximum non-antialiased point width. This
implementation-dependent value must be no less than the implementation-
dependent maximum antialiased point width, rounded to the nearest integer
value, and in any event no less than 1. If rounding the speci ed width results
in the value 0, then it is as if the value were 1. If the resulting width is odd,
then the point
                          x; y = bxw c + 21 ; byw c + 12 
is computed from the vertex's xw and yw , and a square grid of the odd width
centered at x; y de nes the centers of the rasterized fragments recall that
fragment centers lie at half-integer window coordinate values. If the width
is even, then the center point is
                         x; y = bxw + 21 c; byw + 21 c;
the rasterized fragment centers are the half-integer window coordinate values
within the square of the even width centered on x; y. See gure 3.2.
    All fragments produced in rasterizing a non-antialiased point are as-
signed the same associated data, which are those of the vertex corresponding
to the point, with texture coordinates s, t, and r replaced with s=q, t=q, and
r=q, respectively. If q is less than or equal to zero, the results are unde ned.
    If antialiasing is enabled, then point rasterization produces a fragment
for each fragment square that intersects the region lying within the circle
having diameter equal to the current point width and centered at the point's
xw ; yw   gure 3.3. The coverage value for each fragment is the window
coordinate area of the intersection of the circular region with the corre-
sponding fragment square but see section 3.2. This value is saved and
used in the nal step of rasterization section 3.11. The data associated
with each fragment are otherwise the data associated with the point being
rasterized, with texture coordinates s, t, and r replaced with s=q, t=q, and
r=q, respectively. If q is less than or equal to zero, the results are unde ned.
    Not all widths need be supported when point antialiasing is on, but
the width 1:0 must be provided. If an unsupported width is requested, the
nearest supported width is used instead. The range of supported widths and
the width of evenly-spaced gradations within that range are implementation
dependent. The range and gradations may be obtained using the query




                                 Version 1.2.1 - April 1, 1999
62                                                  CHAPTER 3. RASTERIZATION


                                              5.5

                                              4.5

                                              3.5

                                              2.5

                                              1.5

                                              0.5

         0.5   1.5   2.5   3.5   4.5   5.5            0.5   1.5   2.5   3.5   4.5   5.5

                Odd Width                                    Even Width

     Figure 3.2. Rasterization of non-antialiased wide points. The crosses show
     fragment centers produced by rasterization for any point that lies within the
     shaded region. The dotted grid lines lie on half-integer coordinates.


mechanism described in Chapter 6. If, for instance, the width range is from
0.1 to 2.0 and the gradation width is 0.1, then the widths 0:1; 0:2; : : : ; 1:9; 2:0
are supported.

3.3.1 Point Rasterization State
The state required to control point rasterization consists of the oating-point
point width and a bit indicating whether or not antialiasing is enabled.

3.4 Line Segments
A line segment results from a line strip Begin End object, a line loop, or
a series of separate line segments. Line segment rasterization is controlled
by several variables. Line width, which may be set by calling
        void   LineWidth float width ;
with an appropriate positive oating-point width, controls the width of ras-
terized line segments. The default width is 1:0. Values less than or equal




                           Version 1.2.1 - April 1, 1999
3.4. LINE SEGMENTS                                                                 63




                      6.0



                      5.0



                      4.0



                      3.0



                      2.0



                      1.0



                      0.0
                            0.0   1.0     2.0   3.0   4.0   5.0   6.0




  Figure 3.3. Rasterization of antialiased wide points. The black dot indi-
  cates the point to be rasterized. The shaded region has the speci ed width.
  The X marks indicate those fragment centers produced by rasterization. A
  fragment's computed coverage value is based on the portion of the shaded re-
  gion that covers the corresponding fragment square. Solid lines lie on integer
  coordinates.




                                        Version 1.2.1 - April 1, 1999
64                                           CHAPTER 3. RASTERIZATION

to 0:0 generate the error INVALID VALUE. Antialiasing is controlled with En-
able and Disable using the symbolic constant LINE SMOOTH. Finally, line
segments may be stippled. Stippling is controlled by a GL command that
sets a stipple pattern see below.
3.4.1 Basic Line Segment Rasterization
Line segment rasterization begins by characterizing the segment as either
x-major or y-major. x-major line segments have slope in the closed inter-
val ,1; 1 ; all other line segments are y-major slope is determined by the
segment's endpoints. We shall specify rasterization only for x-major seg-
ments except in cases where the modi cations for y-major segments are not
self-evident.
    Ideally, the GL uses a diamond-exit" rule to determine those fragments
that are produced by rasterizing a line segment. For each fragment f with
center at window coordinates xf and yf , de ne a diamond-shaped region
that is the intersection of four half planes:
                   Rf = f x; y j jx , xf j + jy , yf j 1=2:g
    Essentially, a line segment starting at pa and ending at pb produces those
fragments f for which the segment intersects Rf , except if pb is contained
in Rf . See gure 3.4.
    To avoid di culties when an endpoint lies on a boundary of Rf we in
principle perturb the supplied endpoints by a tiny amount. Let pa and
pb have window coordinates xa ; ya and xb; yb , respectively. Obtain the
perturbed endpoints p0a given by xa ; ya  ,  ; 2  and p0b given by xb ; yb  ,
 ; 2 . Rasterizing the line segment starting at pa and ending at pb produces
those fragments f for which the segment starting at p0a and ending on p0b
intersects Rf , except if p0b is contained in Rf . is chosen to be so small
that rasterizing the line segment produces the same fragments when is
substituted for for any 0          .
    When pa and pb lie on fragment centers, this characterization of frag-
ments reduces to Bresenham's algorithm with one modi cation: lines pro-
duced in this description are half-open," meaning that the nal fragment
corresponding to pb  is not drawn. This means that when rasterizing a
series of connected line segments, shared endpoints will be produced only
once rather than twice as would occur with Bresenham's algorithm.
    Because the initial and nal conditions of the diamond-exit rule may
be di cult to implement, other line segment rasterization algorithms are
allowed, subject to the following rules:




                      Version 1.2.1 - April 1, 1999
3.4. LINE SEGMENTS                                                                  65




   Figure 3.4. Visualization of Bresenham's algorithm. A portion of a line
   segment is shown. A diamond shaped region of height 1 is placed around each
   fragment center; those regions that the line segment exits cause rasterization
   to produce corresponding fragments.


   1. The coordinates of a fragment produced by the algorithm may not
      deviate by more than one unit in either x or y window coordinates
      from a corresponding fragment produced by the diamond-exit rule.
   2. The total number of fragments produced by the algorithm may di er
      from that produced by the diamond-exit rule by no more than one.
   3. For an x-major line, no two fragments may be produced that lie in the
      same window-coordinate column for a y-major line, no two fragments
      may appear in the same row.
   4. If two line segments share a common endpoint, and both segments
      are either x-major both left-to-right or both right-to-left or y-major
      both bottom-to-top or both top-to-bottom, then rasterizing both
      segments may not produce duplicate fragments, nor may any frag-
      ments be omitted so as to interrupt continuity of the connected seg-
      ments.
   Next we must specify how the data associated with each rasterized frag-
ment are obtained. Let the window coordinates of a produced fragment
center be given by pr = xd ; yd  and let pa = xa ; ya  and pb = xb ; yb . Set




                                  Version 1.2.1 - April 1, 1999
66                                          CHAPTER 3. RASTERIZATION


                         t = pr ,kppa , ppbk2, pa  :               3.1
                                       b        a
Note that t = 0 at pa and t = 1 at pb . The value of an associated datum
f for the fragment, whether it be R, G, B, or A in RGBA mode or a color
index in color index mode, or the s, t, or r texture coordinate the depth
value, window z , must be found using equation 3.3, below, is found as
                            1 , tfa =wa + tfb=wb
                        f = 1                                          3.2
                               , t =w + t =w
                                       a    a       b   b
where fa and fb are the data associated with the starting and ending end-
points of the segment, respectively; wa and wb are the clip w coordinates of
the starting and ending endpoints of the segments, respectively. a = b = 1
for all data except texture coordinates, in which case a = qa and b = qb
qa and qb are the homogeneous texture coordinates at the starting and end-
ing endpoints of the segment; results are unde ned if either of these is less
than or equal to 0. Note that linear interpolation would use
                        f = 1 , tfa = a + tfb = b :                   3.3
The reason that this formula is incorrect except for the depth value is
that it interpolates a datum in window space, which may be distorted by
perspective. What is actually desired is to nd the corresponding value when
interpolated in clip space, which equation 3.2 does. A GL implementation
may choose to approximate equation 3.2 with 3.3, but this will normally lead
to unacceptable distortion e ects when interpolating texture coordinates.

3.4.2 Other Line Segment Features
We have just described the rasterization of non-antialiased line segments
of width one using the default line stipple of FFFF16 . We now describe
the rasterization of line segments for general values of the line segment
rasterization parameters.

Line Stipple
The command
     void   LineStipple int factor, ushort pattern ;




                    Version 1.2.1 - April 1, 1999
3.4. LINE SEGMENTS                                                             67

de nes a line stipple. pattern is an unsigned short integer. The line stipple is
taken from the lowest order 16 bits of pattern. It determines those fragments
that are to be drawn when the line is rasterized. factor is a count that is
used to modify the e ective line stipple by causing each bit in line stipple to
be used factor times. factor is clamped to the range 1; 256 . Line stippling
may be enabled or disabled using Enable or Disable with the constant
LINE STIPPLE. When disabled, it is as if the line stipple has its default value.
    Line stippling masks certain fragments that are produced by rasteriza-
tion so that they are not sent to the per-fragment stage of the GL. The
masking is achieved using three parameters: the 16-bit line stipple p, the
line repeat count r, and an integer stipple counter s. Let
                              b = bs=rc mod 16;
Then a fragment is produced if the bth bit of p is 1, and not produced
otherwise. The bits of p are numbered with 0 being the least signi cant and
15 being the most signi cant. The initial value of s is zero; s is incremented
after production of each fragment of a line segment fragments are produced
in order, beginning at the starting point and working towards the ending
point. s is reset to 0 whenever a Begin occurs, and before every line
segment in a group of independent segments as speci ed when Begin is
invoked with LINES.
    If the line segment has been clipped, then the value of s at the beginning
of the line segment is indeterminate.
Wide Lines
The actual width of non-antialiased lines is determined by rounding the sup-
plied width to the nearest integer, then clamping it to the implementation-
dependent maximum non-antialiased line width. This implementation-
dependent value must be no less than the implementation-dependent max-
imum antialiased line width, rounded to the nearest integer value, and in
any event no less than 1. If rounding the speci ed width results in the value
0, then it is as if the value were 1.
    Non-antialiased line segments of width other than one are rasterized
by o setting them in the minor direction for an x-major line, the minor
direction is y, and for a y-major line, the minor direction is x and replicating
fragments in the minor direction see gure 3.5. Let w be the width rounded
to the nearest integer if w = 0, then it is as if w = 1. If the line segment has
endpoints given by x0 ; y0  and x1 ; y1  in window coordinates, the segment
with endpoints x0 ; y0 , w , 1=2 and x1 ; y1 , w , 1=2 is rasterized, but




                                 Version 1.2.1 - April 1, 1999
68                                             CHAPTER 3. RASTERIZATION




                     width = 2                            width = 3



     Figure 3.5. Rasterization of non-antialiased wide lines. x-major line segments
     are shown. The heavy line segment is the one speci ed to be rasterized; the
     light segment is the o set segment used for rasterization. x marks indicate
     the fragment centers produced by rasterization.


instead of a single fragment, a column of fragments of height w a row of
fragments of length w for a y-major segment is produced at each x y for
y-major location. The lowest fragment of this column is the fragment that
would be produced by rasterizing the segment of width 1 with the modi ed
coordinates. The whole column is not produced if the stipple bit for the
column's x location is zero; otherwise, the whole column is produced.
Antialiasing
Rasterized antialiased line segments produce fragments whose fragment
squares intersect a rectangle centered on the line segment. Two of the edges
are parallel to the speci ed line segment; each is at a distance of one-half the
current width from that segment: one above the segment and one below it.
The other two edges pass through the line endpoints and are perpendicular
to the direction of the speci ed line segment. Coverage values are computed
for each fragment by computing the area of the intersection of the rectangle
with the fragment square see gure 3.6; see also section 3.2. Equation 3.2
is used to compute associated data values just as with non-antialiased lines;
equation 3.1 is used to nd the value of t for each fragment whose square
is intersected by the line segment's rectangle. Not all widths need be sup-




                        Version 1.2.1 - April 1, 1999
3.4. LINE SEGMENTS                                                               69




   Figure 3.6. The region used in rasterizing and nding corresponding coverage
   values for an antialiased line segment an x-major line segment is shown.


ported for line segment antialiasing, but width 1:0 antialiased segments must
be provided. As with the point width, a GL implementation may be queried
for the range and number of gradations of available antialiased line widths.
    For purposes of antialiasing, a stippled line is considered to be a sequence
of contiguous rectangles centered on the line segment. Each rectangle has
width equal to the current line width and length equal to 1 pixel except the
last, which may be shorter. These rectangles are numbered from 0 to n,
starting with the rectangle incident on the starting endpoint of the segment.
Each of these rectangles is either eliminated or produced according to the
procedure given under Line Stipple, above, where fragment" is replaced
with rectangle." Each rectangle so produced is rasterized as if it were an
antialiased polygon, described below but culling, non-default settings of
PolygonMode, and polygon stippling are not applied.
3.4.3 Line Rasterization State
The state required for line rasterization consists of the oating-point line
width, a 16-bit line stipple, the line stipple repeat count, a bit indicating
whether stippling is enabled or disabled, and a bit indicating whether line
antialiasing is on or o . In addition, during rasterization, an integer stipple
counter must be maintained to implement line stippling. The initial value
of the line width is 1:0. The initial value of the line stipple is FFFF16 a
stipple of all ones. The initial value of the line stipple repeat count is one.




                                 Version 1.2.1 - April 1, 1999
70                                           CHAPTER 3. RASTERIZATION

The initial state of line stippling is disabled. The initial state of line segment
antialiasing is disabled.

3.5 Polygons
A polygon results from a polygon Begin End object, a triangle resulting
from a triangle strip, triangle fan, or series of separate triangles, or a quadri-
lateral arising from a quadrilateral strip, series of separate quadrilaterals, or
a Rect command. Like points and line segments, polygon rasterization is
controlled by several variables. Polygon antialiasing is controlled with En-
able and Disable with the symbolic constant POLYGON SMOOTH. The analog
to line segment stippling for polygons is polygon stippling, described below.
3.5.1 Basic Polygon Rasterization
The rst step of polygon rasterization is to determine if the polygon is
back facing or front facing. This determination is made by examining the
sign of the area computed by equation 2.7 of section 2.13.1 including the
possible reversal of this sign as indicated by the last call to FrontFace. If
this sign is positive, the polygon is frontfacing; otherwise, it is back facing.
This determination is used in conjunction with the CullFace enable bit and
mode value to decide whether or not a particular polygon is rasterized. The
CullFace mode is set by calling
       void CullFace enum mode ;

mode is a symbolic constant: one of FRONT, BACK or FRONT AND BACK. Culling
is enabled or disabled with Enable or Disable using the symbolic constant
CULL FACE. Front facing polygons are rasterized if either culling is disabled or
the CullFace mode is BACK while back facing polygons are rasterized only if
either culling is disabled or the CullFace mode is FRONT. The initial setting
of the CullFace mode is BACK. Initially, culling is disabled.
    The rule for determining which fragments are produced by polygon ras-
terization is called point sampling. The two-dimensional projection obtained
by taking the x and y window coordinates of the polygon's vertices is formed.
Fragment centers that lie inside of this polygon are produced by rasteriza-
tion. Special treatment is given to a fragment whose center lies on a polygon
boundary edge. In such a case we require that if two polygons lie on either
side of a common edge with identical endpoints on which a fragment cen-
ter lies, then exactly one of the polygons results in the production of the
fragment during rasterization.




                      Version 1.2.1 - April 1, 1999
3.5. POLYGONS                                                                  71

   As for the data associated with each fragment produced by rasterizing a
polygon, we begin by specifying how these values are produced for fragments
in a triangle. De ne barycentric coordinates for a triangle. Barycentric
coordinates are a set of three numbers, a, b, and c, each in the range 0; 1 ,
with a + b + c = 1. These coordinates uniquely specify any point p within
the triangle or on the triangle's boundary as
                              p = apa + bpb + cpc;
where pa , pb , and pc are the vertices of the triangle. a, b, and c can be found
as
                    Appb pc ; b = Appa pc  ; c = Appa pb  ;
               a = A ppp
                      a b c           Ap p p 
                                           a b c         Ap p p  a b c
where Almn denotes the area in window coordinates of the triangle with
vertices l, m, and n.
    Denote a datum at pa , pb , or pc as fa , fb , or fc , respectively. Then the
value f of a datum at a fragment produced by rasterizing a triangle is given
by

                       f = aafa=w
                               =wa + bfb=wb + cfc=wc
                                   + b =w + c =w                            3.4
                               a     a      b    b      c   c
where wa , wb and wc are the clip w coordinates of pa , pb , and pc, respectively.
a, b, and c are the barycentric coordinates of the fragment for which the data
are produced. a = b = c = 1 except for texture s, t, and r coordinates,
for which a = qa , b = qb , and c = qc if any of qa , qb , or qc are less
than or equal to zero, results are unde ned. a, b, and c must correspond
precisely to the exact coordinates of the center of the fragment. Another way
of saying this is that the data associated with a fragment must be sampled
at the fragment's center.
    Just as with line segment rasterization, equation 3.4 may be approxi-
mated by
                        f = afa = a + bfb = b + cfc= c ;
this may yield acceptable results for color values it must be used for depth
values, but will normally lead to unacceptable distortion e ects if used for
texture coordinates.
    For a polygon with more than three edges, we require only that a convex
combination of the values of the datum at the polygon's vertices can be used
to obtain the value assigned to each fragment produced by the rasterization




                                   Version 1.2.1 - April 1, 1999
72                                           CHAPTER 3. RASTERIZATION

algorithm. That is, it must be the case that at every fragment
                                       X
                                       n
                                 f=          ai fi
                                       i=1
where n is the number of vertices inPthe polygon, fi is the value of the f at
vertex i; for each i 0  ai  1 and ni=1 ai = 1. The values of the ai may
di er from fragment to fragment, but at vertex i, aj = 0; j 6= i and ai = 1.
    One algorithm that achieves the required behavior is to triangulate a
polygon without adding any vertices and then treat each triangle individ-
ually as already discussed. A scan-line rasterizer that linearly interpolates
data along each edge and then linearly interpolates data across each hor-
izontal span from edge to edge also satis es the restrictions in this case,
the numerator and denominator of equation 3.4 should be iterated indepen-
dently and a division performed for each fragment.
3.5.2 Stippling
Polygon stippling works much the same way as line stippling, masking out
certain fragments produced by rasterization so that they are not sent to the
next stage of the GL. This is the case regardless of the state of polygon
antialiasing. Stippling is controlled with
     void   PolygonStipple ubyte *pattern ;
pattern is a pointer to memory into which a 32  32 pattern is packed.
The pattern is unpacked from memory according to the procedure given
in section 3.6.4 for DrawPixels; it is as if the height and width passed to
that command were both equal to 32, the type were BITMAP, and the format
were COLOR INDEX. The unpacked values before any conversion or arithmetic
would have been performed form a stipple pattern of zeros and ones.
    If xw and yw are the window coordinates of a rasterized polygon frag-
ment, then that fragment is sent to the next stage of the GL if and only if
the bit of the pattern xw mod 32; yw mod 32 is 1.
    Polygon stippling may be enabled or disabled with Enable or Disable
using the constant POLYGON STIPPLE. When disabled, it is as if the stipple
pattern were all ones.
3.5.3 Antialiasing
Polygon antialiasing rasterizes a polygon by producing a fragment wherever
the interior of the polygon intersects that fragment's square. A coverage




                    Version 1.2.1 - April 1, 1999
3.5. POLYGONS                                                                    73

value is computed at each such fragment, and this value is saved to be applied
as described in section 3.11. An associated datum is assigned to a fragment
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
     void   PolygonMode enum face, enum mode ;
face is one of FRONT, BACK, or FRONT AND BACK, indicating that the rasterizing
method described by mode replaces the rasterizing method for front facing
polygons, back facing polygons, or both front and back facing polygons,
respectively. mode is one of the symbolic constants POINT, LINE, or FILL.
Calling PolygonMode with POINT causes certain vertices of a polygon to
be treated, for rasterization purposes, just as if they were enclosed within
a BeginPOINT and End pair. The vertices selected for this treatment are
those that have been tagged as having a polygon boundary edge beginning
on them see section 2.6.2. LINE causes edges that are tagged as boundary
to be rasterized as line segments. The line stipple counter is reset at the
beginning of the rst rasterized edge of the polygon, but not for subsequent
edges. FILL is the default mode of polygon rasterization, corresponding to
the description in sections 3.5.1, 3.5.2, and 3.5.3. Note that these modes
a ect only the nal rasterization of polygons: in particular, a polygon's
vertices are lit, and the polygon is clipped and possibly culled before these
modes are applied.
    Polygon antialiasing applies only to the FILL state of PolygonMode.
For POINT or LINE, point antialiasing or line segment antialiasing, respec-
tively, apply.
3.5.5 Depth O set
The depth values of all fragments generated by the rasterization of a polygon
may be o set by a single value that is computed for that polygon. The




                               Version 1.2.1 - April 1, 1999
74                                          CHAPTER 3. RASTERIZATION

function that determines this value is speci ed by calling
     void   PolygonO set float factor, float units ;
factor scales the maximum depth slope of the polygon, and units scales an
implementation dependent constant that relates to the usable resolution of
the depth bu er. The resulting values are summed to produce the polygon
o set value. Both factor and units may be either positive or negative.
    The maximum depth slope m of a triangle is
                               s         2  @zw 2
                                     @z
                            m = @x + @yw                                3.5
                                        w          w
where xw ; yw ; zw  is a point on the triangle. m may be approximated as
                            m = max @x   @zw ; @zw :                    3.6
                                           w @yw
If the polygon has more than three vertices, one or more values of m may be
used during rasterization. Each may take any value in the range min,max ,
where min and max are the smallest and largest values obtained by evaluat-
ing Equation 3.5 or Equation 3.6 for the triangles formed by all three-vertex
combinations.
    The minimum resolvable di erence r is an implementation constant. It
is the smallest di erence in window coordinate z values that is guaranteed
to remain distinct throughout polygon rasterization and in the depth bu er.
All pairs of fragments generated by the rasterization of two polygons with
otherwise identical vertices, but zw values that di er by r, will have distinct
depth values.
    The o set value o for a polygon is
                         o = m  factor + r  units:                      3.7
m is computed as described above, as a function of depth values in the range
0,1 , and o is applied to depth values in the same range.
    Boolean state values POLYGON OFFSET POINT, POLYGON OFFSET LINE, and
POLYGON OFFSET FILL determine whether o is applied during the rasteriza-
tion of polygons in POINT, LINE, and FILL modes. These boolean state val-
ues are enabled and disabled as argument values to the commands Enable
and Disable. If POLYGON OFFSET POINT is enabled, o is added to the depth
value of each fragment produced by the rasterization of a polygon in POINT
mode. Likewise, if POLYGON OFFSET LINE or POLYGON OFFSET FILL is enabled, o




                     Version 1.2.1 - April 1, 1999
3.6. PIXEL RECTANGLES                                                       75

is added to the depth value of each fragment produced by the rasterization
of a polygon in LINE or FILL modes, respectively.
    Fragment depth values are always limited to the range 0,1 , either by
clamping after o set addition is performed preferred, or by clamping the
vertex values used in the rasterization of the polygon.
3.5.6 Polygon Rasterization State
The state required for polygon rasterization consists of a polygon stipple pat-
tern, whether stippling is enabled or disabled, the current state of polygon
antialiasing enabled or disabled, the current values of the PolygonMode
setting for each of front and back facing polygons, whether point, line, and
 ll mode polygon o sets are enabled or disabled, and the factor and bias
values of the polygon o set equation. The initial stipple pattern is all ones;
initially stippling is disabled. The initial setting of polygon antialiasing is
disabled. The initial state for PolygonMode is FILL for both front and
back facing polygons. The initial polygon o set factor and bias values are
both 0; initially polygon o set is disabled for all modes.

3.6 Pixel Rectangles
Rectangles of color, depth, and certain other values may be converted to
fragments using the DrawPixels command described in section 3.6.4.
Some of the parameters and operations governing the operation of Draw-
Pixels are shared by ReadPixels used to obtain pixel values from the
framebu er and CopyPixels used to copy pixels from one framebu er
location to another; the discussion of ReadPixels and CopyPixels, how-
ever, is deferred until Chapter 4 after the framebu er has been discussed
in detail. Nevertheless, we note in this section when parameters and state
pertaining to DrawPixels also pertain to ReadPixels or CopyPixels.
    A number of parameters control the encoding of pixels in client mem-
ory for reading and writing and how pixels are processed before being
placed in or after being read from the framebu er for reading, writing, and
copying. These parameters are set with three commands: PixelStore,
PixelTransfer, and PixelMap.
3.6.1 Pixel Storage Modes
Pixel storage modes a ect the operation of DrawPixels and ReadPixels
as well as other commands; see sections 3.5.2, 3.7, and 3.8 when one of




                                Version 1.2.1 - April 1, 1999
76                                          CHAPTER 3. RASTERIZATION

         Parameter Name          Type Initial Value Valid Range
        UNPACK SWAP BYTES       boolean   FALSE     TRUE FALSE
         UNPACK LSB FIRST       boolean   FALSE     TRUE FALSE
        UNPACK ROW LENGTH       integer     0           0; 1
         UNPACK SKIP ROWS       integer     0           0; 1
        UNPACK SKIP PIXELS      integer     0           0; 1
         UNPACK ALIGNMENT       integer     4         1,2,4,8
       UNPACK IMAGE HEIGHT      integer     0           0; 1
        UNPACK SKIP IMAGES      integer     0           0; 1
Table 3.1: PixelStore parameters pertaining to one or more of DrawPix-
els, TexImage1D, TexImage2D, and TexImage3D.

these commands is issued. This may di er from the time that the command
is executed if the command is placed in a display list see section 5.4. Pixel
storage modes are set with
     void   PixelStorefifg enum pname, T param ;
pname is a symbolic constant indicating a parameter to be set, and param
is the value to set it to. Table 3.1 summarizes the pixel storage parameters,
their types, their initial values, and their allowable ranges. Setting a param-
eter to a value outside the given range results in the error INVALID VALUE.
    The version of PixelStore that takes a oating-point value may be
used to set any type of parameter; if the parameter is boolean, then it
is set to FALSE if the passed value is 0:0 and TRUE otherwise, while if the
parameter is an integer, then the passed value is rounded to the nearest
integer. The integer version of the command may also be used to set any
type of parameter; if the parameter is boolean, then it is set to FALSE if the
passed value is 0 and TRUE otherwise, while if the parameter is a oating-
point value, then the passed value is converted to oating-point.
3.6.2 The Imaging Subset
Some pixel transfer and per-fragment operations are only made available in
GL implementations which incorporate the optional imaging subset. The
imaging subset includes both new commands, and new enumerants allowed
as parameters to existing commands. If the subset is supported, all of these




                     Version 1.2.1 - April 1, 1999
3.6. PIXEL RECTANGLES                                                      77

calls and enumerants must be implemented as described later in the GL spec-
i cation. If the subset is not supported, calling any of the new commands
generates the error INVALID OPERATION, and using any of the new enumerants
generates the error INVALID ENUM.
    The individual operations available only in the imaging subset are de-
scribed in section 3.6.3, except for blending features, which are described in
chapter 4. Imaging subset operations include:
   1. Color tables, including all commands and enumerants described in
       subsections Color Table Speci cation, Alternate Color Table
       Speci cation Commands, Color Table State and Proxy State,
       Color Table Lookup, Post Convolution Color Table Lookup,
       and Post Color Matrix Color Table Lookup, as well as the query
       commands described in section 6.1.7.
   2. Convolution, including all commands and enumerants described in
       subsections Convolution Filter Speci cation, Alternate Con-
       volution Filter Speci cation Commands, and Convolution, as
       well as the query commands described in section 6.1.8.
   3. Color matrix, including all commands and enumerants described in
       subsections Color Matrix Speci cation and Color Matrix Trans-
       formation, as well as the simple query commands described in sec-
       tion 6.1.6.
   4. Histogram and minmax, including all commands and enumerants de-
       scribed in subsections Histogram Table Speci cation, Histogram
       State and Proxy State, Histogram, Minmax Table Speci ca-
       tion, and Minmax, as well as the query commands described in sec-
       tion 6.1.9 and section 6.1.10.
   5. The subset of blending features described by Blend-
       Equation, BlendColor, and the BlendFunc modes
       CONSTANT COLOR, ONE MINUS CONSTANT COLOR,        CONSTANT ALPHA, and
       ONE MINUS CONSTANT ALPHA. These are described separately in sec-
       tion 4.1.6.
    The imaging subset is supported only if the EXTENSIONS string includes
the substring "ARB imaging". Querying EXTENSIONS is described in sec-
tion 6.1.11.
    If the imaging subset is not supported, the related pixel transfer opera-
tions are not performed; pixels are passed unchanged to the next operation.




                               Version 1.2.1 - April 1, 1999
78                                            CHAPTER 3. RASTERIZATION

           Parameter Name              Type Initial Value Valid Range
                MAP COLOR             boolean   FALSE     TRUE FALSE
               MAP STENCIL            boolean   FALSE     TRUE FALSE
               INDEX SHIFT            integer     0        ,1; 1
               INDEX OFFSET           integer     0        ,1; 1
                 x SCALE                 oat     1.0       ,1; 1
               DEPTH SCALE               oat     1.0       ,1; 1
                  x BIAS                 oat     0.0       ,1; 1
                DEPTH BIAS               oat     0.0       ,1; 1
       POST CONVOLUTION x SCALE          oat     1.0       ,1; 1
       POST CONVOLUTION x BIAS           oat     0.0       ,1; 1
      POST COLOR MATRIX x SCALE          oat     1.0       ,1; 1
       POST COLOR MATRIX x BIAS          oat     0.0       ,1; 1
     Table 3.2: PixelTransfer parameters. x is RED, GREEN, BLUE, or ALPHA.


3.6.3 Pixel Transfer Modes
Pixel transfer modes a ect the operation of DrawPixels section 3.6.4,
ReadPixels section 4.3.2, and CopyPixels section 4.3.3 at the time
when one of these commands is executed which may di er from the time
the command is issued. Some pixel transfer modes are set with
        void   PixelTransferfifg enum param, T value ;
param is a symbolic constant indicating a parameter to be set, and value is
the value to set it to. Table 3.2 summarizes the pixel transfer parameters
that are set with PixelTransfer, their types, their initial values, and their
allowable ranges. Setting a parameter to a value outside the given range
results in the error INVALID VALUE. The same versions of the command exist
as for PixelStore, and the same rules apply to accepting and converting
passed values to set parameters.
    The pixel map lookup tables are set with
        void   PixelMapfui us fgv enum map, sizei size, T values ;
map is a symbolic map name, indicating the map to set, size indicates the
size of the map, and values is a pointer to an array of size map values.




                       Version 1.2.1 - April 1, 1999
3.6. PIXEL RECTANGLES                                                       79

      Map Name           Address       Value    Init. Size Init. Value
   PIXEL MAP I TO I      color idx color idx         1         0.0
   PIXEL MAP S TO S     stencil idx stencil idx      1           0
   PIXEL MAP I TO R      color idx      R            1         0.0
   PIXEL MAP I TO G      color idx      G            1         0.0
   PIXEL MAP I TO B      color idx      B            1         0.0
   PIXEL MAP I TO A      color idx      A            1         0.0
   PIXEL MAP R TO R          R          R            1         0.0
   PIXEL MAP G TO G          G          G            1         0.0
   PIXEL MAP B TO B          B          B            1         0.0
   PIXEL MAP A TO A          A          A            1         0.0
                      Table 3.3: PixelMap parameters.

    The entries of a table may be speci ed using one of three types: single-
precision oating-point, unsigned short integer, or unsigned integer, depend-
ing on which of the three versions of PixelMap is called. A table entry is
converted to the appropriate type when it is speci ed. An entry giving a
color component value is converted according to table 2.6. An entry giving
a color index value is converted from an unsigned short integer or unsigned
integer to oating-point. An entry giving a stencil index is converted from
single-precision oating-point to an integer by rounding to nearest. The
various tables and their initial sizes and entries are summarized in table 3.3.
A table that takes an index as an address must have size = 2n or the error
INVALID VALUE results. The maximum allowable size of each table is speci ed
by the implementation dependent value MAX PIXEL MAP TABLE, but must be at
least 32 a single maximum applies to all tables. The error INVALID VALUE
is generated if a size larger than the implemented maximum, or less than
one, is given to PixelMap.
Color Table Speci cation
Color lookup tables are speci ed with
     void   ColorTable enum target, enum internalformat,
        sizei   width, enum format, enum type, void *data ;
target must be one of the regular color table names listed in table 3.4 to
de ne the table. A proxy table name is a special case discussed later in




                                Version 1.2.1 - April 1, 1999
80                                          CHAPTER 3. RASTERIZATION

                            Table Name                   Type
                            COLOR TABLE                 regular
                  POST CONVOLUTION COLOR TABLE
                  POST COLOR MATRIX COLOR TABLE
                         PROXY COLOR TABLE               proxy
               PROXY POST CONVOLUTION COLOR TABLE
               PROXY POST COLOR MATRIX COLOR TABLE

Table 3.4: Color table names. Regular tables have associated image data.
Proxy tables have no image data, and are used only to determine if an image
can be loaded into the corresponding regular table.


this section. width, format, type, and data specify an image in memory with
the same meaning and allowed values as the corresponding arguments to
DrawPixels see section 3.6.4, with height taken to be 1. The maximum
allowable width of a table is implementation-dependent, but must be at least
32. The formats COLOR INDEX, DEPTH COMPONENT, and STENCIL INDEX and the
type BITMAP are not allowed.
    The speci ed image is taken from memory and processed just as if
DrawPixels were called, stopping after the nal expansion to RGBA.
The R, G, B, and A components of each pixel are then scaled by the
four COLOR TABLE SCALE parameters, biased by the four COLOR TABLE BIAS pa-
rameters, and clamped to 0; 1 . These parameters are set by calling Col-
orTableParameterfv as described below.
    Components are then selected from the resulting R, G, B, and A values
to obtain a table with the base internal format speci ed by or derived
from internalformat, in the same manner as for textures section 3.8.1.
internalformat must be one of the formats in table 3.15 or table 3.16.
    The color lookup table is rede ned to have width entries, each with the
speci ed internal format. The table is formed with indices 0 through width,
1. Table location i is speci ed by the ith image pixel, counting from zero.
    The error INVALID VALUE is generated if width is not zero or a non-negative
power of two. The error TABLE TOO LARGE is generated if the speci ed color
lookup table is too large for the implementation.
    The scale and bias parameters for a table are speci ed by calling

     void   ColorTableParameterfifgv enum target,
        enum   pname, T params ;




                     Version 1.2.1 - April 1, 1999
3.6. PIXEL RECTANGLES                                                     81

target must be a regular color table name. pname is one of COLOR TABLE SCALE
or COLOR TABLE BIAS. params points to an array of four values: red, green,
blue, and alpha, in that order.
    A GL implementation may vary its allocation of internal component
resolution based on any ColorTable parameter, but the allocation must
not be a function of any other factor, and cannot be changed once it is
established. Allocations must be invariant; the same allocation must be
made each time a color table is speci ed with the same parameter values.
These allocation rules also apply to proxy color tables, which are described
later in this section.
Alternate Color Table Speci cation Commands
Color tables may also be speci ed using image data taken directly from the
framebu er, and portions of existing tables may be respeci ed.
   The command
     void   CopyColorTable enum target, enum internalformat,
        int x, int y, sizei    width ;
de nes a color table in exactly the manner of ColorTable, except that table
data are taken from the framebu er, rather than from client memory. target
must be a regular color table name. x, y, and width correspond precisely to
the corresponding arguments of CopyPixels refer to section 4.3.3; they
specify the image's width and the lower left x; y coordinates of the frame-
bu er region to be copied. The image is taken from the framebu er exactly
as if these arguments were passed to CopyPixels with argument type set
to COLOR and height set to 1, stopping after the nal expansion to RGBA.
    Subsequent processing is identical to that described for ColorTable, be-
ginning with scaling by COLOR TABLE SCALE. Parameters target, internalfor-
mat and width are speci ed using the same values, with the same meanings,
as the equivalent arguments of ColorTable. format is taken to be RGBA.
    Two additional commands,
     void   ColorSubTable  enum target, sizei start,
        sizei count, enum format, enum type, void *data ;
     void   CopyColorSubTable    enum target, sizei start,
        int x, int y, sizei count ;

respecify only a portion of an existing color table. No change is made to the
internalformat or width parameters of the speci ed color table, nor is any




                               Version 1.2.1 - April 1, 1999
82                                          CHAPTER 3. RASTERIZATION

change made to table entries outside the speci ed portion. target must be a
regular color table name.
    ColorSubTable arguments format, type, and data match the corre-
sponding arguments to ColorTable, meaning that they are speci ed using
the same values, and have the same meanings. Likewise, CopyColorSub-
Table arguments x, y, and count match the x, y, and width arguments of
CopyColorTable. Both of the ColorSubTable commands interpret and
process pixel groups in exactly the manner of their ColorTable counter-
parts, except that the assignment of R, G, B, and A pixel group values to
the color table components is controlled by the internalformat of the table,
not by an argument to the command.
    Arguments start and count of ColorSubTable and CopyColorSub-
Table specify a subregion of the color table starting at index start and
ending at index start + count , 1. Counting from zero, the nth pixel group
is assigned to the table entry with index count + n. The error INVALID VALUE
is generated if start + count width.

Color Table State and Proxy State
The state necessary for color tables can be divided into two categories. For
each of the three tables, there is an array of values. Each array has associated
with it a width, an integer describing the internal format of the table, six
integer values describing the resolutions of each of the red, green, blue, alpha,
luminance, and intensity components of the table, and two groups of four
  oating-point numbers to store the table scale and bias. Each initial array
is null zero width, internal format RGBA, with zero-sized components. The
initial value of the scale parameters is 1,1,1,1 and the initial value of the
bias parameters is 0,0,0,0.
    In addition to the color lookup tables, partially instantiated proxy color
lookup tables are maintained. Each proxy table includes width and internal
format state values, as well as state for the red, green, blue, alpha, lumi-
nance, and intensity component resolutions. Proxy tables do not include
image data, nor do they include scale and bias parameters. When Col-
orTable is executed with target speci ed as one of the proxy color table
names listed in table 3.4, the proxy state values of the table are recomputed
and updated. If the table is too large, no error is generated, but the proxy
format, width and component resolutions are set to zero. If the color table
would be accommodated by ColorTable called with target set to the corre-
sponding regular table name COLOR TABLE is the regular name corresponding
to PROXY COLOR TABLE, for example, the proxy state values are set exactly as




                     Version 1.2.1 - April 1, 1999
3.6. PIXEL RECTANGLES                                                            83

though the regular table were being speci ed. Calling ColorTable with a
proxy target has no e ect on the image or state of any actual color table.
   There is no image associated with any of the proxy targets. They can-
not be used as color tables, and they must never be queried using GetCol-
orTable. The error INVALID ENUM is generated if this is attempted.
Convolution Filter Speci cation
A two-dimensional convolution lter image is speci ed by calling
     void   ConvolutionFilter2D enum target,
        enum   internalformat, sizei width, sizei height,
        enum   format, enum type, void *data ;
target must be CONVOLUTION 2D. width, height, format, type, and data spec-
ify an image in memory with the same meaning and allowed values as
the corresponding parameters to DrawPixels. The formats COLOR INDEX,
DEPTH COMPONENT, and STENCIL INDEX and the type BITMAP are not allowed.
    The speci ed image is extracted from memory and processed just as
if DrawPixels were called, stopping after the nal expansion to RGBA.
The R, G, B, and A components of each pixel are then scaled by the four
two-dimensional CONVOLUTION FILTER SCALE parameters and biased by the
four two-dimensional CONVOLUTION FILTER BIAS parameters. These parame-
ters are set by calling ConvolutionParameterfv as described below. No
clamping takes place at any time during this process.
    Components are then selected from the resulting R, G, B, and A values
to obtain a table with the base internal format speci ed by or derived
from internalformat, in the same manner as for textures section 3.8.1.
internalformat must be one of the formats in table 3.15 or table 3.16.
    The red, green, blue, alpha, luminance, and or intensity components of
the pixels are stored in oating point, rather than integer format. They form
a two-dimensional image indexed with coordinates i; j such that i increases
from left to right, starting at zero, and j increases from bottom to top, also
starting at zero. Image location i; j is speci ed by the N th pixel, counting
from zero, where
                               N = i + j  width
    The error INVALID VALUE is generated if width or height is greater than
the maximum supported value. These values are queried with GetCon-
volutionParameteriv, setting target to CONVOLUTION 2D and pname to
MAX CONVOLUTION WIDTH or MAX CONVOLUTION HEIGHT, respectively.




                               Version 1.2.1 - April 1, 1999
84                                          CHAPTER 3. RASTERIZATION

   The scale and bias parameters for a two-dimensional lter are speci ed
by calling
      void    ConvolutionParameterfifgv enum target,
         enum   pname, T params ;
with target   CONVOLUTION 2D. pname is one of CONVOLUTION FILTER SCALE or
CONVOLUTION FILTER BIAS  . params points to an array of four values: red,
green, blue, and alpha, in that order.
   A one-dimensional convolution lter is de ned using
      void    ConvolutionFilter1D enum target,
         enum   internalformat, sizei width, enum format,
         enum   type, void *data ;
target must be CONVOLUTION 1D. internalformat, width, format, and type have
identical semantics and accept the same values as do their two-dimensional
counterparts. data must point to a one-dimensional image, however.
    The image is extracted from memory and processed as if Con-
volutionFilter2D were called with a height of 1, except that it is
scaled and biased by the one-dimensional CONVOLUTION FILTER SCALE and
CONVOLUTION FILTER BIAS parameters. These parameters are speci ed ex-
actly as the two-dimensional parameters, except that ConvolutionParam-
eterfv is called with target CONVOLUTION 1D.
    The image is formed with coordinates i such that i increases from left to
right, starting at zero. Image location i is speci ed by the ith pixel, counting
from zero.
    The error INVALID VALUE is generated if width is greater than the
maximum supported value. This value is queried using GetConvo-
lutionParameteriv, setting target to CONVOLUTION 1D and pname to
MAX CONVOLUTION WIDTH.
    Special facilities are provided for the de nition of two-dimensional sep-
arable lters lters whose image can be represented as the product of
two one-dimensional images, rather than as full two-dimensional images. A
two-dimensional separable convolution lter is speci ed with
      void    SeparableFilter2D enum target, enum internalformat,
         sizei width, sizei height, enum format, enum type,
         void *row, void *column ;




                     Version 1.2.1 - April 1, 1999
3.6. PIXEL RECTANGLES                                                        85

target must be SEPARABLE 2D. internalformat speci es the formats of the table
entries of the two one-dimensional images that will be retained. row points
to a width pixel wide image of the speci ed format and type. column points
to a height pixel high image, also of the speci ed format and type.
    The two images are extracted from memory and processed as if
ConvolutionFilter1D were called separately for each, except that
each image is scaled and biased by the two-dimensional separable
CONVOLUTION FILTER SCALE and CONVOLUTION FILTER BIAS parameters. These
parameters are speci ed exactly as the one-dimensional and two-dimensional
parameters, except that ConvolutionParameteriv is called with target
SEPARABLE 2D.


Alternate Convolution Filter Speci cation Commands
One and two-dimensional lters may also be speci ed using image data taken
directly from the framebu er.
    The command
      void  CopyConvolutionFilter2D      enum target,
         enum internalformat, int x, int y, sizei width,
         sizei height ;

de nes a two-dimensional lter in exactly the manner of ConvolutionFil-
ter2D, except that image data are taken from the framebu er, rather than
from client memory. target must be CONVOLUTION 2D. x, y, width, and height
correspond precisely to the corresponding arguments of CopyPixels refer
to section 4.3.3; they specify the image's width and height, and the lower left
x; y coordinates of the framebu er region to be copied. The image is taken
from the framebu er exactly as if these arguments were passed to CopyP-
ixels with argument type set to COLOR, stopping after the nal expansion to
RGBA.
    Subsequent processing is identical to that described for Convolution-
Filter2D, beginning with scaling by CONVOLUTION FILTER SCALE. Parameters
target, internalformat, width, and height are speci ed using the same values,
with the same meanings, as the equivalent arguments of ConvolutionFil-
ter2D. format is taken to be RGBA.
    The command
      void  CopyConvolutionFilter1D enum target,
         enum   internalformat, int x, int y, sizei width ;




                                Version 1.2.1 - April 1, 1999
86                                                    CHAPTER 3. RASTERIZATION

de nes a one-dimensional lter in exactly the manner of ConvolutionFil-
ter1D, except that image data are taken from the framebu er, rather than
from client memory. target must be CONVOLUTION 1D. x, y, and width cor-
respond precisely to the corresponding arguments of CopyPixels refer to
section 4.3.3; they specify the image's width and the lower left x; y co-
ordinates of the framebu er region to be copied. The image is taken from
the framebu er exactly as if these arguments were passed to CopyPixels
with argument type set to COLOR and height set to 1, stopping after the nal
expansion to RGBA.
    Subsequent processing is identical to that described for Convolution-
Filter1D, beginning with scaling by CONVOLUTION FILTER SCALE. Parameters
target, internalformat, and width are speci ed using the same values, with
the same meanings, as the equivalent arguments of ConvolutionFilter2D.
format is taken to be RGBA.
Convolution Filter State
The required state for convolution lters includes a one-dimensional image
array, two one-dimensional image arrays for the separable lter, and a two-
dimensional image array. The two-dimensional array has associated with
it a height. Each array has associated with it a width, an integer describ-
ing the internal format of the table, and six integer values describing the
resolutions of each of the red, green, blue, alpha, luminance, and intensity
components of the table. Each lter one-dimensional, two-dimensional,
and two-dimensional separable also has associated with it two groups of
four oating-point numbers to store the lter scale and bias.
    Each initial convolution lter is null zero width and height, internal
format RGBA, with zero-sized components. The initial value of all scale
parameters is 1,1,1,1 and the initial value of all bias parameters is 0,0,0,0.

Color Matrix Speci cation
Setting the matrix mode to COLOR causes the matrix operations described
in section 2.10.2 to apply to the top matrix on the color matrix stack. All
matrix operations have the same e ect on the color matrix as they do on
the other matrices.
Histogram Table Speci cation
The histogram table is speci ed with




                      Version 1.2.1 - April 1, 1999
3.6. PIXEL RECTANGLES                                                       87

     void   Histogram enum target, sizei width,
        enum   internalformat, boolean sink ;
target must be HISTOGRAM if a histogram table is to be speci ed. target
value PROXY HISTOGRAM is a special case discussed later in this section. width
speci es the number of entries in the histogram table, and internalformat
speci es the format of each table entry. The maximum allowable width of the
histogram table is implementation-dependent, but must be at least 32. sink
speci es whether pixel groups will be consumed by the histogram operation
TRUE or passed on to the minmax operation FALSE.
    If no error results from the execution of Histogram, the speci ed his-
togram table is rede ned to have width entries, each with the speci ed inter-
nal format. The entries are indexed 0 through width , 1. Each component
in each entry is set to zero. The values in the previous histogram table, if
any, are lost.
    The error INVALID VALUE is generated if width is not zero or a non-negative
power of 2. The error TABLE TOO LARGE is generated if the speci ed histogram
table is too large for the implementation. The error INVALID ENUM is gener-
ated if internalformat is not one of the values accepted by the correspond-
ing parameter of TexImage2D, or is 1, 2, 3, 4, INTENSITY, INTENSITY4,
INTENSITY8, INTENSITY12, or INTENSITY16.
    A GL implementation may vary its allocation of internal component
resolution based on any Histogram parameter, but the allocation must
not be a function of any other factor, and cannot be changed once it is
established. In particular, allocations must be invariant; the same allocation
must be made each time a histogram is speci ed with the same parameter
values. These allocation rules also apply to the proxy histogram, which is
described later in this section.

Histogram State and Proxy State
The state necessary for histogram operation is an array of values, with which
is associated a width, an integer describing the internal format of the his-
togram, ve integer values describing the resolutions of each of the red,
green, blue, alpha, and luminance components of the table, and a ag in-
dicating whether or not pixel groups are consumed by the operation. The
initial array is null zero width, internal format RGBA, with zero-sized com-
ponents. The initial value of the ag is false.
    In addition to the histogram table, a partially instantiated proxy his-
togram table is maintained. It includes width, internal format, and red,




                                Version 1.2.1 - April 1, 1999
88                                                  CHAPTER 3. RASTERIZATION

green, blue, alpha, and luminance component resolutions. The proxy table
does not include image data or the ag. When Histogram is executed
with target set to PROXY HISTOGRAM, the proxy state values are recomputed
and updated. If the histogram array is too large, no error is generated, but
the proxy format, width, and component resolutions are set to zero. If the
histogram table would be accomodated by Histogram called with target
set to HISTOGRAM, the proxy state values are set exactly as though the ac-
tual histogram table were being speci ed. Calling Histogram with target
PROXY HISTOGRAM has no e ect on the actual histogram table.
    There is no image associated with PROXY HISTOGRAM. It cannot be used as
a histogram, and its image must never queried using GetHistogram. The
error INVALID ENUM results if this is attempted.
Minmax Table Speci cation
The minmax table is speci ed with
     void   Minmax enum target, enum internalformat,
        boolean   sink ;
target must be MINMAX. internalformat speci es the format of the table en-
tries. sink speci es whether pixel groups will be consumed by the minmax
operation TRUE or passed on to nal conversion FALSE.
    The error INVALID ENUM is generated if internalformat is not one of the
values accepted by the corresponding parameter of TexImage2D, or is 1, 2,
3, 4, INTENSITY, INTENSITY4, INTENSITY8, INTENSITY12, or INTENSITY16. The
resulting table always has 2 entries, each with values corresponding only to
the components of the internal format.
    The state necessary for minmax operation is a table containing two el-
ements the rst element stores the minimum values, the second stores the
maximum values, an integer describing the internal format of the table, and
a ag indicating whether or not pixel groups are consumed by the operation.
The initial state is a minimum table entry set to the maximum representable
value and a maximum table entry set to the minimum representable value.
Internal format is set to RGBA and the initial value of the ag is false.
3.6.4 Rasterization of Pixel Rectangles
The process of drawing pixels encoded in host memory is diagrammed in
 gure 3.7. We describe the stages of this process in the order in which they
occur.




                    Version 1.2.1 - April 1, 1999
3.6. PIXEL RECTANGLES                                                                    89


          byte, short, int, or float pixel
       data stream (index or component)


                                                 unpack

                              RGBA, L                                            color
                                                                                 index
                       convert
                       to float              Pixel Storage
                                              Operations

                       convert
                      L to RGB




                        scale                Pixel Transfer                 shift
                       and bias               Operations                  and offset



                   RGBA to RGBA               index to RGBA             index to index
                      lookup                      lookup                   lookup



                     color table
                       lookup



                     convolution               color table          post
                    scale and bias               lookup         color matrix



     post            color table                histogram
  convolution          lookup



                     color matrix                minmax
                    scale and bias




                        clamp                     final                    mask to
                       to [0,1]                conversion                  (2n − 1)

          RGBA pixel                                         color index pixel
           data out                                              data out



  Figure 3.7. Operation of DrawPixels. Output is RGBA pixels if the GL
  is in RGBA mode, color index pixels otherwise. Operations in dashed boxes
  may be enabled or disabled. RGBA and color index pixel paths are shown;
  depth and stencil pixel paths are not shown.




                                     Version 1.2.1 - April 1, 1999
90                                           CHAPTER 3. RASTERIZATION

     Pixels are drawn using
       void  DrawPixels sizei width, sizei height, enum format,
          enum   type, void *data ;
format is a symbolic constant indicating what the values in memory repre-
sent. width and height are the width and height, respectively, of the pixel
rectangle to be drawn. data is a pointer to the data to be drawn. These
data are represented with one of seven GL data types, speci ed by type.
The correspondence between the twenty type token values and the GL data
types they indicate is given in table 3.5. If the GL is in color index mode
and format is not one of COLOR INDEX, STENCIL INDEX, or DEPTH COMPONENT,
then the error INVALID OPERATION occurs. If type is BITMAP and format is
not COLOR INDEX or STENCIL INDEX then the error INVALID ENUM occurs. Some
additional constraints on the combinations of format and type values that
are accepted is discussed below.

Unpacking
Data are taken from host memory as a sequence of signed or unsigned bytes
GL data types byte and ubyte, signed or unsigned short integers GL data
types short and ushort, signed or unsigned integers GL data types int
and uint, or oating point values GL data type float. These elements
are grouped into sets of one, two, three, or four values, depending on the
format, to form a group. Table 3.6 summarizes the format of groups obtained
from memory; it also indicates those formats that yield indices and those
that yield components.
    By default the values of each GL data type are interpreted as they would
be speci ed in the language of the client's GL binding. If UNPACK SWAP BYTES
is enabled, however, then the values are interpreted with the bit orderings
modi ed as per table 3.7. The modi ed bit orderings are de ned only if the
GL data type ubyte has eight bits, and then for each speci c GL data type
only if that type is represented with 8, 16, or 32 bits.
    The groups in memory are treated as being arranged in a rectangle. This
rectangle consists of a series of rows, with the rst element of the rst group
of the rst row pointed to by the pointer passed to DrawPixels. If the
value of UNPACK ROW LENGTH is not positive, then the number of groups in
a row is width; otherwise the number of groups is UNPACK ROW LENGTH. If p
indicates the location in memory of the rst element of the rst row, then
the rst element of the N th row is indicated by




                      Version 1.2.1 - April 1, 1999
3.6. PIXEL RECTANGLES                                                   91




             type Parameter             Corresponding    Special
              Token Name                GL Data Type Interpretation
             UNSIGNED BYTE                  ubyte          No
                 BITMAP                     ubyte         Yes
                  BYTE                      byte           No
             UNSIGNED SHORT                ushort          No
                 SHORT                      short          No
              UNSIGNED INT                  uint           No
                  INT                        int           No
                 FLOAT                      float          No
          UNSIGNED BYTE 3 3 2               ubyte         Yes
        UNSIGNED BYTE 2 3 3 REV             ubyte         Yes
          UNSIGNED SHORT 5 6 5             ushort         Yes
        UNSIGNED SHORT 5 6 5 REV           ushort         Yes
         UNSIGNED SHORT 4 4 4 4            ushort         Yes
       UNSIGNED SHORT 4 4 4 4 REV          ushort         Yes
         UNSIGNED SHORT 5 5 5 1            ushort         Yes
       UNSIGNED SHORT 1 5 5 5 REV          ushort         Yes
          UNSIGNED INT 8 8 8 8              uint          Yes
        UNSIGNED INT 8 8 8 8 REV            uint          Yes
        UNSIGNED INT 10 10 10 2             uint          Yes
      UNSIGNED INT 2 10 10 10 REV           uint          Yes
Table 3.5: DrawPixels and ReadPixels type parameter values and the
corresponding GL data types. Refer to table 2.2 for de nitions of GL data
types. Special interpretations are described near the end of section 3.6.4.




                                 Version 1.2.1 - April 1, 1999
92                                          CHAPTER 3. RASTERIZATION



      Format Name         Element Meaning and Order Target Bu er
       COLOR INDEX               Color Index           Color
      STENCIL INDEX             Stencil Index          Stencil
     DEPTH COMPONENT                Depth              Depth
            RED                       R                Color
           GREEN                      G                Color
           BLUE                       B                Color
           ALPHA                      A                Color
            RGB                    R, G, B             Color
           RGBA                   R, G, B, A           Color
            BGR                    B, G, R             Color
           BGRA                   B, G, R, A           Color
        LUMINANCE                 Luminance            Color
     LUMINANCE ALPHA            Luminance, A           Color
Table 3.6: DrawPixels and ReadPixels formats. The second column gives
a description of and the number and order of elements in a group. Unless
speci ed as an index, formats yield components.




     Element Size Default Bit Ordering               Modi ed Bit Ordering
         8 bit    7::0                               7::0
        16 bit    15::0                              7::0 15::8
        32 bit    31::0                              7::0 15::8 23::16 31::24
Table 3.7: Bit ordering modi cation of elements when UNPACK SWAP BYTES is
enabled. These reorderings are de ned only when GL data type ubyte has
8 bits, and then only for GL data types with 8, 16, or 32 bits. Bit 0 is the
least signi cant.




                     Version 1.2.1 - April 1, 1999
3.6. PIXEL RECTANGLES                                                       93



                                   ROW_LENGTH



                                  subimage

               SKIP_PIXELS


                             SKIP_ROWS




  Figure 3.8. Selecting a subimage from an image. The indicated parameter
  names are pre xed by UNPACK for DrawPixels and by PACK for ReadPix-
  els.



                                    p + Nk                         3.8
   where N is the row number counting from zero and k is de ned as
                             
                         k = nl             s  a;                       3.9
                                a=s dsnl=ae s a
    where n is the number of elements in a group, l is the number of groups
in the row, a is the value of UNPACK ALIGNMENT, and s is the size, in units of
GL ubytes, of an element. If the number of bits per element is not 1, 2, 4,
or 8 times the number of bits in a GL ubyte, then k = nl for all values of a.
    There is a mechanism for selecting a sub-rectangle of groups from a
larger containing rectangle. This mechanism relies on three integer param-
eters: UNPACK ROW LENGTH, UNPACK SKIP ROWS, and UNPACK SKIP PIXELS. Before
obtaining the rst group from memory, the pointer supplied to DrawPixels
is e ectively advanced by UNPACK SKIP PIXELSn + UNPACK SKIP ROWSk ele-
ments. Then width groups are obtained from contiguous elements in memory
without advancing the pointer, after which the pointer is advanced by k
elements. height sets of width groups of values are obtained this way. See
  gure 3.8.
    Calling DrawPixels with a type of UNSIGNED BYTE 3 3 2,
UNSIGNED BYTE 2 3 3 REV, UNSIGNED SHORT 5 6 5, UNSIGNED SHORT 5 6 5 REV,




                                 Version 1.2.1 - April 1, 1999
94                                           CHAPTER 3. RASTERIZATION

          type Parameter            GL Data Number of  Matching
           Token Name                Type Components Pixel Formats
        UNSIGNED BYTE 3 3 2          ubyte     3          RGB
      UNSIGNED BYTE 2 3 3 REV        ubyte     3          RGB
       UNSIGNED SHORT 5 6 5         ushort     3          RGB
     UNSIGNED SHORT 5 6 5 REV       ushort     3          RGB
      UNSIGNED SHORT 4 4 4 4        ushort     4       RGBA,BGRA
     UNSIGNED SHORT 4 4 4 4 REV     ushort     4       RGBA,BGRA
      UNSIGNED SHORT 5 5 5 1        ushort     4       RGBA,BGRA
     UNSIGNED SHORT 1 5 5 5 REV     ushort     4       RGBA,BGRA
        UNSIGNED INT 8 8 8 8          uint     4       RGBA,BGRA
      UNSIGNED INT 8 8 8 8 REV        uint     4       RGBA,BGRA
      UNSIGNED INT 10 10 10 2         uint     4       RGBA,BGRA
 UNSIGNED INT 2 10 10 10 REV          uint     4       RGBA,BGRA

                       Table 3.8: Packed pixel formats.


                        ,                             ,
UNSIGNED SHORT 4 4 4 4 UNSIGNED SHORT 4 4 4 4 REV UNSIGNED SHORT 5 5 5 1     ,
UNSIGNED SHORT 1 5 5 5 REV, UNSIGNED INT 8 8 8 8, UNSIGNED INT 8 8 8 8 REV,
UNSIGNED INT 10 10 10 2, or UNSIGNED INT 2 10 10 10 REV is a special case in
which all the components of each group are packed into a single unsigned
byte, unsigned short, or unsigned int, depending on the type. The number of
components per packed pixel is xed by the type, and must match the num-
ber of components per group indicated by the format parameter, as listed in
table 3.8. The error INVALID OPERATION is generated if a mismatch occurs.
This constraint also holds for all other functions that accept or return pixel
data using type and format parameters to de ne the type and format of that
data.
    Bit eld locations of the rst, second, third, and fourth components of
each packed pixel type are illustrated in tables 3.9, 3.10, and 3.11. Each
bit eld is interpreted as an unsigned integer value. If the base GL type is
supported with more than the minimum precision e.g. a 9-bit byte the
packed components are right-justi ed in the pixel.
    Components are normally packed with the rst component in the most
signi cant bits of the bit eld, and successive component occupying progres-
sively less signi cant locations. Types whose token names end with REV
reverse the component packing order from least to most signi cant loca-
tions. In all cases, the most signi cant bit of each component is packed in




                      Version 1.2.1 - April 1, 1999
3.6. PIXEL RECTANGLES                                                           95

the most signi cant bit location of its location in the bit eld.
UNSIGNED BYTE 3 3 2:

                     7          6     5      4      3     2       1         0

                          1st Component             2nd               3rd



UNSIGNED BYTE 2 3 3 REV     :
                      7           6   5       4     3     2       1         0

                            3rd               2nd             1st Component

Table 3.9:   UNSIGNED BYTE        formats. Bit numbers are indicated for each com-
ponent.




                                          Version 1.2.1 - April 1, 1999
96                                                                                CHAPTER 3. RASTERIZATION




UNSIGNED SHORT 5 6 5                :
     15     14          13    12    11        10             9    8           7     6         5   4     3       2            1   0

              1st Component                                             2nd                                      3rd



UNSIGNED SHORT 5 6 5 REV                      :
     15     14          13    12    11        10             9    8           7     6         5   4     3       2            1   0

                        3rd                                             2nd                                 1st Component



UNSIGNED SHORT 4 4 4 4                    :
     15     14          13    12    11        10             9    8           7     6         5   4     3       2            1   0

           1st Component                           2nd                                  3rd                            4th



UNSIGNED SHORT 4 4 4 4 REV                         :
     15     14          13    12    11        10             9    8           7     6         5   4     3       2            1   0

                  4th                                  3rd                              2nd                    1st Component



UNSIGNED SHORT 5 5 5 1                    :
     15     14          13    12    11        10             9    8           7     6         5   4     3       2            1   0

              1st Component                                       2nd                                   3rd                      4th



UNSIGNED SHORT 1 5 5 5 REV                         :
     15      14         13    12     11       10             9     8          7     6         5   4     3        2           1   0

     4th                      3rd                                             2nd                           1st Component

                                    Table 3.10:                  UNSIGNED SHORT               formats




                                    Version 1.2.1 - April 1, 1999
3.6. PIXEL RECTANGLES                                                                                                               97




UNSIGNED INT 8 8 8 8           :
  31 30 29 28 27 26 25 24 23 22 21 20 19 18 17 16 15 14 13 12 11 10 9      8     7     6       5    4     3       2   1     0

         1st Component                     2nd                    3rd                                   4th



UNSIGNED INT 8 8 8 8 REV               :
  31 30 29 28 27 26 25 24 23 22 21 20 19 18 17 16 15 14 13 12 11 10 9      8     7     6       5    4     3       2   1     0

              4th                          3rd                   2nd                           1st Component



UNSIGNED INT 10 10 10 2            :
  31 30 29 28 27 26 25 24 23 22 21 20 19 18 17 16 15 14 13 12 11 10 9      8     7     6       5    4     3       2   1     0

            1st Component                           2nd                              3rd                                  4th



UNSIGNED INT 2 10 10 10 REV                :
  31 30 29 28 27 26 25 24 23 22 21 20 19 18 17 16 15 14 13 12 11 10 9       8    7         6    5   4         3   2   1         0

   4th                   3rd                              2nd                          1st Component

                               Table 3.11:         UNSIGNED INT     formats




                                                 Version 1.2.1 - April 1, 1999
98                                         CHAPTER 3. RASTERIZATION

     Format       First     Second    Third     Fourth
                Component Component Component Component
       RGB         red       green    blue
       RGBA        red       green    blue       alpha
       BGRA       blue       green     red       alpha
                Table 3.12: Packed pixel eld assignments


    The assignment of component to elds in the packed pixel is as described
in table 3.12
    Byte swapping, if enabled, is performed before the component are ex-
tracted from each pixel. The above discussions of row length and image
extraction are valid for packed pixels, if group" is substituted for compo-
nent" and the number of components per group is understood to be one.
    Calling DrawPixels with a type of BITMAP is a special case in which the
data are a series of GL ubyte values. Each ubyte value speci es 8 1-bit ele-
ments with its 8 least-signi cant bits. The 8 single-bit elements are ordered
from most signi cant to least signi cant if the value of UNPACK LSB FIRST is
FALSE; otherwise, the ordering is from least signi cant to most signi cant.
The values of bits other than the 8 least signi cant in each ubyte are not
signi cant.
    The rst element of the rst row is the rst bit as de ned above of the
ubyte pointed to by the pointer passed to DrawPixels. The rst element
of the second row is the rst bit again as de ned above of the ubyte at
location p + k, where k is computed as

                                        
                                  k = a 8la                           3.10

    There is a mechanism for selecting a sub-rectangle of elements from
a BITMAP image as well. Before obtaining the rst element from mem-
ory, the pointer supplied to DrawPixels is e ectively advanced by
UNPACK SKIP ROWS  k ubytes. Then UNPACK SKIP PIXELS 1-bit elements are
ignored, and the subsequent width 1-bit elements are obtained, without ad-
vancing the ubyte pointer, after which the pointer is advanced by k ubytes.
height sets of width elements are obtained this way.




                    Version 1.2.1 - April 1, 1999
3.6. PIXEL RECTANGLES                                                      99

Conversion to oating-point
This step applies only to groups of components. It is not performed on in-
dices. Each element in a group is converted to a oating-point value accord-
ing to the appropriate formula in table 2.6 section 2.13. For packed pixel
types, each element in the group is converted by computing c = 2N , 1,
where c is the unsigned integer value of the bit eld containing the element
and N is the number of bits in the bit eld.

Conversion to RGB
This step is applied only if the format is LUMINANCE or LUMINANCE ALPHA. If
the format is LUMINANCE, then each group of one element is converted to a
group of R, G, and B three elements by copying the original single element
into each of the three new elements. If the format is LUMINANCE ALPHA, then
each group of two elements is converted to a group of R, G, B, and A four
elements by copying the rst original element into each of the rst three
new elements and copying the second original element to the A fourth
new element.

Final Expansion to RGBA
This step is performed only for non-depth component groups. Each group
is converted to a group of 4 elements as follows: if a group does not contain
an A element, then A is added and set to 1.0. If any of R, G, or B is missing
from the group, each missing element is added and assigned a value of 0.0.

Pixel Transfer Operations
This step is actually a sequence of steps. Because the pixel transfer opera-
tions are performed equivalently during the drawing, copying, and reading of
pixels, and during the speci cation of texture images either from memory or
from the framebu er, they are described separately in section 3.6.5. After
the processing described in that section is completed, groups are processed
as described in the following sections.

Final Conversion
For a color index, nal conversion consists of masking the bits of the index
to the left of the binary point by 2n , 1, where n is the number of bits in an
index bu er. For RGBA components, each element is clamped to 0; 1 . The




                               Version 1.2.1 - April 1, 1999
100                                         CHAPTER 3. RASTERIZATION

resulting values are converted to xed-point according to the rules given in
section 2.13.9 Final Color Processing.
    For a depth component, an element is rst clamped to 0; 1 and then
converted to xed-point as if it were a window z value see section 2.10.1,
Controlling the Viewport.
    Stencil indices are masked by 2n , 1, where n is the number of bits in
the stencil bu er.
Conversion to Fragments
The conversion of a group to fragments is controlled with
      void   PixelZoom float zx, float zy ;
Let xrp ; yrp  be the current raster position section 2.12. If the current
raster position is invalid, then DrawPixels is ignored; pixel transfer opera-
tions do not update the histogram or minmax tables, and no fragments are
generated. However, the histogram and minmax tables are updated even if
the corresponding fragments are later rejected by the pixel ownership sec-
tion 4.1.1 or scissor section 4.1.2 tests. If a particular group index or
components is the nth in a row and belongs to the mth row, consider the
region in window coordinates bounded by the rectangle with corners
   xrp + zx n; yrp + zy m     and       xrp + zx n + 1; yrp + zy m + 1
either zx or zy may be negative. Any fragments whose centers lie inside
of this rectangle or on its bottom or left boundaries are produced in cor-
respondence with this particular group of elements.
    A fragment arising from a group consisting of color data takes on the
color index or color components of the group; the depth and texture coordi-
nates are taken from the current raster position's associated data. A frag-
ment arising from a depth component takes the component's depth value;
the color and texture coordinates are given by those associated with the
current raster position. In both cases texture coordinates s, t, and r are re-
placed with s=q, t=q, and r=q, respectively. If q is less than or equal to zero,
the results are unde ned. Groups arising from DrawPixels with a format
of STENCIL INDEX are treated specially and are described in section 4.3.1.
3.6.5 Pixel Transfer Operations
The GL de nes four kinds of pixel groups:




                     Version 1.2.1 - April 1, 1999
3.6. PIXEL RECTANGLES                                                        101

   1. RGBA component: Each group comprises four color components: red,
      green, blue, and alpha.
   2. Depth component: Each group comprises a single depth component.
   3. Color index: Each group comprises a single color index.
   4. Stencil index: Each group comprises a single stencil index.
Each operation described in this section is applied sequentially to each pixel
group in an image. Many operations are applied only to pixel groups of
certain kinds; if an operation is not applicable to a given group, it is skipped.
Arithmetic on Components
This step applies only to RGBA component and depth component groups.
Each component is multiplied by an appropriate signed scale factor:
RED SCALE for an R component, GREEN SCALE for a G component, BLUE SCALE
for a B component, and ALPHA SCALE for an A component, or DEPTH SCALE
for a depth component. Then the result is added to the appropriate signed
bias: RED BIAS, GREEN BIAS, BLUE BIAS, ALPHA BIAS, or DEPTH BIAS.
Arithmetic on Indices
This step applies only to color index and stencil index groups. If the in-
dex is a oating-point value, it is converted to xed-point, with an un-
speci ed number of bits to the right of the binary point and at least
dlog2MAX PIXEL MAP TABLEe bits to the left of the binary point. Indices that
are already integers remain so; any fraction bits in the resulting xed-point
value are zero.
    The xed-point index is then shifted by jINDEX SHIFTj bits, left if
INDEX SHIFT     0 and right otherwise. In either case the shift is zero- lled.
Then, the signed integer o set INDEX OFFSET is added to the index.
RGBA to RGBA Lookup
This step applies only to RGBA component groups, and is skipped if
MAP COLOR is FALSE. First, each component is clamped to the range 0; 1 .
There is a table associated with each of the R, G, B, and A component
elements: PIXEL MAP R TO R for R, PIXEL MAP G TO G for G, PIXEL MAP B TO B
for B, and PIXEL MAP A TO A for A. Each element is multiplied by an integer
one less than the size of the corresponding table, and, for each element, an




                                 Version 1.2.1 - April 1, 1999
102                                        CHAPTER 3. RASTERIZATION

address is found by rounding this value to the nearest integer. For each ele-
ment, the addressed value in the corresponding table replaces the element.
Color Index Lookup
This step applies only to color index groups. If the GL command that
invokes the pixel transfer operation requires that RGBA component pixel
groups be generated, then a conversion is performed at this step. RGBA
component pixel groups are required if
   1. The groups will be rasterized, and the GL is in RGBA mode, or
   2. The groups will be loaded as an image into texture memory, or
   3. The groups will be returned to client memory with a format other than
       COLOR INDEX.

If RGBA component groups are required, then the integer part of the in-
dex is used to reference 4 tables of color components: PIXEL MAP I TO R,
PIXEL MAP I TO G, PIXEL MAP I TO B, and PIXEL MAP I TO A. Each of these ta-
bles must have 2n entries for some integer value of n n may be di erent
for each table. For each table, the index is rst rounded to the nearest
integer; the result is ANDed with 2n , 1, and the resulting value used as an
address into the table. The indexed value becomes an R, G, B, or A value,
as appropriate. The group of four elements so obtained replaces the index,
changing the group's type to RGBA component.
    If RGBA component groups are not required, and if MAP COLOR is enabled,
then the index is looked up in the PIXEL MAP I TO I table otherwise, the
index is not looked up. Again, the table must have 2n entries for some
integer n. The index is rst rounded to the nearest integer; the result is
ANDed with 2n , 1, and the resulting value used as an address into the
table. The value in the table replaces the index. The oating-point table
value is rst rounded to a xed-point value with unspeci ed precision. The
group's type remains color index.
Stencil Index Lookup
This step applies only to stencil index groups. If MAP STENCIL is enabled,
then the index is looked up in the PIXEL MAP S TO S table otherwise, the
index is not looked up. The table must have 2n entries for some integer n.
The integer index is ANDed with 2n , 1, and the resulting value used as an
address into the table. The integer value in the table replaces the index.




                    Version 1.2.1 - April 1, 1999
3.6. PIXEL RECTANGLES                                                      103

                 Base Internal Format R           G     B       A
                 ALPHA                                     At
                 LUMINANCE               Lt Lt Lt
                 LUMINANCE ALPHA         Lt Lt Lt At
                 INTENSITY                It It It It
                 RGB                     Rt Gt Bt
                 RGBA                    Rt Gt Bt At
Table 3.13: Color table lookup. Rt , Gt , Bt , At , Lt , and It are color table
values that are assigned to pixel components R, G, B , and A depending on
the table format. When there is no assignment, the component value is left
unchanged by lookup.


Color Table Lookup
This step applies only to RGBA component groups. Color table lookup is
only done if COLOR TABLE is enabled. If a zero-width table is enabled, no
lookup is performed.
   The internal format of the table determines which components of the
group will be replaced see table 3.13. The components to be replaced
are converted to indices by clamping to 0; 1 , multiplying by an integer
one less than the width of the table, and rounding to the nearest integer.
Components are replaced by the table entry at the index.
   The required state is one bit indicating whether color table lookup is
enabled or disabled. In the initial state, lookup is disabled.

Convolution
This step applies only to RGBA component groups. If CONVOLUTION 1D is
enabled, the one-dimensional convolution lter is applied only to the one-
dimensional texture images passed to TexImage1D, TexSubImage1D,
CopyTexImage1D, and CopyTexSubImage1D, and returned by Get-
TexImage see section 6.1.4 with target TEXTURE 1D. If CONVOLUTION 2D
is enabled, the two-dimensional convolution lter is applied only to the
two-dimensional images passed to DrawPixels, CopyPixels, ReadPix-
els, TexImage2D, TexSubImage2D, CopyTexImage2D, CopyTex-
SubImage2D, and CopyTexSubImage3D, and returned by GetTexIm-
age with target TEXTURE 2D. If SEPARABLE 2D is enabled, and CONVOLUTION 2D
is disabled, the separable two-dimensional convolution lter is instead ap-




                                Version 1.2.1 - April 1, 1999
104                                         CHAPTER 3. RASTERIZATION

 Base Filter Format R              G            B           A
 ALPHA                 Rs          Gs           Bs          As  Af
 LUMINANCE             Rs  Lf     Gs  Lf      Bs  Lf     As
 LUMINANCE ALPHA       Rs  Lf     Gs  Lf      Bs  Lf     As  Af
 INTENSITY             Rs  If     Gs  If      Bs  If     As  If
 RGB                   Rs  Rf     Gs  Gf      Bs  Bf     As
 RGBA                  Rs  Rf     Gs  Gf      Bs  Bf     As  Af
Table 3.14: Computation of ltered color components depending on lter
image format. C  F indicates the convolution of image component C with
 lter F .

plied these images.
     The convolution operation is a sum of products of source image pixels and
convolution lter pixels. Source image pixels always have four components:
red, green, blue, and alpha, denoted in the equations below as Rs , Gs, Bs ,
and As . Filter pixels may be stored in one of ve formats, with 1, 2, 3, or
4 components. These components are denoted as Rf , Gf , Bf , Af , Lf , and
If in the equations below. The result of the convolution operation is the
4-tuple R,G,B,A. Depending on the internal format of the lter, individual
color components of each source image pixel are convolved with one lter
component, or are passed unmodi ed. The rules for this are de ned in
table 3.14.
     The convolution operation is de ned di erently for each of the three
convolution lters. The variables Wf and Hf refer to the dimensions of the
convolution lter. The variables Ws and Hs refer to the dimensions of the
source pixel image.
     The convolution equations are de ned as follows, where C refers to the
  ltered result, Cf refers to the one- or two-dimensional convolution lter,
and Crow and Ccolumn refer to the two one-dimensional lters comprising
the two-dimensional separable lter. Cs0 depends on the source image color
Cs and the convolution border mode as described below. Cr , the ltered
output image, depends on all of these variables and is described separately
for each border mode. The pixel indexing nomenclature is decribed in the
Convolution Filter Speci cation subsection of section 3.6.3.
      One-dimensional lter:
                                 f ,1
                                WX
                       C i0 =           Cs0 i0 + n  Cf n
                                 n=0




                    Version 1.2.1 - April 1, 1999
3.6. PIXEL RECTANGLES                                                         105

   Two-dimensional lter:
                   f ,1 HX
                  WX     f ,1
            0 0
             C i ;j =                    Cs0 i0 + n; j 0 + m  Cf n; m
                            n=0 m=0
   Two-dimensional separable lter:
                      f ,1 HX
                     WX     f ,1
       C i0; j 0 =                 Cs0 i0 + n; j 0 + m  Crow n  Ccolumn m
                     n=0 m=0
    If Wf of a one-dimensional lter is zero, then C i is always set to zero.
Likewise, if either Wf or Hf of a two-dimensional lter is zero, then C i; j
is always set to zero.
    The convolution border mode for a speci c convolution lter is speci ed
by calling
     void   ConvolutionParameterfifg enum target,
        enum   pname, T param ;
where target is the name of the lter, pname is CONVOLUTION BORDER MODE,
and param is one of REDUCE, CONSTANT BORDER or REPLICATE BORDER.
Border Mode REDUCE
The width and height of source images convolved with border mode REDUCE
are reduced by Wf , 1 and Hf , 1, respectively. If this reduction would
generate a resulting image with zero or negative width and or height, the
output is simply null, with no error generated. The coordinates of the
image that results from a convolution with border mode REDUCE are zero
through Ws , Wf in width, and zero through Hs , Hf in height. In cases
where errors can result from the speci cation of invalid image dimensions,
it is these resulting dimensions that are tested, not the dimensions of the
source image. A speci c example is TexImage1D and TexImage2D,
which specify constraints for image dimensions. Even if TexImage1D or
TexImage2D is called with a null pixel pointer, the dimensions of the
resulting texture image are those that would result from the convolution of
the speci ed image.
     When the border mode is REDUCE, Cs0 equals the source image color Cs
and Cr equals the ltered result C .
     For the remaining border modes, de ne Cw = bWf =2c and Ch = bHf =2c.
The coordinates Cw ; Ch  de ne the center of the convolution lter.




                                     Version 1.2.1 - April 1, 1999
106                                             CHAPTER 3. RASTERIZATION

Border Mode CONSTANT BORDER
If the convolution border mode is CONSTANT BORDER, the output image has
the same dimensions as the source image. The result of the convolution is
the same as if the source image were surrounded by pixels with the same
color as the current convolution border color. Whenever the convolution l-
ter extends beyond one of the edges of the source image, the constant-color
border pixels are used as input to the lter. The current convolution border
color is set by calling ConvolutionParameterfv or ConvolutionParam-
eteriv with pname set to CONVOLUTION BORDER COLOR and params containing
four values that comprise the RGBA color to be used as the image border.
Integer color components are interpreted linearly such that the most positive
integer maps to 1.0, and the most negative integer maps to -1.0. Floating
point color components are not clamped when they are speci ed.
    For a one-dimensional lter, the result color is de ned by
                                     Cr i = C i , Cw
where C i0 is computed using the following equation for Cs0 i0 :
                                       0      i0 Ws
                          Cs0 i0 = CCs;i ; 0otherwise
                                     c
and Cc is the convolution border color.
    For a two-dimensional or two-dimensional separable lter, the result
color is de ned by
                               Cr i; j = C i , Cw ; j , Ch
where C i0 ; j 0 is computed using the following equation for Cs0 i0 ; j 0 :
                               
              Cs0 i0 ; j 0 =       Cs i0 ; j 0 ; 0  i0 Ws; 0  j 0 Hs
                                   Cc ;          otherwise
Border Mode REPLICATE BORDER
The convolution border mode REPLICATE BORDER also produces an output
image with the same dimensions as the source image. The behavior of
this mode is identical to that of the CONSTANT BORDER mode except for the
treatment of pixel locations where the convolution lter extends beyond the
edge of the source image. For these locations, it is as if the outermost one-
pixel border of the source image was replicated. Conceptually, each pixel in




                        Version 1.2.1 - April 1, 1999
3.6. PIXEL RECTANGLES                                                          107

the leftmost one-pixel column of the source image is replicated Cw times to
provide additional image data along the left edge, each pixel in the rightmost
one-pixel column is replicated Cw times to provide additional image data
along the right edge, and each pixel value in the top and bottom one-pixel
rows is replicated to create Ch rows of image data along the top and bottom
edges. The pixel value at each corner is also replicated in order to provide
data for the convolution operation at each corner of the source image.
    For a one-dimensional lter, the result color is de ned by
                                Cr i = C i , C w
where C i0 is computed using the following equation for Cs0 i0 :
                        Cs0 i0 = Cs clampi0 ; Ws
and the clamping function clampval; max is de ned as
                                8
                                  0;           val 0
            clampval; max = val;             0  val max
                                : max , 1; val = max
    For a two-dimensional or two-dimensional separable lter, the result
color is de ned by
                           Cr i; j = C i , Cw ; j , Ch
where C i0 ; j 0 is computed using the following equation for Cs0 i0 ; j 0 :
                  Cs0 i0 ; j 0 = Cs clampi0 ; Ws ; clampj 0 ; Hs
    After convolution, each component of the resulting image is scaled by
the corresponding PixelTransfer parameters: POST CONVOLUTION RED SCALE
for an R component, POST CONVOLUTION GREEN SCALE for a G com-
ponent, POST CONVOLUTION BLUE SCALE for a B component, and
POST CONVOLUTION ALPHA SCALE for an A component.                    The result
is added to the corresponding bias: POST CONVOLUTION RED BIAS,
POST CONVOLUTION GREEN BIAS,            POST CONVOLUTION BLUE BIAS,         or
POST CONVOLUTION ALPHA BIAS.
    The required state is three bits indicating whether each of one-
dimensional, two-dimensional, or separable two-dimensional convolution is
enabled or disabled, an integer describing the current convolution border
mode, and four oating-point values specifying the convolution border color.
In the initial state, all convolution operations are disabled, the border mode
is REDUCE, and the border color is 0; 0; 0; 0.




                                   Version 1.2.1 - April 1, 1999
108                                         CHAPTER 3. RASTERIZATION

Post Convolution Color Table Lookup
This step applies only to RGBA component groups. Post convolution
color table lookup is enabled or disabled by calling Enable or Disable
with the symbolic constant POST CONVOLUTION COLOR TABLE. The post convo-
lution table is de ned by calling ColorTable with a target argument of
POST CONVOLUTION COLOR TABLE. In all other respects, operation is identical
to color table lookup, as de ned earlier in section 3.6.5.
    The required state is one bit indicating whether post convolution table
lookup is enabled or disabled. In the initial state, lookup is disabled.
Color Matrix Transformation
This step applies only to RGBA component groups. The components are
transformed by the color matrix. Each transformed component is multi-
plied by an appropriate signed scale factor: POST COLOR MATRIX RED SCALE
for an R component, POST COLOR MATRIX GREEN SCALE for a G com-
ponent, POST COLOR MATRIX BLUE SCALE for a B component, and
POST COLOR MATRIX ALPHA SCALE for an A component. The result is added to
a signed bias: POST COLOR MATRIX RED BIAS, POST COLOR MATRIX GREEN BIAS,
POST COLOR MATRIX BLUE BIAS, or POST COLOR MATRIX ALPHA BIAS. The result-
ing components replace each component of the original group.
    That is, if Mc is the color matrix, a subscript of s represents the scale
term for a component, and a subscript of b represents the bias term, then
the components
                                      0R1
                                      BB G CC
                                       @ A
                                        B
                                        A
are transformed to
           0 R0 1 0 Rs 0 0          0 1 0 R 1 0 Rb 1
           BB G0 CC = BB 0 Gs 0     0CC BB G CC BB Gb CC
            @ 0A @
             B           0     0 Bs 0 A Mc @ B A + @ Bb A :
             A0          0     0 0 As        A       Ab

Post Color Matrix Color Table Lookup
This step applies only to RGBA component groups. Post color matrix
color table lookup is enabled or disabled by calling Enable or Disable




                     Version 1.2.1 - April 1, 1999
3.6. PIXEL RECTANGLES                                                     109

with the symbolic constant POST COLOR MATRIX COLOR TABLE. The post color
matrix table is de ned by calling ColorTable with a target argument of
POST COLOR MATRIX COLOR TABLE. In all other respects, operation is identical
to color table lookup, as de ned in section 3.6.5.
    The required state is one bit indicating whether post color matrix lookup
is enabled or disabled. In the initial state, lookup is disabled.

Histogram
This step applies only to RGBA component groups. Histogram operation
is enabled or disabled by calling Enable or Disable with the symbolic
constant HISTOGRAM.
    If the width of the table is non-zero, then indices Ri , Gi , Bi , and Ai
are derived from the red, green, blue, and alpha components of each pixel
group without modifying these components by clamping each component
to 0; 1 , multiplying by one less than the width of the histogram table, and
rounding to the nearest integer. If the format of the HISTOGRAM table includes
red or luminance, the red or luminance component of histogram entry Ri
is incremented by one. If the format of the HISTOGRAM table includes green,
the green component of histogram entry Gi is incremented by one. The blue
and alpha components of histogram entries Bi and Ai are incremented in
the same way. If a histogram entry component is incremented beyond its
maximum value, its value becomes unde ned; this is not an error.
    If the Histogram sink parameter is FALSE, histogram operation has no
e ect on the stream of pixel groups being processed. Otherwise, all RGBA
pixel groups are discarded immediately after the histogram operation is
completed. Because histogram precedes minmax, no minmax operation is
performed. No pixel fragments are generated, no change is made to texture
memory contents, and no pixel values are returned. However, texture object
state is modi ed whether or not pixel groups are discarded.

Minmax
This step applies only to RGBA component groups. Minmax operation
is enabled or disabled by calling Enable or Disable with the symbolic
constant MINMAX.
    If the format of the minmax table includes red or luminance, the red
component value replaces the red or luminance value in the minimum table
element if and only if it is less than that component. Likewise, if the format
includes red or luminance and the red component of the group is greater




                               Version 1.2.1 - April 1, 1999
110                                         CHAPTER 3. RASTERIZATION

than the red or luminance value in the maximum element, the red group
component replaces the red or luminance maximum component. If the for-
mat of the table includes green, the green group component conditionally
replaces the green minimum and or maximum if it is smaller or larger, re-
spectively. The blue and alpha group components are similarly tested and
replaced, if the table format includes blue and or alpha. The internal type
of the minimum and maximum component values is oating point, with at
least the same representable range as a oating point number used to repre-
sent colors section 2.1.1. There are no semantics de ned for the treatment
of group component values that are outside the representable range.
    If the Minmax sink parameter is FALSE, minmax operation has no e ect
on the stream of pixel groups being processed. Otherwise, all RGBA pixel
groups are discarded immediately after the minmax operation is completed.
No pixel fragments are generated, no change is made to texture memory
contents, and no pixel values are returned. However, texture object state is
modi ed whether or not pixel groups are discarded.

3.7 Bitmaps
Bitmaps are rectangles of zeros and ones specifying a particular pattern of
fragments to be produced. Each of these fragments has the same associated
data. These data are those associated with the current raster position.
    Bitmaps are sent using
      void  Bitmap sizei w, sizei h, float xbo , float ybo,
         float   xbi, float ybi, ubyte *data ;
w and h comprise the integer width and height of the rectangular bitmap,
respectively. xbo ; ybo  gives the oating-point x and y values of the bitmap's
origin. xbi ; ybi  gives the oating-point x and y increments that are added
to the raster position after the bitmap is rasterized. data is a pointer to a
bitmap.
    Like a polygon pattern, a bitmap is unpacked from memory according
to the procedure given in section 3.6.4 for DrawPixels; it is as if the width
and height passed to that command were equal to w and h, respectively, the
type were BITMAP, and the format were COLOR INDEX. The unpacked values
before any conversion or arithmetic would have been performed form a
stipple pattern of zeros and ones. See gure 3.9.
    A bitmap sent using Bitmap is rasterized as follows. First, if the cur-
rent raster position is invalid the valid bit is reset, the bitmap is ignored.




                     Version 1.2.1 - April 1, 1999
3.8. TEXTURING                                                              111




                       h = 12




                                ybo = 1.0



                                        xbo = 2.5

                                                    w=8



   Figure 3.9. A bitmap and its associated parameters. xbi and ybi are not
   shown.


Otherwise, a rectangular array of fragments is constructed, with lower left
corner at
                       xll ; yll  = bxrp , xbo c; byrp , ybo c
and upper right corner at xll + w; yll + h where w and h are the width and
height of the bitmap, respectively. Fragments in the array are produced if
the corresponding bit in the bitmap is 1 and not produced otherwise. The
associated data for each fragment are those associated with the current raster
position, with texture coordinates s, t, and r replaced with s=q, t=q, and r=q,
respectively. If q is less than or equal to zero, the results are unde ned. Once
the fragments have been produced, the current raster position is updated:
                      xrp ; yrp   xrp + xbi ; yrp + ybi :
The z and w values of the current raster position remain unchanged.

3.8 Texturing
Texturing maps a portion of a speci ed image onto each primitive for which
texturing is enabled. This mapping is accomplished by using the color of




                                      Version 1.2.1 - April 1, 1999
112                                         CHAPTER 3. RASTERIZATION

an image at the location indicated by a fragment's s; t; r coordinates to
modify the fragment's primary RGBA color. Texturing does not a ect the
secondary color.
    Texturing is speci ed only for RGBA mode; its use in color index mode
is unde ned.
    The GL provides a means to specify the details of how texturing of a
primitive is e ected. These details include speci cation of the image to be
texture mapped, the means by which the image is ltered when applied
to the primitive, and the function that determines what RGBA value is
produced given a fragment color and an image value.

3.8.1 Texture Image Speci cation
The command
      void  TexImage3D     enum target, int level,
         int internalformat, sizei width, sizei height,
         sizei depth, int border, enum format, enum type,
         void *data ;

is used to specify a three-dimensional texture image. target must be either
TEXTURE 3D, or PROXY TEXTURE 3D in the special case discussed in section 3.8.7.
format, type, and data match the corresponding arguments to DrawPixels
refer to section 3.6.4; they specify the format of the image data, the type
of those data, and a pointer to the image data in host memory. The formats
STENCIL INDEX and DEPTH COMPONENT are not allowed.
    The groups in memory are treated as being arranged in a sequence of ad-
jacent rectangles. Each rectangle is a two-dimensional image, whose size and
organization are speci ed by the width and height parameters to TexIm-
age3D. The values of UNPACK ROW LENGTH and UNPACK ALIGNMENT control the
row-to-row spacing in these images in the same manner as DrawPixels. If
the value of the integer parameter UNPACK IMAGE HEIGHT is not positive, then
the number of rows in each two-dimensional image is height; otherwise the
number of rows is UNPACK IMAGE HEIGHT. Each two-dimensional image com-
prises an integral number of rows, and is exactly adjacent to its neighbor
images.
    The mechanism for selecting a sub-volume of a three-dimensional image
relies on the integer parameter UNPACK SKIP IMAGES. If UNPACK SKIP IMAGES is
positive, the pointer is advanced by UNPACK SKIP IMAGES times the number of
elements in one two-dimensional image before obtaining the rst group from




                     Version 1.2.1 - April 1, 1999
3.8. TEXTURING                                                             113

memory. Then depth two-dimensional images are processed, each having a
subimage extracted in the same manner as DrawPixels.
    The selected groups are processed exactly as for DrawPixels, stopping
just before nal conversion. Each R, G, B, and A value so generated is
clamped to 0; 1 .
    Components are then selected from the resulting R, G, B, and A values
to obtain a texture with the base internal format speci ed by or derived
from internalformat. Table 3.15 summarizes the mapping of R, G, B, and
A values to texture components, as a function of the base internal format
of the texture image. internalformat may be speci ed as one of the six base
internal format symbolic constants listed in table 3.15, or as one of the sized
internal format symbolic constants listed in table 3.16. internalformat may
for backwards compatibility with the 1.0 version of the GL also take on
the integer values 1, 2, 3, and 4, which are equivalent to symbolic constants
LUMINANCE, LUMINANCE ALPHA, RGB, and RGBA respectively. Specifying a value
for internalformat that is not one of the above values generates the error
INVALID VALUE.
    The internal component resolution is the number of bits allocated to
each value in a texture image. If internalformat is speci ed as a base in-
ternal format, the GL stores the resulting texture with internal component
resolutions of its own choosing. If a sized internal format is speci ed, the
mapping of the R, G, B, and A values to texture components is equivalent
to the mapping of the corresponding base internal format's components, as
speci ed in table 3.15, and the memory allocation per texture component is
assigned by the GL to match the allocations listed in table 3.16 as closely
as possible. The de nition of closely is left up to the implementation. Im-
plementations are not required to support more than one resolution for each
base internal format.
    A GL implementation may vary its allocation of internal component res-
olution based on any TexImage3D, TexImage2D see below, or TexIm-
age1D see below parameter except target, but the allocation must not be
a function of any other state, and cannot be changed once it is established.
Allocations must be invariant; the same allocation must be made each time a
texture image is speci ed with the same parameter values. These allocation
rules also apply to proxy textures, which are described in section 3.8.7.
    The image itself pointed to by data is a sequence of groups of values.
The rst group is the lower left back corner of the texture image. Subse-
quent groups ll out rows of width width from left to right; height rows are
stacked from bottom to top forming a single two-dimensional image slice;
and depth slices are stacked from back to front. When the nal R, G, B,




                                Version 1.2.1 - April 1, 1999
114                                         CHAPTER 3. RASTERIZATION

       Base Internal Format RGBA Values              Internal Components
       ALPHA                A                        A
       LUMINANCE            R                        L
       LUMINANCE ALPHA      R,A                      L,A
       INTENSITY            R                        I
       RGB                  R,G,B                    R,G,B
       RGBA                 R,G,B,A                  R,G,B ,A
Table 3.15: Conversion from RGBA pixel components to internal texture,
table, or lter components. See section 3.8.9 for a description of the texture
components R, G, B , A, L, and I .


and A components have been computed for a group, they are assigned to
components of a texel as described by table 3.15. Counting from zero, each
resulting N th texel is assigned internal integer coordinates i; j; k, where
                           i = N mod width , bs
                                N c mod height , b
                       j = b width                  s

                   k = b width N height c mod depth , bs
and bs is the speci ed border width. Thus the last two-dimensional image
slice of the three-dimensional image is indexed with the highest value of k.
    Each color component is converted by rounding to nearest to a xed-
point value with n bits, where n is the number of bits of storage allocated to
that component in the image array. We assume that the xed-point repre-
sentation used represents each value k=2n , 1, where k 2 f0; 1; : : : ; 2n , 1g,
as k e.g. 1.0 is represented in binary as a string of all ones.
    The level argument to TexImage3D is an integer level-of-detail number.
Levels of detail are discussed below, under Mipmapping. The main texture
image has a level of detail number of 0. If a level-of-detail less than zero is
speci ed, the error INVALID VALUE is generated.
    The border argument to TexImage3D is a border width. The signi -
cance of borders is described below. The border width a ects the required
dimensions of the texture image: it must be the case that
                                 ws = 2n + 2bs                             3.11




                     Version 1.2.1 - April 1, 1999
3.8. TEXTURING                                                        115

 Sized                  Base             R G B A L I
 Internal Format        Internal Format bits bits bits bits bits bits
 ALPHA4                 ALPHA                            4
 ALPHA8                 ALPHA                            8
 ALPHA12                ALPHA                           12
 ALPHA16                ALPHA                           16
 LUMINANCE4             LUMINANCE                             4
 LUMINANCE8             LUMINANCE                             8
 LUMINANCE12            LUMINANCE                            12
 LUMINANCE16            LUMINANCE                            16
 LUMINANCE4 ALPHA4      LUMINANCE ALPHA                  4    4
 LUMINANCE6 ALPHA2      LUMINANCE ALPHA                  2    6
 LUMINANCE8 ALPHA8      LUMINANCE ALPHA                  8    8
 LUMINANCE12 ALPHA4     LUMINANCE ALPHA                  4 12
 LUMINANCE12 ALPHA12    LUMINANCE ALPHA                 12 12
 LUMINANCE16 ALPHA16    LUMINANCE ALPHA                 16 16
 INTENSITY4             INTENSITY                                  4
 INTENSITY8             INTENSITY                                  8
 INTENSITY12            INTENSITY                                 12
 INTENSITY16            INTENSITY                                 16
 R3 G3 B2               RGB               3   3    2
 RGB4                   RGB               4   4    4
 RGB5                   RGB               5   5    5
 RGB8                   RGB               8   8    8
 RGB10                  RGB              10 10 10
 RGB12                  RGB              12 12 12
 RGB16                  RGB              16 16 16
 RGBA2                  RGBA              2   2    2     2
 RGBA4                  RGBA              4   4    4     4
 RGB5 A1                RGBA              5   5    5     1
 RGBA8                  RGBA              8   8    8     8
 RGB10 A2               RGBA             10 10 10 2
 RGBA12                 RGBA             12 12 12 12
 RGBA16                 RGBA             16 16 16 16
Table 3.16: Correspondence of sized internal formats to base internal for-
mats, and desired component resolutions for each sized internal format.




                              Version 1.2.1 - April 1, 1999
116                                           CHAPTER 3. RASTERIZATION


                                   hs = 2m + 2bs                                3.12

                               ds = 2l + 2bs                           3.13
for some integers n, m, and l, where ws , hs , and ds are the speci ed image
width, height, and depth. If any one of these relationships cannot be satis ed,
then the error INVALID VALUE is generated.
    Currently, the maximum border width bt is 1. If bs is less than zero, or
greater than bt , then the error INVALID VALUE is generated.
    The maximum allowable width, height, or depth of a three-dimensional
texture image is an implementation dependent function of the level-of-detail
and internal format of the resulting image array. It must be at least 2k,lod +
2bt for image arrays of level-of-detail 0 through k, where k is the log base
2 of MAX 3D TEXTURE SIZE, lod is the level-of-detail of the image array, and
bt is the maximum border width. It may be zero for image arrays of any
level-of-detail greater than k. The error INVALID VALUE is generated if the
speci ed image is too large to be stored under any conditions.
    In a similar fashion, the maximum allowable width of a one- or two-
dimensional texture image, and the maximum allowable height of a two-
dimensional texture image, must be at least 2k,lod + 2bt for image arrays of
level 0 through k, where k is the log base 2 of MAX TEXTURE SIZE.
    Furthermore, an implementation may allow a one-, two-, or three-
dimensional image array of level 1 or greater to be created only if a complete1
set of image arrays consistent with the requested array can be supported.
Likewise, an implementation may allow an image array of level 0 to be cre-
ated only if that single image array can be supported.
    The command
      void   TexImage2D enum target, int level,
         int   internalformat, sizei width, sizei height,
         int   border, enum format, enum type, void *data ;
is used to specify a two-dimensional texture image. target must be ei-
ther TEXTURE 2D, or PROXY TEXTURE 2D in the special case discussed in sec-
tion 3.8.7. The other parameters match the corresponding parameters of
TexImage3D.
   1 For this purpose the de nition of complete", as provided under Mipmapping, is aug-
mented as follows: 1 it is as though TEXTURE BASE LEVEL is 0 and TEXTURE MAX LEVEL
is 1000. 2 Excluding borders, the dimensions of the next lower numbered array are all
understood to be twice the corresponding dimensions of the speci ed array.




                       Version 1.2.1 - April 1, 1999
3.8. TEXTURING                                                            117

    For the purposes of decoding the texture image, TexImage2D is equiv-
alent to calling TexImage3D with corresponding arguments and depth of
1, except that
     The depth of the image is always 1 regardless of the value of border.
     Convolution will be performed on the image possibly changing its
     width and height if SEPARABLE 2D or CONVOLUTION 2D is enabled.
     UNPACK SKIP IMAGES is ignored.

   Finally, the command
     void    TexImage1D   enum target, int level,
        int internalformat, sizei width, int border,
        enum format, enum type, void *data ;

is used to specify a one-dimensional texture image. target must be ei-
ther TEXTURE 1D, or PROXY TEXTURE 1D in the special case discussed in sec-
tion 3.8.7.
    For the purposes of decoding the texture image, TexImage1D is equiv-
alent to calling TexImage2D with corresponding arguments and height of
1, except that
     The height of the image is always 1 regardless of the value of border.
     Convolution will be performed on the image possibly changing its
     width only if CONVOLUTION 1D is enabled.
    An image with zero width, height TexImage2D and TexImage3D
only, or depth TexImage3D only indicates the null texture. If the null
texture is speci ed for the level-of-detail speci ed by TEXTURE BASE LEVEL, it
is as if texturing were disabled.
    The image indicated to the GL by the image pointer is decoded and
copied into the GL's internal memory. This copying e ectively places the
decoded image inside a border of the maximum allowable width bt whether
or not a border has been speci ed see gure 3.10 2 . If no border or a
border smaller than the maximum allowable width has been speci ed, then
the image is still stored as if it were surrounded by a border of the maximum
possible width. Any excess border which surrounds the speci ed image,
  2 Figure 3.10   needs to show a three-dimensional texture image.




                                     Version 1.2.1 - April 1, 1999
118                                        CHAPTER 3. RASTERIZATION

including any border is assigned unspeci ed values. A two-dimensional
texture has a border only at its left, right, top, and bottom ends, and a
one-dimensional texture has a border only at its left and right ends.
    We shall refer to the possibly border augmented decoded image as the
texture array. A three-dimensional texture array has width, height, and
depth
                                wt = 2n + 2bt
                                ht = 2m + 2bt
                                 dt = 2l + 2bt
where bt is the maximum allowable border width and n, m, and l are de ned
in equations 3.11, 3.12, and 3.13. A two-dimensional texture array has depth
dt = 1, with height ht and width wt as above, and a one-dimensional texture
array has depth dt = 1, height ht = 1, and width wt as above.
    An element i; j; k of the texture array is called a texel for a two-
dimensional texture, k is irrelevant; for a one-dimensional texture, j and
k are both irrelevant. The texture value used in texturing a fragment is
determined by that fragment's associated s; t; r coordinates, but may not
correspond to any actual texel. See gure 3.10.
    If the data argument of TexImage1D, TexImage2D, or TexImage3D
is a null pointer a zero-valued pointer in the C implementation, a one-,
two-, or three-dimensional texture array is created with the speci ed target,
level, internalformat, width, height, and depth, but with unspeci ed image
contents. In this case no pixel values are accessed in client memory, and
no pixel processing is performed. Errors are generated, however, exactly as
though the data pointer were valid.

3.8.2 Alternate Texture Image Speci cation Commands
Two-dimensional and one-dimensional texture images may also be speci-
 ed using image data taken directly from the framebu er, and rectangular
subregions of existing texture images may be respeci ed.
   The command
      void  CopyTexImage2D      enum target, int level,
         enum internalformat, int x, int y, sizei width,
         sizei height, int border ;




                    Version 1.2.1 - April 1, 1999
3.8. TEXTURING                                                                               119




            5.0
                      4
     1.0
                      3

                      2                             α
      t      v    j                                     β
                      1

                      0
     0.0
                  −1
           −1.0
                          −1         0   1      2       3 i 4     5     6    7     8

                  −1.0                                      u                          9.0
                               0.0                          s                    1.0


  Figure 3.10. A texture image and the coordinates used to access it. This is a
  two-dimensional texture with n = 3 and m = 2. A one-dimensional texture
  would consist of a single horizontal strip. and , values used in blending
  adjacent texels to obtain a texture value, are also shown.




                                             Version 1.2.1 - April 1, 1999
120                                                 CHAPTER 3. RASTERIZATION

de nes a two-dimensional texture array in exactly the manner of TexIm-
age2D, except that the image data are taken from the framebu er rather
than from client memory. Currently, target must be TEXTURE 2D. x, y, width,
and height correspond precisely to the corresponding arguments to Copy-
Pixels refer to section 4.3.3; they specify the image's width and height,
and the lower left x; y coordinates of the framebu er region to be copied.
The image is taken from the framebu er exactly as if these arguments were
passed to CopyPixels, with argument type set to COLOR, stopping after pixel
transfer processing is complete. Subsequent processing is identical to that
described for TexImage2D, beginning with clamping of the R, G, B, and
A values from the resulting pixel groups. Parameters level, internalformat,
and border are speci ed using the same values, with the same meanings, as
the equivalent arguments of TexImage2D, except that internalformat may
not be speci ed as 1, 2, 3, or 4. An invalid value speci ed for internalfor-
mat generates the error INVALID ENUM. The constraints on width, height, and
border are exactly those for the equivalent arguments of TexImage2D.
    The command
      void CopyTexImage1D enum target, int level,
          enum internalformat, int x, int y, sizei width,
          int border ;

de nes a one-dimensional texture array in exactly the manner of TexIm-
age1D, except that the image data are taken from the framebu er, rather
than from client memory. Currently, target must be TEXTURE 1D. For the
purposes of decoding the texture image, CopyTexImage1D is equivalent
to calling CopyTexImage2D with corresponding arguments and height of
1, except that the height of the image is always 1, regardless of the value
of border. level, internalformat, and border are speci ed using the same val-
ues, with the same meanings, as the equivalent arguments of TexImage1D,
except that internalformat may not be speci ed as 1, 2, 3, or 4. The con-
straints on width and border are exactly those of the equivalent arguments
of TexImage1D.
    Six additional commands,
      void TexSubImage3D enum target, int level, int xo set,
          int yo set, int zo set, sizei width, sizei height,
          sizei depth, enum format, enum type, void *data ;
      void TexSubImage2D enum target, int level, int xo set,
          int yo set, sizei width, sizei height, enum format,
          enum type, void *data ;




                    Version 1.2.1 - April 1, 1999
3.8. TEXTURING                                                                121

     void     TexSubImage1D  enum target, int level, int xo          set,
        sizei width, enum format, enum type, void *data ;
     void     CopyTexSubImage3D    enum target, int level,
        int xo set, int yo set, int zo set, int x, int y,
        sizei width, sizei height ;
     void     CopyTexSubImage2D    enum target, int level,
        int xo set, int yo set, int x, int y, sizei width,
        sizei height ;
     void     CopyTexSubImage1D    enum target, int level,
        int xo set, int x, int y, sizei width ;


respecify only a rectangular subregion of an existing texture array. No
change is made to the internalformat, width, height, depth, or border pa-
rameters of the speci ed texture array, nor is any change made to texel
values outside the speci ed subregion. Currently the target arguments of
TexSubImage1D and CopyTexSubImage1D must be TEXTURE 1D, the
target arguments of TexSubImage2D and CopyTexSubImage2D must
be TEXTURE 2D, and the target arguments of TexSubImage3D and Copy-
TexSubImage3D must be TEXTURE 3D. The level parameter of each com-
mand speci es the level of the texture array that is modi ed. If level is
less than zero or greater than the base 2 logarithm of the maximum texture
width or height, the error INVALID VALUE is generated.
    TexSubImage3D arguments width, height, depth, format, type, and
data match the corresponding arguments to TexImage3D, meaning that
they are speci ed using the same values, and have the same meanings. Like-
wise, TexSubImage2D arguments width, height, format, type, and data
match the corresponding arguments to TexImage2D, and TexSubIm-
age1D arguments width, format, type, and data match the corresponding
arguments to TexImage1D.
    CopyTexSubImage3D and CopyTexSubImage2D arguments x, y,
width, and height match the corresponding arguments to CopyTexIm-
age2D3 . CopyTexSubImage1D arguments x, y, and width match the cor-
responding arguments to CopyTexImage1D. Each of the TexSubImage
commands interprets and processes pixel groups in exactly the manner of its
TexImage counterpart, except that the assignment of R, G, B, and A pixel
group values to the texture components is controlled by the internalformat
of the texture array, not by an argument to the command.
  3 Because   the framebu er is inherently two-dimensional, there is no CopyTexIm-
age3D command.




                                  Version 1.2.1 - April 1, 1999
122                                         CHAPTER 3. RASTERIZATION

   Arguments xo set, yo set, and zo set of TexSubImage3D and Copy-
TexSubImage3D specify the lower left texel coordinates of a width-wide by
height-high by depth-deep rectangular subregion of the texture array. The
depth argument associated with CopyTexSubImage3D is always 1, be-
cause framebu er memory is two-dimensional - only a portion of a single s; t
slice of a three-dimensional texture is replaced by CopyTexSubImage3D.
    Negative values of xo set, yo set, and zo set correspond to the coor-
dinates of border texels, addressed as in gure 3.10. Taking ws , hs , ds ,
and bs to be the speci ed width, height, depth, and border width of the
texture array, not the actual array dimensions wt , ht , dt , and bt , and tak-
ing x, y, z , w, h, and d to be the xo set, yo set, zo set, width, height, and
depth argument values, any of the following relationships generates the error
INVALID VALUE:


                                   x      ,bs
                                x+w       ws , bs
                                   y      ,bs
                                y+h       hs , bs
                                   z      ,bs
                                z +d      ds , bs
Recall that ds , ws , and hs include twice the speci ed border width bs.
Counting from zero, the nth pixel group is assigned to the texel with internal
integer coordinates i; j; k , where
                              i = x + n mod w
                            j = y + b wn c mod h
                      k = z + b width nheight c mod d
     Arguments xo set and yo set of TexSubImage2D and CopyTex-
SubImage2D specify the lower left texel coordinates of a width-wide by
height-high rectangular subregion of the texture array. Negative values of
xo set and yo set correspond to the coordinates of border texels, addressed
as in gure 3.10. Taking ws , hs , and bs to be the speci ed width, height,
and border width of the texture array, not the actual array dimensions wt ,
ht , and bt , and taking x, y, w, and h to be the xo set, yo set, width, and




                     Version 1.2.1 - April 1, 1999
3.8. TEXTURING                                                            123

height argument values, any of the following relationships generates the error
INVALID VALUE:


                                x      ,bs
                              x+w      ws , bs
                                y      , bs
                              y+h      hs , bs
Recall that ws and hs include twice the speci ed border width bs . Counting
from zero, the nth pixel group is assigned to the texel with internal integer
coordinates i; j , where
                              i = x + n mod w
                            j = y + b wn c mod h
    The xo set argument of TexSubImage1D and CopyTexSubIm-
age1D speci es the left texel coordinate of a width-wide subregion of the
texture array. Negative values of xo set correspond to the coordinates of
border texels. Taking ws and bs to be the speci ed width and border width
of the texture array, and x and w to be the xo set and width argument val-
ues, either of the following relationships generates the error INVALID VALUE:
                                  x ,bs
                              x + w ws , bs
Counting from zero, the nth pixel group is assigned to the texel with internal
integer coordinates i , where
                             i = x + n mod w
3.8.3 Texture Parameters
Various parameters control how the texture array is treated when applied
to a fragment. Each parameter is set by calling
     void   TexParameterfifg enum target, enum pname,
        T param ;
     void   TexParameterfifgv enum target, enum pname,
        T params ;




                               Version 1.2.1 - April 1, 1999
124                                        CHAPTER 3. RASTERIZATION

             Name              Type Legal Values
         TEXTURE WRAP S       integer CLAMP, CLAMP TO EDGE, REPEAT
         TEXTURE WRAP T       integer CLAMP, CLAMP TO EDGE, REPEAT
         TEXTURE WRAP R       integer CLAMP, CLAMP TO EDGE, REPEAT
       TEXTURE MIN FILTER     integer NEAREST,
                                      LINEAR,
                                      NEAREST MIPMAP NEAREST,
                                      NEAREST MIPMAP LINEAR,
                                      LINEAR MIPMAP NEAREST,
                                      LINEAR MIPMAP LINEAR,
       TEXTURE MAG FILTER     integer NEAREST,
                                         LINEAR
      TEXTURE BORDER COLOR    4 oats     any 4 values in 0; 1
       TEXTURE PRIORITY          oat     any value in 0; 1
        TEXTURE MIN LOD          oat     any value
        TEXTURE MAX LOD          oat     any value
       TEXTURE BASE LEVEL     integer    any non-negative integer
       TEXTURE MAX LEVEL      integer    any non-negative integer
             Table 3.17: Texture parameters and their values.


target is the target, either TEXTURE 1D, TEXTURE 2D, or TEXTURE 3D. pname is
a symbolic constant indicating the parameter to be set; the possible con-
stants and corresponding parameters are summarized in table 3.17. In the
 rst form of the command, param is a value to which to set a single-valued
parameter; in the second form of the command, params is an array of pa-
rameters whose type depends on the parameter being set. If the values for
TEXTURE BORDER COLOR are speci ed as integers, the conversion for signed in-
tegers from table 2.6 is applied to convert the values to oating-point. Each
of the four values set by TEXTURE BORDER COLOR is clamped to lie in 0; 1 .

3.8.4 Texture Wrap Modes
If TEXTURE WRAP S, TEXTURE WRAP T, or TEXTURE WRAP R is set to REPEAT, then
the GL ignores the integer part of s, t, or r coordinates, respectively, using
only the fractional part. For a number f , the fractional part is f , bf c,
regardless of the sign of f ; recall that the oor function truncates towards
,1. CLAMP causes s, t, or r coordinates to be clamped to the range 0; 1 .




                    Version 1.2.1 - April 1, 1999
3.8. TEXTURING                                                              125

The initial state is for all of s, t, and r behavior to be that given by REPEAT.
   CLAMP TO EDGE clamps texture coordinates at all mipmap levels such that
the texture lter never samples a border texel. The color returned when
clamping is derived only from texels at the edge of the texture image.
   Texture coordinates are clamped to the range min; max . The mini-
mum value is de ned as
                                     min = 21N
where N is the size of the one-, two-, or three-dimensional texture image in
the direction of clamping. The maximum value is de ned as
                                max = 1 , min
so that clamping is always symmetric about the 0; 1 mapped range of a
texture coordinate.
3.8.5 Texture Mini cation
Applying a texture to a primitive implies a mapping from texture image
space to framebu er image space. In general, this mapping involves a recon-
struction of the sampled texture image, followed by a homogeneous warping
implied by the mapping to framebu er space, then a ltering, followed -
nally by a resampling of the ltered, warped, reconstructed image before
applying it to a fragment. In the GL this mapping is approximated by one
of two simple ltering schemes. One of these schemes is selected based on
whether the mapping from texture space to framebu er space is deemed to
magnify or minify the texture image.

Scale Factor and Level of Detail
The choice is governed by a scale factor x; y and the level of detail pa-
rameter x; y, de ned as
                            0 x; y = log2 x; y

      8
          TEXTURE MAX LOD; 0     TEXTURE MAX LOD

 =       0 ;              TEXTURE MIN LOD   0  TEXTURE MAX LOD 3.14
                MIN LOD; 0
      : TEXTURE
        undefined;
                                  TEXTURE MIN LOD
                         TEXTURE MIN LOD          TEXTURE MAX LOD




                                Version 1.2.1 - April 1, 1999
126                                         CHAPTER 3. RASTERIZATION

    If x; y is less than or equal to the constant c described below in
section 3.8.6 the texture is said to be magni ed; if it is greater, the texture
is mini ed.
    The initial values of TEXTURE MIN LOD and TEXTURE MAX LOD are chosen so
as to never clamp the normal range of . They may be respeci ed for a
speci c texture by calling TexParameter if .
    Let sx; y be the function that associates an s texture coordinate with
each set of window coordinates x; y that lie within a primitive; de ne
tx; y and rx; y analogously. Let ux; y = 2n sx; y, vx; y = 2m tx; y,
and wx; y = 2l rx; y, where n, m, and l are as de ned by equations 3.11,
3.12, and 3.13 with ws , hs , and ds equal to the width, height, and depth
of the image array whose level is TEXTURE BASE LEVEL. For a one-dimensional
texture, de ne vx; y  0 and wx; y  0; for a two-dimensional texture,
de ne wx; y  0. For a polygon, is given at a fragment with window
coordinates x; y by
         8s      s      9
   = max : @u
               2
                 + @v 2 + @w 2 ; @u 2 + @v 2 + @w 2 =
            @x     @x     @x     @y     @y     @y ;
                                                                  3.15
where @u=@x indicates the derivative of u with respect to window x, and
similarly for the other derivatives.
   For a line, the formula is
      s                 2                         2                 2
  =      @u x + @u y + @v x + @v y + @w x + @w y                        l;
        @x       @y      @x      @y      @x      @y
                                                                       3.16
where x = x2 , x1 and y = y2 , y1 with x1 ;py1  and x2 ; y2  being the
segment's window coordinate endpoints and l = x2 + y2 . For a point,
pixel rectangle, or bitmap,  1.
    While it is generally agreed that equations 3.15 and 3.16 give the best
results when texturing, they are often impractical to implement. Therefore,
an implementation may approximate the ideal with a function f x; y
subject to these conditions:
   1. f x; y is continuous and monotonically increasing in each of j@u=@xj,
      j@u=@yj, j@v=@xj, j@v=@yj, j@w=@xj, and j@w=@yj
   2. Let
                              mu = max @x @u ; @u
                                                 @y




                     Version 1.2.1 - April 1, 1999
3.8. TEXTURING                                                                    127


                                       @v ; @v
                              mv = max @x   @y

                             mw = max @w ;
                                      @x @y
                                           @w :

      Then maxfmu ; mv ; mw g  f x; y  mu + mv + mw .
    When  indicates mini cation, the value assigned to TEXTURE MIN FILTER
is used to determine how the texture value for a fragment is selected.
When TEXTURE MIN FILTER is NEAREST, the texel in the image array of level
TEXTURE BASE LEVEL that is nearest in Manhattan distance to that speci ed
by s; t; r is obtained. This means the texel at location i; j; k becomes the
texture value, with i given by
                                   
                            i=         buc; s 1                                3.17
                                       2n , 1; s = 1
Recall that if   TEXTURE WRAP S   is REPEAT, then 0  s           1. Similarly, j is
found as
                                   
                            j = b2vmc;, 1; tt = 11                             3.18
and k is found as
                                   
                              k = b2wl ,c; 1; rr = 11                 3.19
For a one-dimensional texture, j and k are irrelevant; the texel at location
i becomes the texture value. For a two-dimensional texture, k is irrelevant;
the texel at location i; j  becomes the texture value.
    When TEXTURE MIN FILTER is LINEAR, a 2  2  2 cube of texels in the
image array of level TEXTURE BASE LEVEL is selected. This cube is obtained by
 rst clamping texture coordinates as described above under Texture Wrap
Modes if the wrap mode for a coordinate is CLAMP or CLAMP TO EDGE and
computing
                  
           i0 = bbuu ,
                     , 1=2c mod 2n ; TEXTURE WRAP S is REPEAT
                       1=2c;         otherwise




                                   Version 1.2.1 - April 1, 1999
128                                           CHAPTER 3. RASTERIZATION

               
          j0 = bbvv , 1=2c mod 2m ; TEXTURE WRAP T is REPEAT
                    , 1=2c;         otherwise
and
                
          k0 = bbww ,
                    , 1=2c mod 2l ; TEXTURE WRAP R is REPEAT
                      1=2c;         otherwise
Then
                   
            i1 =       i0 + 1 mod 2n ; TEXTURE WRAP S is REPEAT
                       i0 + 1;           otherwise
                   
           j1 = jj0++11 mod 2m ; TEXTURE WRAP T is REPEAT
                  0 ;              otherwise
and
                   
            k1 = kk0++11 mod 2l ; TEXTURE WRAP R is REPEAT
                   0 ;              otherwise
Let
                               = fracu , 1=2
                               = fracv , 1=2
                               = fracw , 1=2
where fracx denotes the fractional part of x.
   For a three-dimensional texture, the texture value is found as

           = 1 , 1 , 1 ,  i0 j0 k0 + 1 , 1 ,  i1 j0 k0
              + 1 ,  1 ,  i0 j1 k0 + 1 ,  i1 j1 k0
              + 1 , 1 ,  i0 j0 k1 + 1 ,  i1 j0 k1
              + 1 ,  i0 j1 k1 +       i1 j1 k1
where ijk is the texel at location i; j; k in the three-dimensional texture
image.
   For a two-dimensional texture,




                       Version 1.2.1 - April 1, 1999
3.8. TEXTURING                                                             129


    = 1 , 1 ,  i0 j0 + 1 ,  i1 j0 + 1 ,  i0 j1 + i1 j1 3.20
where ij is the texel at location i; j  in the two-dimensional texture image.
   And for a one-dimensional texture,
                             = 1 ,  i0 + i1
   where i is the texel at location i in the one-dimensional texture.
   If any of the selected ijk , ij , or i in the above equations refer to a
border texel with i ,bs, j ,bs, k ,bs , i  ws , bs , j  hs , bs,
or j  ds , bs, then the border color given by the current setting of
TEXTURE BORDER COLOR is used instead of the unspeci ed value or values. The
RGBA values of the TEXTURE BORDER COLOR are interpreted to match the tex-
ture's internal format in a manner consistent with table 3.15.
Mipmapping
TEXTURE MIN FILTER   values NEAREST MIPMAP NEAREST, NEAREST MIPMAP LINEAR,
LINEAR MIPMAP NEAREST  , and LINEAR MIPMAP LINEAR each require the use of a
mipmap. A mipmap is an ordered set of arrays representing the same image;
each array has a resolution lower than the previous one. If the image array of
level TEXTURE BASE LEVEL, excluding its border, has dimensions 2n  2m  2l ,
then there are maxfn; m; lg + 1 image arrays in the mipmap. Each array
subsequent to the array of level TEXTURE BASE LEVEL has dimensions
                       i , 1  j , 1  k , 1
where the dimensions of the previous array are
                               i  j   k
and
                                     
                             x =       2x x 0
                                         1 x0
until the last array is reached with dimension 1  1  1.
    Each array in a mipmap is de ned using TexImage3D, TexImage2D,
CopyTexImage2D, TexImage1D, or CopyTexImage1D; the array be-
ing set is indicated with the level-of-detail argument level. Level-of-detail
numbers proceed from TEXTURE BASE LEVEL for the original texture array




                                Version 1.2.1 - April 1, 1999
130                                        CHAPTER 3. RASTERIZATION

through p = maxfn; m; lg + TEXTURE BASE LEVEL with each unit increase
indicating an array of half the dimensions of the previous one as already
described. If texturing is enabled and TEXTURE MIN FILTER is one that re-
quires a mipmap at the time a primitive is rasterized and if the set of
arrays TEXTURE BASE LEVEL through q = minfp; TEXTURE MAX LEVELg is incom-
plete, then it is as if texture mapping were disabled. The set of arrays
TEXTURE BASE LEVEL through q is incomplete if the internal formats of all
the mipmap arrays were not speci ed with the same symbolic constant, if
the border widths of the mipmap arrays are not the same, if the dimen-
sions of the mipmap arrays do not follow the sequence described above,
if TEXTURE MAX LEVEL TEXTURE BASE LEVEL, or if TEXTURE BASE LEVEL p.
Array levels k where k TEXTURE BASE LEVEL or k q are insigni cant.
    The values of TEXTURE BASE LEVEL and TEXTURE MAX LEVEL may be re-
speci ed for a speci c texture by calling TexParameter if . The error
INVALID VALUE is generated if either value is negative.
    The mipmap is used in conjunction with the level of detail to approxi-
mate the application of an appropriately ltered texture to a fragment. Let
c be the value of  at which the transition from mini cation to magni cation
occurs since this discussion pertains to mini cation, we are concerned only
with values of  where  c. In the following equations, let
    b = TEXTURE BASE LEVEL
    For mipmap lters NEAREST MIPMAP NEAREST and LINEAR MIPMAP NEAREST,
the dth mipmap array is selected, where
                  8
                   b;                  12
              d = db +  + 21 e , 1;  12 ; b +   q + 12            3.21
                 : q;                 12 ; b +  q + 12
    The rules for NEAREST or LINEAR ltering are then applied to the selected
array.
    For mipmap lters NEAREST MIPMAP LINEAR and LINEAR MIPMAP LINEAR, the
level d1 and d2 mipmap arrays are selected, where
                             
                       d1 = q;              b+q                     3.22
                             bb + c;       otherwise
                           
                       d2 = q;              b+  q                   3.23
                              d1 + 1;       otherwise
    The rules for NEAREST or LINEAR ltering are then applied to each of the
selected arrays, yielding two corresponding texture values 1 and 2 . The
 nal texture value is then found as




                    Version 1.2.1 - April 1, 1999
3.8. TEXTURING                                                              131


                         = 1 , frac 1 + frac 2 :

3.8.6 Texture Magni cation
When  indicates magni cation, the value assigned to TEXTURE MAG FILTER
determines how the texture value is obtained. There are two possible val-
ues for TEXTURE MAG FILTER: NEAREST and LINEAR. NEAREST behaves exactly as
NEAREST for TEXTURE MIN FILTER equations 3.17, 3.18, and 3.19 are used;
LINEAR behaves exactly as LINEAR for TEXTURE MIN FILTER equation 3.20 is
used. The level-of-detail TEXTURE BASE LEVEL texture array is always used
for magni cation.
     Finally, there is the choice of c, the mini cation vs. magni cation switch-
over point. If the magni cation lter is given by LINEAR and the mini cation
  lter is given by NEAREST MIPMAP NEAREST or NEAREST MIPMAP LINEAR, then c =
0:5. This is done to ensure that a mini ed texture does not appear sharper"
than a magni ed texture. Otherwise c = 0.

3.8.7 Texture State and Proxy State
The state necessary for texture can be divided into two categories. First,
there are the three sets of mipmap arrays one-, two-, and three-dimensional
and their number. Each array has associated with it a width, height two-
or three-dimensional only, and depth three-dimensional only, a border
width, an integer describing the internal format of the image, and six inte-
ger values describing the resolutions of each of the red, green, blue, alpha,
luminance, and intensity components of the image. Each initial texture
array is null zero width, height, and depth, zero border width, internal
format 1, with zero-sized components. Next, there are the two sets of
texture properties; each consists of the selected mini cation and magni -
cation lters, the wrap modes for s, t two- and three-dimensional only,
and r three-dimensional only, the TEXTURE BORDER COLOR, two integers de-
scribing the minimum and maximum level of detail, two integers describing
the base and maximum mipmap array, a boolean ag indicating whether
the texture is resident and the priority associated with each set of prop-
erties. The value of the resident ag is determined by the GL and may
change as a result of other GL operations. The ag may only be queried,
not set, by applications. See section 3.8.8. In the initial state, the value
assigned to TEXTURE MIN FILTER is NEAREST MIPMAP LINEAR, and the value for
TEXTURE MAG FILTER is LINEAR. s, t, and r wrap modes are all set to REPEAT.




                                Version 1.2.1 - April 1, 1999
132                                                 CHAPTER 3. RASTERIZATION

The values of TEXTURE MIN LOD and TEXTURE MAX LOD are -1000 and 1000 re-
spectively. The values of TEXTURE BASE LEVEL and TEXTURE MAX LEVEL are 0
and 1000 respectively. TEXTURE PRIORITY is 1.0, and TEXTURE BORDER COLOR is
0,0,0,0. The initial value of TEXTURE RESIDENT is determined by the GL.
    In addition to the one-, two-, and three-dimensional sets of image ar-
rays, partially instantiated one-, two-, and three-dimensional sets of proxy
image arrays are maintained. Each proxy array includes width, height two-
and three-dimensional arrays only, depth three-dimensional arrays only,
border width, and internal format state values, as well as state for the red,
green, blue, alpha, luminance, and intensity component resolutions. Proxy
arrays do not include image data, nor do they include texture properties.
When TexImage3D is executed with target speci ed as PROXY TEXTURE 3D,
the three-dimensional proxy state values of the speci ed level-of-detail are
recomputed and updated. If the image array would not be supported by
TexImage3D called with target set to TEXTURE 3D, no error is generated,
but the proxy width, height, depth, border width, and component resolu-
tions are set to zero. If the image array would be supported by such a call to
TexImage3D, the proxy state values are set exactly as though the actual
image array were being speci ed. No pixel data are transferred or processed
in either case.
    One- and two-dimensional proxy arrays are operated on in the same way
when TexImage1D is executed with target speci ed as PROXY TEXTURE 1D,
or TexImage2D is executed with target speci ed as PROXY TEXTURE 2D.
    There is no image associated with any of the proxy textures. Therefore
PROXY TEXTURE 1D, PROXY TEXTURE 2D, and PROXY TEXTURE 3D cannot be used
as textures, and their images must never be queried using GetTexImage.
The error INVALID ENUM is generated if this is attempted. Likewise, there
is no nonlevel-related state associated with a proxy texture, and GetTex-
Parameteriv or GetTexParameterfv may not be called with a proxy
texture target. The error INVALID ENUM is generated if this is attempted.

3.8.8 Texture Objects
In addition to the default textures TEXTURE 1D, TEXTURE 2D, and TEXTURE 3D
named one-, two-, and three-dimensional texture objects can be created and
operated upon. The name space for texture objects is the unsigned integers,
with zero reserved by the GL.
    A texture object is created by binding an unused name to TEXTURE 1D,
TEXTURE 2D, or TEXTURE 3D. The binding is e ected by calling




                    Version 1.2.1 - April 1, 1999
3.8. TEXTURING                                                            133

     void   BindTexture enum target, uint texture ;
with target set to the desired texture target and texture set to the unused
name. The resulting texture object is a new state vector, comprising all
the state values listed in section 3.8.7, set to the same initial values. If
the new texture object is bound to TEXTURE 1D, TEXTURE 2D, or TEXTURE 3D
respectively, it is and remains a one-, two-, or three-dimensional texture
until it is deleted.
    BindTexture may also be used to bind an existing texture object to
either TEXTURE 1D, TEXTURE 2D, or TEXTURE 3D. The error INVALID OPERATION
is generated if an attempt is made to bind a texture object of di erent
dimensionality than the speci ed target. If the bind is successful no change
is made to the state of the bound texture object, and any previous binding
to target is broken.
    While a texture object is bound, GL operations on the target to which
it is bound a ect the bound object, and queries of the target to which it
is bound return state from the bound object. If texture mapping of the
dimensionality of the target to which a texture object is bound is enabled,
the state of the bound texture object directs the texturing operation.
    In the initial state, TEXTURE 1D, TEXTURE 2D, and TEXTURE 3D have one-,
two-, and three-dimensional texture state vectors associated with them. In
order that access to these initial textures not be lost, they are treated as
texture objects all of whose names are 0. The initial one-, two-, or three-
dimensional texture is therefore operated upon, queried, and applied as
TEXTURE 1D, TEXTURE 2D, or TEXTURE 3D respectively while 0 is bound to the
corresponding targets.
    Texture objects are deleted by calling
     void   DeleteTextures sizei n, uint *textures ;
textures contains n names of texture objects to be deleted. After a texture
object is deleted, it has no contents or dimensionality, and its name is again
unused. If a texture that is currently bound to one of the targets TEXTURE 1D,
TEXTURE 2D, or TEXTURE 3D is deleted, it is as though BindTexture had been
executed with the same target and texture zero. Unused names in textures
are silently ignored, as is the value zero.
    The command
     void   GenTextures sizei n, uint *textures ;




                               Version 1.2.1 - April 1, 1999
134                                         CHAPTER 3. RASTERIZATION

returns n previously unused texture object names in textures. These names
are marked as used, for the purposes of GenTextures only, but they acquire
texture state and a dimensionality only when they are rst bound, just as
if they were unused.
    An implementation may choose to establish a working set of texture
objects on which binding operations are performed with higher performance.
A texture object that is currently part of the working set is said to be
resident. The command
      boolean   AreTexturesResident sizei n, uint *textures,
         boolean   *residences ;
returns TRUE if all of the n texture objects named in textures are resident,
or if the implementation does not distinguish a working set. If at least one
of the texture objects named in textures is not resident, then FALSE is re-
turned, and the residence of each texture object is returned in residences.
Otherwise the contents of residences are not changed. If any of the names in
textures are unused or are zero, FALSE is returned, the error INVALID VALUE is
generated, and the contents of residences are indeterminate. The residence
status of a single bound texture object can also be queried by calling Get-
TexParameteriv or GetTexParameterfv with target set to the target
to which the texture object is bound, and pname set to TEXTURE RESIDENT.
    AreTexturesResident indicates only whether a texture object is cur-
rently resident, not whether it could not be made resident. An implemen-
tation may choose to make a texture object resident only on rst use, for
example. The client may guide the GL implementation in determining which
texture objects should be resident by specifying a priority for each texture
object. The command
      void  PrioritizeTextures sizei n, uint *textures,
         clampf   *priorities ;
sets the priorities of the n texture objects named in textures to the values
in priorities. Each priority value is clamped to the range 0,1 before it is
assigned. Zero indicates the lowest priority, with the least likelihood of being
resident. One indicates the highest priority, with the greatest likelihood of
being resident. The priority of a single bound texture object may also be
changed by calling TexParameteri, TexParameterf, TexParameteriv,
or TexParameterfv with target set to the target to which the texture
object is bound, pname set to TEXTURE PRIORITY, and param or params




                     Version 1.2.1 - April 1, 1999
3.8. TEXTURING                                                             135

specifying the new priority value which is clamped to the range 0,1 before
being assigned. PrioritizeTextures silently ignores attempts to prioritize
unused texture object names or zero default textures.

3.8.9 Texture Environments and Texture Functions
The command

     void   TexEnvfifg enum target, enum pname, T param ;
     void   TexEnvfifgv enum target, enum pname, T params ;
sets parameters of the texture environment that speci es how texture values
are interpreted when texturing a fragment. target must currently be the
symbolic constant TEXTURE ENV. pname is a symbolic constant indicating the
parameter to be set. In the rst form of the command, param is a value
to which to set a single-valued parameter; in the second form, params is a
pointer to an array of parameters: either a single symbolic constant or a
value or group of values to which the parameter should be set. The pos-
sible environment parameters are TEXTURE ENV MODE and TEXTURE ENV COLOR.
TEXTURE ENV MODE may be set to one of REPLACE, MODULATE, DECAL, or BLEND;
TEXTURE ENV COLOR is set to an RGBA color by providing four single-precision
  oating-point values in the range 0; 1 values outside this range are clamped
to it. If integers are provided for TEXTURE ENV COLOR, then they are converted
to oating-point as speci ed in table 2.6 for signed integers.
     The value of TEXTURE ENV MODE speci es a texture function. The result
of this function depends on the fragment and the texture array value. The
precise form of the function depends on the base internal formats of the
texture arrays that were last speci ed. In the following two tables, Rf , Gf ,
Bf , and Af are the primary color components of the incoming fragment;
Rt , Gt, Bt , At , Lt, and It are the ltered texture values; Rc, Gc, Bc, and Ac
are the texture environment color values; and Rv , Gv , Bv , and Av are the
primary color components computed by the texture function. All of these
color values are in the range 0; 1 . The REPLACE and MODULATE texture func-
tions are speci ed in table 3.18, and the DECAL and BLEND texture functions
are speci ed in table 3.19.
     The state required for the current texture environment consists of the
four-valued integer indicating the texture function and four oating-point
TEXTURE ENV COLOR values. In the initial state, the texture function is given
by MODULATE and TEXTURE ENV COLOR is 0; 0; 0; 0.




                                Version 1.2.1 - April 1, 1999
136                                   CHAPTER 3. RASTERIZATION




            Base          REPLACE          MODULATE
      Internal Format Texture Function Texture Function
           ALPHA          Rv = Rf          Rv = Rf
                          Gv = Gf          Gv = Gf
                          Bv = Bf          Bv = Bf
                          Av = At         Av = Af At
         LUMINANCE        Rv = Lt         Rv = Rf Lt
           or 1         Gv = Lt         Gv = Gf Lt
                          Bv = Lt         Bv = Bf Lt
                          Av = Af          Av = Af
      LUMINANCE ALPHA     Rv = Lt         Rv = Rf Lt
           or 2         Gv = Lt         Gv = Gf Lt
                          Bv = Lt         Bv = Bf Lt
                          Av = At         Av = Af At
         INTENSITY        Rv = It         Rv = Rf It
                          Gv = It         Gv = Gf It
                          Bv = It         Bv = Bf It
                          Av = It         Av = Af It
            RGB           Rv = Rt        Rv = Rf Rt
           or 3         Gv = Gt        G v = Gf G t
                          Bv = Bt         Bv = Bf Bt
                          Av = Af          Av = Af
            RGBA          Rv = Rt        Rv = Rf Rt
           or 4         Gv = Gt        G v = Gf G t
                          Bv = Bt         Bv = Bf Bt
                          Av = At         Av = Af At
       Table 3.18: Replace and modulate texture functions.




               Version 1.2.1 - April 1, 1999
3.8. TEXTURING                                                       137




       Base                 DECAL                            BLEND
 Internal Format       Texture Function           Texture Function
      ALPHA               unde ned                    Rv = Rf
                                                      Gv = Gf
                                                      Bv = Bf
                                                     Av = Af At
    LUMINANCE             unde ned            Rv = Rf 1 , Lt  + Rc Lt
      or 1                                  Gv = Gf 1 , Lt  + GcLt
                                              Bv = Bf 1 , Lt  + BcLt
                                                      Av = Af
 LUMINANCE ALPHA          unde ned            Rv = Rf 1 , Lt  + Rc Lt
      or 2                                  Gv = Gf 1 , Lt  + GcLt
                                              Bv = Bf 1 , Lt  + BcLt
                                                     Av = Af At
    INTENSITY             unde ned             Rv = Rf 1 , It + Rc It
                                              Gv = Gf 1 , It  + GcIt
                                               Bv = Bf 1 , It + BcIt
                                               Av = Af 1 , It  + AcIt
       RGB                 Rv = Rt            Rv = Rf 1 , Rt  + RcRt
      or 3               Gv = Gt            Gv = Gf 1 , Gt  + GcGt
                           Bv = Bt            Bv = Bf 1 , Bt  + BcBt
                           Av = Af                    Av = Af
       RGBA        Rv = Rf 1 , At  + Rt At Rv = Rf 1 , Rt  + RcRt
      or 4       Gv = Gf 1 , At  + GtAt Gv = Gf 1 , Gt  + GcGt
                   Bv = Bf 1 , At + Bt At Bv = Bf 1 , Bt  + BcBt
                           Av = Af                   Av = Af At
             Table 3.19: Decal and blend texture functions.




                             Version 1.2.1 - April 1, 1999
138                                         CHAPTER 3. RASTERIZATION

3.8.10 Texture Application
Texturing is enabled or disabled using the generic Enable and Disable com-
mands, respectively, with the symbolic constants TEXTURE 1D, TEXTURE 2D, or
TEXTURE 3D to enable the one-, two-, or three-dimensional texture, respec-
tively. If both two- and one-dimensional textures are enabled, the two-
dimensional texture is used. If the three-dimensional and either of the
two- or one-dimensional textures is enabled, the three-dimensional texture
is used. If all texturing is disabled, a rasterized fragment is passed on unal-
tered to the next stage of the GL although its texture coordinates may be
discarded. Otherwise, a texture value is found according to the parameter
values of the currently bound texture image of the appropriate dimension-
ality using the rules given in sections 3.8.5 and 3.8.6. This texture value is
used along with the incoming fragment in computing the texture function
indicated by the currently bound texture environment. The result of this
function replaces the incoming fragment's primary R, G, B, and A values.
These are the color values passed to subsequent operations. Other data
associated with the incoming fragment remain unchanged, except that the
texture coordinates may be discarded.
    The required state is three bits indicating whether each of one-, two-, or
three-dimensional texturing is enabled or disabled. In the initial state, all
texturing is disabled.

3.9 Color Sum
At the beginning of color sum, a fragment has two RGBA colors: a primary
color cpri which texturing, if enabled, may have modi ed and a secondary
color csec. The components of these two colors are summed to produce a
single post-texturing RGBA color c. The components of c are then clamped
to the range 0; 1 .
    Color sum has no e ect in color index mode.

3.10 Fog
If enabled, fog blends a fog color with a rasterized fragment's post-texturing
color using a blending factor f . Fog is enabled and disabled with the Enable
and Disable commands using the symbolic constant FOG.
    This factor f is computed according to one of three equations:
                                f = exp,d  z ;                       3.24




                     Version 1.2.1 - April 1, 1999
3.10. FOG                                                                       139

                              f = exp,d  z2 ; or                        3.25
                                   f = ee ,
                                          ,s
                                            z                                3.26
z is the eye-coordinate distance from the eye, 0; 0; 0; 1 in eye coordinates,
to the fragment center. The equation, along with either d or e and s, is
speci ed with
      void   Fogfifg enum pname, T param ;
      void   Fogfifgv enum pname, T params ;
If pname is FOG MODE, then param must be, or params must point to an integer
that is one of the symbolic constants EXP, EXP2, or LINEAR, in which case
equation 3.24, 3.25, or 3.26, respectively, is selected for the fog calculation if,
when 3.26 is selected, e = s, results are unde ned. If pname is FOG DENSITY,
FOG START, or FOG END, then param is or params points to a value that is d,
s, or e, respectively. If d is speci ed less than zero, the error INVALID VALUE
results.
    An implementation may choose to approximate the eye-coordinate dis-
tance from the eye to each fragment center by jze j. Further, f need not
be computed at each fragment, but may be computed at each vertex and
interpolated as other data are.
    No matter which equation and approximation is used to compute f , the
result is clamped to 0; 1 to obtain the nal f .
    f is used di erently depending on whether the GL is in RGBA or color
index mode. In RGBA mode, if Cr represents a rasterized fragment's R, G,
or B value, then the corresponding value produced by fog is
                             C = fCr + 1 , f Cf :
The rasterized fragment's A value is not changed by fog blending. The R,
G, B, and A values of Cf are speci ed by calling Fog with pname equal to
FOG COLOR; in this case params points to four values comprising Cf . If these
are not oating-point values, then they are converted to oating-point using
the conversion given in table 2.6 for signed integers. Each component of Cf
is clamped to 0; 1 when speci ed.
    In color index mode, the formula for fog blending is
                                I = ir + 1 , f if
where ir is the rasterized fragment's color index and if is a single-precision
 oating-point value. 1 , f if is rounded to the nearest xed-point value




                                  Version 1.2.1 - April 1, 1999
140                                         CHAPTER 3. RASTERIZATION

with the same number of bits to the right of the binary point as ir , and the
integer portion of I is masked bitwise ANDed with 2n , 1, where n is the
number of bits in a color in the color index bu er bu ers are discussed in
chapter 4. The value of if is set by calling Fog with pname set to FOG INDEX
and param being or params pointing to a single value for the fog index. The
integer part of if is masked with 2n , 1.
    The state required for fog consists of a three valued integer to select the
fog equation, three oating-point values d, e, and s, an RGBA fog color and
a fog color index, and a single bit to indicate whether or not fog is enabled.
In the initial state, fog is disabled, FOG MODE is EXP, d = 1:0, e = 1:0, and
s = 0:0; Cf = 0; 0; 0; 0 and if = 0.

3.11 Antialiasing Application
Finally, if antialiasing is enabled for the primitive from which a rasterized
fragment was produced, then the computed coverage value is applied to the
fragment. In RGBA mode, the value is multiplied by the fragment's alpha
A value to yield a nal alpha value. In color index mode, the value is used
to set the low order bits of the color index value as described in section 3.2.




                     Version 1.2.1 - April 1, 1999
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
gether into a bitplane; each bitplane contains a single bit from each pixel.
These bitplanes are grouped into several logical bu ers. These are the color,
depth, stencil, and accumulation bu ers. The color bu er actually consists
of a number of bu ers: the front left bu er, the front right bu er, the back
left bu er, the back right bu er, and some number of auxiliary bu ers. Typ-
ically the contents of the front bu ers are displayed on a color monitor while
the contents of the back bu ers are invisible. Monoscopic contexts display
only the front left bu er; stereoscopic contexts display both the front left
and the front right bu ers. The contents of the auxiliary bu ers are never
visible. All color bu ers must have the same number of bitplanes, although
an implementation or context may choose not to provide right bu ers, back
bu ers, or auxiliary bu ers at all. Further, an implementation or context
may not provide depth, stencil, or accumulation bu ers.
     Color bu ers consist of either unsigned integer color indices or R, G, B,
and, optionally, A unsigned integer values. The number of bitplanes in each
of the color bu ers, the depth bu er, the stencil bu er, and the accumulation
bu er is xed and window dependent. If an accumulation bu er is provided,
                                     141



                               Version 1.2.1 - April 1, 1999
142CHAPTER 4. PER-FRAGMENT OPERATIONS AND THE FRAMEBUFFER


    Fragment               Pixel                                             Alpha
        +                                          Scissor
                         Ownership                                            Test
                                                    Test                   (RGBA Only)
   Associated              Test
      Data




                                    Depth buffer               Stencil
                                       Test                     Test



                     Framebuffer              Framebuffer



                         Blending                                           Logicop
                                                                                             To
                                               Dithering
                         (RGBA Only)                                                     Framebuffer



           Framebuffer                                       Framebuffer



   Figure 4.1. Per-fragment operations.


it must have at least as many bitplanes per R, G, and B color component
as do the color bu ers.
    The initial state of all provided bitplanes is unde ned.

4.1 Per-Fragment Operations
A fragment produced by rasterization with window coordinates of xw ; yw 
modi es the pixel in the framebu er at that location based on a number of
parameters and conditions. We describe these modi cations and tests, dia-
grammed in Figure 4.1, in the order in which they are performed. Figure 4.1
diagrams these modi cations and tests.

4.1.1 Pixel Ownership Test
The rst test is to determine if the pixel at location xw ; yw  in the frame-
bu er is currently owned by the GL more precisely, by this GL context. If
it is not, the window system decides the fate the incoming fragment. Pos-
sible results are that the fragment is discarded or that some subset of the
subsequent per-fragment operations are applied to the fragment. This test




                           Version 1.2.1 - April 1, 1999
4.1. PER-FRAGMENT OPERATIONS                                                  143

allows the window system to control the GL's behavior, for instance, when
a GL window is obscured.
4.1.2 Scissor test
The scissor test determines if xw ; yw  lies within the scissor rectangle de ned
by four values. These values are set with
      void   Scissor int left, int bottom, sizei width,
         sizei   height ;
If left  xw left + width and bottom  yw bottom + height, then the
scissor test passes. Otherwise, the test fails and the fragment is discarded.
The test is enabled or disabled using Enable or Disable using the con-
stant SCISSOR TEST. When disabled, it is as if the scissor test always passes.
If either width or height is less than zero, then the error INVALID VALUE is
generated. The state required consists of four integer values and a bit
indicating whether the test is enabled or disabled. In the initial state
left = bottom = 0; width and height are determined by the size of the
GL window. Initially, the scissor test is disabled.

4.1.3 Alpha test
This step applies only in RGBA mode. In color index mode, proceed to the
next step. The alpha test discards a fragment conditional on the outcome of
a comparison between the incoming fragment's alpha value and a constant
value. The comparison is enabled or disabled with the generic Enable and
Disable commands using the symbolic constant ALPHA TEST. When disabled,
it is as if the comparison always passes. The test is controlled with
      void   AlphaFunc enum func, clampf ref ;
func is a symbolic constant indicating the alpha test function; ref is a refer-
ence value. ref is clamped to lie in 0; 1 , and then converted to a xed-point
value according to the rules given for an A component in section 2.13.9. For
purposes of the alpha test, the fragment's alpha value is also rounded to
the nearest integer. The possible constants specifying the test function are
NEVER, ALWAYS, LESS, LEQUAL, EQUAL, GEQUAL, GREATER, or NOTEQUAL, meaning
pass the fragment never, always, if the fragment's alpha value is less than,
less than or equal to, equal to, greater than or equal to, greater than, or not
equal to the reference value, respectively.




                                 Version 1.2.1 - April 1, 1999
144CHAPTER 4. PER-FRAGMENT OPERATIONS AND THE FRAMEBUFFER

    The required state consists of the oating-point reference value, an eight-
valued integer indicating the comparison function, and a bit indicating if the
comparison is enabled or disabled. The initial state is for the reference value
to be 0 and the function to be ALWAYS. Initially, the alpha test is disabled.

4.1.4 Stencil test
The stencil test conditionally discards a fragment based on the outcome of a
comparison between the value in the stencil bu er at location xw ; yw  and
a reference value. The test is controlled with
      void   StencilFunc enum func, int ref, uint mask ;
      void   StencilOp enum sfail, enum dpfail, enum dppass ;
The test is enabled or disabled with the Enable and Disable commands, us-
ing the symbolic constant STENCIL TEST. When disabled, the stencil test and
associated modi cations are not made, and the fragment is always passed.
    ref is an integer reference value that is used in the unsigned stencil com-
parison. It is clamped to the range 0; 2s , 1 , where s is the number of bits
in the stencil bu er. func is a symbolic constant that determines the stencil
comparison function; the eight symbolic constants are NEVER, ALWAYS, LESS,
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
integer; values clamp at 0 and the maximum representable value. The same
symbolic values are given to indicate the stencil action if the depth bu er
test below fails dpfail, or if it passes dppass.
    If the stencil test fails, the incoming fragment is discarded. The state
required consists of the most recent values passed to StencilFunc and Sten-
cilOp, and a bit indicating whether stencil testing is enabled or disabled.




                     Version 1.2.1 - April 1, 1999
4.1. PER-FRAGMENT OPERATIONS                                                  145

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

      void   DepthFunc enum func ;

This command takes a single symbolic constant: one of NEVER, ALWAYS, LESS,
LEQUAL, EQUAL, GREATER, GEQUAL, NOTEQUAL. Accordingly, the depth bu er test
passes never, always, if the incoming fragment's zw value is less than, less
than or equal to, equal to, greater than, greater than or equal to, or not equal
to the depth value stored at the location given by the incoming fragment's
xw ; yw  coordinates.
    If the depth bu er test fails, the incoming fragment is discarded. The
stencil value at the fragment's xw ; yw  coordinates is updated according to
the function currently in e ect for depth bu er test failure. Otherwise, the
fragment continues to the next operation and the value of the depth bu er
at the fragment's xw ; yw  location is set to the fragment's zw value. In this
case the stencil value is updated according to the function currently in e ect
for depth bu er test success.
    The necessary state is an eight-valued integer and a single bit indicating
whether depth bu ering is enabled or disabled. In the initial state the
function is LESS and the test is disabled.
    If there is no depth bu er, it is as if the depth bu er test always passes.




                                 Version 1.2.1 - April 1, 1999
146CHAPTER 4. PER-FRAGMENT OPERATIONS AND THE FRAMEBUFFER

4.1.6 Blending
Blending combines the incoming fragment's R, G, B, and A values with the
R, G, B, and A values stored in the framebu er at the incoming fragment's
xw ; yw  location.
    This blending is dependent on the incoming fragment's alpha value and
that of the corresponding currently stored pixel. Blending applies only in
RGBA mode; in color index mode it is bypassed. Blending is enabled or
disabled using Enable or Disable with the symbolic constant BLEND. If it
is disabled, or if logical operation on color values is enabled section 4.1.8,
proceed to the next stage.
    In the following discussion, Cs refers to the source color for an incoming
fragment, Cd refers to the destination color at the corresponding framebu er
location, and Cc refers to a constant color in the GL state. Individual
RGBA components of these colors are denoted by subscripts of s, d, and c
respectively.
    Destination framebu er components are taken to be xed-point values
represented according to the scheme given in section 2.13.9 Final Color Pro-
cessing, as are source fragment components. Constant color components
are taken to be oating point values.
    Prior to blending, each xed-point color component undergoes an implied
conversion to oating point. This conversion must leave the values 0 and
1 invariant. Blending computations are treated as if carried out in oating
point.
    The commands that control blending are
      void   BlendColor clampf red, clampf green, clampf blue,
         clampf   alpha ;
      void   BlendEquation enum mode ;
      void   BlendFunc enum src, enum dst ;

Using BlendColor
The constant color Cc to be used in blending is speci ed with BlendColor.
The four parameters are clamped to the range 0; 1 before being stored.
The constant color can be used in both the source and destination blending
factors.
    BlendColor is an imaging subset feature see section 3.6.2, and is only
allowed when the imaging subset is supported.




                     Version 1.2.1 - April 1, 1999
4.1. PER-FRAGMENT OPERATIONS                                           147

Using BlendEquation
Blending capability is de ned by the blend equation. BlendEquation mode
FUNC ADD de nes the blending equation as


                             C = Cs S + Cd D
   where Cs and Cd are the source and destination colors, and S and D are
quadruplets of weighting factors as speci ed by BlendFunc.
   If mode is FUNC SUBTRACT, the blending equation is de ned as
                             C = Cs S , Cd D
   If mode is FUNC REVERSE SUBTRACT, the blending equation is de ned as
                             C = CdD , Cs S
   If mode is MIN, the blending equation is de ned as
                            C = minCs ; Cd 
   Finally, if mode is MAX, the blending equation is de ned as
                            C = maxCs ; Cd 
   The blending equation is evaluated separately for each color component
and the corresponding weighting factors.
   BlendEquation is an imaging subset feature see section 3.6.2. If
the imaging subset is not available, then blending always uses the blending
equation FUNC ADD.
Using BlendFunc
BlendFunc src indicates how to compute a source blending factor, while
dst indicates how to compute a destination factor. The possible arguments
and their corresponding computed source and destination factors are sum-
marized in Tables 4.1 and 4.2. Addition or subtraction of quadruplets means
adding or subtracting them component-wise.
    The computed source and destination blending quadruplets are applied
to the source and destination R, G, B, and A values to obtain a new set of
values that are sent to the next operation. Let the source and destination
blending quadruplets be S and D, respectively. Then a quadruplet of values
is computed using the blend equation speci ed by BlendEquation. Each




                              Version 1.2.1 - April 1, 1999
148CHAPTER 4. PER-FRAGMENT OPERATIONS AND THE FRAMEBUFFER


         Value                            Blend Factors
         ZERO                             0; 0; 0; 0
         ONE                              1; 1; 1; 1
         DST COLOR                        Rd ; Gd ; Bd ; Ad 
         ONE MINUS DST COLOR              1; 1; 1; 1 , Rd ; Gd ; Bd ; Ad 
         SRC ALPHA                        As ; As ; As ; As 
         ONE MINUS SRC ALPHA              1; 1; 1; 1 , As ; As ; As ; As 
         DST ALPHA                        Ad ; Ad ; Ad ; Ad 
         ONE MINUS DST ALPHA              1; 1; 1; 1 , Ad ; Ad ; Ad ; Ad 
         CONSTANT COLOR                   Rc ; Gc; Bc ; Ac 
         ONE MINUS CONSTANT COLOR         1; 1; 1; 1 , Rc ; Gc; Bc ; Ac 
         CONSTANT ALPHA                   Ac ; Ac ; Ac ; Ac 
         ONE MINUS CONSTANT ALPHA         1; 1; 1; 1 , Ac ; Ac ; Ac ; Ac 
         SRC ALPHA SATURATE               f; f; f; 1
Table 4.1: Values controlling the source blending function and the source
blending values they compute. f = minAs ; 1 , Ad .


         Value                            Blend factors
         ZERO                             0; 0; 0; 0
         ONE                              1; 1; 1; 1
         SRC COLOR                        Rs ; Gs ; Bs ; As 
         ONE MINUS SRC COLOR              1; 1; 1; 1 , Rs ; Gs ; Bs ; As 
         SRC ALPHA                        As ; As ; As ; As 
         ONE MINUS SRC ALPHA              1; 1; 1; 1 , As ; As ; As ; As 
         DST ALPHA                        Ad ; Ad ; Ad ; Ad 
         ONE MINUS DST ALPHA              1; 1; 1; 1 , Ad ; Ad ; Ad ; Ad 
         CONSTANT COLOR                   Rc ; Gc ; Bc ; Ac 
         ONE MINUS CONSTANT COLOR         1; 1; 1; 1 , Rc ; Gc ; Bc ; Ac 
         CONSTANT ALPHA                   Ac ; Ac ; Ac ; Ac 
         ONE MINUS CONSTANT ALPHA         1; 1; 1; 1 , Ac ; Ac ; Ac ; Ac 
Table 4.2: Values controlling the destination blending function and the des-
tination blending values they compute.




                     Version 1.2.1 - April 1, 1999
4.1. PER-FRAGMENT OPERATIONS                                              149

 oating-point value in this quadruplet is clamped to 0; 1 and converted
back to a xed-point value in the manner described in section 2.13.9. The
resulting four values are sent to the next operation.
    BlendFunc arguments CONSTANT COLOR, ONE MINUS CONSTANT COLOR,
CONSTANT ALPHA, and ONE MINUS CONSTANT ALPHA are imaging subset features
see section 3.6.2, and are only allowed when the imaging subset is provided.

Blending State
The state required for blending is an integer indicating the blending equa-
tion, two integers indicating the source and destination blending functions,
four oating-point values to store the RGBA constant blend color, and a
bit indicating whether blending is enabled or disabled. The initial blending
equation is FUNC ADD. The initial blending functions are ONE for the source
function and ZERO for the destination function. The initial constant blend
color is R; G; B; A = 0; 0; 0; 0. Initially, blending is disabled.
    Blending occurs once for each color bu er currently enabled for writing
section 4.2.1 using each bu er's color for Cd . If a color bu er has no A
value, then Ad is taken to be 1.

4.1.7 Dithering
Dithering selects between two color values or indices. In RGBA mode, con-
sider the value of any of the color components as a xed-point value with m
bits to the left of the binary point, where m is the number of bits allocated
to that component in the framebu er; call each such value c. For each c,
dithering selects a value c1 such that c1 2 fmaxf0; dce , 1g; dceg after this
selection, treat c1 as a xed point value in 0,1 with m bits. This selec-
tion may depend on the xw and yw coordinates of the pixel. In color index
mode, the same rule applies with c being a single color index. c must not be
larger than the maximum value representable in the framebu er for either
the component or the index, as appropriate.
    Many dithering algorithms are possible, but a dithered value produced
by any algorithm must depend only the incoming value and the fragment's x
and y window coordinates. If dithering is disabled, then each color compo-
nent is truncated to a xed-point value with as many bits as there are in the
corresponding component in the framebu er; a color index is rounded to the
nearest integer representable in the color index portion of the framebu er.
    Dithering is enabled with Enable and disabled with Disable using the




                               Version 1.2.1 - April 1, 1999
150CHAPTER 4. PER-FRAGMENT OPERATIONS AND THE FRAMEBUFFER

symbolic constant DITHER. The state required is thus a single bit. Initially,
dithering is enabled.
4.1.8 Logical Operation
Finally, a logical operation is applied between the incoming fragment's color
or index values and the color or index values stored at the corresponding
location in the framebu er. The result replaces the values in the framebu er
at the fragment's x; y coordinates. The logical operation on color indices
is enabled or disabled with Enable or Disable using the symbolic constant
INDEX LOGIC OP. For compatibility with GL version 1.0, the symbolic con-
stant LOGIC OP may also be used. The logical operation on color values is
enabled or disabled with Enable or Disable using the symbolic constant
COLOR LOGIC OP. If the logical operation is enabled for color values, it is as if
blending were disabled, regardless of the value of BLEND.
    The logical operation is selected by
      void   LogicOp enum op ;
op is a symbolic constant; the possible constants and corresponding opera-
tions are enumerated in Table 4.3. In this table, s is the value of the incoming
fragment and d is the value stored in the framebu er. The numeric values
assigned to the symbolic constants are the same as those assigned to the
corresponding symbolic values in the X window system.
    Logical operations are performed independently for each color index
bu er that is selected for writing, or for each red, green, blue, and alpha
value of each color bu er that is selected for writing. The required state is
an integer indicating the logical operation, and two bits indicating whether
the logical operation is enabled or disabled. The initial state is for the logic
operation to be given by COPY, and to be disabled.

4.2 Whole Framebu er Operations
The preceding sections described the operations that occur as individual
fragments are sent to the framebu er. This section describes operations
that control or a ect the whole framebu er.
4.2.1 Selecting a Bu er for Writing
The rst such operation is controlling the bu er into which color values are
written. This is accomplished with




                     Version 1.2.1 - April 1, 1999
4.2. WHOLE FRAMEBUFFER OPERATIONS                                         151

                        Argument value Operation
                        CLEAR          0
                        AND                   s^d
                        AND REVERSE           s ^ :d
                        COPY                  s
                        AND INVERTED          :s ^ d
                        NOOP                  d
                        XOR                   s xor d
                        OR                    s_d
                        NOR                   :s _ d
                        EQUIV                 :s xor d
                        INVERT                :d
                        OR REVERSE            s _ :d
                        COPY INVERTED         :s
                        OR INVERTED           :s _ d
                        NAND                  :s ^ d
                        SET                   all 1's
  Table 4.3: Arguments to LogicOp and their corresponding operations.

     void   DrawBu er enum buf ;
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
is supplied with a constant other than NONE that does not indicate any of
the color bu ers allocated to the GL context, the error INVALID OPERATION
results.
    Indicating a bu er or bu ers using DrawBu er causes subsequent pixel
color value writes to a ect the indicated bu ers. If more than one color
bu er is selected for drawing, blending and logical operations are computed




                                 Version 1.2.1 - April 1, 1999
152CHAPTER 4. PER-FRAGMENT OPERATIONS AND THE FRAMEBUFFER

            symbolic              front front back back aux
            constant               left right left right i
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
            AUX   i
Table 4.4: Arguments to DrawBu er and the bu ers that they indicate.


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
the initial state, the front bu er or bu ers are enabled if there are no back
bu ers; otherwise, only the back bu er or bu ers are enabled.

4.2.2 Fine Control of Bu er Updates
Four commands are used to mask the writing of bits to each of the logical
framebu ers after all per-fragment operations have been performed. The
commands

     void   IndexMask uint mask ;
     void   ColorMask boolean r, boolean g, boolean b,
        boolean       a ;




                       Version 1.2.1 - April 1, 1999
4.2. WHOLE FRAMEBUFFER OPERATIONS                                         153

control the color bu er or bu ers depending on which bu ers are currently
indicated for writing. The least signi cant n bits of mask, where n is the
number of bits in a color index bu er, specify a mask. Where a 1 appears
in this mask, the corresponding bit in the color index bu er or bu ers is
written; where a 0 appears, the bit is not written. This mask applies only in
color index mode. In RGBA mode, ColorMask is used to mask the writing
of R, G, B and A values to the color bu er or bu ers. r, g, b, and a indicate
whether R, G, B, or A values, respectively, are written or not a value of
TRUE means that the corresponding value is written. In the initial state, all
bits in color index mode and all color values in RGBA mode are enabled
for writing.
    The depth bu er can be enabled or disabled for writing zw values using
     void   DepthMask boolean mask ;
If mask is non-zero, the depth bu er is enabled for writing; otherwise, it is
disabled. In the initial state, the depth bu er is enabled for writing.
    The command
     void   StencilMask uint mask ;
controls the writing of particular bits into the stencil planes. The least
signi cant s bits of mask comprise an integer mask s is the number of bits
in the stencil bu er, just as for IndexMask. The initial state is for the
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
     void   Clear bitfield buf ;
is the bitwise OR of a number of values indicating which bu ers
are to be cleared. The values are COLOR BUFFER BIT, DEPTH BUFFER BIT,




                               Version 1.2.1 - April 1, 1999
154CHAPTER 4. PER-FRAGMENT OPERATIONS AND THE FRAMEBUFFER

STENCIL BUFFER BIT , and ACCUM BUFFER BIT, indicating the bu ers currently
enabled for color writing, the depth bu er, the stencil bu er, and the accu-
mulation bu er see below, respectively. The value to which each bu er is
cleared depends on the setting of the clear value for that bu er. If the mask
is not a bitwise OR of the speci ed values, then the error INVALID VALUE is
generated.
     void   ClearColor clampf r, clampf g, clampf b,
        clampf   a ;
sets the clear value for the color bu ers in RGBA mode. Each of the speci ed
components is clamped to 0; 1 and converted to xed-point according to
the rules of section 2.13.9.
     void   ClearIndex float index ;
sets the clear color index. index is converted to a xed-point value with
unspeci ed precision to the left of the binary point; the integer part of this
value is then masked with 2m , 1, where m is the number of bits in a color
index value stored in the framebu er.
     void   ClearDepth clampd d ;
takes a oating-point value that is clamped to the range 0; 1 and con-
verted to xed-point according to the rules for a window z value given in
section 2.10.1. Similarly,
     void   ClearStencil int s ;
takes a single integer argument that is the value to which to clear the stencil
bu er. s is masked to the number of bitplanes in the stencil bu er.
     void   ClearAccum float r, float g, float b, float a ;
takes four oating-point arguments that are the values, in order, to which
to set the R, G, B, and A values of the accumulation bu er see the next
section. These values are clamped to the range ,1; 1 when they are spec-
i ed.
     When Clear is called, the only per-fragment operations that are applied
if enabled are the pixel ownership test, the scissor test, and dithering. The
masking operations described in the last section 4.2.2 are also e ective. If
a bu er is not present, then a Clear directed at that bu er has no e ect.




                     Version 1.2.1 - April 1, 1999
4.2. WHOLE FRAMEBUFFER OPERATIONS                                            155

    The state required for clearing is a clear value for each of the color bu er,
the depth bu er, the stencil bu er, and the accumulation bu er. Initially,
the RGBA color clear value is 0,0,0,0, the clear color index is 0, and the
stencil bu er and accumulation bu er clear values are all 0. The depth
bu er clear value is initially 1.0.

4.2.4 The Accumulation Bu er
Each portion of a pixel in the accumulation bu er consists of four values: one
for each of R, G, B, and A. The accumulation bu er is controlled exclusively
through the use of
      void   Accum enum op, float value ;
except for clearing it. op is a symbolic constant indicating an accumula-
tion bu er operation, and value is a oating-point value to be used in that
operation. The possible operations are ACCUM, LOAD, RETURN, MULT, and ADD.
    When the scissor test is enabled section 4.1.2, then only those pix-
els within the current scissor box are updated by any Accum operation;
otherwise, all pixels in the window are updated. The accumulation bu er
operations apply identically to every a ected pixel, so we describe the e ect
of each operation on an individual pixel. Accumulation bu er values are
taken to be signed values in the range ,1; 1 . Using ACCUM obtains R, G,
B, and A components from the bu er currently selected for reading sec-
tion 4.3.2. Each component, considered as a xed-point value in 0; 1 . see
section 2.13.9, is converted to oating-point. Each result is then multiplied
by value. The results of this multiplication are then added to the corre-
sponding color component currently in the accumulation bu er, and the
resulting color value replaces the current accumulation bu er color value.
    The LOAD operation has the same e ect as ACCUM, but the computed values
replace the corresponding accumulation bu er components rather than being
added to them.
    The RETURN operation takes each color value from the accumulation
bu er, multiplies each of the R, G, B, and A components by value, and
clamps the results to the range 0; 1 The resulting color value is placed
in the bu ers currently enabled for color writing as if it were a fragment
produced from rasterization, except that the only per-fragment operations
that are applied if enabled are the pixel ownership test, the scissor test
section 4.1.2, and dithering section 4.1.7. Color masking section 4.2.2
is also applied.




                                 Version 1.2.1 - April 1, 1999
156CHAPTER 4. PER-FRAGMENT OPERATIONS AND THE FRAMEBUFFER

    The MULT operation multiplies each R, G, B, and A in the accumulation
bu er by value and then returns the scaled color components to their corre-
sponding accumulation bu er locations. ADD is the same as MULT except that
value is added to each of the color components.
    The color components operated on by Accum must be clamped only if
the operation is RETURN. In this case, a value sent to the enabled color bu ers
is rst clamped to 0; 1 . Otherwise, results are unde ned if the result of an
operation on a color component is out of the range ,1; 1 . If there is no
accumulation bu er, or if the GL is in color index mode, Accum generates
the error INVALID OPERATION.
    No state beyond the accumulation bu er itself is required for accumu-
lation bu ering.

4.3 Drawing, Reading, and Copying Pixels
Pixels may be written to and read from the framebu er using the Draw-
Pixels and ReadPixels commands. CopyPixels can be used to copy a
block of pixels from one portion of the framebu er to another.

4.3.1 Writing to the Stencil Bu er
The operation of DrawPixels was described in section 3.6.4, except if the
format argument was STENCIL INDEX. In this case, all operations described for
DrawPixels take place, but window x; y coordinates, each with the corre-
sponding stencil index, are produced in lieu of fragments. Each coordinate-
stencil index pair is sent directly to the per-fragment operations, bypassing
the texture, fog, and antialiasing application stages of rasterization. Each
pair is then treated as a fragment for purposes of the pixel ownership and
scissor tests; all other per-fragment operations are bypassed. Finally, each
stencil index is written to its indicated location in the framebu er, subject
to the current setting of StencilMask.
    The error INVALID OPERATION results if there is no stencil bu er.

4.3.2 Reading Pixels
The method for reading pixels from the framebu er and placing them in
client memory is diagrammed in Figure 4.2. We describe the stages of the
pixel reading process in the order in which they occur.
    Pixels are read using




                     Version 1.2.1 - April 1, 1999
4.3. DRAWING, READING, AND COPYING PIXELS                                                  157


       RGBA pixel                                    color index pixel
         data in                                          data in

                           convert
                           to float



                            scale              Pixel Transfer                 shift
                           and bias             Operations                  and offset



                       RGBA to RGBA              index to RGBA            index to index
                          lookup                     lookup                  lookup



                          color table
                            lookup



                         convolution               color table        post
                        scale and bias               lookup       color matrix



        post              color table              histogram
     convolution            lookup



                         color matrix               minmax
                        scale and bias




                           convert              Pixel Storage
                           RGB to L              Operations

                             clamp                                           mask to
                            to [0,1]                                         (2n − 1)



                                                      pack


                       byte, short, int, or float pixel
                    data stream (index or component)



  Figure 4.2. Operation of ReadPixels. Operations in dashed boxes may be
  enabled or disabled. RGBA and color index pixel paths are shown; depth
  and stencil pixel paths are not shown.




                                        Version 1.2.1 - April 1, 1999
158CHAPTER 4. PER-FRAGMENT OPERATIONS AND THE FRAMEBUFFER

         Parameter Name         Type Initial Value Valid Range
          PACK SWAP BYTES      boolean   FALSE     TRUE FALSE
          PACK LSB FIRST       boolean   FALSE     TRUE FALSE
          PACK ROW LENGTH      integer     0           0; 1
          PACK SKIP ROWS       integer     0           0; 1
         PACK SKIP PIXELS      integer     0           0; 1
          PACK ALIGNMENT       integer     4         1,2,4,8
        PACK IMAGE HEIGHT      integer     0           0; 1
         PACK SKIP IMAGES      integer     0           0; 1
Table 4.5: PixelStore parameters pertaining to ReadPixels, GetTex-
Image1D, GetTexImage2D, GetTexImage3D, GetColorTable, Get-
ConvolutionFilter, GetSeparableFilter, GetHistogram, and Get-
Minmax.

     void   ReadPixels int x, int y, sizei width, sizei height,
        enum   format, enum type, void *data ;
The arguments after x and y to ReadPixels correspond to those of Draw-
Pixels. The pixel storage modes that apply to ReadPixels and other
commands that query images see section 6.1 are summarized in Table 4.5.
Obtaining Pixels from the Framebu er
If the format is DEPTH COMPONENT, then values are obtained from the depth
bu er. If there is no depth bu er, the error INVALID OPERATION occurs.
    If the format is STENCIL INDEX, then values are taken from the stencil
bu er; again, if there is no stencil bu er, the error INVALID OPERATION occurs.
    For all other formats, the bu er from which values are obtained is one of
the color bu ers; the selection of color bu er is controlled with ReadBu er.
    The command
     void   ReadBu er enum src ;
takes a symbolic constant as argument. The possible values are FRONT LEFT,
FRONT RIGHT, BACK LEFT, BACK RIGHT, FRONT, BACK, LEFT, RIGHT, and AUX0
through AUXn. FRONT and LEFT refer to the front left bu er, BACK refers
to the back left bu er, and RIGHT refers to the front right bu er. The other
constants correspond directly to the bu ers that they name. If the requested




                     Version 1.2.1 - April 1, 1999
4.3. DRAWING, READING, AND COPYING PIXELS                                  159

bu er is missing, then the error INVALID OPERATION is generated. The ini-
tial setting for ReadBu er is FRONT if there is no back bu er and BACK
otherwise.
    ReadPixels obtains values from the selected bu er from each pixel with
lower left hand corner at x + i; y + j  for 0  i width and 0  j
height; this pixel is said to be the ith pixel in the j th row. If any of these
pixels lies outside of the window allocated to the current GL context, the
values obtained for those pixels are unde ned. Results are also unde ned
for individual pixels that are not owned by the current context. Otherwise,
ReadPixels obtains values from the selected bu er, regardless of how those
values were placed there.
    If the GL is in RGBA mode, and format is one of RED, GREEN, BLUE, ALPHA,
RGB, RGBA, BGR, BGRA, LUMINANCE, or LUMINANCE ALPHA, then red, green, blue,
and alpha values are obtained from the selected bu er at each pixel location.
If the framebu er does not support alpha values then the A that is obtained
is 1.0. If format is COLOR INDEX and the GL is in RGBA mode then the error
INVALID OPERATION occurs. If the GL is in color index mode, and format is
not DEPTH COMPONENT or STENCIL INDEX, then the color index is obtained at
each pixel location.

Conversion of RGBA values
This step applies only if the GL is in RGBA mode, and then only if format
is neither STENCIL INDEX nor DEPTH COMPONENT. The R, G, B, and A values
form a group of elements. Each element is taken to be a xed-point value in
 0; 1 with m bits, where m is the number of bits in the corresponding color
component of the selected bu er see section 2.13.9.

Conversion of Depth values
This step applies only if format is DEPTH COMPONENT. An element is taken to
be a xed-point value in 0,1 with m bits, where m is the number of bits in
the depth bu er see section 2.10.1.

Pixel Transfer Operations
This step is actually the sequence of steps that was described separately in
section 3.6.5. After the processing described in that section is completed,
groups are processed as described in the following sections.




                                Version 1.2.1 - April 1, 1999
160CHAPTER 4. PER-FRAGMENT OPERATIONS AND THE FRAMEBUFFER

                       type Parameter Index Mask
                        UNSIGNED BYTE 28 , 1
                           BITMAP     1
                            BYTE      27 , 1
                       UNSIGNED SHORT 216 , 1
                            SHORT     215 , 1
                        UNSIGNED INT  232 , 1
                             INT      231 , 1
Table 4.6: Index masks used by ReadPixels. Floating point data are not
masked.

Conversion to L
This step applies only to RGBA component groups, and only if the format
is either LUMINANCE or LUMINANCE ALPHA. A value L is computed as
                               L = R+G+B
where R, G, and B are the values of the R, G, and B components. The
single computed L component replaces the R, G, and B components in the
group.
Final Conversion
For an index, if the type is not FLOAT, nal conversion consists of masking
the index with the value given in Table 4.6; if the type is FLOAT, then the
integer index is converted to a GL oat data value.
    For an RGBA color, each component is rst clamped to 0; 1 . Then the
appropriate conversion formula from table 4.7 is applied to the component.
Placement in Client Memory
Groups of elements are placed in memory just as they are taken from mem-
ory for DrawPixels. That is, the ith group of the j th row corresponding
to the ith pixel in the j th row is placed in memory just where the ith group
of the j th row would be taken from for DrawPixels. See Unpacking un-
der section 3.6.4. The only di erence is that the storage mode parameters
whose names begin with PACK are used instead of those whose names be-
gin with UNPACK . If the format is RED, GREEN, BLUE, ALPHA, or LUMINANCE,




                    Version 1.2.1 - April 1, 1999
4.3. DRAWING, READING, AND COPYING PIXELS                                 161



         type Parameter           GL Data Type Component
                                               Conversion Formula
          UNSIGNED BYTE               ubyte    c = 28 , 1f
               BYTE                   byte     c = 28 , 1f , 1 =2
         UNSIGNED SHORT              ushort    c = 216 , 1f
              SHORT                   short    c = 216 , 1f , 1 =2
          UNSIGNED INT                uint     c = 232 , 1f
               INT                     int     c = 232 , 1f , 1 =2
              FLOAT                   float    c=f
       UNSIGNED BYTE 3 3 2            ubyte    c = 2N , 1f
     UNSIGNED BYTE 2 3 3 REV          ubyte    c = 2N , 1f
      UNSIGNED SHORT 5 6 5           ushort    c = 2N , 1f
    UNSIGNED SHORT 5 6 5 REV         ushort    c = 2N , 1f
     UNSIGNED SHORT 4 4 4 4          ushort    c = 2N , 1f
   UNSIGNED SHORT 4 4 4 4 REV        ushort    c = 2N , 1f
     UNSIGNED SHORT 5 5 5 1          ushort    c = 2N , 1f
   UNSIGNED SHORT 1 5 5 5 REV        ushort    c = 2N , 1f
      UNSIGNED INT 8 8 8 8            uint     c = 2N , 1f
    UNSIGNED INT 8 8 8 8 REV          uint     c = 2N , 1f
     UNSIGNED INT 10 10 10 2          uint     c = 2N , 1f
  UNSIGNED INT 2 10 10 10 REV         uint     c = 2N , 1f
Table 4.7: Reversed component conversions - used when component data
are being returned to client memory. Color, normal, and depth components
are converted from the internal oating-point representation f  to a datum
of the speci ed GL data type c using the equations in this table. All arith-
metic is done in the internal oating point format. These conversions apply
to component data returned by GL query commands and to components of
pixel data returned to client memory. The equations remain the same even
if the implemented ranges of the GL data types are greater than the mini-
mum required ranges. See Table 2.2. Equations with N as the exponent
are performed for each bit eld of the packed data type, with N set to the
number of bits in the bit eld.




                                Version 1.2.1 - April 1, 1999
162CHAPTER 4. PER-FRAGMENT OPERATIONS AND THE FRAMEBUFFER

only the corresponding single element is written. Likewise if the format is
LUMINANCE ALPHA, RGB, or BGR, only the corresponding two or three elements
are written. Otherwise all the elements of each group are written.
4.3.3 Copying Pixels
CopyPixels transfers a rectangle of pixel values from one region of the
framebu er to another. Pixel copying is diagrammed in Figure 4.3.
      void  CopyPixels int x, int y, sizei width, sizei height,
         enum   type ;
type is a symbolic constant that must be one of COLOR, STENCIL, or DEPTH,
indicating that the values to be transferred are colors, stencil values, or depth
values, respectively. The rst four arguments have the same interpretation
as the corresponding arguments to ReadPixels.
    Values are obtained from the framebu er, converted if appropriate,
then subjected to the pixel transfer operations described in section 3.6.5,
just as if ReadPixels were called with the corresponding arguments. If the
type is STENCIL or DEPTH, then it is as if the format for ReadPixels were
STENCIL INDEX or DEPTH COMPONENT, respectively. If the type is COLOR, then if
the GL is in RGBA mode, it is as if the format were RGBA, while if the GL
is in color index mode, it is as if the format were COLOR INDEX.
    The groups of elements so obtained are then written to the framebu er
just as if DrawPixels had been given width and height, beginning with
  nal conversion of elements. The e ective format is the same as that already
described.
4.3.4 Pixel Draw Read state
The state required for pixel operations consists of the parameters that are
set with PixelStore, PixelTransfer, and PixelMap. This state has been
summarized in Tables 3.1, 3.2, and 3.3. The current setting of ReadBu er,
an integer, is also required, along with the current raster position sec-
tion 2.12. State set with PixelStore is GL client state.




                     Version 1.2.1 - April 1, 1999
4.3. DRAWING, READING, AND COPYING PIXELS                                               163



        RGBA pixel                             color index pixel
   data from framebuffer                     data from framebuffer

                        convert
                        to float



                         scale             Pixel Transfer                  shift
                        and bias            Operations                   and offset



                   RGBA to RGBA             index to RGBA              index to index
                      lookup                    lookup                    lookup



                     color table
                       lookup



                     convolution              color table          post
                    scale and bias              lookup         color matrix



      post           color table              histogram
   convolution         lookup



                     color matrix              minmax
                    scale and bias




                         clamp                  final                     mask to
                        to [0,1]             conversion                   (2n − 1)

           RGBA pixel                                       color index pixel
            data out                                            data out



  Figure 4.3. Operation of CopyPixels. Operations in dashed boxes may be
  enabled or disabled. Index-to-RGBA lookup is currently never performed.
  RGBA and color index pixel paths are shown; depth and stencil pixel paths
  are not shown.




                                     Version 1.2.1 - April 1, 1999
Chapter 5
Special Functions
This chapter describes additional GL functionality that does not t easily
into any of the preceding chapters. This functionality consists of evalua-
tors used to model curves and surfaces, selection used to locate rendered
primitives on the screen, feedback which returns GL results before raster-
ization, display lists used to designate a group of GL commands for later
execution by the GL, ushing and nishing used to synchronize the GL
command stream, and hints.

5.1 Evaluators
Evaluators provide a means to use a polynomial or rational polynomial map-
ping to produce vertex, normal, and texture coordinates, and colors. The
values so produced are sent on to further stages of the GL as if they had
been provided directly by the client. Transformations, lighting, primitive
assembly, rasterization, and per-pixel operations are not a ected by the use
of evaluators.
    Consider the Rk -valued polynomial pu de ned by
                                      X
                                      n
                            pu =          Bin uRi                  5.1
                                      i=0
with Ri 2 Rk and                   !
                        Binu =  n ui 1 , un,i;
                                  i
                                                                ,
the ith Bernstein polynomial of degree n recall that 00  1 and n0  1.
Each Ri is a control point. The relevant command is
                                      164



                    Version 1.2.1 - April 1, 1999
5.1. EVALUATORS                                                             165

  target                    k Values
  MAP1 VERTEX 3             3 x, y, z vertex coordinates
  MAP1 VERTEX 4             4 x, y, z , w vertex coordinates
  MAP1 INDEX                1   color index
  MAP1 COLOR 4              4   R, G, B, A
  MAP1 NORMAL               3   x, y, z normal coordinates
  MAP1 TEXTURE COORD 1      1   s texture coordinate
  MAP1 TEXTURE COORD 2      2   s, t texture coordinates
  MAP1 TEXTURE COORD 3      3   s, t, r texture coordinates
  MAP1 TEXTURE COORD 4      4   s, t, r, q texture coordinates

Table 5.1: Values speci ed by the target to Map1. Values are given in the
order in which they are taken.

      void  Map1ffdg enum type, T u1, T u2 , int stride,
         int   order, T points ;

type is a symbolic constant indicating the range of the de ned polynomial.
Its possible values, along with the evaluations that each indicates, are given
in Table 5.1. order is equal to n + 1; The error INVALID VALUE is generated
if order is less than one or greater than MAX EVAL ORDER. points is a pointer
to a set of n + 1 blocks of storage. Each block begins with k single-precision
  oating-point or double-precision oating-point values, respectively. The
rest of the block may be lled with arbitrary data. Table 5.1 indicates how
k depends on type and what the k values represent in each case.
    stride is the number of single- or double-precision values as appropriate
in each block of storage. The error INVALID VALUE results if stride is less than
k. The order of the polynomial, order, is also the number of blocks of storage
containing control points.
    u1 and u2 give two oating-point values that de ne the endpoints of the
pre-image of the map. When a value u0 is presented for evaluation, the
formula used is
                                            0
                             p0u0  = p uu ,, uu1 :
                                            2     1
The error INVALID VALUE results if u1 = u2 .
   Map2 is analogous to Map1, except that it describes bivariate polyno-




                                 Version 1.2.1 - April 1, 1999
166                                             CHAPTER 5. SPECIAL FUNCTIONS


           Integers                     Reals
                                                                              Vertices
                      k                     [u1,u2]                           Normals
                                                                      ΣBiRi
      EvalMesh                                                [0,1]
                                                       Ax+b                   Texture Coordinates
      EvalPoint       l                     [v1,v2]
                                                              [0,1]
                                                                              Colors


                          MapGrid                               Map
                                      EvalCoord



   Figure 5.1. Map Evaluation.


mials of the form
                                        X
                                        n X
                                          m
                           pu; v =                  BinuBjmvRij :
                                        i=0 j =0
The form of the Map2 command is
      void    Map2ffdg enum target, T u1 , T u2, int ustride,
         int      uorder, T v1 , T v2 , int vstride, int vorder, T points ;
target is a range type selected from the same group as is used for Map1,
except that the string MAP1 is replaced with MAP2. points is a pointer to
n + 1m + 1 blocks of storage uorder = n + 1 and vorder = m + 1; the
error INVALID VALUE is generated if either uorder or vorder is less than one
or greater than MAX EVAL ORDER. The values comprising Rij are located
                                    ustridei + vstridej
values either single- or double-precision oating-point, as appropriate past
the rst value pointed to by points. u1 , u2 , v1 , and v2 de ne the pre-image
rectangle of the map; a domain point u0 ; v0  is evaluated as
                                                0           0
                            p0u0 ; v0  = p uu ,, uu1 ; vv ,, vv1 :
                                                2     1 2 1
   The evaluation of a de ned map is enabled or disabled with Enable and
Disable using the constant corresponding to the map as described above.
The error INVALID VALUE results if either ustride or vstride is less than k, or
if u1 is equal to u2 , or if v1 is equal to v2 .
    Figure 5.1 describes map evaluation schematically; an evaluation of en-
abled maps is e ected in one of two ways. The rst way is to use




                          Version 1.2.1 - April 1, 1999
5.1. EVALUATORS                                                          167

     voidEvalCoordf12gffdg T arg ;
     voidEvalCoordf12gffdgv T arg ;
EvalCoord1 causes evaluation of the enabled one-dimensional maps. The
argument is the value or a pointer to the value that is the domain coor-
dinate, u0 . EvalCoord2 causes evaluation of the enabled two-dimensional
maps. The two values specify the two domain coordinates, u0 and v0 , in that
order.
     When one of the EvalCoord commands is issued, all currently enabled
maps of the indicated dimension are evaluated. Then, for each enabled map,
it is as if a corresponding GL command were issued with the resulting co-
ordinates, with one important di erence. The di erence is that when an
evaluation is performed, the GL uses evaluated values instead of current
values for those evaluations that are enabled otherwise, the current values
are used. The order of the e ective commands is immaterial, except that
Vertex for vertex coordinate evaluation must be issued last. Use of eval-
uators has no e ect on the current color, normal, or texture coordinates. If
ColorMaterial is enabled, evaluated color values a ect the result of the
lighting equation as if the current color was being modi ed, but no change
is made to the tracking lighting parameters or to the current color.
     No command is e ectively issued if the corresponding map of the indi-
cated dimension is not enabled. If more than one evaluation is enabled for a
particular dimension e.g. MAP1 TEXTURE COORD 1 and MAP1 TEXTURE COORD 2,
then only the result of the evaluation of the map with the highest number
of coordinates is used.
     Finally, if either MAP2 VERTEX 3 or MAP2 VERTEX 4 is enabled, then the
normal to the surface is computed. Analytic computation, which sometimes
yields normals of length zero, is one method which may be used. If auto-
matic normal generation is enabled, then this computed normal is used as
the normal associated with a generated vertex. Automatic normal gener-
ation is controlled with Enable and Disable with symbolic the constant
AUTO NORMAL. If automatic normal generation is disabled, then a correspond-
ing normal map, if enabled, is used to produce a normal. If neither automatic
normal generation nor a normal map are enabled, then no normal is sent
with a vertex resulting from an evaluation the e ect is that the current
normal is used.
     For MAP VERTEX 3, let q = p. For MAP VERTEX 4, let q = x=w; y=w; z=w,
where x; y; z; w = p. Then let
                              m = @@uq  @@vq :




                               Version 1.2.1 - April 1, 1999
168                                     CHAPTER 5. SPECIAL FUNCTIONS

Then the generated analytic normal, n, is given by n = m=kmk.
    The second way to carry out evaluations is to use a set of commands
that provide for e cient speci cation of a series of evenly spaced values to
be mapped. This method proceeds in two steps. The rst step is to de ne
a grid in the domain. This is done using
      void    MapGrid1ffdg int n, T u01 , T u02 ;
for a one-dimensional map or
      void    MapGrid2ffdg int nu, T u01 , T u02, int nv , T v10 ,
         T   v20 ;
for a two-dimensional map. In the case of MapGrid1 u01 and u02 describe
an interval, while n describes the number of partitions of the interval. The
error INVALID VALUE results if n  0. For MapGrid2, u01 ; v10  speci es one
two-dimensional point and u02 ; v20  speci es another. nu gives the number of
partitions between u01 and u02 , and nv gives the number of partitions between
v10 and v20 . If either nu  0 or nv  0, then the error INVALID VALUE occurs.
     Once a grid is de ned, an evaluation on a rectangular subset of that grid
may be carried out by calling
      void    EvalMesh1 enum mode, int p1 , int p2 ;
mode is either POINT or LINE. The e ect is the same as performing the fol-
lowing code fragment, with u0 = u02 , u01 =n:
        Begintype;
           for i = p1 to p2 step 1:0
              EvalCoord1i * u0 + u01 ;
        End;
where EvalCoord1f or EvalCoord1d is substituted for EvalCoord1 as
appropriate. If mode is POINT, then type is POINTS; if mode is LINE, then type
is LINE STRIP. The one requirement is that if either i = 0 or i = n, then the
value computed from i  u0 + u01 is precisely u01 or u02 , respectively.
    The corresponding commands for two-dimensional maps are
      void    EvalMesh2 enum mode, int p1 , int p2, int q1,
         int   q2 ;




                       Version 1.2.1 - April 1, 1999
5.1. EVALUATORS                                                           169

mode must be FILL, LINE, or POINT. When mode is FILL, then these commands
are equivalent to the following, with u0 = u02 , u01 =n and v0 = v20 ,
v10 =m:
          for i = q1 to q2 , 1 step 1:0
              BeginQUAD STRIP;
                 for j = p1 to p2 step 1:0
                      EvalCoord2j * u0 + u01 , i * v0 + v10 ;
                      EvalCoord2j * u0 + u01 , i + 1 * v0 + v10 ;
              End;
If mode is LINE, then a call to EvalMesh2 is equivalent to
          for i = q1 to q2 step 1:0
              BeginLINE STRIP;
              for j = p1 to p2 step 1:0
                 EvalCoord2j * u0 + u01 , i * v0 + v10 ;
              End;;
          for i = p1 to p2 step 1:0
              BeginLINE STRIP;
              for j = q1 to q2 step 1:0
                 EvalCoord2i * u0 + u01 , j * v0 + v10 ;
              End;
If mode is POINT, then a call to EvalMesh2 is equivalent to
          BeginPOINTS;
              for i = q1 to q2 step 1:0
                 for j = p1 to p2 step 1:0
                      EvalCoord2j * u0 + u01 , i * v0 + v10 ;
          End;
Again, in all three cases, there is the requirement that 0  u0 + u01 = u01 ,
n  u0 + u01 = u02 , 0  v0 + v10 = v10 , and m  v0 + v10 = v20 .
   An evaluation of a single point on the grid may also be carried out:
     void   EvalPoint1 int p ;
Calling it is equivalent to the command
           EvalCoord1p * u0 + u01;
with u0 and u01 de ned as above.




                               Version 1.2.1 - April 1, 1999
170                                                CHAPTER 5. SPECIAL FUNCTIONS

      void   EvalPoint2 int p, int q ;
is equivalent to the command
          EvalCoord2p * u0         +   u01   ,   q   *   v0   +   v10 ;

    The state required for evaluators potentially consists of 9 one-
dimensional map speci cations and 9 two-dimensional map speci cations,
as well as corresponding ags for each speci cation indicating which are en-
abled. Each map speci cation consists of one or two orders, an appropriately
sized array of control points, and a set of two values for a one-dimensional
map or four values for a two-dimensional map to describe the domain.
The maximum possible order, for either u or v, is implementation dependent
one maximum applies to both u and v, but must be at least 8. Each con-
trol point consists of between one and four oating-point values depending
on the type of the map. Initially, all maps have order 1 making them con-
stant maps. All vertex coordinate maps produce the coordinates 0; 0; 0; 1
or the appropriate subset; all normal coordinate maps produce 0; 0; 1;
RGBA maps produce 1; 1; 1; 1; color index maps produce 1.0; texture co-
ordinate maps produce 0; 0; 0; 1; In the initial state, all maps are disabled.
A ag indicates whether or not automatic normal generation is enabled for
two-dimensional maps. In the initial state, automatic normal generation is
disabled. Also required are two oating-point values and an integer number
of grid divisions for the one-dimensional grid speci cation and four oating-
point values and two integer grid divisions for the two-dimensional grid
speci cation. In the initial state, the bounds of the domain interval for 1-D
is 0 and 1:0, respectively; for 2-D, they are 0; 0 and 1:0; 1:0, respectively.
The number of grid divisions is 1 for 1-D and 1 in both directions for 2-D. If
any evaluation command is issued when no vertex map is enabled, nothing
happens.

5.2 Selection
Selection is used by a programmer to determine which primitives are drawn
into some region of a window. The region is de ned by the current model-
view and perspective matrices.
    Selection works by returning an array of integer-valued names. This
array represents the current contents of the name stack. This stack is con-
trolled with the commands




                     Version 1.2.1 - April 1, 1999
5.2. SELECTION                                                             171

     void   InitNames void ;
     void   PopName void ;
     void   PushName uint name ;
     void   LoadName uint name ;
InitNames empties clears the name stack. PopName pops one name
o the top of the name stack. PushName causes name to be pushed
onto the name stack. LoadName replaces the value on the top of the
stack with name. Loading a name onto an empty stack generates the er-
ror INVALID OPERATION. Popping a name o of an empty stack generates
STACK UNDERFLOW; pushing a name onto a full stack generates STACK OVERFLOW.
The maximum allowable depth of the name stack is implementation depen-
dent but must be at least 64.
    In selection mode, no fragments are rendered into the framebu er. The
GL is placed in selection mode with
     int    RenderMode enum mode ;
mode is a symbolic constant: one of RENDER, SELECT, or FEEDBACK. RENDER
is the default, corresponding to rendering as described until now. SELECT
speci es selection mode, and FEEDBACK speci es feedback mode described
below. Use of any of the name stack manipulation commands while the GL
is not in selection mode has no e ect.
    Selection is controlled using
     void   SelectBu er sizei n, uint *bu er ;
bu er is a pointer to an array of unsigned integers called the selection
array to be potentially lled with names, and n is an integer indicating the
maximum number of values that can be stored in that array. Placing the GL
in selection mode before SelectBu er has been called results in an error of
INVALID OPERATION as does calling SelectBu er while in selection mode.
    In selection mode, if a point, line, polygon, or the valid coordinates pro-
duced by a RasterPos command intersects the clip volume section 2.11
then this primitive or RasterPos command causes a selection hit. In the
case of polygons, no hit occurs if the polygon would have been culled, but
selection is based on the polygon itself, regardless of the setting of Poly-
gonMode. When in selection mode, whenever a name stack manipulation
command is executed or RenderMode is called and there has been a hit
since the last time the stack was manipulated or RenderMode was called,
then a hit record is written into the selection array.




                                Version 1.2.1 - April 1, 1999
172                                  CHAPTER 5. SPECIAL FUNCTIONS

    A hit record consists of the following items in order: a non-negative
integer giving the number of elements on the name stack at the time of the
hit, a minimum depth value, a maximum depth value, and the name stack
with the bottommost element rst. The minimum and maximum depth
values are the minimum and maximum taken over all the window coordinate
z values of each post-clipping vertex of each primitive that intersects the
clipping volume since the last hit record was written. The minimum and
maximum each of which lies in the range 0; 1  are each multiplied by
232 , 1 and rounded to the nearest unsigned integer to obtain the values
that are placed in the hit record. No depth o set arithmetic section 3.5.5
is performed on these values.
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
returns ,1 and clears the over ow ag. The name stack is cleared and the
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




                    Version 1.2.1 - April 1, 1999
5.3. FEEDBACK                                                             173

5.3 Feedback
Feedback, like selection, is a GL mode. The mode is selected by calling
RenderMode with FEEDBACK. When the GL is in feedback mode, no frag-
ments are written to the framebu er. Instead, information about primitives
that would have been rasterized is fed back to the application using the GL.
   Feedback is controlled using
     void   FeedbackBu er sizei n, enum type, float *bu er ;
bu er is a pointer to an array of oating-point values into which feedback in-
formation will be placed, and n is a number indicating the maximum number
of values that can be written to that array. type is a symbolic constant de-
scribing the information to be fed back for each vertex see Figure 5.2. The
error INVALID OPERATION results if the GL is placed in feedback mode before
a call to FeedbackBu er has been made, or if a call to FeedbackBu er
is made while in feedback mode.
    While in feedback mode, each primitive that would be rasterized or
bitmap or call to DrawPixels or CopyPixels, if the raster position is
valid generates a block of values that get copied into the feedback array.
If doing so would cause the number of entries to exceed the maximum, the
block is partially written so as to ll the array if there is any room left at
all. The rst block of values generated after the GL enters feedback mode
is placed at the beginning of the feedback array, with subsequent blocks
following. Each block begins with a code indicating the primitive type, fol-
lowed by values that describe the primitive's vertices and associated data.
Entries are also written for bitmaps and pixel rectangles. Feedback occurs
after polygon culling section 3.5.1 and PolygonMode interpretation of
polygons section 3.5.4 has taken place. It may also occur after polygons
with more than three edges are broken up into triangles if the GL imple-
mentation renders polygons by performing this decomposition. x, y, and z
coordinates returned by feedback are window coordinates; if w is returned,
it is in clip coordinates. No depth o set arithmetic section 3.5.5 is per-
formed on the z values. In the case of bitmaps and pixel rectangles, the
coordinates returned are those of the current raster position.
     The texture coordinates and colors returned are these resulting from the
clipping operations described in Section 2.13.8. The colors returned are
the primary colors.
     The ordering rules for GL command interpretation also apply in feedback
mode. Each command must be fully interpreted and its e ects on both GL




                               Version 1.2.1 - April 1, 1999
174                                       CHAPTER 5. SPECIAL FUNCTIONS

               Type            coordinates      color texture total values
                2D             x, y                           2
                3D             x, y, z                        3
              3D COLOR         x, y, z          k             3+k
        3D COLOR TEXTURE       x, y, z          k     4       7+k
        4D COLOR TEXTURE       x, y, z , w      k     4       8+k

Table 5.2: Correspondence of feedback type to number of values per vertex.
k is 1 in color index mode and 4 in RGBA mode.
state and the values to be written to the feedback bu er completed before
a subsequent command may be executed.
    The GL is taken out of feedback mode by calling RenderMode with an
argument value other than FEEDBACK. When called while in feedback mode,
RenderMode returns the number of values placed in the feedback array
and resets the feedback array pointer to be bu er. The return value never
exceeds the maximum number of values passed to FeedbackBu er.
    If writing a value to the feedback bu er would cause more values to be
written than the speci ed maximum number of values, then the value is not
written and an over ow ag is set. In this case, RenderMode returns ,1
when it is called, after which the over ow ag is reset. While in feedback
mode, values are not guaranteed to be written into the feedback bu er before
RenderMode is called.
    Figure 5.2 gives a grammar for the array produced by feedback. Each
primitive is indicated with a unique identifying value followed by some num-
ber of vertices. A vertex is fed back as some number of oating-point values
determined by the feedback type. Table 5.2 gives the correspondence be-
tween feedback bu er and the number of values returned for each vertex.
      The command
       void    PassThrough float token ;
may be used as a marker in feedback mode. token is returned as if it were a
primitive; it is indicated with its own unique identifying value. The ordering
of any PassThrough commands with respect to primitive speci cation is
maintained by feedback. PassThrough may not occur between Begin and
End. It has no e ect when the GL is not in feedback mode.
    The state required for feedback is the pointer to the feedback array, the
maximum number of values that may be placed there, and the feedback type.




                         Version 1.2.1 - April 1, 1999
5.4. DISPLAY LISTS                                                         175

An over ow ag is required to indicate whether the maximum allowable
number of feedback values has been written; initially this ag is cleared.
These state variables are GL client state. Feedback also relies on the same
mode ag as selection to indicate whether the GL is in feedback, selection,
or normal rendering mode.

5.4 Display Lists
A display list is simply a group of GL commands and arguments that has
been stored for subsequent execution. The GL may be instructed to process
a particular display list possibly repeatedly by providing a number that
uniquely speci es it. Doing so causes the commands within the list to be
executed just as if they were given normally. The only exception pertains
to commands that rely upon client state. When such a command is accu-
mulated into the display list that is, when issued, not when executed, the
client state in e ect at that time applies to the command. Only server state
is a ected when the command is executed. As always, pointers which are
passed as arguments to commands are dereferenced when the command is
issued. Vertex array pointers are dereferenced when the commands Ar-
rayElement, DrawArrays, or DrawElements are accumulated into a
display list.
    A display list is begun by calling
     void   NewList uint n, enum mode ;
n is a positive integer to which the display list that follows is assigned, and
mode is a symbolic constant that controls the behavior of the GL during
display list creation. If mode is COMPILE, then commands are not executed
as they are placed in the display list. If mode is COMPILE AND EXECUTE then
commands are executed as they are encountered, then placed in the display
list. If n = 0, then the error INVALID VALUE is generated.
     After calling NewList all subsequent GL commands are placed in the
display list in the order the commands are issued until a call to
     void   EndList void ;
occurs, after which the GL returns to its normal command execution state.
It is only when EndList occurs that the speci ed display list is actually asso-
ciated with the index indicated with NewList. The error INVALID OPERATION
is generated if EndList is called without a previous matching NewList,




                                Version 1.2.1 - April 1, 1999
176                                     CHAPTER 5. SPECIAL FUNCTIONS



feedback-list:
      feedback-item feedback-list               pixel-rectangle:
      feedback-item                                                    vertex
                                                          DRAW PIXEL TOKEN
                                                      COPY PIXEL TOKEN vertex
feedback-item:                                  passthrough:
      point                                               PASS THROUGH TOKEN   f
      line-segment
      polygon                                   vertex:
      bitmap                                    2D:
      pixel-rectangle                                     ff
      passthrough                               3D   :
                                                          fff
point:                                          3D COLOR   :
         POINT TOKEN   vertex                             f f f color
line-segment:                                   3D COLOR TEXTURE    :
                  vertex vertex
         LINE TOKEN                                       f f f color tex
      LINE RESET TOKEN vertex vertex            4D COLOR TEXTURE    :
polygon:                                                  f f f f color tex
      POLYGON TOKEN n polygon-spec
polygon-spec:                                   color:
      polygon-spec vertex                                 ffff
      vertex vertex vertex                                f
bitmap:
      BITMAP TOKEN vertex                       tex:
                                                          ffff

Figure 5.2: Feedback syntax. f is a oating-point number. n is a oating-
point integer giving the number of vertices in a polygon. The symbols
ending with TOKEN are symbolic oating-point constants. The labels under
the vertex" rule show the di erent data returned for vertices depending
on the feedback type. LINE TOKEN and LINE RESET TOKEN are identical except
that the latter is returned only when the line stipple is reset for that line
segment.




                       Version 1.2.1 - April 1, 1999
5.4. DISPLAY LISTS                                                          177

or if NewList is called a second time before calling EndList. The error
OUT OF MEMORY is generated if EndList is called and the speci ed display list
cannot be stored because insu cient memory is available. In this case GL
implementations of revision 1.1 or greater insure that no change is made to
the previous contents of the display list, if any, and that no other change
is made to the GL state, except for the state changed by execution of GL
commands when the display list mode is COMPILE AND EXECUTE.
    Once de ned, a display list is executed by calling
      void   CallList uint n ;
n gives the index of the display list to be called. This causes the commands
saved in the display list to be executed, in order, just as if they were issued
without using a display list. If n = 0, then the error INVALID VALUE is
generated.
    The command
      void   CallLists sizei n, enum type, void *lists ;
provides an e cient means for executing a number of display lists. n is
an integer indicating the number of display lists to be called, and lists is
a pointer that points to an array of o sets. Each o set is constructed as
determined by lists as follows. First, type may be one of the constants BYTE,
UNSIGNED BYTE, SHORT, UNSIGNED SHORT, INT, UNSIGNED INT, or FLOAT indicating
that the array pointed to by lists is an array of bytes, unsigned bytes, shorts,
unsigned shorts, integers, unsigned integers, or oats, respectively. In this
case each o set is found by simply converting each array element to an
integer  oating point values are truncated. Further, type may be one of
2 BYTES, 3 BYTES, or 4 BYTES, indicating that the array contains sequences of
2, 3, or 4 unsigned bytes, in which case each integer o set is constructed
according to the following algorithm:
offset  0
for i = 1 to b
     offset  offset shifted left 8 bits
     offset  offset + byte
     advance to next byte in the array
b is 2, 3, or 4, as indicated by type. If n = 0, CallLists does nothing.
     Each of the n constructed o sets is taken in order and added to a display
list base to obtain a display list number. For each number, the indicated
display list is executed. The base is set by calling




                                Version 1.2.1 - April 1, 1999
178                                   CHAPTER 5. SPECIAL FUNCTIONS

      void   ListBase uint base ;
to specify the o set.
     Indicating a display list index that does not correspond to any display
list has no e ect. CallList or CallLists may appear inside a display list. If
the mode supplied to NewList is COMPILE AND EXECUTE, then the appropriate
lists are executed, but the CallList or CallLists, rather than those lists'
constituent commands, is placed in the list under construction. To avoid
the possibility of in nite recursion resulting from display lists calling one
another, an implementation dependent limit is placed on the nesting level
of display lists during display list execution. This limit must be at least 64.
     Two commands are provided to manage display list indices.
      uint   GenLists sizei s ;
returns an integer n such that the indices n; : : : ; n + s , 1 are previously
unused i.e. there are s previously unused display list indices starting at n.
GenLists also has the e ect of creating an empty display list for each of
the indices n; : : : ; n + s , 1, so that these indices all become used. GenLists
returns 0 if there is no group of s contiguous previously unused display list
indices, or if s = 0.
      boolean   IsList uint list ;
returns TRUE if list is the index of some display list.
    A contiguous group of display lists may be deleted by calling
      void   DeleteLists uint list, sizei range ;
where list is the index of the rst display list to be deleted and range is
the number of display lists to be deleted. All information about the display
lists is lost, and the indices become unused. Indices to which no display list
corresponds are ignored. If range = 0, nothing happens.
     Certain commands, when called while compiling a display list, are not
compiled into the display list but are executed immediately. These are:
IsList, GenLists, DeleteLists, FeedbackBu er, SelectBu er, Ren-
derMode, VertexPointer, NormalPointer, ColorPointer, Index-
Pointer, TexCoordPointer, EdgeFlagPointer, InterleavedArrays,
EnableClientState, DisableClientState, PushClientAttrib, Pop-
ClientAttrib, ReadPixels, PixelStore, GenTextures, DeleteTex-
tures, AreTexturesResident, IsTexture, Flush, Finish, as well as
IsEnabled and all of the Get commands see Chapter 6.




                     Version 1.2.1 - April 1, 1999
5.5. FLUSH AND FINISH                                                        179

   TexImage3D, TexImage2D, TexImage1D, Histogram,
and   ColorTable are executed immediately when called
with    the     corresponding proxy arguments                 PROXY TEXTURE 3D,
PROXY TEXTURE 2D,          PROXY TEXTURE 1D,         PROXY HISTOGRAM,        and
PROXY COLOR TABLE,            PROXY POST CONVOLUTION COLOR TABLE,              or
PROXY POST COLOR MATRIX COLOR TABLE.
     Display lists require one bit of state to indicate whether a GL command
should be executed immediately or placed in a display list. In the initial
state, commands are executed immediately. If the bit indicates display
list creation, an index is required to indicate the current display list being
de ned. Another bit indicates, during display list creation, whether or not
commands should be executed as they are compiled into the display list.
One integer is required for the current ListBase setting; its initial value
is zero. Finally, state must be maintained to indicate which integers are
currently in use as display list indices. In the initial state, no indices are in
use.

5.5 Flush and Finish
The command
       void   Flush void ;
indicates that all commands that have previously been sent to the GL must
complete in nite time.
    The command
       void   Finish void ;
forces all previous GL commands to complete. Finish does not return until
all e ects from previously issued commands on GL client and server state
and the framebu er are fully realized.

5.6 Hints
Certain aspects of GL behavior, when there is room for variation, may be
controlled with hints. A hint is speci ed using
       void   Hint enum target, enum hint ;




                                 Version 1.2.1 - April 1, 1999
180                                  CHAPTER 5. SPECIAL FUNCTIONS

target is a symbolic constant indicating the behavior to be controlled, and
hint is a symbolic constant indicating what type of behavior is desired.
target may be one of PERSPECTIVE CORRECTION HINT, indicating the desired
quality of parameter interpolation; POINT SMOOTH HINT, indicating the desired
sampling quality of points; LINE SMOOTH HINT, indicating the desired sampling
quality of lines; POLYGON SMOOTH HINT, indicating the desired sampling quality
of polygons; and FOG HINT, indicating whether fog calculations are done per
pixel or per vertex. hint must be one of FASTEST, indicating that the most
e cient option should be chosen; NICEST, indicating that the highest quality
option should be chosen; and DONT CARE, indicating no preference in the
matter.
    The interpretation of hints is implementation dependent. An implemen-
tation may ignore them entirely.
    The initial value of all hints is DONT CARE.




                    Version 1.2.1 - April 1, 1999
Chapter 6
State and State Requests
The state required to describe the GL machine is enumerated in section 6.2.
Most state is set through the calls described in previous chapters, and can
be queried using the calls described in section 6.1.

6.1 Querying GL State
6.1.1 Simple Queries
Much of the GL state is completely identi ed by symbolic constants. The
values of these state variables can be obtained using a set of Get commands.
There are four commands for obtaining simple state variables:
     void   GetBooleanv enum value, boolean *data ;
     void   GetIntegerv enum value, int *data ;
     void   GetFloatv enum value, float *data ;
     void   GetDoublev enum value, double *data ;
The commands obtain boolean, integer, oating-point, or double-precision
state variables. value is a symbolic constant indicating the state variable to
return. data is a pointer to a scalar or array of the indicated type in which
to place the returned data. In addition
     boolean    IsEnabled enum value ;
can be used to determine if value is currently enabled as with Enable or
disabled.
                                     181



                               Version 1.2.1 - April 1, 1999
182                                CHAPTER 6. STATE AND STATE REQUESTS

6.1.2 Data Conversions
If a Get command is issued that returns value types di erent from the
type of the value being obtained, a type conversion is performed. If Get-
Booleanv is called, a oating-point or integer value converts to FALSE if
and only if it is zero otherwise it converts to TRUE. If GetIntegerv or
any of the Get commands below is called, a boolean value is interpreted
as either 1 or 0, and a oating-point value is rounded to the nearest integer,
unless the value is an RGBA color component, a DepthRange value, a
depth bu er clear value, or a normal coordinate. In these cases, the Get
command converts the oating-point value to an integer according the INT
entry of Table 4.7; a value not in ,1; 1 converts to an unde ned value.
If GetFloatv is called, a boolean value is interpreted as either 1:0 or 0:0,
an integer is coerced to oating-point, and a double-precision oating-point
value is converted to single-precision. Analogous conversions are carried
out in the case of GetDoublev. If a value is so large in magnitude that
it cannot be represented with the requested type, then the nearest value
representable using the requested type is returned.
    Unless otherwise indicated, multi-valued state variables return their mul-
tiple values in the same order as they are given as arguments to the com-
mands that set them. For instance, the two DepthRange parameters are
returned in the order n followed by f. Similarly, points for evaluator maps
are returned in the order that they appeared when passed to Map1. Map2
returns Rij in the uorderi + j th block of values see page 166 for i, j ,
uorder, and Rij .
6.1.3 Enumerated Queries
Other commands exist to obtain state variables that are identi ed by a
category clip plane, light, material, etc. as well as a symbolic constant.
These are
      void  GetClipPlane enum plane, double eqn 4 ;
      void  GetLightfifgv enum light, enum value, T data ;
      void  GetMaterialfifgv enum face, enum value, T data ;
      void  GetTexEnvfifgv enum env, enum value, T data ;
      void  GetTexGenfifgv enum coord, enum value, T data ;
      void  GetTexParameterfifgv enum target, enum value,
         T data ;
      void  GetTexLevelParameterfifgv enum target, int lod,
         enum value, T   data ;




                    Version 1.2.1 - April 1, 1999
6.1. QUERYING GL STATE                                                   183

     void   GetPixelMapfui us fgv enum map, T data ;
     void   GetMapfifdgv enum map, enum value, T data ;
GetClipPlane always returns four double-precision values in eqn; these
are the coe cients of the plane equation of plane in eye coordinates these
coordinates are those that were computed when the plane was speci ed.
    GetLight places information about value a symbolic constant for light
also a symbolic constant in data. POSITION or SPOT DIRECTION returns val-
ues in eye coordinates again, these are the coordinates that were computed
when the position or direction was speci ed.
    GetMaterial, GetTexGen, GetTexEnv, and GetTexParameter
are similar to GetLight, placing information about value for the target indi-
cated by their rst argument into data. The face argument to GetMaterial
must be either FRONT or BACK, indicating the front or back material, respec-
tively. The env argument to GetTexEnv must currently be TEXTURE ENV.
The coord argument to GetTexGen must be one of S, T, R, or Q. For Get-
TexGen, EYE LINEAR coe cients are returned in the eye coordinates that
were computed when the plane was speci ed; OBJECT LINEAR coe cients are
returned in object coordinates.
    GetTexParameter and GetTexLevelParameter parameter target
may be one of TEXTURE 1D, TEXTURE 2D, or TEXTURE 3D, indicating the
currently bound one-, two-, or three-dimensional texture object. For
GetTexLevelParameter, target may also be one of PROXY TEXTURE 1D,
PROXY TEXTURE 2D, or PROXY TEXTURE 3D, indicating the one-, two-, or three-
dimensional proxy state vector. value is a symbolic value indicat-
ing which texture parameter is to be obtained. The lod argument to
GetTexLevelParameter determines which level-of-detail's state is re-
turned. If the lod argument is less than zero or if it is larger than
the maximum allowable level-of-detail then the error INVALID VALUE oc-
curs. Queries of TEXTURE RED SIZE, TEXTURE GREEN SIZE, TEXTURE BLUE SIZE,
TEXTURE ALPHA SIZE, TEXTURE LUMINANCE SIZE, and TEXTURE INTENSITY SIZE
return the actual resolutions of the stored image array components, not
the resolutions speci ed when the image array was de ned. Queries of
TEXTURE WIDTH, TEXTURE HEIGHT, TEXTURE DEPTH, and TEXTURE BORDER return
the width, height, depth, and border as speci ed when the image ar-
ray was created. The internal format of the image array is queried as
TEXTURE INTERNAL FORMAT, or as TEXTURE COMPONENTS for compatibility with
GL version 1.0.
    For GetPixelMap, the map must be a map name from Table 3.3. For
GetMap, map must be one of the map types described in section 5.1, and




                               Version 1.2.1 - April 1, 1999
184                                 CHAPTER 6. STATE AND STATE REQUESTS

value must be one of ORDER, COEFF, or DOMAIN.
6.1.4 Texture Queries
The command
      void   GetTexImage enum tex, int lod, enum format,
         enum    type, void *img ;
is used to obtain texture images. It is somewhat di erent from the other get
commands; tex is a symbolic value indicating which texture is to be obtained.
TEXTURE 1D indicates a one-dimensional texture, TEXTURE 2D indicates a two-
dimensional texture, and TEXTURE 3D indicates a three-dimensional texture.
lod is a level-of-detail number, format is a pixel format from Table 3.6, type
is a pixel type from Table 3.5, and img is a pointer to a block of memory.
    GetTexImage obtains component groups from a texture image with
the indicated level-of-detail. The components are assigned among R, G, B,
and A according to Table 6.1, starting with the rst group in the rst row,
and continuing by obtaining groups in order from each row and proceeding
from the rst row to the last, and from the rst image to the last for three-
dimensional textures. These groups are then packed and placed in client
memory. No pixel transfer operations are performed on this image, but
pixel storage modes that are applicable to ReadPixels are applied.
    For three-dimensional textures, pixel storage operations are applied as
if the image were two-dimensional, except that the additional pixel storage
state values PACK IMAGE HEIGHT and PACK SKIP IMAGES are applied. The cor-
respondence of texels to memory locations is as de ned for TexImage3D
in section 3.8.1.
    The row length, number of rows, image depth, and number of images
are determined by the size of the texture image including any borders.
Calling GetTexImage with lod less than zero or larger than the maxi-
mum allowable causes the error INVALID VALUE . Calling GetTexImage with
format of COLOR INDEX, STENCIL INDEX, or DEPTH COMPONENT causes the error
INVALID ENUM.
    The command
       boolean IsTexture uint texture ;

returns TRUE if texture is the name of a texture object. If texture is zero, or is
a non-zero value that is not the name of a texture object, or if an error condi-
tion occurs, IsTexture returns FALSE. A name returned by GenTextures,
but not yet bound, is not the name of a texture object.




                      Version 1.2.1 - April 1, 1999
6.1. QUERYING GL STATE                                                        185

                  Base Internal Format        R
                                           G B A
                         ALPHA             0 0 Ai
                                              0
                    LUMINANCE or 1    Li 0 0 1
                 LUMINANCE ALPHA or 2 Li 0 0 Ai
                       INTENSITY        Ii 0 0 1
                       RGB or 3       Ri Gi Bi 1
                      RGBA or 4       Ri Gi Bi Ai

Table 6.1: Texture, table, and lter return values. Ri , Gi , Bi , Ai , Li , and Ii
are components of the internal format that are assigned to pixel values R,
G, B, and A. If a requested pixel value is not present in the internal format,
the speci ed constant value is used.

6.1.5 Stipple Query
The command
      void   GetPolygonStipple void *pattern ;
obtains the polygon stipple. The pattern is packed into memory according
to the procedure given in section 4.3.2 for ReadPixels; it is as if the height
and width passed to that command were both equal to 32, the type were
BITMAP, and the format were COLOR INDEX.


6.1.6 Color Matrix Query
The scale and bias variables are queried using GetFloatv with pname set to
the appropriate variable name. The top matrix on the color matrix stack is
returned by GetFloatv called with pname set to COLOR MATRIX. The depth
of the color matrix stack, and the maximum depth of the color matrix stack,
are queried with GetIntegerv, setting pname to COLOR MATRIX STACK DEPTH
and MAX COLOR MATRIX STACK DEPTH respectively.

6.1.7 Color Table Query
The current contents of a color table are queried using
      void   GetColorTable enum target, enum format, enum type,
         void   *table ;




                                 Version 1.2.1 - April 1, 1999
186                       CHAPTER 6. STATE AND STATE REQUESTS

target must be one of the regular color table names listed in table 3.4. format
and type accept the same values as do the corresponding parameters of
GetTexImage. The one-dimensional color table image is returned to client
memory starting at table. No pixel transfer operations are performed on
this image, but pixel storage modes that are applicable to ReadPixels are
performed. Color components that are requested in the speci ed format,
but which are not included in the internal format of the color lookup table,
are returned as zero. The assignments of internal color components to the
components requested by format are described in Table 6.1.
    The functions
      void  GetColorTableParameterfifgv enum target,
         enum   pname, T params ;
are used for integer and oating point query.
    target must be one of the regular or proxy color table names listed
in table 3.4. pname is one of COLOR TABLE SCALE, COLOR TABLE BIAS,
COLOR TABLE FORMAT,        COLOR TABLE WIDTH,      COLOR TABLE RED SIZE,
COLOR TABLE GREEN SIZE, COLOR TABLE BLUE SIZE, COLOR TABLE ALPHA SIZE,
COLOR TABLE LUMINANCE SIZE, or COLOR TABLE INTENSITY SIZE. The value of
the speci ed parameter is returned in params.

6.1.8 Convolution Query
The current contents of a convolution lter image are queried with the com-
mand
      void  GetConvolutionFilter enum target, enum format,
         enum   type, void *image ;
target must be CONVOLUTION 1D or CONVOLUTION 2D. format and type accept the
same values as do the corresponding parameters of GetTexImage. The
one-dimensional or two-dimensional images is returned to client memory
starting at image. Pixel processing and component mapping are identical
to those of GetTexImage.
    The current contents of a separable lter image are queried using
      void  GetSeparableFilter enum target, enum format,
         enum   type, void *row, void *column, void *span ;




                     Version 1.2.1 - April 1, 1999
6.1. QUERYING GL STATE                                                     187

target must be SEPARABLE 2D. format and type accept the same values as
do the corresponding parameters of GetTexImage. The row and column
images are returned to client memory starting at row and column respec-
tively. span is currently unused. Pixel processing and component mapping
are identical to those of GetTexImage.
    The functions
     void   GetConvolutionParameterfifgv enum target,
        enum   pname, T params ;
are used for integer and oating point query.                 target must
be CONVOLUTION 1D, CONVOLUTION 2D, or SEPARABLE 2D. pname
is one of CONVOLUTION BORDER COLOR, CONVOLUTION BORDER MODE,
CONVOLUTION FILTER SCALE, CONVOLUTION FILTER BIAS, CONVOLUTION FORMAT,
CONVOLUTION WIDTH,   CONVOLUTION HEIGHT,      MAX CONVOLUTION WIDTH,    or
MAX CONVOLUTION HEIGHT. The value of the speci ed parameter is returned in
params.
6.1.9 Histogram Query
The current contents of the histogram table are queried using
     void   GetHistogram enum target, boolean reset,
        enum   format, enum type, void* values ;
target must be HISTOGRAM. type and format accept the same values as do
the corresponding parameters of GetTexImage. The one-dimensional his-
togram table image is returned to values. Pixel processing and component
mapping are identical to those of GetTexImage.
    If reset is TRUE, then all counters of all elements of the histogram are
reset to zero. Counters are reset whether returned or not.
    No counters are modi ed if reset is FALSE.
    Calling
     void   ResetHistogram enum target ;
resets all counters of all elements of the histogram table to zero. target must
be HISTOGRAM.
    It is not an error to reset or query the contents of a histogram table with
zero entries.
    The functions




                                Version 1.2.1 - April 1, 1999
188                       CHAPTER 6. STATE AND STATE REQUESTS

      void   GetHistogramParameterfifgv enum target,
         enum   pname, T params ;
are used for integer and oating point query. target must be HISTOGRAM or
PROXY HISTOGRAM. pname is one of HISTOGRAM FORMAT, HISTOGRAM WIDTH,
HISTOGRAM RED SIZE,       HISTOGRAM GREEN SIZE,     HISTOGRAM BLUE SIZE,
HISTOGRAM ALPHA SIZE, or HISTOGRAM LUMINANCE SIZE. pname may be
HISTOGRAM SINK only for target HISTOGRAM. The value of the speci ed
parameter is returned in params.

6.1.10 Minmax Query
The current contents of the minmax table are queried using
      void   GetMinmax enum target, boolean reset,
         enum   format, enum type, void* values ;
target must be MINMAX. type and format accept the same values as do the
corresponding parameters of GetTexImage. A one-dimensional image of
width 2 is returned to values. Pixel processing and component mapping are
identical to those of GetTexImage.
    If reset is TRUE, then each minimum value is reset to the maximum rep-
resentable value, and each maximum value is reset to the minimum repre-
sentable value. All values are reset, whether returned or not.
    No values are modi ed if reset is FALSE.
    Calling
      void   ResetMinmax enum target ;
resets all minimum and maximum values of target to to their maximum and
minimum representable values, respectively, target must be MINMAX.
    The functions
      void   GetMinmaxParameterfifgv enum target,
         enum   pname, T params ;
are used for integer and oating point query. target must be MINMAX. pname
is MINMAX FORMAT or MINMAX SINK. The value of the speci ed parameter is
returned in params.




                     Version 1.2.1 - April 1, 1999
6.1. QUERYING GL STATE                                                    189

6.1.11 Pointer and String Queries
The command
     void    GetPointerv enum pname, void **params ;
   obtains the pointer or pointers named pname in the array
params. The possible values for pname are SELECTION BUFFER POINTER,
FEEDBACK BUFFER POINTER,   VERTEX ARRAY POINTER,    NORMAL ARRAY POINTER,
COLOR ARRAY POINTER, INDEX ARRAY POINTER, TEXTURE COORD ARRAY POINTER,
and EDGE FLAG ARRAY POINTER. Each returns a single pointer value.
   Finally,
     ubyte    *GetString enum name ;
returns a pointer to a static string describing some aspect of the current
GL connection. The possible values for name are VENDOR, RENDERER, VERSION,
and EXTENSIONS. The format of the RENDERER and VERSION strings is imple-
mentation dependent. The EXTENSIONS string contains a space separated list
of extension names The extension names themselves do not contain any
spaces; the VERSION string is laid out as follows:
       version number      space    vendor-speci c information
The version number is either of the form major number.minor number or
major number.minor number.release number, where the numbers all have
one or more digits. The vendor speci c information is optional. However, if
it is present then it pertains to the server and the format and contents are
implementation dependent.
     GetString returns the version number returned in the VERSION string
and the extension names returned in the EXTENSIONS string that can be
supported on the connection. Thus, if the client and server support di erent
versions and or extensions, a compatible version and list of extensions is
returned.
6.1.12 Saving and Restoring State
Besides providing a means to obtain the values of state variables, the GL also
provides a means to save and restore groups of state variables. The PushAt-
trib, PushClientAttrib, PopAttrib and PopClientAttrib commands
are used for this purpose. The commands




                               Version 1.2.1 - April 1, 1999
190                       CHAPTER 6. STATE AND STATE REQUESTS

      void   PushAttrib bitfield mask ;
      void   PushClientAttrib bitfield mask ;
take a bitwise OR of symbolic constants indicating which groups of state
variables to push onto an attribute stack. PushAttrib uses a server at-
tribute stack while PushClientAttrib uses a client attribute stack. Each
constant refers to a group of state variables. The classi cation of each vari-
able into a group is indicated in the following tables of state variables. The
error STACK OVERFLOW is generated if PushAttrib or PushClientAttrib is
executed while the corresponding stack depth is MAX ATTRIB STACK DEPTH or
MAX CLIENT ATTRIB STACK DEPTH respectively. The commands


      void   PopAttrib void ;
      void   PopClientAttrib void ;
reset the values of those state variables that were saved with the last cor-
responding PushAttrib or PopClientAttrib. Those not saved remain
unchanged. The error STACK UNDERFLOW is generated if PopAttrib or Pop-
ClientAttrib is executed while the respective stack is empty.
    Table 6.2 shows the attribute groups with their corresponding symbolic
constant names and stacks.
    When PushAttrib is called with TEXTURE BIT set, the priorities, border
colors, lter modes, and wrap modes of the currently bound texture objects,
as well as the current texture bindings and enables, are pushed onto the
attribute stack. Unbound texture objects are not pushed or restored.
When an attribute set that includes texture information is popped, the
bindings and enables are rst restored to their pushed values, then the bound
texture objects' priorities, border colors, lter modes, and wrap modes are
restored to their pushed values.
    The depth of each attribute stack is implementation dependent but must
be at least 16. The state required for each attribute stack is potentially 16
copies of each state variable, 16 masks indicating which groups of variables
are stored in each stack entry, and an attribute stack pointer. In the initial
state, both attribute stacks are empty.
    In the tables that follow, a type is indicated for each variable. Table 6.3
explains these types. The type actually identi es all state associated with
the indicated description; in certain cases only a portion of this state is
returned. This is the case with all matrices, where only the top entry on
the stack is returned; with clip planes, where only the selected clip plane is
returned, with parameters describing lights, where only the value pertaining




                     Version 1.2.1 - April 1, 1999
6.1. QUERYING GL STATE                                    191




        Stack     Attribute             Constant
        server accum-bu er         ACCUM BUFFER BIT
        server color-bu er         COLOR BUFFER BIT
        server     current            CURRENT BIT
        server depth-bu er         DEPTH BUFFER BIT
        server      enable             ENABLE BIT
        server        eval               EVAL BIT
        server        fog                 FOG BIT
        server        hint               HINT BIT
        server     lighting           LIGHTING BIT
        server        line               LINE BIT
        server        list               LIST BIT
        server       pixel           PIXEL MODE BIT
        server       point              POINT BIT
        server    polygon             POLYGON BIT
        server polygon-stipple   POLYGON STIPPLE BIT
        server      scissor           SCISSOR BIT
        server stencil-bu er      STENCIL BUFFER BIT
        server     texture            TEXTURE BIT
        server   transform           TRANSFORM BIT
        server    viewport            VIEWPORT BIT
        server                      ALL ATTRIB BITS
        client vertex-array CLIENT VERTEX ARRAY BIT
        client   pixel-store    CLIENT PIXEL STORE BIT
        client       select    can't be pushed or pop'd
        client    feedback     can't be pushed or pop'd
        client                  ALL CLIENT ATTRIB BITS


                  Table 6.2: Attribute groups




                         Version 1.2.1 - April 1, 1999
192                      CHAPTER 6. STATE AND STATE REQUESTS

        Type code Explanation
            B     Boolean
            C     Color  oating-point R, G, B, and A values
            CI    Color index  oating-point index value
             T    Texture coordinates  oating-point s, t, r, q
                  values
            N     Normal coordinates  oating-point x, y, z val-
                  ues
            V     Vertex, including associated data
            Z     Integer
            Z +   Non-negative integer
         Zk , Zk k-valued integer k indicates k is minimum
            R     Floating-point number
            R+    Non-negative oating-point number
           R a;b  Floating-point number in the range a; b
            Rk    k-tuple of oating-point numbers
            P     Position x, y, z , w oating-point coordinates
            D     Direction x, y, z oating-point coordinates
           M   4  4  4 oating-point matrix
             I    Image
            A     Attribute stack entry, including mask
            Y     Pointer data type unspeci ed
         n  type n copies of type type n indicates n is mini-
                  mum

                       Table 6.3: State variable types



to the selected light is returned; with textures, where only the selected
texture or texture parameter is returned; and with evaluator maps, where
only the selected map is returned. Finally, a " in the attribute column
indicates that the indicated value is not included in any attribute group and
thus can not be pushed or popped with PushAttrib, PushClientAttrib,
PopAttrib, or PopClientAttrib.
   The M and m entries for initial minmax table values represent the max-
imum and minimum possible representable values, respectively.




                    Version 1.2.1 - April 1, 1999
6.2. STATE TABLES                                                     193

6.2 State Tables
The tables on the following pages indicate which state variables are ob-
tained with what commands. State variables that can be obtained using any
of GetBooleanv, GetIntegerv, GetFloatv, or GetDoublev are listed
with just one of these commands the one that is most appropriate given
the type of the data to be returned. These state variables cannot be ob-
tained using IsEnabled. However, state variables for which IsEnabled is
listed as the query command can also be obtained using GetBooleanv,
GetIntegerv, GetFloatv, and GetDoublev. State variables for which
any other command is listed as the query command can be obtained only
by using that command.
    State table entries which are required only by the imaging subset see
section 3.6.2 are typeset against a gray background .




                              Version 1.2.1 - April 1, 1999
                                                                                                                                                                              194



                                                                                                                 Get  Initial
                                                                                                  Get value Type Cmnd Value        Description               Sec. Attribute
                                                                                                            Z11         0     When 6= 0, indicates           2.6.1
                                                                                                                              begin end object
                                                                                                             V                Previous vertex in             2.6.1
                                                                                                                                 Begin End line
                                                                                                             B                   Indicates if line-vertex    2.6.1
                                                                                                                                 is the rst
                                                                                                             V                   First vertex of a           2.6.1
                                                                                                                                 Begin End line loop
                                                                                                            Z+                   Line stipple counter         3.4
                                                                                                           nV                   Vertices inside of          2.6.1
                                                                                                                                 Begin End polygon
                                                                                                             Z+                  Number of                   2.6.1
                                                                                                                                 polygon-vertices
                                                                                                            2V                  Previous two vertices       2.6.1




Version 1.2.1 - April 1, 1999
                                                                                                                                 in a Begin End
                                                                                                                                 triangle strip
                                                                                                             Z3                  Number of vertices so       2.6.1
                                                                                                                                 far in triangle strip: 0,
                                                                                                                                 1, or more
                                                                                                             Z2                  Triangle strip A B          2.6.1
                                                                                                                                 vertex pointer
                                                                                                            3V                  Vertices of the quad        2.6.1
                                                                                                                                 under construction
                                                                                                             Z4                  Number of vertices so       2.6.1
                                                                                                                                 far in quad strip: 0, 1,




                                Table 6.4. GL Internal begin-end state variables inaccessible
                                                                                                                                 2, or more
                                                                                                                                                                              CHAPTER 6. STATE AND STATE REQUESTS
                                                                                                                          Get       Initial
                                                                                          Get value             Type      Cmnd      Value         Description         Sec. Attribute
                                                                                                                       GetIntegerv,
                                                                                       CURRENT COLOR             C     GetFloatv    1,1,1,1 Current color             2.7 current
                                                                                                                       GetIntegerv,
                                                                                       CURRENT INDEX             CI    GetFloatv       1    Current color index       2.7 current
                                                                                   CURRENT TEXTURE COORDS        T      GetFloatv 0,0,0,1 Current texture             2.7 current
                                                                                                                                            coordinates
                                                                                       CURRENT NORMAL            N      GetFloatv 0,0,1 Current normal                2.7     current
                                                                                                                                                                                        6.2. STATE TABLES




                                                                                                                 C                     -    Color associated with     2.6
                                                                                                                                            last vertex
                                                                                                                CI                     -    Color index associated    2.6
                                                                                                                                            with last vertex
                                                                                                                 T                     -    Texture coordinates       2.6
                                                                                                                                            associated with last
                                                                                                                                            vertex
                                                                                   CURRENT RASTER POSITION      R4      GetFloatv 0,0,0,1 Current raster position     2.12    current
                                                                                   CURRENT RASTER DISTANCE      R+      GetFloatv      0    Current raster distance   2.12    current
                                                                                                                       GetIntegerv,
                                                                                    CURRENT RASTER COLOR        C      GetFloatv    1,1,1,1 Color associated with     2.12    current
                                                                                                                                            raster position
                                                                                                                       GetIntegerv,




Version 1.2.1 - April 1, 1999
                                                                                    CURRENT RASTER INDEX        CI     GetFloatv       1    Color index associated    2.12    current
                                                                                                                                            with raster position
                                                                                CURRENT RASTER TEXTURE COORDS    T      GetFloatv 0,0,0,1 Texture coordinates         2.12    current




                                Table 6.5. Current Values and Associated Data
                                                                                                                                            associated with raster
                                                                                                                                            position
                                                                                CURRENT RASTER POSITION VALID    B     GetBooleanv True Raster position valid         2.12    current
                                                                                                                                            bit
                                                                                          EDGE FLAG              B     GetBooleanv True Edge ag                       2.6.2   current
                                                                                                                                                                                        195
                                                                                                       Get      Initial
                                                                                                                                                                             196



                                                                        Get value            Type      Cmnd     Value             Description          Sec.    Attribute
                                                                        VERTEX ARRAY          B      IsEnabled False Vertex array enable               2.8    vertex-array
                                                                      VERTEX ARRAY SIZE       Z+    GetIntegerv 4 Coordinates per vertex               2.8    vertex-array
                                                                     VERTEX ARRAY TYPE        Z4    GetIntegerv FLOAT Type of vertex coordinates       2.8    vertex-array
                                                                    VERTEX ARRAY STRIDE       Z+    GetIntegerv 0 Stride between vertices              2.8    vertex-array
                                                                   VERTEX ARRAY POINTER       Y     GetPointerv 0 Pointer to the vertex array          2.8    vertex-array
                                                                        NORMAL ARRAY          B      IsEnabled False Normal array enable               2.8    vertex-array
                                                                     NORMAL ARRAY TYPE        Z5    GetIntegerv FLOAT Type of normal coordinates       2.8    vertex-array
                                                                    NORMAL ARRAY STRIDE       Z+    GetIntegerv 0 Stride between normals               2.8    vertex-array
                                                                   NORMAL ARRAY POINTER       Y     GetPointerv 0 Pointer to the normal array          2.8    vertex-array
                                                                         COLOR ARRAY          B      IsEnabled False Color array enable                2.8    vertex-array
                                                                      COLOR ARRAY SIZE        Z+    GetIntegerv 4 Colors per vertex                    2.8    vertex-array
                                                                      COLOR ARRAY TYPE        Z8    GetIntegerv FLOAT Type of color components         2.8    vertex-array
                                                                     COLOR ARRAY STRIDE       Z+    GetIntegerv 0 Stride between colors                2.8    vertex-array
                                                                    COLOR ARRAY POINTER       Y     GetPointerv 0 Pointer to the color array           2.8    vertex-array
                                                                         INDEX ARRAY          B      IsEnabled False Index array enable                2.8    vertex-array




Version 1.2.1 - April 1, 1999
                                                                      INDEX ARRAY TYPE        Z4    GetIntegerv FLOAT Type of indices                  2.8    vertex-array
                                                                     INDEX ARRAY STRIDE       Z+    GetIntegerv 0 Stride between indices               2.8    vertex-array
                                                                    INDEX ARRAY POINTER       Y     GetPointerv 0 Pointer to the index array           2.8    vertex-array




                                Table 6.6. Vertex Array Data
                                                                   TEXTURE COORD ARRAY        B      IsEnabled False Texture coordinate array enable   2.8    vertex-array
                                                                 TEXTURE COORD ARRAY SIZE     Z+    GetIntegerv 4 Coordinates per element              2.8    vertex-array
                                                                 TEXTURE COORD ARRAY TYPE     Z4    GetIntegerv FLOAT Type of texture coordinates      2.8    vertex-array
                                                                TEXTURE COORD ARRAY STRIDE    Z+    GetIntegerv 0 Stride between texture coordinates   2.8    vertex-array
                                                               TEXTURE COORD ARRAY POINTER    Y     GetPointerv 0 Pointer to the texture coordinate    2.8    vertex-array
                                                                                                                        array
                                                                     EDGE FLAG ARRAY         B       IsEnabled False Edge ag array enable              2.8    vertex-array
                                                                  EDGE FLAG ARRAY STRIDE     Z+     GetIntegerv 0 Stride between edge ags              2.8    vertex-array
                                                                 EDGE FLAG ARRAY POINTER     Y      GetPointerv 0 Pointer to the edge ag array         2.8    vertex-array
                                                                                                                                                                             CHAPTER 6. STATE AND STATE REQUESTS
                                                                                                            Get           Initial
                                                                         Get value              Type        Cmnd          Value            Description          Sec.       Attribute
                                                                       COLOR MATRIX           2  M 4    GetFloatv      Identity    Color matrix stack         3.6.3
                                                                     MODELVIEW MATRIX        32  M 4    GetFloatv      Identity    Model-view matrix         2.10.2
                                                                                                                                     stack
                                                                     PROJECTION MATRIX       2  M 4     GetFloatv      Identity    Projection matrix         2.10.2
                                                                                                                                     stack
                                                                      TEXTURE MATRIX         2  M 4     GetFloatv      Identity    Texture matrix stack      2.10.2
                                                                                                                                                                                           6.2. STATE TABLES




                                                                         VIEWPORT              4Z       GetIntegerv    see 2.10.1   Viewport origin &         2.10.1      viewport
                                                                                                                                     extent
                                                                        DEPTH RANGE           2  R+      GetFloatv        0,1       Depth range near &        2.10.1      viewport
                                                                                                                                     far
                                                                  COLOR MATRIX STACK DEPTH      Z+       GetIntegerv        1        Color matrix stack        3.6.3
                                                                                                                                     pointer
                                                                   MODELVIEW STACK DEPTH        Z+       GetIntegerv        1        Model-view matrix         2.10.2
                                                                                                                                     stack pointer
                                                                   PROJECTION STACK DEPTH       Z+       GetIntegerv        1        Projection matrix         2.10.2
                                                                                                                                     stack pointer
                                                                    TEXTURE STACK DEPTH         Z+       GetIntegerv        1        Texture matrix stack      2.10.2
                                                                                                                                     pointer
                                                                        MATRIX MODE             Z4       GetIntegerv    MODELVIEW    Current matrix mode       2.10.2     transform




                                Table 6.7. Transformation state
Version 1.2.1 - April 1, 1999
                                                                         NORMALIZE              B         IsEnabled       False      Current normal            2.10.3 transform enable
                                                                                                                                     normalization on o
                                                                      RESCALE NORMAL            B         IsEnabled       False      Current normal            2.10.3 transform enable
                                                                                                                                     rescaling on o
                                                                         CLIP PLANEi         6  R 4    GetClipPlane    0,0,0,0     User clipping plane       2.11        transform
                                                                                                                                     coe cients
                                                                         CLIP PLANEi          6  B      IsEnabled       False      ith user clipping plane   2.11     transform enable
                                                                                                                                     enabled
                                                                                                                                                                                           197
                                                                                                                                       198




                                                                              Get       Initial
                                                       Get value    Type      Cmnd      Value         Description   Sec.   Attribute
                                                       FOG COLOR     C      GetFloatv 0,0,0,0 Fog color             3.10      fog
                                                       FOG INDEX     CI     GetFloatv      0    Fog index           3.10      fog
                                                      FOG DENSITY    R      GetFloatv     1.0   Exponential fog     3.10      fog
                                                                                                density
                                                       FOG START    R       GetFloatv     0.0   Linear fog start     3.10     fog
                                                         FOG END    R       GetFloatv     1.0   Linear fog end       3.10     fog




Version 1.2.1 - April 1, 1999
                                                        FOG MODE    Z3     GetIntegerv EXP Fog mode                  3.10     fog




                                Table 6.8. Coloring
                                                           FOG      B       IsEnabled False True if fog enabled      3.10 fog enable
                                                      SHADE MODEL   Z+     GetIntegerv SMOOTH ShadeModel setting    2.13.7 lighting
                                                                                                                                       CHAPTER 6. STATE AND STATE REQUESTS
                                                                                                                              Get                Initial
                                                                                                Get value           Type      Cmnd               Value             Description      Sec.     Attribute
                                                                                                LIGHTING             B      IsEnabled             False         True if lighting   2.13.1 lighting enable
                                                                                                                                                                is enabled
                                                                                             COLOR MATERIAL          B      IsEnabled            False          True if color      2.13.3 lighting enable
                                                                                                                                                                tracking is
                                                                                                                                                                enabled
                                                                                        COLOR MATERIAL PARAMETER     Z5    GetIntegerv    AMBIENT AND DIFFUSE   Material           2.13.3     lighting
                                                                                                                                                                properties
                                                                                                                                                                                                            6.2. STATE TABLES




                                                                                                                                                                tracking current
                                                                                                                                                                color
                                                                                           COLOR MATERIAL FACE       Z3    GetIntegerv      FRONT AND BACK      Faces a ected    2.13.3     lighting
                                                                                                                                                                by color
                                                                                                                                                                tracking
                                                                                                AMBIENT             2  C GetMaterialfv     0.2,0.2,0.2,1.0   Ambient            2.13.1     lighting
                                                                                                                                                                material color
                                                                                                 DIFFUSE            2  C GetMaterialfv     0.8,0.8,0.8,1.0   Di use material    2.13.1     lighting
                                                                                                                                                                color
                                                                                                SPECULAR            2  C GetMaterialfv     0.0,0.0,0.0,1.0   Specular           2.13.1     lighting
                                                                                                                                                                material color
                                                                                                EMISSION            2  C GetMaterialfv     0.0,0.0,0.0,1.0   Emissive mat.      2.13.1     lighting
                                                                                                                                                                color




Version 1.2.1 - April 1, 1999
                                                                                                SHININESS           2  R GetMaterialfv           0.0           Specular           2.13.1     lighting
                                                                                                                                                                exponent of
                                                                                                                                                                material
                                                                                           LIGHT MODEL AMBIENT       C      GetFloatv       0.2,0.2,0.2,1.0   Ambient scene      2.13.1     lighting




                                Table 6.9. Lighting see also Table 2.7 for defaults
                                                                                                                                                                color
                                                                                        LIGHT MODEL LOCAL VIEWER     B     GetBooleanv           False          Viewer is local    2.13.1     lighting
                                                                                           LIGHT MODEL TWO SIDE      B     GetBooleanv           False          Use two-sided      2.13.1     lighting
                                                                                                                                                                lighting
                                                                                                                                                                                                            199




                                                                                        LIGHT MODEL COLOR CONTROL    Z2    GetIntegerv       SINGLE COLOR       Color control      2.13.1     lighting
                                                                                                                                                                                  200




                                                                                                      Get          Initial
                                                                     Get value           Type         Cmnd         Value              Description         Sec.     Attribute
                                                                     AMBIENT            8  C    GetLightfv 0.0,0.0,0.0,1.0 Ambient intensity of      2.13.1     lighting
                                                                                                                               light i
                                                                      DIFFUSE            8  C   GetLightfv      see 2.5      Di use intensity of       2.13.1     lighting
                                                                                                                               light i
                                                                     SPECULAR            8  C   GetLightfv      see 2.5      Specular intensity of     2.13.1     lighting
                                                                                                                               light i
                                                                      POSITION           8  P   GetLightfv 0.0,0.0,1.0,0.0 Position of light i       2.13.1     lighting
                                                               CONSTANT ATTENUATION     8  R +  GetLightfv         1.0       Constant atten. factor    2.13.1     lighting
                                                                 LINEAR ATTENUATION     8  R +  GetLightfv         0.0       Linear atten. factor      2.13.1     lighting
                                                               QUADRATIC ATTENUATION    8  R +  GetLightfv         0.0       Quadratic atten.          2.13.1     lighting
                                                                                                                               factor




Version 1.2.1 - April 1, 1999
                                                                  SPOT DIRECTION         8  D   GetLightfv   0.0,0.0,-1.0 Spotlight direction of     2.13.1     lighting
                                                                                                                               light i
                                                                  SPOT EXPONENT         8  R +  GetLightfv         0.0       Spotlight exponent of     2.13.1     lighting




                                Table 6.10. Lighting cont.
                                                                                                                               light i
                                                                    SPOT CUTOFF         8  R +  GetLightfv       180.0       Spot. angle of light i    2.13.1     lighting
                                                                       LIGHTi            8  B   IsEnabled         False      True if light i enabled   2.13.1 lighting enable
                                                                   COLOR INDEXES       2  3  R GetMaterialfv      0,1,1      am , dm , and sm for      2.13.1     lighting
                                                                                                                               color index lighting
                                                                                                                                                                                  CHAPTER 6. STATE AND STATE REQUESTS
                                                                                                   Get         Initial
                                                                  Get value         Type           Cmnd        Value           Description        Sec.     Attribute
                                                                   POINT SIZE        R+         GetFloatv        1.0     Point size                3.3       point
                                                                 POINT SMOOTH        B          IsEnabled       False    Point antialiasing on     3.3   point enable
                                                                   LINE WIDTH        R+         GetFloatv        1.0     Line width                3.4        line
                                                                  LINE SMOOTH        B          IsEnabled       False    Line antialiasing on      3.4    line enable
                                                             LINE STIPPLE PATTERN    Z+        GetIntegerv       1's     Line stipple             3.4.2       line
                                                              LINE STIPPLE REPEAT    Z+        GetIntegerv        1      Line stipple repeat      3.4.2       line
                                                                  LINE STIPPLE       B          IsEnabled       False    Line stipple enable      3.4.2   line enable
                                                                    CULL FACE        B          IsEnabled       False    Polygon culling          3.5.1 polygon enable
                                                                                                                                                                           6.2. STATE TABLES




                                                                                                                         enabled
                                                               CULL FACE MODE        Z3        GetIntegerv      BACK     Cull front back facing   3.5.1      polygon
                                                                                                                         polygons
                                                                 FRONT FACE          Z2        GetIntegerv      CCW      Polygon frontface        3.5.1      polygon
                                                                                                                         CW CCW indicator
                                                               POLYGON SMOOTH         B         IsEnabled       False    Polygon antialiasing     3.5     polygon enable
                                                                                                                         on
                                                                POLYGON MODE        2  Z3     GetIntegerv      FILL     Polygon rasterization    3.5.4      polygon
                                                                                                                         mode front & back
                                                            POLYGON OFFSET FACTOR     R         GetFloatv         0      Polygon o set factor     3.5.5     polygon
                                                             POLYGON OFFSET UNITS     R         GetFloatv         0      Polygon o set bias       3.5.5     polygon




                                Table 6.11. Rasterization
                                                             POLYGON OFFSET POINT     B         IsEnabled       False    Polygon o set enable     3.5.5 polygon enable




Version 1.2.1 - April 1, 1999
                                                                                                                         for POINT mode
                                                                                                                         rasterization
                                                             POLYGON OFFSET LINE      B         IsEnabled       False    Polygon o set enable     3.5.5 polygon enable
                                                                                                                         for LINE mode
                                                                                                                         rasterization
                                                             POLYGON OFFSET FILL      B         IsEnabled       False    Polygon o set enable     3.5.5 polygon enable
                                                                                                                         for FILL mode
                                                                                                                         rasterization
                                                                                                                                                                           201




                                                                                      I      GetPolygonStipple 1's       Polygon stipple           3.5 polygon-stipple
                                                               POLYGON STIPPLE        B         IsEnabled      False     Polygon stipple enable   3.5.2 polygon enable
                                                                                                        Get             Initial
                                                                                                                                                                               202



                                                                      Get value         Type            Cmnd            Value          Description       Sec.    Attribute
                                                              TEXTURE xD                3B           IsEnabled          False True if xD texturing is 3.8.10 texture enable
                                                                                                                                enabled; x is 1, 2, or 3
                                                              TEXTURE BINDING xD        3  Z+       GetIntegerv           0    Texture object bound     3.8.8    texture
                                                                                                                                to TEXTURE xD
                                                              TEXTURE xD                nI          GetTexImage        see 3.8 xD texture image at       3.8
                                                                                                                                l.o.d. i
                                                              TEXTURE WIDTH             n  Z+   GetTexLevelParameter      0    xD texture image i's      3.8
                                                                                                                                speci ed width
                                                              TEXTURE HEIGHT            n  Z + GetTexLevelParameter       0    2D texture image i's      3.8
                                                                                                                                speci ed height
                                                              TEXTURE DEPTH             n  Z + GetTexLevelParameter       0    3D texture image i's      3.8
                                                                                                                                speci ed depth
                                                              TEXTURE BORDER            n  Z + GetTexLevelParameter       0    xD texture image i's      3.8
                                                                                                                                speci ed border width
                                                              TEXTURE INTERNAL FORMAT   n  Z42 GetTexLevelParameter       1    xD texture image i's      3.8




Version 1.2.1 - April 1, 1999
                                                              TEXTURE COMPONENTS                                              internal image format
                                                              TEXTURE RED SIZE          n  Z + GetTexLevelParameter       0    xD texture image i's      3.8
                                                                                                                                red resolution
                                                              TEXTURE GREEN SIZE                                           0    xD texture image i's      3.8




                                Table 6.12. Texture Objects
                                                                                        n  Z + GetTexLevelParameter
                                                                                                                                green resolution
                                                              TEXTURE BLUE SIZE         n  Z + GetTexLevelParameter       0    xD texture image i's      3.8
                                                                                                                                blue resolution
                                                              TEXTURE ALPHA SIZE        n  Z + GetTexLevelParameter       0    xD texture image i's      3.8
                                                                                                                                alpha resolution
                                                              TEXTURE LUMINANCE SIZE    n  Z + GetTexLevelParameter       0    xD texture image i's      3.8
                                                                                                                                luminance resolution
                                                              TEXTURE INTENSITY SIZE    n  Z + GetTexLevelParameter       0    xD texture image i's      3.8
                                                                                                                                                                               CHAPTER 6. STATE AND STATE REQUESTS




                                                                                                                                intensity resolution
                                                                                                               Get           Initial
                                                                             Get value         Type            Cmnd          Value            Description        Sec. Attribute
                                                                      TEXTURE BORDER COLOR    2+  C     GetTexParameter     0,0,0,0   Texture border color       3.8 texture
                                                                                                                                                                                   6.2. STATE TABLES




                                                                      TEXTURE MIN FILTER      2+  Z6    GetTexParameter     see 3.8   Texture mini cation       3.8.5 texture
                                                                                                                                       function
                                                                      TEXTURE MAG FILTER      2+  Z2     GetTexParameter     see 3.8 Texture magni cation       3.8.6   texture
                                                                                                                                       function
                                                                      TEXTURE WRAP S          3+  Z3     GetTexParameter     REPEAT   Texture wrap mode S        3.8    texture
                                                                      TEXTURE WRAP T          2+  Z3     GetTexParameter     REPEAT   Texture wrap mode T        3.8    texture
                                                                      TEXTURE WRAP R          1+  Z3     GetTexParameter     REPEAT   Texture wrap mode R        3.8    texture
                                                                      TEXTURE PRIORITY        +
                                                                                             2  R 0;1   GetTexParameterfv       1     Texture object priority   3.8.8   texture
                                                                      TEXTURE RESIDENT        2+  B     GetTexParameteriv   see 3.8.8 Texture residency         3.8.8   texture
                                                                      TEXTURE MIN LOD          nR       GetTexParameterfv     -1000 Minimum level of             3.8    texture
                                                                                                                                       detail
                                                                      TEXTURE MAX LOD          nR       GetTexParameterfv      1000 Maximum level of            3.8     texture
                                                                                                                                       detail




Version 1.2.1 - April 1, 1999
                                                                      TEXTURE BASE LEVEL                                         0     Base texture array        3.8     texture




                                Table 6.13. Texture Objects cont.
                                                                                               nR       GetTexParameterfv
                                                                      TEXTURE MAX LEVEL        nR       GetTexParameterfv      1000 Maximum texture             3.8     texture
                                                                                                                                       array level
                                                                                                                                                                                   203
                                                                                                                                                                                         204




                                                                                                                 Get          Initial
                                                                                     Get value       Type        Cmnd         Value            Description       Sec.      Attribute
                                                                                 TEXTURE ENV MODE     Z4      GetTexEnviv   MODULATE     Texture application     3.8.9      texture
                                                                                                                                         function
                                                                                 TEXTURE ENV COLOR     C      GetTexEnvfv     0,0,0,0    Texture environment     3.8.9      texture
                                                                                                                                         color
                                                                                   TEXTURE GEN x     4B       IsEnabled      False      Texgen enabled x is    2.10.4 texture enable
                                                                                                                                         S, T, R, or Q
                                                                                     EYE PLANE       4  R4   GetTexGenfv   see 2.10.4   Texgen plane equation   2.10.4     texture
                                                                                                                                         coe cients for S, T,
                                                                                                                                         R, and Q




Version 1.2.1 - April 1, 1999
                                                                                   OBJECT PLANE      4  R4 GetTexGenfv     see 2.10.4   Texgen object linear    2.10.4     texture
                                                                                                                                         coe cients for S, T,
                                                                                                                                         R, and Q
                                                                                 TEXTURE GEN MODE    4  Z3 GetTexGeniv     EYE LINEAR   Function used for       2.10.4     texture
                                                                                                                                         texgen for S, T, R,
                                                                                                                                         and Q




                                Table 6.14. Texture Environment and Generation
                                                                                                                                                                                         CHAPTER 6. STATE AND STATE REQUESTS
                                                                                                             Get         Initial
                                                                          Get value                 Type     Cmnd        Value             Description        Sec.          Attribute
                                                                         SCISSOR TEST                 B    IsEnabled      False     Scissoring enabled        4.1.2      scissor enable
                                                                          SCISSOR BOX               4  Z GetIntegerv   see 4.1.2   Scissor box               4.1.2          scissor
                                                                          ALPHA TEST                  B    IsEnabled      False     Alpha test enabled        4.1.3   color-bu er enable
                                                                       ALPHA TEST FUNC                Z8 GetIntegerv    ALWAYS      Alpha test function       4.1.3       color-bu er
                                                                        ALPHA TEST REF               R+ GetIntegerv        0        Alpha test reference      4.1.3       color-bu er
                                                                                                                                    value
                                                                        STENCIL TEST                B      IsEnabled     False      Stenciling enabled        4.1.4 stencil-bu er enable
                                                                                                                                                                                           6.2. STATE TABLES




                                                                        STENCIL FUNC                Z8    GetIntegerv   ALWAYS      Stencil function          4.1.4     stencil-bu er
                                                                     STENCIL VALUE MASK             Z+    GetIntegerv      1's      Stencil mask              4.1.4     stencil-bu er
                                                                         STENCIL REF                Z+    GetIntegerv       0       Stencil reference value   4.1.4     stencil-bu er
                                                                         STENCIL FAIL               Z6    GetIntegerv    KEEP       Stencil fail action       4.1.4     stencil-bu er
                                                                   STENCIL PASS DEPTH FAIL          Z6    GetIntegerv    KEEP       Stencil depth bu er       4.1.4     stencil-bu er
                                                                                                                                    fail action
                                                                   STENCIL PASS DEPTH PASS           Z6   GetIntegerv    KEEP       Stencil depth bu er       4.1.4     stencil-bu er
                                                                                                                                    pass action
                                                                          DEPTH TEST                 B     IsEnabled     False      Depth bu er enabled       4.1.5 depth-bu er enable
                                                                          DEPTH FUNC                 Z8   GetIntegerv    LESS       Depth bu er test          4.1.5    depth-bu er
                                                                                                                                    function
                                                                            BLEND                    B     IsEnabled     False      Blending enabled          4.1.6   color-bu er enable




                                Table 6.15. Pixel Operations
                                                                          BLEND SRC                 Z13   GetIntegerv     ONE       Blending source           4.1.6       color-bu er




Version 1.2.1 - April 1, 1999
                                                                                                                                    function
                                                                          BLEND DST                 Z12   GetIntegerv    ZERO       Blending destination      4.1.6      color-bu er
                                                                                                                                    function
                                                                       BLEND EQUATION               Z5    GetIntegerv   FUNC ADD    Blending equation         4.1.6       color-bu er
                                                                         BLEND COLOR                 C     GetFloatv     0,0,0,0    Constant blend color      4.1.6       color-bu er
                                                                            DITHER                   B     IsEnabled      True      Dithering enabled         4.1.7   color-bu er enable
                                                               INDEX LOGIC OP v1.0: GL LOGIC OP    B     IsEnabled      False     Index logic op enabled    4.1.8   color-bu er enable
                                                                       COLOR LOGIC OP                B     IsEnabled      False     Color logic op enabled    4.1.8   color-bu er enable
                                                                                                                                                                                           205




                                                                        LOGIC OP MODE               Z16   GetIntegerv    COPY       Logic op function         4.1.8       color-bu er
                                                                                                                                                                    206




                                                                                                   Get     Initial
                                                                     Get value         Type        Cmnd    Value          Description         Sec.     Attribute
                                                                    DRAW BUFFER        Z10   GetIntegerv see 4.2.1 Bu ers selected for       4.2.1   color-bu er
                                                                                                                    drawing
                                                                  INDEX WRITEMASK        Z +  GetIntegerv    1's    Color index writemask     4.2.2   color-bu er
                                                                  COLOR WRITEMASK       4  B GetBooleanv True Color write enables; R,        4.2.2   color-bu er
                                                                                                                    G, B, or A
                                                                  DEPTH WRITEMASK         B   GetBooleanv True Depth bu er enabled            4.2.2 depth-bu er
                                                                                                                    for writing
                                                                 STENCIL WRITEMASK       Z+   GetIntegerv    1's    Stencil bu er             4.2.2 stencil-bu er
                                                                                                                    writemask
                                                                 COLOR CLEAR VALUE        C    GetFloatv 0,0,0,0 Color bu er clear            4.2.3   color-bu er




Version 1.2.1 - April 1, 1999
                                                                                                                    value RGBA mode
                                                                 INDEX CLEAR VALUE        CI   GetFloatv      0     Color bu er clear value   4.2.3   color-bu er
                                                                                                                    color index mode
                                                                 DEPTH CLEAR VALUE       R+   GetIntegerv     1     Depth bu er clear         4.2.3 depth-bu er




                                Table 6.16. Framebu er Control
                                                                                                                    value
                                                                 STENCIL CLEAR VALUE     Z+   GetIntegerv     0     Stencil clear value       4.2.3 stencil-bu er
                                                                  ACCUM CLEAR VALUE    4  R+ GetFloatv       0     Accumulation bu er        4.2.3 accum-bu er
                                                                                                                    clear value
                                                                                                                                                                    CHAPTER 6. STATE AND STATE REQUESTS
                                                                                 Get      Initial
                                                          Get value        Type  Cmnd     Value      Description         Sec. Attribute
                                                     UNPACK SWAP BYTES      B GetBooleanv False Value of                 4.3 pixel-store
                                                                                                   UNPACK SWAP BYTES
                                                      UNPACK LSB FIRST      B   GetBooleanv False Value of               4.3   pixel-store
                                                                                                  UNPACK LSB FIRST
                                                     UNPACK IMAGE HEIGHT   Z+   GetIntegerv   0   Value of               4.3   pixel-store
                                                                                                   UNPACK IMAGE HEIGHT
                                                     UNPACK SKIP IMAGES    Z+   GetIntegerv    0   Value of              4.3   pixel-store
                                                                                                   UNPACK SKIP IMAGES
                                                     UNPACK ROW LENGTH     Z+   GetIntegerv    0   Value of              4.3   pixel-store
                                                                                                                                             6.2. STATE TABLES




                                                                                                   UNPACK ROW LENGTH
                                                      UNPACK SKIP ROWS     Z+   GetIntegerv    0   Value of              4.3   pixel-store
                                                                                                   UNPACK SKIP ROWS
                                                      UNPACK SKIP PIXELS   Z+   GetIntegerv    0   Value of              4.3   pixel-store
                                                                                                   UNPACK SKIP PIXELS
                                                      UNPACK ALIGNMENT     Z+   GetIntegerv    4   Value of              4.3   pixel-store
                                                                                                   UNPACK ALIGNMENT
                                                       PACK SWAP BYTES      B   GetBooleanv False Value of               4.3   pixel-store
                                                                                                  PACK SWAP BYTES




                                Table 6.17. Pixels
                                                        PACK LSB FIRST      B   GetBooleanv False Value of               4.3   pixel-store
                                                                                                   PACK LSB FIRST
                                                      PACK IMAGE HEIGHT    Z+   GetIntegerv    0   Value of              4.3   pixel-store
                                                                                                   PACK IMAGE HEIGHT




Version 1.2.1 - April 1, 1999
                                                      PACK SKIP IMAGES     Z+   GetIntegerv    0   Value of              4.3   pixel-store
                                                                                                   PACK SKIP IMAGES
                                                      PACK ROW LENGTH      Z+   GetIntegerv    0   Value of              4.3   pixel-store
                                                                                                   PACK ROW LENGTH
                                                       PACK SKIP ROWS      Z+   GetIntegerv    0   Value of              4.3   pixel-store
                                                                                                   PACK SKIP ROWS
                                                       PACK SKIP PIXELS    Z+   GetIntegerv    0   Value of              4.3   pixel-store
                                                                                                                                             207




                                                                                                   PACK SKIP PIXELS
                                                       PACK ALIGNMENT      Z+   GetIntegerv    4   Value of              4.3   pixel-store
                                                                                                   PACK ALIGNMENT
                                                                                                                   Get          Initial
                                                                       Get value                 Type              Cmnd         Value         Description         Sec.    Attribute
                                                                      MAP COLOR                   B           GetBooleanv        False True if colors are         4.3       pixel
                                                                                                                                        mapped
                                                                                                                                                                                       208



                                                                      MAP STENCIL                  B          GetBooleanv        False True if stencil values     4.3       pixel
                                                                                                                                        are mapped
                                                                      INDEX SHIFT                  Z          GetIntegerv          0    Value of INDEX SHIFT      4.3       pixel
                                                                     INDEX OFFSET                  Z          GetIntegerv          0    Value of INDEX OFFSET     4.3       pixel
                                                                        x SCALE                    R          GetFloatv            1    Value of x SCALE; x is    4.3       pixel
                                                                                                                                        RED, GREEN, BLUE,
                                                                                                                                        ALPHA, or DEPTH
                                                                         x BIAS                    R          GetFloatv            0    Value of x BIAS; x is     4.3       pixel
                                                                                                                                        one of RED, GREEN,
                                                                                                                                        BLUE, ALPHA, or DEPTH
                                                                     COLOR TABLE                   B          IsEnabled          False True if color table        3.6.3 pixel enable
                                                                                                                                        lookup is done
                                                             POST CONVOLUTION COLOR TABLE          B          IsEnabled          False True if post               3.6.3 pixel enable
                                                                                                                                        convolution color table
                                                                                                                                        lookup is done
                                                             POST COLOR MATRIX COLOR TABLE         B          IsEnabled          False True if post color         3.6.3 pixel enable




Version 1.2.1 - April 1, 1999
                                                                                                                                        matrix color table
                                                                                                                                        lookup is done
                                                                     COLOR TABLE                 3I          GetColorTable     empty Color tables                3.6.3




                                Table 6.18. Pixels cont.
                                                                  COLOR TABLE FORMAT          2  3  Z42     GetColorTable-     RGBA   Color tables' internal    3.6.3
                                                                                                              Parameteriv               image format
                                                                  COLOR TABLE WIDTH           2  3  Z+      GetColorTable-       0    Color tables' speci ed    3.6.3
                                                                                                              Parameteriv               width
                                                                   COLOR TABLE x SIZE        6  2  3  Z+   GetColorTable-       0    Color table component     3.6.3
                                                                                                              Parameteriv               resolution; x is RED,
                                                                                                                                        GREEN, BLUE, ALPHA,
                                                                                                                                        LUMINANCE, or
                                                                                                                                        INTENSITY
                                                                                                                                                                                       CHAPTER 6. STATE AND STATE REQUESTS




                                                                   COLOR TABLE SCALE            3  R4        GetColorTable- 1,1,1,1 Scale factors applied 3.6.3            pixel
                                                                                                              Parameterfv            to color table entries
                                                                   COLOR TABLE BIAS             3  R4        GetColorTable- 0,0,0,0 Bias factors applied to 3.6.3          pixel
                                                                                                              Parameterfv            color table entries
                                                                                                      Get           Initial
                                                                    Get value            Type         Cmnd          Value           Description        Sec. Attribute
                                                                  CONVOLUTION 1D          B       IsEnabled          False    True if 1D convolution   3.6.3 pixel enable
                                                                                                                              is done
                                                                  CONVOLUTION 2D          B       IsEnabled          False    True if 2D convolution   3.6.3 pixel enable
                                                                                                                              is done
                                                                   SEPARABLE 2D           B       IsEnabled          False    True if separable 2D     3.6.3 pixel enable
                                                                                                                              convolution is done
                                                                                                                                                                            6.2. STATE TABLES




                                                                   CONVOLUTION           2I      GetConvolution-   empty     Convolution lters        3.6.3
                                                                                                  Filter
                                                                   CONVOLUTION           2I      GetSeparable-     empty   Separable convolution      3.6.3
                                                                                                  Filter                      lter
                                                             CONVOLUTION BORDER COLOR   3C       GetConvolution-   0,0,0,0 Convolution border         4.3       pixel
                                                                                                  Parameterfv               color
                                                             CONVOLUTION BORDER MODE    3  Z4    GetConvolution-   REDUCE Convolution border          4.3       pixel
                                                                                                  Parameteriv               mode
                                                             CONVOLUTION FILTER SCALE   3  R4    GetConvolution-   1,1,1,1 Scale factors applied      3.6.3     pixel
                                                                                                  Parameterfv               to convolution lter
                                                                                                                            entries




                                Table 6.19. Pixels cont.
                                                              CONVOLUTION FILTER BIAS   3  R4    GetConvolution-   0,0,0,0 Bias factors applied to    3.6.3     pixel




Version 1.2.1 - April 1, 1999
                                                                                                  Parameterfv               convolution lter
                                                                                                                            entries
                                                               CONVOLUTION FORMAT       3  Z42   GetConvolution-    RGBA   Convolution lter           4.3
                                                                                                  Parameteriv               internal format
                                                                CONVOLUTION WIDTH       3  Z+    GetConvolution-      0    Convolution lter           4.3
                                                                                                  Parameteriv               width
                                                                CONVOLUTION HEIGHT      2  Z+    GetConvolution-      0    Convolution lter           4.3
                                                                                                  Parameteriv               height
                                                                                                                                                                            209
                                                                                                          Get         Initial
                                                                    Get value              Type           Cmnd        Value         Description        Sec.    Attribute
                                                                                                                                                                            210



                                                             POST CONVOLUTION x SCALE       R         GetFloatv          1    Component scale          3.6.3     pixel
                                                                                                                              factors after
                                                                                                                              convolution: x is RED,
                                                                                                                              GREEN, BLUE, or ALPHA
                                                              POST CONVOLUTION x BIAS        R        GetFloatv          0    Component bias           3.6.3     pixel
                                                                                                                              factors after
                                                                                                                              convolution: x is RED,
                                                                                                                              GREEN, BLUE, or ALPHA
                                                             POST COLOR MATRIX x SCALE       R        GetFloatv          1    Component scale          3.6.3     pixel
                                                                                                                              factors after color
                                                                                                                              matrix; x is RED,
                                                                                                                              GREEN, BLUE, or ALPHA
                                                             POST COLOR MATRIX x BIAS        R        GetFloatv          0    Component bias           3.6.3     pixel
                                                                                                                              factors after color
                                                                                                                              matrix; x is RED,
                                                                                                                              GREEN, BLUE, or ALPHA




Version 1.2.1 - April 1, 1999
                                                                    HISTOGRAM                B        IsEnabled        False True if histogramming     3.6.3 pixel enable
                                                                                                                              is enabled
                                                                    HISTOGRAM




                                Table 6.20. Pixels cont.
                                                                                             I        GetHistogram    empty Histogram table            3.6.3
                                                                 HISTOGRAM WIDTH          2  Z+      GetHistogram-      0    Histogram table width    3.6.3
                                                                                                      Parameteriv
                                                                HISTOGRAM FORMAT          2  Z42     GetHistogram-   RGBA    Histogram table          3.6.3
                                                                                                      Parameteriv             internal format
                                                                 HISTOGRAM x SIZE        5  2  Z+   GetHistogram-     0     Histogram table          3.6.3
                                                                                                      Parameteriv             component resolution;
                                                                                                                              x is RED, GREEN, BLUE,
                                                                                                                              ALPHA, or LUMINANCE
                                                                  HISTOGRAM SINK             B        GetHistogram-   False   True if histogramming    3.6.3
                                                                                                                                                                            CHAPTER 6. STATE AND STATE REQUESTS




                                                                                                      Parameteriv             consumes pixel groups
                                                                                            Get                Initial
                                                               Get value       Type         Cmnd               Value             Description          Sec. Attribute
                                                                MINMAX          B        IsEnabled              False      True if minmax is          3.6.3 pixel enable
                                                                                                                           enabled
                                                                                                                                                                           6.2. STATE TABLES




                                                                MINMAX           Rn      GetMinmax     M,M,M,M,m,m,m,m Minmax table               3.6.3
                                                             MINMAX FORMAT       Z42     GetMinmax-            RGBA        Minmax table internal      3.6.3
                                                                                         Parameteriv                       format
                                                              MINMAX SINK         B      GetMinmax-            False       True if minmax             3.6.3
                                                                                         Parameteriv                       consumes pixel groups
                                                                ZOOM X            R      GetFloatv              1.0        x zoom factor              4.3       pixel
                                                                ZOOM Y            R      GetFloatv              1.0        y zoom factor              4.3       pixel
                                                                   x         8  32  R GetPixelMap            0's        RGBA PixelMap              4.3
                                                                                                                           translation tables; x is
                                                                                                                           a map name from
                                                                                                                           Table 3.3
                                                                   x




                                Table 6.21. Pixels cont.
                                                                             2  32  Z GetPixelMap            0's        Index PixelMap             4.3
                                                                                                                           translation tables; x is




Version 1.2.1 - April 1, 1999
                                                                                                                           a map name from
                                                                                                                           Table 3.3
                                                                 x SIZE         Z+      GetIntegerv              1         Size of table x            4.3
                                                              READ BUFFER       Z3      GetIntegerv          see 4.3.2     Read source bu er          4.3       pixel
                                                                                                                                                                           211
                                                                                                                                                                                        212




                                                                                                                             Get       Initial
                                                                                       Get value              Type           Cmnd      Value       Description      Sec. Attribute
                                                                                        ORDER                9  Z8       GetMapiv       1  1d map order           5.1
                                                                                        ORDER              9  2  Z8     GetMapiv      1,1 2d map orders          5.1
                                                                                         COEFF            9  8  Rn      GetMapfv    see 5.1
                                                                                                                                             1d control points      5.1
                                                                                         COEFF          9  8  8  Rn   GetMapfv    see 5.1
                                                                                                                                             2d control points      5.1
                                                                                        DOMAIN              92R          GetMapfv    see 5.1
                                                                                                                                             1d domain endpoints    5.1
                                                                                        DOMAIN              94R          GetMapfv    see 5.1
                                                                                                                                             2d domain endpoints    5.1
                                                                                        MAP1 x                9B          IsEnabled    False1d map enables: x is   5.1 eval enable
                                                                                                                                             map type
                                                                                         MAP2 x              9B           IsEnabled False 2d map enables: x is     5.1   eval enable
                                                                                                                                             map type




Version 1.2.1 - April 1, 1999
                                                                                    MAP1 GRID DOMAIN         2R           GetFloatv 0,1 1d grid endpoints          5.1       eval
                                                                                    MAP2 GRID DOMAIN         4R           GetFloatv 0,1;0,1 2d grid endpoints      5.1       eval
                                                                                   MAP1 GRID SEGMENTS         Z+           GetFloatv    1    1d grid divisions      5.1       eval
                                                                                   MAP2 GRID SEGMENTS       2  Z+         GetFloatv 1,1 2d grid divisions          5.1       eval
                                                                                      AUTO NORMAL              B           IsEnabled False True if automatic        5.1   eval enable
                                                                                                                                             normal generation
                                                                                                                                             enabled




                                Table 6.22. Evaluators GetMap takes a map name
                                                                                                                                                                                        CHAPTER 6. STATE AND STATE REQUESTS
                                                                                                                                                             6.2. STATE TABLES




                                                                                         Get          Initial
                                                            Get value             Type   Cmnd         Value              Description        Sec. Attribute
                                                    PERSPECTIVE CORRECTION HINT    Z3 GetIntegerv    DONT CARE     Perspective correction   5.6    hint
                                                                                                                   hint
                                                        POINT SMOOTH HINT         Z3   GetIntegerv   DONT   CARE   Point smooth hint        5.6     hint
                                                         LINE SMOOTH HINT         Z3   GetIntegerv   DONT   CARE   Line smooth hint         5.6     hint
                                                       POLYGON SMOOTH HINT        Z3   GetIntegerv   DONT   CARE   Polygon smooth hint      5.6     hint




                                Table 6.23. Hints
                                                             FOG HINT             Z3   GetIntegerv   DONT   CARE   Fog hint                 5.6     hint




Version 1.2.1 - April 1, 1999
                                                                                                                                                             213
                                                                                                                         Get      Minimum
                                                                                       Get value              Type       Cmnd     Value             Description        Sec. Attribute
                                                                                       MAX LIGHTS              Z+     GetIntegerv     8      Maximum number of        2.13.1
                                                                                                                                             lights
                                                                                     MAX CLIP PLANES            Z + GetIntegerv       6      Maximum number of        2.11
                                                                                                                                             user clipping planes
                                                                              MAX COLOR MATRIX STACK DEPTH      Z + GetIntegerv       2      Maximum color matrix     3.6.3
                                                                                                                                                                                        214



                                                                                                                                             stack depth
                                                                               MAX MODELVIEW STACK DEPTH        Z + GetIntegerv       32     Maximum model-view       2.10.2
                                                                                                                                             stack depth
                                                                               MAX PROJECTION STACK DEPTH       Z + GetIntegerv       2      Maximum projection       2.10.2
                                                                                                                                             matrix stack depth
                                                                                MAX TEXTURE STACK DEPTH         Z + GetIntegerv       2      Maximum number           2.10.2
                                                                                                                                             depth of texture
                                                                                                                                             matrix stack
                                                                                      SUBPIXEL BITS             Z + GetIntegerv       4      Number of bits of          3
                                                                                                                                             subpixel precision in
                                                                                                                                             screen xw and yw
                                                                                   MAX 3D TEXTURE SIZE          Z + GetIntegerv       16     See the discussion in     3.8
                                                                                                                                             Section 3.8.
                                                                                    MAX TEXTURE SIZE            Z + GetIntegerv       64     See the discussion in     3.8
                                                                                                                                             Section 3.8.
                                                                                  MAX PIXEL MAP TABLE           Z + GetIntegerv       32     Maximum size of a        3.6.3




Version 1.2.1 - April 1, 1999
                                                                                                                                             PixelMap translation
                                                                                                                                             table
                                                                                 MAX NAME STACK DEPTH           Z + GetIntegerv       64     Maximum selection         5.2
                                                                                                                                             name stack depth
                                                                                    MAX LIST NESTING            Z + GetIntegerv       64     Maximum display list      5.4
                                                                                                                                             call nesting
                                                                                     MAX EVAL ORDER             Z +   GetIntegerv     8      Maximum evaluator         5.1




                                Table 6.24. Implementation Dependent Values
                                                                                                                                             polynomial order
                                                                                   MAX VIEWPORT DIMS          2  Z + GetIntegerv see 2.10.1 Maximum viewport         2.10.1
                                                                                                                                             dimensions
                                                                                 MAX ATTRIB STACK DEPTH         Z + GetIntegerv       16     Maximum depth of the       6
                                                                                                                                             server attribute stack
                                                                                                                                                                                        CHAPTER 6. STATE AND STATE REQUESTS




                                                                              MAX CLIENT ATTRIB STACK DEPTH     Z + GetIntegerv       16     Maximum depth of the       6
                                                                                                                                             client attribute stack
                                                                                                              3  Z+       -          32     Maximum size of a        3.6.3
                                                                                                                                             color table
                                                                                                                Z+         -          32     Maximum size of the      3.6.3
                                                                                                                                             histogram table
                                                                                                                                 Get        Minimum
                                                                                                Get value           Type         Cmnd       Value         Description         Sec. Attribute
                                                                                   AUX BUFFERS                       Z+     GetIntegerv         0   Number of auxiliary       4.2.1
                                                                                                                                                    bu ers
                                                                                   RGBA MODE                           B    GetBooleanv             True if color bu ers      2.7
                                                                                                                                                    store rgba
                                                                                   INDEX MODE                          B    GetBooleanv             True if color bu ers      2.7
                                                                                                                                                    store indexes
                                                                                   DOUBLEBUFFER                        B    GetBooleanv             True if front & back      4.2.1
                                                                                                                                                    bu ers exist
                                                                                   STEREO                              B    GetBooleanv             True if left & right       6
                                                                                                                                                    bu ers exist
                                                                                                                                                                                               6.2. STATE TABLES




                                                                                   ALIASED POINT SIZE RANGE         2  R+ GetFloatv           1,1  Range lo to hi of       3.3
                                                                                                                                                    aliased point sizes
                                                                                   SMOOTH POINT SIZE RANGE          2  R+ GetFloatv           1,1  Range lo to hi of       3.3
                                                                                   v1.1: POINT SIZE RANGE                                         antialiased point sizes
                                                                                   SMOOTH POINT SIZE GRANULARITY      R+ GetFloatv                  Antialiased point size    3.3
                                                                                   v1.1: POINT SIZE GRANULARITY                                   granularity
                                                                                   ALIASED LINE WIDTH RANGE         2  R+ GetFloatv           1,1  Range lo to hi of       3.4
                                                                                                                                                    aliased line widths
                                                                                   SMOOTH LINE WIDTH RANGE          2  R+ GetFloatv           1,1  Range lo to hi of       3.4
                                                                                   v1.1: LINE WIDTH RANGE                                         antialiased line widths
                                                                                   SMOOTH LINE WIDTH GRANULARITY      R+ GetFloatv                  Antialiased line width    3.4
                                                                                   v1.1: LINE WIDTH GRANULARITY                                   granularity
                                                                                   MAX CONVOLUTION WIDTH




Version 1.2.1 - April 1, 1999
                                                                                                                    3  Z + GetConvolution-     3   Maximum width of          4.3
                                                                                                                            Parameteriv             convolution lter
                                                                                   MAX CONVOLUTION HEIGHT                 +
                                                                                                                    2  Z GetConvolution-       3   Maximum height of         4.3
                                                                                                                            Parameteriv             convolution lter
                                                                                   MAX ELEMENTS INDICES               Z +   GetIntegerv             Recommended               2.8




                                Table 6.25. More Implementation Dependent Values
                                                                                                                                                    maximum number of
                                                                                                                                                        DrawRangeEle-
                                                                                                                                                        ments indices
                                                                                                                                                                                               215




                                                                                   MAX ELEMENTS VERTICES             Z+     GetIntegerv                 Recommended           2.8
                                                                                                                                                        maximum number of
                                                                                                                                                        DrawRangeEle-
                                                                                                                                                        ments vertices
                                                                                                                                                                      216




                                                                                                           Get      Initial
                                                                                     Get value     Type    Cmnd     Value         Description        Sec. Attribute
                                                                                       x BITS       Z + GetIntegerv    -    Number of bits in x       4
                                                                                                                            color bu er
                                                                                                                            component; x is one of
                                                                                                                            RED, GREEN, BLUE,
                                                                                                                            ALPHA, or INDEX
                                                                                    DEPTH BITS      Z + GetIntegerv    -    Number of depth           4
                                                                                                                            bu er planes
                                                                                    STENCIL BITS    Z + GetIntegerv    -    Number of stencil         4




Version 1.2.1 - April 1, 1999
                                                                                                                            planes
                                                                                    ACCUM x BITS    Z + GetIntegerv    -    Number of bits in x       4
                                                                                                                            accumulation bu er
                                                                                                                            component x is RED,
                                                                                                                            GREEN, BLUE, or ALPHA




                                Table 6.26. Implementation Dependent Pixel Depths
                                                                                                                                                                      CHAPTER 6. STATE AND STATE REQUESTS
                                                                                                    Get        Initial
                                                                   Get value             Type       Cmnd       Value           Description        Sec. Attribute
                                                                   LIST BASE              Z+     GetIntegerv     0       Setting of ListBase      5.4     list
                                                                   LIST INDEX             Z+     GetIntegerv     0       number of display list   5.4
                                                                                                                         under construction; 0
                                                                                                                         if none
                                                                   LIST MODE             Z+      GetIntegerv     0       Mode of display list     5.4
                                                                                                                                                                   6.2. STATE TABLES




                                                                                                                         under construction;
                                                                                                                         unde ned if none
                                                                                        16  A                empty     Server attribute stack    6
                                                               ATTRIB STACK DEPTH         Z+    GetIntegerv      0       Server attribute stack    6
                                                                                                                         pointer
                                                                                        16  A                empty     Client attribute stack    6
                                                            CLIENT ATTRIB STACK DEPTH     Z+    GetIntegerv      0       Client attribute stack    6
                                                                                                                         pointer
                                                                NAME STACK DEPTH         Z+      GetIntegerv     0       Name stack depth         5.2
                                                                  RENDER MODE            Z3      GetIntegerv   RENDER    RenderMode setting       5.2
                                                            SELECTION BUFFER POINTER     Y       GetPointerv     0       Selection bu er          5.2    select
                                                                                                                         pointer




                                Table 6.27. Miscellaneous
                                                              SELECTION BUFFER SIZE      Z+      GetIntegerv     0       Selection bu er size     5.2     select




Version 1.2.1 - April 1, 1999
                                                            FEEDBACK BUFFER POINTER      Y       GetPointerv     0       Feedback bu er           5.3   feedback
                                                                                                                         pointer
                                                             FEEDBACK BUFFER SIZE         Z+     GetIntegerv     0       Feedback bu er size      5.3   feedback
                                                             FEEDBACK BUFFER TYPE         Z5     GetIntegerv     2D      Feedback type            5.3   feedback
                                                                                        n  Z8    GetError       0       Current error codes    2.5
                                                                                        nB                    False     True if there is a       2.5
                                                                                                                         corresponding error
                                                                                                                                                                   217
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
peatability as a requirement, two scenes rendered with one small polygon
changed in position might di er at every pixel. Such a di erence, while
within the law of repeatability, is certainly not within its spirit. Additional
invariance rules are desirable to ensure useful operation.
                                       218



                     Version 1.2.1 - April 1, 1999
A.2. MULTI-PASS ALGORITHMS                                               219

A.2 Multi-pass Algorithms
Invariance is necessary for a whole set of useful multi-pass algorithms. Such
algorithms render multiple times, each time with a di erent GL mode vec-
tor, to eventually produce a result in the framebu er. Examples of these
algorithms include:
      Erasing" a primitive from the framebu er by redrawing it, either in
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
that may be very di cult to achieve for example, if the hardware does
  oating-point operations with di erent precision than the software.
    What is desired is a compromise that results in many compliant, high-
performance implementations, and in many software vendors choosing to
port to OpenGL.

A.3 Invariance Rules
For a given instantiation of an OpenGL rendering context:
Rule 1 For any given GL and framebu er state vector, and for any given
GL command, the resulting GL and framebu er state must be identical each
time the command is executed on that initial GL and framebu er state.
Rule 2 Changes to the following state values have no side e ects the use
of any other state value is not a ected by the change:
Required:
           Framebu er contents all bitplanes
           The color bu ers enabled for writing




                               Version 1.2.1 - April 1, 1999
220                                            APPENDIX A. INVARIANCE

           The values of matrices other than the top-of-stack matrices
           Scissor parameters other than enable
           Writemasks color, index, depth, stencil
           Clear values color, index, depth, stencil, accumulation
           Current values color, index, normal, texture coords, edge ag
           Current raster color, index and texture coordinates.
           Material properties ambient, di use, specular, emission, shini-
           ness
Strongly suggested:
           Matrix mode
           Matrix stack depths
           Alpha test parameters other than enable
           Stencil parameters other than enable
           Depth test parameters other than enable
           Blend parameters other than enable
           Logical operation parameters other than enable
           Pixel storage and transfer state
           Evaluator state except as it a ects the vertex data generated by
           the evaluators
           Polygon o set parameters other than enables, and except as they
           a ect the depth values of fragments
Corollary 1 Fragment generation is invariant with respect to the state val-
ues marked with in Rule 2.
Corollary 2 The window coordinates x, y, and z of generated fragments
are also invariant with respect to
Required:
           Current values color, color index, normal, texture coords, edge-
            ag
           Current raster color, color index, and texture coordinates
           Material properties ambient, di use, specular, emission, shini-
           ness




                    Version 1.2.1 - April 1, 1999
A.4. WHAT ALL THIS MEANS                                                     221

Rule 3 The arithmetic of each per-fragment operation is invariant except
with respect to parameters that directly control it the parameters that control
the alpha test, for instance, are the alpha test enable, the alpha test function,
and the alpha test reference value.
Corollary 3 Images rendered into di erent color bu ers sharing the same
framebu er, either simultaneously or separately using the same command
sequence, are pixel identical.

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
in di erent renderers hardware and software, many OpenGL state values
may change subtly when renderers are swapped. This is the type of state
value change that Rule 1 seeks to avoid.




                                 Version 1.2.1 - April 1, 1999
Appendix B
Corollaries
The following observations are derived from the body and the other ap-
pendixes of the speci cation. Absence of an observation from this list in no
way impugns its veracity.
  1. The CURRENT RASTER TEXTURE COORDS must be maintained correctly at
     all times, including periods while texture mapping is not enabled, and
     when the GL is in color index mode.
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
  7. The mask speci ed as the third argument to StencilFunc a ects the
     operands of the stencil comparison function, but has no direct e ect on
                                      222



                    Version 1.2.1 - April 1, 1999
                                                                         223

      the update of the stencil bu er. The mask speci ed by StencilMask
      has no e ect on the stencil comparison function; it limits the e ect of
      the update of the stencil bu er.
 8.   Polygon shading is completed before the polygon mode is interpreted.
      If the shade model is FLAT, all of the points or lines generated by a
      single polygon will have the same color.
 9.   A display list is just a group of commands and arguments, so errors
      generated by commands in a display list must be generated when the
      list is executed. If the list is created in COMPILE mode, errors should
      not be generated while the list is being created.
10.   RasterPos does not change the current raster index from its default
      value in an RGBA mode GL context. Likewise, RasterPos does not
      change the current raster color from its default value in a color index
      GL context. Both the current raster index and the current raster
      color can be queried, however, regardless of the color mode of the GL
      context.
11.   A material property that is attached to the current color via Color-
      Material always takes the value of the current color. Attempts to
      change that material property via Material calls have no e ect.
12.   Material and ColorMaterial can be used to modify the RGBA ma-
      terial properties, even in a color index context. Likewise, Material
      can be used to modify the color index material properties, even in an
      RGBA context.
13.   There is no atomicity requirement for OpenGL rendering commands,
      even at the fragment level.
14.   Because rasterization of non-antialiased polygons is point sampled,
      polygons that have no area generate no fragments when they are ras-
      terized in FILL mode, and the fragments generated by the rasterization
      of narrow" polygons may not form a continuous array.
15.   OpenGL does not force left- or right-handedness on any of its coor-
      dinates systems. Consider, however, the following conditions: 1 the
      object coordinate system is right-handed; 2 the only commands used
      to manipulate the model-view matrix are Scale with positive scaling
      values only, Rotate, and Translate; 3 exactly one of either Frus-
      tum or Ortho is used to set the projection matrix; 4 the near value




                               Version 1.2.1 - April 1, 1999
224                                            APPENDIX B. COROLLARIES

       is less than the far value for DepthRange. If these conditions are all
       satis ed, then the eye coordinate system is right-handed and the clip,
       normalized device, and window coordinate systems are left-handed.
 16.   ColorMaterial has no e ect on color index lighting.
 17.   No pixel dropouts or duplicates. Let two polygons share an identical
       edge that is, there exist vertices A and B of an edge of one polygon,
       and vertices C and D of an edge of the other polygon, and the coordi-
       nates of vertex A resp. B are identical to those of vertex C resp. D,
       and the state of the the coordinate transfomations is identical when
       A, B, C, and D are speci ed. Then, when the fragments produced
       by rasterization of both polygons are taken together, each fragment
       intersecting the interior of the shared edge is produced exactly once.
 18.   OpenGL state continues to be modi ed in FEEDBACK mode and in
       SELECT mode. The contents of the framebu er are not modi ed.

 19.   The current raster position, the user de ned clip planes, the spot direc-
       tions and the light positions for LIGHTi, and the eye planes for texgen
       are transformed when they are speci ed. They are not transformed
       during a PopAttrib, or when copying a context.
 20.   Dithering algorithms may be di erent for di erent components. In
       particular, alpha may be dithered di erently from red, green, or blue,
       and an implementation may choose to not dither alpha at all.
 21.   For any GL and framebu er state, and for any group of GL commands
       and arguments, the resulting GL and framebu er state is identical
       whether the GL commands and arguments are executed normally or
       from a display list.




                      Version 1.2.1 - April 1, 1999
Appendix C
Version 1.1
OpenGL version 1.1 is the rst revision since the original version 1.0 was
released on 1 July 1992. Version 1.1 is upward compatible with version 1.0,
meaning that any program that runs with a 1.0 GL implementation will also
run unchanged with a 1.1 GL implementation. Several additions were made
to the GL, especially to the texture mapping capabilities, but also to the
geometry and fragment operations. Following are brief descriptions of each
addition.

C.1 Vertex Array
Arrays of vertex data may be transferred to the GL with many fewer com-
mands than were previously necessary. Six arrays are de ned, one each
storing vertex positions, normal coordinates, colors, color indices, texture
coordinates, and edge ags. The arrays may be speci ed and enabled inde-
pendently, or one of the pre-de ned con gurations may be selected with a
single command.
    The primary goal was to decrease the number of subroutine calls required
to transfer non-display listed geometry data to the GL. A secondary goal was
to improve the e ciency of the transfer; especially to allow direct memory
access DMA hardware to be used to e ect the transfer. The additions
match those of the EXT vertex array extension, except that static array data
are not supported because they complicated the interface, and were not
being used, and the pre-de ned con gurations are added both to reduce
subroutine count even further, and to allow for e cient transfer of array
data.
                                     225



                               Version 1.2.1 - April 1, 1999
226                                             APPENDIX C. VERSION 1.1

C.2 Polygon O set
Depth values of fragments generated by the rasterization of a polygon may be
shifted toward or away from the origin, as an a ne function of the window
coordinate depth slope of the polygon. Shifted depth values allow copla-
nar geometry, especially facet outlines, to be rendered without depth bu er
artifacts. They may also be used by future shadow generation algorithms.
    The additions match those of the EXT polygon offset extension, with two
exceptions. First, the o set is enabled separately for POINT, LINE, and FILL
rasterization modes, all sharing a single a ne function de nition. Shifting
the depth values of the outline fragments, instead of the ll fragments, allows
the contents of the depth bu er to be maintained correctly. Second, the
o set bias is speci ed in units of depth bu er resolution, rather than in the
 0,1 depth range.

C.3 Logical Operation
Fragments generated by RGBA rendering may be merged into the frame-
bu er using a logical operation, just as color index fragments are in GL
version 1.0. Blending is disabled during such operation because it is rarely
desired, because many systems could not support it, and to match the se-
mantics of the EXT blend logic op extension, on which this addition is loosely
based.

C.4 Texture Image Formats
Stored texture arrays have a format, known as the internal format, rather
than a simple count of components. The internal format is represented as
a single enumerated value, indicating both the organization of the image
data LUMINANCE, RGB, etc. and the number of bits of storage for each image
component. Clients can use the internal format speci cation to suggest the
desired storage precision of texture images. New base formats, ALPHA and
INTENSITY, provide new texture environment operations. These additions
match those of a subset of the EXT texture extension.

C.5 Texture Replace Environment
A common use of texture mapping is to replace the color values of generated
fragments with texture color data. This could be speci ed only indirectly




                    Version 1.2.1 - April 1, 1999
C.6. TEXTURE PROXIES                                                       227

in GL version 1.0, which required that client speci ed white" geometry
be modulated by a texture. GL version 1.1 allows such replacement to be
speci ed explicitly, possibly improving performance. These additions match
those of a subset of the EXT texture extension.

C.6 Texture Proxies
Texture proxies allow a GL implementation to advertise di erent maximum
texture image sizes as a function of some other texture parameters, especially
of the internal image format. Clients may use the proxy query mechanism
to tailor their use of texture resources at run time. The proxy interface is
designed to allow such queries without adding new routines to the GL inter-
face. These additions match those of a subset of the EXT texture extension,
except that implementations return allocation information consistent with
support for complete mipmap arrays.

C.7 Copy Texture and Subtexture
Texture array data can be speci ed from framebu er memory, as well as
from client memory, and rectangular subregions of texture arrays can be
rede ned either from client or framebu er memory. These additions match
those de ned by the EXT copy texture and EXT subtexture extensions.

C.8 Texture Objects
A set of texture arrays and their related texture state can be treated as a
single object. Such treatment allows for greater implementation e ciency
when multiple arrays are used. In conjunction with the subtexture capabil-
ity, it also allows clients to make gradual changes to existing texture arrays,
rather than completely rede ning them. These additions match those of the
EXT texture object extension, with slight additions to the texture residency
semantics.

C.9 Other Changes
  1. Color indices may now be speci ed as unsigned bytes.




                                Version 1.2.1 - April 1, 1999
228                                             APPENDIX C. VERSION 1.1

  2. Texture coordinates s, t, and r are divided by q during the rasterization
     of points, pixel rectangles, and bitmaps. This division was documented
     only for lines and polygons in the 1.0 version.
  3. The line rasterization algorithm was changed so that vertical lines on
     pixel borders rasterize correctly.
  4. Separate pixel transfer discussions in chapter 3 and chapter 4 were
     combined into a single discussion in chapter 3.
  5. Texture alpha values are returned as 1.0 if there is no alpha channel
     in the texture array. This behavior was unspeci ed in the 1.0 version,
     and was incorrectly documented in the reference manual.
  6. Fog start and end values may now be negative.
  7. Evaluated color values direct the evaluation of the lighting equation if
     ColorMaterial is enabled.
C.10 Acknowledgements
OpenGL 1.1 is the result of the contributions of many people, representing
a cross section of the computer industry. Following is a partial list of the
contributors, including the company that they represented at the time of
their contribution:
    Kurt Akeley, Silicon Graphics
    Bill Armstrong, Evans & Sutherland
    Andy Bigos, 3Dlabs
    Pat Brown, IBM
    Jim Cobb, Evans & Sutherland
    Dick Coulter, Digital Equipment
    Bruce D'Amora, GE Medical Systems
    John Dennis, Digital Equipment
    Fred Fisher, Accel Graphics
    Chris Frazier, Silicon Graphics
    Todd Frazier, Evans & Sutherland
    Tim Freese, NCD
    Ken Garnett, NCD
    Mike Heck, Template Graphics Software
    Dave Higgins, IBM
    Phil Huxley, 3Dlabs




                    Version 1.2.1 - April 1, 1999
C.10. ACKNOWLEDGEMENTS                                    229

  Dale Kirkland, Intergraph
  Hock San Lee, Microsoft
  Kevin LeFebvre, Hewlett Packard
  Jim Miller, IBM
  Tim Misner, SunSoft
  Jeremy Morris, 3Dlabs
  Israel Pinkas, Intel
  Bimal Poddar, IBM
  Lyle Ramshaw, Digital Equipment
  Randi Rost, Hewlett Packard
  John Schimpf, Silicon Graphics
  Mark Segal, Silicon Graphics
  Igor Sinyak, Intel
  Je Stevenson, Hewlett Packard
  Bill Sweeney, SunSoft
  Kelvin Thompson, Portable Graphics
  Neil Trevett, 3Dlabs
  Linas Vepstas, IBM
  Andy Vesper, Digital Equipment
  Henri Warren, Megatek
  Paula Womack, Silicon Graphics
  Mason Woo, Silicon Graphics
  Steve Wright, Microsoft




                          Version 1.2.1 - April 1, 1999
Appendix D
Version 1.2
OpenGL version 1.2, released on March 16, 1998, is the second revision since
the original version 1.0. Version 1.2 is upward compatible with version 1.1,
meaning that any program that runs with a 1.1 GL implementation will also
run unchanged with a 1.2 GL implementation.
    Several additions were made to the GL, especially to texture mapping ca-
pabilities and the pixel processing pipeline. Following are brief descriptions
of each addition.

D.1 Three-Dimensional Texturing
Three-dimensional textures can be de ned and used. In-memory formats
for three-dimensional images, and pixel storage modes to support them, are
also de ned. The additions match those of the EXT texture3D extension.
    One important application of three-dimensional textures is rendering
volumes of image data.

D.2 BGRA Pixel Formats
BGRA  extends the list of host-memory color formats. Speci cally, it pro-
vides a component order matching le and framebu er formats common on
Windows platforms. The additions match those of the EXT bgra extension.

D.3 Packed Pixel Formats
Packed pixels in host memory are represented entirely by one unsigned byte,
one unsigned short, or one unsigned integer. The elds with the packed pixel
                                      230



                    Version 1.2.1 - April 1, 1999
D.4. NORMAL RESCALING                                                    231

are not proper machine types, but the pixel as a whole is. Thus the pixel
storage modes and their unpacking counterparts all work correctly with
packed pixels.
    The additions match those of the EXT packed pixels extension, with the
further addition of reversed component order packed formats.

D.4 Normal Rescaling
Normals may be rescaled by a constant factor derived from the modelview
matrix. Rescaling can operate faster than renormalization in many cases,
while resulting in the same unit normals.
   The additions are based on the EXT rescale normal extension.

D.5 Separate Specular Color
Lighting calculations are modi ed to produce a primary color consisting of
emissive, ambient and di use terms of the usual GL lighting equation, and
a secondary color consisting of the specular term. Only the primary color
is modi ed by the texture environment; the secondary color is added to
the result of texturing to produce a single post-texturing color. This allows
highlights whose color is based on the light source creating them, rather
than surface properties.
    The additions match those of the EXT separate specular color exten-
sion.

D.6 Texture Coordinate Edge Clamping
GL normally clamps such that the texture coordinates are limited to exactly
the range 0; 1 . When a texture coordinate is clamped using this algorithm,
the texture sampling lter straddles the edge of the texture image, taking
half its sample values from within the texture image, and the other half from
the texture border. It is sometimes desirable to clamp a texture without
requiring a border, and without using the constant border color.
    A new texture clamping algorithm, CLAMP TO EDGE, clamps texture coor-
dinates at all mipmap levels such that the texture lter never samples a
border texel. The color returned when clamping is derived only from texels
at the edge of the texture image.
    The additions match those of the SGIS texture edge clamp extension.




                               Version 1.2.1 - April 1, 1999
232                                              APPENDIX D. VERSION 1.2

D.7 Texture Level of Detail Control
Two constraints related to the texture level of detail parameter  are added.
One constraint clamps  to a speci ed oating point range. The other limits
the selection of mipmap image arrays to a subset of the arrays that would
otherwise be considered.
    Together these constraints allow a large texture to be loaded and used
initially at low resolution, and to have its resolution raised gradually as more
resolution is desired or available. Image array speci cation is necessarily in-
tegral, rather than continuous. By providing separate, continuous clamping
of the  parameter, it is possible to avoid "popping" artifacts when higher
resolution images are provided.
    The additions match those of the SGIS texture lod extension.

D.8 Vertex Array Draw Element Range
A new form of DrawElements that provides explicit information on the
range of vertices referred to by the index set is added. Implementations can
take advantage of this additional information to process vertex data without
having to scan the index data to determine which vertices are referenced.
   The additions match those of the EXT draw range elements extension.

D.9 Imaging Subset
The remaining new features are primarily intended for advanced image pro-
cessing applications, and may not be present in all GL implementations.
The are collectively referred to as the imaging subset.

D.9.1 Color Tables
A new RGBA-format color lookup mechanism is de ned in the pixel trans-
fer process, providing additional lookup capabilities beyond the existing
lookup. The key di erence is that the new lookup tables are treated as
one-dimensional images with internal formats, like texture images and con-
volution lter images. Thus the new tables can operate on a subset of the
components of passing pixel groups. For example, a table with internal for-
mat ALPHA modi es only the A component of each pixel group, leaving the
R, G, and B components unmodi ed.




                     Version 1.2.1 - April 1, 1999
D.9. IMAGING SUBSET                                                        233

    Three independent lookups may be performed: prior to convolution;
after convolution and prior to color matrix transformation; after color matrix
transformation and prior to gathering pipeline statistics.
    Methods to initialize the color lookup tables from the framebu er, in
addition to the standard memory source mechanisms, are provided.
    Portions of a color lookup table may be rede ned without reinitializing
the entire table. The a ected portions may be speci ed either from host
memory or from the framebu er.
    The additions match those of the EXT color table and
EXT color subtable extensions.


D.9.2 Convolution
One- or two-dimensional convolution operations are executed following the
  rst color table lookup in the pixel transfer process. The convolution kernels
are themselves treated as one- and two-dimensional images, which can be
loaded from application memory or from the framebu er.
     The convolution framework is designed to accommodate three-
dimensional convolution, but that API is left for a future extension.
     The additions match those of the EXT convolution and
HP convolution border modes extensions.


D.9.3 Color Matrix
A 4x4 matrix transformation and associated matrix stack are added to the
pixel transfer path. The matrix operates on RGBA pixel groups, using the
equation
                                  C 0 = MC;
where                              0R1
                                   B G CC
                                 C=B
                                   @ A   B
                                         A
    and M is the 4  4 matrix on the top of the color matrix stack. After the
matrix multiplication, each resulting color component is scaled and biased
by a programmed amount. Color matrix multiplication follows convolution.
    The color matrix can be used to reassign and duplicate color components.
It can also be used to implement simple color space conversions.
    The additions match those of the SGI color matrix extension.




                                Version 1.2.1 - April 1, 1999
234                                             APPENDIX D. VERSION 1.2

D.9.4 Pixel Pipeline Statistics
Pixel operations that count occurences of speci c color component values
histogram and that track the minimum and maximum color component
values minmax are performed at the end of the pixel transfer pipeline. An
optional mode allows pixel data to be discarded after the histogram and or
minmax operations are completed. Otherwise the pixel data continues on
to the next operation una ected.
    The additions match those of the EXT histogram extension.

D.9.5 Constant Blend Color
A constant color that can be used to de ne blend weighting factors may be
de ned. A typical usage is blending two RGB images. Without the constant
blend factor, one image must have an alpha channel with each pixel set to
the desired blend factor.
   The additions match those of the EXT blend color extension.

D.9.6 New Blending Equations
Blending equations other than the normal weighted sum of source and des-
tination components may be used.
    Two of the new equations produce the minimum or maximum color
components of the source and destination colors. Taking the maximum is
useful for applications such as maximum projection in medical imaging.
    The other two equations are similar to the default blending equation,
but produce the di erence of its left and right hand sides, rather than the
sum. Image di erences are useful in many image processing applications.
    The additions match those of the EXT blend minmax and
EXT blend subtract extensions.



D.10 Acknowledgements
OpenGL 1.2 is the result of the contributions of many people, representing
a cross section of the computer industry. Following is a partial list of the
contributors, including the company that they represented at the time of
their contribution:
    Kurt Akeley, Silicon Graphics
    Bill Armstrong, Evans & Sutherland
    Otto Berkes, Microsoft




                    Version 1.2.1 - April 1, 1999
D.10. ACKNOWLEDGEMENTS                                    235

  Pierre-Luc Bisaillon, Matrox Graphics
  Drew Bliss, Microsoft
  David Blythe, Silicon Graphics
  Jon Brewster, Hewlett Packard
  Dan Brokenshire, IBM
  Pat Brown, IBM
  Newton Cheung, S3
  Bill Cli ord, Digital
  Jim Cobb, Parametric Technology
  Bruce D'Amora, IBM
  Kevin Dallas, Microsoft
  Mahesh Dandapani, Rendition
  Daniel Daum, AccelGraphics
  Suzy De eyes, IBM
  Peter Doyle, Intel
  Jay Duluk, Raycer
  Craig Dunwoody, Silicon Graphics
  Dave Erb, IBM
  Fred Fisher, AccelGraphics Dynamic Pictures
  Celeste Fowler, Silicon Graphics
  Allen Gallotta, ATI
  Ken Garnett, NCD
  Michael Gold, Nvidia Silicon Graphics
  Craig Groeschel, Metro Link
  Jan Hardenbergh, Mitsubishi Electric
  Mike Heck, Template Graphics Software
  Dick Hessel, Raycer Graphics
  Paul Ho, Silicon Graphics
  Shawn Hopwood, Silicon Graphics
  Jim Hurley, Intel
  Phil Huxley, 3Dlabs
  Dick Jay, Template Graphics Software
  Paul Jensen, 3Dfx
  Brett Johnson, Hewlett Packard
  Michael Jones, Silicon Graphics
  Tim Kelley, Real3D
  Jon Khazam, Intel
  Louis Khouw, Sun
  Dale Kirkland, Intergraph
  Chris Kitrick, Raycer




                          Version 1.2.1 - April 1, 1999
236                                               APPENDIX D. VERSION 1.2

      Don Kuo, S3
      Herb Kuta, Quantum 3D
      Phil Lacroute, Silicon Graphics
      Prakash Ladia, S3
      Jon Leech, Silicon Graphics
      Kevin Lefebvre, Hewlett Packard
      David Ligon, Raycer Graphics
      Kent Lin, S3
      Dan McCabe, S3
      Jack Middleton, Sun
      Tim Misner, Intel
      Bill Mitchell, National Institute of Standards
      Jeremy Morris, 3Dlabs
      Gene Munce, Intel
      William Newhall, Real3D
      Matthew Papakipos, Nvidia Raycer
      Garry Paxinos, Metro Link
      Hanspeter P ster, Mitsubishi Electric
      Richard Pimentel, Parametric Technology
      Bimal Poddar, IBM Intel
      Rob Putney, IBM
      Mike Quinlan, Real3D
      Nate Robins, University of Utah
      Detlef Roettger, Elsa
      Randi Rost, Hewlett Packard
      Kevin Rushforth, Sun
      Richard S. Wright, Real3D
      Hock San Lee, Microsoft
      John Schimpf, Silicon Graphics
      Stefan Seeboth, ELSA
      Mark Segal, Silicon Graphics
      Bob Seitsinger, S3
      Min-Zhi Shao, S3
      Colin Sharp, Rendition
      Igor Sinyak, Intel
      Bill Sweeney, Sun
      William Sweeney, Sun
      Nathan Tuck, Raycer
      Doug Twillenger, Sun
      John Tynefeld, 3dfx




                      Version 1.2.1 - April 1, 1999
D.10. ACKNOWLEDGEMENTS                                   237

  Kartik Venkataraman, Intel
  Andy Vesper, Digital Equipment
  Henri Warren, Digital Equipment Megatek
  Paula Womack, Silicon Graphics
  Steve Wright, Microsoft
  David Yu, Silicon Graphics
  Randy Zhao, S3




                         Version 1.2.1 - April 1, 1999
Appendix E
Version 1.2.1
OpenGL version 1.2.1, released on October 14, 1998, introduced ARB ex-
tensions see Appendix F. The only ARB extension de ned in this version
is multitexture, allowing application of multiple textures to a fragment in
one rendering pass. Multitexture is based on the SGIS multitexture exten-
sion, simpli ed by removing the ability to route texture coordinate sets to
arbitrary texture units.
    A new corollary discussing display list and immediate mode invariance
was added to Appendix B on April 1, 1999.




                                      238



                    Version 1.2.1 - April 1, 1999
Appendix F
ARB Extensions
OpenGL extensions that have been approved by the OpenGL Architectural
Review Board ARB are described in this chapter. These extensions are
not required to be supported by a conformant OpenGL implementation, but
are expected to be widely available; they de ne functionality that is likely
to move into the required feature set in a future revision of the speci cation.
    In order not to compromise the readability of the core speci cation,
ARB extensions are not integrated into the core language; instead, they are
presented in this chapter, as changes to the core.

F.1 Naming Conventions
To distinguish ARB extensions from core OpenGL features and from vendor-
speci c extensions, the following naming conventions are used:

     A unique name string of the form "GL ARB name" is associated with
     each extension. If the extension is supported by an implementation,
     this string will be present in the EXTENSIONS string described in sec-
     tion 6.1.11.
     All functions de ned by the extension will have names of the form
     FunctionARB
     All enumerants de ned by the extension will have names of the form
     NAME ARB.


                                      239



                                Version 1.2.1 - April 1, 1999
240                                     APPENDIX F. ARB EXTENSIONS

F.2 Multitexture
Multitexture adds support for multiple texture units. The capabilities of
the multiple texture units are identical, except that evaluation and feedback
are supported only for texture unit 0. Each texture unit has its own state
vector which includes texture vertex array speci cation, texture image and
  ltering parameters, and texture environment application.
     The texture environments of the texture units are applied in a pipelined
fashion whereby the output of one texture environment is used as the input
fragment color for the next texture environment. Changes to texture client
state and texture server state are each routed through one of two selectors
which control which instance of texture state is a ected.
     The speci cation is written using four texture units though the actual
number supported is implementation dependent and can be larger or smaller
than four.
     The name string for multitexture is GL ARB multitexture.
F.2.1 Dependencies
Multitexture requires features of OpenGL 1.1.
F.2.2 Issues
The extension currently requires a separate texture coordinate input for each
texture unit. Modi cation to allow routing and or broadcasting texcoords
and TexGen output would be useful, possibly as a future extension layered
on multitexture.
F.2.3 Changes to Section 2.6 Begin End Paradigm
Amend paragraphs 2 and 3
    Each vertex is speci ed with two, three, or four coordinates. In addition,
a current normal, multiple current texture coordinate sets, and current color
may be used in processing each vertex. Normals are used by the GL in
lighting calculations; the current normal is a three-dimensional vector that
may be set by sending three coordinates that specify it. Texture coordinates
determine how a texture image is mapped onto a primitive. Multiple sets
of texture coordinates may be used to specify how multiple texture images
are mapped onto a primitive. The number of texture units supported is
implementation dependent but must be at least one. The number of active
textures supported can be queried with the state MAX TEXTURE UNITS ARB.




                    Version 1.2.1 - April 1, 1999
F.2. MULTITEXTURE                                                         241

    Primary and secondary colors are associated with each vertex see sec-
tion 3.9. These associated colors are either based on the current color or
produced by lighting, depending on whether or not lighting is enabled. Tex-
ture coordinates are similarly associated with each vertex. Multiple sets of
texture coordinates may be associated with a vertex. Figure F.1 summa-
rizes the association of auxiliary data with a transformed vertex to produce
a processed vertex.
Amend paragraph 6
    Before colors have been assigned to a vertex, the state required by a
vertex is the vertex's coordinates, the current normal, the current edge ag
see section 2.6.2, the current material properties see section 2.13.2, and
the multiple current texture coordinate sets. Because color assignment is
done vertex-by-vertex, a processed vertex comprises the vertex's coordinates,
its edge ag, its assigned colors, and its multiple texture coordinate sets.
F.2.4 Changes to Section 2.7 Vertex Speci cation
Amend paragraph 2
    Current values are used in associating auxiliary data with a vertex as
described in section 2.6. A current value may be changed at any time by
issuing an appropriate command. The commands
     void   TexCoordf1234gfsifdg T coords ;
     void   TexCoordf1234gfsifdgv T coords ;
specify the current homogeneous texture coordinates, named s, t, r, and q.
The TexCoord1 family of commands set the s coordinate to the provided
single argument while setting t and r to 0 and q to 1. Similarly, TexCoord2
sets s and t to the speci ed values, r to 0 and q to 1; TexCoord3 sets s, t,
and r, with q set to 1, and TexCoord4 sets all four texture coordinates.
    Implementations may support more than one texture unit, and thus more
than one set of texture coordinates. The commands
     void   MultiTexCoordf1234gfsifdgARBenum texture,T
         coords
     void   MultiTexCoordf1234gfsifdgvARBenum texture,T
         coords
take the coordinate set to be modi ed as the texture parameter. texture
is a symbolic constant of the form TEXTUREi ARB, indicating that texture
coordinate set i is to be modi ed. The constants obey TEXTUREi ARB =




                               Version 1.2.1 - April 1, 1999
242                                               APPENDIX F. ARB EXTENSIONS


                  Vertex
               Coordinates In


                                    vertex / normal          Transformed
                                    transformation
                                                             Coordinates
        Current
        Normal
                                                                              Processed
                                                                                Vertex
                                                                                 Out

        Current                               lighting        Associated
       Color and                                                 Data
       Materials                                             (Colors, Edge Flag,
                                                                and Texture
                                                                Coordinates)
       Current
      Edge Flag


       Current
       Texture                                    texture
                           texgen
                                                  matrix 1
      Coord Set 1




       Current
       Texture             texgen                 texture
                                                  matrix 2
      Coord Set 2




       Current
       Texture             texgen                 texture
                                                  matrix 3
      Coord Set 3




       Current
       Texture             texgen                 texture
                                                  matrix 4
      Coord Set 4



  Figure F.1. Association of current values with a vertex. The heavy lined
  boxes represent GL state. Four texture units are shown; however, multitex-
  turing may support a di erent number of units depending on the implemen-
  tation.




                        Version 1.2.1 - April 1, 1999
F.2. MULTITEXTURE                                                         243

TEXTURE0 ARB + i i is in the range 0 to k , 1, where k is the implementation-
dependent number of texture units de ned by MAX TEXTURE UNITS ARB.
   The TexCoord commands are exactly equivalent to the corresponding
MultiTexCoordARB commands with texture set to TEXTURE0 ARB.
   Gets of CURRENT TEXTURE COORDS return the texture coordinate set de ned
by the value of ACTIVE TEXTURE ARB.
   Specifying an invalid texture coordinate set for the texture argument of
MultiTexCoordARB results in unde ned behavior.
F.2.5 Changes to Section 2.8 Vertex Arrays
Amend paragraph 1
    The vertex speci cation commands described in section 2.7 accept data
in almost any format, but their use requires many command executions to
specify even simple geometry. Vertex data may also be placed into arrays
that are stored in the client's address space. Blocks of data in these arrays
may then be used to specify multiple geometric primitives through the ex-
ecution of a single GL command. The client may specify up to 5 plus the
value of MAX TEXTURE UNITS ARB arrays: one each to store vertex coordinates,
edge ags, colors, color indices, normals, and one or more texture coordinate
sets. The commands . . .
Insert between paragraph 2 and 3
    In implementations which support more than one texture unit, the com-
mand
     void   ClientActiveTextureARB enum texture ;
    is used to select the vertex array client state parameters to
be modi ed by the TexCoordPointer command and the array af-
fected by EnableClientState and DisableClientState with parame-
ter TEXTURE COORD ARRAY. This command sets the client state variable
CLIENT ACTIVE TEXTURE ARB. Each texture unit has a client state vector which
is selected when this command is invoked. This state vector includes the
vertex array state. This call also selects which texture units' client state
vector is used for queries of client state.
    Specifying an invalid texture generates the error INVALID ENUM. Valid val-
ues of texture are the same as for the MultiTexCoordARB commands
described in section 2.7.
Amend nal paragraph




                               Version 1.2.1 - April 1, 1999
244                                                 APPENDIX F. ARB EXTENSIONS

    If the number of supported texture units the value of
MAX TEXTURE UNITS ARB   is k, then the client state required to imple-
ment vertex arrays consists of 5 + k boolean values, 5 + k memory pointers,
5 + k integer stride values, 4 + k symbolic constants representing array
types, and 3 + k integers representing values per element. In the initial
state, the boolean values are each disabled, the memory pointers are each
null, the strides are each zero, the array types are each FLOAT, and the
integers representing values per element are each four.

F.2.6 Changes to Section 2.10.2 Matrices
Amend paragraph 8
    For each texture unit, a 4  4 matrix is applied to the corresponding
texture coordinates. This matrix is applied as
                      0 m1 m5 m9 m13 1 0 s 1
                      BB m2 m6 m10 m14 CC BB t CC ;
                       @ m3 m7 m11 m15 A @ r A
                        m4 m8 m12 m16                 q
where the left matrix is the current texture matrix. The matrix is applied
to the coordinates resulting from texture coordinate generation which may
simply be the current texture coordinates, and the resulting transformed co-
ordinates become the texture coordinates associated with a vertex. Setting
the matrix mode to TEXTURE causes the already described matrix operations
to apply to the texture matrix.
    There is also a corresponding texture matrix stack for each texture unit.
To change the stack a ected by matrix operations, set the active texture
unit selector by calling
      void   ActiveTextureARB enum texture ;
The selector also a ects calls modifying texture environment state, texture
coordinate generation state, texture binding state, and queries of all these
state values as well as current texture coordinates and current raster texture
coordinates.
    Specifying an invalid texture generates the error INVALID ENUM. Valid val-
ues of texture are the same as for the MultiTexCoordARB commands
described in section 2.7.
    The active texture unit selector may be queried by calling GetIntegerv
with pname set to ACTIVE TEXTURE ARB.




                    Version 1.2.1 - April 1, 1999
F.2. MULTITEXTURE                                                          245

    There is a stack of matrices for each of matrix modes MODELVIEW,
PROJECTION  , and COLOR, and for each texture unit. For MODELVIEW mode,
the stack depth is at least 32 that is, there is a stack of at least 32 model-
view matrices. For the other modes, the depth is at least 2. Texture matrix
stacks for all texture units have the same depth. The current matrix in any
mode is the matrix on the top of the stack for that mode.
      void PushMatrix void ;

pushes the stack down by one, duplicating the current matrix in both the
top of the stack and the entry below it.
      void PopMatrix void ;

pops the top entry o of the stack, replacing the current matrix with the
matrix that was the second entry in the stack. The pushing or popping takes
place on the stack corresponding to the current matrix mode. Popping a
matrix o a stack with only one entry generates the error STACK UNDERFLOW;
pushing a matrix onto a full stack generates STACK OVERFLOW.
    When the current matrix mode is TEXTURE, the texture matrix stack of
the active texture unit is pushed or popped.
    The state required to implement transformations consists of a four-
valued integer indicating the current matrix mode, one stack of at least
two 4  4 matrices for each of COLOR, PROJECTION, each texture unit, TEXTURE,
and a stack of at least 32 4  4 matrices for MODELVIEW. Each matrix stack
has an associated stack pointer. Initially, there is only one matrix on each
stack, and all matrices are set to the identity. The initial matrix mode is
MODELVIEW. The initial value of ACTIVE TEXTURE ARB is TEXTURE0 ARB.


F.2.7 Changes to Section 2.10.4 Generating Texture Coor-
      dinates
Amend paragraph 4
    The state required for texture coordinate generation for each texture
unit comprises a three-valued integer for each coordinate indicating coor-
dinate generation mode, and a bit for each coordinate to indicate whether
texture coordinate generation is enabled or disabled. In addition, four co-
e cients are required for the four coordinates for each of EYE LINEAR and
OBJECT LINEAR. The initial state has the texture generation function dis-
abled for all texture coordinates. The initial values of pi for s are all 0
except p1 which is one; for t all the pi are zero except p2 , which is 1.
The values of pi for r and q are all 0. These values of pi apply for both




                                Version 1.2.1 - April 1, 1999
246                                      APPENDIX F. ARB EXTENSIONS

the EYE LINEAR and OBJECT LINEAR versions. Initially all texture generation
modes are EYE LINEAR.
    For implementations which support more than one texture unit, there is
texture coordinate generation state for each unit. The texture coordinate
generation state which is a ected by the TexGen, Enable, and Disable
operations is set with ActiveTextureARB.
F.2.8 Changes to Section 2.12 Current Raster Position
Amend paragraph 2
    The state required for the current raster position consists of three window
coordinates xw , yw , and zw , a clip coordinate wc value, an eye coordinate
distance, a valid bit, and associated data consisting of a color and multiple
texture coordinate sets. It is set using one of the RasterPos commands:
         RasterPosf234gfsifdg T coords ;
      void
         RasterPosf234gfsifdgv T coords ;
      void

RasterPos4 takes four values indicating x, y, z, and w. RasterPos3 or
RasterPos2 is analogous, but sets only x, y, and z with w implicitly set
to 1 or only x and y with z implicitly set to 0 and w implicitly set to 1.
    Gets of CURRENT RASTER TEXTURE COORDS are a ected by the setting of the
state ACTIVE TEXTURE ARB.
Modify gure 2.7
Amend paragraph 5
    The current raster position requires ve single-precision oating-point
values for its xw , yw , and zw window coordinates, its wc clip coordinate,
and its eye coordinate distance, a single valid bit, a color RGBA and color
index, and texture coordinates for each texture unit. In the initial state,
the coordinates and texture coordinates are all 0; 0; 0; 1, the eye coordinate
distance is 0, the valid bit is set, the associated RGBA color is 1; 1; 1; 1
and the associated color index color is 1. In RGBA mode, the associated
color index always has its initial value; in color index mode, the RGBA color
always maintains its initial value.
F.2.9 Changes to Section 3.8 Texturing
Amend paragraphs 1 and 2
    Texturing maps a portion of one or more speci ed images onto each
primitive for which texturing is enabled. This mapping is accomplished by
using the color of an image at the location indicated by a fragment's s; t; r




                     Version 1.2.1 - April 1, 1999
F.2. MULTITEXTURE                                                                     247




                                                            Valid
   Rasterpos In                Clip         Project
                                                                 Raster
                         Vertex/Normal                          Position
     Current             Transformation
     Normal

                                                                 Raster
    Current                      Lighting                       Distance
    Color &
    Materials
                                                            Associated
                                              Texture          Data
    Current               Texgen              Matrix 0
    Texture                                                                Current
   Coord Set 0                                                              Raster
                                                                           Position
                                              Texture
    Current               Texgen              Matrix 1
    Texture
   Coord Set 1

                                              Texture
    Current               Texgen              Matrix 2
    Texture
   Coord Set 2

                                              Texture
    Current               Texgen              Matrix 3
    Texture
   Coord Set 3



 Figure F.2. The current raster position and how it is set. Four texture units
 are shown; however, multitexturing may support a di erent number of units
 depending on the implementation.




                                Version 1.2.1 - April 1, 1999
248                                     APPENDIX F. ARB EXTENSIONS

coordinates to modify the fragment's primary RGBA color. Texturing does
not a ect the secondary color.
     An implementation may support texturing using more than one image at
a time. In this case the fragment carries multiple sets of texture coordinates
s; t; r which are used to index separate images to produce color values
which are collectively used to modify the fragment's RGBA color. Texturing
is speci ed only for RGBA mode; its use in color index mode is unde ned.
The following subsections up to and including Section 3.8.5 specify the
GL operation with a single texture and Section 3.8.10 speci es the details
of how multiple texture units interact.

F.2.10 Changes to Section 3.8.5 Texture Mini cation
Amend second paragraph under the Mipmapping subheading
    Each array in a mipmap is de ned using TexImage3D, TexImage2D,
CopyTexImage2D, TexImage1D, or CopyTexImage1D; the array be-
ing set is indicated with the level-of-detail argument level. Level-of-detail
numbers proceed from TEXTURE BASE LEVEL for the original texture array
through p = maxfn; m; lg + TEXTURE BASE LEVEL with each unit increase in-
dicating an array of half the dimensions of the previous one as already de-
scribed. If texturing is enabled and TEXTURE MIN FILTER is one that requires
a mipmap at the time a primitive is rasterized and if the set of arrays
TEXTURE BASE LEVEL through q = minfp; TEXTURE MAX LEVELg is incomplete,
then it is as if texture mapping were disabled for that texture unit. The set
of arrays TEXTURE BASE LEVEL through q is incomplete if the internal formats
of all the mipmap arrays were not speci ed with the same symbolic constant,
if the border widths of the mipmap arrays are not the same, if the dimen-
sions of the mipmap arrays do not follow the sequence described above,
if TEXTURE MAX LEVEL TEXTURE BASE LEVEL, or if TEXTURE BASE LEVEL p.
Array levels k where k TEXTURE BASE LEVEL or k q are insigni cant.

F.2.11 Changes to Section 3.8.8 Texture Objects
Insert following the last paragraph
    The texture object name space, including the initial one-, two-, and
three-dimensional texture objects, is shared among all texture units. A
texture object may be bound to more than one texture unit simultaneously.
After a texture object is bound, any GL operations on that target object
a ect any other texture units to which the same texture object is bound.
    Texture binding is a ected by the setting of the state ACTIVE TEXTURE ARB.




                    Version 1.2.1 - April 1, 1999
F.2. MULTITEXTURE                                                             249

    If a texture object is deleted, it as if all texture units which are bound
to that texture object are rebound to texture object zero.

F.2.12 Changes to Section 3.8.10 Texture Application
Amend second paragraph
    Each texture unit is enabled and bound to texture objects independently
from the other texture units. Each texture unit follows the precendence
rules for one-, two-, and three-dimensional textures. Thus texture units can
be performing texture mapping of di erent dimensionalities simultaneously.
Each unit has its own enable and binding states.
    Each texture unit is paired with an environment function, as shown
in gure F.3. The second texture function is computed using the texture
value from the second texture, the fragment resulting from the rst texture
function computation and the second texture unit's environment function.
If there is a third texture, the fragment resulting from the second texture
function is combined with the third texture value using the third texture
unit's environment function and so on. The texture unit selected by Ac-
tiveTextureARB determines which texture unit's environment is modi ed
by TexEnv calls.
    Texturing is enabled and disabled individually for each texture unit. If
texturing is disabled for one of the units, then the fragment resulting from
the previous unit, is passed unaltered to the following unit.
    The required state, per texture unit, is three bits indicating whether
each of one-, two-, or three-dimensional texturing is enabled or disabled. In
the intial state, all texturing is disabled for all texture units.

F.2.13 Changes to Section 5.1 Evaluators
Amend paragraph 7
    The evaluation of a de ned map is enabled or disabled with Enable and
Disable using the constant corresponding to the map as described above.
The evaluator map generates only coordinates for texture unit TEXTURE0 ARB.
The error INVALID VALUE results if either ustride or vstride is less than k, or
if u1 is equal to u2, or if v1 is equal to v2 . If the value of ACTIVE TEXTURE ARB
is not TEXTURE0 ARB, calling Map 12 generates the error INVALID OPERATION.

F.2.14 Changes to Section 5.3 Feedback
Amend paragraph 4




                                 Version 1.2.1 - April 1, 1999
250                                        APPENDIX F. ARB EXTENSIONS




      Cf

                 TE0
      CT0                        TE1
      CT1                                         TE2
      CT2                                                    TE3          C’f
      CT3

            Cf   = fragment color input to texturing

            C’f = fragment color output from texturing

            CTi = texture color from texture lookup i

            TEi = texture environment i


  Figure F.3. Multitexture pipeline. Four texture units are shown; however,
  multitexturing may support a di erent number of units depending on the
  implementation. The input fragment color is successively combined with each
  texture according to the state of the corresponding texture environment, and
  the resulting fragment color passed as input to the next texture unit in the
  pipeline.




                       Version 1.2.1 - April 1, 1999
F.2. MULTITEXTURE                                                           251

    The texture coordinates and colors returned are those resulting from the
clipping operations described in Section 2.13.8. Only coordinates for tex-
ture unit TEXTURE0 ARB are returned even for implementations which support
multiple texture units. The colors returned are the primary colors.




F.2.15 Changes to Section 6.1.2 Data Conversions
Insert following the last paragraph
    Most texture state variables are quali ed by the
value of ACTIVE TEXTURE ARB to determine which server texture state vector
is queried. Client texture state variables such as texture coordinate array
pointers are quali ed by the value of CLIENT ACTIVE TEXTURE ARB. Tables 6.5,
6.6, 6.7, 6.12, 6.14, and 6.25 indicate those state variables which are quali ed
by ACTIVE TEXTURE ARB or CLIENT ACTIVE TEXTURE ARB during state queries.




F.2.16 Changes to Section 6.1.12 Saving and Restoring
       State
Insert following paragraph 3
    Operations on groups containing replicated texture state push or pop
texture state within that group for all texture units. When state for a
group is pushed, all state corresponding to TEXTURE0 ARB is pushed rst,
followed by state corresponding to TEXTURE1 ARB, and so on up to and in-
cluding the state corresponding to TEXTUREk ARB where k + 1 is the value of
MAX TEXTURE UNITS ARB. When state for a group is popped, the replicated tex-
ture state is restored in the opposite order that it was pushed, starting with
state corresponding to TEXTUREk ARB and ending with TEXTURE0 ARB. Identical
rules are observed for client texture state push and pop operations. Matrix
stacks are never pushed or popped with PushAttrib, PushClientAttrib,
PopAttrib, or PopClientAttrib.




                                Version 1.2.1 - April 1, 1999
                                                                                                                                                                                  252




                                                                                                                 Get        Initial
                                                                              Get value               Type       Cmnd       Value         Description       Sec.    Attribute
                                                                     Modi ed state in table 6.5
                                                                         CURRENT TEXTURE COORDS      1  T   GetFloatv     0,0,0,1 Current texture         2.7      current
                                                                                                                                    coordinates
                                                                     CURRENT RASTER TEXTURE COORDS   1  T   GetFloatv     0,0,0,1 Texture coordinates     2.12     current
                                                                                                                                    associated with
                                                                                                                                    raster position
                                                                     Modi ed state in table 6.6
                                                                          TEXTURE COORD ARRAY        1  B    IsEnabled    False     Texture coordinate    2.8    vertex-array
                                                                                                                                      array enable
                                                                        TEXTURE COORD ARRAY SIZE     1  Z + GetIntegerv     4       Coordinates per       2.8    vertex-array




Version 1.2.1 - April 1, 1999
                                                                                                                                      element
                                                                        TEXTURE COORD ARRAY TYPE     1  Z4 GetIntegerv    FLOAT     Type of texture       2.8    vertex-array
                                                                                                                                      coordinates
                                                                       TEXTURE COORD ARRAY STRIDE    1  Z + GetIntegerv     0       Stride between        2.8    vertex-array




                                Table F.1. Changes to State Tables
                                                                                                                                      texture coordinates
                                                                      TEXTURE COORD ARRAY POINTER    1  Y   GetPointerv     0       Pointer to the        2.8    vertex-array
                                                                                                                                      texture coordinate
                                                                                                                                      array
                                                                                                                                                                                  APPENDIX F. ARB EXTENSIONS
                                                                                                                       Get          Initial
                                                                                 Get value               Type          Cmnd         Value          Description          Sec.     Attribute
                                                                             Modi ed state in table 6.7
                                                                               TEXTURE MATRIX       1  2  M 4    GetFloatv     Identity    Texture matrix stack 2.10.2
                                                                             TEXTURE STACK DEPTH       1  Z +     GetIntegerv       1        Texture matrix stack 2.10.2
                                                                                                                                               pointer
                                                                             Modi ed state in table 6.12
                                                                                 TEXTURE xD          1  3  B      IsEnabled      False      True if xD texturing 3.8.10 texture enable
                                                                                                                                               is enabled; x is 1, 2,
                                                                                                                                                                                               F.2. MULTITEXTURE




                                                                                                                                               or 3
                                                                              TEXTURE BINDING xD    1  3  Z +    GetIntegerv       0        Texture object         3.8.8    texture
                                                                                                                                               bound to TEXTURE xD
                                                                             Modi ed state in table 6.14
                                                                              TEXTURE ENV MODE         1  Z4      GetTexEnviv   MODULATE     Texture application     3.8.9      texture
                                                                                                                                               function
                                                                              TEXTURE ENV COLOR        1  C       GetTexEnvfv    0,0,0,0     Texture environment     3.8.9      texture
                                                                                                                                               color
                                                                                TEXTURE GEN x        1  4  B      IsEnabled      False      Texgen enabled x is    2.10.4 texture enable
                                                                                                                                               S, T, R, or Q
                                                                                  EYE PLANE         1  4  R 4    GetTexGenfv see 2.10.4     Texgen plane            2.10.4     texture




Version 1.2.1 - April 1, 1999
                                                                                                                                               equation coe cients
                                                                                                                                               for S, T, R, and Q




                                Table F.2. Changes to State Tables cont.
                                                                                 OBJECT PLANE       1  4  R 4    GetTexGenfv see 2.10.4     Texgen object linear    2.10.4     texture
                                                                                                                                               coe cients for S, T,
                                                                                                                                               R, and Q
                                                                               TEXTURE GEN MODE     1  4  Z3     GetTexGeniv   EYE LINEAR   Function used for       2.10.4     texture
                                                                                                                                               texgen for S, T, R,
                                                                                                                                                                                               253




                                                                                                                                               and Q
                                                                                                                                                                                             254




                                                                                                                        Get           Initial
                                                                                         Get value            Type      Cmnd          Value            Description        Sec.   Attribute
                                                                                  Added to table 6.6
                                                                                  CLIENT ACTIVE TEXTURE ARB   Z1    GetIntegerv   TEXTURE0 ARB   Client active texture   2.7 vertex-array
                                                                                                                                                  unit selector
                                                                                  Added to table 6.14




Version 1.2.1 - April 1, 1999
                                                                                     ACTIVE TEXTURE ARB       Z1    GetIntegerv   TEXTURE0 ARB   Active texture unit     2.7     texture
                                                                                                                                                  selector




                                Table F.3. New State Introduced by Multitexture
                                                                                                                                                                                             APPENDIX F. ARB EXTENSIONS
                                                                                                                                                                                                           F.2. MULTITEXTURE




                                                                                                                                               Get       Minimum
                                                                                                                      Get value     Type       Cmnd      Value         Description        Sec. Attribute
                                                                                                            Added to table 6.25
                                                                                                            MAX TEXTURE UNITS ARB   Z+     GetIntegerv      1      Number of texture      2.6
                                                                                                                                                                   units not to exceed
                                                                                                                                                                   32




Version 1.2.1 - April 1, 1999
                                                                                                                                                                                                           255




                                Table F.4. New Implementation-Dependent Values Introduced by Multitexture
Index of OpenGL Commands
x BIAS, 78, 208                               AlphaFunc, 143
x SCALE, 78, 208                              ALWAYS, 143 145, 205
2D, 174, 176, 217                             AMBIENT, 50, 51
2 BYTES, 177                                  AMBIENT AND DIFFUSE, 50, 51,
3D, 174, 176                                          53
3D COLOR, 174, 176                            AND, 151
3D COLOR TEXTURE, 174, 176                    AND INVERTED, 151
3 BYTES, 177                                  AND REVERSE, 151
4D COLOR TEXTURE, 174, 176                    AreTexturesResident, 134, 178
4 BYTES, 177                                  ArrayElement, 19, 23, 24, 175
                                              AUTO NORMAL, 167
1, 113, 120, 131, 136, 137, 185, 202,         AUXi, 151, 152
          253                                 AUXn, 151, 158
2, 113, 120, 136, 137, 185, 202, 253          AUX0, 151, 158
3, 113, 120, 136, 137, 185, 202, 253
4, 113, 120, 136, 137, 185                    BACK, 49, 51, 52, 70, 73, 151, 152,
                                                       158, 159, 183, 201
ACCUM, 155                                    BACK LEFT, 151, 152, 158
Accum, 155, 156                               BACK RIGHT, 151, 152, 158
ACCUM BUFFER BIT, 154, 191                    Begin, 12, 15 20, 23, 24, 28, 55, 62,
ACTIVE TEXTURE ARB, 243 246,                           67, 70, 73, 168, 169, 174
        248, 249, 251                         BGR, 92, 159, 162
ActiveTextureARB, 244, 246, 249               BGRA, 92, 94, 98, 159, 230
ADD, 155, 156                                 BindTexture, 133
ALL ATTRIB BITS, 191                          BITMAP, 72, 80, 83, 90, 91, 98, 110,
ALL CLIENT ATTRIB BITS, 191                            160, 185
ALPHA, 78, 92, 103, 104, 114, 115,            Bitmap, 110
        136, 137, 159, 160, 185, 208,         BITMAP TOKEN, 176
        210, 216, 226, 232                    BLEND, 135, 137, 146, 150
ALPHA12, 115                                  BlendColor, 77, 146
ALPHA16, 115                                  BlendEquation, 77, 146, 147
ALPHA4, 115                                   BlendFunc, 77, 146, 147, 149
ALPHA8, 115                                   BLUE, 78, 92, 159, 160, 208, 210, 216
ALPHA BIAS, 101                               BLUE BIAS, 101
ALPHA SCALE, 101                              BLUE SCALE, 101
ALPHA TEST, 143                               BYTE, 22, 91, 160, 161, 177

                                        256



                     Version 1.2.1 - April 1, 1999
INDEX                                                                         257

C3F V3F, 25, 26                               COLOR TABLE BIAS, 80, 81, 186
C4F N3F V3F, 25, 26                           COLOR TABLE BLUE SIZE, 186
C4UB V2F, 25, 26                              COLOR TABLE FORMAT, 186
C4UB V3F, 25, 26                              COLOR TABLE GREEN SIZE, 186
CallList, 19, 177, 178                        COLOR TABLE INTENSITY
CallLists, 19, 177, 178                                SIZE, 186
CCW, 48, 201                                  COLOR TABLE LUMINANCE
CLAMP, 124, 127                                        SIZE, 186
CLAMP TO EDGE, 124, 125, 127,                 COLOR TABLE RED SIZE, 186
          231                                 COLOR TABLE SCALE, 80, 81, 186
CLEAR, 151                                    COLOR TABLE WIDTH, 186
Clear, 153, 154                               ColorMask, 152, 153
ClearAccum, 154                               ColorMaterial, 51 53, 167, 223, 228
ClearColor, 154                               ColorPointer, 19, 21, 22, 27, 178
ClearDepth, 154                               ColorSubTable, 81, 82
ClearIndex, 154                               ColorTable, 79, 81 83, 108, 109, 179
ClearStencil, 154                             ColorTableParameter, 80
CLIENT ACTIVE TEXTURE                         ColorTableParameterfv, 80
          ARB, 243, 251                       Colorub, 56
CLIENT PIXEL STORE BIT, 191                   Colorui, 56
CLIENT VERTEX ARRAY BIT,                      Colorus, 56
          191                                 COMPILE, 175, 223
ClientActiveTextureARB, 243                   COMPILE AND EXECUTE, 175,
CLIP PLANEi, 39                                        177, 178
CLIP PLANE0, 39                               CONSTANT ALPHA, 77, 148, 149
ClipPlane, 38                                 CONSTANT ATTENUATION, 50
COEFF, 184                                    CONSTANT BORDER, 105, 106
COLOR, 31, 34, 81, 85, 86, 120, 162,          CONSTANT COLOR, 77, 148, 149
          245                                 CONVOLUTION 1D, 84, 86, 103,
Color, 19 21, 43, 56                                   117, 186, 187
Color3, 20                                    CONVOLUTION 2D, 83 85, 103,
Color4, 20                                             117, 186, 187
COLOR ARRAY, 23, 27                           CONVOLUTION BORDER
COLOR ARRAY POINTER, 189                               COLOR, 106, 187
COLOR BUFFER BIT, 153, 191                    CONVOLUTION BORDER
COLOR INDEX, 72, 80, 83, 90, 92,                       MODE, 105, 187
          102, 110, 159, 162, 184, 185        CONVOLUTION FILTER BIAS,
COLOR INDEXES, 50, 54                                  83 85, 187
COLOR LOGIC OP, 150                           CONVOLUTION FILTER SCALE,
COLOR MATERIAL, 51, 53                                 83 86, 187
COLOR MATRIX, 185                             CONVOLUTION FORMAT, 187
COLOR MATRIX STACK DEPTH,                     CONVOLUTION HEIGHT, 187
          185                                 CONVOLUTION WIDTH, 187
COLOR TABLE, 80, 82, 103                      ConvolutionFilter1D, 84 86
COLOR TABLE ALPHA SIZE, 186                   ConvolutionFilter2D, 83 86




                                  Version 1.2.1 - April 1, 1999
258                                                                         INDEX

ConvolutionParameter, 84, 105                 Disable, 35, 38, 39, 44, 51, 60, 64,
ConvolutionParameterfv, 83, 84, 106                    67, 70, 72, 74, 108, 109, 138,
ConvolutionParameteriv, 85, 106                        143 146, 149, 150, 166, 167,
COPY, 150, 151, 205                                    246, 249
COPY INVERTED, 151                            DisableClientState, 19, 23, 27, 178,
COPY PIXEL TOKEN, 176                                  243
CopyColorSubTable, 81, 82                     DITHER, 150
CopyColorTable, 81, 82                        DOMAIN, 184
CopyConvolutionFilter1D, 85                   DONT CARE, 180, 213
CopyConvolutionFilter2D, 85                   DOUBLE, 22
CopyPixels, 75, 78, 81, 85, 86, 103,          DRAW PIXEL TOKEN, 176
         120, 156, 162, 163, 173              DrawArrays, 23, 24, 175
CopyTexImage1D, 103, 120, 121, 129,           DrawBu er, 151, 152
         248                                  DrawElements, 24, 25, 175, 232
CopyTexImage2D, 103, 118, 120, 121,           DrawPixels, 72, 75, 76, 78, 80, 83, 89
         129, 248                                      93, 98, 100, 103, 110, 112,
CopyTexImage3D, 121                                    113, 156, 158, 160, 162, 173
CopyTexSubImage1D, 103, 121, 123              DrawRangeElements, 25, 215
CopyTexSubImage2D, 103, 121, 122              DST ALPHA, 148
CopyTexSubImage3D, 103, 121, 122              DST COLOR, 148
CULL FACE, 70
CullFace, 70                                  EDGE FLAG ARRAY, 23, 27
CURRENT BIT, 191                              EDGE FLAG ARRAY POINTER,
CURRENT RASTER                                         189
         TEXTURE COORDS, 222,                 EdgeFlag, 18, 19
         246                                  EdgeFlagPointer, 19, 21, 22, 178
CURRENT TEXTURE COORDS,                       EdgeFlagv, 18
         243                                  EMISSION, 50, 51
CW, 48                                        Enable, 35, 38, 39, 44, 51, 60, 64,
                                                       67, 70, 72, 74, 108, 109, 138,
DECAL, 135, 137                                        143 146, 149, 150, 166, 167,
DECR, 144                                              181, 246, 249
DeleteLists, 178                              ENABLE BIT, 191
DeleteTextures, 133, 178                      EnableClientState, 19, 23, 27, 178,
DEPTH, 162, 208                                        243
DEPTH BIAS, 78, 101                           End, 12, 15 20, 23, 24, 28, 55, 62, 70,
DEPTH BUFFER BIT, 153, 191                             73, 168, 169, 174
DEPTH COMPONENT, 80, 83, 90,                  EndList, 175, 177
         92, 112, 158, 159, 162, 184          EQUAL, 143 145
DEPTH SCALE, 78, 101                          EQUIV, 151
DEPTH TEST, 145                               EVAL BIT, 191
DepthFunc, 145                                EvalCoord, 19, 167
DepthMask, 153                                EvalCoord1, 167 169
DepthRange, 30, 182, 224                      EvalCoord1d, 168
DIFFUSE, 50, 51                               EvalCoord1f, 168




                     Version 1.2.1 - April 1, 1999
INDEX                                                                         259

EvalCoord2, 167, 169, 170                    FLOAT, 22, 26, 27, 91, 160, 161, 177,
EvalMesh1, 168                                        196, 244, 252
EvalMesh2, 168, 169                          Flush, 178, 179, 222
EvalPoint, 19                                FOG, 138
EvalPoint1, 169                              Fog, 139, 140
EvalPoint2, 170                              FOG BIT, 191
EXP, 139, 140, 198                           FOG COLOR, 139
EXP2, 139                                    FOG DENSITY, 139
EXT bgra, 230                                FOG END, 139
EXT blend color, 234                         FOG HINT, 180
EXT blend logic op, 226                      FOG INDEX, 140
EXT blend minmax, 234                        FOG MODE, 139, 140
EXT blend subtract, 234                      FOG START, 139
EXT color subtable, 233                      FRONT, 49, 51, 70, 73, 151, 152, 158,
EXT color table, 233                                  159, 183
EXT convolution, 233                         FRONT AND BACK, 49, 51 53, 70,
EXT copy texture, 227                                 73, 151, 152
EXT draw range elements, 232                 FRONT LEFT, 151, 152, 158
EXT histogram, 234                           FRONT RIGHT, 151, 152, 158
EXT packed pixels, 231                       FrontFace, 48, 70
EXT polygon o set, 226                       Frustum, 32, 33, 223
EXT rescale normal, 231                      FUNC ADD, 147, 149, 205
EXT separate specular color, 231             FUNC REVERSE SUBTRACT, 147
EXT subtexture, 227                          FUNC SUBTRACT, 147
EXT texture, 226, 227                        GenLists, 178
EXT texture3D, 230                           GenTextures, 133, 134, 178, 184
EXT texture object, 227                      GEQUAL, 143 145
EXT vertex array, 225                        Get, 30, 178, 181, 182, 243, 246
EXTENSIONS, 77, 189, 239                     GetBooleanv, 181, 182, 193
EYE LINEAR, 37, 38, 183, 204, 245,           GetClipPlane, 182, 183
        246, 253                             GetColorTable, 83, 158, 185
EYE PLANE, 37                                GetColorTableParameter, 186
                                             GetConvolutionFilter, 158, 186
FALSE, 18, 19, 46 48, 76, 78, 87, 88,        GetConvolutionParameter, 187
         98, 101, 109, 110, 134, 158,        GetConvolutionParameteriv, 83, 84
         182, 184, 187, 188                  GetDoublev, 181, 182, 193
FASTEST, 180                                 GetError, 11
FEEDBACK, 171, 173, 174, 224                 GetFloatv, 181, 182, 185, 193
FEEDBACK BUFFER POINTER,                     GetHistogram, 88, 158, 187
         189                                 GetHistogramParameter, 188
FeedbackBu er, 173, 174, 178                 GetIntegerv, 25, 181, 182, 185, 193,
FILL, 73 75, 169, 201, 223, 226                       244
Finish, 178, 179, 222                        GetLight, 182, 183
FLAT, 54, 223                                GetMap, 183




                                 Version 1.2.1 - April 1, 1999
260                                                                         INDEX

GetMaterial, 182, 183                        INDEX LOGIC OP, 150
GetMinmax, 158, 188                          INDEX OFFSET, 78, 101, 208
GetMinmaxParameter, 188                      INDEX SHIFT, 78, 101, 208
GetPixelMap, 183                             IndexMask, 152, 153
GetPointerv, 189                             IndexPointer, 19, 22, 178
GetPolygonStipple, 185                       InitNames, 171
GetSeparableFilter, 158, 186                 INT, 22, 91, 160, 161, 177
GetString, 189                               INTENSITY, 87, 88, 103, 104, 114,
GetTexEnv, 182, 183                                    115, 136, 137, 185, 208, 226
GetTexGen, 182, 183                          INTENSITY12, 87, 88, 115
GetTexImage, 103, 132, 184, 186 188          INTENSITY16, 87, 88, 115
GetTexImage1D, 158                           INTENSITY4, 87, 88, 115
GetTexImage2D, 158                           INTENSITY8, 87, 88, 115
GetTexImage3D, 158                           InterleavedArrays, 19, 25, 26, 178
GetTexLevelParameter, 182, 183               INVALID ENUM, 12, 13, 38, 49, 77,
GetTexParameter, 182, 183                              83, 87, 88, 90, 120, 132, 184,
GetTexParameterfv, 132, 134                            243, 244
GetTexParameteriv, 132, 134                  INVALID OPERATION, 13, 19, 77,
GL ARB multitexture, 240                               90, 94, 133, 151, 156, 158,
GREATER, 143 145                                       159, 171, 173, 175, 249
GREEN, 78, 92, 159, 160, 208, 210,           INVALID VALUE, 12, 13, 22, 25, 30,
        216                                            33, 49, 60, 64, 76, 78 80, 82
GREEN BIAS, 101                                        84, 87, 113, 114, 116, 121
GREEN SCALE, 101                                       123, 130, 134, 139, 143, 154,
                                                       165, 166, 168, 175, 177, 183,
Hint, 179                                              184, 249
HINT BIT, 191                                INVERT, 144, 151
HISTOGRAM, 87, 88, 109, 187, 188             IsEnabled, 178, 181, 193
Histogram, 87, 88, 109, 179                  IsList, 178
HISTOGRAM ALPHA SIZE, 188                    IsTexture, 178, 184
HISTOGRAM BLUE SIZE, 188
HISTOGRAM FORMAT, 188                        KEEP, 144, 145, 205
HISTOGRAM GREEN SIZE, 188
HISTOGRAM LUMINANCE SIZE,                    LEFT, 151, 152, 158
         188                                 LEQUAL, 143 145
HISTOGRAM RED SIZE, 188                      LESS, 143 145, 205
HISTOGRAM SINK, 188                          Light, 49, 50
HISTOGRAM WIDTH, 188                         LIGHTi, 49, 51, 224
HP convolution border modes, 233             LIGHT0, 49
                                             LIGHT MODEL AMBIENT, 50
INCR, 144                                    LIGHT MODEL COLOR
INDEX, 216                                            CONTROL, 50
Index, 19, 21                                LIGHT MODEL LOCAL VIEWER,
INDEX ARRAY, 23, 27                                   50
INDEX ARRAY POINTER, 189                     LIGHT MODEL TWO SIDE, 50




                    Version 1.2.1 - April 1, 1999
INDEX                                                                   261

LIGHTING, 44                                  Map1, 165, 166, 182
LIGHTING BIT, 191                             MAP1 COLOR 4, 165
LightModel, 49, 50                            MAP1 INDEX, 165
LINE, 73 75, 168, 169, 201, 226               MAP1 NORMAL, 165
LINE BIT, 191                                 MAP1 TEXTURE COORD 1, 165,
LINE LOOP, 15                                          167
LINE RESET TOKEN, 176                         MAP1 TEXTURE COORD 2, 165,
LINE SMOOTH, 64                                        167
LINE SMOOTH HINT, 180                         MAP1 TEXTURE COORD 3, 165
LINE STIPPLE, 67                              MAP1 TEXTURE COORD 4, 165
LINE STRIP, 15, 168                           MAP1 VERTEX 3, 165
LINE TOKEN, 176                               MAP1 VERTEX 4, 165
LINEAR, 124, 127, 130, 131, 139               Map2, 165, 166, 182
LINEAR ATTENUATION, 50                        MAP2 VERTEX 3, 167
LINEAR MIPMAP LINEAR, 124,                    MAP2 VERTEX 4, 167
         129, 130                             Map 12 , 249
LINEAR MIPMAP NEAREST, 124,                   MAP COLOR, 78, 101, 102
         129, 130                             MAP STENCIL, 78, 102
LINES, 16, 67                                 MAP VERTEX 3, 167
LineStipple, 66                               MAP VERTEX 4, 167
LineWidth, 62                                 MapGrid1, 168
LIST BIT, 191                                 MapGrid2, 168
ListBase, 178, 179                            Material, 19, 49, 50, 54, 223
LOAD, 155                                     MatrixMode, 31
LoadIdentity, 31                              MAX, 147
LoadMatrix, 31, 32                            MAX 3D TEXTURE SIZE, 116
LoadName, 171                                 MAX ATTRIB STACK DEPTH,
LOGIC OP, 150                                          190
LogicOp, 150, 151                             MAX CLIENT ATTRIB STACK
LUMINANCE, 92, 99, 103, 104, 113                       DEPTH, 190
         115, 136, 137, 159, 160, 185,        MAX COLOR MATRIX STACK
         208, 210, 226                                 DEPTH, 185
LUMINANCE12, 115                              MAX CONVOLUTION HEIGHT,
LUMINANCE12 ALPHA12, 115                               83, 187
LUMINANCE12 ALPHA4, 115                       MAX CONVOLUTION WIDTH,
LUMINANCE16, 115                                       83, 84, 187
LUMINANCE16 ALPHA16, 115                      MAX ELEMENTS INDICES, 25
LUMINANCE4, 115                               MAX ELEMENTS VERTICES, 25
LUMINANCE4 ALPHA4, 115                        MAX EVAL ORDER, 165, 166
LUMINANCE6 ALPHA2, 115                        MAX PIXEL MAP TABLE, 79, 101
LUMINANCE8, 115                               MAX TEXTURE SIZE, 116
LUMINANCE8 ALPHA8, 115                        MAX TEXTURE UNITS ARB, 240,
LUMINANCE ALPHA, 92, 99, 103,                          243, 244, 251
         104, 113 115, 136, 137, 159,         MIN, 147
         160, 162, 185                        MINMAX, 88, 109, 188




                                  Version 1.2.1 - April 1, 1999
262                                                                     INDEX

Minmax, 88, 110                             ONE MINUS DST COLOR, 148
MINMAX FORMAT, 188                          ONE MINUS SRC ALPHA, 148
MINMAX SINK, 188                            ONE MINUS SRC COLOR, 148
MODELVIEW, 31, 34, 245                      OR, 151
MODULATE, 135, 136                          OR INVERTED, 151
MULT, 155, 156                              OR REVERSE, 151
MultiTexCoord, 241                          ORDER, 184
MultiTexCoordARB, 243, 244                  Ortho, 32, 33, 223
MultMatrix, 31, 32                          OUT OF MEMORY, 12, 13, 177
N3F V3F, 25, 26                             PACK ALIGNMENT, 158, 207
NAND, 151                                   PACK IMAGE HEIGHT, 158, 184,
NEAREST, 124, 127, 130, 131                          207
NEAREST MIPMAP LINEAR, 124,                 PACK LSB FIRST, 158, 207
        129 131                             PACK ROW LENGTH, 158, 207
NEAREST MIPMAP NEAREST,                     PACK SKIP IMAGES, 158, 184, 207
        124, 129 131                        PACK SKIP PIXELS, 158, 207
NEVER, 143 145                              PACK SKIP ROWS, 158, 207
NewList, 175, 177, 178                      PACK SWAP BYTES, 158, 207
NICEST, 180                                 PASS THROUGH TOKEN, 176
NO ERROR, 11, 12                            PassThrough, 174
NONE, 151, 152                              PERSPECTIVE CORRECTION
NOOP, 151                                            HINT, 180
NOR, 151                                    PIXEL MAP A TO A, 79, 101
Normal, 19, 20                              PIXEL MAP B TO B, 79, 101
Normal3, 8, 9, 20                           PIXEL MAP G TO G, 79, 101
Normal3d, 8                                 PIXEL MAP I TO A, 79, 102
Normal3dv, 9                                PIXEL MAP I TO B, 79, 102
Normal3f, 8                                 PIXEL MAP I TO G, 79, 102
Normal3fv, 9                                PIXEL MAP I TO I, 79, 102
NORMAL ARRAY, 23, 27                        PIXEL MAP I TO R, 79, 102
NORMAL ARRAY POINTER, 189                   PIXEL MAP R TO R, 79, 101
NORMALIZE, 35                               PIXEL MAP S TO S, 79, 102
NormalPointer, 19, 22, 27, 178              PIXEL MODE BIT, 191
NOTEQUAL, 143 145                           PixelMap, 75, 78, 79, 162
                                            PixelStore, 19, 75, 76, 78, 158, 162,
OBJECT LINEAR, 37, 38, 183, 245,                     178
       246                                  PixelTransfer, 75, 78, 107, 162
OBJECT PLANE, 37                            PixelZoom, 100
ONE, 148, 149, 205                          POINT, 73, 74, 168, 169, 201, 226
ONE MINUS CONSTANT ALPHA,                   POINT BIT, 191
       77, 148, 149                         POINT SMOOTH, 60
ONE MINUS CONSTANT COLOR,                   POINT SMOOTH HINT, 180
       77, 148, 149                         POINT TOKEN, 176
ONE MINUS DST ALPHA, 148                    POINTS, 15, 168




                   Version 1.2.1 - April 1, 1999
INDEX                                                                      263

PointSize, 60                              POST CONVOLUTION ALPHA
POLYGON, 16, 19                                      BIAS, 107
POLYGON BIT, 191                           POST CONVOLUTION ALPHA
POLYGON OFFSET FILL, 74                              SCALE, 107
POLYGON OFFSET LINE, 74                    POST CONVOLUTION BLUE
POLYGON OFFSET POINT, 74                             BIAS, 107
POLYGON SMOOTH, 70                         POST CONVOLUTION BLUE
POLYGON SMOOTH HINT, 180                             SCALE, 107
POLYGON STIPPLE, 72                        POST CONVOLUTION COLOR
POLYGON STIPPLE BIT, 191                             TABLE, 80, 108
POLYGON TOKEN, 176                         POST CONVOLUTION GREEN
PolygonMode, 69, 73, 75, 171, 173                    BIAS, 107
PolygonO set, 74                           POST CONVOLUTION GREEN
PolygonStipple, 72                                   SCALE, 107
PopAttrib, 189, 190, 192, 224, 251         POST CONVOLUTION RED
PopClientAttrib, 19, 178, 189, 190,                  BIAS, 107
         192, 251                          POST CONVOLUTION RED
PopMatrix, 34, 245                                   SCALE, 107
PopName, 171                               PrioritizeTextures, 134, 135
POSITION, 50, 183                          PROJECTION, 31, 34, 245
POST COLOR MATRIX x BIAS,                  PROXY COLOR TABLE, 80, 82,
         78                                          179
POST COLOR MATRIX x SCALE,                 PROXY HISTOGRAM, 87, 88, 179,
         78                                          188
POST COLOR MATRIX ALPHA                    PROXY POST COLOR MATRIX
         BIAS, 108                                   COLOR TABLE, 80, 179
POST COLOR MATRIX ALPHA                    PROXY POST CONVOLUTION
         SCALE, 108                                  COLOR TABLE, 80, 179
POST COLOR MATRIX BLUE                     PROXY TEXTURE 1D, 117, 132,
         BIAS, 108                                   179, 183
POST COLOR MATRIX BLUE                     PROXY TEXTURE 2D, 116, 132,
         SCALE, 108                                  179, 183
POST COLOR MATRIX COLOR                    PROXY TEXTURE 3D, 112, 132,
         TABLE, 80, 109                              179, 183
POST COLOR MATRIX GREEN                    PushAttrib, 189, 190, 192, 251
         BIAS, 108                         PushClientAttrib, 19, 178, 189, 190,
POST COLOR MATRIX GREEN                              192, 251
         SCALE, 108                        PushMatrix, 34, 245
POST COLOR MATRIX RED                      PushName, 171
         BIAS, 108                         Q, 36, 38, 183
POST COLOR MATRIX RED                      QUAD STRIP, 17
         SCALE, 108                        QUADRATIC ATTENUATION, 50
POST CONVOLUTION x BIAS, 78                QUADS, 18, 19
POST CONVOLUTION x SCALE,
         78                                R, 36, 38, 183




                               Version 1.2.1 - April 1, 1999
264                                                                         INDEX

R3 G3 B2, 115                                 S, 36, 37, 183
RasterPos, 41, 171, 223, 246                  Scale, 32, 33, 223
RasterPos2, 41, 246                           Scissor, 143
RasterPos3, 41, 246                           SCISSOR BIT, 191
RasterPos4, 41, 246                           SCISSOR TEST, 143
ReadBu er, 158, 159, 162                      SELECT, 171, 172, 224
ReadPixels, 75, 78, 91 93, 103, 156           SelectBu er, 171, 172, 178
         160, 162, 178, 184 186               SELECTION BUFFER POINTER,
Rect, 28, 70                                            189
RED, 78, 92, 159, 160, 208, 210, 216          SEPARABLE 2D, 85, 103, 117, 187
RED BIAS, 101                                 SeparableFilter2D, 84
RED SCALE, 101                                SEPARATE SPECULAR COLOR,
REDUCE, 105, 107, 209                                   47
RENDER, 171, 172, 217                         SET, 151
RENDERER, 189                                 SGI color matrix, 233
RenderMode, 171 174, 178                      SGIS multitexture, 238
REPEAT, 124, 125, 127, 128, 131,              SGIS texture edge clamp, 231
         203                                  SGIS texture lod, 232
REPLACE, 135, 136, 144                        ShadeModel, 54
REPLICATE BORDER, 105, 106                    SHININESS, 50
RESCALE NORMAL, 35                            SHORT, 22, 91, 160, 161, 177
ResetHistogram, 187                           SINGLE COLOR, 46, 47, 199
ResetMinmax, 188                              SMOOTH, 54, 198
RETURN, 155, 156                              SPECULAR, 50, 51
RGB, 92, 94, 98, 103, 104, 113 115,           SPHERE MAP, 37, 38
         136, 137, 159, 162, 185, 226         SPOT CUTOFF, 50
RGB10, 115                                    SPOT DIRECTION, 50, 183
RGB10 A2, 115                                 SPOT EXPONENT, 50
RGB12, 115                                    SRC ALPHA, 148
RGB16, 115                                    SRC ALPHA SATURATE, 148
RGB4, 115                                     SRC COLOR, 148
RGB5, 115                                     STACK OVERFLOW, 13, 34, 171,
RGB5 A1, 115                                            190, 245
RGB8, 115                                     STACK UNDERFLOW, 13, 34, 171,
RGBA, 81, 82, 85 88, 92, 94, 98, 103,                   190, 245
         104, 113 115, 136, 137, 159,         STENCIL, 162
         162, 185, 208 211                    STENCIL BUFFER BIT, 154, 191
RGBA12, 115                                   STENCIL INDEX, 80, 83, 90, 92,
RGBA16, 115                                             100, 112, 156, 158, 159, 162,
RGBA2, 115                                              184
RGBA4, 115                                    STENCIL TEST, 144
RGBA8, 115                                    StencilFunc, 144, 222
RIGHT, 151, 152, 158                          StencilMask, 153, 156, 223
Rotate, 32, 223                               StencilOp, 144, 145




                     Version 1.2.1 - April 1, 1999
INDEX                                                                       265

T, 36, 183                                    TEXTURE 2D, 103, 116, 120, 121,
T2F C3F V3F, 25, 26                                 124, 132, 133, 138, 183, 184
T2F C4F N3F V3F, 25, 26                       TEXTURE 3D, 112, 121, 124, 132,
T2F C4UB V3F, 25, 26                                133, 138, 183, 184
T2F N3F V3F, 25, 26                           TEXTURE ALPHA SIZE, 183
T2F V3F, 25, 26                               TEXTURE BASE LEVEL, 116, 117,
T4F C4F N3F V4F, 25, 26                             124, 126, 127, 129 132, 248
T4F V4F, 25, 26                               TEXTURE BIT, 190, 191
TABLE TOO LARGE, 13, 80, 87                   TEXTURE BLUE SIZE, 183
TexCoord, 19, 20, 241, 243                    TEXTURE BORDER, 183
TexCoord1, 20, 241                            TEXTURE BORDER COLOR, 124,
TexCoord2, 20, 241                                  129, 131, 132
TexCoord3, 20, 241                            TEXTURE COMPONENTS, 183
TexCoord4, 20, 241                            TEXTURE COORD ARRAY, 23,
TexCoordPointer, 19, 21, 22, 27, 178,               27, 243
         243                                  TEXTURE COORD ARRAY
TexEnv, 135, 249                                    POINTER, 189
TexGen, 36 38, 240, 246                       TEXTURE DEPTH, 183
TexImage, 121                                 TEXTURE ENV, 135, 183
TexImage1D, 76, 103, 105, 113, 117,           TEXTURE ENV COLOR, 135
         118, 120, 121, 129, 132, 179,        TEXTURE ENV MODE, 135
         248                                  TEXTURE GEN MODE, 37, 38
TexImage2D, 76, 87, 88, 103, 105,             TEXTURE GEN Q, 38
         113, 116 118, 120, 121, 129,         TEXTURE GEN R, 38
         132, 179, 248                        TEXTURE GEN S, 38
TexImage3D, 76, 112 114, 116 118,             TEXTURE GEN T, 38
         121, 129, 132, 178, 184, 248         TEXTURE GREEN SIZE, 183
TexParameter, 123                             TEXTURE HEIGHT, 183
TexParameter if , 126, 130                    TEXTURE INTENSITY SIZE, 183
TexParameterf, 134                            TEXTURE INTERNAL FORMAT,
TexParameterfv, 134                                 183
TexParameteri, 134                            TEXTURE LUMINANCE SIZE,
TexParameteriv, 134                                 183
TexSubImage, 121                              TEXTURE MAG FILTER, 124, 131
TexSubImage1D, 103, 121, 123                  TEXTURE MAX LEVEL, 116, 124,
TexSubImage2D, 103, 120 122                         130, 132, 248
TexSubImage3D, 120 122                        TEXTURE MAX LOD, 124 126,
TEXTURE, 31, 34, 244, 245                           132
TEXTUREi ARB, 241                             TEXTURE MIN FILTER, 124, 127,
TEXTURE0 ARB, 243, 245, 249,                        129 131, 248
         251, 254                             TEXTURE MIN LOD, 124 126, 132
TEXTURE1 ARB, 251                             TEXTURE PRIORITY, 124, 132,
TEXTURE xD, 202, 253                                134
TEXTURE 1D, 103, 117, 120, 121,               TEXTURE RED SIZE, 183
         124, 132, 133, 138, 183, 184         TEXTURE RESIDENT, 132, 134




                                  Version 1.2.1 - April 1, 1999
266                                                                      INDEX

TEXTURE WIDTH, 183                            UNSIGNED SHORT, 22, 24, 91, 96,
TEXTURE WRAP R, 124, 128                            160, 161, 177
TEXTURE WRAP S, 124, 127, 128                 UNSIGNED SHORT 1 5 5 5 REV,
TEXTURE WRAP T, 124, 128                            91, 94, 96, 161
TRANSFORM BIT, 191                            UNSIGNED SHORT 4 4 4 4, 91, 94,
Translate, 32, 223                                  96, 161
TRIANGLE FAN, 17                              UNSIGNED SHORT 4 4 4 4 REV,
TRIANGLE STRIP, 16                                  91, 94, 96, 161
TRIANGLES, 17, 19                             UNSIGNED SHORT 5 5 5 1, 91, 94,
TRUE, 18, 19, 40, 46 48, 76, 78, 87,                96, 161
         88, 134, 153, 158, 178, 182,         UNSIGNED SHORT 5 6 5, 91, 93,
         184, 187, 188                              94, 96, 161
                                              UNSIGNED SHORT 5 6 5 REV, 91,
                                                    93, 94, 96, 161
UNPACK ALIGNMENT, 76, 93,
      112, 207                                V2F, 25, 26
UNPACK IMAGE HEIGHT,           76,            V3F, 25, 26
      112, 207                                VENDOR, 189
UNPACK LSB FIRST, 76, 98, 207                 VERSION, 189
UNPACK ROW LENGTH, 76, 90,                    Vertex, 7, 19, 20, 41, 167
      93, 112, 207                            Vertex2, 20, 28
UNPACK SKIP IMAGES, 76, 112,                  Vertex2sv, 7
      117, 207                                Vertex3, 20
UNPACK SKIP PIXELS, 76, 93, 98,               Vertex3f, 7
      207                                     Vertex4, 20
UNPACK SKIP ROWS, 76, 93, 98,                 VERTEX ARRAY, 23, 27
      207                                     VERTEX ARRAY POINTER, 189
UNPACK SWAP BYTES, 76, 90, 92,                VertexPointer, 19, 22, 27, 178
      207                                     Viewport, 30
UNSIGNED BYTE, 22, 24, 26, 91,                VIEWPORT BIT, 191
      95, 160, 161, 177
UNSIGNED BYTE 2 3 3 REV, 91,                  XOR, 151
      93 95, 161                              ZERO, 144, 148, 149, 205
UNSIGNED BYTE 3 3 2, 91, 93 95,
      161
UNSIGNED INT, 22, 24, 91, 97, 160,
      161, 177
UNSIGNED INT 10 10 10 2, 91, 94,
      97, 161
UNSIGNED INT 2 10 10 10 REV,
      91, 94, 97, 161
UNSIGNED INT 8 8 8 8, 91, 94, 97,
      161
UNSIGNED INT 8 8 8 8 REV, 91,
      94, 97, 161




                     Version 1.2.1 - April 1, 1999
