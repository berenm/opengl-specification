                  R
The OpenGL Graphics System:
       A Specification
        (Version 1.3)

                Mark Segal
                Kurt Akeley

     Editor (version 1.1): Chris Frazier
 Editor (versions 1.2, 1.2.1, 1.3): Jon Leech
                  Copyright c 1992-2001 Silicon Graphics, Inc.


               This document contains unpublished information of
                            Silicon Graphics, Inc.

This document is protected by copyright, and contains information proprietary to
Silicon Graphics, Inc. Any copying, adaptation, distribution, public performance,
or public display of this document without the express written consent of Silicon
Graphics, Inc. is strictly prohibited. The receipt or possession of this document
does not convey any rights to reproduce, disclose, or distribute its contents, or to
manufacture, use, or sell anything that it may describe, in whole or in part.

                    U.S. Government Restricted Rights Legend

Use, duplication, or disclosure by the Government is subject to restrictions set forth
in FAR 52.227.19(c)(2) or subparagraph (c)(1)(ii) of the Rights in Technical Data
and Computer Software clause at DFARS 252.227-7013 and/or in similar or succes-
sor clauses in the FAR or the DOD or NASA FAR Supplement. Unpublished rights
reserved under the copyright laws of the United States. Contractor/manufacturer is
Silicon Graphics, Inc., 1600 Amphitheatre Parkway, Mountain View, CA 94043.

            OpenGL is a registered trademark of Silicon Graphics, Inc.
               Unix is a registered trademark of The Open Group.
            The ”X” device and X Windows System are trademarks of
                                 The Open Group.
Contents

1   Introduction                                                                                            1
    1.1 Formatting of Optional Features . . . .     .   .   .   .   .   .   .   .   .   .   .   .   .   .   1
    1.2 What is the OpenGL Graphics System?         .   .   .   .   .   .   .   .   .   .   .   .   .   .   1
    1.3 Programmer’s View of OpenGL . . . .         .   .   .   .   .   .   .   .   .   .   .   .   .   .   2
    1.4 Implementor’s View of OpenGL . . . .        .   .   .   .   .   .   .   .   .   .   .   .   .   .   2
    1.5 Our View . . . . . . . . . . . . . . . .    .   .   .   .   .   .   .   .   .   .   .   .   .   .   3

2   OpenGL Operation                                                                                         4
    2.1 OpenGL Fundamentals . . . . . . . . . .         .   .   .   .   .   .   .   .   .   .   .   .   .    4
         2.1.1 Floating-Point Computation . . .         .   .   .   .   .   .   .   .   .   .   .   .   .    6
    2.2 GL State . . . . . . . . . . . . . . . . . .    .   .   .   .   .   .   .   .   .   .   .   .   .    6
    2.3 GL Command Syntax . . . . . . . . . . .         .   .   .   .   .   .   .   .   .   .   .   .   .    7
    2.4 Basic GL Operation . . . . . . . . . . . .      .   .   .   .   .   .   .   .   .   .   .   .   .   10
    2.5 GL Errors . . . . . . . . . . . . . . . . .     .   .   .   .   .   .   .   .   .   .   .   .   .   11
    2.6 Begin/End Paradigm . . . . . . . . . . .        .   .   .   .   .   .   .   .   .   .   .   .   .   12
         2.6.1 Begin and End Objects . . . . . .        .   .   .   .   .   .   .   .   .   .   .   .   .   13
         2.6.2 Polygon Edges . . . . . . . . . .        .   .   .   .   .   .   .   .   .   .   .   .   .   18
         2.6.3 GL Commands within Begin/End             .   .   .   .   .   .   .   .   .   .   .   .   .   19
    2.7 Vertex Specification . . . . . . . . . . . .    .   .   .   .   .   .   .   .   .   .   .   .   .   19
    2.8 Vertex Arrays . . . . . . . . . . . . . . .     .   .   .   .   .   .   .   .   .   .   .   .   .   21
    2.9 Rectangles . . . . . . . . . . . . . . . . .    .   .   .   .   .   .   .   .   .   .   .   .   .   28
    2.10 Coordinate Transformations . . . . . . .       .   .   .   .   .   .   .   .   .   .   .   .   .   29
         2.10.1 Controlling the Viewport . . . . .      .   .   .   .   .   .   .   .   .   .   .   .   .   30
         2.10.2 Matrices . . . . . . . . . . . . . .    .   .   .   .   .   .   .   .   .   .   .   .   .   31
         2.10.3 Normal Transformation . . . . . .       .   .   .   .   .   .   .   .   .   .   .   .   .   36
         2.10.4 Generating Texture Coordinates .        .   .   .   .   .   .   .   .   .   .   .   .   .   37
    2.11 Clipping . . . . . . . . . . . . . . . . . .   .   .   .   .   .   .   .   .   .   .   .   .   .   39
    2.12 Current Raster Position . . . . . . . . . .    .   .   .   .   .   .   .   .   .   .   .   .   .   42
    2.13 Colors and Coloring . . . . . . . . . . . .    .   .   .   .   .   .   .   .   .   .   .   .   .   44

                                         i
ii                                                                                      CONTENTS


          2.13.1   Lighting . . . . . . . . . . . . . . . . .   .   .   .   .   .   .   .   .   .   .   46
          2.13.2   Lighting Parameter Specification . . . .     .   .   .   .   .   .   .   .   .   .   50
          2.13.3   ColorMaterial . . . . . . . . . . . . .      .   .   .   .   .   .   .   .   .   .   51
          2.13.4   Lighting State . . . . . . . . . . . . . .   .   .   .   .   .   .   .   .   .   .   54
          2.13.5   Color Index Lighting . . . . . . . . . .     .   .   .   .   .   .   .   .   .   .   54
          2.13.6   Clamping or Masking . . . . . . . . .        .   .   .   .   .   .   .   .   .   .   55
          2.13.7   Flatshading . . . . . . . . . . . . . . .    .   .   .   .   .   .   .   .   .   .   55
          2.13.8   Color and Texture Coordinate Clipping        .   .   .   .   .   .   .   .   .   .   56
          2.13.9   Final Color Processing . . . . . . . . .     .   .   .   .   .   .   .   .   .   .   57

3    Rasterization                                                                                       58
     3.1 Invariance . . . . . . . . . . . . . . . . . . . . . .         .   .   .   .   .   .   .   .    60
     3.2 Antialiasing . . . . . . . . . . . . . . . . . . . . .         .   .   .   .   .   .   .   .    60
          3.2.1 Multisampling . . . . . . . . . . . . . . .             .   .   .   .   .   .   .   .    61
     3.3 Points . . . . . . . . . . . . . . . . . . . . . . . .         .   .   .   .   .   .   .   .    63
          3.3.1 Point Rasterization State . . . . . . . . . .           .   .   .   .   .   .   .   .    66
          3.3.2 Point Multisample Rasterization . . . . . .             .   .   .   .   .   .   .   .    66
     3.4 Line Segments . . . . . . . . . . . . . . . . . . .            .   .   .   .   .   .   .   .    66
          3.4.1 Basic Line Segment Rasterization . . . . .              .   .   .   .   .   .   .   .    66
          3.4.2 Other Line Segment Features . . . . . . . .             .   .   .   .   .   .   .   .    69
          3.4.3 Line Rasterization State . . . . . . . . . .            .   .   .   .   .   .   .   .    72
          3.4.4 Line Multisample Rasterization . . . . . .              .   .   .   .   .   .   .   .    72
     3.5 Polygons . . . . . . . . . . . . . . . . . . . . . .           .   .   .   .   .   .   .   .    73
          3.5.1 Basic Polygon Rasterization . . . . . . . .             .   .   .   .   .   .   .   .    73
          3.5.2 Stippling . . . . . . . . . . . . . . . . . .           .   .   .   .   .   .   .   .    75
          3.5.3 Antialiasing . . . . . . . . . . . . . . . . .          .   .   .   .   .   .   .   .    76
          3.5.4 Options Controlling Polygon Rasterization               .   .   .   .   .   .   .   .    76
          3.5.5 Depth Offset . . . . . . . . . . . . . . . .            .   .   .   .   .   .   .   .    77
          3.5.6 Polygon Multisample Rasterization . . . .               .   .   .   .   .   .   .   .    78
          3.5.7 Polygon Rasterization State . . . . . . . .             .   .   .   .   .   .   .   .    78
     3.6 Pixel Rectangles . . . . . . . . . . . . . . . . . . .         .   .   .   .   .   .   .   .    79
          3.6.1 Pixel Storage Modes . . . . . . . . . . . .             .   .   .   .   .   .   .   .    79
          3.6.2 The Imaging Subset . . . . . . . . . . . .              .   .   .   .   .   .   .   .    80
          3.6.3 Pixel Transfer Modes . . . . . . . . . . . .            .   .   .   .   .   .   .   .    81
          3.6.4 Rasterization of Pixel Rectangles . . . . .             .   .   .   .   .   .   .   .    91
          3.6.5 Pixel Transfer Operations . . . . . . . . .             .   .   .   .   .   .   .   .   103
          3.6.6 Pixel Rectangle Multisample Rasterization               .   .   .   .   .   .   .   .   113
     3.7 Bitmaps . . . . . . . . . . . . . . . . . . . . . . .          .   .   .   .   .   .   .   .   113
     3.8 Texturing . . . . . . . . . . . . . . . . . . . . . .          .   .   .   .   .   .   .   .   115
          3.8.1 Texture Image Specification . . . . . . . .             .   .   .   .   .   .   .   .   116

                           Version 1.3 - August 14, 2001
CONTENTS                                                                                       iii


         3.8.2 Alternate Texture Image Specification Commands                 .   .   .   .   123
         3.8.3 Compressed Texture Images . . . . . . . . . . . .              .   .   .   .   129
         3.8.4 Texture Parameters . . . . . . . . . . . . . . . . .           .   .   .   .   132
         3.8.5 Texture Wrap Modes . . . . . . . . . . . . . . . .             .   .   .   .   134
         3.8.6 Cube Map Texture Selection . . . . . . . . . . . .             .   .   .   .   135
         3.8.7 Texture Minification . . . . . . . . . . . . . . . .           .   .   .   .   135
         3.8.8 Texture Magnification . . . . . . . . . . . . . . .            .   .   .   .   141
         3.8.9 Texture Completeness . . . . . . . . . . . . . . .             .   .   .   .   141
         3.8.10 Texture State and Proxy State . . . . . . . . . . .           .   .   .   .   143
         3.8.11 Texture Objects . . . . . . . . . . . . . . . . . . .         .   .   .   .   144
         3.8.12 Texture Environments and Texture Functions . . .              .   .   .   .   146
         3.8.13 Texture Application . . . . . . . . . . . . . . . . .         .   .   .   .   149
    3.9 Color Sum . . . . . . . . . . . . . . . . . . . . . . . . . .         .   .   .   .   154
    3.10 Fog . . . . . . . . . . . . . . . . . . . . . . . . . . . . .        .   .   .   .   154
    3.11 Antialiasing Application . . . . . . . . . . . . . . . . . .         .   .   .   .   155

4   Per-Fragment Operations and the Framebuffer                                               156
    4.1 Per-Fragment Operations . . . . . . . . . . . . . . .     .   .   .   .   .   .   .   157
         4.1.1 Pixel Ownership Test . . . . . . . . . . . . .     .   .   .   .   .   .   .   157
         4.1.2 Scissor test . . . . . . . . . . . . . . . . . .   .   .   .   .   .   .   .   158
         4.1.3 Multisample Fragment Operations . . . . . .        .   .   .   .   .   .   .   158
         4.1.4 Alpha test . . . . . . . . . . . . . . . . . . .   .   .   .   .   .   .   .   159
         4.1.5 Stencil test . . . . . . . . . . . . . . . . . .   .   .   .   .   .   .   .   160
         4.1.6 Depth buffer test . . . . . . . . . . . . . . .    .   .   .   .   .   .   .   161
         4.1.7 Blending . . . . . . . . . . . . . . . . . . .     .   .   .   .   .   .   .   161
         4.1.8 Dithering . . . . . . . . . . . . . . . . . . .    .   .   .   .   .   .   .   165
         4.1.9 Logical Operation . . . . . . . . . . . . . .      .   .   .   .   .   .   .   165
         4.1.10 Additional Multisample Fragment Operations        .   .   .   .   .   .   .   167
    4.2 Whole Framebuffer Operations . . . . . . . . . . . .      .   .   .   .   .   .   .   167
         4.2.1 Selecting a Buffer for Writing . . . . . . . .     .   .   .   .   .   .   .   168
         4.2.2 Fine Control of Buffer Updates . . . . . . .       .   .   .   .   .   .   .   169
         4.2.3 Clearing the Buffers . . . . . . . . . . . . .     .   .   .   .   .   .   .   170
         4.2.4 The Accumulation Buffer . . . . . . . . . .        .   .   .   .   .   .   .   172
    4.3 Drawing, Reading, and Copying Pixels . . . . . . . .      .   .   .   .   .   .   .   173
         4.3.1 Writing to the Stencil Buffer . . . . . . . . .    .   .   .   .   .   .   .   173
         4.3.2 Reading Pixels . . . . . . . . . . . . . . . .     .   .   .   .   .   .   .   173
         4.3.3 Copying Pixels . . . . . . . . . . . . . . . .     .   .   .   .   .   .   .   177
         4.3.4 Pixel Draw/Read State . . . . . . . . . . . .      .   .   .   .   .   .   .   180

                          Version 1.3 - August 14, 2001
iv                                                                                                                     CONTENTS


5    Special Functions                                                                                                                 181
     5.1 Evaluators . . . .    .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   181
     5.2 Selection . . . .     .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   187
     5.3 Feedback . . . .      .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   189
     5.4 Display Lists . .     .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   191
     5.5 Flush and Finish .    .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   195
     5.6 Hints . . . . . . .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   196

6    State and State Requests                                                                                                          197
     6.1 Querying GL State . . . . . . . .                         .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   197
           6.1.1 Simple Queries . . . . . .                        .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   197
           6.1.2 Data Conversions . . . . .                        .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   198
           6.1.3 Enumerated Queries . . .                          .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   199
           6.1.4 Texture Queries . . . . . .                       .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   200
           6.1.5 Stipple Query . . . . . . .                       .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   202
           6.1.6 Color Matrix Query . . . .                        .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   203
           6.1.7 Color Table Query . . . .                         .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   203
           6.1.8 Convolution Query . . . .                         .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   204
           6.1.9 Histogram Query . . . . .                         .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   204
           6.1.10 Minmax Query . . . . . .                         .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   205
           6.1.11 Pointer and String Queries                       .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   206
           6.1.12 Saving and Restoring State                       .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   207
     6.2 State Tables . . . . . . . . . . . .                      .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   209

A Invariance                                                                                                                           240
  A.1 Repeatability . . . . .              .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   240
  A.2 Multi-pass Algorithms                .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   241
  A.3 Invariance Rules . . . .             .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   241
  A.4 What All This Means .                .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   243

B Corollaries                                                                                                                          244

C Version 1.1                                                                                                                          247
  C.1 Vertex Array . . . . . . . . . .                     .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   247
  C.2 Polygon Offset . . . . . . . .                       .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   248
  C.3 Logical Operation . . . . . . .                      .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   248
  C.4 Texture Image Formats . . . .                        .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   248
  C.5 Texture Replace Environment .                        .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   248
  C.6 Texture Proxies . . . . . . . .                      .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   249
  C.7 Copy Texture and Subtexture .                        .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   249

                          Version 1.3 - August 14, 2001
CONTENTS                                                                                                         v


   C.8 Texture Objects . . . . . . . . . . . . . . . . . . . . . . . . . . . 249
   C.9 Other Changes . . . . . . . . . . . . . . . . . . . . . . . . . . . 249
   C.10 Acknowledgements . . . . . . . . . . . . . . . . . . . . . . . . . 250

D Version 1.2                                                                                                  252
  D.1 Three-Dimensional Texturing . . . .      .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   252
  D.2 BGRA Pixel Formats . . . . . . . .       .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   252
  D.3 Packed Pixel Formats . . . . . . . .     .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   253
  D.4 Normal Rescaling . . . . . . . . . .     .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   253
  D.5 Separate Specular Color . . . . . .      .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   253
  D.6 Texture Coordinate Edge Clamping         .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   253
  D.7 Texture Level of Detail Control . . .    .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   254
  D.8 Vertex Array Draw Element Range .        .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   254
  D.9 Imaging Subset . . . . . . . . . . .     .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   254
       D.9.1 Color Tables . . . . . . . .      .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   254
       D.9.2 Convolution . . . . . . . . .     .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   255
       D.9.3 Color Matrix . . . . . . . .      .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   255
       D.9.4 Pixel Pipeline Statistics . . .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   256
       D.9.5 Constant Blend Color . . . .      .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   256
       D.9.6 New Blending Equations . .        .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   256
  D.10 Acknowledgements . . . . . . . . .      .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   256

E Version 1.2.1                                                                                                260

F Version 1.3                                                                                                  261
  F.1 Compressed Textures . . . . . . . . .        .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   261
  F.2 Cube Map Textures . . . . . . . . . .        .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   261
  F.3 Multisample . . . . . . . . . . . . . .      .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   262
  F.4 Multitexture . . . . . . . . . . . . . .     .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   262
  F.5 Texture Add Environment Mode . . .           .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   263
  F.6 Texture Combine Environment Mode             .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   263
  F.7 Texture Dot3 Environment Mode . . .          .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   263
  F.8 Texture Border Clamp . . . . . . . .         .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   263
  F.9 Transpose Matrix . . . . . . . . . . .       .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   264
  F.10 Acknowledgements . . . . . . . . . .        .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   264

G ARB Extensions                                                             269
  G.1 Naming Conventions . . . . . . . . . . . . . . . . . . . . . . . . 269
  G.2 Promoting Extensions to Core Features . . . . . . . . . . . . . . 270
  G.3 Multitexture . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 270

                         Version 1.3 - August 14, 2001
vi                                                                                                 CONTENTS


     G.4    Transpose Matrix . . . . . . . . . . .     .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   270
     G.5    Multisample . . . . . . . . . . . . . .    .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   270
     G.6    Texture Add Environment Mode . . .         .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   270
     G.7    Cube Map Textures . . . . . . . . . .      .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   271
     G.8    Compressed Textures . . . . . . . . .      .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   271
     G.9    Texture Border Clamp . . . . . . . .       .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   271
     G.10   Point Parameters . . . . . . . . . . .     .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   271
     G.11   Vertex Blend . . . . . . . . . . . . .     .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   271
     G.12   Matrix Palette . . . . . . . . . . . . .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   271
     G.13   Texture Combine Environment Mode           .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   272
     G.14   Texture Crossbar Environment Mode .        .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   272
     G.15   Texture Dot3 Environment Mode . . .        .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   272

     Index of OpenGL Commands                                                                                      273




                             Version 1.3 - August 14, 2001
List of Figures

 2.1  Block diagram of the GL. . . . . . . . . . . . . . . . . . . . . . .              10
 2.2  Creation of a processed vertex from a transformed vertex and cur-
      rent values. . . . . . . . . . . . . . . . . . . . . . . . . . . . . .            13
 2.3 Primitive assembly and processing. . . . . . . . . . . . . . . . . .               13
 2.4 Triangle strips, fans, and independent triangles. . . . . . . . . . .              16
 2.5 Quadrilateral strips and independent quadrilaterals. . . . . . . . .               17
 2.6 Vertex transformation sequence. . . . . . . . . . . . . . . . . . .                29
 2.7 Current raster position. . . . . . . . . . . . . . . . . . . . . . . .             42
 2.8 Processing of RGBA colors. . . . . . . . . . . . . . . . . . . . .                 44
 2.9 Processing of color indices. . . . . . . . . . . . . . . . . . . . . .             44
 2.10 ColorMaterial operation. . . . . . . . . . . . . . . . . . . . . . .              51

 3.1    Rasterization. . . . . . . . . . . . . . . . . . . . . . . . .   .   .   .   . 58
 3.2    Rasterization of non-antialiased wide points. . . . . . . . .    .   .   .   . 63
 3.3    Rasterization of antialiased wide points. . . . . . . . . . .    .   .   .   . 64
 3.4    Visualization of Bresenham’s algorithm. . . . . . . . . . .      .   .   .   . 67
 3.5    Rasterization of non-antialiased wide lines. . . . . . . . .     .   .   .   . 70
 3.6    The region used in rasterizing an antialiased line segment.      .   .   .   . 71
 3.7    Operation of DrawPixels. . . . . . . . . . . . . . . . . .       .   .   .   . 91
 3.8    Selecting a subimage from an image . . . . . . . . . . . .       .   .   .   . 96
 3.9    A bitmap and its associated parameters. . . . . . . . . . .      .   .   .   . 114
 3.10   A texture image and the coordinates used to access it. . . .     .   .   .   . 123
 3.11   Multitexture pipeline. . . . . . . . . . . . . . . . . . . . .   .   .   .   . 152

 4.1    Per-fragment operations. . . . . . . . . . . . . . . . . . . . . . . 157
 4.2    Operation of ReadPixels. . . . . . . . . . . . . . . . . . . . . . . 173
 4.3    Operation of CopyPixels. . . . . . . . . . . . . . . . . . . . . . . 177

 5.1    Map Evaluation. . . . . . . . . . . . . . . . . . . . . . . . . . . . 183
 5.2    Feedback syntax. . . . . . . . . . . . . . . . . . . . . . . . . . . 192


                                       vii
List of Tables

 2.1    GL command suffixes . . . . . . . . . . . . . . . . . . .     .   .   .   .   .    8
 2.2    GL data types . . . . . . . . . . . . . . . . . . . . . . .   .   .   .   .   .    9
 2.3    Summary of GL errors . . . . . . . . . . . . . . . . . .      .   .   .   .   .   12
 2.4    Vertex array sizes (values per vertex) and data types . . .   .   .   .   .   .   23
 2.5    Variables that direct the execution of InterleavedArrays.     .   .   .   .   .   27
 2.6    Component conversions . . . . . . . . . . . . . . . . . .     .   .   .   .   .   45
 2.7    Summary of lighting parameters. . . . . . . . . . . . . .     .   .   .   .   .   47
 2.8    Correspondence of lighting parameter symbols to names.        .   .   .   .   .   52
 2.9    Polygon flatshading color selection. . . . . . . . . . . .    .   .   .   .   .   56

 3.1    PixelStore parameters. . . . . . . . . . . . . . . . . . . . . . . .              80
 3.2    PixelTransfer parameters. . . . . . . . . . . . . . . . . . . . . .               82
 3.3    PixelMap parameters. . . . . . . . . . . . . . . . . . . . . . . .                83
 3.4    Color table names. . . . . . . . . . . . . . . . . . . . . . . . . .              83
 3.5    DrawPixels and ReadPixels types. . . . . . . . . . . . . . . . . .                94
 3.6    DrawPixels and ReadPixels formats. . . . . . . . . . . . . . . .                  95
 3.7    Swap Bytes bit ordering. . . . . . . . . . . . . . . . . . . . . . .              95
 3.8    Packed pixel formats. . . . . . . . . . . . . . . . . . . . . . . . .             97
 3.9    UNSIGNED BYTE formats. Bit numbers are indicated for each com-
        ponent. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .              98
 3.10   UNSIGNED SHORT formats . . . . . . . . . . . . . . . . . . . . .                   99
 3.11   UNSIGNED INT formats . . . . . . . . . . . . . . . . . . . . . . .                100
 3.12   Packed pixel field assignments. . . . . . . . . . . . . . . . . . . .             101
 3.13   Color table lookup. . . . . . . . . . . . . . . . . . . . . . . . . .             106
 3.14   Computation of filtered color components. . . . . . . . . . . . . .               107
 3.15   Conversion from RGBA pixel components to internal texture, ta-
        ble, or filter components. . . . . . . . . . . . . . . . . . . . . . .            118
 3.16   Correspondence of sized internal formats to base internal formats.                119
 3.17   Specific compressed internal formats. . . . . . . . . . . . . . . .               120
 3.18   Generic compressed internal formats. . . . . . . . . . . . . . . .                120

                                       viii
LIST OF TABLES                                                                                      ix


  3.19   Texture parameters and their values. . . . . . . . . .        .   .   .   .   .   .   .   133
  3.20   Selection of cube map images. . . . . . . . . . . . .         .   .   .   .   .   .   .   135
  3.21   Correspondence of filtered texture components. . . .          .   .   .   .   .   .   .   148
  3.22   Texture functions REPLACE, MODULATE, and DECAL .              .   .   .   .   .   .   .   148
  3.23   Texture functions BLEND and ADD. . . . . . . . . . .          .   .   .   .   .   .   .   149
  3.24   COMBINE texture functions. . . . . . . . . . . . . . .        .   .   .   .   .   .   .   150
  3.25   Arguments for COMBINE RGB functions. . . . . . . .            .   .   .   .   .   .   .   151
  3.26   Arguments for COMBINE ALPHA functions. . . . . .              .   .   .   .   .   .   .   151

  4.1    Values controlling the source blending function and the source
         blending values they compute. f = min(As , 1 − Ad ). . . . . . .                          164
  4.2    Values controlling the destination blending function and the desti-
         nation blending values they compute. . . . . . . . . . . . . . . .                        164
  4.3    Arguments to LogicOp and their corresponding operations. . . . .                          166
  4.4    Arguments to DrawBuffer and the buffers that they indicate. . . .                         168
  4.5    PixelStore parameters. . . . . . . . . . . . . . . . . . . . . . . .                      175
  4.6    ReadPixels index masks. . . . . . . . . . . . . . . . . . . . . . .                       177
  4.7    ReadPixels GL data types and reversed component conversion for-
         mulas. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .                    178

  5.1    Values specified by the target to Map1. . . . . . . . . . . . . . . 182
  5.2    Correspondence of feedback type to number of values per vertex. . 191

  6.1    Texture, table, and filter return values. . . . . . . .   .   .   .   .   .   .   .   .   202
  6.2    Attribute groups . . . . . . . . . . . . . . . . . . .    .   .   .   .   .   .   .   .   208
  6.3    State variable types . . . . . . . . . . . . . . . . .    .   .   .   .   .   .   .   .   210
  6.4    GL Internal begin-end state variables (inaccessible)      .   .   .   .   .   .   .   .   212
  6.5    Current Values and Associated Data . . . . . . . .        .   .   .   .   .   .   .   .   213
  6.6    Vertex Array Data . . . . . . . . . . . . . . . . . .     .   .   .   .   .   .   .   .   214
  6.7    Vertex Array Data (cont.) . . . . . . . . . . . . . .     .   .   .   .   .   .   .   .   215
  6.8    Transformation state . . . . . . . . . . . . . . . .      .   .   .   .   .   .   .   .   216
  6.9    Coloring . . . . . . . . . . . . . . . . . . . . . . .    .   .   .   .   .   .   .   .   217
  6.10   Lighting (see also Table 2.7 for defaults) . . . . . .    .   .   .   .   .   .   .   .   218
  6.11   Lighting (cont.) . . . . . . . . . . . . . . . . . . .    .   .   .   .   .   .   .   .   219
  6.12   Rasterization . . . . . . . . . . . . . . . . . . . .     .   .   .   .   .   .   .   .   220
  6.13   Multisampling . . . . . . . . . . . . . . . . . . . .     .   .   .   .   .   .   .   .   221
  6.14   Texture Objects . . . . . . . . . . . . . . . . . . .     .   .   .   .   .   .   .   .   222
  6.15   Texture Objects (cont.) . . . . . . . . . . . . . . .     .   .   .   .   .   .   .   .   223
  6.16   Texture Objects (cont.) . . . . . . . . . . . . . . .     .   .   .   .   .   .   .   .   224
  6.17   Texture Environment and Generation . . . . . . . .        .   .   .   .   .   .   .   .   225

                          Version 1.3 - August 14, 2001
x                                                                                  LIST OF TABLES


    6.18   Pixel Operations . . . . . . . . . . . . . .    .   .   .   .   .   .   .   .   .   .   .   .   .   226
    6.19   Framebuffer Control . . . . . . . . . . .       .   .   .   .   .   .   .   .   .   .   .   .   .   227
    6.20   Pixels . . . . . . . . . . . . . . . . . . .    .   .   .   .   .   .   .   .   .   .   .   .   .   228
    6.21   Pixels (cont.) . . . . . . . . . . . . . . .    .   .   .   .   .   .   .   .   .   .   .   .   .   229
    6.22   Pixels (cont.) . . . . . . . . . . . . . . .    .   .   .   .   .   .   .   .   .   .   .   .   .   230
    6.23   Pixels (cont.) . . . . . . . . . . . . . . .    .   .   .   .   .   .   .   .   .   .   .   .   .   231
    6.24   Pixels (cont.) . . . . . . . . . . . . . . .    .   .   .   .   .   .   .   .   .   .   .   .   .   232
    6.25   Evaluators (GetMap takes a map name) .          .   .   .   .   .   .   .   .   .   .   .   .   .   233
    6.26   Hints . . . . . . . . . . . . . . . . . . . .   .   .   .   .   .   .   .   .   .   .   .   .   .   234
    6.27   Implementation Dependent Values . . . .         .   .   .   .   .   .   .   .   .   .   .   .   .   235
    6.28   Implementation Dependent Values (cont.)         .   .   .   .   .   .   .   .   .   .   .   .   .   236
    6.29   Implementation Dependent Values (cont.)         .   .   .   .   .   .   .   .   .   .   .   .   .   237
    6.30   Implementation Dependent Pixel Depths .         .   .   .   .   .   .   .   .   .   .   .   .   .   238
    6.31   Miscellaneous . . . . . . . . . . . . . . .     .   .   .   .   .   .   .   .   .   .   .   .   .   239




                            Version 1.3 - August 14, 2001
Chapter 1

Introduction

This document describes the OpenGL graphics system: what it is, how it acts, and
what is required to implement it. We assume that the reader has at least a rudi-
mentary understanding of computer graphics. This means familiarity with the es-
sentials of computer graphics algorithms as well as familiarity with basic graphics
hardware and associated terms.


1.1    Formatting of Optional Features
Starting with version 1.2 of OpenGL, some features in the specification are consid-
ered optional; an OpenGL implementation may or may not choose to provide them
(see section 3.6.2).
    Portions of the specification which are optional are described where the op-
tional features are first defined (see section 3.6.2). State table entries which are
optional are typeset against a gray background .


1.2    What is the OpenGL Graphics System?
OpenGL (for “Open Graphics Library”) is a software interface to graphics hard-
ware. The interface consists of a set of several hundred procedures and functions
that allow a programmer to specify the objects and operations involved in produc-
ing high-quality graphical images, specifically color images of three-dimensional
objects.
    Most of OpenGL requires that the graphics hardware contain a framebuffer.
Many OpenGL calls pertain to drawing objects such as points, lines, polygons, and
bitmaps, but the way that some of this drawing occurs (such as when antialiasing

                                         1
2                                                CHAPTER 1. INTRODUCTION


or texturing is enabled) relies on the existence of a framebuffer. Further, some of
OpenGL is specifically concerned with framebuffer manipulation.


1.3    Programmer’s View of OpenGL
To the programmer, OpenGL is a set of commands that allow the specification of
geometric objects in two or three dimensions, together with commands that control
how these objects are rendered into the framebuffer. For the most part, OpenGL
provides an immediate-mode interface, meaning that specifying an object causes it
to be drawn.
    A typical program that uses OpenGL begins with calls to open a window into
the framebuffer into which the program will draw. Then, calls are made to allocate
a GL context and associate it with the window. Once a GL context is allocated,
the programmer is free to issue OpenGL commands. Some calls are used to draw
simple geometric objects (i.e. points, line segments, and polygons), while others
affect the rendering of these primitives including how they are lit or colored and
how they are mapped from the user’s two- or three-dimensional model space to
the two-dimensional screen. There are also calls to effect direct control of the
framebuffer, such as reading and writing pixels.


1.4    Implementor’s View of OpenGL
To the implementor, OpenGL is a set of commands that affect the operation of
graphics hardware. If the hardware consists only of an addressable framebuffer,
then OpenGL must be implemented almost entirely on the host CPU. More typi-
cally, the graphics hardware may comprise varying degrees of graphics accelera-
tion, from a raster subsystem capable of rendering two-dimensional lines and poly-
gons to sophisticated floating-point processors capable of transforming and com-
puting on geometric data. The OpenGL implementor’s task is to provide the CPU
software interface while dividing the work for each OpenGL command between
the CPU and the graphics hardware. This division must be tailored to the available
graphics hardware to obtain optimum performance in carrying out OpenGL calls.
    OpenGL maintains a considerable amount of state information. This state con-
trols how objects are drawn into the framebuffer. Some of this state is directly
available to the user: he or she can make calls to obtain its value. Some of it, how-
ever, is visible only by the effect it has on what is drawn. One of the main goals of
this specification is to make OpenGL state information explicit, to elucidate how it
changes, and to indicate what its effects are.

                          Version 1.3 - August 14, 2001
1.5. OUR VIEW                                                                    3


1.5    Our View
We view OpenGL as a state machine that controls a set of specific drawing oper-
ations. This model should engender a specification that satisfies the needs of both
programmers and implementors. It does not, however, necessarily provide a model
for implementation. An implementation must produce results conforming to those
produced by the specified methods, but there may be ways to carry out a particular
computation that are more efficient than the one specified.




                          Version 1.3 - August 14, 2001
Chapter 2

OpenGL Operation

2.1    OpenGL Fundamentals
OpenGL (henceforth, the “GL”) is concerned only with rendering into a frame-
buffer (and reading values stored in that framebuffer). There is no support for
other peripherals sometimes associated with graphics hardware, such as mice and
keyboards. Programmers must rely on other mechanisms to obtain user input.
     The GL draws primitives subject to a number of selectable modes. Each prim-
itive is a point, line segment, polygon, or pixel rectangle. Each mode may be
changed independently; the setting of one does not affect the settings of others
(although many modes may interact to determine what eventually ends up in the
framebuffer). Modes are set, primitives specified, and other GL operations de-
scribed by sending commands in the form of function or procedure calls.
     Primitives are defined by a group of one or more vertices. A vertex defines a
point, an endpoint of an edge, or a corner of a polygon where two edges meet. Data
(consisting of positional coordinates, colors, normals, and texture coordinates) are
associated with a vertex and each vertex is processed independently, in order, and
in the same way. The only exception to this rule is if the group of vertices must
be clipped so that the indicated primitive fits within a specified region; in this
case vertex data may be modified and new vertices created. The type of clipping
depends on which primitive the group of vertices represents.
     Commands are always processed in the order in which they are received, al-
though there may be an indeterminate delay before the effects of a command are
realized. This means, for example, that one primitive must be drawn completely
before any subsequent one can affect the framebuffer. It also means that queries
and pixel read operations return state consistent with complete execution of all pre-
viously invoked GL commands. In general, the effects of a GL command on either

                                         4
2.1. OPENGL FUNDAMENTALS                                                          5


GL modes or the framebuffer must be complete before any subsequent command
can have any such effects.
     In the GL, data binding occurs on call. This means that data passed to a com-
mand are interpreted when that command is received. Even if the command re-
quires a pointer to data, those data are interpreted when the call is made, and any
subsequent changes to the data have no effect on the GL (unless the same pointer
is used in a subsequent command).
     The GL provides direct control over the fundamental operations of 3D and 2D
graphics. This includes specification of such parameters as transformation matri-
ces, lighting equation coefficients, antialiasing methods, and pixel update opera-
tors. It does not provide a means for describing or modeling complex geometric
objects. Another way to describe this situation is to say that the GL provides mech-
anisms to describe how complex geometric objects are to be rendered rather than
mechanisms to describe the complex objects themselves.
     The model for interpretation of GL commands is client-server. That is, a pro-
gram (the client) issues commands, and these commands are interpreted and pro-
cessed by the GL (the server). The server may or may not operate on the same
computer as the client. In this sense, the GL is “network-transparent.” A server
may maintain a number of GL contexts, each of which is an encapsulation of cur-
rent GL state. A client may choose to connect to any one of these contexts. Issuing
GL commands when the program is not connected to a context results in undefined
behavior.
     The effects of GL commands on the framebuffer are ultimately controlled by
the window system that allocates framebuffer resources. It is the window sys-
tem that determines which portions of the framebuffer the GL may access at any
given time and that communicates to the GL how those portions are structured.
Therefore, there are no GL commands to configure the framebuffer or initialize the
GL. Similarly, display of framebuffer contents on a CRT monitor (including the
transformation of individual framebuffer values by such techniques as gamma cor-
rection) is not addressed by the GL. Framebuffer configuration occurs outside of
the GL in conjunction with the window system; the initialization of a GL context
occurs when the window system allocates a window for GL rendering.
     The GL is designed to be run on a range of graphics platforms with varying
graphics capabilities and performance. To accommodate this variety, we specify
ideal behavior instead of actual behavior for certain GL operations. In cases where
deviation from the ideal is allowed, we also specify the rules that an implemen-
tation must obey if it is to approximate the ideal behavior usefully. This allowed
variation in GL behavior implies that two distinct GL implementations may not
agree pixel for pixel when presented with the same input even when run on identi-
cal framebuffer configurations.

                          Version 1.3 - August 14, 2001
6                                            CHAPTER 2. OPENGL OPERATION


    Finally, command names, constants, and types are prefixed in the GL (by gl,
GL , and GL, respectively in C) to reduce name clashes with other packages. The
prefixes are omitted in this document for clarity.


2.1.1   Floating-Point Computation
The GL must perform a number of floating-point operations during the course of
its operation. We do not specify how floating-point numbers are to be represented
or how operations on them are to be performed. We require simply that numbers’
floating-point parts contain enough bits and that their exponent fields are large
enough so that individual results of floating-point operations are accurate to about
1 part in 105 . The maximum representable magnitude of a floating-point number
used to represent positional or normal coordinates must be at least 232 ; the maxi-
mum representable magnitude for colors or texture coordinates must be at least 210 .
The maximum representable magnitude for all other floating-point values must be
at least 232 . x · 0 = 0 · x = 0 for any non-infinite and non-NaN x. 1 · x = x · 1 = x.
x + 0 = 0 + x = x. 00 = 1. (Occasionally further requirements will be specified.)
Most single-precision floating-point formats meet these requirements.
     Any representable floating-point value is legal as input to a GL command that
requires floating-point data. The result of providing a value that is not a floating-
point number to such a command is unspecified, but must not lead to GL interrup-
tion or termination. In IEEE arithmetic, for example, providing a negative zero or a
denormalized number to a GL command yields predictable results, while providing
a NaN or an infinity yields unspecified results.
     Some calculations require division. In such cases (including implied divisions
required by vector normalizations), a division by zero produces an unspecified re-
sult but must not lead to GL interruption or termination.


2.2     GL State
The GL maintains considerable state. This document enumerates each state vari-
able and describes how each variable can be changed. For purposes of discussion,
state variables are categorized somewhat arbitrarily by their function. Although we
describe the operations that the GL performs on the framebuffer, the framebuffer
is not a part of GL state.
    We distinguish two types of state. The first type of state, called GL server
state, resides in the GL server. The majority of GL state falls into this category.
The second type of state, called GL client state, resides in the GL client. Unless
otherwise specified, all state referred to in this document is GL server state; GL

                           Version 1.3 - August 14, 2001
2.3. GL COMMAND SYNTAX                                                                          7


client state is specifically identified. Each instance of a GL context implies one
complete set of GL server state; each connection from a client to a server implies
a set of both GL client state and GL server state.
    While an implementation of the GL may be hardware dependent, this discus-
sion is independent of the specific hardware on which a GL is implemented. We are
therefore concerned with the state of graphics hardware only when it corresponds
precisely to GL state.


2.3     GL Command Syntax
GL commands are functions or procedures. Various groups of commands perform
the same operation but differ in how arguments are supplied to them. To conve-
niently accommodate this variation, we adopt a notation for describing commands
and their arguments.
    GL commands are formed from a name followed, depending on the particular
command, by up to 4 characters. The first character indicates the number of values
of the indicated type that must be presented to the command. The second character
or character pair indicates the specific type of the arguments: 8-bit integer, 16-bit
integer, 32-bit integer, single-precision floating-point, or double-precision floating-
point. The final character, if present, is v, indicating that the command takes a
pointer to an array (a vector) of values rather than a series of individual arguments.
Two specific examples come from the Vertex command:

       void Vertex3f( float x, float y, float z );

and

       void Vertex2sv( short v[2] );

    These examples show the ANSI C declarations for these commands. In general,
a command declaration has the form1

       rtype Name{ 1234}{ b s i f d ub us ui}{ v}
                       ( [args ,] T arg1 , . . . , T argN [, args] );

rtype is the return type of the function. The braces ({}) enclose a series of char-
acters (or character pairs) of which one is selected. indicates no character. The
arguments enclosed in brackets ([args ,] and [, args]) may or may not be present.
   1
     The declarations shown in this document apply to ANSI C. Languages such as C++ and Ada
that allow passing of argument type information admit simpler declarations and fewer entry points.


                               Version 1.3 - August 14, 2001
8                                             CHAPTER 2. OPENGL OPERATION


                          Letter    Corresponding GL Type
                            b       byte
                            s       short
                            i       int
                            f       float
                            d       double
                           ub       ubyte
                           us       ushort
                           ui       uint

Table 2.1: Correspondence of command suffix letters to GL argument types. Refer
to Table 2.2 for definitions of the GL types.


The N arguments arg1 through argN have type T, which corresponds to one of the
type letters or letter pairs as indicated in Table 2.1 (if there are no letters, then the
arguments’ type is given explicitly). If the final character is not v, then N is given
by the digit 1, 2, 3, or 4 (if there is no digit, then the number of arguments is fixed).
If the final character is v, then only arg1 is present and it is an array of N values
of the indicated type. Finally, we indicate an unsigned type by the shorthand of
prepending a u to the beginning of the type name (so that, for instance, unsigned
char is abbreviated uchar).
     For example,
        void Normal3{fd}( T arg );
indicates the two declarations
        void Normal3f( float arg1, float arg2, float arg3 );
        void Normal3d( double arg1, double arg2, double arg3 );
while
        void Normal3{fd}v( T arg );
means the two declarations
        void Normal3fv( float arg[3] );
        void Normal3dv( double arg[3] );
    Arguments whose type is fixed (i.e. not indicated by a suffix on the command)
are of one of 14 types (or pointers to one of these). These types are summarized in
Table 2.2.

                            Version 1.3 - August 14, 2001
2.3. GL COMMAND SYNTAX                                                       9




       GL Type        Minimum     Description
                      Bit Width
       boolean            1       Boolean
       byte               8       signed 2’s complement binary integer
       ubyte              8       unsigned binary integer
       short              16      signed 2’s complement binary integer
       ushort             16      unsigned binary integer
       int                32      signed 2’s complement binary integer
       uint               32      unsigned binary integer
       sizei              32      Non-negative binary integer size
       enum               32      Enumerated binary integer value
       bitfield           32      Bit field
       float              32      Floating-point value
       clampf             32      Floating-point value clamped to [0, 1]
       double             64      Floating-point value
       clampd             64      Floating-point value clamped to [0, 1]

Table 2.2: GL data types. GL types are not C types. Thus, for example, GL
type int is referred to as GLint outside this document, and is not necessarily
equivalent to the C type int. An implementation may use more bits than the
number indicated in the table to represent a GL type. Correct interpretation of
integer values outside the minimum range is not required, however.




                         Version 1.3 - August 14, 2001
10                                                CHAPTER 2. OPENGL OPERATION




            Display
             List


                                    Per−Vertex
                                    Operations                 Per−
                                                   Rasteriz−
                      Evaluator                                Fragment     Framebuffer
                                    Primitive      ation
                                                               Operations
                                    Assembly



                                                   Texture
                                                   Memory

                                     Pixel
                                     Operations




     Figure 2.1. Block diagram of the GL.




2.4      Basic GL Operation
Figure 2.1 shows a schematic diagram of the GL. Commands enter the GL on the
left. Some commands specify geometric objects to be drawn while others control
how the objects are handled by the various stages. Most commands may be ac-
cumulated in a display list for processing by the GL at a later time. Otherwise,
commands are effectively sent through a processing pipeline.
     The first stage provides an efficient means for approximating curve and sur-
face geometry by evaluating polynomial functions of input values. The next stage
operates on geometric primitives described by vertices: points, line segments, and
polygons. In this stage vertices are transformed and lit, and primitives are clipped
to a viewing volume in preparation for the next stage, rasterization. The rasterizer
produces a series of framebuffer addresses and values using a two-dimensional de-
scription of a point, line segment, or polygon. Each fragment so produced is fed
to the next stage that performs operations on individual fragments before they fi-
nally alter the framebuffer. These operations include conditional updates into the
framebuffer based on incoming and previously stored depth values (to effect depth
buffering), blending of incoming fragment colors with stored colors, as well as
masking and other logical operations on fragment values.
     Finally, there is a way to bypass the vertex processing portion of the pipeline to
send a block of fragments directly to the individual fragment operations, eventually
causing a block of pixels to be written to the framebuffer; values may also be read

                                  Version 1.3 - August 14, 2001
2.5. GL ERRORS                                                                      11


back from the framebuffer or copied from one portion of the framebuffer to another.
These transfers may include some type of decoding or encoding.
    This ordering is meant only as a tool for describing the GL, not as a strict rule
of how the GL is implemented, and we present it only as a means to organize the
various operations of the GL. Objects such as curved surfaces, for instance, may
be transformed before they are converted to polygons.


2.5    GL Errors
The GL detects only a subset of those conditions that could be considered errors.
This is because in many cases error checking would adversely impact the perfor-
mance of an error-free program.
   The command

      enum GetError( void );

is used to obtain error information. Each detectable error is assigned a numeric
code. When an error is detected, a flag is set and the code is recorded. Further
errors, if they occur, do not affect this recorded code. When GetError is called,
the code is returned and the flag is cleared, so that a further error will again record
its code. If a call to GetError returns NO ERROR, then there has been no detectable
error since the last call to GetError (or since the GL was initialized).
     To allow for distributed implementations, there may be several flag-code pairs.
In this case, after a call to GetError returns a value other than NO ERROR each
subsequent call returns the non-zero code of a distinct flag-code pair (in unspecified
order), until all non-NO ERROR codes have been returned. When there are no more
non-NO ERROR error codes, all flags are reset. This scheme requires some positive
number of pairs of a flag bit and an integer. The initial state of all flags is cleared
and the initial value of all codes is NO ERROR.
     Table 2.3 summarizes GL errors. Currently, when an error flag is set, results of
GL operation are undefined only if OUT OF MEMORY has occurred. In other cases,
the command generating the error is ignored so that it has no effect on GL state or
framebuffer contents. If the generating command returns a value, it returns zero. If
the generating command modifies values through a pointer argument, no change is
made to these values. These error semantics apply only to GL errors, not to system
errors such as memory access errors. This behavior is the current behavior; the
action of the GL in the presence of errors is subject to change.
     Three error generation conditions are implicit in the description of every GL
command. First, if a command that requires an enumerated value is passed a sym-
bolic constant that is not one of those specified as allowable for that command, the

                           Version 1.3 - August 14, 2001
12                                           CHAPTER 2. OPENGL OPERATION


  Error                      Description                            Offending com-
                                                                    mand ignored?
  INVALID ENUM               enum argument out of range             Yes
  INVALID VALUE              Numeric argument out of range          Yes
  INVALID OPERATION          Operation illegal in current state     Yes
  STACK OVERFLOW             Command would cause a stack            Yes
                             overflow
  STACK UNDERFLOW            Command would cause a stack            Yes
                             underflow
  OUT OF MEMORY              Not enough memory left to exe-         Unknown
                             cute command
  TABLE TOO LARGE            The specified table is too large       Yes


                          Table 2.3: Summary of GL errors


error INVALID ENUM results. This is the case even if the argument is a pointer to
a symbolic constant if that value is not allowable for the given command. Second,
if a negative number is provided where an argument of type sizei is specified,
the error INVALID VALUE results. Finally, if memory is exhausted as a side effect
of the execution of a command, the error OUT OF MEMORY may be generated. Oth-
erwise errors are generated only for conditions that are explicitly described in this
specification.


2.6       Begin/End Paradigm
In the GL, most geometric objects are drawn by enclosing a series of coordinate
sets that specify vertices and optionally normals, texture coordinates, and colors
between Begin/End pairs. There are ten geometric objects that are drawn this
way: points, line segments, line segment loops, separated line segments, polygons,
triangle strips, triangle fans, separated triangles, quadrilateral strips, and separated
quadrilaterals.
    Each vertex is specified with two, three, or four coordinates. In addition, a
current normal, multiple current texture coordinate sets, and current color may
be used in processing each vertex. Normals are used by the GL in lighting cal-
culations; the current normal is a three-dimensional vector that may be set by
sending three coordinates that specify it. Texture coordinates determine how a
texture image is mapped onto a primitive. Multiple sets of texture coordinates
may be used to specify how multiple texture images are mapped onto a primitive.

                           Version 1.3 - August 14, 2001
2.6. BEGIN/END PARADIGM                                                            13


The number of texture units supported is implementation dependent but must be
at least two. The number of texture units supported can be queried with the state
MAX TEXTURE UNITS.
     Primary and secondary colors are associated with each vertex (see section 3.9).
These associated colors are either based on the current color or produced by light-
ing, depending on whether or not lighting is enabled. Texture coordinates are sim-
ilarly associated with each vertex. Multiple sets of texture coordinates may be
associated with a vertex. Figure 2.2 summarizes the association of auxiliary data
with a transformed vertex to produce a processed vertex.
     The current values are part of GL state. Vertices and normals are transformed,
colors may be affected or replaced by lighting, and texture coordinates are trans-
formed and possibly affected by a texture coordinate generation function. The
processing indicated for each current value is applied for each vertex that is sent to
the GL.
     The methods by which vertices, normals, texture coordinates, and colors are
sent to the GL, as well as how normals are transformed and how vertices are
mapped to the two-dimensional screen, are discussed later.
     Before colors have been assigned to a vertex, the state required by a vertex
is the vertex’s coordinates, the current normal, the current edge flag (see sec-
tion 2.6.2), the current material properties (see section 2.13.2), and the multiple
current texture coordinate sets. Because color assignment is done vertex-by-vertex,
a processed vertex comprises the vertex’s coordinates, its edge flag, its assigned
colors, and its multiple texture coordinate sets.
     Figure 2.3 shows the sequence of operations that builds a primitive (point, line
segment, or polygon) from a sequence of vertices. After a primitive is formed, it is
clipped to a viewing volume. This may alter the primitive by altering vertex coordi-
nates, texture coordinates, and colors. In the case of a polygon primitive, clipping
may insert new vertices into the primitive. The vertices defining a primitive to be
rasterized have texture coordinates and colors associated with them.

2.6.1    Begin and End Objects
Begin and End require one state variable with eleven values: one value for each
of the ten possible Begin/End objects, and one other value indicating that no Be-
gin/End object is being processed. The two relevant commands are

        void Begin( enum mode );
        void End( void );

There is no limit on the number of vertices that may be specified between a Begin
and an End.

                           Version 1.3 - August 14, 2001
14                                                     CHAPTER 2. OPENGL OPERATION



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

         Current                               lighting           Associated
        Color and                                                    Data
        Materials                                                (Colors, Edge Flag,
                                                                    and Texture
                                                                    Coordinates)
         Current
        Edge Flag


        Current
        Texture             texgen                 texture
                                                   matrix 0
       Coord Set 0




        Current
        Texture             texgen                 texture
                                                   matrix 1
       Coord Set 1




        Current
        Texture                                    texture
                            texgen
                                                   matrix 2
       Coord Set 2




        Current
        Texture             texgen                 texture
                                                   matrix 3
       Coord Set 3




     Figure 2.2. Association of current values with a vertex. The heavy lined boxes rep-
     resent GL state. Four texture units are shown; however, multitexturing may support
     a different number of units depending on the implementation.




                              Version 1.3 - August 14, 2001
2.6. BEGIN/END PARADIGM                                                                15



                                                      Point culling;
                                                      Line Segment
                Coordinates        Point,               or Polygon
                              Line Segment, or           Clipping
    Processed
                                  Polygon                              Rasterization
     Vertices   Associated       (Primitive)
                  Data           Assembly                 Color
                                                       Processing




                                 Begin/End
                                   State




   Figure 2.3. Primitive assembly and processing.




     Points. A series of individual points may be specified by calling Begin with an
argument value of POINTS. No special state need be kept between Begin and End
in this case, since each point is independent of previous and following points.
     Line Strips. A series of one or more connected line segments is specified by
enclosing a series of two or more endpoints within a Begin/End pair when Begin is
called with LINE STRIP. In this case, the first vertex specifies the first segment’s
start point while the second vertex specifies the first segment’s endpoint and the
second segment’s start point. In general, the ith vertex (for i > 1) specifies the
beginning of the ith segment and the end of the i − 1st. The last vertex specifies
the end of the last segment. If only one vertex is specified between the Begin/End
pair, then no primitive is generated.
     The required state consists of the processed vertex produced from the last ver-
tex that was sent (so that a line segment can be generated from it to the current
vertex), and a boolean flag indicating if the current vertex is the first vertex.
     Line Loops. Line loops, specified with the LINE LOOP argument value to
Begin, are the same as line strips except that a final segment is added from the final
specified vertex to the first vertex. The additional state consists of the processed
first vertex.
     Separate Lines. Individual line segments, each specified by a pair of vertices,
are generated by surrounding vertex pairs with Begin and End when the value
of the argument to Begin is LINES. In this case, the first two vertices between a
Begin and End pair define the first segment, with subsequent pairs of vertices each
defining one more segment. If the number of specified vertices is odd, then the last

                                  Version 1.3 - August 14, 2001
16                                             CHAPTER 2. OPENGL OPERATION


one is ignored. The state required is the same as for lines but it is used differently: a
vertex holding the first vertex of the current segment, and a boolean flag indicating
whether the current vertex is odd or even (a segment start or end).
     Polygons. A polygon is described by specifying its boundary as a series of
line segments. When Begin is called with POLYGON, the bounding line segments
are specified in the same way as line loops. Depending on the current state of the
GL, a polygon may be rendered in one of several ways such as outlining its border
or filling its interior. A polygon described with fewer than three vertices does not
generate a primitive.
     Only convex polygons are guaranteed to be drawn correctly by the GL. If a
specified polygon is nonconvex when projected onto the window, then the rendered
polygon need only lie within the convex hull of the projected vertices defining its
boundary.
     The state required to support polygons consists of at least two processed ver-
tices (more than two are never required, although an implementation may use
more); this is because a convex polygon can be rasterized as its vertices arrive,
before all of them have been specified. The order of the vertices is significant in
lighting and polygon rasterization (see sections 2.13.1 and 3.5.1).
     Triangle strips. A triangle strip is a series of triangles connected along shared
edges. A triangle strip is specified by giving a series of defining vertices between
a Begin/End pair when Begin is called with TRIANGLE STRIP. In this case, the
first three vertices define the first triangle (and their order is significant, just as for
polygons). Each subsequent vertex defines a new triangle using that point along
with two vertices from the previous triangle. A Begin/End pair enclosing fewer
than three vertices, when TRIANGLE STRIP has been supplied to Begin, produces
no primitive. See Figure 2.4.
     The state required to support triangle strips consists of a flag indicating if the
first triangle has been completed, two stored processed vertices, (called vertex A
and vertex B), and a one bit pointer indicating which stored vertex will be replaced
with the next vertex. After a Begin(TRIANGLE STRIP), the pointer is initialized
to point to vertex A. Each vertex sent between a Begin/End pair toggles the pointer.
Therefore, the first vertex is stored as vertex A, the second stored as vertex B, the
third stored as vertex A, and so on. Any vertex after the second one sent forms a
triangle from vertex A, vertex B, and the current vertex (in that order).
     Triangle fans. A triangle fan is the same as a triangle strip with one exception:
each vertex after the first always replaces vertex B of the two stored vertices. The
vertices of a triangle fan are enclosed between Begin and End when the value of
the argument to Begin is TRIANGLE FAN.
     Separate Triangles. Separate triangles are specified by placing vertices be-
tween Begin and End when the value of the argument to Begin is TRIANGLES. In

                            Version 1.3 - August 14, 2001
2.6. BEGIN/END PARADIGM                                                                       17




    2               4                 2                          2
                                                  3                                      6
                                                                           4
                                                      4

                                                          5                          5
    1           3            5        1                          1             3

             (a)                            (b)                                (c)


   Figure 2.4. (a) A triangle strip. (b) A triangle fan. (c) Independent triangles. The
   numbers give the sequencing of the vertices between Begin and End. Note that in
   (a) and (b) triangle edge ordering is determined by the first triangle, while in (c) the
   order of each triangle’s edges is independent of the other triangles.




this case, The 3i + 1st, 3i + 2nd, and 3i + 3rd vertices (in that order) determine
a triangle for each i = 0, 1, . . . , n − 1, where there are 3n + k vertices between
the Begin and End. k is either 0, 1, or 2; if k is not zero, the final k vertices are
ignored. For each triangle, vertex A is vertex 3i and vertex B is vertex 3i + 1.
Otherwise, separate triangles are the same as a triangle strip.
      The rules given for polygons also apply to each triangle generated from a tri-
angle strip, triangle fan or from separate triangles.
      Quadrilateral (quad) strips. Quad strips generate a series of edge-sharing
quadrilaterals from vertices appearing between Begin and End, when Begin is
called with QUAD STRIP. If the m vertices between the Begin and End are
v1 , . . . , vm , where vj is the jth specified vertex, then quad i has vertices (in or-
der) v2i , v2i+1 , v2i+3 , and v2i+2 with i = 0, . . . , m/2 . The state required is thus
three processed vertices, to store the last two vertices of the previous quad along
with the third vertex (the first new vertex) of the current quad, a flag to indicate
when the first quad has been completed, and a one-bit counter to count members
of a vertex pair. See Figure 2.5.
      A quad strip with fewer than four vertices generates no primitive. If the number
of vertices specified for a quadrilateral strip between Begin and End is odd, the
final vertex is ignored.
      Separate Quadrilaterals Separate quads are just like quad strips except that
each group of four vertices, the 4j + 1st, the 4j + 2nd, the 4j + 3rd, and the

                             Version 1.3 - August 14, 2001
18                                             CHAPTER 2. OPENGL OPERATION



              2          4         6              2         3     6        7




               1         3          5             1         4     5        8


                        (a)                                     (b)



     Figure 2.5. (a) A quad strip. (b) Independent quads. The numbers give the sequenc-
     ing of the vertices between Begin and End.




4j + 4th, generate a single quad, for j = 0, 1, . . . , n − 1. The total number of
vertices between Begin and End is 4n + k, where 0 ≤ k ≤ 3; if k is not zero, the
final k vertices are ignored. Separate quads are generated by calling Begin with
the argument value QUADS.
    The rules given for polygons also apply to each quad generated in a quad strip
or from separate quads.

2.6.2     Polygon Edges
Each edge of each primitive generated from a polygon, triangle strip, triangle fan,
separate triangle set, quadrilateral strip, or separate quadrilateral set, is flagged as
either boundary or non-boundary. These classifications are used during polygon
rasterization; some modes affect the interpretation of polygon boundary edges (see
section 3.5.4). By default, all edges are boundary edges, but the flagging of poly-
gons, separate triangles, or separate quadrilaterals may be altered by calling

        void EdgeFlag( boolean flag );
        void EdgeFlagv( boolean *flag );

to change the value of a flag bit. If flag is zero, then the flag bit is set to FALSE; if
flag is non-zero, then the flag bit is set to TRUE.
     When Begin is supplied with one of the argument values POLYGON, TRIAN-
GLES, or QUADS, each vertex specified within a Begin and End pair begins an edge.
If the edge flag bit is TRUE, then each specified vertex begins an edge that is flagged
as boundary. If the bit is FALSE, then induced edges are flagged as non-boundary.

                              Version 1.3 - August 14, 2001
2.7. VERTEX SPECIFICATION                                                              19


     The state required for edge flagging consists of one current flag bit. Initially, the
bit is TRUE. In addition, each processed vertex of an assembled polygonal primitive
must be augmented with a bit indicating whether or not the edge beginning on that
vertex is boundary or non-boundary.

2.6.3 GL Commands within Begin/End
The only GL commands that are allowed within any Begin/End pairs are the com-
mands for specifying vertex coordinates, vertex color, normal coordinates, and tex-
ture coordinates (Vertex, Color, Index, Normal, TexCoord), the ArrayElement
command (see section 2.8), the EvalCoord and EvalPoint commands (see sec-
tion 5.1), commands for specifying lighting material parameters (Material com-
mands; see section 2.13.2), display list invocation commands (CallList and Cal-
lLists; see section 5.4), and the EdgeFlag command. Executing any other GL
command between the execution of Begin and the corresponding execution of End
results in the error INVALID OPERATION. Executing Begin after Begin has already
been executed but before an End is executed generates the INVALID OPERATION
error, as does executing End without a previous corresponding Begin.
    Execution of the commands EnableClientState, DisableClientState, Push-
ClientAttrib, PopClientAttrib, EdgeFlagPointer, TexCoordPointer, Color-
Pointer, IndexPointer, NormalPointer, VertexPointer, InterleavedArrays, and
PixelStore, is not allowed within any Begin/End pair, but an error may or may not
be generated if such execution occurs. If an error is not generated, GL operation is
undefined. (These commands are described in sections 2.8, 3.6.1, and Chapter 6.)


2.7     Vertex Specification
Vertices are specified by giving their coordinates in two, three, or four dimensions.
This is done using one of several versions of the Vertex command:

      void Vertex{234}{sifd}( T coords );
      void Vertex{234}{sifd}v( T coords );

A call to any Vertex command specifies four coordinates: x, y, z, and w. The
x coordinate is the first coordinate, y is second, z is third, and w is fourth. A
call to Vertex2 sets the x and y coordinates; the z coordinate is implicitly set to
zero and the w coordinate to one. Vertex3 sets x, y, and z to the provided values
and w to one. Vertex4 sets all four coordinates, allowing the specification of an
arbitrary point in projective three-space. Invoking a Vertex command outside of a
Begin/End pair results in undefined behavior.

                            Version 1.3 - August 14, 2001
20                                          CHAPTER 2. OPENGL OPERATION


    Current values are used in associating auxiliary data with a vertex as described
in section 2.6. A current value may be changed at any time by issuing an appropri-
ate command. The commands

      void TexCoord{1234}{sifd}( T coords );
      void TexCoord{1234}{sifd}v( T coords );

specify the current homogeneous texture coordinates, named s, t, r, and q. The
TexCoord1 family of commands set the s coordinate to the provided single argu-
ment while setting t and r to 0 and q to 1. Similarly, TexCoord2 sets s and t to the
specified values, r to 0 and q to 1; TexCoord3 sets s, t, and r, with q set to 1, and
TexCoord4 sets all four texture coordinates.
    Implementations support more than one texture unit, and thus more than one
set of texture coordinates. The commands

      void MultiTexCoord{1234}{sifd}(enum texture,T coords)
      void MultiTexCoord{1234}{sifd}v(enum texture,T
         coords)

take the coordinate set to be modified as the texture parameter. texture is a symbolic
constant of the form TEXTUREi, indicating that texture coordinate set i is to be
modified. The constants obey TEXTUREi = TEXTURE0 + i (i is in the range 0 to
k − 1, where k is the implementation-dependent number of texture units defined
by MAX TEXTURE UNITS).
    The TexCoord commands are exactly equivalent to the corresponding Multi-
TexCoord commands with texture set to TEXTURE0.
    Gets of CURRENT TEXTURE COORDS return the texture coordinate set defined
by the value of ACTIVE TEXTURE.
    Specifying an invalid texture coordinate set for the texture argument of Multi-
TexCoord results in undefined behavior.
    The current normal is set using
      void Normal3{bsifd}( T coords );
      void Normal3{bsifd}v( T coords );
Byte, short, or integer values passed to Normal are converted to floating-point
values as indicated for the corresponding (signed) type in Table 2.6.
    Finally, there are several ways to set the current color. The GL stores both
a current single-valued color index, and a current four-valued RGBA color. One
or the other of these is significant depending as the GL is in color index mode or
RGBA mode. The mode selection is made when the GL is initialized.
    The command to set RGBA colors is

                           Version 1.3 - August 14, 2001
2.8. VERTEX ARRAYS                                                                   21


      void Color{34}{bsifd ubusui}( T components );
      void Color{34}{bsifd ubusui}v( T components );

The Color command has two major variants: Color3 and Color4. The four value
versions set all four values. The three value versions set R, G, and B to the provided
values; A is set to 1.0. (The conversion of integer color components (R, G, B, and
A) to floating-point values is discussed in section 2.13.)
    Versions of the Color command that take floating-point values accept values
nominally between 0.0 and 1.0. 0.0 corresponds to the minimum while 1.0 corre-
sponds to the maximum (machine dependent) value that a component may take on
in the framebuffer (see section 2.13 on colors and coloring). Values outside [0, 1]
are not clamped.
    The command

      void Index{sifd ub}( T index );
      void Index{sifd ub}v( T index );

updates the current (single-valued) color index. It takes one argument, the value
to which the current color index should be set. Values outside the (machine-
dependent) representable range of color indices are not clamped.
    The state required to support vertex specification consists of four floating-point
numbers to store the current texture coordinates s, t, r, and q, three floating-point
numbers to store the three coordinates of the current normal, four floating-point
values to store the current RGBA color, and one floating-point value to store the
current color index. There is no notion of a current vertex, so no state is devoted to
vertex coordinates. The initial values of s, t, and r of the current texture coordinates
are zero; the initial value of q is one. The initial current normal has coordinates
(0, 0, 1). The initial RGBA color is (R, G, B, A) = (1, 1, 1, 1). The initial color
index is 1.


2.8    Vertex Arrays
The vertex specification commands described in section 2.7 accept data in almost
any format, but their use requires many command executions to specify even simple
geometry. Vertex data may also be placed into arrays that are stored in the client’s
address space. Blocks of data in these arrays may then be used to specify multiple
geometric primitives through the execution of a single GL command. The client
may specify up to 5 plus the value of MAX TEXTURE UNITS arrays: one each to
store vertex coordinates, edge flags, colors, color indices, normals, and one or
more texture coordinate sets. The commands

                           Version 1.3 - August 14, 2001
22                                                   CHAPTER 2. OPENGL OPERATION


      void EdgeFlagPointer( sizei stride, void *pointer );

      void TexCoordPointer( int size, enum type, sizei stride,
         void *pointer );

      void ColorPointer( int size, enum type, sizei stride,
         void *pointer );

      void IndexPointer( enum type, sizei stride, void *pointer );

      void NormalPointer( enum type, sizei stride,
         void *pointer );

      void VertexPointer( int size, enum type, sizei stride,
         void *pointer );

describe the locations and organizations of these arrays. For each command, type
specifies the data type of the values stored in the array. Because edge flags are al-
ways type boolean, EdgeFlagPointer has no type argument. size, when present,
indicates the number of values per vertex that are stored in the array. Because
normals are always specified with three values, NormalPointer has no size argu-
ment. Likewise, because color indices and edge flags are always specified with
a single value, IndexPointer and EdgeFlagPointer also have no size argument.
Table 2.4 indicates the allowable values for size and type (when present). For type
the values BYTE, SHORT, INT, FLOAT, and DOUBLE indicate types byte, short,
int, float, and double, respectively; and the values UNSIGNED BYTE, UN-
SIGNED SHORT, and UNSIGNED INT indicate types ubyte, ushort, and uint,
respectively. The error INVALID VALUE is generated if size is specified with a
value other than that indicated in the table.
    The one, two, three, or four values in an array that correspond to a single vertex
comprise an array element. The values within each array element are stored se-
quentially in memory. If stride is specified as zero, then array elements are stored
sequentially as well. Otherwise pointers to the ith and (i+1)st elements of an array
differ by stride basic machine units (typically unsigned bytes), the pointer to the
(i + 1)st element being greater. For each command, pointer specifies the location
in memory of the first value of the first element of the array being specified.
    An individual array is enabled or disabled by calling one of

      void EnableClientState( enum array );
      void DisableClientState( enum array );

                               Version 1.3 - August 14, 2001
2.8. VERTEX ARRAYS                                                                   23


       Command                Sizes     Types
       VertexPointer          2,3,4     short, int, float, double
       NormalPointer            3       byte, short, int, float, dou-
                                        ble
       ColorPointer            3,4      byte, ubyte, short, ushort,
                                        int, uint, float, double
       IndexPointer             1       ubyte, short, int, float, dou-
                                        ble
       TexCoordPointer       1,2,3,4    short, int, float, double
       EdgeFlagPointer          1       boolean

          Table 2.4: Vertex array sizes (values per vertex) and data types.


with array set to EDGE FLAG ARRAY, TEXTURE COORD ARRAY, COLOR ARRAY,
INDEX ARRAY, NORMAL ARRAY, or VERTEX ARRAY, for the edge flag, texture co-
ordinate, color, color index, normal, or vertex array, respectively.
    The command

      void ClientActiveTexture( enum texture );

    is used to select the vertex array client state parameters to be modified by
the TexCoordPointer command and the array affected by EnableClientState and
DisableClientState with parameter TEXTURE COORD ARRAY. This command sets
the client state variable CLIENT ACTIVE TEXTURE. Each texture unit has a client
state vector which is selected when this command is invoked. This state vector in-
cludes the vertex array state. This call also selects which texture units’ client state
vector is used for queries of client state.
    Specifying an invalid texture generates the error INVALID ENUM. Valid values
of texture are the same as for the MultiTexCoord commands described in sec-
tion 2.7. .
    The ith element of every enabled array is transferred to the GL by calling

      void ArrayElement( int i );

For each enabled array, it is as though the corresponding command from section 2.7
or section 2.6.2 were called with a pointer to element i. For the vertex array, the cor-
responding command is Vertex[size][type]v, where size is one of [2,3,4], and type
is one of [s,i,f,d], corresponding to array types short, int, float, and dou-
ble respectively. The corresponding commands for the edge flag, texture coordi-
nate, color, color index, and normal arrays are EdgeFlagv, TexCoord[size][type]v,

                           Version 1.3 - August 14, 2001
24                                          CHAPTER 2. OPENGL OPERATION


Color[size][type]v, Index[type]v, and Normal[type]v, respectively. If the vertex
array is enabled, it is as though Vertex[size][type]v is executed last, after the exe-
cutions of the other corresponding commands.
    Changes made to array data between the execution of Begin and the corre-
sponding execution of End may affect calls to ArrayElement that are made within
the same Begin/End period in non-sequential ways. That is, a call to ArrayEle-
ment that precedes a change to array data may access the changed data, and a call
that follows a change to array data may access original data.
    The command
      void DrawArrays( enum mode, int first, sizei count );
constructs a sequence of geometric primitives using elements f irst through
f irst + count − 1 of each enabled array. mode specifies what kind of primi-
tives are constructed; it accepts the same token values as the mode parameter of
the Begin command. The effect of
         DrawArrays (mode, f irst, count);
is the same as the effect of the command sequence
         if (mode or count is invalid )
           generate appropriate error
         else {
           int i;
           Begin(mode);
           for (i=0; i < count ; i++)
             ArrayElement(f irst+ i);
           End();
         }
with one exception: the current edge flag, texture coordinates, color, color index,
and normal coordinates are each indeterminate after the execution of DrawArrays,
if the corresponding array is enabled. Current values corresponding to disabled
arrays are not modified by the execution of DrawArrays.
     The command
      void DrawElements( enum mode, sizei count, enum type,
         void *indices );
constructs a sequence of geometric primitives using the count elements whose
indices are stored in indices. type must be one of UNSIGNED BYTE, UN-
SIGNED SHORT, or UNSIGNED INT, indicating that the values in indices are in-
dices of GL type ubyte, ushort, or uint respectively. mode specifies what

                           Version 1.3 - August 14, 2001
2.8. VERTEX ARRAYS                                                              25


kind of primitives are constructed; it accepts the same token values as the mode
parameter of the Begin command. The effect of

         DrawElements (mode, count, type, indices);

is the same as the effect of the command sequence

         if (mode, count, or type is invalid )
           generate appropriate error
         else {
           int i;
           Begin(mode);
           for (i=0; i < count ; i++)
             ArrayElement(indices[i]);
           End();
         }

with one exception: the current edge flag, texture coordinates, color, color index,
and normal coordinates are each indeterminate after the execution of DrawEle-
ments, if the corresponding array is enabled. Current values corresponding to
disabled arrays are not modified by the execution of DrawElements.
    The command

      void DrawRangeElements( enum mode, uint start,
         uint end, sizei count, enum type, void *indices );

is a restricted form of DrawElements. mode, count, type, and indices match the
corresponding arguments to DrawElements, with the additional constraint that all
values in the array indices must lie between start and end inclusive.
    Implementations denote recommended maximum amounts of vertex and index
data, which may be queried by calling GetIntegerv with the symbolic constants
MAX ELEMENTS VERTICES and MAX ELEMENTS INDICES. If end − start + 1 is
greater than the value of MAX ELEMENTS VERTICES, or if count is greater than
the value of MAX ELEMENTS INDICES, then the call may operate at reduced per-
formance. There is no requirement that all vertices in the range [start, end] be
referenced. However, the implementation may partially process unused vertices,
reducing performance from what could be achieved with an optimal index set.
    The error INVALID VALUE is generated if end < start. Invalid mode, count,
or type parameters generate the same errors as would the corresponding call to
DrawElements. It is an error for indices to lie outside the range [start, end], but

                          Version 1.3 - August 14, 2001
26                                                  CHAPTER 2. OPENGL OPERATION


implementations may not check for this. Such indices will cause implementation-
dependent behavior.
   The command

       void InterleavedArrays( enum format, sizei stride,
          void *pointer );

efficiently initializes the six arrays and their enables to one of 14 con-
figurations.       format must be one of 14 symbolic constants:       V2F,
V3F, C4UB V2F, C4UB V3F, C3F V3F, N3F V3F, C4F N3F V3F, T2F V3F,
T4F V4F, T2F C4UB V3F, T2F C3F V3F, T2F N3F V3F, T2F C4F N3F V3F, or
T4F C4F N3F V4F.
     The effect of

          InterleavedArrays(f ormat, stride, pointer);

     is the same as the effect of the command sequence

          if (f ormat or stride is invalid)
            generate appropriate error
          else {
            int str;
            set et , ec , en , st , sc , sv , tc , pc , pn , pv , and s as a function
               of Table 2.5 and the value of f ormat.
            str = stride;
            if (str is zero)
               str = s;
            DisableClientState(EDGE FLAG ARRAY);
            DisableClientState(INDEX ARRAY);
            if (et ) {
               EnableClientState(TEXTURE COORD ARRAY);
               TexCoordPointer(st , FLOAT, str, pointer);
            } else {
               DisableClientState(TEXTURE COORD ARRAY);
            }
            if (ec ) {
               EnableClientState(COLOR ARRAY);
               ColorPointer(sc , tc , str, pointer + pc );
            } else {
               DisableClientState(COLOR ARRAY);
            }

                               Version 1.3 - August 14, 2001
2.8. VERTEX ARRAYS                                                           27




 f ormat              et           ec      en     st   sc   sv        tc
 V2F                 False        False   False             2
 V3F                 False        False   False             3
 C4UB V2F            False        True    False        4    2    UNSIGNED BYTE
 C4UB V3F            False        True    False        4    3    UNSIGNED BYTE
 C3F V3F             False        True    False        3    3        FLOAT
 N3F V3F             False        False   True              3
 C4F N3F V3F         False        True    True         4    3       FLOAT
 T2F V3F             True         False   False   2         3
 T4F V4F             True         False   False   4         4
 T2F C4UB V3F        True         True    False   2    4    3    UNSIGNED BYTE
 T2F C3F V3F         True         True    False   2    3    3        FLOAT
 T2F N3F V3F         True         False   True    2         3
 T2F C4F N3F V3F     True         True    True    2    4    3       FLOAT
 T4F C4F N3F V4F     True         True    True    4    4    4       FLOAT

 f ormat             pc      pn        pv        s
 V2F                                    0       2f
 V3F                                    0       3f
 C4UB V2F            0                  c     c + 2f
 C4UB V3F            0                  c     c + 3f
 C3F V3F             0                 3f       6f
 N3F V3F                      0        3f       6f
 C4F N3F V3F         0       4f        7f       10f
 T2F V3F                               2f       5f
 T4F V4F                               4f       8f
 T2F C4UB V3F        2f             c + 2f    c + 5f
 T2F C3F V3F         2f                5f       8f
 T2F N3F V3F                 2f        5f       8f
 T2F C4F N3F V3F     2f      6f        9f       12f
 T4F C4F N3F V4F     4f      8f       11f       15f

Table 2.5: Variables that direct the execution of InterleavedArrays. f is
sizeof(FLOAT). c is 4 times sizeof(UNSIGNED BYTE), rounded up to
the nearest multiple of f . All pointer arithmetic is performed in units of
sizeof(UNSIGNED BYTE).




                          Version 1.3 - August 14, 2001
28                                         CHAPTER 2. OPENGL OPERATION


             if (en ) {
               EnableClientState(NORMAL ARRAY);
               NormalPointer(FLOAT, str, pointer + pn );
             } else {
               DisableClientState(NORMAL ARRAY);
             }
             EnableClientState(VERTEX ARRAY);
             VertexPointer(sv , FLOAT, str, pointer + pv );
         }

     If the number of supported texture units (the value of MAX TEXTURE UNITS) is
k, then the client state required to implement vertex arrays consists of 5+k boolean
values, 5+k memory pointers, 5+k integer stride values, 4+k symbolic constants
representing array types, and 3 + k integers representing values per element. In the
initial state, the boolean values are each disabled, the memory pointers are each
null, the strides are each zero, the array types are each FLOAT, and the integers
representing values per element are each four.


2.9    Rectangles
There is a set of GL commands to support efficient specification of rectangles as
two corner vertices.

      void Rect{sifd}( T x1, T y1, T x2, T y2 );
      void Rect{sifd}v( T v1[2], T v2[2] );

Each command takes either four arguments organized as two consecutive pairs of
(x, y) coordinates, or two pointers to arrays each of which contains an x value
followed by a y value. The effect of the Rect command
         Rect (x1 , y1 , x2 , y2 );
is exactly the same as the following sequence of commands:
         Begin(POLYGON);
           Vertex2(x1 , y1 );
           Vertex2(x2 , y1 );
           Vertex2(x2 , y2 );
           Vertex2(x1 , y2 );
         End();
The appropriate Vertex2 command would be invoked depending on which of the
Rect commands is issued.

                           Version 1.3 - August 14, 2001
2.10. COORDINATE TRANSFORMATIONS                                                                     29



                                                                                       Normalized
      Object      Model−View      Eye        Projection      Clip        Perspective     Device
    Coordinates                Coordinates                Coordinates     Division     Coordinates
                   Matrix                     Matrix




                                                                           Viewport     Window
                                                                        Transformation Coordinates




   Figure 2.6. Vertex transformation sequence.




2.10      Coordinate Transformations

Vertices, normals, and texture coordinates are transformed before their coordinates
are used to produce an image in the framebuffer. We begin with a description of
how vertex coordinates are transformed and how this transformation is controlled.
    Figure 2.6 diagrams the sequence of transformations that are applied to ver-
tices. The vertex coordinates that are presented to the GL are termed object co-
ordinates. The model-view matrix is applied to these coordinates to yield eye co-
ordinates. Then another matrix, called the projection matrix, is applied to eye
coordinates to yield clip coordinates. A perspective division is carried out on clip
coordinates to yield normalized device coordinates. A final viewport transforma-
tion is applied to convert these coordinates into window coordinates.
   Object coordinates, eye coordinates, and clip coordinates are four-dimensional,
consisting of x, y, z, and w coordinates (in that order). The model-view and per-
spective matrices are thus 4 × 4.
                                                   xo
                                                                   
                                                  yo 
   If a vertex in object coordinates is given by 
                                                  zo  and the model-view matrix
                                                      

                                                   wo

                                Version 1.3 - August 14, 2001
30                                              CHAPTER 2. OPENGL OPERATION


is M , then the vertex’s eye coordinates are found as
                                  xe          xo
                                                   
                                 ye        yo 
                                 z e  = M  zo  .
                                              

                                  we          wo
Similarly, if P is the projection matrix, then the vertex’s clip coordinates are
                                  xc         xe
                                                  
                                 yc       ye 
                                 zc  = P  ze  .
                                             

                                  wc         we
The vertex’s normalized device coordinates are then
                                  xd       xc /wc
                                                   
                                 yd  =  yc /wc  .
                                  zd       zc /wc

2.10.1    Controlling the Viewport
The viewport transformation is determined by the viewport’s width and height in
pixels, px and py , respectively, and its center (ox , oy ) (also in pixels). The vertex’s
                         xw
                            

window coordinates,  yw , are given by
                         zw

                      xw             (px /2)xd + ox
                                                               
                     yw  =        (py /2)yd + oy       .
                      zw       [(f − n)/2]zd + (n + f )/2
The factor and offset applied to zd encoded by n and f are set using

      void DepthRange( clampd n, clampd f );

Each of n and f are clamped to lie within [0, 1], as are all arguments of type clampd
or clampf. zw is taken to be represented in fixed-point with at least as many bits
as there are in the depth buffer of the framebuffer. We assume that the fixed-point
representation used represents each value k/(2m − 1), where k ∈ {0, 1, . . . , 2m −
1}, as k (e.g. 1.0 is represented in binary as a string of all ones).
    Viewport transformation parameters are specified using

      void Viewport( int x, int y, sizei w, sizei h );

                            Version 1.3 - August 14, 2001
2.10. COORDINATE TRANSFORMATIONS                                                  31


where x and y give the x and y window coordinates of the viewport’s lower left
corner and w and h give the viewport’s width and height, respectively. The viewport
parameters shown in the above equations are found from these values as ox =
x + w/2 and oy = y + h/2; px = w, py = h.
    Viewport width and height are clamped to implementation-dependent maxi-
mums when specified. The maximum width and height may be found by issuing
an appropriate Get command (see Chapter 6). The maximum viewport dimen-
sions must be greater than or equal to the visible dimensions of the display being
rendered to. INVALID VALUE is generated if either w or h is negative.
    The state required to implement the viewport transformation is 6 integers. In
the initial state, w and h are set to the width and height, respectively, of the win-
dow into which the GL is to do its rendering. ox and oy are set to w/2 and h/2,
respectively. n and f are set to 0.0 and 1.0, respectively.

2.10.2   Matrices
The projection matrix and model-view matrix are set and modified with a variety
of commands. The affected matrix is determined by the current matrix mode. The
current matrix mode is set with

      void MatrixMode( enum mode );

which takes one of the pre-defined constants TEXTURE, MODELVIEW, COLOR, or
PROJECTION as the argument value. TEXTURE is described later in section 2.10.2,
and COLORis described in section 3.6.3. If the current matrix mode is MODELVIEW,
then matrix operations apply to the model-view matrix; if PROJECTION, then they
apply to the projection matrix.
    The two basic commands for affecting the current matrix are

      void LoadMatrix{fd}( T m[16] );
      void MultMatrix{fd}( T m[16] );

LoadMatrix takes a pointer to a 4 × 4 matrix stored in column-major order as 16
consecutive floating-point values, i.e. as

                                 a1 a5 a9 a13
                                                   
                               a2 a6 a10 a14 
                               a3 a7 a11 a15  .
                                                   

                                 a4 a8 a12 a16
(This differs from the standard row-major C ordering for matrix elements. If the
standard ordering is used, all of the subsequent transformation equations are trans-
posed, and the columns representing vectors become rows.)

                          Version 1.3 - August 14, 2001
32                                             CHAPTER 2. OPENGL OPERATION


     The specified matrix replaces the current matrix with the one pointed to. Mult-
Matrix takes the same type argument as LoadMatrix, but multiplies the current
matrix by the one pointed to and replaces the current matrix with the product. If C
is the current matrix and M is the matrix pointed to by MultMatrix’s argument,
then the resulting current matrix, C , is

                                       C = C · M.

     The commands
       void LoadTransposeMatrix{fd}( T m[16] );
       void MultTransposeMatrix{fd}( T m[16] );
take pointers to 4×4 matrices stored in row-major order as 16 consecutive floating-
point values, i.e. as

                                 a1      a2    a3     a4
                                                           
                                a5      a6    a7     a8 
                                                         .
                                a9      a10   a11    a12 
                                 a13     a14   a15    a16
     The effect of
          LoadTransposeMatrix[fd](m);
is the same as the effect of

          LoadMatrix[fd](mT );

     The effect of
          MultTransposeMatrix[fd](m);
is the same as the effect of

          MultMatrix[fd](mT );

     The command
       void LoadIdentity( void );
effectively calls LoadMatrix with the identity matrix:

                                     1    0    0     0
                                                     
                                   0     1    0     0
                                                      .
                                   0     0    1     0
                                     0    0    0     1

                           Version 1.3 - August 14, 2001
2.10. COORDINATE TRANSFORMATIONS                                                 33


    There are a variety of other commands that manipulate matrices. Rotate,
Translate, Scale, Frustum, and Ortho manipulate the current matrix. Each com-
putes a matrix and then invokes MultMatrix with this matrix. In the case of

       void Rotate{fd}( T θ, T x, T y, T z );

θ gives an angle of rotation in degrees; the coordinates of a vector v are given by
v = (x y z)T . The computed matrix is a counter-clockwise rotation about the line
through the origin with the specified axis when that axis is pointing up (i.e. the
right-hand rule determines the sense of the rotation angle). The matrix is thus

                                                0
                                                   
                                
                                         R     0.
                                               0
                                    0     0   0 1
Let u = v/||v|| = ( x    y    z )T . If
                                 0            −z      y
                                                         

                             S= z             0     −x 
                                −y            x       0
then
                      R = uuT + cos θ(I − uuT ) + sin θS.
   The arguments to

       void Translate{fd}( T x, T y, T z );

give the coordinates of a translation vector as (x y z)T . The resulting matrix is a
translation by the specified vector:
                                  1       0   0    x
                                                   
                                0        1   0    y
                                                    .
                                0        0   1    z
                                  0       0   0    1
       void Scale{fd}( T x, T y, T z );

produces a general scaling along the x-, y-, and z- axes. The corresponding matrix
is
                                  x 0 0 0
                                               
                               0 y 0 0
                               0 0 z 0.
                                               

                                  0 0 0 1
   For

                          Version 1.3 - August 14, 2001
34                                                        CHAPTER 2. OPENGL OPERATION


      void Frustum( double l, double r, double b, double t,
         double n, double f );

the coordinates (l b − n)T and (r t − n)T specify the points on the near clipping
plane that are mapped to the lower left and upper right corners of the window,
respectively (assuming that the eye is located at (0 0 0)T ). f gives the distance
from the eye to the far clipping plane. If either n or f is less than or equal to zero,
l is equal to r, b is equal to t, or n is equal to f , the error INVALID VALUE results.
The corresponding matrix is
                              2n              r+l
                                       0                 0
                                                                
                              r−l             r−l
                           0          2n     t+b
                                      t−b     t−b        0       
                                                                 .
                                                                
                                             − ff +n   − f2f−n
                                                             n
                          
                           0          0                         
                                                  −n
                              0        0      −1          0

      void Ortho( double l, double r, double b, double t,
         double n, double f );

describes a matrix that produces parallel projection. (l b − n)T and (r t − n)T
specify the points on the near clipping plane that are mapped to the lower left and
upper right corners of the window, respectively. f gives the distance from the eye
to the far clipping plane. If l is equal to r, b is equal to t, or n is equal to f , the
error INVALID VALUE results. The corresponding matrix is
                               2
                                       0       0       − r+l
                                                                
                              r−l                        r−l
                                       2
                           0
                                     t−b      0       − t+b  
                                                         t−b  .
                                                2       f +n 
                           0          0     − f −n    − f −n 
                              0        0       0         1

   For each texture unit, a 4 × 4 matrix is applied to the corresponding texture
coordinates. This matrix is applied as

                           m1        m5     m9     m13     s
                                                        
                          m2        m6     m10    m14  t
                                                       ,
                          m3        m7     m11    m15   r 
                           m4        m8     m12    m16     q
where the left matrix is the current texture matrix. The matrix is applied to the
coordinates resulting from texture coordinate generation (which may simply be the
current texture coordinates), and the resulting transformed coordinates become the
texture coordinates associated with a vertex. Setting the matrix mode to TEXTURE
causes the already described matrix operations to apply to the texture matrix.

                                    Version 1.3 - August 14, 2001
2.10. COORDINATE TRANSFORMATIONS                                                   35


    There is also a corresponding texture matrix stack for each texture unit. To
change the stack affected by matrix operations, set the active texture unit selector
by calling

      void ActiveTexture( enum texture );

The selector also affects calls modifying texture environment state, texture coordi-
nate generation state, texture binding state, and queries of all these state values as
well as current texture coordinates and current raster texture coordinates.
     Specifying an invalid texture generates the error INVALID ENUM. Valid values
of texture are the same as for the MultiTexCoord commands described in sec-
tion 2.7.
     The active texture unit selector may be queried by calling GetIntegerv with
pname set to ACTIVE TEXTURE.
     There is a stack of matrices for each of matrix modes MODELVIEW, PROJEC-
TION, and COLOR, and for each texture unit. For MODELVIEW mode, the stack depth
is at least 32 (that is, there is a stack of at least 32 model-view matrices). For the
other modes, the depth is at least 2. Texture matrix stacks for all texture units have
the same depth. The current matrix in any mode is the matrix on the top of the
stack for that mode.
      void PushMatrix( void );
pushes the stack down by one, duplicating the current matrix in both the top of the
stack and the entry below it.
      void PopMatrix( void );
pops the top entry off of the stack, replacing the current matrix with the matrix
that was the second entry in the stack. The pushing or popping takes place on the
stack corresponding to the current matrix mode. Popping a matrix off a stack with
only one entry generates the error STACK UNDERFLOW; pushing a matrix onto a full
stack generates STACK OVERFLOW.
    When the current matrix mode is TEXTURE, the texture matrix stack of the
active texture unit is pushed or popped.
    The state required to implement transformations consists of a four-valued in-
teger indicating the current matrix mode, one stack of at least two 4 × 4 matrices
for each of COLOR; PROJECTION; each texture unit, TEXTURE; and a stack of at
least 32 4 × 4 matrices for MODELVIEW. Each matrix stack has an associated stack
pointer. Initially, there is only one matrix on each stack, and all matrices are set
to the identity. The initial matrix mode is MODELVIEW. The initial value of AC-
TIVE TEXTURE is TEXTURE0.

                           Version 1.3 - August 14, 2001
36                                           CHAPTER 2. OPENGL OPERATION


2.10.3   Normal Transformation
Finally, we consider how the model-view matrix and transformation state affect
normals. Before use in lighting, normals are transformed to eye coordinates by a
matrix derived from the model-view matrix. Rescaling and normalization opera-
tions are performed on the transformed normals to make them unit length prior to
use in lighting. Rescaling and normalization are controlled by

      void Enable( enum target );

and

      void Disable( enum target );

with target equal to RESCALE NORMAL or NORMALIZE. This requires two bits of
state. The initial state is for normals not to be rescaled or normalized.
    If the model-view matrix is M , then the normal is transformed to eye coordi-
nates by:

              ( nx     ny     nz     q ) = ( nx   ny   nz   q ) · M −1
            x
            
          y
where, if 
           z  are the associated vertex coordinates, then
              

            w           
                        
                        
                        
                           0,                         w = 0,
                                              x
                                            
                        
                   q=      −( nx ny nz ) y                                      (2.1)
                        
                        
                        
                                             z
                        
                                      w           , w=0
    Implementations may choose instead to transform ( nx        ny    nz ) to eye coor-
dinates using

                  ( nx      ny     nz ) = ( nx    ny   nz ) · Mu −1
where Mu is the upper leftmost 3x3 matrix taken from M .
   Rescale multiplies the transformed normals by a scale factor

                     ( nx    ny      nz ) = f ( nx     ny    nz )
If rescaling is disabled, then f = 1. If rescaling is enabled, then f is computed
as (mij denotes the matrix element in row i and column j of M −1 , numbering the
topmost row of the matrix as row 1 and the leftmost column as column 1)

                            Version 1.3 - August 14, 2001
2.10. COORDINATE TRANSFORMATIONS                                                   37



                                           1
                           f=√
                                   m31 + m32 2 + m33 2
                                         2

    Note that if the normals sent to GL were unit length and the model-view matrix
uniformly scales space, then rescale makes the transformed normals unit length.
    Alternatively, an implementation may chose f as
                                               1
                            f=
                                    nx + ny 2 + nz
                                         2                     2

recomputing f for each normal. This makes all non-zero length normals unit length
regardless of their input length and the nature of the model-view matrix.
    After rescaling, the final transformed normal used in lighting, nf , is computed
as

                            nf = m ( nx        ny        nz )
If normalization is disabled, then m = 1. Otherwise
                                               1
                           m=
                                         2          2              2
                                    nx       + ny       + nz
    Because we specify neither the floating-point format nor the means for matrix
inversion, we cannot specify behavior in the case of a poorly-conditioned (nearly
singular) model-view matrix M . In case of an exactly singular matrix, the trans-
formed normal is undefined. If the GL implementation determines that the model-
view matrix is uninvertible, then the entries in the inverted matrix are arbitrary. In
any case, neither normal transformation nor use of the transformed normal may
lead to GL interruption or termination.

2.10.4 Generating Texture Coordinates
Texture coordinates associated with a vertex may either be taken from the current
texture coordinates or generated according to a function dependent on vertex coor-
dinates. The command

      void TexGen{ifd}( enum coord, enum pname, T param );
      void TexGen{ifd}v( enum coord, enum pname, T params );

controls texture coordinate generation. coord must be one of the constants S, T,
R, or Q, indicating that the pertinent coordinate is the s, t, r, or q coordinate, re-
spectively. In the first form of the command, param is a symbolic constant speci-
fying a single-valued texture generation parameter; in the second form, params is

                           Version 1.3 - August 14, 2001
38                                               CHAPTER 2. OPENGL OPERATION


a pointer to an array of values that specify texture generation parameters. pname
must be one of the three symbolic constants TEXTURE GEN MODE, OBJECT PLANE,
or EYE PLANE. If pname is TEXTURE GEN MODE, then either params points to
or param is an integer that is one of the symbolic constants OBJECT LINEAR,
EYE LINEAR, SPHERE MAP, REFLECTION MAP, or NORMAL MAP.
    If TEXTURE GEN MODE indicates OBJECT LINEAR, then the generation func-
tion for the coordinate indicated by coord is

                           g = p1 xo + p2 yo + p3 zo + p4 wo .

xo , yo , zo , and wo are the object coordinates of the vertex. p1 , . . . , p4 are specified
by calling TexGen with pname set to OBJECT PLANE in which case params points
to an array containing p1 , . . . , p4 . There is a distinct group of plane equation co-
efficients for each texture coordinate; coord indicates the coordinate to which the
specified coefficients pertain.
     If TEXTURE GEN MODE indicates EYE LINEAR, then the function is

                           g = p1 xe + p2 ye + p3 ze + p4 we

where
                   ( p1   p2    p3     p 4 ) = ( p1   p2   p3   p4 ) M −1
xe , ye , ze , and we are the eye coordinates of the vertex. p1 , . . . , p4 are set by
calling TexGen with pname set to EYE PLANE in correspondence with setting the
coefficients in the OBJECT PLANE case. M is the model-view matrix in effect
when p1 , . . . , p4 are specified. Computed texture coordinates may be inaccurate or
undefined if M is poorly conditioned or singular.
     When used with a suitably constructed texture image, calling TexGen with
TEXTURE GEN MODE indicating SPHERE MAP can simulate the reflected image of
a spherical environment on a polygon. SPHERE MAP texture coordinates are gen-
erated as follows. Denote the unit vector pointing from the origin to the vertex
(in eye coordinates) by u. Denote the current normal, after transformation to eye
coordinates, by n . Let r = ( rx ry rz )T , the reflection vector, be given by

                                     r = u − 2n T n u ,

and let m = 2 rx2 + ry2 + (rz + 1)2 . Then the value assigned to an s coordinate
(the first TexGen argument value is S) is s = rx /m + 12 ; the value assigned to a t
coordinate is t = ry /m + 12 . Calling TexGen with a coord of either R or Q when
pname indicates SPHERE MAP generates the error INVALID ENUM.
    If TEXTURE GEN MODE indicates REFLECTION MAP, compute the reflection
vector r as described for the SPHERE MAP mode. Then the value assigned to an

                               Version 1.3 - August 14, 2001
2.11. CLIPPING                                                                        39


s coordinate is s = rx ; the value assigned to a t coordinate is t = ry ; and the value
assigned to an r coordinate is r = rz . Calling TexGen with a coord of Q when
pname indicates REFLECTION MAP generates the error INVALID ENUM.
    If TEXTURE GEN MODE indicates NORMAL MAP, compute the normal vector nf
as described in section 2.10.3. Then the value assigned to an s coordinate is s =
nf x ; the value assigned to a t coordinate is t = nf y ; and the value assigned to an
r coordinate is r = nf z (the values nf x , nf y , and nf z are the components of nf .)
Calling TexGen with a coord of Q when pname indicates NORMAL MAP generates
the error INVALID ENUM.
    A texture coordinate generation function is enabled or disabled using En-
able and Disable with an argument of TEXTURE GEN S, TEXTURE GEN T, TEX-
TURE GEN R, or TEXTURE GEN Q (each indicates the corresponding texture coor-
dinate). When enabled, the specified texture coordinate is computed according
to the current EYE LINEAR, OBJECT LINEAR or SPHERE MAP specification, de-
pending on the current setting of TEXTURE GEN MODE for that coordinate. When
disabled, subsequent vertices will take the indicated texture coordinate from the
current texture coordinates.
    The state required for texture coordinate generation for each texture unit com-
prises a five-valued integer for each coordinate indicating coordinate generation
mode, and a bit for each coordinate to indicate whether texture coordinate genera-
tion is enabled or disabled. In addition, four coefficients are required for the four
coordinates for each of EYE LINEAR and OBJECT LINEAR. The initial state has the
texture generation function disabled for all texture coordinates. The initial values
of pi for s are all 0 except p1 which is one; for t all the pi are zero except p2 , which
is 1. The values of pi for r and q are all 0. These values of pi apply for both the
EYE LINEAR and OBJECT LINEAR versions. Initially all texture generation modes
are EYE LINEAR.


2.11     Clipping
Primitives are clipped to the clip volume. In clip coordinates, the view volume is
defined by
                                 −wc ≤ xc ≤ wc
                                  −wc ≤ yc ≤ wc .
                                  −wc ≤ zc ≤ wc

This view volume may be further restricted by as many as n client-defined clip
planes to generate the clip volume. (n is an implementation dependent maximum
that must be at least 6.) Each client-defined plane specifies a half-space. The clip

                            Version 1.3 - August 14, 2001
40                                             CHAPTER 2. OPENGL OPERATION


volume is the intersection of all such half-spaces with the view volume (if there no
client-defined clip planes are enabled, the clip volume is the view volume).
    A client-defined clip plane is specified with

      void ClipPlane( enum p, double eqn[4] );

The value of the first argument, p, is a symbolic constant, CLIP PLANEi, where i is
an integer between 0 and n − 1, indicating one of n client-defined clip planes. eqn
is an array of four double-precision floating-point values. These are the coefficients
of a plane equation in object coordinates: p1 , p2 , p3 , and p4 (in that order). The
inverse of the current model-view matrix is applied to these coefficients, at the time
they are specified, yielding

                  ( p1   p2    p3    p 4 ) = ( p1   p2   p3   p4 ) M −1

(where M is the current model-view matrix; the resulting plane equation is unde-
fined if M is singular and may be inaccurate if M is poorly-conditioned) to obtain
the plane equation coefficients in eye coordinates. All points with eye coordinates
( xe ye ze we )T that satisfy

                                                     xe
                                                        
                                                    ye 
                          ( p1      p2   p3         ze  ≥ 0
                                              p4 )     

                                                     we

lie in the half-space defined by the plane; points that do not satisfy this condition
do not lie in the half-space.
     Client-defined clip planes are enabled with the generic Enable command and
disabled with the Disable command. The value of the argument to either com-
mand is CLIP PLANEi where i is an integer between 0 and n; specifying a value
of i enables or disables the plane equation with index i. The constants obey
CLIP PLANEi = CLIP PLANE0 + i.
     If the primitive under consideration is a point, then clipping passes it un-
changed if it lies within the clip volume; otherwise, it is discarded. If the prim-
itive is a line segment, then clipping does nothing to it if it lies entirely within the
clip volume and discards it if it lies entirely outside the volume. If part of the line
segment lies in the volume and part lies outside, then the line segment is clipped
and new vertex coordinates are computed for one or both vertices. A clipped line
segment endpoint lies on both the original line segment and the boundary of the
clip volume.

                              Version 1.3 - August 14, 2001
2.11. CLIPPING                                                                        41


   This clipping produces a value, 0 ≤ t ≤ 1, for each clipped vertex. If the
coordinates of a clipped vertex are P and the original vertices’ coordinates are P1
and P2 , then t is given by


                               P = tP1 + (1 − t)P2 .


The value of t is used in color and texture coordinate clipping (section 2.13.8).
    If the primitive is a polygon, then it is passed if every one of its edges lies
entirely inside the clip volume and either clipped or discarded otherwise. Polygon
clipping may cause polygon edges to be clipped, but because polygon connectivity
must be maintained, these clipped edges are connected by new edges that lie along
the clip volume’s boundary. Thus, clipping may require the introduction of new
vertices into a polygon. Edge flags are associated with these vertices so that edges
introduced by clipping are flagged as boundary (edge flag TRUE), and so that orig-
inal edges of the polygon that become cut off at these vertices retain their original
flags.
    If it happens that a polygon intersects an edge of the clip volume’s boundary,
then the clipped polygon must include a point on this boundary edge. This point
must lie in the intersection of the boundary edge and the convex hull of the vertices
of the original polygon. We impose this requirement because the polygon may not
be exactly planar.
    A line segment or polygon whose vertices have wc values of differing signs
may generate multiple connected components after clipping. GL implementations
are not required to handle this situation. That is, only the portion of the primitive
that lies in the region of wc > 0 need be produced by clipping.
    Primitives rendered with clip planes must satisfy a complementarity crite-
rion. Suppose a single clip plane with coefficients ( p1 p2 p3 p4 ) (or a num-
ber of similarly specified clip planes) is enabled and a series of primitives are
drawn. Next, suppose that the original clip plane is respecified with coefficients
( −p1 −p2 −p3 −p4 ) (and correspondingly for any other clip planes) and
the primitives are drawn again (and the GL is otherwise in the same state). In this
case, primitives must not be missing any pixels, nor may any pixels be drawn twice
in regions where those primitives are cut by the clip planes.
     The state required for clipping is at least 6 sets of plane equations (each consist-
ing of four double-precision floating-point coefficients) and at least 6 correspond-
ing bits indicating which of these client-defined plane equations are enabled. In the
initial state, all client-defined plane equation coefficients are zero and all planes are
disabled.

                            Version 1.3 - August 14, 2001
42                                            CHAPTER 2. OPENGL OPERATION


2.12     Current Raster Position
The current raster position is used by commands that directly affect pixels in the
framebuffer. These commands, which bypass vertex transformation and primitive
assembly, are described in the next chapter. The current raster position, however,
shares some of the characteristics of a vertex.
    The state required for the current raster position consists of three window co-
ordinates xw , yw , and zw , a clip coordinate wc value, an eye coordinate distance, a
valid bit, and associated data consisting of a color and multiple texture coordinate
sets. It is set using one of the RasterPos commands:

       void RasterPos{234}{sifd}( T coords );
       void RasterPos{234}{sifd}v( T coords );

RasterPos4 takes four values indicating x, y, z, and w. RasterPos3 (or Raster-
Pos2) is analogous, but sets only x, y, and z with w implicitly set to 1 (or only x
and y with z implicitly set to 0 and w implicitly set to 1).
    Gets of CURRENT RASTER TEXTURE COORDS are affected by the setting of the
state ACTIVE TEXTURE.
    The coordinates are treated as if they were specified in a Vertex command.
The x, y, z, and w coordinates are transformed by the current model-view and
perspective matrices. These coordinates, along with current values, are used to
generate a color and texture coordinates just as is done for a vertex. The color and
texture coordinates so produced replace the color and texture coordinates stored in
the current raster position’s associated data. The distance from the origin of the
eye coordinate system to the vertex as transformed by only the current model-view
matrix replaces the current raster distance. This distance can be approximated (see
section 3.10).
    The transformed coordinates are passed to clipping as if they represented a
point. If the “point” is not culled, then the projection to window coordinates is
computed (section 2.10) and saved as the current raster position, and the valid
bit is set. If the “point” is culled, the current raster position and its associated
data become indeterminate and the valid bit is cleared. Figure 2.7 summarizes the
behavior of the current raster position.
    The current raster position requires five single-precision floating-point values
for its xw , yw , and zw window coordinates, its wc clip coordinate, and its eye
coordinate distance, a single valid bit, a color (RGBA and color index), and texture
coordinates for each texture unit. In the initial state, the coordinates and texture
coordinates are all (0, 0, 0, 1), the eye coordinate distance is 0, the valid bit is set,
the associated RGBA color is (1, 1, 1, 1) and the associated color index color is 1.

                            Version 1.3 - August 14, 2001
2.12. CURRENT RASTER POSITION                                                         43




                                                              Valid
    Rasterpos In                  Clip        Project
                                                                Raster
                           Vertex/Normal                       Position
      Current              Transformation
      Normal

                                                                Raster
      Current                      Lighting                    Distance
      Color &
      Materials
                                                              Associated
                                                Texture          Data
     Current                 Texgen             Matrix 0
     Texture                                                               Current
    Coord Set 0                                                             Raster
                                                                           Position
                                                Texture
     Current                 Texgen             Matrix 1
     Texture
    Coord Set 1

                                                Texture
     Current                 Texgen             Matrix 2
     Texture
    Coord Set 2

                                                Texture
     Current                 Texgen             Matrix 3
     Texture
    Coord Set 3




  Figure 2.7. The current raster position and how it is set. Four texture units are
  shown; however, multitexturing may support a different number of units depending
  on the implementation.




                          Version 1.3 - August 14, 2001
44                                               CHAPTER 2. OPENGL OPERATION




       [0,2k−1]      Convert to
                      [0.0,1.0]             Current
                                            RGBA                            Clamp to
                                             Color        Lighting          [0.0, 1.0]
                     Convert to
     [−2k,2k−1]
                     [−1.0,1.0]
          float
                                                       Color
                                                      Clipping


                               Convert to                            Flatshade?
                              fixed−point
                                                      Primitive
                                                      Clipping




     Figure 2.8. Processing of RGBA colors. The heavy dotted lines indicate both pri-
     mary and secondary vertex colors, which are processed in the same fashion. See
     Table 2.6 for the interpretation of k.




In RGBA mode, the associated color index always has its initial value; in color
index mode, the RGBA color always maintains its initial value.


2.13 Colors and Coloring
Figures 2.8 and 2.9 diagram the processing of RGBA colors and color indices be-
fore rasterization. Incoming colors arrive in one of several formats. Table 2.6 sum-
marizes the conversions that take place on R, G, B, and A components depending
on which version of the Color command was invoked to specify the components.
As a result of limited precision, some converted values will not be represented
exactly. In color index mode, a single-valued color index is not mapped.
    Next, lighting, if enabled, produces either a color index or primary and sec-
ondary colors. If lighting is disabled, the current color index or color is used in
further processing (the current color is the primary color, and the secondary color
is (0, 0, 0, 0)). After lighting, RGBA colors are clamped to the range [0, 1]. A
color index is converted to fixed-point and then its integer portion is masked (see
section 2.13.6). After clamping or masking, a primitive may be flatshaded, indi-
cating that all vertices of the primitive are to have the same color. Finally, if a
primitive is clipped, then colors (and texture coordinates) must be computed at the

                             Version 1.3 - August 14, 2001
2.13. COLORS AND COLORING                                                                 45




    [0,2n−1]       Convert to
                                      Current
                     float
                                       Color                                Mask to
       float                           Index        Lighting                [0.0, 2n−1]



                                                 Color
                                                Clipping


                         Convert to                                 Flatshade?
                        fixed−point
                                                Primitive
                                                Clipping




   Figure 2.9. Processing of color indices. n is the number of bits in a color index.




                            GL Type          Conversion
                            ubyte            c/(28 − 1)
                            byte         (2c + 1)/(28 − 1)
                            ushort           c/(216 − 1)
                            short        (2c + 1)/(216 − 1)
                            uint             c/(232 − 1)
                            int          (2c + 1)/(232 − 1)
                            float                 c
                            double                c

Table 2.6: Component conversions. Color, normal, and depth components, (c),
are converted to an internal floating-point representation, (f ), using the equations
in this table. All arithmetic is done in the internal floating point format. These
conversions apply to components specified as parameters to GL commands and to
components in pixel data. The equations remain the same even if the implemented
ranges of the GL data types are greater than the minimum required ranges. (Refer
to table 2.2)




                            Version 1.3 - August 14, 2001
46                                            CHAPTER 2. OPENGL OPERATION


vertices introduced or modified by clipping.

2.13.1     Lighting
GL lighting computes colors for each vertex sent to the GL. This is accomplished
by applying an equation defined by a client-specified lighting model to a collection
of parameters that can include the vertex coordinates, the coordinates of one or
more light sources, the current normal, and parameters defining the characteristics
of the light sources and a current material. The following discussion assumes that
the GL is in RGBA mode. (Color index lighting is described in section 2.13.5.)
    Lighting may be in one of two states:

     1. Lighting Off. In this state, the current color is assigned to the vertex primary
        color. The secondary color is (0, 0, 0, 0).

     2. Lighting On. In this state, the vertex primary and secondary colors are com-
        puted from the current lighting parameters.

Lighting is turned on or off using the generic Enable or Disable commands with
the symbolic value LIGHTING.

Lighting Operation
A lighting parameter is of one of five types: color, position, direction, real, or
boolean. A color parameter consists of four floating-point values, one for each of
R, G, B, and A, in that order. There are no restrictions on the allowable values for
these parameters. A position parameter consists of four floating-point coordinates
(x, y, z, and w) that specify a position in object coordinates (w may be zero,
indicating a point at infinity in the direction given by x, y, and z). A direction
parameter consists of three floating-point coordinates (x, y, and z) that specify a
direction in object coordinates. A real parameter is one floating-point value. The
various values and their types are summarized in Table 2.7. The result of a lighting
computation is undefined if a value for a parameter is specified that is outside the
range given for that parameter in the table.
    There are n light sources, indexed by i = 0, . . . , n−1. (n is an implementation
dependent maximum that must be at least 8.) Note that the default values for dcli
and scli differ for i = 0 and i > 0.
    Before specifying the way that lighting computes colors, we introduce oper-
ators and notation that simplify the expressions involved. If c1 and c2 are col-
ors without alpha where c1 = (r1 , g1 , b1 ) and c2 = (r2 , g2 , b2 ), then define
c1 ∗ c2 = (r1 r2 , g1 g2 , b1 b2 ). Addition of colors is accomplished by addition of

                             Version 1.3 - August 14, 2001
2.13. COLORS AND COLORING                                                           47


 Parameter      Type          Default Value        Description
 Material Parameters
    acm         color       (0.2, 0.2, 0.2, 1.0)   ambient color of material
    dcm         color       (0.8, 0.8, 0.8, 1.0)   diffuse color of material
    scm         color       (0.0, 0.0, 0.0, 1.0)   specular color of material
    ecm         color       (0.0, 0.0, 0.0, 1.0)   emissive color of material
    srm          real               0.0            specular exponent (range:
                                                   [0.0, 128.0])
      am          real              0.0            ambient color index
      dm          real              1.0            diffuse color index
       sm         real              1.0            specular color index
 Light Source Parameters
      acli       color      (0.0, 0.0, 0.0, 1.0)   ambient intensity of light i
 dcli (i = 0)    color      (1.0, 1.0, 1.0, 1.0)   diffuse intensity of light 0
 dcli (i > 0)    color      (0.0, 0.0, 0.0, 1.0)   diffuse intensity of light i
 scli (i = 0)    color      (1.0, 1.0, 1.0, 1.0)   specular intensity of light 0
 scli (i > 0)    color      (0.0, 0.0, 0.0, 1.0)   specular intensity of light i
     Ppli      position     (0.0, 0.0, 1.0, 0.0)   position of light i
      sdli     direction     (0.0, 0.0, −1.0)      direction of spotlight for light i
      srli        real              0.0            spotlight exponent for light i
                                                   (range: [0.0, 128.0])
     crli         real            180.0            spotlight cutoff angle for light i
                                                   (range: [0.0, 90.0], 180.0)
     k0i          real              1.0            constant attenuation factor for
                                                   light i (range: [0.0, ∞))
     k1i          real              0.0            linear attenuation factor for
                                                   light i (range: [0.0, ∞))
     k2i          real              0.0            quadratic attenuation factor for
                                                   light i (range: [0.0, ∞))
 Lighting Model Parameters
    acs         color    (0.2, 0.2, 0.2, 1.0)      ambient color of scene
     vbs      boolean          FALSE               viewer assumed to be at
                                                   (0, 0, 0) in eye coordinates
                                                   (TRUE) or (0, 0, ∞) (FALSE)
     ces         enum        SINGLE COLOR          controls computation of colors
     tbs        boolean         FALSE              use two-sided lighting mode

Table 2.7: Summary of lighting parameters. The range of individual color compo-
nents is (−∞, +∞).


                           Version 1.3 - August 14, 2001
48                                              CHAPTER 2. OPENGL OPERATION


the components. Multiplication of colors by a scalar means multiplying each com-
ponent by that scalar. If d1 and d2 are directions, then define
                            d1       d2 = max{d1 · d2 , 0}.
(Directions are taken to have three coordinates.) If P1 and P2 are (homogeneous,
                                         −−−→
with four coordinates) points then let P1 P2 be the unit vector that points from P1
to P2 . Note that if P2 has a zero w coordinate and P1 has non-zero w coordinate,
      −−−→
then P1 P2 is the unit vector corresponding to the direction specified by the x, y,
and z coordinates of P2 ; if P1 has a zero w coordinate and P2 has a non-zero w
                  −−−→
coordinate then P1 P2 is the unit vector that is the negative of that corresponding
to the direction specified by P1 . If both P1 and P2 have zero w coordinates, then
−−−→
P1 P2 is the unit vector obtained by normalizing the direction corresponding to
P2 − P 1 .
                                              ˆ be the unit vector in d’s direction. Let
     If d is an arbitrary direction, then let d
  P1 P2 be the distance between P1 and P2 . Finally, let V be the point corre-
sponding to the vertex being lit, and n be the corresponding normal. Let Pe be the
eyepoint ((0, 0, 0, 1) in eye coordinates).
     Lighting produces two colors at a vertex: a primary color cpri and a secondary
color csec . The values of cpri and csec depend on the light model color control, ces .
If ces = SINGLE COLOR, then the equations to compute cpri and csec are


              cpri = ecm
                     + acm ∗ acs
                          n−1
                     +     (atti )(spoti ) [acm ∗ acli
                                                −−→
                          i=0        + (n VPpli )dcm ∗ dcli
                                     + (fi )(n h     ˆ i )srm scm ∗ scli ]
              csec   = (0, 0, 0, 0)
     If ces = SEPARATE SPECULAR COLOR, then


               cpri = ecm
                      + acm ∗ acs
                          n−1
                      +          (atti )(spoti ) [acm ∗ acli
                                                      −−→
                           i=0             + (n VPpli )dcm ∗ dcli ]
                          n−1
               csec =            (atti )(spoti )(fi )(n   ˆ i )srm scm ∗ scli
                                                          h
                           i=0


                            Version 1.3 - August 14, 2001
2.13. COLORS AND COLORING                                                               49


    where

                          −−→
                   1, n VPpli = 0,
      fi =                                                                           (2.2)
                   0, otherwise,



                   −−→     −−→
                   VPpli + VPe ,             vbs = TRUE,
      hi =         −−→                                                               (2.3)
                   VPpli + ( 0 0      1 )T , vbs = FALSE,



                                  1
               
                                                          2,   if Ppli ’s w = 0,
               
                   k0i + k1i VPpli + k2i VPpli
               
    atti =                                                                           (2.4)
               
               
                                     1.0,                      otherwise.


                −−−→                                     −−−→
                (Ppli V
                             ˆsdli )srli , crli = 180.0, Ppli V   ˆsdli ≥ cos(crli ),
                                                          −−−→
  spoti =                  0.0,             crli = 180.0, Ppli V   ˆsdli < cos(crli ),(2.5)
               
               
                           1.0,             crli = 180.0.
                                                                                     (2.6)


All computations are carried out in eye coordinates.
     The value of A produced by lighting is the alpha value associated with dcm . A
is always associated with the primary color cpri ; the alpha component of csec is 0.
Results of lighting are undefined if the we coordinate (w in eye coordinates) of V
is zero.
    Lighting may operate in two-sided mode (tbs = TRUE), in which a front color
is computed with one set of material parameters (the front material) and a back
color is computed with a second set of material parameters (the back material).
This second computation replaces n with −n. If tbs = FALSE, then the back color
and front color are both assigned the color computed using the front material with
n.
    The selection between back color and front color depends on the primitive of
which the vertex being lit is a part. If the primitive is a point or a line segment,
the front color is always selected. If it is a polygon, then the selection is based on
the sign of the (clipped or unclipped) polygon’s signed area computed in window

                            Version 1.3 - August 14, 2001
50                                           CHAPTER 2. OPENGL OPERATION


coordinates. One way to compute this area is

                                 1 n−1 i i⊕1
                            a=        x y    − xi⊕1
                                                w yw
                                                    i
                                                                                 (2.7)
                                 2 i=0 w w

where xiw and yw i are the x and y window coordinates of the ith vertex of the

n-vertex polygon (vertices are numbered starting at zero for purposes of this com-
putation) and i ⊕ 1 is (i + 1) mod n. The interpretation of the sign of this value is
controlled with

      void FrontFace( enum dir );

Setting dir to CCW (corresponding to counter-clockwise orientation of the projected
polygon in window coordinates) indicates that if a ≤ 0, then the color of each
vertex of the polygon becomes the back color computed for that vertex while if
a > 0, then the front color is selected. If dir is CW, then a is replaced by −a in the
above inequalities. This requires one bit of state; initially, it indicates CCW.

2.13.2    Lighting Parameter Specification
Lighting parameters are divided into three categories: material parameters, light
source parameters, and lighting model parameters (see Table 2.7). Sets of lighting
parameters are specified with

      void    Material{if}( enum face, enum pname, T param );
      void    Material{if}v( enum face, enum pname, T params );
      void    Light{if}( enum light, enum pname, T param );
      void    Light{if}v( enum light, enum pname, T params );
      void    LightModel{if}( enum pname, T param );
      void    LightModel{if}v( enum pname, T params );

pname is a symbolic constant indicating which parameter is to be set (see Ta-
ble 2.8). In the vector versions of the commands, params is a pointer to a group
of values to which to set the indicated parameter. The number of values pointed to
depends on the parameter being set. In the non-vector versions, param is a value to
which to set a single-valued parameter. (If param corresponds to a multi-valued pa-
rameter, the error INVALID ENUM results.) For the Material command, face must
be one of FRONT, BACK, or FRONT AND BACK, indicating that the property name of
the front or back material, or both, respectively, should be set. In the case of Light,
light is a symbolic constant of the form LIGHTi, indicating that light i is to have
the specified parameter set. The constants obey LIGHTi = LIGHT0 + i.

                           Version 1.3 - August 14, 2001
2.13. COLORS AND COLORING                                                        51


    Table 2.8 gives, for each of the three parameter groups, the correspondence
between the pre-defined constant names and their names in the lighting equations,
along with the number of values that must be specified with each. Color param-
eters specified with Material and Light are converted to floating-point values (if
specified as integers) as indicated in Table 2.6 for signed integers. The error IN-
VALID VALUE occurs if a specified lighting parameter lies outside the allowable
range given in Table 2.7. (The symbol “∞” indicates the maximum representable
magnitude for the indicated type.)
    The current model-view matrix is applied to the position parameter indicated
with Light for a particular light source when that position is specified. These
transformed values are the values used in the lighting equation.
    The spotlight direction is transformed when it is specified using only the upper
leftmost 3x3 portion of the model-view matrix. That is, if Mu is the upper left 3x3
matrix taken from the current model-view matrix M , then the spotlight direction
                                         dx
                                          
                                        dy 
                                         dz
is transformed to
                                dx         dx
                                               
                               d  = Mu  d y  .
                                 y
                                dz         dz
   An individual light is enabled or disabled by calling Enable or Disable with the
symbolic value LIGHTi (i is in the range 0 to n − 1, where n is the implementation-
dependent number of lights). If light i is disabled, the ith term in the lighting
equation is effectively removed from the summation.

2.13.3 ColorMaterial
It is possible to attach one or more material properties to the current color, so
that they continuously track its component values. This behavior is enabled and
disabled by calling Enable or Disable with the symbolic value COLOR MATERIAL.
     The command that controls which of these modes is selected is
      void ColorMaterial( enum face, enum mode );
face is one of FRONT, BACK, or FRONT AND BACK, indicating whether the front
material, back material, or both are affected by the current color. mode is one
of EMISSION, AMBIENT, DIFFUSE, SPECULAR, or AMBIENT AND DIFFUSE and
specifies which material property or properties track the current color. If mode is
EMISSION, AMBIENT, DIFFUSE, or SPECULAR, then the value of ecm , acm , dcm or

                          Version 1.3 - August 14, 2001
52                                   CHAPTER 2. OPENGL OPERATION




      Parameter                 Name                  Number of values
     Material Parameters (Material)
         acm                   AMBIENT                       4
         dcm                   DIFFUSE                       4
      acm , dcm        AMBIENT AND DIFFUSE                   4
         scm                  SPECULAR                       4
         ecm                  EMISSION                       4
         srm                 SHININESS                       1
     am , dm , sm          COLOR INDEXES                     3
     Light Source Parameters (Light)
         acli                  AMBIENT                       4
         dcli                  DIFFUSE                       4
          scli                SPECULAR                       4
         Ppli                 POSITION                       4
         sdli             SPOT DIRECTION                     3
         srli              SPOT EXPONENT                     1
          crli              SPOT CUTOFF                      1
          k0          CONSTANT ATTENUATION                   1
          k1           LINEAR ATTENUATION                    1
          k2         QUADRATIC ATTENUATION                   1
     Lighting Model Parameters (LightModel)
          acs          LIGHT MODEL AMBIENT                   4
          vbs       LIGHT MODEL LOCAL VIEWER                 1
          tbs         LIGHT MODEL TWO SIDE                   1
          ces      LIGHT MODEL COLOR CONTROL                 1


Table 2.8: Correspondence of lighting parameter symbols to names. AMBI-
ENT AND DIFFUSE is used to set acm and dcm to the same value.




                      Version 1.3 - August 14, 2001
2.13. COLORS AND COLORING                                                                                                    53




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




  Figure 2.10. ColorMaterial operation. Material properties are continuously up-
  dated from the current color while ColorMaterial is enabled and has the appro-
  priate mode. Only the front material properties are included in this figure. The
  back material properties are treated identically, except that face must be BACK or
  FRONT AND BACK.




                                   Version 1.3 - August 14, 2001
54                                             CHAPTER 2. OPENGL OPERATION


scm , respectively, will track the current color. If mode is AMBIENT AND DIFFUSE,
both acm and dcm track the current color. The replacements made to material prop-
erties are permanent; the replaced values remain until changed by either sending a
new color or by setting a new material value when ColorMaterial is not currently
enabled to override that particular value. When COLOR MATERIAL is enabled, the
indicated parameter or parameters always track the current color. For instance,
calling

      ColorMaterial(FRONT, AMBIENT)

while COLOR MATERIAL is enabled sets the front material acm to the value of the
current color.

2.13.4   Lighting State
The state required for lighting consists of all of the lighting parameters (front
and back material parameters, lighting model parameters, and at least 8 sets of
light parameters), a bit indicating whether a back color distinct from the front
color should be computed, at least 8 bits to indicate which lights are enabled,
a five-valued variable indicating the current ColorMaterial mode, a bit indicat-
ing whether or not COLOR MATERIAL is enabled, and a single bit to indicate
whether lighting is enabled or disabled. In the initial state, all lighting parame-
ters have their default values. Back color evaluation does not take place, Color-
Material is FRONT AND BACK and AMBIENT AND DIFFUSE, and both lighting and
COLOR MATERIAL are disabled.


2.13.5   Color Index Lighting
A simplified lighting computation applies in color index mode that uses many of
the parameters controlling RGBA lighting, but none of the RGBA material param-
eters. First, the RGBA diffuse and specular intensities of light i (dcli and scli ,
respectively) determine color index diffuse and specular light intensities, dli and
sli from
                dli = (.30)R(dcli ) + (.59)G(dcli ) + (.11)B(dcli )
and
                sli = (.30)R(scli ) + (.59)G(scli ) + (.11)B(scli ).
R(x) indicates the R component of the color x and similarly for G(x) and B(x).
   Next, let
                          n
                    s=         (atti )(spoti )(sli )(fi )(n   ˆ i )srm
                                                              h
                         i=0


                          Version 1.3 - August 14, 2001
2.13. COLORS AND COLORING                                                          55


where atti and spoti are given by equations 2.4 and 2.5, respectively, and fi and
ˆ i are given by equations 2.2 and 2.3, respectively. Let s = min{s, 1}. Finally,
h
let
                           n
                                                      −−→
                      d=      (atti )(spoti )(dli )(n VPpli ).
                           i=0
Then color index lighting produces a value c, given by
                 c = am + d(1 − s )(dm − am ) + s (sm − am ).
The final color index is
                                 c = min{c, sm }.
The values am , dm and sm are material properties described in Tables 2.7 and 2.8.
Any ambient light intensities are incorporated into am . As with RGBA lighting,
disabled lights cause the corresponding terms from the summations to be omitted.
The interpretation of tbs and the calculation of front and back colors is carried out
as has already been described for RGBA lighting.
    The values am , dm , and sm are set with Material using a pname of
COLOR INDEXES. Their initial values are 0, 1, and 1, respectively. The additional
state consists of three floating-point values. These values have no effect on RGBA
lighting.

2.13.6    Clamping or Masking
After lighting (whether enabled or not), all components of both primary and sec-
ondary colors are clamped to the range [0, 1].
    For a color index, the index is first converted to fixed-point with an unspecified
number of bits to the right of the binary point; the nearest fixed-point value is
selected. Then, the bits to the right of the binary point are left alone while the
integer portion is masked (bitwise ANDed) with 2n − 1, where n is the number of
bits in a color in the color index buffer (buffers are discussed in chapter 4).

2.13.7    Flatshading
A primitive may be flatshaded, meaning that all vertices of the primitive are as-
signed the same color index or the same primary and secondary colors. These
colors are the colors of the vertex that spawned the primitive. For a point, these
are the colors associated with the point. For a line segment, they are the colors of
the second (final) vertex of the segment. For a polygon, they come from a selected
vertex depending on how the polygon was generated. Table 2.9 summarizes the
possibilities.
    Flatshading is controlled by

                           Version 1.3 - August 14, 2001
56                                            CHAPTER 2. OPENGL OPERATION


                     Primitive type of polygon i            Vertex
                     single polygon (i ≡ 1)                    1
                     triangle strip                          i+2
                     triangle fan                            i+2
                     independent triangle                     3i
                     quad strip                             2i + 2
                     independent quad                         4i


Table 2.9: Polygon flatshading color selection. The colors used for flatshading
the ith polygon generated by the indicated Begin/End type are derived from the
current color (if lighting is disabled) in effect when the indicated vertex is specified.
If lighting is enabled, the colors are produced by lighting the indicated vertex.
Vertices are numbered 1 through n, where n is the number of vertices between the
Begin/End pair.


      void ShadeModel( enum mode );

mode value must be either of the symbolic constants SMOOTH or FLAT. If mode is
SMOOTH (the initial state), vertex colors are treated individually. If mode is FLAT,
flatshading is turned on. ShadeModel thus requires one bit of state.

2.13.8    Color and Texture Coordinate Clipping
After lighting, clamping or masking and possible flatshading, colors are clipped.
Those colors associated with a vertex that lies within the clip volume are unaffected
by clipping. If a primitive is clipped, however, the colors assigned to vertices
produced by clipping are clipped colors.
    Let the colors assigned to the two vertices P1 and P2 of an unclipped edge be
c1 and c2 . The value of t (section 2.11) for a clipped point P is used to obtain the
color associated with P as

                                 c = tc1 + (1 − t)c2 .
(For a color index color, multiplying a color by a scalar means multiplying the
index by the scalar. For an RGBA color, it means multiplying each of R, G, B, and
A by the scalar. Both primary and secondary colors are treated in the same fashion.)
Polygon clipping may create a clipped vertex along an edge of the clip volume’s
boundary. This situation is handled by noting that polygon clipping proceeds by
clipping against one plane of the clip volume’s boundary at a time. Color clipping

                            Version 1.3 - August 14, 2001
2.13. COLORS AND COLORING                                                          57


is done in the same way, so that clipped points always occur at the intersection of
polygon edges (possibly already clipped) with the clip volume’s boundary.
    Texture coordinates must also be clipped when a primitive is clipped. The
method is exactly analogous to that used for color clipping.

2.13.9    Final Color Processing
For an RGBA color, each color component (which lies in [0, 1]) is converted
(by rounding to nearest) to a fixed-point value with m bits. We assume that
the fixed-point representation used represents each value k/(2m − 1), where
k ∈ {0, 1, . . . , 2m − 1}, as k (e.g. 1.0 is represented in binary as a string of
all ones). m must be at least as large as the number of bits in the corresponding
component of the framebuffer. m must be at least 2 for A if the framebuffer does
not contain an A component, or if there is only 1 bit of A in the framebuffer. A
color index is converted (by rounding to nearest) to a fixed-point value with at least
as many bits as there are in the color index portion of the framebuffer.
    Because a number of the form k/(2m − 1) may not be represented exactly as
a limited-precision floating-point quantity, we place a further requirement on the
fixed-point conversion of RGBA components. Suppose that lighting is disabled, the
color associated with a vertex has not been clipped, and one of Colorub, Colorus,
or Colorui was used to specify that color. When these conditions are satisfied, an
RGBA component must convert to a value that matches the component as specified
in the Color command: if m is less than the number of bits b with which the
component was specified, then the converted value must equal the most significant
m bits of the specified value; otherwise, the most significant b bits of the converted
value must equal the specified value.




                           Version 1.3 - August 14, 2001
Chapter 3

Rasterization

Rasterization is the process by which a primitive is converted to a two-dimensional
image. Each point of this image contains such information as color and depth.
Thus, rasterizing a primitive consists of two parts. The first is to determine which
squares of an integer grid in window coordinates are occupied by the primitive.
The second is assigning a color and a depth value to each such square. The results
of this process are passed on to the next stage of the GL (per-fragment operations),
which uses the information to update the appropriate locations in the framebuffer.
Figure 3.1 diagrams the rasterization process.

    A grid square along with its parameters of assigned color, z (depth), and texture
coordinates is called a fragment; the parameters are collectively dubbed the frag-
ment’s associated data. A fragment is located by its lower left corner, which lies on
integer grid coordinates. Rasterization operations also refer to a fragment’s center,
which is offset by (1/2, 1/2) from its lower left corner (and so lies on half-integer
coordinates).

    Grid squares need not actually be square in the GL. Rasterization rules are not
affected by the actual aspect ratio of the grid squares. Display of non-square grids,
however, will cause rasterized points and line segments to appear fatter in one
direction than the other. We assume that fragments are square, since it simplifies
antialiasing and texturing.

   Several factors affect rasterization. Lines and polygons may be stippled. Points
may be given differing diameters and line segments differing widths. A point, line
segment, or polygon may be antialiased.

                                         58
                                                                           59




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
       DrawPixels        Rectangle
                        Rasterization



                          Bitmap
          Bitmap                                     Fog
                        Rasterization
                                                               Fragments




Figure 3.1. Rasterization.




                         Version 1.3 - August 14, 2001
60                                                CHAPTER 3. RASTERIZATION


3.1    Invariance
Consider a primitive p obtained by translating a primitive p through an offset (x, y)
in window coordinates, where x and y are integers. As long as neither p nor p is
clipped, it must be the case that each fragment f produced from p is identical to
a corresponding fragment f from p except that the center of f is offset by (x, y)
from the center of f .


3.2    Antialiasing
Antialiasing of a point, line, or polygon is effected in one of two ways depending
on whether the GL is in RGBA or color index mode.
     In RGBA mode, the R, G, and B values of the rasterized fragment are left
unaffected, but the A value is multiplied by a floating-point value in the range
[0, 1] that describes a fragment’s screen pixel coverage. The per-fragment stage of
the GL can be set up to use the A value to blend the incoming fragment with the
corresponding pixel already present in the framebuffer.
     In color index mode, the least significant b bits (to the left of the binary point)
of the color index are used for antialiasing; b = min{4, m}, where m is the number
of bits in the color index portion of the framebuffer. The antialiasing process sets
these b bits based on the fragment’s coverage value: the bits are set to zero for no
coverage and to all ones for complete coverage.
     The details of how antialiased fragment coverage values are computed are dif-
ficult to specify in general. The reason is that high-quality antialiasing may take
into account perceptual issues as well as characteristics of the monitor on which
the contents of the framebuffer are displayed. Such details cannot be addressed
within the scope of this document. Further, the coverage value computed for a
fragment of some primitive may depend on the primitive’s relationship to a num-
ber of grid squares neighboring the one corresponding to the fragment, and not just
on the fragment’s grid square. Another consideration is that accurate calculation
of coverage values may be computationally expensive; consequently we allow a
given GL implementation to approximate true coverage values by using a fast but
not entirely accurate coverage computation.
     In light of these considerations, we chose to specify the behavior of exact an-
tialiasing in the prototypical case that each displayed pixel is a perfect square of
uniform intensity. The square is called a fragment square and has lower left corner
(x, y) and upper right corner (x+1, y +1). We recognize that this simple box filter
may not produce the most favorable antialiasing results, but it provides a simple,
well-defined model.

                           Version 1.3 - August 14, 2001
3.2. ANTIALIASING                                                                 61


    A GL implementation may use other methods to perform antialiasing, subject
to the following conditions:

   1. If f1 and f2 are two fragments, and the portion of f1 covered by some prim-
      itive is a subset of the corresponding portion of f2 covered by the primitive,
      then the coverage computed for f1 must be less than or equal to that com-
      puted for f2 .

   2. The coverage computation for a fragment f must be local: it may depend
      only on f ’s relationship to the boundary of the primitive being rasterized. It
      may not depend on f ’s x and y coordinates.

Another property that is desirable, but not required, is:

   3. The sum of the coverage values for all fragments produced by rasterizing a
      particular primitive must be constant, independent of any rigid motions in
      window coordinates, as long as none of those fragments lies along window
      edges.

In some implementations, varying degrees of antialiasing quality may be obtained
by providing GL hints (section 5.6), allowing a user to make an image quality
versus speed tradeoff.

3.2.1 Multisampling
Multisampling is a mechanism to antialias all GL primitives: points, lines, poly-
gons, bitmaps, and images. The technique is to sample all primitives multiple times
at each pixel. The color sample values are resolved to a single, displayable color
each time a pixel is updated, so the antialiasing appears to be automatic at the
application level. Because each sample includes color, depth, and stencil informa-
tion, the color (including texture operation), depth, and stencil functions perform
equivalently to the single-sample mode.
    An additional buffer, called the multisample buffer, is added to the framebuffer.
Pixel sample values, including color, depth, and stencil values, are stored in this
buffer. When the framebuffer includes a multisample buffer, it does not include
depth or stencil buffers, even if the multisample buffer does not store depth or
stencil values. Color buffers (left, right, front, back, and aux) do coexist with the
multisample buffer, however.
    Multisample antialiasing is most valuable for rendering polygons, because it
requires no sorting for hidden surface elimination, and it correctly handles adjacent
polygons, object silhouettes, and even intersecting polygons. If only points or
lines are being rendered, the “smooth” antialiasing mechanism provided by the

                           Version 1.3 - August 14, 2001
62                                              CHAPTER 3. RASTERIZATION


base GL may result in a higher quality image. This mechanism is designed to
allow multisample and smooth antialiasing techniques to be alternated during the
rendering of a single scene.
     If the value of SAMPLE BUFFERS is one, the rasterization of all primitives
is changed, and is referred to as multisample rasterization. Otherwise, prim-
itive rasterization is referred to as single-sample rasterization. The value of
SAMPLE BUFFERS is queried by calling GetIntegerv with pname set to SAM-
PLE BUFFERS.
     During multisample rendering the contents of a pixel fragment are changed
in two ways. First, each fragment includes a coverage value with SAMPLES bits.
The value of SAMPLES is an implementation-dependent constant, and is queried by
calling GetIntegerv with pname set to SAMPLES.
     Second, each fragment includes SAMPLES depth values, color values, and sets
of texture coordinates, instead of the single depth value, color value, and set of
texture coordinates that is maintained in single-sample rendering mode. An imple-
mentation may choose to assign the same color value and the same set of texture
coordinates to more than one sample. The location for evaluating the color value
and the set of texture coordinates can be anywhere within the pixel including the
fragment center or any of the sample locations. The color value and the set of tex-
ture coordinates need not be evaluated at the same location. Each pixel fragment
thus consists of integer x and y grid coordinates, SAMPLES color and depth values,
SAMPLES sets of texture coordinates, and a coverage value with a maximum of
SAMPLES bits.
     Multisample rasterization is enabled or disabled by calling Enable or Disable
with the symbolic constant MULTISAMPLE.
     If MULTISAMPLE is disabled, multisample rasterization of all primitives is
equivalent to single-sample (fragment-center) rasterization, except that the frag-
ment coverage value is set to full coverage. The color and depth values and the
sets of texture coordinates may all be set to the values that would have been as-
signed by single-sample rasterization, or they may be assigned as described below
for multisample rasterization.
     If MULTISAMPLE is enabled, multisample rasterization of all primitives differs
substantially from single-sample rasterization. It is understood that each pixel
in the framebuffer has SAMPLES locations associated with it. These locations are
exact positions, rather than regions or areas, and each is referred to as a sample
point. The sample points associated with a pixel may be located inside or outside
of the unit square that is considered to bound the pixel. Furthermore, the relative
locations of sample points may be identical for each pixel in the framebuffer, or
they may differ.
     If the sample locations differ per pixel, they should be aligned to window, not

                          Version 1.3 - August 14, 2001
3.3. POINTS                                                                          63


screen, boundaries. Otherwise rendering results will be window-position specific.
The invariance requirement described in section 3.1 is relaxed for all multisample
rasterization, because the sample locations may be a function of pixel location.
    It is not possible to query the actual sample locations of a pixel.


3.3    Points
The rasterization of points is controlled with

      void PointSize( float size );

size specifies the width or diameter of a point. The default value is 1.0. A value
less than or equal to zero results in the error INVALID VALUE.
     Point antialiasing is enabled or disabled by calling Enable or Disable with the
symbolic constant POINT SMOOTH. The default state is for point antialiasing to be
disabled.
     In the default state, a point is rasterized by truncating its xw and yw coordinates
(recall that the subscripts indicate that these are x and y window coordinates) to
integers. already been effected if the subpixel flag is false). This (x, y) address,
along with data derived from the data associated with the vertex corresponding to
the point, is sent as a single fragment to the per-fragment stage of the GL.
     The effect of a point width other than 1.0 depends on the state of point an-
tialiasing. If antialiasing is disabled, the actual width is determined by rounding
the supplied width to the nearest integer, then clamping it to the implementation-
dependent maximum non-antialiased point width. This implementation-dependent
value must be no less than the implementation-dependent maximum antialiased
point width, rounded to the nearest integer value, and in any event no less than 1.
If rounding the specified width results in the value 0, then it is as if the value were
1. If the resulting width is odd, then the point
                                         1      1
                          (x, y) = ( xw + , yw + )
                                         2      2
is computed from the vertex’s xw and yw , and a square grid of the odd width cen-
tered at (x, y) defines the centers of the rasterized fragments (recall that fragment
centers lie at half-integer window coordinate values). If the width is even, then the
center point is
                                             1           1
                           (x, y) = ( xw + , yw + );
                                             2           2
the rasterized fragment centers are the half-integer window coordinate values
within the square of the even width centered on (x, y). See figure 3.2.

                           Version 1.3 - August 14, 2001
64                                                        CHAPTER 3. RASTERIZATION




                                                   5.5

                                                   4.5
                                  




                                  




                                                   3.5                ¡    ¡    ¡




                                                                      ¡    ¡    ¡




                                                   2.5

                                                   1.5

                                                   0.5

          0.5   1.5   2.5       3.5    4.5   5.5          0.5   1.5       2.5       3.5   4.5   5.5

                 Odd Width                                       Even Width


     Figure 3.2. Rasterization of non-antialiased wide points. The crosses show fragment
     centers produced by rasterization for any point that lies within the shaded region.
     The dotted grid lines lie on half-integer coordinates.




    All fragments produced in rasterizing a non-antialiased point are assigned the
same associated data, which are those of the vertex corresponding to the point, with
texture coordinates s, t, and r replaced with s/q, t/q, and r/q, respectively. If q is
less than or equal to zero, the results are undefined.
    If antialiasing is enabled, then point rasterization produces a fragment for each
fragment square that intersects the region lying within the circle having diameter
equal to the current point width and centered at the point’s (xw , yw ) (figure 3.3).
The coverage value for each fragment is the window coordinate area of the in-
tersection of the circular region with the corresponding fragment square (but see
section 3.2). This value is saved and used in the final step of rasterization (sec-
tion 3.11). The data associated with each fragment are otherwise the data associ-
ated with the point being rasterized, with texture coordinates s, t, and r replaced
with s/q, t/q, and r/q, respectively. If q is less than or equal to zero, the results
are undefined.
    Not all widths need be supported when point antialiasing is on, but the width
1.0 must be provided. If an unsupported width is requested, the nearest supported
width is used instead. The range of supported widths and the width of evenly-
spaced gradations within that range are implementation dependent. The range and

                                      Version 1.3 - August 14, 2001
3.3. POINTS                                                                                                        65




                       6.0



                       5.0
                                                                                                    




                                                                                                    




                                                                                                    




                       4.0
                                                                                                    




                                                                                                    




                                                                                                    




                                                                                                    




                       3.0
                                                                                                    




                                                                                                    




                                                                                                    




                                                                                                    




                       2.0
                                                                                                    




                                                                                                    




                                                                                                    




                                                                                                    




                       1.0
                                                                                                    




                       0.0
                             0.0       1.0               2.0               3.0               4.0       5.0   6.0




  Figure 3.3. Rasterization of antialiased wide points. The black dot indicates the
  point to be rasterized. The shaded region has the specified width. The X marks
  indicate those fragment centers produced by rasterization. A fragment’s computed
  coverage value is based on the portion of the shaded region that covers the corre-
  sponding fragment square. Solid lines lie on integer coordinates.




                              Version 1.3 - August 14, 2001
66                                               CHAPTER 3. RASTERIZATION


gradations may be obtained using the query mechanism described in Chapter 6. If,
for instance, the width range is from 0.1 to 2.0 and the gradation width is 0.1, then
the widths 0.1, 0.2, . . . , 1.9, 2.0 are supported.

3.3.1    Point Rasterization State
The state required to control point rasterization consists of the floating-point point
width and a bit indicating whether or not antialiasing is enabled.

3.3.2    Point Multisample Rasterization
If MULTISAMPLE is enabled, and the value of SAMPLE BUFFERS is one, then points
are rasterized using the following algorithm, regardless of whether point antialias-
ing (POINT SMOOTH) is enabled or disabled. Point rasterization produces a frag-
ment for each framebuffer pixel with one or more sample points that intersect the
region lying within the circle having diameter equal to the current point width and
centered at the point’s (xw , yw ). Coverage bits that correspond to sample points
that intersect the circular region are 1, other coverage bits are 0. All data associ-
ated with each sample for the fragment are the data associated with the point being
rasterized.
    Point size range and number of gradations are equivalent to those supported for
antialiased points.


3.4 Line Segments
A line segment results from a line strip Begin/End object, a line loop, or a se-
ries of separate line segments. Line segment rasterization is controlled by several
variables. Line width, which may be set by calling

        void LineWidth( float width );

with an appropriate positive floating-point width, controls the width of rasterized
line segments. The default width is 1.0. Values less than or equal to 0.0 generate
the error INVALID VALUE. Antialiasing is controlled with Enable and Disable
using the symbolic constant LINE SMOOTH. Finally, line segments may be stippled.
Stippling is controlled by a GL command that sets a stipple pattern (see below).

3.4.1    Basic Line Segment Rasterization
Line segment rasterization begins by characterizing the segment as either x-major
or y-major. x-major line segments have slope in the closed interval [−1, 1]; all

                           Version 1.3 - August 14, 2001
3.4. LINE SEGMENTS                                                                   67


other line segments are y-major (slope is determined by the segment’s endpoints).
We shall specify rasterization only for x-major segments except in cases where the
modifications for y-major segments are not self-evident.
    Ideally, the GL uses a “diamond-exit” rule to determine those fragments that
are produced by rasterizing a line segment. For each fragment f with center at win-
dow coordinates xf and yf , define a diamond-shaped region that is the intersection
of four half planes:

                   Rf = { (x, y) | |x − xf | + |y − yf | < 1/2.}

    Essentially, a line segment starting at pa and ending at pb produces those frag-
ments f for which the segment intersects Rf , except if pb is contained in Rf . See
figure 3.4.
    To avoid difficulties when an endpoint lies on a boundary of Rf we (in princi-
ple) perturb the supplied endpoints by a tiny amount. Let pa and pb have window
coordinates (xa , ya ) and (xb , yb ), respectively. Obtain the perturbed endpoints pa
given by (xa , ya ) − ( , 2 ) and pb given by (xb , yb ) − ( , 2 ). Rasterizing the line
segment starting at pa and ending at pb produces those fragments f for which the
segment starting at pa and ending on pb intersects Rf , except if pb is contained in
Rf . is chosen to be so small that rasterizing the line segment produces the same
fragments when δ is substituted for for any 0 < δ ≤ .
    When pa and pb lie on fragment centers, this characterization of fragments
reduces to Bresenham’s algorithm with one modification: lines produced in this
description are “half-open,” meaning that the final fragment (corresponding to pb )
is not drawn. This means that when rasterizing a series of connected line segments,
shared endpoints will be produced only once rather than twice (as would occur with
Bresenham’s algorithm).
    Because the initial and final conditions of the diamond-exit rule may be difficult
to implement, other line segment rasterization algorithms are allowed, subject to
the following rules:

   1. The coordinates of a fragment produced by the algorithm may not deviate by
      more than one unit in either x or y window coordinates from a corresponding
      fragment produced by the diamond-exit rule.

   2. The total number of fragments produced by the algorithm may differ from
      that produced by the diamond-exit rule by no more than one.

   3. For an x-major line, no two fragments may be produced that lie in the same
      window-coordinate column (for a y-major line, no two fragments may ap-
      pear in the same row).

                           Version 1.3 - August 14, 2001
68                                                                                                 CHAPTER 3. RASTERIZATION


                          ©   ©   ©   ©      ©                                           $      $   $   $   $




                          ©   ©   ©   ©      ©                                           $      $   $   $   $




                          ©   ©   ©   ©      ©                                           $      $   $   $   $




                          ©   ©   ©   ©      ©                                           $      $   $   $   $




                          ¨   ¨   ¨   ¨      ¨                                           #      #   #   #   #




                          ¨   ¨   ¨   ¨      ¨                                           #      #   #   #   #




                          ¨   ¨   ¨   ¨      ¨                                           #      #   #   #   #




                          ¨   ¨   ¨   ¨      ¨                                           #      #   #   #   #




                          §   §   §   §      §             ¡      ¡   ¡   ¡      ¡            "      "   "   "   "




                          §   §   §   §      §             ¡      ¡   ¡   ¡      ¡            "      "   "   "   "




                          §   §   §   §      §             ¡      ¡   ¡   ¡      ¡            "      "   "   "   "




                          §   §   §   §      §             ¡      ¡   ¡   ¡      ¡            "      "   "   "   "




                          ¦   ¦   ¦   ¦       ¦                ¢       ¢   ¢   ¢      ¢            !      !   !   !   !




                          ¦   ¦   ¦   ¦       ¦                ¢       ¢   ¢   ¢      ¢            !      !   !   !   !




                          ¦   ¦   ¦   ¦       ¦                ¢       ¢   ¢   ¢      ¢            !      !   !   !   !




                          ¦   ¦   ¦   ¦       ¦                ¢       ¢   ¢   ¢      ¢            !      !   !   !   !




                          ¥   ¥   ¥   ¥   ¤   ¥   ¤    ¤   ¤   £   ¤   £   £   £      £                




                          ¥   ¥   ¥   ¥   ¤   ¥   ¤    ¤   ¤   £   ¤   £   £   £      £                




                          ¥   ¥   ¥   ¥   ¤   ¥   ¤    ¤   ¤   £   ¤   £   £   £      £                




                          ¥   ¥   ¥   ¥   ¤   ¥   ¤    ¤   ¤   £   ¤   £   £   £      £                




     Figure 3.4. Visualization of Bresenham’s algorithm. A portion of a line segment is
     shown. A diamond shaped region of height 1 is placed around each fragment center;
     those regions that the line segment exits cause rasterization to produce correspond-
     ing fragments.




     4. If two line segments share a common endpoint, and both segments are either
        x-major (both left-to-right or both right-to-left) or y-major (both bottom-to-
        top or both top-to-bottom), then rasterizing both segments may not produce
        duplicate fragments, nor may any fragments be omitted so as to interrupt
        continuity of the connected segments.

    Next we must specify how the data associated with each rasterized fragment
are obtained. Let the window coordinates of a produced fragment center be given
by pr = (xd , yd ) and let pa = (xa , ya ) and pb = (xb , yb ). Set

                                                      (pr − pa ) · (pb − pa )
                                      t=                                      .                                                (3.1)
                                                            pb − pa 2
(Note that t = 0 at pa and t = 1 at pb .) The value of an associated datum f for the
fragment, whether it be R, G, B, or A (in RGBA mode) or a color index (in color
index mode), or the s, t, or r texture coordinate (the depth value, window z, must
be found using equation 3.3, below), is found as

                                                      (1 − t)fa /wa + tfb /wb
                                  f=                                                                                           (3.2)
                                                      (1 − t)αa /wa + tαb /wb

                                  Version 1.3 - August 14, 2001
3.4. LINE SEGMENTS                                                                   69


where fa and fb are the data associated with the starting and ending endpoints of
the segment, respectively; wa and wb are the clip w coordinates of the starting
and ending endpoints of the segments, respectively. αa = αb = 1 for all data
except texture coordinates, in which case αa = qa and αb = qb (qa and qb are
the homogeneous texture coordinates at the starting and ending endpoints of the
segment; results are undefined if either of these is less than or equal to 0). Note
that linear interpolation would use

                            f = (1 − t)fa /αa + tfb /αb .                         (3.3)

The reason that this formula is incorrect (except for the depth value) is that it inter-
polates a datum in window space, which may be distorted by perspective. What is
actually desired is to find the corresponding value when interpolated in clip space,
which equation 3.2 does. A GL implementation may choose to approximate equa-
tion 3.2 with 3.3, but this will normally lead to unacceptable distortion effects when
interpolating texture coordinates.

3.4.2 Other Line Segment Features
We have just described the rasterization of non-antialiased line segments of width
one using the default line stipple of F F F F16 . We now describe the rasterization
of line segments for general values of the line segment rasterization parameters.

Line Stipple
The command

      void LineStipple( int factor, ushort pattern );

defines a line stipple. pattern is an unsigned short integer. The line stipple is taken
from the lowest order 16 bits of pattern. It determines those fragments that are
to be drawn when the line is rasterized. factor is a count that is used to modify
the effective line stipple by causing each bit in line stipple to be used factor times.
f actor is clamped to the range [1, 256]. Line stippling may be enabled or disabled
using Enable or Disable with the constant LINE STIPPLE. When disabled, it is as
if the line stipple has its default value.
     Line stippling masks certain fragments that are produced by rasterization so
that they are not sent to the per-fragment stage of the GL. The masking is achieved
using three parameters: the 16-bit line stipple p, the line repeat count r, and an
integer stipple counter s. Let

                                 b = s/r mod 16,

                           Version 1.3 - August 14, 2001
70                                                   CHAPTER 3. RASTERIZATION




                       width = 2                              width = 3




     Figure 3.5. Rasterization of non-antialiased wide lines. x-major line segments are
     shown. The heavy line segment is the one specified to be rasterized; the light seg-
     ment is the offset segment used for rasterization. x marks indicate the fragment
     centers produced by rasterization.




Then a fragment is produced if the bth bit of p is 1, and not produced otherwise.
The bits of p are numbered with 0 being the least significant and 15 being the
most significant. The initial value of s is zero; s is incremented after production
of each fragment of a line segment (fragments are produced in order, beginning at
the starting point and working towards the ending point). s is reset to 0 whenever
a Begin occurs, and before every line segment in a group of independent segments
(as specified when Begin is invoked with LINES).
    If the line segment has been clipped, then the value of s at the beginning of the
line segment is indeterminate.

Wide Lines
The actual width of non-antialiased lines is determined by rounding the supplied
width to the nearest integer, then clamping it to the implementation-dependent
maximum non-antialiased line width. This implementation-dependent value must
be no less than the implementation-dependent maximum antialiased line width,
rounded to the nearest integer value, and in any event no less than 1. If rounding
the specified width results in the value 0, then it is as if the value were 1.
    Non-antialiased line segments of width other than one are rasterized by off-

                               Version 1.3 - August 14, 2001
3.4. LINE SEGMENTS                                                                 71


setting them in the minor direction (for an x-major line, the minor direction is
y, and for a y-major line, the minor direction is x) and replicating fragments in
the minor direction (see figure 3.5). Let w be the width rounded to the nearest
integer (if w = 0, then it is as if w = 1). If the line segment has endpoints
given by (x0 , y0 ) and (x1 , y1 ) in window coordinates, the segment with endpoints
(x0 , y0 − (w − 1)/2) and (x1 , y1 − (w − 1)/2) is rasterized, but instead of a single
fragment, a column of fragments of height w (a row of fragments of length w for
a y-major segment) is produced at each x (y for y-major) location. The lowest
fragment of this column is the fragment that would be produced by rasterizing the
segment of width 1 with the modified coordinates. The whole column is not pro-
duced if the stipple bit for the column’s x location is zero; otherwise, the whole
column is produced.




Antialiasing

Rasterized antialiased line segments produce fragments whose fragment squares
intersect a rectangle centered on the line segment. Two of the edges are parallel to
the specified line segment; each is at a distance of one-half the current width from
that segment: one above the segment and one below it. The other two edges pass
through the line endpoints and are perpendicular to the direction of the specified
line segment. Coverage values are computed for each fragment by computing the
area of the intersection of the rectangle with the fragment square (see figure 3.6;
see also section 3.2). Equation 3.2 is used to compute associated data values just as
with non-antialiased lines; equation 3.1 is used to find the value of t for each frag-
ment whose square is intersected by the line segment’s rectangle. Not all widths
need be supported for line segment antialiasing, but width 1.0 antialiased segments
must be provided. As with the point width, a GL implementation may be queried
for the range and number of gradations of available antialiased line widths.
     For purposes of antialiasing, a stippled line is considered to be a sequence of
contiguous rectangles centered on the line segment. Each rectangle has width equal
to the current line width and length equal to 1 pixel (except the last, which may be
shorter). These rectangles are numbered from 0 to n, starting with the rectangle
incident on the starting endpoint of the segment. Each of these rectangles is ei-
ther eliminated or produced according to the procedure given under Line Stipple,
above, where “fragment” is replaced with “rectangle.” Each rectangle so produced
is rasterized as if it were an antialiased polygon, described below (but culling, non-
default settings of PolygonMode, and polygon stippling are not applied).

                           Version 1.3 - August 14, 2001
72                                                                                          CHAPTER 3. RASTERIZATION




                                                                                                         




                                                                                                         




                                                                                                         




                                                                                                         




                                                                                                         




                                                                                                         




                                                                                                         




                                                                                                         




                                                                                                         




                                                                                                         




                                                                                                         




                                                                                                         




                                                                                                         




                                                                                                         




     Figure 3.6. The region used in rasterizing and finding corresponding coverage val-
     ues for an antialiased line segment (an x-major line segment is shown).




3.4.3     Line Rasterization State
The state required for line rasterization consists of the floating-point line width, a
16-bit line stipple, the line stipple repeat count, a bit indicating whether stippling
is enabled or disabled, and a bit indicating whether line antialiasing is on or off.
In addition, during rasterization, an integer stipple counter must be maintained to
implement line stippling. The initial value of the line width is 1.0. The initial value
of the line stipple is F F F F16 (a stipple of all ones). The initial value of the line
stipple repeat count is one. The initial state of line stippling is disabled. The initial
state of line segment antialiasing is disabled.


3.4.4     Line Multisample Rasterization
If MULTISAMPLE is enabled, and the value of SAMPLE BUFFERS is one, then lines
are rasterized using the following algorithm, regardless of whether line antialiasing
(LINE SMOOTH) is enabled or disabled. Line rasterization produces a fragment for
each framebuffer pixel with one or more sample points that intersect the rectangular
region that is described in the Antialiasing portion of section 3.4.2 (Other Line
Segment Features). If line stippling is enabled, the rectangular region is subdivided
into adjacent unit-length rectangles, with some rectangles eliminated according to
the procedure given in section 3.4.2, where “fragment” is replaced by “rectangle”.
    Coverage bits that correspond to sample points that intersect a retained rectan-

                                Version 1.3 - August 14, 2001
3.5. POLYGONS                                                                         73


gle are 1, other coverage bits are 0. Each color, depth, and set of texture coordinates
is produced by substituting the corresponding sample location into equation 3.1,
then using the result to evaluate equation 3.3. An implementation may choose to
assign the same color value and the same set of texture coordinates to more than
one sample by evaluating equation 3.1 at any location within the pixel including
the fragment center or any one of the sample locations, then substituting into equa-
tion 3.2. The color value and the set of texture coordinates need not be evaluated
at the same location.
     Line width range and number of gradations are equivalent to those supported
for antialiased lines.


3.5     Polygons
A polygon results from a polygon Begin/End object, a triangle resulting from a
triangle strip, triangle fan, or series of separate triangles, or a quadrilateral arising
from a quadrilateral strip, series of separate quadrilaterals, or a Rect command.
Like points and line segments, polygon rasterization is controlled by several vari-
ables. Polygon antialiasing is controlled with Enable and Disable with the sym-
bolic constant POLYGON SMOOTH. The analog to line segment stippling for poly-
gons is polygon stippling, described below.


3.5.1    Basic Polygon Rasterization
The first step of polygon rasterization is to determine if the polygon is back facing
or front facing. This determination is made by examining the sign of the area com-
puted by equation 2.7 of section 2.13.1 (including the possible reversal of this sign
as indicated by the last call to FrontFace). If this sign is positive, the polygon is
frontfacing; otherwise, it is back facing. This determination is used in conjunction
with the CullFace enable bit and mode value to decide whether or not a particular
polygon is rasterized. The CullFace mode is set by calling

        void CullFace( enum mode );

mode is a symbolic constant: one of FRONT, BACK or FRONT AND BACK. Culling
is enabled or disabled with Enable or Disable using the symbolic constant
CULL FACE. Front facing polygons are rasterized if either culling is disabled or
the CullFace mode is BACK while back facing polygons are rasterized only if ei-
ther culling is disabled or the CullFace mode is FRONT. The initial setting of the
CullFace mode is BACK. Initially, culling is disabled.

                            Version 1.3 - August 14, 2001
74                                                   CHAPTER 3. RASTERIZATION


    The rule for determining which fragments are produced by polygon rasteriza-
tion is called point sampling. The two-dimensional projection obtained by taking
the x and y window coordinates of the polygon’s vertices is formed. Fragment
centers that lie inside of this polygon are produced by rasterization. Special treat-
ment is given to a fragment whose center lies on a polygon boundary edge. In
such a case we require that if two polygons lie on either side of a common edge
(with identical endpoints) on which a fragment center lies, then exactly one of the
polygons results in the production of the fragment during rasterization.
    As for the data associated with each fragment produced by rasterizing a poly-
gon, we begin by specifying how these values are produced for fragments in a
triangle. Define barycentric coordinates for a triangle. Barycentric coordinates are
a set of three numbers, a, b, and c, each in the range [0, 1], with a + b + c = 1.
These coordinates uniquely specify any point p within the triangle or on the trian-
gle’s boundary as
                                 p = apa + bpb + cpc ,
where pa , pb , and pc are the vertices of the triangle. a, b, and c can be found as
                    A(ppb pc )            A(ppa pc )            A(ppa pb )
              a=                 ,   b=                ,   c=                ,
                    A(pa pb pc )          A(pa pb pc )          A(pa pb pc )
where A(lmn) denotes the area in window coordinates of the triangle with vertices
l, m, and n.
    Denote a datum at pa , pb , or pc as fa , fb , or fc , respectively. Then the value f
of a datum at a fragment produced by rasterizing a triangle is given by

                                afa /wa + bfb /wb + cfc /wc
                          f=                                                       (3.4)
                                aαa /wa + bαb /wb + cαc /wc
where wa , wb and wc are the clip w coordinates of pa , pb , and pc , respectively.
a, b, and c are the barycentric coordinates of the fragment for which the data are
produced. αa = αb = αc = 1 except for texture s, t, and r coordinates, for which
αa = qa , αb = qb , and αc = qc (if any of qa , qb , or qc are less than or equal
to zero, results are undefined). a, b, and c must correspond precisely to the exact
coordinates of the center of the fragment. Another way of saying this is that the
data associated with a fragment must be sampled at the fragment’s center.
    Just as with line segment rasterization, equation 3.4 may be approximated by

                           f = afa /αa + bfb /αb + cfc /αc ;

this may yield acceptable results for color values (it must be used for depth val-
ues), but will normally lead to unacceptable distortion effects if used for texture
coordinates.

                             Version 1.3 - August 14, 2001
3.5. POLYGONS                                                                      75


     For a polygon with more than three edges, we require only that a convex com-
bination of the values of the datum at the polygon’s vertices can be used to obtain
the value assigned to each fragment produced by the rasterization algorithm. That
is, it must be the case that at every fragment
                                          n
                                    f=         ai fi
                                         i=1

where n is the number of vertices in the polygon, fi is the value of the f at vertex
i; for each i 0 ≤ ai ≤ 1 and ni=1 ai = 1. The values of the ai may differ from
fragment to fragment, but at vertex i, aj = 0, j = i and ai = 1.
     One algorithm that achieves the required behavior is to triangulate a polygon
(without adding any vertices) and then treat each triangle individually as already
discussed. A scan-line rasterizer that linearly interpolates data along each edge
and then linearly interpolates data across each horizontal span from edge to edge
also satisfies the restrictions (in this case, the numerator and denominator of equa-
tion 3.4 should be iterated independently and a division performed for each frag-
ment).

3.5.2    Stippling
Polygon stippling works much the same way as line stippling, masking out certain
fragments produced by rasterization so that they are not sent to the next stage of
the GL. This is the case regardless of the state of polygon antialiasing. Stippling is
controlled with

        void PolygonStipple( ubyte *pattern );

pattern is a pointer to memory into which a 32 × 32 pattern is packed. The pattern
is unpacked from memory according to the procedure given in section 3.6.4 for
DrawPixels; it is as if the height and width passed to that command were both equal
to 32, the type were BITMAP, and the format were COLOR INDEX. The unpacked
values (before any conversion or arithmetic would have been performed) form a
stipple pattern of zeros and ones.
     If xw and yw are the window coordinates of a rasterized polygon fragment,
then that fragment is sent to the next stage of the GL if and only if the bit of the
pattern (xw mod 32, yw mod 32) is 1.
     Polygon stippling may be enabled or disabled with Enable or Disable using
the constant POLYGON STIPPLE. When disabled, it is as if the stipple pattern were
all ones.

                           Version 1.3 - August 14, 2001
76                                               CHAPTER 3. RASTERIZATION


3.5.3    Antialiasing

Polygon antialiasing rasterizes a polygon by producing a fragment wherever the
interior of the polygon intersects that fragment’s square. A coverage value is com-
puted at each such fragment, and this value is saved to be applied as described
in section 3.11. An associated datum is assigned to a fragment by integrating the
datum’s value over the region of the intersection of the fragment square with the
polygon’s interior and dividing this integrated value by the area of the intersection.
For a fragment square lying entirely within the polygon, the value of a datum at the
fragment’s center may be used instead of integrating the value across the fragment.
    Polygon stippling operates in the same way whether polygon antialiasing is
enabled or not. The polygon point sampling rule defined in section 3.5.1, however,
is not enforced for antialiased polygons.


3.5.4    Options Controlling Polygon Rasterization

The interpretation of polygons for rasterization is controlled using


        void PolygonMode( enum face, enum mode );


face is one of FRONT, BACK, or FRONT AND BACK, indicating that the rasterizing
method described by mode replaces the rasterizing method for front facing poly-
gons, back facing polygons, or both front and back facing polygons, respectively.
mode is one of the symbolic constants POINT, LINE, or FILL. Calling Polygon-
Mode with POINT causes certain vertices of a polygon to be treated, for rasteriza-
tion purposes, just as if they were enclosed within a Begin(POINT) and End pair.
The vertices selected for this treatment are those that have been tagged as having a
polygon boundary edge beginning on them (see section 2.6.2). LINE causes edges
that are tagged as boundary to be rasterized as line segments. (The line stipple
counter is reset at the beginning of the first rasterized edge of the polygon, but
not for subsequent edges.) FILL is the default mode of polygon rasterization, cor-
responding to the description in sections 3.5.1, 3.5.2, and 3.5.3. Note that these
modes affect only the final rasterization of polygons: in particular, a polygon’s ver-
tices are lit, and the polygon is clipped and possibly culled before these modes are
applied.
     Polygon antialiasing applies only to the FILL state of PolygonMode. For
POINT or LINE, point antialiasing or line segment antialiasing, respectively, ap-
ply.

                           Version 1.3 - August 14, 2001
3.5. POLYGONS                                                                     77


3.5.5    Depth Offset
The depth values of all fragments generated by the rasterization of a polygon may
be offset by a single value that is computed for that polygon. The function that
determines this value is specified by calling

        void PolygonOffset( float factor, float units );

factor scales the maximum depth slope of the polygon, and units scales an im-
plementation dependent constant that relates to the usable resolution of the depth
buffer. The resulting values are summed to produce the polygon offset value. Both
factor and units may be either positive or negative.
    The maximum depth slope m of a triangle is
                                           2             2
                                     ∂zw           ∂zw
                           m=                  +                                (3.5)
                                     ∂xw           ∂yw
where (xw , yw , zw ) is a point on the triangle. m may be approximated as
                                         ∂zw   ∂zw
                           m = max           ,           .                      (3.6)
                                         ∂xw   ∂yw
If the polygon has more than three vertices, one or more values of m may be used
during rasterization. Each may take any value in the range [min,max], where min
and max are the smallest and largest values obtained by evaluating Equation 3.5
or Equation 3.6 for the triangles formed by all three-vertex combinations.
     The minimum resolvable difference r is an implementation constant. It is the
smallest difference in window coordinate z values that is guaranteed to remain
distinct throughout polygon rasterization and in the depth buffer. All pairs of frag-
ments generated by the rasterization of two polygons with otherwise identical ver-
tices, but zw values that differ by r, will have distinct depth values.
     The offset value o for a polygon is

                           o = m ∗ f actor + r ∗ units.                         (3.7)

m is computed as described above, as a function of depth values in the range [0,1],
and o is applied to depth values in the same range.
    Boolean state values POLYGON OFFSET POINT, POLYGON OFFSET LINE, and
POLYGON OFFSET FILL determine whether o is applied during the rasterization
of polygons in POINT, LINE, and FILL modes. These boolean state values are
enabled and disabled as argument values to the commands Enable and Disable. If
POLYGON OFFSET POINT is enabled, o is added to the depth value of each frag-
ment produced by the rasterization of a polygon in POINT mode. Likewise, if

                          Version 1.3 - August 14, 2001
78                                                  CHAPTER 3. RASTERIZATION


POLYGON OFFSET LINE or POLYGON OFFSET FILL is enabled, o is added to the
depth value of each fragment produced by the rasterization of a polygon in LINE
or FILL modes, respectively.
    Fragment depth values are always limited to the range [0,1], either by clamping
after offset addition is performed (preferred), or by clamping the vertex values used
in the rasterization of the polygon.

3.5.6    Polygon Multisample Rasterization
If MULTISAMPLE is enabled and the value of SAMPLE BUFFERS is one, then poly-
gons are rasterized using the following algorithm, regardless of whether polygon
antialiasing (POLYGON SMOOTH) is enabled or disabled. Polygon rasterization pro-
duces a fragment for each framebuffer pixel with one or more sample points that
satisfy the point sampling criteria described in section 3.5.1, including the special
treatment for sample points that lie on a polygon boundary edge. If a polygon is
culled, based on its orientation and the CullFace mode, then no fragments are pro-
duced during rasterization. Fragments are culled by the polygon stipple just as they
are for aliased and antialiased polygons.
    Coverage bits that correspond to sample points that satisfy the point sampling
criteria are 1, other coverage bits are 0. Each color, depth, and set of texture co-
ordinates is produced by substituting the corresponding sample location into the
barycentric equations described in section 3.5.1, using the approximation to equa-
tion 3.4 that omits w components. An implementation may choose to assign the
same color value and the same set of texture coordinates to more than one sample
by barycentric evaluation using any location with the pixel including the fragment
center or one of the sample locations. The color value and the set of texture coor-
dinates need not be evaluated at the same location.
    The rasterization described above applies only to the FILL state of Polygon-
Mode. For POINT and LINE, the rasterizations described in sections 3.3.2 (Point
Multisample Rasterization) and 3.4.4 (Line Multisample Rasterization) apply.

3.5.7    Polygon Rasterization State
The state required for polygon rasterization consists of a polygon stipple pattern,
whether stippling is enabled or disabled, the current state of polygon antialiasing
(enabled or disabled), the current values of the PolygonMode setting for each of
front and back facing polygons, whether point, line, and fill mode polygon offsets
are enabled or disabled, and the factor and bias values of the polygon offset equa-
tion. The initial stipple pattern is all ones; initially stippling is disabled. The initial
setting of polygon antialiasing is disabled. The initial state for PolygonMode is

                            Version 1.3 - August 14, 2001
3.6. PIXEL RECTANGLES                                                             79


FILL for both front and back facing polygons. The initial polygon offset factor
and bias values are both 0; initially polygon offset is disabled for all modes.


3.6     Pixel Rectangles
Rectangles of color, depth, and certain other values may be converted to fragments
using the DrawPixels command (described in section 3.6.4). Some of the param-
eters and operations governing the operation of DrawPixels are shared by Read-
Pixels (used to obtain pixel values from the framebuffer) and CopyPixels (used to
copy pixels from one framebuffer location to another); the discussion of ReadPix-
els and CopyPixels, however, is deferred until Chapter 4 after the framebuffer has
been discussed in detail. Nevertheless, we note in this section when parameters
and state pertaining to DrawPixels also pertain to ReadPixels or CopyPixels.
    A number of parameters control the encoding of pixels in client memory (for
reading and writing) and how pixels are processed before being placed in or after
being read from the framebuffer (for reading, writing, and copying). These param-
eters are set with three commands: PixelStore, PixelTransfer, and PixelMap.


3.6.1    Pixel Storage Modes
Pixel storage modes affect the operation of DrawPixels and ReadPixels (as well as
other commands; see sections 3.5.2, 3.7, and 3.8) when one of these commands is
issued. This may differ from the time that the command is executed if the command
is placed in a display list (see section 5.4). Pixel storage modes are set with

        void PixelStore{if}( enum pname, T param );

pname is a symbolic constant indicating a parameter to be set, and param is the
value to set it to. Table 3.1 summarizes the pixel storage parameters, their types,
their initial values, and their allowable ranges. Setting a parameter to a value out-
side the given range results in the error INVALID VALUE.
     The version of PixelStore that takes a floating-point value may be used to
set any type of parameter; if the parameter is boolean, then it is set to FALSE if
the passed value is 0.0 and TRUE otherwise, while if the parameter is an integer,
then the passed value is rounded to the nearest integer. The integer version of
the command may also be used to set any type of parameter; if the parameter is
boolean, then it is set to FALSE if the passed value is 0 and TRUE otherwise, while
if the parameter is a floating-point value, then the passed value is converted to
floating-point.

                           Version 1.3 - August 14, 2001
80                                             CHAPTER 3. RASTERIZATION


         Parameter Name             Type     Initial Value   Valid Range
         UNPACK   SWAP BYTES       boolean      FALSE        TRUE/FALSE
         UNPACK   LSB FIRST        boolean      FALSE        TRUE/FALSE
         UNPACK   ROW LENGTH       integer         0           [0, ∞)
         UNPACK   SKIP ROWS        integer         0           [0, ∞)
         UNPACK   SKIP PIXELS      integer         0           [0, ∞)
         UNPACK   ALIGNMENT        integer         4           1,2,4,8
         UNPACK   IMAGE HEIGHT     integer         0           [0, ∞)
         UNPACK   SKIP IMAGES      integer         0           [0, ∞)

Table 3.1: PixelStore parameters pertaining to one or more of DrawPixels, Tex-
Image1D, TexImage2D, and TexImage3D.



3.6.2    The Imaging Subset
Some pixel transfer and per-fragment operations are only made available in GL
implementations which incorporate the optional imaging subset. The imaging sub-
set includes both new commands, and new enumerants allowed as parameters to
existing commands. If the subset is supported, all of these calls and enumer-
ants must be implemented as described later in the GL specification. If the sub-
set is not supported, calling any of the new commands generates the error IN-
VALID OPERATION, and using any of the new enumerants generates the error IN-
VALID ENUM.
    The individual operations available only in the imaging subset are described
in section 3.6.3, except for blending features, which are described in chapter 4.
Imaging subset operations include:

     1. Color tables, including all commands and enumerants described in sub-
        sections Color Table Specification, Alternate Color Table Specification
        Commands, Color Table State and Proxy State, Color Table Lookup,
        Post Convolution Color Table Lookup, and Post Color Matrix Color Ta-
        ble Lookup, as well as the query commands described in section 6.1.7.

     2. Convolution, including all commands and enumerants described in sub-
        sections Convolution Filter Specification, Alternate Convolution Filter
        Specification Commands, and Convolution, as well as the query com-
        mands described in section 6.1.8.

     3. Color matrix, including all commands and enumerants described in subsec-
        tions Color Matrix Specification and Color Matrix Transformation, as

                          Version 1.3 - August 14, 2001
3.6. PIXEL RECTANGLES                                                             81


        well as the simple query commands described in section 6.1.6.

   4. Histogram and minmax, including all commands and enumerants described
      in subsections Histogram Table Specification, Histogram State and
      Proxy State, Histogram, Minmax Table Specification, and Minmax, as
      well as the query commands described in section 6.1.9 and section 6.1.10.

   5. The subset of blending features described by BlendE-
      quation,      BlendColor,  and the BlendFunc modes CON-
      STANT COLOR,       ONE MINUS CONSTANT COLOR,  CONSTANT ALPHA,
      and ONE MINUS CONSTANT ALPHA. These are described separately in
      section 4.1.7.

    The imaging subset is supported only if the EXTENSIONS string includes the
substring "ARB imaging". Querying EXTENSIONS is described in section 6.1.11.
    If the imaging subset is not supported, the related pixel transfer operations are
not performed; pixels are passed unchanged to the next operation.

3.6.3    Pixel Transfer Modes
Pixel transfer modes affect the operation of DrawPixels (section 3.6.4), ReadPix-
els (section 4.3.2), and CopyPixels (section 4.3.3) at the time when one of these
commands is executed (which may differ from the time the command is issued).
Some pixel transfer modes are set with

        void PixelTransfer{if}( enum param, T value );

param is a symbolic constant indicating a parameter to be set, and value is the value
to set it to. Table 3.2 summarizes the pixel transfer parameters that are set with
PixelTransfer, their types, their initial values, and their allowable ranges. Setting
a parameter to a value outside the given range results in the error INVALID VALUE.
The same versions of the command exist as for PixelStore, and the same rules
apply to accepting and converting passed values to set parameters.
    The pixel map lookup tables are set with

        void PixelMap{ui us f}v( enum map, sizei size, T values );

map is a symbolic map name, indicating the map to set, size indicates the size of
the map, and values is a pointer to an array of size map values.
    The entries of a table may be specified using one of three types: single-
precision floating-point, unsigned short integer, or unsigned integer, depending on

                           Version 1.3 - August 14, 2001
82                                                 CHAPTER 3. RASTERIZATION


     Parameter Name                       Type      Initial Value   Valid Range
     MAP COLOR                           boolean      FALSE         TRUE/FALSE
     MAP STENCIL                         boolean      FALSE         TRUE/FALSE
     INDEX SHIFT                         integer         0           (−∞, ∞)
     INDEX OFFSET                        integer         0           (−∞, ∞)
     x SCALE                              float         1.0          (−∞, ∞)
     DEPTH SCALE                          float         1.0          (−∞, ∞)
     x BIAS                               float         0.0          (−∞, ∞)
     DEPTH BIAS                           float         0.0          (−∞, ∞)
     POST CONVOLUTION x SCALE             float         1.0          (−∞, ∞)
     POST CONVOLUTION x BIAS              float         0.0          (−∞, ∞)
     POST COLOR MATRIX x SCALE            float         1.0          (−∞, ∞)
     POST COLOR MATRIX x BIAS             float         0.0          (−∞, ∞)

     Table 3.2: PixelTransfer parameters. x is RED, GREEN, BLUE, or ALPHA.



which of the three versions of PixelMap is called. A table entry is converted to the
appropriate type when it is specified. An entry giving a color component value is
converted according to table 2.6. An entry giving a color index value is converted
from an unsigned short integer or unsigned integer to floating-point. An entry giv-
ing a stencil index is converted from single-precision floating-point to an integer by
rounding to nearest. The various tables and their initial sizes and entries are sum-
marized in table 3.3. A table that takes an index as an address must have size = 2n
or the error INVALID VALUE results. The maximum allowable size of each ta-
ble is specified by the implementation dependent value MAX PIXEL MAP TABLE,
but must be at least 32 (a single maximum applies to all tables). The error IN-
VALID VALUE is generated if a size larger than the implemented maximum, or less
than one, is given to PixelMap.


Color Table Specification

Color lookup tables are specified with

      void ColorTable( enum target, enum internalformat,
         sizei width, enum format, enum type, void *data );

target must be one of the regular color table names listed in table 3.4 to define
the table. A proxy table name is a special case discussed later in this section.

                           Version 1.3 - August 14, 2001
3.6. PIXEL RECTANGLES                                                                    83


     Map Name                      Address         Value      Init. Size   Init. Value
     PIXEL   MAP   I   TO   I      color idx     color idx         1           0.0
     PIXEL   MAP   S   TO   S     stencil idx   stencil idx        1             0
     PIXEL   MAP   I   TO   R      color idx        R              1           0.0
     PIXEL   MAP   I   TO   G      color idx        G              1           0.0
     PIXEL   MAP   I   TO   B      color idx        B              1           0.0
     PIXEL   MAP   I   TO   A      color idx        A              1           0.0
     PIXEL   MAP   R   TO   R         R             R              1           0.0
     PIXEL   MAP   G   TO   G         G             G              1           0.0
     PIXEL   MAP   B   TO   B         B             B              1           0.0
     PIXEL   MAP   A   TO   A         A             A              1           0.0

                            Table 3.3: PixelMap parameters.



             Table Name                                               Type
             COLOR TABLE                                             regular
             POST CONVOLUTION COLOR TABLE
             POST COLOR MATRIX COLOR TABLE
             PROXY COLOR TABLE                                        proxy
             PROXY POST CONVOLUTION COLOR TABLE
             PROXY POST COLOR MATRIX COLOR TABLE

Table 3.4: Color table names. Regular tables have associated image data. Proxy
tables have no image data, and are used only to determine if an image can be loaded
into the corresponding regular table.




width, format, type, and data specify an image in memory with the same mean-
ing and allowed values as the corresponding arguments to DrawPixels (see sec-
tion 3.6.4), with height taken to be 1. The maximum allowable width of a table
is implementation-dependent, but must be at least 32. The formats COLOR INDEX,
DEPTH COMPONENT, and STENCIL INDEX and the type BITMAP are not allowed.
    The specified image is taken from memory and processed just as if DrawPixels
were called, stopping after the final expansion to RGBA. The R, G, B, and A com-
ponents of each pixel are then scaled by the four COLOR TABLE SCALE parameters,
biased by the four COLOR TABLE BIAS parameters, and clamped to [0, 1]. These
parameters are set by calling ColorTableParameterfv as described below.

                                Version 1.3 - August 14, 2001
84                                             CHAPTER 3. RASTERIZATION


    Components are then selected from the resulting R, G, B, and A values to
obtain a table with the base internal format specified by (or derived from) inter-
nalformat, in the same manner as for textures (section 3.8.1). internalformat must
be one of the formats in table 3.15 or table 3.16.
    The color lookup table is redefined to have width entries, each with the speci-
fied internal format. The table is formed with indices 0 through width − 1. Table
location i is specified by the ith image pixel, counting from zero.
    The error INVALID VALUE is generated if width is not zero or a non-negative
power of two. The error TABLE TOO LARGE is generated if the specified color
lookup table is too large for the implementation.
    The scale and bias parameters for a table are specified by calling

      void ColorTableParameter{if}v( enum target, enum pname,
         T params );

target must be a regular color table name. pname is one of COLOR TABLE SCALE
or COLOR TABLE BIAS. params points to an array of four values: red, green, blue,
and alpha, in that order.
    A GL implementation may vary its allocation of internal component resolution
based on any ColorTable parameter, but the allocation must not be a function of
any other factor, and cannot be changed once it is established. Allocations must
be invariant; the same allocation must be made each time a color table is specified
with the same parameter values. These allocation rules also apply to proxy color
tables, which are described later in this section.

Alternate Color Table Specification Commands
Color tables may also be specified using image data taken directly from the frame-
buffer, and portions of existing tables may be respecified.
    The command

      void CopyColorTable( enum target, enum internalformat,
         int x, int y, sizei width );

defines a color table in exactly the manner of ColorTable, except that table data
are taken from the framebuffer, rather than from client memory. target must be a
regular color table name. x, y, and width correspond precisely to the corresponding
arguments of CopyPixels (refer to section 4.3.3); they specify the image’s width
and the lower left (x, y) coordinates of the framebuffer region to be copied. The
image is taken from the framebuffer exactly as if these arguments were passed to

                          Version 1.3 - August 14, 2001
3.6. PIXEL RECTANGLES                                                               85


CopyPixels with argument type set to COLOR and height set to 1, stopping after the
final expansion to RGBA.
    Subsequent processing is identical to that described for ColorTable, beginning
with scaling by COLOR TABLE SCALE. Parameters target, internalformat and width
are specified using the same values, with the same meanings, as the equivalent
arguments of ColorTable. format is taken to be RGBA.
    Two additional commands,

      void ColorSubTable( enum target, sizei start, sizei count,
         enum format, enum type, void *data );
      void CopyColorSubTable( enum target, sizei start, int x,
        int y, sizei count );

respecify only a portion of an existing color table. No change is made to the inter-
nalformat or width parameters of the specified color table, nor is any change made
to table entries outside the specified portion. target must be a regular color table
name.
    ColorSubTable arguments format, type, and data match the corresponding ar-
guments to ColorTable, meaning that they are specified using the same values,
and have the same meanings. Likewise, CopyColorSubTable arguments x, y, and
count match the x, y, and width arguments of CopyColorTable. Both of the Color-
SubTable commands interpret and process pixel groups in exactly the manner of
their ColorTable counterparts, except that the assignment of R, G, B, and A pixel
group values to the color table components is controlled by the internalformat of
the table, not by an argument to the command.
    Arguments start and count of ColorSubTable and CopyColorSubTable spec-
ify a subregion of the color table starting at index start and ending at index
start + count − 1. Counting from zero, the nth pixel group is assigned to the
table entry with index count + n. The error INVALID VALUE is generated if
start + count > width.

Color Table State and Proxy State
The state necessary for color tables can be divided into two categories. For each
of the three tables, there is an array of values. Each array has associated with it
a width, an integer describing the internal format of the table, six integer values
describing the resolutions of each of the red, green, blue, alpha, luminance, and
intensity components of the table, and two groups of four floating-point numbers to
store the table scale and bias. Each initial array is null (zero width, internal format
RGBA, with zero-sized components). The initial value of the scale parameters is
(1,1,1,1) and the initial value of the bias parameters is (0,0,0,0).

                           Version 1.3 - August 14, 2001
86                                               CHAPTER 3. RASTERIZATION


    In addition to the color lookup tables, partially instantiated proxy color lookup
tables are maintained. Each proxy table includes width and internal format state
values, as well as state for the red, green, blue, alpha, luminance, and intensity
component resolutions. Proxy tables do not include image data, nor do they in-
clude scale and bias parameters. When ColorTable is executed with target speci-
fied as one of the proxy color table names listed in table 3.4, the proxy state values
of the table are recomputed and updated. If the table is too large, no error is gener-
ated, but the proxy format, width and component resolutions are set to zero. If the
color table would be accommodated by ColorTable called with target set to the
corresponding regular table name (COLOR TABLE is the regular name correspond-
ing to PROXY COLOR TABLE, for example), the proxy state values are set exactly
as though the regular table were being specified. Calling ColorTable with a proxy
target has no effect on the image or state of any actual color table.
    There is no image associated with any of the proxy targets. They cannot be
used as color tables, and they must never be queried using GetColorTable. The
error INVALID ENUM is generated if this is attempted.

Convolution Filter Specification
A two-dimensional convolution filter image is specified by calling

      void ConvolutionFilter2D( enum target, enum internalformat,
         sizei width, sizei height, enum format, enum type,
         void *data );

target must be CONVOLUTION 2D. width, height, format, type, and data specify an
image in memory with the same meaning and allowed values as the corresponding
parameters to DrawPixels. The formats COLOR INDEX, DEPTH COMPONENT, and
STENCIL INDEX and the type BITMAP are not allowed.
    The specified image is extracted from memory and processed just as if Draw-
Pixels were called, stopping after the final expansion to RGBA. The R, G, B, and A
components of each pixel are then scaled by the four two-dimensional CONVOLU-
TION FILTER SCALE parameters and biased by the four two-dimensional CONVO-
LUTION FILTER BIAS parameters. These parameters are set by calling Convolu-
tionParameterfv as described below. No clamping takes place at any time during
this process.
    Components are then selected from the resulting R, G, B, and A values to
obtain a table with the base internal format specified by (or derived from) inter-
nalformat, in the same manner as for textures (section 3.8.1). internalformat must
be one of the formats in table 3.15 or table 3.16.

                           Version 1.3 - August 14, 2001
3.6. PIXEL RECTANGLES                                                                   87


    The red, green, blue, alpha, luminance, and/or intensity components of the
pixels are stored in floating point, rather than integer format. They form a two-
dimensional image indexed with coordinates i, j such that i increases from left to
right, starting at zero, and j increases from bottom to top, also starting at zero.
Image location i, j is specified by the N th pixel, counting from zero, where

                                N = i + j ∗ width

    The error INVALID VALUE is generated if width or height is greater
than the maximum supported value. These values are queried with Get-
ConvolutionParameteriv, setting target to CONVOLUTION 2D and pname to
MAX CONVOLUTION WIDTH or MAX CONVOLUTION HEIGHT, respectively.
    The scale and bias parameters for a two-dimensional filter are specified by
calling

      void ConvolutionParameter{if}v( enum target, enum pname,
         T params );

with target CONVOLUTION 2D. pname is one of CONVOLUTION FILTER SCALE
or CONVOLUTION FILTER BIAS. params points to an array of four values: red,
green, blue, and alpha, in that order.
    A one-dimensional convolution filter is defined using

      void ConvolutionFilter1D( enum target, enum internalformat,
         sizei width, enum format, enum type, void *data );

target must be CONVOLUTION 1D. internalformat, width, format, and type have
identical semantics and accept the same values as do their two-dimensional coun-
terparts. data must point to a one-dimensional image, however.
    The image is extracted from memory and processed as if ConvolutionFilter2D
were called with a height of 1, except that it is scaled and biased by the one-
dimensional CONVOLUTION FILTER SCALE and CONVOLUTION FILTER BIAS
parameters. These parameters are specified exactly as the two-dimensional pa-
rameters, except that ConvolutionParameterfv is called with target CONVOLU-
TION 1D.
    The image is formed with coordinates i such that i increases from left to right,
starting at zero. Image location i is specified by the ith pixel, counting from zero.
    The error INVALID VALUE is generated if width is greater than the maximum
supported value. This value is queried using GetConvolutionParameteriv, setting
target to CONVOLUTION 1D and pname to MAX CONVOLUTION WIDTH.

                               Version 1.3 - August 14, 2001
88                                             CHAPTER 3. RASTERIZATION


    Special facilities are provided for the definition of two-dimensional sepa-
rable filters – filters whose image can be represented as the product of two
one-dimensional images, rather than as full two-dimensional images. A two-
dimensional separable convolution filter is specified with

      void SeparableFilter2D( enum target, enum internalformat,
         sizei width, sizei height, enum format, enum type,
         void *row, void *column );

target must be SEPARABLE 2D. internalformat specifies the formats of the table
entries of the two one-dimensional images that will be retained. row points to a
width pixel wide image of the specified format and type. column points to a height
pixel high image, also of the specified format and type.
    The two images are extracted from memory and processed as if Convolution-
Filter1D were called separately for each, except that each image is scaled and bi-
ased by the two-dimensional separable CONVOLUTION FILTER SCALE and CON-
VOLUTION FILTER BIAS parameters. These parameters are specified exactly as
the one-dimensional and two-dimensional parameters, except that Convolution-
Parameteriv is called with target SEPARABLE 2D.

Alternate Convolution Filter Specification Commands
One and two-dimensional filters may also be specified using image data taken di-
rectly from the framebuffer.
    The command

      void CopyConvolutionFilter2D( enum target,
         enum internalformat, int x, int y, sizei width,
         sizei height );

defines a two-dimensional filter in exactly the manner of ConvolutionFilter2D,
except that image data are taken from the framebuffer, rather than from client mem-
ory. target must be CONVOLUTION 2D. x, y, width, and height correspond precisely
to the corresponding arguments of CopyPixels (refer to section 4.3.3); they specify
the image’s width and height, and the lower left (x, y) coordinates of the frame-
buffer region to be copied. The image is taken from the framebuffer exactly as
if these arguments were passed to CopyPixels with argument type set to COLOR,
stopping after the final expansion to RGBA.
     Subsequent processing is identical to that described for ConvolutionFilter2D,
beginning with scaling by CONVOLUTION FILTER SCALE. Parameters target, in-
ternalformat, width, and height are specified using the same values, with the same

                          Version 1.3 - August 14, 2001
3.6. PIXEL RECTANGLES                                                                   89


meanings, as the equivalent arguments of ConvolutionFilter2D. format is taken to
be RGBA.
    The command


      void CopyConvolutionFilter1D( enum target,
         enum internalformat, int x, int y, sizei width );

defines a one-dimensional filter in exactly the manner of ConvolutionFilter1D,
except that image data are taken from the framebuffer, rather than from client mem-
ory. target must be CONVOLUTION 1D. x, y, and width correspond precisely to the
corresponding arguments of CopyPixels (refer to section 4.3.3); they specify the
image’s width and the lower left (x, y) coordinates of the framebuffer region to
be copied. The image is taken from the framebuffer exactly as if these arguments
were passed to CopyPixels with argument type set to COLOR and height set to 1,
stopping after the final expansion to RGBA.
    Subsequent processing is identical to that described for ConvolutionFilter1D,
beginning with scaling by CONVOLUTION FILTER SCALE. Parameters target, in-
ternalformat, and width are specified using the same values, with the same mean-
ings, as the equivalent arguments of ConvolutionFilter2D. format is taken to be
RGBA.


Convolution Filter State

The required state for convolution filters includes a one-dimensional image array,
two one-dimensional image arrays for the separable filter, and a two-dimensional
image array. Each filter has associated with it a width and height (two-dimensional
and separable only), an integer describing the internal format of the filter, and two
groups of four floating-point numbers to store the filter scale and bias.
    Each initial convolution filter is null (zero width and height, internal format
RGBA, with zero-sized components). The initial value of all scale parameters is
(1,1,1,1) and the initial value of all bias parameters is (0,0,0,0).


Color Matrix Specification

Setting the matrix mode to COLOR causes the matrix operations described in sec-
tion 2.10.2 to apply to the top matrix on the color matrix stack. All matrix oper-
ations have the same effect on the color matrix as they do on the other matrices.


                               Version 1.3 - August 14, 2001
90                                               CHAPTER 3. RASTERIZATION


Histogram Table Specification
The histogram table is specified with

      void Histogram( enum target, sizei width,
         enum internalformat, boolean sink );

target must be HISTOGRAM if a histogram table is to be specified. target value
PROXY HISTOGRAM is a special case discussed later in this section. width speci-
fies the number of entries in the histogram table, and internalformat specifies the
format of each table entry. The maximum allowable width of the histogram table
is implementation-dependent, but must be at least 32. sink specifies whether pixel
groups will be consumed by the histogram operation (TRUE) or passed on to the
minmax operation (FALSE).
     If no error results from the execution of Histogram, the specified histogram
table is redefined to have width entries, each with the specified internal format.
The entries are indexed 0 through width − 1. Each component in each entry is set
to zero. The values in the previous histogram table, if any, are lost.
     The error INVALID VALUE is generated if width is not zero or a non-negative
power of 2. The error TABLE TOO LARGE is generated if the specified histogram
table is too large for the implementation. The error INVALID ENUM is generated
if internalformat is not one of the values accepted by the corresponding param-
eter of TexImage2D, or is 1, 2, 3, 4, INTENSITY, INTENSITY4, INTENSITY8,
INTENSITY12, or INTENSITY16.
     A GL implementation may vary its allocation of internal component resolution
based on any Histogram parameter, but the allocation must not be a function of any
other factor, and cannot be changed once it is established. In particular, allocations
must be invariant; the same allocation must be made each time a histogram is
specified with the same parameter values. These allocation rules also apply to the
proxy histogram, which is described later in this section.

Histogram State and Proxy State
The state necessary for histogram operation is an array of values, with which is
associated a width, an integer describing the internal format of the histogram, five
integer values describing the resolutions of each of the red, green, blue, alpha,
and luminance components of the table, and a flag indicating whether or not pixel
groups are consumed by the operation. The initial array is null (zero width, internal
format RGBA, with zero-sized components). The initial value of the flag is false.
    In addition to the histogram table, a partially instantiated proxy histogram table
is maintained. It includes width, internal format, and red, green, blue, alpha, and

                           Version 1.3 - August 14, 2001
3.6. PIXEL RECTANGLES                                                           91


luminance component resolutions. The proxy table does not include image data or
the flag. When Histogram is executed with target set to PROXY HISTOGRAM, the
proxy state values are recomputed and updated. If the histogram array is too large,
no error is generated, but the proxy format, width, and component resolutions are
set to zero. If the histogram table would be accomodated by Histogram called
with target set to HISTOGRAM, the proxy state values are set exactly as though
the actual histogram table were being specified. Calling Histogram with target
PROXY HISTOGRAM has no effect on the actual histogram table.
    There is no image associated with PROXY HISTOGRAM. It cannot be used as
a histogram, and its image must never queried using GetHistogram. The error
INVALID ENUM results if this is attempted.


Minmax Table Specification
The minmax table is specified with

        void Minmax( enum target, enum internalformat,
           boolean sink );

target must be MINMAX. internalformat specifies the format of the table entries.
sink specifies whether pixel groups will be consumed by the minmax operation
(TRUE) or passed on to final conversion (FALSE).
    The error INVALID ENUM is generated if internalformat is not one of the val-
ues accepted by the corresponding parameter of TexImage2D, or is 1, 2, 3, 4, IN-
TENSITY, INTENSITY4, INTENSITY8, INTENSITY12, or INTENSITY16. The
resulting table always has 2 entries, each with values corresponding only to the
components of the internal format.
    The state necessary for minmax operation is a table containing two elements
(the first element stores the minimum values, the second stores the maximum val-
ues), an integer describing the internal format of the table, and a flag indicating
whether or not pixel groups are consumed by the operation. The initial state is
a minimum table entry set to the maximum representable value and a maximum
table entry set to the minimum representable value. Internal format is set to RGBA
and the initial value of the flag is false.

3.6.4    Rasterization of Pixel Rectangles
The process of drawing pixels encoded in host memory is diagrammed in fig-
ure 3.7. We describe the stages of this process in the order in which they occur.
    Pixels are drawn using

                          Version 1.3 - August 14, 2001
92                                                                                       CHAPTER 3. RASTERIZATION



              byte, short, int, or float pixel
           data stream (index or component)
                                                                                                                                                   




                                                                                                                                                   




                                                                             




                                                                                unpack
                                                                                                                                                   




                                                                                                                                                   




                                              RGBA, L                                                                                 color
                                                                                                                                                   




                                                                                                                                   




                                                                                                                                      index
                                                                                                                                                   




                                 




                                    convert
                                                                                                                                                   




                                 




                                    to float
                                                                   




                                                                      Pixel Storage
                                                                                                                                                   




                                                                   




                                                                       Operations
                                                                                                                                                   




                                                                                                                                                   




                                                                                                                                                   




                                 
                                 convert
                                                                                                                                                   




                             
                                L to RGB
                                                                                                                                                   




                ¡   ¡   ¡   ¡   ¡     ¡   ¡   ¡   ¡   ¡   ¡   ¡   ¡    ¡    ¡    ¡   ¡    ¡   ¡    ¡   ¡   ¡   ¡   ¡     ¡    ¡   ¡   ¡   ¡   ¡   ¡   ¡




                ¡   ¡   ¡   ¡   ¡     ¡   ¡   ¡   ¡   ¡   ¡   ¡   ¡    ¡    ¡    ¡   ¡    ¡   ¡    ¡   ¡   ¡   ¡   ¡     ¡    ¡   ¡   ¡   ¡   ¡   ¡   ¡




                ¡   ¡   ¡   ¡   ¡     ¡




                                     scale
                                          ¡   ¡   ¡   ¡   ¡   ¡   ¡




                                                                      Pixel Transfer
                                                                       ¡    ¡    ¡   ¡    ¡   ¡    ¡   ¡   ¡   ¡   ¡     ¡    ¡




                                                                                                                           shift
                                                                                                                                  ¡   ¡   ¡   ¡   ¡   ¡




                ¡




                ¡
                    ¡




                    ¡
                        ¡




                        ¡
                            ¡




                            ¡
                                ¡




                                ¡
                                      ¡   ¡




                                    and bias
                                      ¡   ¡
                                              ¡




                                              ¡
                                                  ¡




                                                  ¡
                                                      ¡




                                                      ¡
                                                          ¡




                                                          ¡
                                                              ¡




                                                              ¡
                                                                  ¡




                                                                  ¡
                                                                       Operations
                                                                       ¡




                                                                       ¡
                                                                            ¡




                                                                            ¡
                                                                                 ¡




                                                                                 ¡
                                                                                     ¡




                                                                                     ¡
                                                                                          ¡




                                                                                          ¡
                                                                                              ¡




                                                                                              ¡
                                                                                                   ¡




                                                                                                   ¡
                                                                                                       ¡




                                                                                                       ¡
                                                                                                           ¡




                                                                                                           ¡
                                                                                                               ¡




                                                                                                               ¡
                                                                                                                   ¡




                                                                                                                   ¡
                                                                                                                         ¡    ¡   ¡




                                                                                                                         and offset
                                                                                                                         ¡    ¡   ¡
                                                                                                                                      ¡




                                                                                                                                      ¡
                                                                                                                                          ¡




                                                                                                                                          ¡
                                                                                                                                              ¡




                                                                                                                                              ¡
                                                                                                                                                  ¡




                                                                                                                                                  ¡
                                                                                                                                                      ¡




                                                                                                                                                      ¡




                ¡   ¡   ¡   ¡   ¡     ¡   ¡   ¡   ¡   ¡   ¡   ¡   ¡    ¡    ¡    ¡   ¡    ¡   ¡    ¡   ¡   ¡   ¡   ¡     ¡    ¡   ¡   ¡   ¡   ¡   ¡   ¡




                ¡   ¡   ¡   ¡   ¡     ¡   ¡   ¡   ¡   ¡   ¡   ¡   ¡    ¡    ¡    ¡   ¡    ¡   ¡    ¡   ¡   ¡   ¡   ¡     ¡    ¡   ¡   ¡   ¡   ¡   ¡   ¡




                ¡   ¡   ¡




                            RGBA to RGBA
                            ¡   ¡     ¡   ¡   ¡   ¡   ¡   ¡   ¡   ¡




                                                                       index to RGBA
                                                                       ¡    ¡    ¡   ¡    ¡   ¡    ¡   ¡   ¡   ¡   ¡




                                                                                                                       index to index
                                                                                                                         ¡    ¡   ¡   ¡   ¡   ¡   ¡   ¡




                ¡   ¡   ¡   ¡




                               lookup
                                ¡     ¡   ¡   ¡   ¡   ¡   ¡   ¡   ¡    ¡




                                                                           lookup
                                                                            ¡    ¡   ¡    ¡   ¡    ¡   ¡   ¡   ¡   ¡     ¡




                                                                                                                          lookup
                                                                                                                              ¡   ¡   ¡   ¡   ¡   ¡   ¡




                ¡   ¡   ¡   ¡   ¡     ¡   ¡   ¡   ¡   ¡   ¡   ¡   ¡    ¡    ¡    ¡   ¡    ¡   ¡    ¡   ¡   ¡   ¡   ¡     ¡    ¡   ¡   ¡   ¡   ¡   ¡   ¡




                ¡   ¡   ¡   ¡   ¡     ¡   ¡   ¡   ¡   ¡   ¡   ¡   ¡    ¡    ¡    ¡   ¡    ¡   ¡    ¡   ¡   ¡   ¡   ¡     ¡    ¡   ¡   ¡   ¡   ¡   ¡   ¡




                ¡   ¡   ¡   ¡   ¡     ¡   ¡   ¡   ¡   ¡   ¡   ¡   ¡    ¡    ¡    ¡   ¡    ¡   ¡    ¡   ¡   ¡   ¡   ¡     ¡    ¡   ¡   ¡   ¡   ¡   ¡   ¡




                ¡   ¡   ¡   ¡
                                color table
                                ¡     ¡   ¡   ¡   ¡   ¡   ¡   ¡   ¡    ¡    ¡    ¡   ¡    ¡   ¡    ¡   ¡   ¡   ¡   ¡     ¡    ¡   ¡   ¡   ¡   ¡   ¡   ¡




                ¡   ¡   ¡   ¡   ¡
                                  lookup
                                      ¡   ¡   ¡   ¡   ¡   ¡   ¡   ¡    ¡    ¡    ¡   ¡    ¡   ¡    ¡   ¡   ¡   ¡   ¡     ¡    ¡   ¡   ¡   ¡   ¡   ¡   ¡




                ¡   ¡   ¡   ¡   ¡     ¡   ¡   ¡   ¡   ¡   ¡   ¡   ¡    ¡    ¡    ¡   ¡    ¡   ¡    ¡   ¡   ¡   ¡   ¡     ¡    ¡   ¡   ¡   ¡   ¡   ¡   ¡




                ¡   ¡   ¡   ¡   ¡     ¡   ¡   ¡   ¡   ¡   ¡   ¡   ¡    ¡    ¡    ¡   ¡    ¡   ¡    ¡   ¡   ¡   ¡   ¡     ¡    ¡   ¡   ¡   ¡   ¡   ¡   ¡




                ¡   ¡   ¡   ¡




                             convolution
                                ¡     ¡   ¡   ¡   ¡   ¡   ¡   ¡   ¡    ¡




                                                                           color table
                                                                            ¡    ¡   ¡    ¡   ¡    ¡   ¡
                                                                                                           post
                                                                                                           ¡   ¡   ¡     ¡    ¡   ¡   ¡   ¡   ¡   ¡   ¡




                ¡   ¡   ¡




                            scale and bias
                            ¡   ¡     ¡   ¡   ¡   ¡   ¡   ¡   ¡   ¡    ¡    ¡




                                                                             lookup
                                                                                 ¡   ¡    ¡   ¡    ¡
                                                                                                       color matrix
                                                                                                       ¡   ¡   ¡   ¡     ¡    ¡   ¡   ¡   ¡   ¡   ¡   ¡




                ¡   ¡   ¡   ¡   ¡     ¡   ¡   ¡   ¡   ¡   ¡   ¡   ¡    ¡    ¡    ¡   ¡    ¡   ¡    ¡   ¡   ¡   ¡   ¡     ¡    ¡   ¡   ¡   ¡   ¡   ¡   ¡




                ¡   ¡   ¡   ¡   ¡     ¡   ¡   ¡   ¡   ¡   ¡   ¡   ¡    ¡    ¡    ¡   ¡    ¡   ¡    ¡   ¡   ¡   ¡   ¡     ¡    ¡   ¡   ¡   ¡   ¡   ¡   ¡




                ¡   ¡   ¡   ¡   ¡     ¡   ¡   ¡   ¡   ¡   ¡   ¡   ¡    ¡    ¡    ¡   ¡    ¡   ¡    ¡   ¡   ¡   ¡   ¡     ¡    ¡   ¡   ¡   ¡   ¡   ¡   ¡




         post                   color table                                histogram
      convolution                 lookup
                ¡   ¡   ¡   ¡   ¡     ¡   ¡   ¡   ¡   ¡   ¡   ¡   ¡    ¡    ¡    ¡   ¡    ¡   ¡    ¡   ¡   ¡   ¡   ¡     ¡    ¡   ¡   ¡   ¡   ¡   ¡   ¡




                ¡   ¡   ¡   ¡   ¡     ¡   ¡   ¡   ¡   ¡   ¡   ¡   ¡    ¡    ¡    ¡   ¡    ¡   ¡    ¡   ¡   ¡   ¡   ¡     ¡    ¡   ¡   ¡   ¡   ¡   ¡   ¡




                ¡   ¡   ¡   ¡   ¡     ¡   ¡   ¡   ¡   ¡   ¡   ¡   ¡    ¡    ¡    ¡   ¡    ¡   ¡    ¡   ¡   ¡   ¡   ¡     ¡    ¡   ¡   ¡   ¡   ¡   ¡   ¡




                ¡   ¡   ¡   ¡   ¡     ¡   ¡   ¡   ¡   ¡   ¡   ¡   ¡    ¡    ¡    ¡   ¡    ¡   ¡    ¡   ¡   ¡   ¡   ¡     ¡    ¡   ¡   ¡   ¡   ¡   ¡   ¡




                ¡   ¡   ¡   ¡




                             color matrix
                                ¡     ¡   ¡   ¡   ¡   ¡   ¡   ¡   ¡    ¡    ¡




                                                                                minmax
                                                                                 ¡   ¡    ¡   ¡    ¡   ¡   ¡   ¡   ¡     ¡    ¡   ¡   ¡   ¡   ¡   ¡   ¡




                ¡   ¡   ¡




                            scale and bias
                            ¡   ¡     ¡   ¡   ¡   ¡   ¡   ¡   ¡   ¡    ¡    ¡    ¡   ¡    ¡   ¡    ¡   ¡   ¡   ¡   ¡     ¡    ¡   ¡   ¡   ¡   ¡   ¡   ¡




                ¡   ¡   ¡   ¡   ¡     ¡   ¡   ¡   ¡   ¡   ¡   ¡   ¡    ¡    ¡    ¡   ¡    ¡   ¡    ¡   ¡   ¡   ¡   ¡     ¡    ¡   ¡   ¡   ¡   ¡   ¡   ¡




                ¡   ¡   ¡   ¡   ¡     ¡   ¡   ¡   ¡   ¡   ¡   ¡   ¡    ¡    ¡    ¡   ¡    ¡   ¡    ¡   ¡   ¡   ¡   ¡     ¡    ¡   ¡   ¡   ¡   ¡   ¡   ¡




                                     clamp                                    final                                          mask to
                                    to [0,1]                               conversion                                        (2n − 1)

              RGBA pixel                                                                          color index pixel
               data out                                                                               data out




     Figure 3.7. Operation of DrawPixels. Output is RGBA pixels if the GL is in RGBA
     mode, color index pixels otherwise. Operations in dashed boxes may be enabled
     or disabled. RGBA and color   index
                              Version 1.3pixel paths 14,
                                          - August   are shown;
                                                         2001 depth and stencil pixel
     paths are not shown.
3.6. PIXEL RECTANGLES                                                                93


      void DrawPixels( sizei width, sizei height, enum format,
         enum type, void *data );

format is a symbolic constant indicating what the values in memory represent.
width and height are the width and height, respectively, of the pixel rectangle to be
drawn. data is a pointer to the data to be drawn. These data are represented with
one of seven GL data types, specified by type. The correspondence between the
twenty type token values and the GL data types they indicate is given in table 3.5.
If the GL is in color index mode and format is not one of COLOR INDEX, STEN-
CIL INDEX, or DEPTH COMPONENT, then the error INVALID OPERATION occurs.
If type is BITMAP and format is not COLOR INDEX or STENCIL INDEX then the
error INVALID ENUM occurs. Some additional constraints on the combinations of
format and type values that are accepted is discussed below.

Unpacking

Data are taken from host memory as a sequence of signed or unsigned bytes (GL
data types byte and ubyte), signed or unsigned short integers (GL data types
short and ushort), signed or unsigned integers (GL data types int and uint),
or floating point values (GL data type float). These elements are grouped into
sets of one, two, three, or four values, depending on the format, to form a group.
Table 3.6 summarizes the format of groups obtained from memory; it also indicates
those formats that yield indices and those that yield components.
     By default the values of each GL data type are interpreted as they would be
specified in the language of the client’s GL binding. If UNPACK SWAP BYTES is
enabled, however, then the values are interpreted with the bit orderings modified
as per table 3.7. The modified bit orderings are defined only if the GL data type
ubyte has eight bits, and then for each specific GL data type only if that type is
represented with 8, 16, or 32 bits.
     The groups in memory are treated as being arranged in a rectangle. This rect-
angle consists of a series of rows, with the first element of the first group of the
first row pointed to by the pointer passed to DrawPixels. If the value of UN-
PACK ROW LENGTH is not positive, then the number of groups in a row is width;
otherwise the number of groups is UNPACK ROW LENGTH. If p indicates the loca-
tion in memory of the first element of the first row, then the first element of the N th
row is indicated by

                                       p + Nk                                     (3.8)

    where N is the row number (counting from zero) and k is defined as

                           Version 1.3 - August 14, 2001
94                                            CHAPTER 3. RASTERIZATION




      type Parameter                       Corresponding      Special
      Token Name                           GL Data Type    Interpretation
      UNSIGNED    BYTE                        ubyte             No
      BITMAP                                  ubyte             Yes
      BYTE                                     byte             No
      UNSIGNED    SHORT                      ushort             No
      SHORT                                   short             No
      UNSIGNED    INT                          uint             No
      INT                                       int             No
      FLOAT                                   float             No
      UNSIGNED    BYTE 3 3 2                  ubyte             Yes
      UNSIGNED    BYTE 2 3 3 REV              ubyte             Yes
      UNSIGNED    SHORT 5 6 5                ushort             Yes
      UNSIGNED    SHORT 5 6 5 REV            ushort             Yes
      UNSIGNED    SHORT 4 4 4 4              ushort             Yes
      UNSIGNED    SHORT 4 4 4 4 REV          ushort             Yes
      UNSIGNED    SHORT 5 5 5 1              ushort             Yes
      UNSIGNED    SHORT 1 5 5 5 REV          ushort             Yes
      UNSIGNED    INT 8 8 8 8                  uint             Yes
      UNSIGNED    INT 8 8 8 8 REV              uint             Yes
      UNSIGNED    INT 10 10 10 2               uint             Yes
      UNSIGNED    INT 2 10 10 10 REV           uint             Yes

Table 3.5: DrawPixels and ReadPixels type parameter values and the correspond-
ing GL data types. Refer to table 2.2 for definitions of GL data types. Special
interpretations are described near the end of section 3.6.4.




                          Version 1.3 - August 14, 2001
3.6. PIXEL RECTANGLES                                                               95




       Format Name              Element Meaning and Order        Target Buffer
       COLOR INDEX                     Color Index                  Color
       STENCIL INDEX                  Stencil Index                 Stencil
       DEPTH COMPONENT                    Depth                     Depth
       RED                                  R                       Color
       GREEN                                G                       Color
       BLUE                                 B                       Color
       ALPHA                                A                       Color
       RGB                               R, G, B                    Color
       RGBA                             R, G, B, A                  Color
       BGR                               B, G, R                    Color
       BGRA                             B, G, R, A                  Color
       LUMINANCE                       Luminance                    Color
       LUMINANCE ALPHA                Luminance, A                  Color

Table 3.6: DrawPixels and ReadPixels formats. The second column gives a de-
scription of and the number and order of elements in a group. Unless specified as
an index, formats yield components.




       Element Size      Default Bit Ordering     Modified Bit Ordering
       8 bit             [7..0]                   [7..0]
       16 bit            [15..0]                  [7..0][15..8]
       32 bit            [31..0]                  [7..0][15..8][23..16][31..24]

Table 3.7: Bit ordering modification of elements when UNPACK SWAP BYTES is
enabled. These reorderings are defined only when GL data type ubyte has 8 bits,
and then only for GL data types with 8, 16, or 32 bits. Bit 0 is the least significant.




                           Version 1.3 - August 14, 2001
96                                                                       CHAPTER 3. RASTERIZATION




                                                ROW_LENGTH
                                                                      




                                                                      




                                                                      




                                                                      




                                         
                                            subimage
                                                                      




                                                                      




                  SKIP_PIXELS    




                                 
                                     




                                     
                                         




                                         
                                             




                                             
                                                  




                                                  
                                                      




                                                      
                                                          




                                                          
                                                              




                                                              
                                                                  




                                                                  
                                                                      




                                                                      




                                    SKIP_ROWS




     Figure 3.8. Selecting a subimage from an image. The indicated parameter names
     are prefixed by UNPACK for DrawPixels and by PACK for ReadPixels.




                                        nl                               s ≥ a,
                           k=                                                                (3.9)
                                        a/s snl/a                        s<a

    where n is the number of elements in a group, l is the number of groups in
the row, a is the value of UNPACK ALIGNMENT, and s is the size, in units of GL
ubytes, of an element. If the number of bits per element is not 1, 2, 4, or 8 times
the number of bits in a GL ubyte, then k = nl for all values of a.
    There is a mechanism for selecting a sub-rectangle of groups from a larger
containing rectangle. This mechanism relies on three integer parameters: UN-
PACK ROW LENGTH, UNPACK SKIP ROWS, and UNPACK SKIP PIXELS. Before ob-
taining the first group from memory, the pointer supplied to DrawPixels is effec-
tively advanced by (UNPACK SKIP PIXELS)n+(UNPACK SKIP ROWS)k elements.
Then width groups are obtained from contiguous elements in memory (without ad-
vancing the pointer), after which the pointer is advanced by k elements. height sets
of width groups of values are obtained this way. See figure 3.8.
    Calling                                                                  Draw-
Pixels with a type of UNSIGNED BYTE 3 3 2, UNSIGNED BYTE 2 3 3 REV, UN-
SIGNED SHORT 5 6 5,                                  UNSIGNED SHORT 5 6 5 REV,
UNSIGNED SHORT 4 4 4 4,                            UNSIGNED SHORT 4 4 4 4 REV,
UNSIGNED SHORT 5 5 5 1,                            UNSIGNED SHORT 1 5 5 5 REV,
UNSIGNED INT 8 8 8 8,                  UNSIGNED INT 8 8 8 8 REV,                UN-

                            Version 1.3 - August 14, 2001
3.6. PIXEL RECTANGLES                                                             97


  type Parameter                        GL Data      Number of        Matching
  Token Name                             Type       Components      Pixel Formats
  UNSIGNED    BYTE 3 3 2                ubyte           3               RGB
  UNSIGNED    BYTE 2 3 3 REV            ubyte           3               RGB
  UNSIGNED    SHORT 5 6 5               ushort          3               RGB
  UNSIGNED    SHORT 5 6 5 REV           ushort          3               RGB
  UNSIGNED    SHORT 4 4 4 4             ushort          4            RGBA,BGRA
  UNSIGNED    SHORT 4 4 4 4 REV         ushort          4            RGBA,BGRA
  UNSIGNED    SHORT 5 5 5 1             ushort          4            RGBA,BGRA
  UNSIGNED    SHORT 1 5 5 5 REV         ushort          4            RGBA,BGRA
  UNSIGNED    INT 8 8 8 8                uint           4            RGBA,BGRA
  UNSIGNED    INT 8 8 8 8 REV            uint           4            RGBA,BGRA
  UNSIGNED    INT 10 10 10 2             uint           4            RGBA,BGRA
  UNSIGNED    INT 2 10 10 10 REV         uint           4            RGBA,BGRA

                         Table 3.8: Packed pixel formats.



SIGNED INT 10 10 10 2, or UNSIGNED INT 2 10 10 10 REV is a special case
in which all the components of each group are packed into a single unsigned byte,
unsigned short, or unsigned int, depending on the type. The number of components
per packed pixel is fixed by the type, and must match the number of components
per group indicated by the format parameter, as listed in table 3.8. The error IN-
VALID OPERATION is generated if a mismatch occurs. This constraint also holds
for all other functions that accept or return pixel data using type and format param-
eters to define the type and format of that data.
     Bitfield locations of the first, second, third, and fourth components of each
packed pixel type are illustrated in tables 3.9, 3.10, and 3.11. Each bitfield is
interpreted as an unsigned integer value. If the base GL type is supported with
more than the minimum precision (e.g. a 9-bit byte) the packed components are
right-justified in the pixel.
     Components are normally packed with the first component in the most signif-
icant bits of the bitfield, and successive component occupying progressively less
significant locations. Types whose token names end with REV reverse the compo-
nent packing order from least to most significant locations. In all cases, the most
significant bit of each component is packed in the most significant bit location of
its location in the bitfield.




                          Version 1.3 - August 14, 2001
98                                                  CHAPTER 3. RASTERIZATION




UNSIGNED BYTE 3 3 2:
                    7       6       5   4     3     2       1         0

                        1st Component         2nd               3rd




UNSIGNED BYTE 2 3 3 REV:
                    7           6   5   4     3     2       1         0

                          3rd           2nd             1st Component


Table 3.9: UNSIGNED BYTE formats. Bit numbers are indicated for each compo-
nent.




                          Version 1.3 - August 14, 2001
3.6. PIXEL RECTANGLES                                                                                                    99




UNSIGNED SHORT 5 6 5:
  15     14         13    12    11     10         9   8           7     6         5   4   3       2            1   0

           1st Component                                    2nd                                    3rd




UNSIGNED SHORT 5 6 5 REV:
  15     14         13    12    11     10         9   8           7     6         5   4   3       2            1   0

                    3rd                                     2nd                               1st Component




UNSIGNED SHORT 4 4 4 4:
  15     14         13    12    11     10         9   8           7     6         5   4   3       2            1   0

        1st Component                       2nd                             3rd                          4th




UNSIGNED SHORT 4 4 4 4 REV:
  15     14         13    12    11     10         9   8           7     6         5   4   3       2            1   0

              4th                           3rd                             2nd                  1st Component




UNSIGNED SHORT 5 5 5 1:
  15     14         13    12    11     10         9   8           7     6         5   4   3       2            1   0

           1st Component                              2nd                                 3rd                      4th




UNSIGNED SHORT 1 5 5 5 REV:
  15     14         13    12     11    10         9   8           7     6         5   4   3        2           1   0

  4th                     3rd                                     2nd                         1st Component


                                Table 3.10: UNSIGNED SHORT formats




                                      Version 1.3 - August 14, 2001
100                                                      CHAPTER 3. RASTERIZATION




UNSIGNED INT 8 8 8 8:
  31 30 29 28 27 26 25 24 23 22 21 20 19 18 17 16 15 14 13 12 11 10 9   8   7   6   5    4     3       2   1     0

         1st Component               2nd                   3rd                               4th




UNSIGNED INT 8 8 8 8 REV:
  31 30 29 28 27 26 25 24 23 22 21 20 19 18 17 16 15 14 13 12 11 10 9   8   7   6   5    4     3       2   1     0

              4th                    3rd                   2nd                      1st Component




UNSIGNED INT 10 10 10 2:
  31 30 29 28 27 26 25 24 23 22 21 20 19 18 17 16 15 14 13 12 11 10 9   8   7   6   5    4     3       2   1     0

            1st Component                   2nd                             3rd                                4th




UNSIGNED INT 2 10 10 10 REV:
  31 30 29 28 27 26 25 24 23 22 21 20 19 18 17 16 15 14 13 12 11 10 9   8   7   6    5   4         3   2   1         0

   4th                   3rd                       2nd                          1st Component


                               Table 3.11: UNSIGNED INT formats




                                 Version 1.3 - August 14, 2001
3.6. PIXEL RECTANGLES                                                              101


        Format       First          Second          Third          Fourth
                   Component       Component      Component      Component
        RGB           red            green          blue
        RGBA          red            green          blue             alpha
        BGRA         blue            green           red             alpha

                    Table 3.12: Packed pixel field assignments.



    The assignment of component to fields in the packed pixel is as described in
table 3.12
    Byte swapping, if enabled, is performed before the component are extracted
from each pixel. The above discussions of row length and image extraction are
valid for packed pixels, if “group” is substituted for “component” and the number
of components per group is understood to be one.
    Calling DrawPixels with a type of BITMAP is a special case in which the data
are a series of GL ubyte values. Each ubyte value specifies 8 1-bit elements
with its 8 least-significant bits. The 8 single-bit elements are ordered from most
significant to least significant if the value of UNPACK LSB FIRST is FALSE; other-
wise, the ordering is from least significant to most significant. The values of bits
other than the 8 least significant in each ubyte are not significant.
    The first element of the first row is the first bit (as defined above) of the ubyte
pointed to by the pointer passed to DrawPixels. The first element of the second
row is the first bit (again as defined above) of the ubyte at location p + k, where
k is computed as

                                              l
                                    k=a                                         (3.10)
                                             8a
    There is a mechanism for selecting a sub-rectangle of elements from a BITMAP
image as well. Before obtaining the first element from memory, the pointer sup-
plied to DrawPixels is effectively advanced by UNPACK SKIP ROWS ∗ k ubytes.
Then UNPACK SKIP PIXELS 1-bit elements are ignored, and the subsequent width
1-bit elements are obtained, without advancing the ubyte pointer, after which the
pointer is advanced by k ubytes. height sets of width elements are obtained this
way.

Conversion to floating-point
This step applies only to groups of components. It is not performed on indices.
Each element in a group is converted to a floating-point value according to the ap-

                           Version 1.3 - August 14, 2001
102                                              CHAPTER 3. RASTERIZATION


propriate formula in table 2.6 (section 2.13). For packed pixel types, each element
in the group is converted by computing c / (2N − 1), where c is the unsigned inte-
ger value of the bitfield containing the element and N is the number of bits in the
bitfield.

Conversion to RGB
This step is applied only if the format is LUMINANCE or LUMINANCE ALPHA. If the
format is LUMINANCE, then each group of one element is converted to a group of
R, G, and B (three) elements by copying the original single element into each of
the three new elements. If the format is LUMINANCE ALPHA, then each group of
two elements is converted to a group of R, G, B, and A (four) elements by copying
the first original element into each of the first three new elements and copying the
second original element to the A (fourth) new element.

Final Expansion to RGBA
This step is performed only for non-depth component groups. Each group is con-
verted to a group of 4 elements as follows: if a group does not contain an A element,
then A is added and set to 1.0. If any of R, G, or B is missing from the group, each
missing element is added and assigned a value of 0.0.

Pixel Transfer Operations
This step is actually a sequence of steps. Because the pixel transfer operations
are performed equivalently during the drawing, copying, and reading of pixels,
and during the specification of texture images (either from memory or from the
framebuffer), they are described separately in section 3.6.5. After the processing
described in that section is completed, groups are processed as described in the
following sections.

Final Conversion
For a color index, final conversion consists of masking the bits of the index to the
left of the binary point by 2n − 1, where n is the number of bits in an index buffer.
For RGBA components, each element is clamped to [0, 1]. The resulting values are
converted to fixed-point according to the rules given in section 2.13.9 (Final Color
Processing).
     For a depth component, an element is first clamped to [0, 1] and then converted
to fixed-point as if it were a window z value (see section 2.10.1, Controlling the
Viewport).

                          Version 1.3 - August 14, 2001
3.6. PIXEL RECTANGLES                                                             103


    Stencil indices are masked by 2n − 1, where n is the number of bits in the
stencil buffer.

Conversion to Fragments
The conversion of a group to fragments is controlled with

        void PixelZoom( float zx , float zy );

Let (xrp , yrp ) be the current raster position (section 2.12). (If the current raster
position is invalid, then DrawPixels is ignored; pixel transfer operations do not
update the histogram or minmax tables, and no fragments are generated. However,
the histogram and minmax tables are updated even if the corresponding fragments
are later rejected by the pixel ownership (section 4.1.1) or scissor (section 4.1.2)
tests.) If a particular group (index or components) is the nth in a row and belongs to
the mth row, consider the region in window coordinates bounded by the rectangle
with corners

   (xrp + zx n, yrp + zy m)       and      (xrp + zx (n + 1), yrp + zy (m + 1))

(either zx or zy may be negative). Any fragments whose centers lie inside of this
rectangle (or on its bottom or left boundaries) are produced in correspondence with
this particular group of elements.
    A fragment arising from a group consisting of color data takes on the color in-
dex or color components of the group; the depth and texture coordinates are taken
from the current raster position’s associated data. A fragment arising from a depth
component takes the component’s depth value; the color and texture coordinates
are given by those associated with the current raster position. In both cases texture
coordinates s, t, and r are replaced with s/q, t/q, and r/q, respectively. If q is
less than or equal to zero, the results are undefined. Groups arising from Draw-
Pixels with a format of STENCIL INDEX are treated specially and are described in
section 4.3.1.

3.6.5    Pixel Transfer Operations
The GL defines four kinds of pixel groups:

   1. RGBA component: Each group comprises four color components: red, green,
      blue, and alpha.

   2. Depth component: Each group comprises a single depth component.

                           Version 1.3 - August 14, 2001
104                                              CHAPTER 3. RASTERIZATION


   3. Color index: Each group comprises a single color index.

   4. Stencil index: Each group comprises a single stencil index.

Each operation described in this section is applied sequentially to each pixel group
in an image. Many operations are applied only to pixel groups of certain kinds; if
an operation is not applicable to a given group, it is skipped.


Arithmetic on Components

This step applies only to RGBA component and depth component groups. Each
component is multiplied by an appropriate signed scale factor: RED SCALE for an
R component, GREEN SCALE for a G component, BLUE SCALE for a B component,
and ALPHA SCALE for an A component, or DEPTH SCALE for a depth component.
Then the result is added to the appropriate signed bias: RED BIAS, GREEN BIAS,
BLUE BIAS, ALPHA BIAS, or DEPTH BIAS.


Arithmetic on Indices

This step applies only to color index and stencil index groups. If the index is a
floating-point value, it is converted to fixed-point, with an unspecified number of
bits to the right of the binary point and at least log2 (MAX PIXEL MAP TABLE)
bits to the left of the binary point. Indices that are already integers remain so; any
fraction bits in the resulting fixed-point value are zero.
    The fixed-point index is then shifted by |INDEX SHIFT| bits, left if
INDEX SHIFT > 0 and right otherwise. In either case the shift is zero-filled. Then,
the signed integer offset INDEX OFFSET is added to the index.


RGBA to RGBA Lookup

This step applies only to RGBA component groups, and is skipped if MAP COLOR is
FALSE. First, each component is clamped to the range [0, 1]. There is a table associ-
ated with each of the R, G, B, and A component elements: PIXEL MAP R TO R for
R, PIXEL MAP G TO G for G, PIXEL MAP B TO B for B, and PIXEL MAP A TO A
for A. Each element is multiplied by an integer one less than the size of the corre-
sponding table, and, for each element, an address is found by rounding this value
to the nearest integer. For each element, the addressed value in the corresponding
table replaces the element.

                           Version 1.3 - August 14, 2001
3.6. PIXEL RECTANGLES                                                             105


Color Index Lookup
This step applies only to color index groups. If the GL command that invokes the
pixel transfer operation requires that RGBA component pixel groups be generated,
then a conversion is performed at this step. RGBA component pixel groups are
required if
   1. The groups will be rasterized, and the GL is in RGBA mode, or
   2. The groups will be loaded as an image into texture memory, or
   3. The groups will be returned to client memory with a format other than
      COLOR INDEX.
If RGBA component groups are required, then the integer part of the in-
dex is used to reference 4 tables of color components: PIXEL MAP I TO R,
PIXEL MAP I TO G, PIXEL MAP I TO B, and PIXEL MAP I TO A. Each of these
tables must have 2n entries for some integer value of n (n may be different for
each table). For each table, the index is first rounded to the nearest integer; the
result is ANDed with 2n − 1, and the resulting value used as an address into the
table. The indexed value becomes an R, G, B, or A value, as appropriate. The
group of four elements so obtained replaces the index, changing the group’s type
to RGBA component.
    If RGBA component groups are not required, and if MAP COLOR is enabled,
then the index is looked up in the PIXEL MAP I TO I table (otherwise, the index
is not looked up). Again, the table must have 2n entries for some integer n. The
index is first rounded to the nearest integer; the result is ANDed with 2n − 1, and
the resulting value used as an address into the table. The value in the table replaces
the index. The floating-point table value is first rounded to a fixed-point value with
unspecified precision. The group’s type remains color index.

Stencil Index Lookup
This step applies only to stencil index groups. If MAP STENCIL is enabled, then
the index is looked up in the PIXEL MAP S TO S table (otherwise, the index is not
looked up). The table must have 2n entries for some integer n. The integer index
is ANDed with 2n − 1, and the resulting value used as an address into the table.
The integer value in the table replaces the index.

Color Table Lookup
This step applies only to RGBA component groups. Color table lookup is only
done if COLOR TABLE is enabled. If a zero-width table is enabled, no lookup is

                           Version 1.3 - August 14, 2001
106                                               CHAPTER 3. RASTERIZATION


                    Base Internal Format     R     G     B    A
                    ALPHA                                     At
                    LUMINANCE                Lt    Lt    Lt
                    LUMINANCE ALPHA          Lt    Lt    Lt   At
                    INTENSITY                It    It    It   It
                    RGB                      Rt    Gt    Bt
                    RGBA                     Rt    Gt    Bt   At

Table 3.13: Color table lookup. Rt , Gt , Bt , At , Lt , and It are color table values
that are assigned to pixel components R, G, B, and A depending on the table
format. When there is no assignment, the component value is left unchanged by
lookup.



performed.
    The internal format of the table determines which components of the group
will be replaced (see table 3.13). The components to be replaced are converted
to indices by clamping to [0, 1], multiplying by an integer one less than the width
of the table, and rounding to the nearest integer. Components are replaced by the
table entry at the index.
    The required state is one bit indicating whether color table lookup is enabled
or disabled. In the initial state, lookup is disabled.

Convolution
This step applies only to RGBA component groups. If CONVOLUTION 1D
is enabled, the one-dimensional convolution filter is applied only to the one-
dimensional texture images passed to TexImage1D, TexSubImage1D, CopyTex-
Image1D, and CopyTexSubImage1D, and returned by GetTexImage (see sec-
tion 6.1.4) with target TEXTURE 1D. If CONVOLUTION 2D is enabled, the two-
dimensional convolution filter is applied only to the two-dimensional images
passed to DrawPixels, CopyPixels, ReadPixels, TexImage2D, TexSubImage2D,
CopyTexImage2D, CopyTexSubImage2D, and CopyTexSubImage3D. If SEP-
ARABLE 2D is enabled, and CONVOLUTION 2D is disabled, the separable two-
dimensional convolution filter is instead applied these images.
    The convolution operation is a sum of products of source image pixels and
convolution filter pixels. Source image pixels always have four components: red,
green, blue, and alpha, denoted in the equations below as Rs , Gs , Bs , and As .
Filter pixels may be stored in one of five formats, with 1, 2, 3, or 4 components.
These components are denoted as Rf , Gf , Bf , Af , Lf , and If in the equations

                           Version 1.3 - August 14, 2001
3.6. PIXEL RECTANGLES                                                            107


 Base Filter Format       R             G             B             A
 ALPHA                    Rs            Gs            Bs            As ∗ Af
 LUMINANCE                Rs ∗ Lf       Gs ∗ Lf       Bs ∗ Lf       As
 LUMINANCE ALPHA          Rs ∗ Lf       Gs ∗ Lf       Bs ∗ Lf       As ∗ Af
 INTENSITY                Rs ∗ If       Gs ∗ If       Bs ∗ If       As ∗ If
 RGB                      Rs ∗ Rf       Gs ∗ Gf       Bs ∗ Bf       As
 RGBA                     Rs ∗ Rf       Gs ∗ Gf       Bs ∗ Bf       As ∗ Af

Table 3.14: Computation of filtered color components depending on filter image
format. C ∗ F indicates the convolution of image component C with filter F .

below. The result of the convolution operation is the 4-tuple R,G,B,A. Depending
on the internal format of the filter, individual color components of each source
image pixel are convolved with one filter component, or are passed unmodified.
The rules for this are defined in table 3.14.
     The convolution operation is defined differently for each of the three convolu-
tion filters. The variables Wf and Hf refer to the dimensions of the convolution
filter. The variables Ws and Hs refer to the dimensions of the source pixel image.
     The convolution equations are defined as follows, where C refers to the filtered
result, Cf refers to the one- or two-dimensional convolution filter, and Crow and
Ccolumn refer to the two one-dimensional filters comprising the two-dimensional
separable filter. Cs depends on the source image color Cs and the convolution bor-
der mode as described below. Cr , the filtered output image, depends on all of these
variables and is described separately for each border mode. The pixel indexing
nomenclature is decribed in the Convolution Filter Specification subsection of
section 3.6.3.
     One-dimensional filter:
                                      Wf −1
                           C[i ] =            Cs [i + n] ∗ Cf [n]
                                       n=0
    Two-dimensional filter:
                             Wf −1 Hf −1
               C[i , j ] =                 Cs [i + n, j + m] ∗ Cf [n, m]
                             n=0 m=0
    Two-dimensional separable filter:

                      Wf −1 Hf −1
        C[i , j ] =                 Cs [i + n, j + m] ∗ Crow [n] ∗ Ccolumn [m]
                      n=0 m=0


                             Version 1.3 - August 14, 2001
108                                              CHAPTER 3. RASTERIZATION


     If Wf of a one-dimensional filter is zero, then C[i] is always set to zero. Like-
wise, if either Wf or Hf of a two-dimensional filter is zero, then C[i, j] is always
set to zero.
     The convolution border mode for a specific convolution filter is specified by
calling

      void ConvolutionParameter{if}( enum target, enum pname,
         T param );

where target is the name of the filter, pname is CONVOLUTION BORDER MODE, and
param is one of REDUCE, CONSTANT BORDER or REPLICATE BORDER.

Border Mode REDUCE
The width and height of source images convolved with border mode REDUCE are
reduced by Wf − 1 and Hf − 1, respectively. If this reduction would generate
a resulting image with zero or negative width and/or height, the output is simply
null, with no error generated. The coordinates of the image that results from a con-
volution with border mode REDUCE are zero through Ws − Wf in width, and zero
through Hs − Hf in height. In cases where errors can result from the specification
of invalid image dimensions, it is these resulting dimensions that are tested, not
the dimensions of the source image. (A specific example is TexImage1D and Tex-
Image2D, which specify constraints for image dimensions. Even if TexImage1D
or TexImage2D is called with a null pixel pointer, the dimensions of the result-
ing texture image are those that would result from the convolution of the specified
image).
    When the border mode is REDUCE, Cs equals the source image color Cs and
Cr equals the filtered result C.
    For the remaining border modes, define Cw = Wf /2 and Ch = Hf /2 .
The coordinates (Cw , Ch ) define the center of the convolution filter.

Border Mode CONSTANT BORDER
If the convolution border mode is CONSTANT BORDER, the output image has the
same dimensions as the source image. The result of the convolution is the same
as if the source image were surrounded by pixels with the same color as the cur-
rent convolution border color. Whenever the convolution filter extends beyond
one of the edges of the source image, the constant-color border pixels are used
as input to the filter. The current convolution border color is set by calling Con-
volutionParameterfv or ConvolutionParameteriv with pname set to CONVOLU-
TION BORDER COLOR and params containing four values that comprise the RGBA

                           Version 1.3 - August 14, 2001
3.6. PIXEL RECTANGLES                                                            109


color to be used as the image border. Integer color components are interpreted
linearly such that the most positive integer maps to 1.0, and the most negative inte-
ger maps to -1.0. Floating point color components are not clamped when they are
specified.
    For a one-dimensional filter, the result color is defined by

                                   Cr [i] = C[i − Cw ]
where C[i ] is computed using the following equation for Cs [i ]:

                                       Cs [i ], 0 ≤ i < Ws
                         Cs [i ] =
                                       Cc ,     otherwise

and Cc is the convolution border color.
    For a two-dimensional or two-dimensional separable filter, the result color is
defined by

                              Cr [i, j] = C[i − Cw , j − Ch ]
where C[i , j ] is computed using the following equation for Cs [i , j ]:

                                Cs [i , j ], 0 ≤ i < Ws , 0 ≤ j < Hs
              Cs [i , j ] =
                                Cc ,         otherwise

Border Mode REPLICATE BORDER
The convolution border mode REPLICATE BORDER also produces an output im-
age with the same dimensions as the source image. The behavior of this mode is
identical to that of the CONSTANT BORDER mode except for the treatment of pixel
locations where the convolution filter extends beyond the edge of the source im-
age. For these locations, it is as if the outermost one-pixel border of the source
image was replicated. Conceptually, each pixel in the leftmost one-pixel column
of the source image is replicated Cw times to provide additional image data along
the left edge, each pixel in the rightmost one-pixel column is replicated Cw times
to provide additional image data along the right edge, and each pixel value in the
top and bottom one-pixel rows is replicated to create Ch rows of image data along
the top and bottom edges. The pixel value at each corner is also replicated in order
to provide data for the convolution operation at each corner of the source image.
    For a one-dimensional filter, the result color is defined by

                                   Cr [i] = C[i − Cw ]

                              Version 1.3 - August 14, 2001
110                                              CHAPTER 3. RASTERIZATION


where C[i ] is computed using the following equation for Cs [i ]:

                            Cs [i ] = Cs [clamp(i , Ws )]
and the clamping function clamp(val, max) is defined as
                                    
                                     0,
                                              val < 0
              clamp(val, max) =       val,     0 ≤ val < max
                                     max − 1, val ≥ max
                                    


    For a two-dimensional or two-dimensional separable filter, the result color is
defined by

                           Cr [i, j] = C[i − Cw , j − Ch ]
where C[i , j ] is computed using the following equation for Cs [i , j ]:

                  Cs [i , j ] = Cs [clamp(i , Ws ), clamp(j , Hs )]
    After convolution, each component of the resulting image is scaled by the
corresponding PixelTransfer parameters: POST CONVOLUTION RED SCALE
for an R component, POST CONVOLUTION GREEN SCALE for a G com-
ponent, POST CONVOLUTION BLUE SCALE for a B component, and
POST CONVOLUTION ALPHA SCALE for an A component.                      The result
is added to the corresponding bias:              POST CONVOLUTION RED BIAS,
POST CONVOLUTION GREEN BIAS,             POST CONVOLUTION BLUE BIAS,            or
POST CONVOLUTION ALPHA BIAS.
    The required state is three bits indicating whether each of one-dimensional,
two-dimensional, or separable two-dimensional convolution is enabled or disabled,
an integer describing the current convolution border mode, and four floating-point
values specifying the convolution border color. In the initial state, all convolu-
tion operations are disabled, the border mode is REDUCE, and the border color is
(0, 0, 0, 0).

Post Convolution Color Table Lookup
This step applies only to RGBA component groups. Post convolution color
table lookup is enabled or disabled by calling Enable or Disable with
the symbolic constant POST CONVOLUTION COLOR TABLE. The post convo-
lution table is defined by calling ColorTable with a target argument of
POST CONVOLUTION COLOR TABLE. In all other respects, operation is identical
to color table lookup, as defined earlier in section 3.6.5.

                           Version 1.3 - August 14, 2001
3.6. PIXEL RECTANGLES                                                             111


    The required state is one bit indicating whether post convolution table lookup
is enabled or disabled. In the initial state, lookup is disabled.


Color Matrix Transformation

This step applies only to RGBA component groups. The components are
transformed by the color matrix. Each transformed component is multiplied
by an appropriate signed scale factor: POST COLOR MATRIX RED SCALE
for an R component, POST COLOR MATRIX GREEN SCALE for a G
component,       POST COLOR MATRIX BLUE SCALE for a B component,
and POST COLOR MATRIX ALPHA SCALE for an A component.                             The
result is added to a signed bias:                 POST COLOR MATRIX RED BIAS,
POST COLOR MATRIX GREEN BIAS,              POST COLOR MATRIX BLUE BIAS,             or
POST COLOR MATRIX ALPHA BIAS. The resulting components replace each
component of the original group.
    That is, if Mc is the color matrix, a subscript of s represents the scale term for
a component, and a subscript of b represents the bias term, then the components

                                        R
                                           
                                       G
                                        
                                       B
                                        A
are transformed to

              R     Rs          0     0    0         R       Rb
                                                              
            G   0            Gs    0    0      G   Gb 
                                                          
            B  =  0                          Mc      +
                                                             .
                                0     Bs   0       B   Bb 
              A      0          0     0    As        A       Ab


Post Color Matrix Color Table Lookup

This step applies only to RGBA component groups.               Post color matrix
color table lookup is enabled or disabled by calling Enable or Disable
with the symbolic constant POST COLOR MATRIX COLOR TABLE. The post color
matrix table is defined by calling ColorTable with a target argument of
POST COLOR MATRIX COLOR TABLE. In all other respects, operation is identical
to color table lookup, as defined in section 3.6.5.
    The required state is one bit indicating whether post color matrix lookup is
enabled or disabled. In the initial state, lookup is disabled.

                            Version 1.3 - August 14, 2001
112                                              CHAPTER 3. RASTERIZATION


Histogram

This step applies only to RGBA component groups. Histogram operation is en-
abled or disabled by calling Enable or Disable with the symbolic constant HIS-
TOGRAM.
    If the width of the table is non-zero, then indices Ri , Gi , Bi , and Ai are de-
rived from the red, green, blue, and alpha components of each pixel group (without
modifying these components) by clamping each component to [0, 1] , multiplying
by one less than the width of the histogram table, and rounding to the nearest in-
teger. If the format of the HISTOGRAM table includes red or luminance, the red or
luminance component of histogram entry Ri is incremented by one. If the format
of the HISTOGRAM table includes green, the green component of histogram entry
Gi is incremented by one. The blue and alpha components of histogram entries
Bi and Ai are incremented in the same way. If a histogram entry component is
incremented beyond its maximum value, its value becomes undefined; this is not
an error.
    If the Histogram sink parameter is FALSE, histogram operation has no effect
on the stream of pixel groups being processed. Otherwise, all RGBA pixel groups
are discarded immediately after the histogram operation is completed. Because
histogram precedes minmax, no minmax operation is performed. No pixel frag-
ments are generated, no change is made to texture memory contents, and no pixel
values are returned. However, texture object state is modified whether or not pixel
groups are discarded.


Minmax

This step applies only to RGBA component groups. Minmax operation is enabled
or disabled by calling Enable or Disable with the symbolic constant MINMAX.
     If the format of the minmax table includes red or luminance, the red compo-
nent value replaces the red or luminance value in the minimum table element if
and only if it is less than that component. Likewise, if the format includes red or
luminance and the red component of the group is greater than the red or luminance
value in the maximum element, the red group component replaces the red or lumi-
nance maximum component. If the format of the table includes green, the green
group component conditionally replaces the green minimum and/or maximum if
it is smaller or larger, respectively. The blue and alpha group components are
similarly tested and replaced, if the table format includes blue and/or alpha. The
internal type of the minimum and maximum component values is floating point,
with at least the same representable range as a floating point number used to rep-
resent colors (section 2.1.1). There are no semantics defined for the treatment of

                          Version 1.3 - August 14, 2001
3.7. BITMAPS                                                                            113


group component values that are outside the representable range.
    If the Minmax sink parameter is FALSE, minmax operation has no effect on
the stream of pixel groups being processed. Otherwise, all RGBA pixel groups are
discarded immediately after the minmax operation is completed. No pixel frag-
ments are generated, no change is made to texture memory contents, and no pixel
values are returned. However, texture object state is modified whether or not pixel
groups are discarded.

3.6.6   Pixel Rectangle Multisample Rasterization
If MULTISAMPLE is enabled, and the value of SAMPLE BUFFERS is one, then pixel
rectangles are rasterized using the following algorithm. Let (Xrp , Yrp ) be the cur-
rent raster position. (If the current raster position is invalid, then DrawPixels is
ignored.) If a particular group (index or components) is the nth in a row and be-
longs to the mth row, consider the region in window coordinates bounded by the
rectangle with corners

                          (Xrp + Zx ∗ n, Yrp + Zy ∗ m)
and
                    (Xrp + Zx ∗ (n + 1), Yrp + Zy ∗ (m + 1))


where Zx and Zy are the pixel zoom factors specified by PixelZoom, and may
each be either positive or negative. A fragment representing group (n, m) is pro-
duced for each framebuffer pixel with one or more sample points that lie inside,
or on the bottom or left boundary, of this rectangle. Each fragment so produced
takes its associated data from the group and from the current raster position, in a
manner consistent with the discussion in the Conversion to Fragments subsection
of section 3.6.4. All depth and color sample values are assigned the same value,
taken either from their group (for depth and color component groups) or from the
current raster position (if they are not). All sample values are assigned the same
set of texture coordinates, taken from the current raster position.
    A single pixel rectangle will generate multiple, perhaps very many fragments
for the same framebuffer pixel, depending on the pixel zoom factors.


3.7     Bitmaps
Bitmaps are rectangles of zeros and ones specifying a particular pattern of frag-
ments to be produced. Each of these fragments has the same associated data. These
data are those associated with the current raster position.

                               Version 1.3 - August 14, 2001
114                                                                                              CHAPTER 3. RASTERIZATION


                                                                                                 )        )        )
                                                  2       2   3   2   3   1   3   1   0 1    0        0




                                                                                                 )        )        )
                                                  2       2   3   2   3   1   3   1   0 1    0        0




                                         4    4   5   4   5   (   5   (   '   (   '   & '    &   )%   &   )%   $   )%   $   #   $   #   #
                                                  2       2   3   2   3   1   3   1   0 1    0        0




                                         4    4   5   4   5   (   5   (   '   (   '   & '    &   %    &   %    $   %    $   #   $   #   #




                                         6    6   7   6   7       7                                            !        !   "   !   "   "
                                         4    4   5   4   5   (   5   (   '   (   '   & '    &   %    &   %    $   %    $   #   $   #   #




                                         6    6   7   6   7       7                                            !        !   "   !   "   "




                                         8    8   9   8   9       9                                                           
                                         6    6   7   6   7       7                                            !        !   "   !   "   "




                                         8    8   9   8   9       9                                                           




                                                                                                                                
                                         8    8   9   8   9       9                                                           




                                                                                                                                




                                                                                                                     
                                                                                                                                




                                                                                                                     




                         h = 12                               ¨       ¨   ©
                                                                          
                                                                              ¨   ©
                                                                                  
                                                                                       ©
                                                                                       
                                                                                             
                                                                                             
                                                                                                 
                                                                                                 
                                                                                                      
                                                                                                      
                                                                                                          
                                                                                                              
                                                                                                                   
                                                                                                                              




                                                              ¨       ¨   ©   ¨   ©    ©                      




                                                              ¦       ¦   §   ¦   §      §
                                                              ¨       ¨   ©   ¨   ©    ©                      




                                                              ¦       ¦   §   ¦   §      §




                                                              ¤       ¤   ¥   ¤   ¥      ¥
                                                              ¦       ¦   §   ¦   §      §




                                                              ¤       ¤   ¥   ¤   ¥      ¥




                                                              ¤       ¤   ¥   ¤   ¥      ¥




                                                              ¢       ¢   £   ¢   £      £




                                  ybo = 1.0
                                                              ¢       ¢   £   ¢   £      £




                                                                          ¡       ¡      ¡
                                                              ¢       ¢   £   ¢   £      £




                                                                          ¡       ¡      ¡




                                                                          ¡       ¡      ¡




                                             xbo = 2.5

                                                                                             w=8




   Figure 3.9. A bitmap and its associated parameters. xbi and ybi are not shown.



      Bitmaps are sent using

        void Bitmap( sizei w, sizei h, float xbo , float ybo ,
           float xbi , float ybi , ubyte *data );

w and h comprise the integer width and height of the rectangular bitmap, respec-
tively. (xbo , ybo ) gives the floating-point x and y values of the bitmap’s origin.
(xbi , ybi ) gives the floating-point x and y increments that are added to the raster
position after the bitmap is rasterized. data is a pointer to a bitmap.
    Like a polygon pattern, a bitmap is unpacked from memory according to the
procedure given in section 3.6.4 for DrawPixels; it is as if the width and height
passed to that command were equal to w and h, respectively, the type were BITMAP,
and the format were COLOR INDEX. The unpacked values (before any conversion
or arithmetic would have been performed) form a stipple pattern of zeros and ones.
See figure 3.9.
    A bitmap sent using Bitmap is rasterized as follows. First, if the current raster
position is invalid (the valid bit is reset), the bitmap is ignored. Otherwise, a rect-
angular array of fragments is constructed, with lower left corner at

                       (xll , yll ) = ( xrp − xbo , yrp − ybo )

                            Version 1.3 - August 14, 2001
3.8. TEXTURING                                                                    115


and upper right corner at (xll + w, yll + h) where w and h are the width and height
of the bitmap, respectively. Fragments in the array are produced if the correspond-
ing bit in the bitmap is 1 and not produced otherwise. The associated data for each
fragment are those associated with the current raster position, with texture coordi-
nates s, t, and r replaced with s/q, t/q, and r/q, respectively. If q is less than or
equal to zero, the results are undefined. Once the fragments have been produced,
the current raster position is updated:

                        (xrp , yrp ) ← (xrp + xbi , yrp + ybi ).

The z and w values of the current raster position remain unchanged.

Bitmap Multisample Rasterization
If MULTISAMPLE is enabled, and the value of SAMPLE BUFFERS is one, then
bitmaps are rasterized using the following algorithm. If the current raster position
is invalid, the bitmap is ignored. Otherwise, a screen-aligned array of pixel-size
rectangles is constructed, with its lower left corner at (Xrp , Yrp ), and its upper
right corner at (Xrp + w, Yrp + h), where w and h are the width and height of
the bitmap. Rectangles in this array are eliminated if the corresponding bit in the
bitmap is 0, and are retained otherwise. Bitmap rasterization produces a fragment
for each framebuffer pixel with one or more sample points either inside or on the
bottom or left edge of a retained rectangle.
     Coverage bits that correspond to sample points either inside or on the bottom
or left edge of a retained rectangle are 1, other coverage bits are 0. The associated
data for each sample are those associated with the current raster position. Once the
fragments have been produced, the current raster position is updated exactly as it
is in the single-sample rasterization case.


3.8    Texturing
Texturing maps a portion of one or more specified images onto each primitive for
which texturing is enabled. This mapping is accomplished by using the color of an
image at the location indicated by a fragment’s (s, t, r) coordinates to modify the
fragment’s primary RGBA color. Texturing does not affect the secondary color.
    An implementation may support texturing using more than one image at a time.
In this case the fragment carries multiple sets of texture coordinates (s, t, r) which
are used to index separate images to produce color values which are collectively
used to modify the fragment’s RGBA color. Texturing is specified only for RGBA
mode; its use in color index mode is undefined. The following subsections (up

                           Version 1.3 - August 14, 2001
116                                            CHAPTER 3. RASTERIZATION


to and including Section 3.8.7) specify the GL operation with a single texture and
Section 3.8.13 specifies the details of how multiple texture units interact.
     The GL provides a means to specify the details of how texturing of a primitive
is effected. These details include specification of the image to be texture mapped,
the means by which the image is filtered when applied to the primitive, and the
function that determines what RGBA value is produced given a fragment color and
an image value.

3.8.1    Texture Image Specification
The command

        void TexImage3D( enum target, int level, int internalformat,
           sizei width, sizei height, sizei depth, int border,
           enum format, enum type, void *data );

is used to specify a three-dimensional texture image. target must be either TEX-
TURE 3D, or PROXY TEXTURE 3D in the special case discussed in section 3.8.10.
format, type, and data match the corresponding arguments to DrawPixels (refer to
section 3.6.4); they specify the format of the image data, the type of those data,
and a pointer to the image data in host memory. The formats STENCIL INDEX and
DEPTH COMPONENT are not allowed.
     The groups in memory are treated as being arranged in a sequence of adja-
cent rectangles. Each rectangle is a two-dimensional image, whose size and or-
ganization are specified by the width and height parameters to TexImage3D. The
values of UNPACK ROW LENGTH and UNPACK ALIGNMENT control the row-to-row
spacing in these images in the same manner as DrawPixels. If the value of the in-
teger parameter UNPACK IMAGE HEIGHT is not positive, then the number of rows
in each two-dimensional image is height; otherwise the number of rows is UN-
PACK IMAGE HEIGHT. Each two-dimensional image comprises an integral number
of rows, and is exactly adjacent to its neighbor images.
     The mechanism for selecting a sub-volume of a three-dimensional image re-
lies on the integer parameter UNPACK SKIP IMAGES. If UNPACK SKIP IMAGES
is positive, the pointer is advanced by UNPACK SKIP IMAGES times the number of
elements in one two-dimensional image before obtaining the first group from mem-
ory. Then depth two-dimensional images are processed, each having a subimage
extracted in the same manner as DrawPixels.
     The selected groups are processed exactly as for DrawPixels, stopping just
before final conversion. Each R, G, B, and A value so generated is clamped to
[0, 1].

                          Version 1.3 - August 14, 2001
3.8. TEXTURING                                                                    117


     Components are then selected from the resulting R, G, B, and A values to
obtain a texture with the base internal format specified by (or derived from) inter-
nalformat. Table 3.15 summarizes the mapping of R, G, B, and A values to texture
components, as a function of the base internal format of the texture image. internal-
format may be specified as one of the six base internal format symbolic constants
listed in table 3.15, as one of the sized internal format symbolic constants listed
in table 3.16, as one of the specific compressed internal format symbolic constants
listed in table 3.17, or as one of the six generic compressed internal format sym-
bolic constants listed in table 3.18. internalformat may (for backwards compati-
bility with the 1.0 version of the GL) also take on the integer values 1, 2, 3, and
4, which are equivalent to symbolic constants LUMINANCE, LUMINANCE ALPHA,
RGB, and RGBA respectively. Specifying a value for internalformat that is not one
of the above values generates the error INVALID VALUE.
     The GL provides no specific compressed internal formats but does provide a
mechanism to obtain token values for such formats provided by extensions. The
number of specific compressed internal formats supported by the renderer can
be obtained by querying the value of NUM COMPRESSED TEXTURE FORMATS. The
set of specific compressed internal formats supported by the renderer can be ob-
tained by querying the value of COMPRESSED TEXTURE FORMATS. The only val-
ues returned by this query are those corresponding to formats suitable for general-
purpose usage. The renderer will not enumerate formats with restrictions that need
to be specifically understood prior to use.
     Generic compressed internal formats are never used directly as the internal for-
mats of texture images. If internalformat is one of the six generic compressed
internal formats, its value is replaced by the symbolic constant for a specific com-
pressed internal format of the GL’s choosing with the same base internal format.
If no specific compressed format is available, internalformat is instead replaced by
the corresponding base internal format. If internalformat is given as or mapped
to a specific compressed internal format, but the GL can not support images com-
pressed in the chosen internal format for any reason (e.g., the compression format
might not support 3D textures or borders), internalformat is replaced by the corre-
sponding base internal format and the texture image will not be compressed by the
GL.
     The internal component resolution is the number of bits allocated to each value
in a texture image. If internalformat is specified as a base internal format, the GL
stores the resulting texture with internal component resolutions of its own choos-
ing. If a sized internal format is specified, the mapping of the R, G, B, and A values
to texture components is equivalent to the mapping of the corresponding base in-
ternal format’s components, as specified in table 3.15, and the memory allocation
per texture component is assigned by the GL to match the allocations listed in

                           Version 1.3 - August 14, 2001
118                                              CHAPTER 3. RASTERIZATION


          Base Internal Format     RGBA Values       Internal Components
          ALPHA                    A                 A
          LUMINANCE                R                 L
          LUMINANCE ALPHA          R,A               L,A
          INTENSITY                R                 I
          RGB                      R,G,B             R,G,B
          RGBA                     R,G,B,A           R,G,B,A

Table 3.15: Conversion from RGBA pixel components to internal texture, table, or
filter components. See section 3.8.12 for a description of the texture components
R, G, B, A, L, and I.



table 3.16 as closely as possible. (The definition of closely is left up to the imple-
mentation. Implementations are not required to support more than one resolution
for each base internal format.) If a compressed internal format is specified, the
mapping of the R, G, B, and A values to texture components is equivalent to the
mapping of the corresponding base internal format’s components, as specified in
table 3.15. The specified image is compressed using a (possibly lossy) compression
algorithm chosen by the GL.
     A GL implementation may vary its allocation of internal component resolution
or compressed internal format based on any TexImage3D, TexImage2D (see be-
low), or TexImage1D (see below) parameter (except target), but the allocation and
chosen compressed image format must not be a function of any other state and can-
not be changed once they are established. In addition, the choice of a compressed
image format may not be affected by the data parameter. Allocations must be in-
variant; the same allocation and compressed image format must be chosen each
time a texture image is specified with the same parameter values. These allocation
rules also apply to proxy textures, which are described in section 3.8.10.
     The image itself (pointed to by data) is a sequence of groups of values. The
first group is the lower left back corner of the texture image. Subsequent groups
fill out rows of width width from left to right; height rows are stacked from bottom
to top forming a single two-dimensional image slice; and depth slices are stacked
from back to front. When the final R, G, B, and A components have been computed
for a group, they are assigned to components of a texel as described by table 3.15.
Counting from zero, each resulting N th texel is assigned internal integer coordi-
nates (i, j, k), where

                             i = (N mod width) − bs

                           Version 1.3 - August 14, 2001
3.8. TEXTURING                                                                  119


 Sized                       Base                    R      G      B      A      L      I
 Internal Format             Internal Format        bits   bits   bits   bits   bits   bits
 ALPHA4                      ALPHA                                        4
 ALPHA8                      ALPHA                                        8
 ALPHA12                     ALPHA                                       12
 ALPHA16                     ALPHA                                       16
 LUMINANCE4                  LUMINANCE                                           4
 LUMINANCE8                  LUMINANCE                                           8
 LUMINANCE12                 LUMINANCE                                          12
 LUMINANCE16                 LUMINANCE                                          16
 LUMINANCE4 ALPHA4           LUMINANCE    ALPHA                           4      4
 LUMINANCE6 ALPHA2           LUMINANCE    ALPHA                           2      6
 LUMINANCE8 ALPHA8           LUMINANCE    ALPHA                           8      8
 LUMINANCE12 ALPHA4          LUMINANCE    ALPHA                           4     12
 LUMINANCE12 ALPHA12         LUMINANCE    ALPHA                          12     12
 LUMINANCE16 ALPHA16         LUMINANCE    ALPHA                          16     16
 INTENSITY4                  INTENSITY                                                 4
 INTENSITY8                  INTENSITY                                                 8
 INTENSITY12                 INTENSITY                                                 12
 INTENSITY16                 INTENSITY                                                 16
 R3 G3 B2                    RGB                     3     3      2
 RGB4                        RGB                     4     4      4
 RGB5                        RGB                     5     5      5
 RGB8                        RGB                     8     8      8
 RGB10                       RGB                     10    10     10
 RGB12                       RGB                     12    12     12
 RGB16                       RGB                     16    16     16
 RGBA2                       RGBA                    2     2      2      2
 RGBA4                       RGBA                    4     4      4      4
 RGB5 A1                     RGBA                    5     5      5      1
 RGBA8                       RGBA                    8     8      8      8
 RGB10 A2                    RGBA                    10    10     10     2
 RGBA12                      RGBA                    12    12     12     12
 RGBA16                      RGBA                    16    16     16     16

Table 3.16: Correspondence of sized internal formats to base internal formats, and
desired component resolutions for each sized internal format.



                          Version 1.3 - August 14, 2001
120                                               CHAPTER 3. RASTERIZATION


               Compressed Internal Format        Base Internal Format
               (none)

Table 3.17: Specific compressed internal formats. None are defined by OpenGL
1.3; however, several specific compression types are defined in GL extensions.


           Generic Compressed Internal Format         Base Internal Format
           COMPRESSED     ALPHA                       ALPHA
           COMPRESSED     LUMINANCE                   LUMINANCE
           COMPRESSED     LUMINANCE ALPHA             LUMINANCE ALPHA
           COMPRESSED     INTENSITY                   INTENSITY
           COMPRESSED     RGB                         RGB
           COMPRESSED     RGBA                        RGBA

                 Table 3.18: Generic compressed internal formats.


                                   N
                         j=(              mod height) − bs
                                 width
                                    N
                     k=(                        mod depth) − bs
                           width × height
and bs is the specified border width. Thus the last two-dimensional image slice of
the three-dimensional image is indexed with the highest value of k.
    Each color component is converted (by rounding to nearest) to a fixed-point
value with n bits, where n is the number of bits of storage allocated to that com-
ponent in the image array. We assume that the fixed-point representation used
represents each value k/(2n − 1), where k ∈ {0, 1, . . . , 2n − 1}, as k (e.g. 1.0 is
represented in binary as a string of all ones).
    The level argument to TexImage3D is an integer level-of-detail number. Levels
of detail are discussed below, under Mipmapping. The main texture image has a
level of detail number of 0. If a level-of-detail less than zero is specified, the error
INVALID VALUE is generated.
    The border argument to TexImage3D is a border width. The significance of
borders is described below. The border width affects the required dimensions of
the texture image: it must be the case that

                                   ws = 2n + 2bs                                 (3.11)

                                   hs = 2m + 2bs                                 (3.12)

                           Version 1.3 - August 14, 2001
3.8. TEXTURING                                                                   121



                                   ds = 2l + 2bs                              (3.13)
for some integers n, m, and l, where ws , hs , and ds are the specified image width,
height, and depth. If any one of these relationships cannot be satisfied, then the
error INVALID VALUE is generated.
     Currently, the maximum border width bt is 1. If bs is less than zero, or greater
than bt , then the error INVALID VALUE is generated.
     The maximum allowable width, height, or depth of a three-dimensional texture
image is an implementation dependent function of the level-of-detail and internal
format of the resulting image array. It must be at least 2k−lod +2bt for image arrays
of level-of-detail 0 through k, where k is the log base 2 of MAX 3D TEXTURE SIZE,
lod is the level-of-detail of the image array, and bt is the maximum border width.
It may be zero for image arrays of any level-of-detail greater than k. The error
INVALID VALUE is generated if the specified image is too large to be stored under
any conditions.
     In a similar fashion, the maximum allowable width of a one- or two-
dimensional texture image, and the maximum allowable height of a two-
dimensional texture image, must be at least 2k−lod + 2bt for image arrays of level
0 through k, where k is the log base 2 of MAX TEXTURE SIZE. The maximum al-
lowable width and height of a cube map texture must be the same, and must be at
least 2k−lod + 2bt for image arrays level 0 through k, where k is the log base 2 of
MAX CUBE MAP TEXTURE SIZE.
     An implementation may allow an image array of level 0 to be created only if
that single image array can be supported. Additional constraints on the creation of
image arrays of level 1 or greater are described in more detail in section 3.8.9.
     The command

      void TexImage2D( enum target, int level,
        int internalformat, sizei width, sizei height,
        int border, enum format, enum type, void *data );

is used to specify a two-dimensional texture image. target must be one of TEX-
TURE 2D              for            a            two-dimensional            texture,
or one of TEXTURE CUBE MAP POSITIVE X, TEXTURE CUBE MAP NEGATIVE X,
TEXTURE CUBE MAP POSITIVE Y, TEXTURE CUBE MAP NEGATIVE Y, TEX-
TURE CUBE MAP POSITIVE Z, or TEXTURE CUBE MAP NEGATIVE Z for a cube
map texture. Additionally, target may be either PROXY TEXTURE 2D for a two-
dimensional proxy texture or PROXY TEXTURE CUBE MAP for a cube map proxy
texture in the special case discussed in section 3.8.10. The other parameters match
the corresponding parameters of TexImage3D.

                          Version 1.3 - August 14, 2001
122                                             CHAPTER 3. RASTERIZATION


    For the purposes of decoding the texture image, TexImage2D is equivalent to
calling TexImage3D with corresponding arguments and depth of 1, except that

   • The depth of the image is always 1 regardless of the value of border.

   • Convolution will be performed on the image (possibly changing its width
     and height) if SEPARABLE 2D or CONVOLUTION 2D is enabled.

   • UNPACK SKIP IMAGES is ignored.

    A two-dimensional texture consists of a single two-dimensional texture image.
A cube map texture is a set of six two-dimensional texture images. The six cube
map texture targets form a single cube map texture though each target names a
distinct face of the cube map. The TEXTURE CUBE MAP * targets listed above up-
date their appropriate cube map face 2D texture image. Note that the six cube map
two-dimensional image tokens such as TEXTURE CUBE MAP POSITIVE X are used
when specifying, updating, or querying one of a cube map’s six two-dimensional
images, but when enabling cube map texturing or binding to a cube map texture
object (that is when the cube map is accessed as a whole as opposed to a particular
two-dimensional image), the TEXTURE CUBE MAP target is specified.
    When the target parameter to TexImage2D is one of the six cube map two-
dimensional image targets, the error INVALID VALUE is generated if the width and
height parameters are not equal.
    Finally, the command

      void TexImage1D( enum target, int level,
         int internalformat, sizei width, int border,
         enum format, enum type, void *data );

is used to specify a one-dimensional texture image. target must be either TEX-
TURE 1D, or PROXY TEXTURE 1D in the special case discussed in section 3.8.10.)
    For the purposes of decoding the texture image, TexImage1D is equivalent to
calling TexImage2D with corresponding arguments and height of 1, except that

   • The height of the image is always 1 regardless of the value of border.

   • Convolution will be performed on the image (possibly changing its width)
     only if CONVOLUTION 1D is enabled.

   An image with zero width, height (TexImage2D and TexImage3D only), or
depth (TexImage3D only) indicates the null texture. If the null texture is specified

                          Version 1.3 - August 14, 2001
3.8. TEXTURING                                                                           123


for the level-of-detail specified by texture parameter TEXTURE BASE LEVEL (see
section 3.8.4), it is as if texturing were disabled.
    The image indicated to the GL by the image pointer is decoded and copied into
the GL’s internal memory. This copying effectively places the decoded image in-
side a border of the maximum allowable width bt whether or not a border has been
specified (see figure 3.10) 1 . If no border or a border smaller than the maximum
allowable width has been specified, then the image is still stored as if it were sur-
rounded by a border of the maximum possible width. Any excess border (which
surrounds the specified image, including any border) is assigned unspecified val-
ues. A two-dimensional texture has a border only at its left, right, top, and bottom
ends, and a one-dimensional texture has a border only at its left and right ends.
    We shall refer to the (possibly border augmented) decoded image as the texture
array. A three-dimensional texture array has width, height, and depth

                                          wt = 2n + 2bt
                                         ht = 2m + 2bt
                                          dt = 2l + 2bt
where bt is the maximum allowable border width and n, m, and l are defined in
equations 3.11, 3.12, and 3.13. A two-dimensional texture array has depth dt = 1,
with height ht and width wt as above, and a one-dimensional texture array has
depth dt = 1, height ht = 1, and width wt as above.
    An element (i, j, k) of the texture array is called a texel (for a two-dimensional
texture, k is irrelevant; for a one-dimensional texture, j and k are both irrelevant).
The texture value used in texturing a fragment is determined by that fragment’s
associated (s, t, r) coordinates, but may not correspond to any actual texel. See
figure 3.10.
    If the data argument of TexImage1D, TexImage2D, or TexImage3D is a null
pointer (a zero-valued pointer in the C implementation), a one-, two-, or three-
dimensional texture array is created with the specified target, level, internalformat,
width, height, and depth, but with unspecified image contents. In this case no pixel
values are accessed in client memory, and no pixel processing is performed. Errors
are generated, however, exactly as though the data pointer were valid.

3.8.2      Alternate Texture Image Specification Commands
Two-dimensional and one-dimensional texture images may also be specified us-
ing image data taken directly from the framebuffer, and rectangular subregions of
existing texture images may be respecified.
   1
       Figure 3.10 needs to show a three-dimensional texture image.


                                     Version 1.3 - August 14, 2001
124                                                                     CHAPTER 3. RASTERIZATION




             5.0
                       4
      1.0
                       3

                       2                            α
       t      v    j                                    β
                       1

                       0
      0.0
                   −1
            −1.0
                           −1         0    1    2       3       4   5     6   7     8
                                                            i
                   −1.0                                     u                           9.0
                                0.0                         s                     1.0



  Figure 3.10. A texture image and the coordinates used to access it. This is a two-
  dimensional texture with n = 3 and m = 2. A one-dimensional texture would
  consist of a single horizontal strip. α and β, values used in blending adjacent texels
  to obtain a texture value, are also shown.




                                          Version 1.3 - August 14, 2001
3.8. TEXTURING                                                                  125


   The command

      void CopyTexImage2D( enum target, int level,
         enum internalformat, int x, int y, sizei width,
         sizei height, int border );

defines a two-dimensional texture array in exactly the manner of Tex-
Image2D, except that the image data are taken from the framebuffer
rather than from client memory. Currently, target must be one of TEX-
TURE 2D, TEXTURE CUBE MAP POSITIVE X, TEXTURE CUBE MAP NEGATIVE X,
TEXTURE CUBE MAP POSITIVE Y, TEXTURE CUBE MAP NEGATIVE Y, TEX-
TURE CUBE MAP POSITIVE Z, or TEXTURE CUBE MAP NEGATIVE Z. x, y, width,
and height correspond precisely to the corresponding arguments to CopyPixels (re-
fer to section 4.3.3); they specify the image’s width and height, and the lower left
(x, y) coordinates of the framebuffer region to be copied. The image is taken from
the framebuffer exactly as if these arguments were passed to CopyPixels, with
argument type set to COLOR, stopping after pixel transfer processing is complete.
Subsequent processing is identical to that described for TexImage2D, beginning
with clamping of the R, G, B, and A values from the resulting pixel groups. Pa-
rameters level, internalformat, and border are specified using the same values, with
the same meanings, as the equivalent arguments of TexImage2D, except that in-
ternalformat may not be specified as 1, 2, 3, or 4. An invalid value specified
for internalformat generates the error INVALID ENUM. The constraints on width,
height, and border are exactly those for the equivalent arguments of TexImage2D.
     When the target parameter to CopyTexImage2D is one of the six cube map
two-dimensional image targets, the error INVALID VALUE is generated if the width
and height parameters are not equal.
     The command

      void CopyTexImage1D( enum target, int level,
         enum internalformat, int x, int y, sizei width,
         int border );

defines a one-dimensional texture array in exactly the manner of TexImage1D,
except that the image data are taken from the framebuffer, rather than from client
memory. Currently, target must be TEXTURE 1D. For the purposes of decoding
the texture image, CopyTexImage1D is equivalent to calling CopyTexImage2D
with corresponding arguments and height of 1, except that the height of the image
is always 1, regardless of the value of border. level, internalformat, and border
are specified using the same values, with the same meanings, as the equivalent

                          Version 1.3 - August 14, 2001
126                                               CHAPTER 3. RASTERIZATION


arguments of TexImage1D, except that internalformat may not be specified as 1,
2, 3, or 4. The constraints on width and border are exactly those of the equivalent
arguments of TexImage1D.
    Six additional commands,
      void TexSubImage3D( enum target, int level, int xoffset,
         int yoffset, int zoffset, sizei width, sizei height,
         sizei depth, enum format, enum type, void *data );
      void TexSubImage2D( enum target, int level, int xoffset,
         int yoffset, sizei width, sizei height, enum format,
         enum type, void *data );
      void TexSubImage1D( enum target, int level, int xoffset,
         sizei width, enum format, enum type, void *data );
      void CopyTexSubImage3D( enum target, int level,
         int xoffset, int yoffset, int zoffset, int x, int y,
         sizei width, sizei height );
      void CopyTexSubImage2D( enum target, int level,
         int xoffset, int yoffset, int x, int y, sizei width,
         sizei height );
      void CopyTexSubImage1D( enum target, int level,
         int xoffset, int x, int y, sizei width );
respecify only a rectangular subregion of an existing texture array.                 No
change is made to the internalformat, width, height, depth, or border pa-
rameters of the specified texture array, nor is any change made to texel val-
ues outside the specified subregion. Currently the target arguments of Tex-
SubImage1D and CopyTexSubImage1D must be TEXTURE 1D, the target ar-
guments of TexSubImage2D and CopyTexSubImage2D must be one of TEX-
TURE 2D, TEXTURE CUBE MAP POSITIVE X, TEXTURE CUBE MAP NEGATIVE X,
TEXTURE CUBE MAP POSITIVE Y,                       TEXTURE CUBE MAP NEGATIVE Y,
TEXTURE CUBE MAP POSITIVE Z, or TEXTURE CUBE MAP NEGATIVE Z, and the
target arguments of TexSubImage3D and CopyTexSubImage3D must be TEX-
TURE 3D. The level parameter of each command specifies the level of the texture
array that is modified. If level is less than zero or greater than the base 2 logarithm
of the maximum texture width or height, the error INVALID VALUE is generated.
    TexSubImage3D arguments width, height, depth, format, type, and data match
the corresponding arguments to TexImage3D, meaning that they are specified us-
ing the same values, and have the same meanings. Likewise, TexSubImage2D
arguments width, height, format, type, and data match the corresponding argu-
ments to TexImage2D, and TexSubImage1D arguments width, format, type, and
data match the corresponding arguments to TexImage1D.

                           Version 1.3 - August 14, 2001
3.8. TEXTURING                                                                       127


    CopyTexSubImage3D and CopyTexSubImage2D arguments x, y, width,
and height match the corresponding arguments to CopyTexImage2D2 . CopyTex-
SubImage1D arguments x, y, and width match the corresponding arguments to
CopyTexImage1D. Each of the TexSubImage commands interprets and processes
pixel groups in exactly the manner of its TexImage counterpart, except that the
assignment of R, G, B, and A pixel group values to the texture components is
controlled by the internalformat of the texture array, not by an argument to the
command.
    Arguments xoffset, yoffset, and zoffset of TexSubImage3D and CopyTex-
SubImage3D specify the lower left texel coordinates of a width-wide by height-
high by depth-deep rectangular subregion of the texture array. The depth argument
associated with CopyTexSubImage3D is always 1, because framebuffer memory
is two-dimensional - only a portion of a single s, t slice of a three-dimensional
texture is replaced by CopyTexSubImage3D.
    Negative values of xoffset, yoffset, and zoffset correspond to the coordinates
of border texels, addressed as in figure 3.10. Taking ws , hs , ds , and bs to be
the specified width, height, depth, and border width of the texture array, (not the
actual array dimensions wt , ht , dt , and bt ), and taking x, y, z, w, h, and d to be
the xoffset, yoffset, zoffset, width, height, and depth argument values, any of the
following relationships generates the error INVALID VALUE:

                                        x < −bs
                                   x + w > ws − b s
                                        y < −bs
                                   y + h > hs − bs
                                        z < −bs
                                    z + d > d s − bs
(Recall that ds , ws , and hs include twice the specified border width bs .) Count-
ing from zero, the nth pixel group is assigned to the texel with internal integer
coordinates [i, j, k], where

                                  i = x + (n mod w)
                                           n
                                j =y+(        mod h)
                                           w
   2
    Because the framebuffer is inherently two-dimensional, there is no CopyTexImage3D com-
mand.


                            Version 1.3 - August 14, 2001
128                                              CHAPTER 3. RASTERIZATION

                                          n
                        k =z+(                     mod d
                                    width ∗ height
    Arguments xoffset and yoffset of TexSubImage2D and CopyTexSubImage2D
specify the lower left texel coordinates of a width-wide by height-high rectangular
subregion of the texture array. Negative values of xoffset and yoffset correspond
to the coordinates of border texels, addressed as in figure 3.10. Taking ws , hs ,
and bs to be the specified width, height, and border width of the texture array,
(not the actual array dimensions wt , ht , and bt ), and taking x, y, w, and h to
be the xoffset, yoffset, width, and height argument values, any of the following
relationships generates the error INVALID VALUE:

                                      x < −bs
                                 x + w > ws − bs
                                      y < −bs
                                  y + h > hs − bs
(Recall that ws and hs include twice the specified border width bs .) Counting from
zero, the nth pixel group is assigned to the texel with internal integer coordinates
[i, j], where

                                 i = x + (n mod w)
                                           n
                               j =y+(         mod h)
                                          w
     The xoffset argument of TexSubImage1D and CopyTexSubImage1D speci-
fies the left texel coordinate of a width-wide subregion of the texture array. Neg-
ative values of xoffset correspond to the coordinates of border texels. Taking ws
and bs to be the specified width and border width of the texture array, and x and
w to be the xoffset and width argument values, either of the following relationships
generates the error INVALID VALUE:

                                      x < −bs
                                 x + w > ws − bs
Counting from zero, the nth pixel group is assigned to the texel with internal integer
coordinates [i], where

                                i = x + (n mod w)
    Texture images with compressed internal formats may be stored in such a way
that it is not possible to modify an image with subimage commands without having

                           Version 1.3 - August 14, 2001
3.8. TEXTURING                                                                  129


to decompress and recompress the texture image. Even if the image were modi-
fied in this manner, it may not be possible to preserve the contents of some of
the texels outside the region being modified. To avoid these complications, the
GL does not support arbitrary modifications to texture images with compressed
internal formats. Calling TexSubImage3D, CopyTexSubImage3D, TexSubIm-
age2D, CopyTexSubImage2D, TexSubImage1D, or CopyTexSubImage1D will
result in an INVALID OPERATION error if xoffset, yoffset, or zoffset is not equal to
−bs (border width). In addition, the contents of any texel outside the region mod-
ified by such a call are undefined. These restrictions may be relaxed for specific
compressed internal formats whose images are easily modified.

3.8.3    Compressed Texture Images
Texture images may also be specified or modified using image data already stored
in a known compressed image format. The GL currently defines no such formats,
but provides mechanisms for GL extensions that do.
    The commands

        void CompressedTexImage1D( enum target, int level,
           enum internalformat, sizei width, int border,
           sizei imageSize, void *data );
        void CompressedTexImage2D( enum target, int level,
           enum internalformat, sizei width, sizei height,
           int border, sizei imageSize, void *data );
        void CompressedTexImage3D( enum target, int level,
           enum internalformat, sizei width, sizei height,
           sizei depth, int border, sizei imageSize, void *data );

define one-, two-, and three-dimensional texture images, respectively, with incom-
ing data stored in a specific compressed image format. The target, level, internal-
format, width, height, depth, and border parameters have the same meaning as in
TexImage1D, TexImage2D, and TexImage3D. data points to compressed image
data stored in the compressed image format corresponding to internalformat. Since
the GL provides no specific image formats, using any of the six generic compressed
internal formats as internalformat will result in an INVALID ENUM error.
    For all other compressed internal formats, the compressed image will be de-
coded according to the specification defining the internalformat token. Com-
pressed texture images are treated as an array of imageSize ubytes beginning at
address data. All pixel storage and pixel transfer modes are ignored when decoding
a compressed texture image. If the imageSize parameter is not consistent with the

                          Version 1.3 - August 14, 2001
130                                            CHAPTER 3. RASTERIZATION


format, dimensions, and contents of the compressed image, an INVALID VALUE
error results. If the compressed image is not encoded according to the defined
image format, the results of the call are undefined.
    Specific compressed internal formats may impose format-specific restrictions
on the use of the compressed image specification calls or parameters. For example,
the compressed image format might be supported only for 2D textures, or might
not allow non-zero border values. Any such restrictions will be documented in the
extension specification defining the compressed internal format; violating these
restrictions will result in an INVALID OPERATION error.
    Any restrictions imposed by specific compressed internal formats will be
invariant, meaning that if the GL accepts and stores a texture image in com-
pressed form, providing the same image to CompressedTexImage1D, Com-
pressedTexImage2D, or CompressedTexImage3D will not result in an IN-
VALID OPERATION error if the following restrictions are satisfied:

   • data points to a compressed texture image returned by GetCompressedTex-
     Image (section 6.1.4).
   • target, level, and internalformat match the target, level and format parame-
     ters provided to the GetCompressedTexImage call returning data.
   • width,     height,     depth,     border,     internalformat,      and
     imageSize match the values of TEXTURE WIDTH, TEXTURE HEIGHT, TEX-
     TURE DEPTH, TEXTURE BORDER, TEXTURE INTERNAL FORMAT, and TEX-
     TURE COMPRESSED IMAGE SIZE for image level level in effect at the time
     of the GetCompressedTexImage call returning data.

This guarantee applies not just to images returned by GetCompressedTexImage,
but also to any other properly encoded compressed texture image of the same size
and format.
    The commands

      void CompressedTexSubImage1D( enum target, int level,
         int xoffset, sizei width, enum format, sizei imageSize,
         void *data );
      void CompressedTexSubImage2D( enum target, int level,
         int xoffset, int yoffset, sizei width, sizei height,
         enum format, sizei imageSize, void *data );
      void CompressedTexSubImage3D( enum target, int level,
         int xoffset, int yoffset, int zoffset, sizei width,
         sizei height, sizei depth, enum format,
         sizei imageSize, void *data );

                          Version 1.3 - August 14, 2001
3.8. TEXTURING                                                                   131


respecify only a rectangular region of an existing texture array, with incoming data
stored in a known compressed image format. The target, level, xoffset, yoffset, zoff-
set, width, height, and depth parameters have the same meaning as in TexSubIm-
age1D, TexSubImage2D, and TexSubImage3D. data points to compressed im-
age data stored in the compressed image format corresponding to format. Since
the core GL provides no specific image formats, using any of these six generic
compressed internal formats as format will result in an INVALID ENUM error.
     The image pointed to by data and the imageSize parameter are interpreted
as though they were provided to CompressedTexImage1D, CompressedTexIm-
age2D, and CompressedTexImage3D. These commands do not provide for im-
age format conversion, so an INVALID OPERATION error results if format does
not match the internal format of the texture image being modified. If the image-
Size parameter is not consistent with the format, dimensions, and contents of the
compressed image (too little or too much data), an INVALID VALUE error results.
     As with CompressedTexImage calls, compressed internal formats may have
additional restrictions on the use of the compressed image specification calls or
parameters. Any such restrictions will be documented in the specification defin-
ing the compressed internal format; violating these restrictions will result in an
INVALID OPERATION error.
     Any restrictions imposed by specific compressed internal formats will be
invariant, meaning that if the GL accepts and stores a texture image in com-
pressed form, providing the same image to CompressedTexSubImage1D, Com-
pressedTexSubImage2D, CompressedTexSubImage3D will not result in an IN-
VALID OPERATION error if the following restrictions are satisfied:

   • data points to a compressed texture image returned by GetCompressedTex-
     Image (Section 6.1.4).

   • target, level, and format match the target, level and format parameters pro-
     vided to the GetCompressedTexImage call returning data.

   • width,                                                          height,
     depth, format, and imageSize match the values of TEXTURE WIDTH, TEX-
     TURE HEIGHT, TEXTURE DEPTH, TEXTURE INTERNAL FORMAT, and TEX-
     TURE COMPRESSED IMAGE SIZE for image level level in effect at the time
     of the GetCompressedTexImage call returning data.

   • width, height, depth, format match the values of TEXTURE WIDTH, TEX-
     TURE HEIGHT, TEXTURE DEPTH, and TEXTURE INTERNAL FORMAT cur-
     rently in effect for image level level.

                          Version 1.3 - August 14, 2001
132                                              CHAPTER 3. RASTERIZATION


   • xoffset, yoffset, and zoffset are all −b, where b is the value of TEX-
     TURE BORDER currently in effect for image level level.


     This guarantee applies not just to images returned by GetCompressedTexIm-
age, but also to any other properly encoded compressed texture image of the same
size.
     Calling CompressedTexSubImage3D, CompressedTexSubImage2D, or
CompressedTexSubImage1D will result in an INVALID OPERATION error if xoff-
set, yoffset, or zoffset is not equal to −bs (border width), or if width, height, and
depth do not match the values of TEXTURE WIDTH, TEXTURE HEIGHT, or TEX-
TURE DEPTH, respectively. The contents of any texel outside the region modified
by the call are undefined. These restrictions may be relaxed for specific compressed
internal formats whose images are easily modified.


3.8.4    Texture Parameters
Various parameters control how the texture array is treated when applied to a frag-
ment. Each parameter is set by calling


        void TexParameter{if}( enum target, enum pname, T param );
        void TexParameter{if}v( enum target, enum pname,
           T params );

target is the target, either TEXTURE 1D, TEXTURE 2D, TEXTURE 3D, or TEX-
TURE CUBE MAP. pname is a symbolic constant indicating the parameter to be
set; the possible constants and corresponding parameters are summarized in ta-
ble 3.19. In the first form of the command, param is a value to which to set a
single-valued parameter; in the second form of the command, params is an array
of parameters whose type depends on the parameter being set. If the values for
TEXTURE BORDER COLOR are specified as integers, the conversion for signed inte-
gers from table 2.6 is applied to convert the values to floating-point. Each of the
four values set by TEXTURE BORDER COLOR is clamped to lie in [0, 1].
    In the remainder of section 3.8, denote by lodmin , lodmax , levelbase ,
and levelmax the values of the texture parameters TEXTURE MIN LOD, TEX-
TURE MAX LOD, TEXTURE BASE LEVEL, and TEXTURE MAX LEVEL respectively.
    Texture parameters for a cube map texture apply to the cube map as a whole;
the six distinct two-dimensional texture images use the texture parameters of the
cube map itself.

                          Version 1.3 - August 14, 2001
3.8. TEXTURING                                                          133




  Name                        Type      Legal Values
  TEXTURE WRAP S             integer    CLAMP, CLAMP TO EDGE, REPEAT,
                                        CLAMP TO BORDER
  TEXTURE WRAP T             integer    CLAMP, CLAMP TO EDGE, REPEAT,
                                        CLAMP TO BORDER
  TEXTURE WRAP R             integer    CLAMP, CLAMP TO EDGE, REPEAT,
                                        CLAMP TO BORDER
  TEXTURE MIN FILTER         integer    NEAREST,
                                        LINEAR,
                                        NEAREST MIPMAP NEAREST,
                                        NEAREST MIPMAP LINEAR,
                                        LINEAR MIPMAP NEAREST,
                                        LINEAR MIPMAP LINEAR,
  TEXTURE MAG FILTER         integer    NEAREST,
                                        LINEAR
  TEXTURE   BORDER COLOR     4 floats   any 4 values in [0, 1]
  TEXTURE   PRIORITY          float     any value in [0, 1]
  TEXTURE   MIN LOD           float     any value
  TEXTURE   MAX LOD           float     any value
  TEXTURE   BASE LEVEL       integer    any non-negative integer
  TEXTURE   MAX LEVEL        integer    any non-negative integer

             Table 3.19: Texture parameters and their values.




                      Version 1.3 - August 14, 2001
134                                              CHAPTER 3. RASTERIZATION


3.8.5   Texture Wrap Modes
If TEXTURE WRAP S, TEXTURE WRAP T, or TEXTURE WRAP R is set to REPEAT,
then the GL ignores the integer part of s, t, or r coordinates, respectively, using
only the fractional part. (For a number f , the fractional part is f − f , regardless
of the sign of f ; recall that the floor function truncates towards −∞.) CLAMP
causes s, t, or r coordinates to be clamped to the range [0, 1]. The initial state is
for all of s, t, and r behavior to be that given by REPEAT.
    CLAMP TO EDGE clamps texture coordinates at all mipmap levels such that the
texture filter never samples a border texel. The color returned when clamping is
derived only from texels at the edge of the texture image.
    Texture coordinates are clamped to the range [min, max]. The minimum value
is defined as

                                             1
                                    min =
                                            2N
where N is the size of the one-, two-, or three-dimensional texture image in the
direction of clamping. The maximum value is defined as

                                 max = 1 − min

so that clamping is always symmetric about the [0, 1] mapped range of a texture
coordinate.
    CLAMP TO BORDER clamps texture coordinates at all mipmaps such that the
texture filter always samples border texels for fragments whose corresponding tex-
ture coordinate is sufficiently far outside the range [0, 1]. The color returned when
clamping is derived only from the border texels of the texture image, or from the
constant border color if the texture image does not have a border.
    Texture coordinates are clamped to the range [min, max]. The minimum value
is defined as

                                            −1
                                    min =
                                            2N
where N is the size (not including borders) of the one-, two-, or three-dimensional
texture image in the direction of clamping. The maximum value is defined as

                                 max = 1 − min

so that clamping is always symmetric about the [0, 1] mapped range of a texture
coordinate.

                          Version 1.3 - August 14, 2001
3.8. TEXTURING                                                                    135


 Major Axis Direction      Target                                 sc     tc      ma
 +rx                       TEXTURE   CUBE   MAP   POSITIVE   X    −rz    −ry     rx
 −rx                       TEXTURE   CUBE   MAP   NEGATIVE   X    rz     −ry     rx
 +ry                       TEXTURE   CUBE   MAP   POSITIVE   Y    rx     rz      ry
 −ry                       TEXTURE   CUBE   MAP   NEGATIVE   Y    rx     −rz     ry
 +rz                       TEXTURE   CUBE   MAP   POSITIVE   Z    rx     −ry     rz
 −rz                       TEXTURE   CUBE   MAP   NEGATIVE   Z    −rx    −ry     rz

Table 3.20: Selection of cube map images based on major axis direction of texture
coordinates.


3.8.6   Cube Map Texture Selection
When cube map texturing is enabled, the ( s t r ) texture coordinates are treated
as a direction vector ( rx ry rz ) emanating from the center of a cube (the q
coordinate can be ignored, since it merely scales the vector without affecting the
direction.) At texture application time, the interpolated per-fragment direction vec-
tor selects one of the cube map face’s two-dimensional images based on the largest
magnitude coordinate direction (the major axis direction). If two or more coor-
dinates have the identical magnitude, the implementation may define the rule to
disambiguate this situation. The rule must be deterministic and depend only on
( rx ry rz ). The target column in table 3.20 explains how the major axis direc-
tion maps to the two-dimensional image of a particular cube map target.
     Using the sc , tc , and ma determined by the major axis direction as specified in
table 3.20, an updated ( s t ) is calculated as follows:

                                     1    sc
                                s=             +1
                                     2   |ma |
                                     1    tc
                                t=             +1
                                     2   |ma |

   This new ( s t ) is used to find a texture value in the determined face’s two-
dimensional texture image using the rules given in sections 3.8.7 and 3.8.8.

3.8.7   Texture Minification
Applying a texture to a primitive implies a mapping from texture image space to
framebuffer image space. In general, this mapping involves a reconstruction of
the sampled texture image, followed by a homogeneous warping implied by the

                           Version 1.3 - August 14, 2001
136                                                        CHAPTER 3. RASTERIZATION


mapping to framebuffer space, then a filtering, followed finally by a resampling
of the filtered, warped, reconstructed image before applying it to a fragment. In
the GL this mapping is approximated by one of two simple filtering schemes. One
of these schemes is selected based on whether the mapping from texture space to
framebuffer space is deemed to magnify or minify the texture image.

Scale Factor and Level of Detail
The choice is governed by a scale factor ρ(x, y) and the level of detail parameter
λ(x, y), defined as

                                  λ (x, y) = log2 [ρ(x, y)]

                        
                        
                         lodmax ,  λ > lodmax
                        
                        λ,
                                   lodmin ≤ λ ≤ lodmax
                   λ=                                                                       (3.14)
                      
                       lod min ,   λ < lodmin
                      
                      
                        undef ined, lodmin > lodmax
     If λ(x, y) is less than or equal to the constant c (described below in sec-
tion 3.8.8) the texture is said to be magnified; if it is greater, the texture is minified.
     The initial values of lodmin and lodmax are chosen so as to never clamp the
normal range of λ. They may be respecified for a specific texture by calling Tex-
Parameter[if] with pname set to TEXTURE MIN LOD or TEXTURE MAX LOD re-
spectively.
     Let s(x, y) be the function that associates an s texture coordinate with each
set of window coordinates (x, y) that lie within a primitive; define t(x, y) and
r(x, y) analogously. Let u(x, y) = 2n s(x, y), v(x, y) = 2m t(x, y), and w(x, y) =
2l r(x, y), where n, m, and l are as defined by equations 3.11, 3.12, and 3.13 with
ws , hs , and ds equal to the width, height, and depth of the image array whose level
is levelbase . For a one-dimensional texture, define v(x, y) ≡ 0 and w(x, y) ≡ 0;
for a two-dimensional texture, define w(x, y) ≡ 0. For a polygon, ρ is given at a
fragment with window coordinates (x, y) by

                                                                                             
                        2             2            2              2            2             2
                 ∂u             ∂v           ∂w             ∂u           ∂v           ∂w
 ρ = max                    +             +            ,              +            +
                 ∂x             ∂x           ∂x             ∂y           ∂y           ∂y     
                                                                           (3.15)
where ∂u/∂x indicates the derivative of u with respect to window x, and similarly
for the other derivatives.
    For a line, the formula is

                                Version 1.3 - August 14, 2001
3.8. TEXTURING                                                                   137




                           2                        2                        2
         ∂u      ∂u                 ∂v      ∂v              ∂w      ∂w
ρ=          ∆x +    ∆y         +       ∆x +    ∆y       +      ∆x +    ∆y         l,
         ∂x      ∂y                 ∂x      ∂y              ∂x      ∂y
                                                                             (3.16)
where ∆x = x2 − x1 and ∆y = y2 − y1 with (x1 , y1 ) and (x2 , y2 ) being the
segment’s window coordinate endpoints and l = ∆x2 + ∆y 2 . For a point, pixel
rectangle, or bitmap, ρ ≡ 1.
    While it is generally agreed that equations 3.15 and 3.16 give the best results
when texturing, they are often impractical to implement. Therefore, an imple-
mentation may approximate the ideal ρ with a function f (x, y) subject to these
conditions:

   1. f (x, y) is continuous and monotonically increasing in each of |∂u/∂x|,
      |∂u/∂y|, |∂v/∂x|, |∂v/∂y|, |∂w/∂x|, and |∂w/∂y|

   2. Let
                                              ∂u ∂u
                                   mu = max     ,
                                              ∂x ∂y

                                              ∂v   ∂v
                                   mv = max      ,
                                              ∂x ∂y

                                              ∂w ∂w
                               mw = max          ,          .
                                              ∂x   ∂y

      Then max{mu , mv , mw } ≤ f (x, y) ≤ mu + mv + mw .

    When λ indicates minification, the value assigned to TEXTURE MIN FILTER is
used to determine how the texture value for a fragment is selected. When TEX-
TURE MIN FILTER is NEAREST, the texel in the image array of level levelbase that
is nearest (in Manhattan distance) to that specified by (s, t, r) is obtained. This
means the texel at location (i, j, k) becomes the texture value, with i given by

                                       u ,    s<1
                               i=                                           (3.17)
                                      2n − 1, s = 1
(Recall that if TEXTURE WRAP S is REPEAT, then 0 ≤ s < 1.) Similarly, j is found
as

                                       v ,   t<1
                               j=      m                                    (3.18)
                                      2 − 1, t = 1

                          Version 1.3 - August 14, 2001
138                                              CHAPTER 3. RASTERIZATION


and k is found as

                                      w ,    r<1
                             k=                                               (3.19)
                                     2l − 1, r = 1
For a one-dimensional texture, j and k are irrelevant; the texel at location i be-
comes the texture value. For a two-dimensional texture, k is irrelevant; the texel at
location (i, j) becomes the texture value.
    When TEXTURE MIN FILTER is LINEAR, a 2 × 2 × 2 cube of texels in the
image array of level levelbase is selected. This cube is obtained by first clamping
texture coordinates as described above under Texture Wrap Modes (if the wrap
mode for a coordinate is CLAMP or CLAMP TO EDGE) and computing

                    u − 1/2 mod 2n , TEXTURE WRAP S is REPEAT
          i0 =
                    u − 1/2 ,        otherwise


                    v − 1/2 mod 2m , TEXTURE WRAP T is REPEAT
          j0 =
                    v − 1/2 ,        otherwise

and

                    w − 1/2 mod 2l , TEXTURE WRAP R is REPEAT
          k0 =
                    w − 1/2 ,        otherwise

Then

                    (i0 + 1) mod 2n , TEXTURE WRAP S is REPEAT
            i1 =
                    i0 + 1,           otherwise


                    (j0 + 1) mod 2m , TEXTURE WRAP T is REPEAT
           j1 =
                    j0 + 1,           otherwise

and

                    (k0 + 1) mod 2l , TEXTURE WRAP R is REPEAT
           k1 =
                    k0 + 1,           otherwise

Let
                                α = frac(u − 1/2)
                                β = frac(v − 1/2)

                          Version 1.3 - August 14, 2001
3.8. TEXTURING                                                                     139


                                 γ = frac(w − 1/2)
where frac(x) denotes the fractional part of x.
   For a three-dimensional texture, the texture value τ is found as


         τ   = (1 − α)(1 − β)(1 − γ)τi0 j0 k0 + α(1 − β)(1 − γ)τi1 j0 k0
                  + (1 − α)β(1 − γ)τi0 j1 k0 + αβ(1 − γ)τi1 j1 k0
                  + (1 − α)(1 − β)γτi0 j0 k1 + α(1 − β)γτi1 j0 k1
                  + (1 − α)βγτi0 j1 k1 + αβγτi1 j1 k1

where τijk is the texel at location (i, j, k) in the three-dimensional texture image.
   For a two-dimensional texture,


   τ = (1 − α)(1 − β)τi0 j0 + α(1 − β)τi1 j0 + (1 − α)βτi0 j1 + αβτi1 j1        (3.20)

where τij is the texel at location (i, j) in the two-dimensional texture image.
   And for a one-dimensional texture,

                               τ = (1 − α)τi0 + ατi1

    where τi is the texel at location i in the one-dimensional texture.
    If any of the selected τijk , τij , or τi in the above equations refer to a border
texel with i < −bs , j < −bs , k < −bs , i ≥ ws − bs , j ≥ hs − bs , or j ≥ ds − bs ,
then the border color given by the current setting of TEXTURE BORDER COLOR is
used instead of the unspecified value or values. The RGBA values of the TEX-
TURE BORDER COLOR are interpreted to match the texture’s internal format in a
manner consistent with table 3.15.

Mipmapping
TEXTURE MIN FILTER                     values                   NEAR-
EST MIPMAP NEAREST, NEAREST MIPMAP LINEAR, LINEAR MIPMAP NEAREST,
and LINEAR MIPMAP LINEAR each require the use of a mipmap. A mipmap is
an ordered set of arrays representing the same image; each array has a resolution
lower than the previous one. If the image array of level levelbase , excluding its bor-
der, has dimensions 2n × 2m × 2l , then there are max{n, m, l} + 1 image arrays in
the mipmap. Each array subsequent to the array of level levelbase has dimensions

                          σ(i − 1) × σ(j − 1) × σ(k − 1)

                           Version 1.3 - August 14, 2001
140                                                CHAPTER 3. RASTERIZATION


where the dimensions of the previous array are

                                  σ(i) × σ(j) × σ(k)
and

                                             2x x > 0
                                 σ(x) =
                                             1 x≤0

until the last array is reached with dimension 1 × 1 × 1.
    Each array in a mipmap is defined using TexImage3D, TexImage2D, Copy-
TexImage2D, TexImage1D, or CopyTexImage1D; the array being set is indicated
with the level-of-detail argument level. Level-of-detail numbers proceed from
levelbase for the original texture array through p = max{n, m, l} + levelbase
with each unit increase indicating an array of half the dimensions of the previous
one as already described. All arrays from levelbase through q = min{p, levelmax }
must be defined, as discussed in section 3.8.9.
    The values of levelbase and levelmax may be respecified for a specific texture
by calling TexParameter[if] with pname set to TEXTURE BASE LEVEL or TEX-
TURE MAX LEVEL respectively.
    The error INVALID VALUE is generated if either value is negative.
    The mipmap is used in conjunction with the level of detail to approximate the
application of an appropriately filtered texture to a fragment. Let c be the value
of λ at which the transition from minification to magnification occurs (since this
discussion pertains to minification, we are concerned only with values of λ where
λ > c).
    For
mipmap filters NEAREST MIPMAP NEAREST and LINEAR MIPMAP NEAREST, the
dth mipmap array is selected, where

           
            levelbase ,
                                          λ ≤ 12
                                  1
      d=       levelbase + λ +    2   − 1, λ > 12 , levelbase + λ ≤ q +   1
                                                                          2   (3.21)
                                           λ > 12 , levelbase + λ > q +   1
           
            q,
                                                                          2

    The rules for NEAREST or LINEAR filtering are then applied to the selected
array.
    For mipmap filters NEAREST MIPMAP LINEAR and LINEAR MIPMAP LINEAR,
the level d1 and d2 mipmap arrays are selected, where

                                      q,       b+λ≥q
                           d1 =                                               (3.22)
                                       b + λ , otherwise

                           Version 1.3 - August 14, 2001
3.8. TEXTURING                                                                  141



                                  q,      b+λ≥q
                          d2 =                                               (3.23)
                                  d1 + 1, otherwise
    The rules for NEAREST or LINEAR filtering are then applied to each of the
selected arrays, yielding two corresponding texture values τ1 and τ2 . The final
texture value is then found as

                        τ = [1 − frac(λ)]τ1 + frac(λ)τ2 .

3.8.8   Texture Magnification
When λ indicates magnification, the value assigned to TEXTURE MAG FILTER de-
termines how the texture value is obtained. There are two possible values for TEX-
TURE MAG FILTER: NEAREST and LINEAR. NEAREST behaves exactly as NEAR-
EST for TEXTURE MIN FILTER (equations 3.17, 3.18, and 3.19 are used); LINEAR
behaves exactly as LINEAR for TEXTURE MIN FILTER (equation 3.20 is used).
The level-of-detail levelbase texture array is always used for magnification.
     Finally, there is the choice of c, the minification vs. magnification switch-
over point. If the magnification filter is given by LINEAR and the minification
filter is given by NEAREST MIPMAP NEAREST or NEAREST MIPMAP LINEAR, then
c = 0.5. This is done to ensure that a minified texture does not appear “sharper”
than a magnified texture. Otherwise c = 0.

3.8.9   Texture Completeness
A texture is said to be complete if all the image arrays and texture parameters
required to utilize the texture for texture application is consistently defined. The
definition of completeness varies depending on the texture dimensionality.
    For one-, two-, or three-dimensional textures, a texture is complete if the fol-
lowing conditions all hold true:

   • The set of mipmap arrays levelbase through q (where q is defined in the
     Mipmapping discussion of section 3.8.7) were each specified with the same
     internal format.

   • The border widths of each array are the same.

   • The dimensions of the arrays follow the sequence described in the Mipmap-
     ping discussion of section 3.8.7.

   • levelbase ≤ levelmax

                          Version 1.3 - August 14, 2001
142                                             CHAPTER 3. RASTERIZATION


   • levelbase ≤ p

Array levels k where k < levelbase or k > q are insignificant to the definition of
completeness.
     For cube map textures, a texture is cube complete if the following conditions
all hold true:

   • The levelbase arrays of each of the six texture images making up the cube
     map have identical, positive, and square dimensions.

   • The levelbase arrays were each specified with the same internal format.

   • The levelbase arrays each have the same border width.

   Finally, a cube map texture is mipmap cube complete if, in addition to being
cube complete, each of the six texture images considered individually is complete.


Effects of Completeness on Texture Application

If one-, two-, or three-dimensional texturing (but not cube map texturing)
is enabled for a texture unit at the time a primitive is rasterized, if TEX-
TURE MIN FILTER is one that requires a mipmap, and if the texture image bound
to the enabled texture target is not complete, then it is as if texture mapping were
disabled for that texture unit.
    If cube map texturing is enabled for a texture unit at the time a primitive is
rasterized, and if the bound cube map texture is not cube complete, then it is
as if texture mapping were disabled for that texture unit. Additionally, if TEX-
TURE MIN FILTER is one that requires a mipmap, and if the texture is not mipmap
cube complete, then it is as if texture mapping were disabled for that texture unit.


Effects of Completeness on Texture Image Specification

An implementation may allow a texture image array of level 1 or greater to be cre-
ated only if a mipmap complete set of image arrays consistent with the requested
array can be supported. A mipmap complete set of arrays is equivalent to a com-
plete set of arrays where levelbase = 0 and levelmax = 1000, and where, excluding
borders, the dimensions of the image array being created are understood to be half
the corresponding dimensions of the next lower numbered array.

                          Version 1.3 - August 14, 2001
3.8. TEXTURING                                                                     143


3.8.10    Texture State and Proxy State

The state necessary for texture can be divided into two categories. First, there are
the nine sets of mipmap arrays (one each for the one-, two-, and three-dimensional
texture targets and six for the cube map texture targets) and their number. Each ar-
ray has associated with it a width, height (two- and three-dimensional and cubemap
only), and depth (three-dimensional only), a border width, an integer describing the
internal format of the image, six integer values describing the resolutions of each
of the red, green, blue, alpha, luminance, and intensity components of the image,
a boolean describing whether the image is compressed or not, and an integer size
of a compressed image. Each initial texture array is null (zero width, height, and
depth, zero border width, internal format 1, with the compressed flag set to FALSE,
a zero compressed size, and zero-sized components). Next, there are the two sets of
texture properties; each consists of the selected minification and magnification fil-
ters, the wrap modes for s, t (two- and three-dimensional and cubemap only), and
r (three-dimensional only), the TEXTURE BORDER COLOR, two integers describing
the minimum and maximum level of detail, two integers describing the base and
maximum mipmap array, a boolean flag indicating whether the texture is resident
and the priority associated with each set of properties. The value of the resident flag
is determined by the GL and may change as a result of other GL operations. The
flag may only be queried, not set, by applications (see section 3.8.11). In the initial
state, the value assigned to TEXTURE MIN FILTER is NEAREST MIPMAP LINEAR,
and the value for TEXTURE MAG FILTER is LINEAR. s, t, and r wrap modes are
all set to REPEAT. The values of TEXTURE MIN LOD and TEXTURE MAX LOD are
-1000 and 1000 respectively. The values of TEXTURE BASE LEVEL and TEX-
TURE MAX LEVEL are 0 and 1000 respectively. TEXTURE PRIORITY is 1.0, and
TEXTURE BORDER COLOR is (0,0,0,0). The initial value of TEXTURE RESIDENT is
determined by the GL.
     In addition to the one-, two-, and three-dimensional and the six cube map sets
of image arrays, the partially instantiated one-, two-, and three-dimensional and
one cube map set of proxy image arrays are maintained. Each proxy array includes
width, height (two- and three-dimensional arrays only), depth (three-dimensional
arrays only), border width, and internal format state values, as well as state for
the red, green, blue, alpha, luminance, and intensity component resolutions. Proxy
arrays do not include image data, nor do they include texture properties. When
TexImage3D is executed with target specified as PROXY TEXTURE 3D, the three-
dimensional proxy state values of the specified level-of-detail are recomputed and
updated. If the image array would not be supported by TexImage3D called with
target set to TEXTURE 3D, no error is generated, but the proxy width, height, depth,
border width, and component resolutions are set to zero. If the image array would

                           Version 1.3 - August 14, 2001
144                                              CHAPTER 3. RASTERIZATION


be supported by such a call to TexImage3D, the proxy state values are set exactly
as though the actual image array were being specified. No pixel data are transferred
or processed in either case.
    One- and two-dimensional proxy arrays are operated on in the same way when
TexImage1D is executed with target specified as PROXY TEXTURE 1D, or TexIm-
age2D is executed with target specified as PROXY TEXTURE 2D.
    The cube map proxy arrays are operated on in the same manner when TexIm-
age2D is executed with the target field specified as PROXY TEXTURE CUBE MAP,
with the addition that determining that a given cube map texture is supported with
PROXY TEXTURE CUBE MAP indicates that all six of the cube map 2D images are
supported. Likewise, if the specified PROXY TEXTURE CUBE MAP is not supported,
none of the six cube map 2D images are supported.
    There is no image associated with any of the proxy textures. There-
fore PROXY TEXTURE 1D, PROXY TEXTURE 2D, and PROXY TEXTURE 3D, and
PROXY TEXTURE CUBE MAP cannot be used as textures, and their images must
never be queried using GetTexImage. The error INVALID ENUM is generated if
this is attempted. Likewise, there is no non level-related state associated with a
proxy texture, and GetTexParameteriv or GetTexParameterfv may not be called
with a proxy texture target. The error INVALID ENUM is generated if this is at-
tempted.

3.8.11    Texture Objects
In addition to the default textures TEXTURE 1D, TEXTURE 2D, TEXTURE 3D, and
TEXTURE CUBE MAP, named one-, two-, and three-dimensional and cube map tex-
ture objects can be created and operated upon. The name space for texture objects
is the unsigned integers, with zero reserved by the GL.
     A texture object is created by binding an unused name to TEXTURE 1D, TEX-
TURE 2D, TEXTURE 3D, or TEXTURE CUBE MAP. The binding is effected by calling

      void BindTexture( enum target, uint texture );

with target set to the desired texture target and texture set to the unused name.
The resulting texture object is a new state vector, comprising all the state values
listed in section 3.8.10, set to the same initial values. If the new texture object is
bound to TEXTURE 1D, TEXTURE 2D, TEXTURE 3D, or TEXTURE CUBE MAP, it is
and remains a one-, two-, three-dimensional, or cube map texture respectively until
it is deleted.
     BindTexture may also be used to bind an existing texture object to either
TEXTURE 1D, TEXTURE 2D, TEXTURE 3D, or TEXTURE CUBE MAP. The error IN-
VALID OPERATION is generated if an attempt is made to bind a texture object

                           Version 1.3 - August 14, 2001
3.8. TEXTURING                                                                   145


of different dimensionality than the specified target. If the bind is successful no
change is made to the state of the bound texture object, and any previous binding
to target is broken.
     While a texture object is bound, GL operations on the target to which it is
bound affect the bound object, and queries of the target to which it is bound return
state from the bound object. If texture mapping of the dimensionality of the target
to which a texture object is bound is enabled, the state of the bound texture object
directs the texturing operation.
     In the initial state, TEXTURE 1D, TEXTURE 2D, TEXTURE 3D, and TEX-
TURE CUBE MAP have one-, two-, three-dimensional, and cube map texture state
vectors respectively associated with them. In order that access to these initial tex-
tures not be lost, they are treated as texture objects all of whose names are 0. The
initial one-, two-, three-dimensional, and cube map texture is therefore operated
upon, queried, and applied as TEXTURE 1D, TEXTURE 2D, TEXTURE 3D, or TEX-
TURE CUBE MAP respectively while 0 is bound to the corresponding targets.
     Texture objects are deleted by calling

      void DeleteTextures( sizei n, uint *textures );

textures contains n names of texture objects to be deleted. After a texture object
is deleted, it has no contents or dimensionality, and its name is again unused. If
a texture that is currently bound to one of the targets TEXTURE 1D, TEXTURE 2D,
TEXTURE 3D, or TEXTURE CUBE MAP is deleted, it is as though BindTexture had
been executed with the same target and texture zero. Unused names in textures are
silently ignored, as is the value zero.
    The command

      void GenTextures( sizei n, uint *textures );

returns n previously unused texture object names in textures. These names are
marked as used, for the purposes of GenTextures only, but they acquire texture
state and a dimensionality only when they are first bound, just as if they were
unused.
    An implementation may choose to establish a working set of texture objects on
which binding operations are performed with higher performance. A texture object
that is currently part of the working set is said to be resident. The command

      boolean AreTexturesResident( sizei n, uint *textures,
         boolean *residences );

                          Version 1.3 - August 14, 2001
146                                                       CHAPTER 3. RASTERIZATION


returns TRUE if all of the n texture objects named in textures are resident, or if the
implementation does not distinguish a working set. If at least one of the texture
objects named in textures is not resident, then FALSE is returned, and the residence
of each texture object is returned in residences. Otherwise the contents of resi-
dences are not changed. If any of the names in textures are unused or are zero,
FALSE is returned, the error INVALID VALUE is generated, and the contents of res-
idences are indeterminate. The residence status of a single bound texture object
can also be queried by calling GetTexParameteriv or GetTexParameterfv with
target set to the target to which the texture object is bound, and pname set to
TEXTURE RESIDENT.
    AreTexturesResident indicates only whether a texture object is currently resi-
dent, not whether it could not be made resident. An implementation may choose to
make a texture object resident only on first use, for example. The client may guide
the GL implementation in determining which texture objects should be resident by
specifying a priority for each texture object. The command

      void PrioritizeTextures( sizei n, uint *textures,
         clampf *priorities );

sets the priorities of the n texture objects named in textures to the values in priori-
ties. Each priority value is clamped to the range [0,1] before it is assigned. Zero in-
dicates the lowest priority, with the least likelihood of being resident. One indicates
the highest priority, with the greatest likelihood of being resident. The priority of a
single bound texture object may also be changed by calling TexParameteri, Tex-
Parameterf, TexParameteriv, or TexParameterfv with target set to the target to
which the texture object is bound, pname set to TEXTURE PRIORITY, and param
or params specifying the new priority value (which is clamped to the range [0,1]
before being assigned). PrioritizeTextures silently ignores attempts to prioritize
unused texture object names or zero (default textures).
     The texture object name space, including the initial one-, two-, and three-
dimensional texture objects, is shared among all texture units. A texture object
may be bound to more than one texture unit simultaneously. After a texture object
is bound, any GL operations on that target object affect any other texture units to
which the same texture object is bound.
     Texture binding is affected by the setting of the state ACTIVE TEXTURE.
     If a texture object is deleted, it as if all texture units which are bound to that
texture object are rebound to texture object zero.

3.8.12    Texture Environments and Texture Functions
The command

                               Version 1.3 - August 14, 2001
3.8. TEXTURING                                                                                     147


       void TexEnv{if}( enum target, enum pname, T param );
       void TexEnv{if}v( enum target, enum pname, T params );

sets parameters of the texture environment that specifies how texture values are
interpreted when texturing a fragment. target must currently be the symbolic con-
stant TEXTURE ENV. pname is a symbolic constant indicating the parameter to be
set. In the first form of the command, param is a value to which to set a single-
valued parameter; in the second form, params is a pointer to an array of parameters:
either a single symbolic constant or a value or group of values to which the param-
eter should be set. The possible environment parameters are TEXTURE ENV MODE,
TEXTURE ENV COLOR, COMBINE RGB, and COMBINE ALPHA. TEXTURE ENV MODE
may be set to one of REPLACE, MODULATE, DECAL, BLEND, ADD, or COMBINE.
TEXTURE ENV COLOR is set to an RGBA color by providing four single-precision
floating-point values in the range [0, 1] (values outside this range are clamped to
it). If integers are provided for TEXTURE ENV COLOR, then they are converted to
floating-point as specified in table 2.6 for signed integers.
     The value of TEXTURE ENV MODE specifies a texture function. The result of
this function depends on the fragment and the texture array value. The precise
form of the function depends on the base internal formats of the texture arrays that
were last specified.
     Cf and Af 3 are the primary color components of the incoming fragment; Cs
and As are the components of the texture source color, derived from the filtered
texture values Rt , Gt , Bt , At , Lt , and It as shown in table 3.21; Cc and Ac are
the components of the texture environment color; Cp and Ap are the components
resulting from the previous texture environment (for texture environment 0, Cp and
Ap are identical to Cf and Af , respectively); and Cv and Av are the primary color
components computed by the texture function.
     All of these color values are in the range [0, 1]. The texture functions are spec-
ified in tables 3.22, 3.23, and 3.24.
     If the value of TEXTURE ENV MODE is COMBINE, the form of the texture func-
tion depends on the values of COMBINE RGB and COMBINE ALPHA, according to
table 3.24. The RGB and ALPHA results of the texture function are then multi-
plied by the values of RGB SCALE and ALPHA SCALE, respectively. The results are
clamped to [0, 1].
     The arguments Arg0, Arg1, and Arg2 are determined by the values of
SOURCEn RGB, SOURCEn ALPHA, OPERANDn RGB and OPERANDn ALPHA, where
    3
      In the remainder of section 3.8.12, the notation Cx is used to denote each of the three components
Rx , Gx , and Bx of a color specified by x. Operations on Cx are performed independently for each
color component. The A component of colors is usually operated on in a different fashion, and is
therefore denoted separately by Ax .


                                Version 1.3 - August 14, 2001
148                                           CHAPTER 3. RASTERIZATION




                    Texture Base         Texture source color
                    Internal Format            Cs         As
                    ALPHA                  (0, 0, 0)      At
                    LUMINANCE            (Lt , Lt , Lt )  1
                    LUMINANCE ALPHA      (Lt , Lt , Lt )  At
                    INTENSITY             (It , It , It ) It
                    RGB                  (Rt , Gt , Bt )  1
                    RGBA                 (Rt , Gt , Bt )  At

Table 3.21: Correspondence of filtered texture components to texture source com-
ponents.




  Texture Base           REPLACE      MODULATE     DECAL
  Internal Format        Function     Function     Function
  ALPHA                  Cv = Cf      Cv = Cf      undefined
                         Av = As      Av = Af As
  LUMINANCE              Cv = Cs      Cv = Cf Cs   undefined
  (or 1)                 Av = Af      Av = Af
  LUMINANCE ALPHA        Cv = Cs      Cv = Cf Cs   undefined
  (or 2)                 Av = As      Av = Af As
  INTENSITY              Cv = Cs      Cv = Cf Cs   undefined
                         Av = As      Av = Af As
  RGB                    Cv = Cs      Cv = Cf Cs   Cv     = Cs
  (or 3)                 Av = Af      Av = Af      Av     = Af
  RGBA                   Cv = Cs      Cv = Cf Cs   Cv     = Cf (1 − As ) + Cs As
  (or 4)                 Av = As      Av = Af As   Av     = Af

           Table 3.22: Texture functions REPLACE, MODULATE, and DECAL.




                          Version 1.3 - August 14, 2001
3.8. TEXTURING                                                                   149


       Texture Base           BLEND                          ADD
       Internal Format        Function                       Function
       ALPHA                  Cv = Cf                        Cv = Cf
                              Av = Af As                     Av = Af As
       LUMINANCE              Cv = Cf (1 − Cs ) + Cc Cs      Cv = Cf + Cs
       (or 1)                 Av = Af                        Av = Af
       LUMINANCE ALPHA        Cv = Cf (1 − Cs ) + Cc Cs      Cv = Cf + Cs
       (or 2)                 Av = Af As                     Av = Af As
       INTENSITY              Cv = Cf (1 − Cs ) + Cc Cs      Cv = Cf + Cs
                              Av = Af (1 − As ) + Ac As      Av = Af + As
       RGB                    Cv = Cf (1 − Cs ) + Cc Cs      Cv = Cf + Cs
       (or 3)                 Av = Af                        Av = Af
       RGBA                   Cv = Cf (1 − Cs ) + Cc Cs      Cv = Cf + Cs
       (or 4)                 Av = Af As                     Av = Af As

                  Table 3.23: Texture functions BLEND and ADD.


n = 0, 1, or 2, as shown in tables 3.25 and 3.26.
    The state required for the current texture environment, for each texture unit,
consists of a six-valued integer indicating the texture function, an eight-valued in-
teger indicating the RGB combiner function and a six-valued integer indicating the
ALPHA combiner function, six four-valued integers indicating the combiner RGB
and ALPHA source arguments, three four-valued integers indicating the combiner
RGB operands, three two-valued integers indicating the combiner ALPHA operands,
and four floating-point environment color values. In the initial state, the texture
and combiner functions are each MODULATE, the combiner RGB and ALPHA sources
are each TEXTURE, PREVIOUS, and CONSTANT for sources 0, 1, and 2 respectively,
the combiner RGB operands for sources 0 and 1 are each SRC COLOR, the combiner
RGB operand for source 2, as well as for the combiner ALPHA operands, are each
SRC ALPHA, and the environment color is (0, 0, 0, 0),


3.8.13 Texture Application
Texturing is enabled or disabled using the generic Enable and Disable com-
mands, respectively, with the symbolic constants TEXTURE 1D, TEXTURE 2D,
TEXTURE 3D, or TEXTURE CUBE MAP to enable the one-, two-, three-dimensional,
or cube map texture, respectively. If both two- and one-dimensional textures are
enabled, the two-dimensional texture is used. If the three-dimensional and either
of the two- or one-dimensional textures is enabled, the three-dimensional texture

                          Version 1.3 - August 14, 2001
150                                          CHAPTER 3. RASTERIZATION




            COMBINE RGB      Texture Function
            REPLACE          Arg0
            MODULATE         Arg0 ∗ Arg1
            ADD              Arg0 + Arg1
            ADD SIGNED       Arg0 + Arg1 − 0.5
            INTERPOLATE      Arg0 ∗ Arg2 + Arg1 ∗ (1 − Arg2)
            SUBTRACT         Arg0 − Arg1
            DOT3 RGB         4 × ((Arg0r − 0.5) ∗ (Arg1r − 0.5)+
                                  (Arg0g − 0.5) ∗ (Arg1g − 0.5)+
                                   (Arg0b − 0.5) ∗ (Arg1b − 0.5))
            DOT3 RGBA        4 × ((Arg0r − 0.5) ∗ (Arg1r − 0.5)+
                                  (Arg0g − 0.5) ∗ (Arg1g − 0.5)+
                                   (Arg0b − 0.5) ∗ (Arg1b − 0.5))


            COMBINE ALPHA      Texture Function
            REPLACE            Arg0
            MODULATE           Arg0 ∗ Arg1
            ADD                Arg0 + Arg1
            ADD SIGNED         Arg0 + Arg1 − 0.5
            INTERPOLATE        Arg0 ∗ Arg2 + Arg1 ∗ (1 − Arg2)
            SUBTRACT           Arg0 − Arg1

Table 3.24: COMBINE texture functions. The scalar expression computed for the
DOT3 RGB and DOT3 RGBA functions is placed into each of the 3 (RGB) or 4 (RGBA)
components of the output. The result generated from COMBINE ALPHA is ignored
for DOT3 RGBA.




                         Version 1.3 - August 14, 2001
3.8. TEXTURING                                                 151




        SOURCEn RGB       OPERANDn RGB              Argument
        TEXTURE           SRC   COLOR               Cs
                          ONE   MINUS   SRC COLOR   1 − Cs
                          SRC   ALPHA               As
                          ONE   MINUS   SRC ALPHA   1 − As
        CONSTANT          SRC   COLOR               Cc
                          ONE   MINUS   SRC COLOR   1 − Cc
                          SRC   ALPHA               Ac
                          ONE   MINUS   SRC ALPHA   1 − Ac
        PRIMARY COLOR     SRC   COLOR               Cf
                          ONE   MINUS   SRC COLOR   1 − Cf
                          SRC   ALPHA               Af
                          ONE   MINUS   SRC ALPHA   1 − Af
        PREVIOUS          SRC   COLOR               Cp
                          ONE   MINUS   SRC COLOR   1 − Cp
                          SRC   ALPHA               Ap
                          ONE   MINUS   SRC ALPHA   1 − Ap

          Table 3.25: Arguments for COMBINE RGB functions.




        SOURCEn ALPHA     OPERANDn ALPHA            Argument
        TEXTURE           SRC   ALPHA               As
                          ONE   MINUS   SRC ALPHA   1 − As
        CONSTANT          SRC   ALPHA               Ac
                          ONE   MINUS   SRC ALPHA   1 − Ac
        PRIMARY COLOR     SRC   ALPHA               Af
                          ONE   MINUS   SRC ALPHA   1 − Af
        PREVIOUS          SRC   ALPHA               Ap
                          ONE   MINUS   SRC ALPHA   1 − Ap

         Table 3.26: Arguments for COMBINE ALPHA functions.




                    Version 1.3 - August 14, 2001
152                                                CHAPTER 3. RASTERIZATION


is used. If the cube map texture and any of the three-, two-, or one-dimensional
textures is enabled, then cube map texturing is used. If all texturing is disabled, a
rasterized fragment is passed on unaltered to the next stage of the GL (although its
texture coordinates may be discarded). Otherwise, a texture value is found accord-
ing to the parameter values of the currently bound texture image of the appropriate
dimensionality using the rules given in sections 3.8.6, 3.8.7, and 3.8.8. This texture
value is used along with the incoming fragment in computing the texture function
indicated by the currently bound texture environment. The result of this function
replaces the incoming fragment’s primary R, G, B, and A values. These are the
color values passed to subsequent operations. Other data associated with the in-
coming fragment remain unchanged, except that the texture coordinates may be
discarded.
     Each texture unit is enabled and bound to texture objects independently from
the other texture units. Each texture unit follows the precedence rules for one-, two-
, three-dimensional, and cube map textures. Thus texture units can be performing
texture mapping of different dimensionalities simultaneously. Each unit has its
own enable and binding states.
     Each texture unit is paired with an environment function, as shown in fig-
ure 3.11. The second texture function is computed using the texture value from
the second texture, the fragment resulting from the first texture function computa-
tion and the second texture unit’s environment function. If there is a third texture,
the fragment resulting from the second texture function is combined with the third
texture value using the third texture unit’s environment function and so on. The tex-
ture unit selected by ActiveTexture determines which texture unit’s environment
is modified by TexEnv calls.
     If the value of TEXTURE ENV MODE is COMBINE, the texture function associated
with a given texture unit is computed using the values specified by SOURCEn RGB,
SOURCEn ALPHA, OPERANDn RGB and OPERANDn ALPHA. If TEXTUREn is spec-
ified as SOURCEn RGB or SOURCEn ALPHA, the texture value from texture unit n
will be used in computing the texture function for this texture unit.
     Texturing is enabled and disabled individually for each texture unit. If texturing
is disabled for one of the units, then the fragment resulting from the previous unit
is passed unaltered to the following unit.
     If the texture environment for a given texture unit references a texture unit that
is disabled or does not have a valid texture object bound to it, or if the texture object
bound to a texture unit is not complete, as defined in section 3.8.9, then it is as if
texturing is disabled for that texture unit. Every texture unit implicitly references
the texture object that is bound to it, regardless of the texture function specified by
COMBINE RGB or COMBINE ALPHA.
     The required state, per texture unit, is four bits indicating whether each of one-,

                            Version 1.3 - August 14, 2001
3.8. TEXTURING                                                                          153




    Cf




                 TE0
  CT0                            TE1
  CT1                                             TE2
  CT2                                                              TE3            C’f
  CT3

            Cf   = fragment primary color input to texturing

            C’f = fragment color output from texturing

            CTi = texture color from texture lookup i

            TEi = texture environment i




  Figure 3.11. Multitexture pipeline. Four texture units are shown; however, multi-
  texturing may support a different number of units depending on the implementation.
  The input fragment color is successively combined with each texture according to
  the state of the corresponding texture environment, and the resulting fragment color
  passed as input to the next texture unit in the pipeline.




                           Version 1.3 - August 14, 2001
154                                               CHAPTER 3. RASTERIZATION


two-, three-dimensional, or cube map texturing is enabled or disabled. In the intial
state, all texturing is disabled for all texture units.


3.9    Color Sum
At the beginning of color sum, a fragment has two RGBA colors: a primary color
cpri (which texturing, if enabled, may have modified) and a secondary color csec .
The components of these two colors are summed to produce a single post-texturing
RGBA color c. The components of c are then clamped to the range [0, 1].
    Color sum has no effect in color index mode.


3.10     Fog
If enabled, fog blends a fog color with a rasterized fragment’s post-texturing color
using a blending factor f . Fog is enabled and disabled with the Enable and Disable
commands using the symbolic constant FOG.
    This factor f is computed according to one of three equations:

                                 f = exp(−d · z),                               (3.24)

                               f = exp(−(d · z)2 ), or                          (3.25)
                                           e−z
                                     f=                                         (3.26)
                                           e−s
(z is the eye-coordinate distance from the eye, (0, 0, 0, 1) in eye coordinates, to the
fragment center). The equation, along with either d or e and s, is specified with

       void Fog{if}( enum pname, T param );
       void Fog{if}v( enum pname, T params );

If pname is FOG MODE, then param must be, or params must point to an inte-
ger that is one of the symbolic constants EXP, EXP2, or LINEAR, in which case
equation 3.24, 3.25, or 3.26, respectively, is selected for the fog calculation (if,
when 3.26 is selected, e = s, results are undefined). If pname is FOG DENSITY,
FOG START, or FOG END, then param is or params points to a value that is d, s, or
e, respectively. If d is specified less than zero, the error INVALID VALUE results.
     An implementation may choose to approximate the eye-coordinate distance
from the eye to each fragment center by |ze |. Further, f need not be computed at
each fragment, but may be computed at each vertex and interpolated as other data
are.

                           Version 1.3 - August 14, 2001
3.11. ANTIALIASING APPLICATION                                                     155


     No matter which equation and approximation is used to compute f , the result
is clamped to [0, 1] to obtain the final f .
     f is used differently depending on whether the GL is in RGBA or color index
mode. In RGBA mode, if Cr represents a rasterized fragment’s R, G, or B value,
then the corresponding value produced by fog is

                               C = f Cr + (1 − f )Cf .

(The rasterized fragment’s A value is not changed by fog blending.) The R, G, B,
and A values of Cf are specified by calling Fog with pname equal to FOG COLOR;
in this case params points to four values comprising Cf . If these are not floating-
point values, then they are converted to floating-point using the conversion given
in table 2.6 for signed integers. Each component of Cf is clamped to [0, 1] when
specified.
    In color index mode, the formula for fog blending is

                                 I = ir + (1 − f )if

where ir is the rasterized fragment’s color index and if is a single-precision
floating-point value. (1 − f )if is rounded to the nearest fixed-point value with
the same number of bits to the right of the binary point as ir , and the integer por-
tion of I is masked (bitwise ANDed) with 2n − 1, where n is the number of bits in
a color in the color index buffer (buffers are discussed in chapter 4). The value of
if is set by calling Fog with pname set to FOG INDEX and param being or params
pointing to a single value for the fog index. The integer part of if is masked with
2n − 1.
    The state required for fog consists of a three valued integer to select the fog
equation, three floating-point values d, e, and s, an RGBA fog color and a fog color
index, and a single bit to indicate whether or not fog is enabled. In the initial state,
fog is disabled, FOG MODE is EXP, d = 1.0, e = 1.0, and s = 0.0; Cf = (0, 0, 0, 0)
and if = 0.


3.11     Antialiasing Application
Finally, if antialiasing is enabled for the primitive from which a rasterized fragment
was produced, then the computed coverage value is applied to the fragment. In
RGBA mode, the value is multiplied by the fragment’s alpha (A) value to yield a
final alpha value. In color index mode, the value is used to set the low order bits of
the color index value as described in section 3.2.



                           Version 1.3 - August 14, 2001
Chapter 4

Per-Fragment Operations and the
Framebuffer

The framebuffer consists of a set of pixels arranged as a two-dimensional array.
The height and width of this array may vary from one GL implementation to an-
other. For purposes of this discussion, each pixel in the framebuffer is simply a set
of some number of bits. The number of bits per pixel may also vary depending on
the particular GL implementation or context.
     Corresponding bits from each pixel in the framebuffer are grouped together
into a bitplane; each bitplane contains a single bit from each pixel. These bitplanes
are grouped into several logical buffers. These are the color, depth, stencil, and
accumulation buffers. The color buffer actually consists of a number of buffers:
the front left buffer, the front right buffer, the back left buffer, the back right buffer,
and some number of auxiliary buffers. Typically the contents of the front buffers
are displayed on a color monitor while the contents of the back buffers are invisi-
ble. (Monoscopic contexts display only the front left buffer; stereoscopic contexts
display both the front left and the front right buffers.) The contents of the aux-
iliary buffers are never visible. All color buffers must have the same number of
bitplanes, although an implementation or context may choose not to provide right
buffers, back buffers, or auxiliary buffers at all. Further, an implementation or
context may not provide depth, stencil, or accumulation buffers.
     Color buffers consist of either unsigned integer color indices or R, G, B, and,
optionally, A unsigned integer values. The number of bitplanes in each of the color
buffers, the depth buffer, the stencil buffer, and the accumulation buffer is fixed and
window dependent. If an accumulation buffer is provided, it must have at least as
many bitplanes per R, G, and B color component as do the color buffers.
     The initial state of all provided bitplanes is undefined.

                                           156
4.1. PER-FRAGMENT OPERATIONS                                                                            157




     Fragment               Pixel                                             Alpha
         +                                          Scissor
                          Ownership                                           Test
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




4.1     Per-Fragment Operations

A fragment produced by rasterization with window coordinates of (xw , yw ) mod-
ifies the pixel in the framebuffer at that location based on a number of parame-
ters and conditions. We describe these modifications and tests, diagrammed in
Figure 4.1, in the order in which they are performed. Figure 4.1 diagrams these
modifications and tests.



4.1.1   Pixel Ownership Test

The first test is to determine if the pixel at location (xw , yw ) in the framebuffer
is currently owned by the GL (more precisely, by this GL context). If it is not,
the window system decides the fate the incoming fragment. Possible results are
that the fragment is discarded or that some subset of the subsequent per-fragment
operations are applied to the fragment. This test allows the window system to
control the GL’s behavior, for instance, when a GL window is obscured.

                                        Version 1.3 - August 14, 2001
158              CHAPTER 4. PER-FRAGMENT OPERATIONS AND THE . . .


4.1.2    Scissor test
The scissor test determines if (xw , yw ) lies within the scissor rectangle defined by
four values. These values are set with

        void Scissor( int left, int bottom, sizei width,
           sizei height );

If left ≤ xw < left + width and bottom ≤ yw < bottom + height, then the scissor
test passes. Otherwise, the test fails and the fragment is discarded. The test is
enabled or disabled using Enable or Disable using the constant SCISSOR TEST.
When disabled, it is as if the scissor test always passes. If either width or height
is less than zero, then the error INVALID VALUE is generated. The state required
consists of four integer values and a bit indicating whether the test is enabled or
disabled. In the initial state lef t = bottom = 0; width and height are determined
by the size of the GL window. Initially, the scissor test is disabled.

4.1.3    Multisample Fragment Operations
This step modifies fragment alpha and coverage values based on the values of SAM-
PLE ALPHA TO COVERAGE, SAMPLE ALPHA TO ONE, SAMPLE COVERAGE, SAM-
PLE COVERAGE VALUE, and SAMPLE COVERAGE INVERT. No changes to the frag-
ment alpha or coverage values are made at this step if MULTISAMPLE is disabled,
or if SAMPLE BUFFERS is not a value of one.
     SAMPLE ALPHA TO COVERAGE,                                                  SAM-
PLE ALPHA TO ONE, and SAMPLE COVERAGE are enabled and disabled by calling
Enable and Disable with cap specified as one of the three token values. All three
values are queried by calling IsEnabled with cap set to the desired token value.
If SAMPLE ALPHA TO COVERAGE is enabled, a temporary coverage value is gener-
ated where each bit is determined by the alpha value at the corresponding sample
location. The temporary coverage value is then ANDed with the fragment coverage
value. Otherwise the fragment coverage value is unchanged at this point.
     No specific algorithm is required for converting the sample alpha values to a
temporary coverage value. It is intended that the number of 1’s in the temporary
coverage be proportional to the set of alpha values for the fragment, with all 1’s
corresponding to the maximum of all alpha values, and all 0’s corresponding to
all alpha values being 0. It is also intended that the algorithm be pseudo-random
in nature, to avoid image artifacts due to regular coverage sample locations. The
algorithm can and probably should be different at different pixel locations. If it
does differ, it should be defined relative to window, not screen, coordinates, so that
rendering results are invariant with respect to window position.

                           Version 1.3 - August 14, 2001
4.1. PER-FRAGMENT OPERATIONS                                                       159


    Next, if SAMPLE ALPHA TO ONE is enabled, each alpha value is replaced by the
maximum representable alpha value. Otherwise, the alpha values are not changed.
    Finally, if SAMPLE COVERAGE is enabled, the fragment coverage is ANDed
with another temporary coverage. This temporary coverage is generated in the
same manner as the one described above, but as a function of the value of SAM-
PLE COVERAGE VALUE. The function need not be identical, but it must have the
same properties of proportionality and invariance. If SAMPLE COVERAGE INVERT
is TRUE, the temporary coverage is inverted (all bit values are inverted) before it is
ANDed with the fragment coverage.
    The values of SAMPLE COVERAGE VALUE and SAMPLE COVERAGE INVERT
are specified by calling

        void SampleCoverage( clampf value, boolean invert );

with value set to the desired coverage value, and invert set to TRUE or FALSE.
value is clamped to [0,1] before being stored as SAMPLE COVERAGE VALUE. SAM-
PLE COVERAGE VALUE is queried by calling GetFloatv with pname set to SAM-
PLE COVERAGE VALUE. SAMPLE COVERAGE INVERT is queried by calling Get-
Booleanv with pname set to SAMPLE COVERAGE INVERT.

4.1.4    Alpha test
This step applies only in RGBA mode. In color index mode, proceed to the next
step. The alpha test discards a fragment conditional on the outcome of a com-
parison between the incoming fragment’s alpha value and a constant value. The
comparison is enabled or disabled with the generic Enable and Disable commands
using the symbolic constant ALPHA TEST. When disabled, it is as if the comparison
always passes. The test is controlled with

        void AlphaFunc( enum func, clampf ref );

func is a symbolic constant indicating the alpha test function; ref is a reference
value. ref is clamped to lie in [0, 1], and then converted to a fixed-point value ac-
cording to the rules given for an A component in section 2.13.9. For purposes
of the alpha test, the fragment’s alpha value is also rounded to the nearest inte-
ger. The possible constants specifying the test function are NEVER, ALWAYS, LESS,
LEQUAL, EQUAL, GEQUAL, GREATER, or NOTEQUAL, meaning pass the fragment
never, always, if the fragment’s alpha value is less than, less than or equal to, equal
to, greater than or equal to, greater than, or not equal to the reference value, respec-
tively.

                           Version 1.3 - August 14, 2001
160               CHAPTER 4. PER-FRAGMENT OPERATIONS AND THE . . .


    The required state consists of the floating-point reference value, an eight-
valued integer indicating the comparison function, and a bit indicating if the com-
parison is enabled or disabled. The initial state is for the reference value to be 0
and the function to be ALWAYS. Initially, the alpha test is disabled.

4.1.5    Stencil test
The stencil test conditionally discards a fragment based on the outcome of a com-
parison between the value in the stencil buffer at location (xw , yw ) and a reference
value. The test is controlled with

        void StencilFunc( enum func, int ref, uint mask );
        void StencilOp( enum sfail, enum dpfail, enum dppass );

The test is enabled or disabled with the Enable and Disable commands, using the
symbolic constant STENCIL TEST. When disabled, the stencil test and associated
modifications are not made, and the fragment is always passed.
     ref is an integer reference value that is used in the unsigned stencil comparison.
It is clamped to the range [0, 2s − 1], where s is the number of bits in the stencil
buffer. func is a symbolic constant that determines the stencil comparison function;
the eight symbolic constants are NEVER, ALWAYS, LESS, LEQUAL, EQUAL, GEQUAL,
GREATER, or NOTEQUAL. Accordingly, the stencil test passes never, always, if the
reference value is less than, less than or equal to, equal to, greater than or equal to,
greater than, or not equal to the masked stored value in the stencil buffer. The s least
significant bits of mask are bitwise ANDed with both the reference and the stored
stencil value. The ANDed values are those that participate in the comparison.
     StencilOp takes three arguments that indicate what happens to the stored sten-
cil value if this or certain subsequent tests fail or pass. sfail indicates what action
is taken if the stencil test fails. The symbolic constants are KEEP, ZERO, REPLACE,
INCR, DECR, and INVERT. These correspond to keeping the current value, setting
it to zero, replacing it with the reference value, incrementing it, decrementing it,
or bitwise inverting it. For purposes of increment and decrement, the stencil bits
are considered as an unsigned integer; values clamp at 0 and the maximum repre-
sentable value. The same symbolic values are given to indicate the stencil action if
the depth buffer test (below) fails (dpfail), or if it passes (dppass).
     If the stencil test fails, the incoming fragment is discarded. The state required
consists of the most recent values passed to StencilFunc and StencilOp, and a
bit indicating whether stencil testing is enabled or disabled. In the initial state,
stenciling is disabled, the stencil reference value is zero, the stencil comparison
function is ALWAYS, and the stencil mask is all ones. Initially, all three stencil

                           Version 1.3 - August 14, 2001
4.1. PER-FRAGMENT OPERATIONS                                                      161


operations are KEEP. If there is no stencil buffer, no stencil modification can occur,
and it is as if the stencil tests always pass, regardless of any calls to StencilOp.

4.1.6    Depth buffer test
The depth buffer test discards the incoming fragment if a depth comparison fails.
The comparison is enabled or disabled with the generic Enable and Disable com-
mands using the symbolic constant DEPTH TEST. When disabled, the depth com-
parison and subsequent possible updates to the depth buffer value are bypassed and
the fragment is passed to the next operation. The stencil value, however, is modi-
fied as indicated below as if the depth buffer test passed. If enabled, the comparison
takes place and the depth buffer and stencil value may subsequently be modified.
    The comparison is specified with

        void DepthFunc( enum func );

This command takes a single symbolic constant: one of NEVER, ALWAYS, LESS,
LEQUAL, EQUAL, GREATER, GEQUAL, NOTEQUAL. Accordingly, the depth buffer
test passes never, always, if the incoming fragment’s zw value is less than, less
than or equal to, equal to, greater than, greater than or equal to, or not equal to
the depth value stored at the location given by the incoming fragment’s (xw , yw )
coordinates.
    If the depth buffer test fails, the incoming fragment is discarded. The stencil
value at the fragment’s (xw , yw ) coordinates is updated according to the function
currently in effect for depth buffer test failure. Otherwise, the fragment continues
to the next operation and the value of the depth buffer at the fragment’s (xw , yw )
location is set to the fragment’s zw value. In this case the stencil value is updated
according to the function currently in effect for depth buffer test success.
    The necessary state is an eight-valued integer and a single bit indicating
whether depth buffering is enabled or disabled. In the initial state the function
is LESS and the test is disabled.
    If there is no depth buffer, it is as if the depth buffer test always passes.

4.1.7    Blending
Blending combines the incoming fragment’s R, G, B, and A values with the R,
G, B, and A values stored in the framebuffer at the incoming fragment’s (xw , yw )
location.
    This blending is dependent on the incoming fragment’s alpha value and that of
the corresponding currently stored pixel. Blending applies only in RGBA mode; in
color index mode it is bypassed. Blending is enabled or disabled using Enable or

                           Version 1.3 - August 14, 2001
162              CHAPTER 4. PER-FRAGMENT OPERATIONS AND THE . . .


Disable with the symbolic constant BLEND. If it is disabled, or if logical operation
on color values is enabled (section 4.1.9), proceed to the next stage.
    In the following discussion, Cs refers to the source color for an incoming frag-
ment, Cd refers to the destination color at the corresponding framebuffer location,
and Cc refers to a constant color in the GL state. Individual RGBA components of
these colors are denoted by subscripts of s, d, and c respectively.
    Destination (framebuffer) components are taken to be fixed-point values rep-
resented according to the scheme given in section 2.13.9 (Final Color Processing),
as are source (fragment) components. Constant color components are taken to be
floating point values.
    Prior to blending, each fixed-point color component undergoes an implied con-
version to floating point. This conversion must leave the values 0 and 1 invariant.
Blending computations are treated as if carried out in floating point.
    The commands that control blending are

      void BlendColor( clampf red, clampf green, clampf blue,
         clampf alpha );
      void BlendEquation( enum mode );


      void BlendFunc( enum src, enum dst );


Using BlendColor
The constant color Cc to be used in blending is specified with BlendColor. The
four parameters are clamped to the range [0, 1] before being stored. The constant
color can be used in both the source and destination blending factors.
    BlendColor is an imaging subset feature (see section 3.6.2), and is only al-
lowed when the imaging subset is supported.

Using BlendEquation
Blending capability is defined by the blend equation.       BlendEquation mode
FUNC ADD defines the blending equation as

                                C = Cs S + Cd D
   where Cs and Cd are the source and destination colors, and S and D are
quadruplets of weighting factors as specified by BlendFunc.
   If mode is FUNC SUBTRACT, the blending equation is defined as

                          Version 1.3 - August 14, 2001
4.1. PER-FRAGMENT OPERATIONS                                                    163



                                C = Cs S − Cd D

   If mode is FUNC REVERSE SUBTRACT, the blending equation is defined as

                                C = Cd D − Cs S

   If mode is MIN, the blending equation is defined as

                                C = min(Cs , Cd )

   Finally, if mode is MAX, the blending equation is defined as

                                C = max(Cs , Cd )

    The blending equation is evaluated separately for each color component and
the corresponding weighting factors.
    BlendEquation is an imaging subset feature (see section 3.6.2). If the imaging
subset is not available, then blending always uses the blending equation FUNC ADD.



Using BlendFunc

BlendFunc src indicates how to compute a source blending factor, while dst indi-
cates how to compute a destination factor. The possible arguments and their cor-
responding computed source and destination factors are summarized in Tables 4.1
and 4.2. Addition or subtraction of quadruplets means adding or subtracting them
component-wise.
    The computed source and destination blending quadruplets are applied to the
source and destination R, G, B, and A values to obtain a new set of values that are
sent to the next operation. Let the source and destination blending quadruplets be S
and D, respectively. Then a quadruplet of values is computed using the blend equa-
tion specified by BlendEquation. Each floating-point value in this quadruplet is
clamped to [0, 1] and converted back to a fixed-point value in the manner described
in section 2.13.9. The resulting four values are sent to the next operation.
    BlendFunc arguments CONSTANT COLOR, ONE MINUS CONSTANT COLOR,
CONSTANT ALPHA, and ONE MINUS CONSTANT ALPHA are imaging subset fea-
tures (see section 3.6.2), and are only allowed when the imaging subset is provided.


                          Version 1.3 - August 14, 2001
164              CHAPTER 4. PER-FRAGMENT OPERATIONS AND THE . . .



        Value                              Blend Factors
        ZERO                               (0, 0, 0, 0)
        ONE                                (1, 1, 1, 1)
        DST COLOR                          (Rd , Gd , Bd , Ad )
        ONE MINUS DST COLOR                (1, 1, 1, 1) − (Rd , Gd , Bd , Ad )
        SRC ALPHA                          (As , As , As , As )
        ONE MINUS SRC ALPHA                (1, 1, 1, 1) − (As , As , As , As )
        DST ALPHA                          (Ad , Ad , Ad , Ad )
        ONE MINUS DST ALPHA                (1, 1, 1, 1) − (Ad , Ad , Ad , Ad )
        CONSTANT COLOR                     (Rc , Gc , Bc , Ac )
        ONE MINUS CONSTANT COLOR           (1, 1, 1, 1) − (Rc , Gc , Bc , Ac )
        CONSTANT ALPHA                     (Ac , Ac , Ac , Ac )
        ONE MINUS CONSTANT ALPHA           (1, 1, 1, 1) − (Ac , Ac , Ac , Ac )
        SRC ALPHA SATURATE                 (f, f, f, 1)

Table 4.1: Values controlling the source blending function and the source blending
values they compute. f = min(As , 1 − Ad ).




        Value                              Blend factors
        ZERO                               (0, 0, 0, 0)
        ONE                                (1, 1, 1, 1)
        SRC COLOR                          (Rs , Gs , Bs , As )
        ONE MINUS SRC COLOR                (1, 1, 1, 1) − (Rs , Gs , Bs , As )
        SRC ALPHA                          (As , As , As , As )
        ONE MINUS SRC ALPHA                (1, 1, 1, 1) − (As , As , As , As )
        DST ALPHA                          (Ad , Ad , Ad , Ad )
        ONE MINUS DST ALPHA                (1, 1, 1, 1) − (Ad , Ad , Ad , Ad )
        CONSTANT COLOR                     (Rc , Gc , Bc , Ac )
        ONE MINUS CONSTANT COLOR           (1, 1, 1, 1) − (Rc , Gc , Bc , Ac )
        CONSTANT ALPHA                     (Ac , Ac , Ac , Ac )
        ONE MINUS CONSTANT ALPHA           (1, 1, 1, 1) − (Ac , Ac , Ac , Ac )

Table 4.2: Values controlling the destination blending function and the destination
blending values they compute.




                          Version 1.3 - August 14, 2001
4.1. PER-FRAGMENT OPERATIONS                                                     165


Blending State

The state required for blending is an integer indicating the blending equation, two
integers indicating the source and destination blending functions, four floating-
point values to store the RGBA constant blend color, and a bit indicating whether
blending is enabled or disabled. The initial blending equation is FUNC ADD. The
initial blending functions are ONE for the source function and ZERO for the des-
tination function. The initial constant blend color is (R, G, B, A) = (0, 0, 0, 0).
Initially, blending is disabled.
     Blending occurs once for each color buffer currently enabled for writing (sec-
tion 4.2.1) using each buffer’s color for Cd . If a color buffer has no A value, then
Ad is taken to be 1.


4.1.8   Dithering
Dithering selects between two color values or indices. In RGBA mode, consider
the value of any of the color components as a fixed-point value with m bits to the
left of the binary point, where m is the number of bits allocated to that component
in the framebuffer; call each such value c. For each c, dithering selects a value
c1 such that c1 ∈ {max{0, c − 1}, c } (after this selection, treat c1 as a fixed
point value in [0,1] with m bits). This selection may depend on the xw and yw
coordinates of the pixel. In color index mode, the same rule applies with c being a
single color index. c must not be larger than the maximum value representable in
the framebuffer for either the component or the index, as appropriate.
     Many dithering algorithms are possible, but a dithered value produced by any
algorithm must depend only the incoming value and the fragment’s x and y window
coordinates. If dithering is disabled, then each color component is truncated to a
fixed-point value with as many bits as there are in the corresponding component in
the framebuffer; a color index is rounded to the nearest integer representable in the
color index portion of the framebuffer.
     Dithering is enabled with Enable and disabled with Disable using the symbolic
constant DITHER. The state required is thus a single bit. Initially, dithering is
enabled.


4.1.9 Logical Operation
Finally, a logical operation is applied between the incoming fragment’s color or
index values and the color or index values stored at the corresponding location in
the framebuffer. The result replaces the values in the framebuffer at the fragment’s
(x, y) coordinates. The logical operation on color indices is enabled or disabled

                          Version 1.3 - August 14, 2001
166              CHAPTER 4. PER-FRAGMENT OPERATIONS AND THE . . .


                           Argument value       Operation
                           CLEAR                0
                           AND                  s∧d
                           AND REVERSE          s ∧ ¬d
                           COPY                 s
                           AND INVERTED         ¬s ∧ d
                           NOOP                 d
                           XOR                  s xor d
                           OR                   s∨d
                           NOR                  ¬(s ∨ d)
                           EQUIV                ¬(s xor d)
                           INVERT               ¬d
                           OR REVERSE           s ∨ ¬d
                           COPY INVERTED        ¬s
                           OR INVERTED          ¬s ∨ d
                           NAND                 ¬(s ∧ d)
                           SET                  all 1’s

      Table 4.3: Arguments to LogicOp and their corresponding operations.


with Enable or Disable using the symbolic constant INDEX LOGIC OP. (For com-
patibility with GL version 1.0, the symbolic constant LOGIC OP may also be used.)
The logical operation on color values is enabled or disabled with Enable or Disable
using the symbolic constant COLOR LOGIC OP. If the logical operation is enabled
for color values, it is as if blending were disabled, regardless of the value of BLEND.
    The logical operation is selected by
      void LogicOp( enum op );
op is a symbolic constant; the possible constants and corresponding operations are
enumerated in Table 4.3. In this table, s is the value of the incoming fragment
and d is the value stored in the framebuffer. The numeric values assigned to the
symbolic constants are the same as those assigned to the corresponding symbolic
values in the X window system.
    Logical operations are performed independently for each color index buffer
that is selected for writing, or for each red, green, blue, and alpha value of each
color buffer that is selected for writing. The required state is an integer indicating
the logical operation, and two bits indicating whether the logical operation is en-
abled or disabled. The initial state is for the logic operation to be given by COPY,
and to be disabled.

                           Version 1.3 - August 14, 2001
4.2. WHOLE FRAMEBUFFER OPERATIONS                                                        167


4.1.10    Additional Multisample Fragment Operations
If the DrawBuffer mode is NONE, no change is made to any multisample or color
buffer. Otherwise, fragment processing is as described below.
     If MULTISAMPLE is enabled, and the value of SAMPLE BUFFERS is one, the
alpha test, stencil test, depth test, blending, and dithering operations are performed
for each pixel sample, rather than just once for each fragment. Failure of the alpha,
stencil, or depth test results in termination of the processing of that sample, rather
than discarding of the fragment. All operations are performed on the color, depth,
and stencil values stored in the multisample buffer (to be described in a following
section). The contents of the color buffers are not modified at this point.
     Stencil, depth, blending, and dithering operations are performed for a pixel
sample only if that sample’s fragment coverage bit is a value of 1. If the corre-
sponding coverage bit is 0, no operations are performed for that sample.
     If MULTISAMPLE is disabled, and the value of SAMPLE BUFFERS is one, the
fragment may be treated exactly as described above, with optimization possible
because the fragment coverage must be set to full coverage. Further optimization is
allowed, however. An implementation may choose to identify a centermost sample,
and to perform alpha, stencil, and depth tests on only that sample. Regardless of
the outcome of the stencil test, all multisample buffer stencil sample values are set
to the appropriate new stencil value. If the depth test passes, all multisample buffer
depth sample values are set to the depth of the fragment’s centermost sample’s
depth value, and all multisample buffer color sample values are set to the color
value of the incoming fragment. Otherwise, no change is made to any multisample
buffer color or depth value.
     After all operations have been completed on the multisample buffer, the color
sample values are combined to produce a single color value, and that value is writ-
ten into each color buffer that is currently enabled, based on the DrawBuffer mode.
An implementation may defer the writing of the color buffer until a later time,
but the state of the framebuffer must behave as if the color buffer was updated
as each fragment was processed. The method of combination is not specified,
though a simple average computed independently for each color component is rec-
ommended.


4.2      Whole Framebuffer Operations
The preceding sections described the operations that occur as individual fragments
are sent to the framebuffer. This section describes operations that control or affect
the whole framebuffer.

                               Version 1.3 - August 14, 2001
168               CHAPTER 4. PER-FRAGMENT OPERATIONS AND THE . . .


              symbolic              front    front   back    back    aux
              constant               left    right    left   right    i
              NONE
              FRONT LEFT              •
              FRONT RIGHT                      •
              BACK LEFT                                •
              BACK RIGHT                                       •
              FRONT                   •        •
              BACK                                     •       •
              LEFT                    •                •
              RIGHT                            •               •
              FRONT AND BACK          •        •       •       •
              AUXi                                                    •

      Table 4.4: Arguments to DrawBuffer and the buffers that they indicate.



4.2.1    Selecting a Buffer for Writing
The first such operation is controlling the buffer into which color values are written.
This is accomplished with

        void DrawBuffer( enum buf );

buf is a symbolic constant specifying zero, one, two, or four buffers for writing.
The constants are NONE, FRONT LEFT, FRONT RIGHT, BACK LEFT, BACK RIGHT,
FRONT, BACK, LEFT, RIGHT, FRONT AND BACK, and AUX0 through AUXn, where
n + 1 is the number of available auxiliary buffers.
    The constants refer to the four potentially visible buffers front left, front right,
back left, and back right, and to the auxiliary buffers. Arguments other than AUXi
that omit reference to LEFT or RIGHT refer to both left and right buffers. Argu-
ments other than AUXi that omit reference to FRONT or BACK refer to both front and
back buffers. AUXi enables drawing only to auxiliary buffer i. Each AUXi adheres
to AUXi = AUX0 + i. The constants and the buffers they indicate are summarized
in Table 4.4. If DrawBuffer is is supplied with a constant (other than NONE) that
does not indicate any of the color buffers allocated to the GL context, the error
INVALID OPERATION results.
    Indicating a buffer or buffers using DrawBuffer causes subsequent pixel color
value writes to affect the indicated buffers. If more than one color buffer is se-
lected for drawing, blending and logical operations are computed and applied in-

                           Version 1.3 - August 14, 2001
4.2. WHOLE FRAMEBUFFER OPERATIONS                                                    169


dependently for each buffer. Calling DrawBuffer with a value of NONE inhibits
the writing of color values to any buffer.
    Monoscopic contexts include only left buffers, while stereoscopic contexts in-
clude both left and right buffers. Likewise, single buffered contexts include only
front buffers, while double buffered contexts include both front and back buffers.
The type of context is selected at GL initialization.
    The state required to handle buffer selection is a set of up to 4 + n bits. 4 bits
indicate if the front left buffer, the front right buffer, the back left buffer, or the
back right buffer, are enabled for color writing. The other n bits indicate which of
the auxiliary buffers is enabled for color writing. In the initial state, the front buffer
or buffers are enabled if there are no back buffers; otherwise, only the back buffer
or buffers are enabled.

4.2.2    Fine Control of Buffer Updates
Four commands are used to mask the writing of bits to each of the logical frame-
buffers after all per-fragment operations have been performed. The commands

        void IndexMask( uint mask );
        void ColorMask( boolean r, boolean g, boolean b,
           boolean a );

control the color buffer or buffers (depending on which buffers are currently indi-
cated for writing). The least significant n bits of mask, where n is the number of
bits in a color index buffer, specify a mask. Where a 1 appears in this mask, the
corresponding bit in the color index buffer (or buffers) is written; where a 0 ap-
pears, the bit is not written. This mask applies only in color index mode. In RGBA
mode, ColorMask is used to mask the writing of R, G, B and A values to the color
buffer or buffers. r, g, b, and a indicate whether R, G, B, or A values, respectively,
are written or not (a value of TRUE means that the corresponding value is written).
In the initial state, all bits (in color index mode) and all color values (in RGBA
mode) are enabled for writing.
    The depth buffer can be enabled or disabled for writing zw values using

        void DepthMask( boolean mask );

If mask is non-zero, the depth buffer is enabled for writing; otherwise, it is disabled.
In the initial state, the depth buffer is enabled for writing.
    The command

        void StencilMask( uint mask );

                            Version 1.3 - August 14, 2001
170               CHAPTER 4. PER-FRAGMENT OPERATIONS AND THE . . .


controls the writing of particular bits into the stencil planes. The least significant s
bits of mask comprise an integer mask (s is the number of bits in the stencil buffer),
just as for IndexMask. The initial state is for the stencil plane mask to be all ones.
    The state required for the various masking operations is two integers and a bit:
an integer for color indices, an integer for stencil values, and a bit for depth values.
A set of four bits is also required indicating which color components of an RGBA
value should be written. In the initial state, the integer masks are all ones as are the
bits controlling depth value and RGBA component writing.

Fine Control of Multisample Buffer Updates
When the value of SAMPLE BUFFERS is one, ColorMask, DepthMask, and Sten-
cilMask control the modification of values in the multisample buffer. The color
mask has no effect on modifications to the color buffers. If the color mask is
entirely disabled, the color sample values must still be combined (as described
above) and the result used to replace the color values of the buffers enabled by
DrawBuffer.

4.2.3    Clearing the Buffers
The GL provides a means for setting portions of every pixel in a particular buffer
to the same value. The argument to

        void Clear( bitfield buf );

is the bitwise OR of a number of values indicating which buffers are to
be cleared. The values are COLOR BUFFER BIT, DEPTH BUFFER BIT, STEN-
CIL BUFFER BIT, and ACCUM BUFFER BIT, indicating the buffers currently en-
abled for color writing, the depth buffer, the stencil buffer, and the accumulation
buffer (see below), respectively. The value to which each buffer is cleared depends
on the setting of the clear value for that buffer. If the mask is not a bitwise OR of
the specified values, then the error INVALID VALUE is generated.

        void ClearColor( clampf r, clampf g, clampf b,
           clampf a );

sets the clear value for the color buffers in RGBA mode. Each of the specified
components is clamped to [0, 1] and converted to fixed-point according to the rules
of section 2.13.9.

        void ClearIndex( float index );

                           Version 1.3 - August 14, 2001
4.2. WHOLE FRAMEBUFFER OPERATIONS                                                          171


sets the clear color index. index is converted to a fixed-point value with unspecified
precision to the left of the binary point; the integer part of this value is then masked
with 2m − 1, where m is the number of bits in a color index value stored in the
framebuffer.

      void ClearDepth( clampd d );

takes a floating-point value that is clamped to the range [0, 1] and converted to
fixed-point according to the rules for a window z value given in section 2.10.1.
Similarly,

      void ClearStencil( int s );

takes a single integer argument that is the value to which to clear the stencil buffer.
s is masked to the number of bitplanes in the stencil buffer.

      void ClearAccum( float r, float g, float b, float a );

takes four floating-point arguments that are the values, in order, to which to set the
R, G, B, and A values of the accumulation buffer (see the next section). These
values are clamped to the range [−1, 1] when they are specified.
     When Clear is called, the only per-fragment operations that are applied (if
enabled) are the pixel ownership test, the scissor test, and dithering. The masking
operations described in the last section (4.2.2) are also effective. If a buffer is not
present, then a Clear directed at that buffer has no effect.
     The state required for clearing is a clear value for each of the color buffer, the
depth buffer, the stencil buffer, and the accumulation buffer. Initially, the RGBA
color clear value is (0,0,0,0), the clear color index is 0, and the stencil buffer and
accumulation buffer clear values are all 0. The depth buffer clear value is initially
1.0.


Clearing the Multisample Buffer

The color samples of the multisample buffer are cleared when one or more color
buffers are cleared, as specified by the Clear mask bit COLOR BUFFER BIT and
the DrawBuffer mode. If the DrawBuffer mode is NONE, the color samples of the
multisample buffer cannot be cleared.
    If the Clear mask bits DEPTH BUFFER BIT or STENCIL BUFFER BIT are set,
then the corresponding depth or stencil samples, respectively, are cleared.

                                Version 1.3 - August 14, 2001
172              CHAPTER 4. PER-FRAGMENT OPERATIONS AND THE . . .


4.2.4    The Accumulation Buffer
Each portion of a pixel in the accumulation buffer consists of four values: one for
each of R, G, B, and A. The accumulation buffer is controlled exclusively through
the use of

        void Accum( enum op, float value );

(except for clearing it). op is a symbolic constant indicating an accumulation buffer
operation, and value is a floating-point value to be used in that operation. The
possible operations are ACCUM, LOAD, RETURN, MULT, and ADD.
    When the scissor test is enabled (section 4.1.2), then only those pixels within
the current scissor box are updated by any Accum operation; otherwise, all pixels
in the window are updated. The accumulation buffer operations apply identically
to every affected pixel, so we describe the effect of each operation on an individ-
ual pixel. Accumulation buffer values are taken to be signed values in the range
[−1, 1]. Using ACCUM obtains R, G, B, and A components from the buffer currently
selected for reading (section 4.3.2). Each component, considered as a fixed-point
value in [0, 1]. (see section 2.13.9), is converted to floating-point. Each result is
then multiplied by value. The results of this multiplication are then added to the
corresponding color component currently in the accumulation buffer, and the re-
sulting color value replaces the current accumulation buffer color value.
    The LOAD operation has the same effect as ACCUM, but the computed values
replace the corresponding accumulation buffer components rather than being added
to them.
    The RETURN operation takes each color value from the accumulation buffer,
multiplies each of the R, G, B, and A components by value, and clamps the re-
sults to the range [0, 1] The resulting color value is placed in the buffers currently
enabled for color writing as if it were a fragment produced from rasterization, ex-
cept that the only per-fragment operations that are applied (if enabled) are the pixel
ownership test, the scissor test (section 4.1.2), and dithering (section 4.1.8). Color
masking (section 4.2.2) is also applied.
    The MULT operation multiplies each R, G, B, and A in the accumulation buffer
by value and then returns the scaled color components to their corresponding ac-
cumulation buffer locations. this case value is clamped to the range [−1, 1]. ADD is
the same as MULT except that value is added to each of the color components.
    The color components operated on by Accum must be clamped only if the
operation is RETURN. In this case, a value sent to the enabled color buffers is first
clamped to [0, 1]. Otherwise, results are undefined if the result of an operation on a
color component is out of the range [−1, 1]. If there is no accumulation buffer, or if
the GL is in color index mode, Accum generates the error INVALID OPERATION.

                           Version 1.3 - August 14, 2001
4.3. DRAWING, READING, AND COPYING PIXELS                                         173


    No state (beyond the accumulation buffer itself) is required for accumulation
buffering.


4.3     Drawing, Reading, and Copying Pixels
Pixels may be written to and read from the framebuffer using the DrawPixels and
ReadPixels commands. CopyPixels can be used to copy a block of pixels from
one portion of the framebuffer to another.

4.3.1    Writing to the Stencil Buffer
The operation of DrawPixels was described in section 3.6.4, except if the format
argument was STENCIL INDEX. In this case, all operations described for Draw-
Pixels take place, but window (x, y) coordinates, each with the corresponding
stencil index, are produced in lieu of fragments. Each coordinate-stencil index
pair is sent directly to the per-fragment operations, bypassing the texture, fog, and
antialiasing application stages of rasterization. Each pair is then treated as a frag-
ment for purposes of the pixel ownership and scissor tests; all other per-fragment
operations are bypassed. Finally, each stencil index is written to its indicated loca-
tion in the framebuffer, subject to the current setting of StencilMask.
    The error INVALID OPERATION results if there is no stencil buffer.

4.3.2    Reading Pixels
The method for reading pixels from the framebuffer and placing them in client
memory is diagrammed in Figure 4.2. We describe the stages of the pixel reading
process in the order in which they occur.
   Pixels are read using

        void ReadPixels( int x, int y, sizei width, sizei height,
          enum format, enum type, void *data );

The arguments after x and y to ReadPixels correspond to those of DrawPixels.
The pixel storage modes that apply to ReadPixels and other commands that query
images (see section 6.1) are summarized in Table 4.5.

Obtaining Pixels from the Framebuffer
If the format is DEPTH COMPONENT, then values are obtained from the depth buffer.
If there is no depth buffer, the error INVALID OPERATION occurs.

                           Version 1.3 - August 14, 2001
174                 CHAPTER 4. PER-FRAGMENT OPERATIONS AND THE . . .



        RGBA pixel                                                                color index pixel
          data in                                                                      data in

                                      convert
                                      to float
                                                                                                                                                  




                                                                                                                                                  




                                                                                                                                                  




                                   




                                   scale                             
                                                                        Pixel Transfer
                                                                                                                         




                                                                                                                          shift
                                                                                                                                                  




                              




                                  and bias
                                                                     
                                                                         Operations
                                                                                                                     




                                                                                                                        and offset
                                                                                                                                                  




                                                                                                                                                  




                                                                                                                                                  




                                                                                                                                                  




                             RGBA to RGBA                                index to RGBA                              index to index
                                lookup                                       lookup                                    lookup
                                                                                                                                                  




                                                                                                                                                  




                                                                                                                                                  




                                                                                                                                                  




                              




                                 color table
                                                                                                                                                  




                                   




                                   lookup
                                                                                                                                                  




                                                                                                                                                  




                                                                                                                                                  




                                         




                              convolution
                                                                                        




                                                                             color table
                                                                                                         




                                                                                                           post
                                                                                                                                                  




                          




                             scale and bias
                                                                               




                                                                               lookup
                                                                                                    




                                                                                                       color matrix
                                                                                                                                                  




                                                                                                                                                  




                                                                                                                                                  




                                                                                                                                                  




         post                 




                                 color table
                                                                          




                                                                             histogram
                                                                                                                                                  




      convolution
                                   




                                   lookup
                                                                                                                                                  




                                                                                                                                                  




                                                                                                                                                  




                                                                                                                                                  




                              color matrix                                        minmax
                             scale and bias
                                                                                                                                                  




                                                                                                                                                  




                                                                                                                                                  




                ¡    ¡   ¡   ¡    ¡     ¡   ¡   ¡   ¡   ¡   ¡   ¡   ¡    ¡    ¡    ¡   ¡   ¡   ¡   ¡    ¡   ¡   ¡   ¡   ¡    ¡   ¡   ¡   ¡   ¡   ¡




                ¡    ¡   ¡   ¡    ¡     ¡   ¡   ¡   ¡   ¡   ¡   ¡   ¡    ¡    ¡    ¡   ¡   ¡   ¡   ¡    ¡   ¡   ¡   ¡   ¡    ¡   ¡   ¡   ¡   ¡   ¡




                ¡    ¡   ¡   ¡




                                 convert
                                  ¡     ¡   ¡   ¡   ¡   ¡   ¡   ¡   ¡




                                                                        Pixel Storage
                                                                         ¡    ¡    ¡   ¡   ¡   ¡   ¡    ¡   ¡   ¡   ¡   ¡    ¡   ¡   ¡   ¡   ¡   ¡




                ¡    ¡   ¡   ¡
                                 RGB to L
                                  ¡     ¡   ¡   ¡   ¡   ¡   ¡   ¡   ¡




                                                                         Operations
                                                                         ¡    ¡    ¡   ¡   ¡   ¡   ¡    ¡   ¡   ¡   ¡   ¡    ¡   ¡   ¡   ¡   ¡   ¡




                ¡    ¡   ¡   ¡    ¡     ¡   ¡   ¡   ¡   ¡   ¡   ¡   ¡    ¡    ¡    ¡   ¡   ¡   ¡   ¡    ¡   ¡   ¡   ¡   ¡    ¡   ¡   ¡   ¡   ¡   ¡




                ¡    ¡   ¡   ¡    ¡     ¡   ¡   ¡   ¡   ¡   ¡   ¡   ¡    ¡    ¡    ¡   ¡   ¡   ¡   ¡    ¡   ¡   ¡   ¡   ¡    ¡   ¡   ¡   ¡   ¡   ¡




                ¡    ¡   ¡   ¡    ¡




                                       clamp
                                        ¡   ¡   ¡   ¡   ¡   ¡   ¡   ¡    ¡    ¡    ¡   ¡   ¡   ¡   ¡    ¡   ¡   ¡   ¡   ¡




                                                                                                                            mask to
                                                                                                                             ¡   ¡   ¡   ¡   ¡   ¡




                                      to [0,1]                                                                              (2n − 1)
                ¡    ¡   ¡   ¡    ¡     ¡   ¡   ¡   ¡   ¡   ¡   ¡   ¡    ¡    ¡    ¡   ¡   ¡   ¡   ¡    ¡   ¡   ¡   ¡   ¡    ¡   ¡   ¡   ¡   ¡   ¡




                ¡    ¡   ¡   ¡    ¡     ¡   ¡   ¡   ¡   ¡   ¡   ¡   ¡    ¡    ¡    ¡   ¡   ¡   ¡   ¡    ¡   ¡   ¡   ¡   ¡    ¡   ¡   ¡   ¡   ¡   ¡




                ¡    ¡   ¡   ¡    ¡     ¡   ¡   ¡   ¡   ¡   ¡   ¡   ¡    ¡    ¡    ¡   ¡   ¡   ¡   ¡    ¡   ¡   ¡   ¡   ¡    ¡   ¡   ¡   ¡   ¡   ¡




                ¡    ¡   ¡   ¡    ¡     ¡   ¡   ¡   ¡   ¡   ¡   ¡   ¡    ¡    ¡    ¡   ¡   ¡   ¡   ¡    ¡   ¡   ¡   ¡   ¡    ¡   ¡   ¡   ¡   ¡   ¡




                ¡    ¡   ¡   ¡    ¡     ¡   ¡   ¡   ¡   ¡   ¡   ¡   ¡    ¡    ¡




                                                                                   pack
                                                                                   ¡   ¡   ¡   ¡   ¡    ¡   ¡   ¡   ¡   ¡    ¡   ¡   ¡   ¡   ¡   ¡




                ¡    ¡   ¡   ¡    ¡     ¡   ¡   ¡   ¡   ¡   ¡   ¡   ¡    ¡    ¡    ¡   ¡   ¡   ¡   ¡    ¡   ¡   ¡   ¡   ¡    ¡   ¡   ¡   ¡   ¡   ¡




                ¡    ¡   ¡   ¡    ¡     ¡   ¡   ¡   ¡   ¡   ¡   ¡   ¡    ¡    ¡    ¡   ¡   ¡   ¡   ¡    ¡   ¡   ¡   ¡   ¡    ¡   ¡   ¡   ¡   ¡   ¡




                        byte, short, int, or float pixel
                     data stream (index or component)




  Figure 4.2. Operation of ReadPixels. Operations in dashed boxes may be enabled
  or disabled. RGBA and color index pixel paths are shown; depth and stencil pixel
  paths are not shown.

                                       Version 1.3 - August 14, 2001
4.3. DRAWING, READING, AND COPYING PIXELS                                         175


         Parameter Name             Type      Initial Value   Valid Range
         PACK   SWAP BYTES         boolean       FALSE        TRUE/FALSE
         PACK   LSB FIRST          boolean       FALSE        TRUE/FALSE
         PACK   ROW LENGTH         integer          0           [0, ∞)
         PACK   SKIP ROWS          integer          0           [0, ∞)
         PACK   SKIP PIXELS        integer          0           [0, ∞)
         PACK   ALIGNMENT          integer          4           1,2,4,8
         PACK   IMAGE HEIGHT       integer          0           [0, ∞)
         PACK   SKIP IMAGES        integer          0           [0, ∞)

Table 4.5: PixelStore parameters pertaining to ReadPixels, GetTexIm-
age1D, GetTexImage2D, GetTexImage3D, GetColorTable, GetConvolution-
Filter, GetSeparableFilter, GetHistogram, and GetMinmax.



    If there is a multisample buffer (SAMPLE BUFFERS is 1), then values are ob-
tained from the depth samples in this buffer. It is recommended that the depth
value of the centermost sample be used, though implementations may choose any
function of the depth sample values at each pixel.
    If the format is STENCIL INDEX, then values are taken from the stencil buffer;
again, if there is no stencil buffer, the error INVALID OPERATION occurs.
    If there is a multisample buffer, then values are obtained from the stencil sam-
ples in this buffer. It is recommended that the stencil value of the centermost sam-
ple be used, though implementations may choose any function of the stencil sample
values at each pixel.
    For all other formats, the buffer from which values are obtained is one of the
color buffers; the selection of color buffer is controlled with ReadBuffer.
    The command

      void ReadBuffer( enum src );

takes a symbolic constant as argument. The possible values are FRONT LEFT,
FRONT RIGHT, BACK LEFT, BACK RIGHT, FRONT, BACK, LEFT, RIGHT, and AUX0
through AUXn. FRONT and LEFT refer to the front left buffer, BACK refers to the
back left buffer, and RIGHT refers to the front right buffer. The other constants cor-
respond directly to the buffers that they name. If the requested buffer is missing,
then the error INVALID OPERATION is generated. The initial setting for Read-
Buffer is FRONT if there is no back buffer and BACK otherwise.
     ReadPixels obtains values from the selected buffer from each pixel with lower
left hand corner at (x + i, y + j) for 0 ≤ i < width and 0 ≤ j < height; this pixel

                           Version 1.3 - August 14, 2001
176              CHAPTER 4. PER-FRAGMENT OPERATIONS AND THE . . .


is said to be the ith pixel in the jth row. If any of these pixels lies outside of the
window allocated to the current GL context, the values obtained for those pixels
are undefined. Results are also undefined for individual pixels that are not owned
by the current context. Otherwise, ReadPixels obtains values from the selected
buffer, regardless of how those values were placed there.
    If the GL is in RGBA mode, and format is one of RED, GREEN, BLUE, AL-
PHA, RGB, RGBA, BGR, BGRA, LUMINANCE, or LUMINANCE ALPHA, then red, green,
blue, and alpha values are obtained from the selected buffer at each pixel location.
If the framebuffer does not support alpha values then the A that is obtained is
1.0. If format is COLOR INDEX and the GL is in RGBA mode then the error IN-
VALID OPERATION occurs. If the GL is in color index mode, and format is not
DEPTH COMPONENT or STENCIL INDEX, then the color index is obtained at each
pixel location.

Conversion of RGBA values

This step applies only if the GL is in RGBA mode, and then only if format is
neither STENCIL INDEX nor DEPTH COMPONENT. The R, G, B, and A values form
a group of elements. Each element is taken to be a fixed-point value in [0, 1] with
m bits, where m is the number of bits in the corresponding color component of the
selected buffer (see section 2.13.9).

Conversion of Depth values

This step applies only if format is DEPTH COMPONENT. An element is taken to be a
fixed-point value in [0,1] with m bits, where m is the number of bits in the depth
buffer (see section 2.10.1).

Pixel Transfer Operations

This step is actually the sequence of steps that was described separately in sec-
tion 3.6.5. After the processing described in that section is completed, groups are
processed as described in the following sections.

Conversion to L

This step applies only to RGBA component groups, and only if the format is either
LUMINANCE or LUMINANCE ALPHA. A value L is computed as

                                  L=R+G+B

                           Version 1.3 - August 14, 2001
4.3. DRAWING, READING, AND COPYING PIXELS                                        177


                         type Parameter        Index Mask
                         UNSIGNED BYTE         28 − 1
                         BITMAP                1
                         BYTE                  27 − 1
                         UNSIGNED SHORT        216 − 1
                         SHORT                 215 − 1
                         UNSIGNED INT          232 − 1
                         INT                   231 − 1

Table 4.6: Index masks used by ReadPixels. Floating point data are not masked.



where R, G, and B are the values of the R, G, and B components. The single
computed L component replaces the R, G, and B components in the group.

Final Conversion
For an index, if the type is not FLOAT, final conversion consists of masking the
index with the value given in Table 4.6; if the type is FLOAT, then the integer index
is converted to a GL float data value.
    For an RGBA color, each component is first clamped to [0, 1]. Then the
appropriate conversion formula from table 4.7 is applied to the component.

Placement in Client Memory
Groups of elements are placed in memory just as they are taken from memory for
DrawPixels. That is, the ith group of the jth row (corresponding to the ith pixel in
the jth row) is placed in memory just where the ith group of the jth row would be
taken from for DrawPixels. See Unpacking under section 3.6.4. The only differ-
ence is that the storage mode parameters whose names begin with PACK are used
instead of those whose names begin with UNPACK . If the format is RED, GREEN,
BLUE, ALPHA, or LUMINANCE, only the corresponding single element is written.
Likewise if the format is LUMINANCE ALPHA, RGB, or BGR, only the corresponding
two or three elements are written. Otherwise all the elements of each group are
written.

4.3.3   Copying Pixels
CopyPixels transfers a rectangle of pixel values from one region of the framebuffer
to another. Pixel copying is diagrammed in Figure 4.3.

                          Version 1.3 - August 14, 2001
178              CHAPTER 4. PER-FRAGMENT OPERATIONS AND THE . . .




  type Parameter                       GL Data Type     Component
                                                        Conversion Formula
  UNSIGNED    BYTE                         ubyte        c = (28 − 1)f
  BYTE                                     byte         c = [(28 − 1)f − 1]/2
  UNSIGNED    SHORT                       ushort        c = (216 − 1)f
  SHORT                                    short        c = [(216 − 1)f − 1]/2
  UNSIGNED    INT                           uint        c = (232 − 1)f
  INT                                       int         c = [(232 − 1)f − 1]/2
  FLOAT                                    float        c=f
  UNSIGNED    BYTE 3 3 2                   ubyte        c = (2N − 1)f
  UNSIGNED    BYTE 2 3 3 REV               ubyte        c = (2N − 1)f
  UNSIGNED    SHORT 5 6 5                 ushort        c = (2N − 1)f
  UNSIGNED    SHORT 5 6 5 REV             ushort        c = (2N − 1)f
  UNSIGNED    SHORT 4 4 4 4               ushort        c = (2N − 1)f
  UNSIGNED    SHORT 4 4 4 4 REV           ushort        c = (2N − 1)f
  UNSIGNED    SHORT 5 5 5 1               ushort        c = (2N − 1)f
  UNSIGNED    SHORT 1 5 5 5 REV           ushort        c = (2N − 1)f
  UNSIGNED    INT 8 8 8 8                   uint        c = (2N − 1)f
  UNSIGNED    INT 8 8 8 8 REV               uint        c = (2N − 1)f
  UNSIGNED    INT 10 10 10 2                uint        c = (2N − 1)f
  UNSIGNED    INT 2 10 10 10 REV            uint        c = (2N − 1)f

Table 4.7: Reversed component conversions, used when component data are being
returned to client memory. Color, normal, and depth components are converted
from the internal floating-point representation (f ) to a datum of the specified GL
data type (c) using the specified equation. All arithmetic is done in the internal
floating point format. These conversions apply to component data returned by GL
query commands and to components of pixel data returned to client memory. The
equations remain the same even if the implemented ranges of the GL data types are
greater than the minimum required ranges. (See Table 2.2.) Equations with N as
the exponent are performed for each bitfield of the packed data type, with N set to
the number of bits in the bitfield.




                          Version 1.3 - August 14, 2001
4.3. DRAWING, READING, AND COPYING PIXELS                                                                                                               179




        RGBA pixel                                                         color index pixel
   data from framebuffer                                                 data from framebuffer

                                   convert
                                   to float
                                                                                                                                                     




                                                                                                                                                     




                               




                                    scale
                                                                  



                                                                     Pixel Transfer
                                                                                                                             




                                                                                                                             shift
                                                                                                                                                     




                               




                                   and bias
                                                                      




                                                                      Operations
                                                                                                                        




                                                                                                                           and offset
                                                                                                                                                     




                                                                                                                                                     




                                                                                                                                                     




                                                                                                                                                     




                          
                             RGBA to RGBA
                                                                      
                                                                         index to RGBA
                                                                                                                   
                                                                                                                      index to index
                                                                                                                                                     




                               
                                lookup
                                                                           
                                                                             lookup
                                                                                                                        
                                                                                                                         lookup
                                                                                                                                                     




                                                                                                                                                     




                                                                                                                                                     




                               




                                  color table
                                                                                                                                                     




                               




                                    lookup
                                                                                                                                                     




                                                                                                                                                     




                                                                                                                                                     




                                                                                                            post
                                                                                                                                                     




                              convolution                                     color table
                                         




                             scale and bias
                                                                                     




                                                                                lookup
                                                                                                     




                                                                                                        color matrix
                                                                                                                                                     




                                                                                                                                                     




                                                                                                                                                     




                                                                                                                                                     




      post                     




                                  color table
                                                                           




                                                                              histogram
                                                                                                                                                     




   convolution                 




                                    lookup
                                                                                                                                                     




                                                                                                                                                     




                                                                                                                                                     




                                                                                                                                                     




                          
                              color matrix
                                                                           
                                                                               minmax
                                                                                                                                                     




                          
                             scale and bias
                                                                                                                                                     




                                                                                                                                                     




                                    clamp                                    final                                         mask to
                                   to [0,1]                               conversion                                       (2n − 1)

           RGBA pixel                                                                           color index pixel
            data out                                                                                data out




  Figure 4.3. Operation of CopyPixels. Operations in dashed boxes may be enabled
  or disabled. Index-to-RGBA lookup is currently never performed. RGBA and color
  index pixel paths are shown; depth and stencil pixel paths are not shown.




                                            Version 1.3 - August 14, 2001
180              CHAPTER 4. PER-FRAGMENT OPERATIONS AND THE . . .


        void CopyPixels( int x, int y, sizei width, sizei height,
           enum type );

type is a symbolic constant that must be one of COLOR, STENCIL, or DEPTH, indi-
cating that the values to be transferred are colors, stencil values, or depth values,
respectively. The first four arguments have the same interpretation as the corre-
sponding arguments to ReadPixels.
     Values are obtained from the framebuffer, converted (if appropriate), then sub-
jected to the pixel transfer operations described in section 3.6.5, just as if Read-
Pixels were called with the corresponding arguments. If the type is STENCIL
or DEPTH, then it is as if the format for ReadPixels were STENCIL INDEX or
DEPTH COMPONENT, respectively. If the type is COLOR, then if the GL is in RGBA
mode, it is as if the format were RGBA, while if the GL is in color index mode, it is
as if the format were COLOR INDEX.
     The groups of elements so obtained are then written to the framebuffer just as
if DrawPixels had been given width and height, beginning with final conversion
of elements. The effective format is the same as that already described.

4.3.4    Pixel Draw/Read State
The state required for pixel operations consists of the parameters that are set with
PixelStore, PixelTransfer, and PixelMap. This state has been summarized in
Tables 3.1, 3.2, and 3.3. The current setting of ReadBuffer, an integer, is also
required, along with the current raster position (section 2.12). State set with Pixel-
Store is GL client state.




                           Version 1.3 - August 14, 2001
Chapter 5

Special Functions

This chapter describes additional GL functionality that does not fit easily into any
of the preceding chapters. This functionality consists of evaluators (used to model
curves and surfaces), selection (used to locate rendered primitives on the screen),
feedback (which returns GL results before rasterization), display lists (used to des-
ignate a group of GL commands for later execution by the GL), flushing and fin-
ishing (used to synchronize the GL command stream), and hints.


5.1    Evaluators
Evaluators provide a means to use a polynomial or rational polynomial mapping
to produce vertex, normal, and texture coordinates, and colors. The values so pro-
duced are sent on to further stages of the GL as if they had been provided directly
by the client. Transformations, lighting, primitive assembly, rasterization, and per-
pixel operations are not affected by the use of evaluators.
    Consider the Rk -valued polynomial p(u) defined by
                                         n
                               p(u) =         Bin (u)Ri                         (5.1)
                                        i=0

with Ri ∈ Rk and
                                        n i
                           Bin (u) =      u (1 − u)n−i ,
                                        i
                                                                     n
the ith Bernstein polynomial of degree n (recall that 00 ≡ 1 and     0   ≡ 1). Each
Ri is a control point. The relevant command is

      void Map1{fd}( enum target, T u1 , T u2 , int stride,
        int order, T points );

                                        181
182                                           CHAPTER 5. SPECIAL FUNCTIONS


 target                       k    Values
 MAP1     VERTEX 3            3    x, y, z vertex coordinates
 MAP1     VERTEX 4            4    x, y, z, w vertex coordinates
 MAP1     INDEX               1    color index
 MAP1     COLOR 4             4    R, G, B, A
 MAP1     NORMAL              3    x, y, z normal coordinates
 MAP1     TEXTURE COORD   1   1    s texture coordinate
 MAP1     TEXTURE COORD   2   2    s, t texture coordinates
 MAP1     TEXTURE COORD   3   3    s, t, r texture coordinates
 MAP1     TEXTURE COORD   4   4    s, t, r, q texture coordinates


Table 5.1: Values specified by the target to Map1. Values are given in the order in
which they are taken.


target is a symbolic constant indicating the range of the defined polynomial. Its
possible values, along with the evaluations that each indicates, are given in Ta-
ble 5.1. order is equal to n + 1; The error INVALID VALUE is generated if order
is less than one or greater than MAX EVAL ORDER. points is a pointer to a set of
n + 1 blocks of storage. Each block begins with k single-precision floating-point
or double-precision floating-point values, respectively. The rest of the block may
be filled with arbitrary data. Table 5.1 indicates how k depends on target and what
the k values represent in each case.
     stride is the number of single- or double-precision values (as appropriate) in
each block of storage. The error INVALID VALUE results if stride is less than
k. The order of the polynomial, order, is also the number of blocks of storage
containing control points.
     u1 and u2 give two floating-point values that define the endpoints of the pre-
image of the map. When a value u is presented for evaluation, the formula used
is
                                             u − u1
                                p (u ) = p(          ).
                                             u2 − u1
The error INVALID VALUE results if u1 = u2 .
    Map2 is analogous to Map1, except that it describes bivariate polynomials of
the form
                                   n   m
                       p(u, v) =             Bin (u)Bjm (v)Rij .
                                   i=0 j=0

The form of the Map2 command is

                          Version 1.3 - August 14, 2001
5.1. EVALUATORS                                                                                    183



           Integers                     Reals
                                                                             Vertices
                      k                     [u1,u2]                          Normals
                                                                     ΣBiRi
      EvalMesh                                               [0,1]
                                                      Ax+b                   Texture Coordinates
      EvalPoint       l                     [v1,v2]
                                                             [0,1]
                                                                             Colors


                          MapGrid                              Map
                                      EvalCoord




   Figure 5.1. Map Evaluation.



      void Map2{fd}( enum target, T u1 , T u2 , int ustride,
        int uorder, T v1 , T v2 , int vstride, int vorder, T points );

target is a range type selected from the same group as is used for Map1, except
that the string MAP1 is replaced with MAP2. points is a pointer to (n + 1)(m + 1)
blocks of storage (uorder = n + 1 and vorder = m + 1; the error IN-
VALID VALUE is generated if either uorder or vorder is less than one or greater
than MAX EVAL ORDER). The values comprising Rij are located

                                    (ustride)i + (vstride)j

values (either single- or double-precision floating-point, as appropriate) past the
first value pointed to by points. u1 , u2 , v1 , and v2 define the pre-image rectangle
of the map; a domain point (u , v ) is evaluated as

                                                u − u1 v − v1
                            p (u , v ) = p(            ,        ).
                                                u2 − u1 v2 − v1
    The evaluation of a defined map is enabled or disabled with Enable and Dis-
able using the constant corresponding to the map as described above. The eval-
uator map generates only coordinates for texture unit TEXTURE0. The error IN-
VALID VALUE results if either ustride or vstride is less than k, or if u1 is equal
to u2, or if v1 is equal to v2 . If the value of ACTIVE TEXTURE is not TEXTURE0,
calling Map{12} generates the error INVALID OPERATION.
    Figure 5.1 describes map evaluation schematically; an evaluation of enabled
maps is effected in one of two ways. The first way is to use

      void EvalCoord{12}{fd}( T arg );
      void EvalCoord{12}{fd}v( T arg );

                              Version 1.3 - August 14, 2001
184                                         CHAPTER 5. SPECIAL FUNCTIONS


EvalCoord1 causes evaluation of the enabled one-dimensional maps. The argu-
ment is the value (or a pointer to the value) that is the domain coordinate, u . Eval-
Coord2 causes evaluation of the enabled two-dimensional maps. The two values
specify the two domain coordinates, u and v , in that order.
     When one of the EvalCoord commands is issued, all currently enabled maps
of the indicated dimension are evaluated. Then, for each enabled map, it is as if a
corresponding GL command were issued with the resulting coordinates, with one
important difference. The difference is that when an evaluation is performed, the
GL uses evaluated values instead of current values for those evaluations that are
enabled (otherwise, the current values are used). The order of the effective com-
mands is immaterial, except that Vertex (for vertex coordinate evaluation) must be
issued last. Use of evaluators has no effect on the current color, normal, or texture
coordinates. If ColorMaterial is enabled, evaluated color values affect the result
of the lighting equation as if the current color was being modified, but no change
is made to the tracking lighting parameters or to the current color.
     No command is effectively issued if the corresponding map (of the indicated
dimension) is not enabled. If more than one evaluation is enabled for a particu-
lar dimension (e.g. MAP1 TEXTURE COORD 1 and MAP1 TEXTURE COORD 2), then
only the result of the evaluation of the map with the highest number of coordinates
is used.
     Finally, if either MAP2 VERTEX 3 or MAP2 VERTEX 4 is enabled, then the nor-
mal to the surface is computed. Analytic computation, which sometimes yields
normals of length zero, is one method which may be used. If automatic normal
generation is enabled, then this computed normal is used as the normal associated
with a generated vertex. Automatic normal generation is controlled with Enable
and Disable with symbolic the constant AUTO NORMAL. If automatic normal gener-
ation is disabled, then a corresponding normal map, if enabled, is used to produce
a normal. If neither automatic normal generation nor a normal map are enabled,
then no normal is sent with a vertex resulting from an evaluation (the effect is that
the current normal is used).
     For MAP VERTEX 3, let q = p. For MAP VERTEX 4, let q = (x/w, y/w, z/w),
where (x, y, z, w) = p. Then let
                                        ∂q ∂q
                                  m=       ×    .
                                        ∂u   ∂v
Then the generated analytic normal, n, is given by n = m/ m .
    The second way to carry out evaluations is to use a set of commands that pro-
vide for efficient specification of a series of evenly spaced values to be mapped.
This method proceeds in two steps. The first step is to define a grid in the domain.
This is done using

                           Version 1.3 - August 14, 2001
5.1. EVALUATORS                                                                  185


      void MapGrid1{fd}( int n, T u1 , T u2 );

for a one-dimensional map or

      void MapGrid2{fd}( int nu , T u1 , T u2 , int nv , T v1 ,
         T v2 );

for a two-dimensional map. In the case of MapGrid1 u1 and u2 describe an
interval, while n describes the number of partitions of the interval. The error
INVALID VALUE results if n ≤ 0. For MapGrid2, (u1 , v1 ) specifies one two-
dimensional point and (u2 , v2 ) specifies another. nu gives the number of partitions
between u1 and u2 , and nv gives the number of partitions between v1 and v2 . If
either nu ≤ 0 or nv ≤ 0, then the error INVALID VALUE occurs.
    Once a grid is defined, an evaluation on a rectangular subset of that grid may
be carried out by calling

      void EvalMesh1( enum mode, int p1 , int p2 );

mode is either POINT or LINE. The effect is the same as performing the following
code fragment, with ∆u = (u2 − u1 )/n:
         Begin(type);
           for i = p1 to p2 step 1.0
              EvalCoord1(i * ∆u + u1 );
         End();
where EvalCoord1f or EvalCoord1d is substituted for EvalCoord1 as appro-
priate. If mode is POINT, then type is POINTS; if mode is LINE, then type is
LINE STRIP. The one requirement is that if either i = 0 or i = n, then the value
computed from i ∗ ∆u + u1 is precisely u1 or u2 , respectively.
    The corresponding commands for two-dimensional maps are

      void EvalMesh2( enum mode, int p1 , int p2 , int q1 ,
         int q2 );

mode must be FILL, LINE, or POINT. When mode is FILL, then these commands
are equivalent to the following, with ∆u = (u2 − u1 )/n and ∆v = (v2 − v1 )/m:
         for i = q1 to q2 − 1 step 1.0
            Begin(QUAD STRIP);
               for j = p1 to p2 step 1.0
                  EvalCoord2(j * ∆u + u1 , i * ∆v + v1 );
                  EvalCoord2(j * ∆u + u1 , (i + 1) * ∆v + v1 );
            End();

                          Version 1.3 - August 14, 2001
186                                        CHAPTER 5. SPECIAL FUNCTIONS


If mode is LINE, then a call to EvalMesh2 is equivalent to
         for i = q1 to q2 step 1.0
            Begin(LINE STRIP);
            for j = p1 to p2 step 1.0
               EvalCoord2(j * ∆u + u1 , i * ∆v + v1 );
            End();;
         for i = p1 to p2 step 1.0
            Begin(LINE STRIP);
            for j = q1 to q2 step 1.0
               EvalCoord2(i * ∆u + u1 , j * ∆v + v1 );
            End();
If mode is POINT, then a call to EvalMesh2 is equivalent to
         Begin(POINTS);
           for i = q1 to q2 step 1.0
              for j = p1 to p2 step 1.0
                 EvalCoord2(j * ∆u + u1 , i * ∆v + v1 );
         End();
Again, in all three cases, there is the requirement that 0 ∗ ∆u + u1 = u1 , n ∗ ∆u +
u1 = u2 , 0 ∗ ∆v + v1 = v1 , and m ∗ ∆v + v1 = v2 .
   An evaluation of a single point on the grid may also be carried out:

      void EvalPoint1( int p );

Calling it is equivalent to the command
         EvalCoord1(p * ∆u + u1 );
with ∆u and u1 defined as above.

      void EvalPoint2( int p, int q );

is equivalent to the command
         EvalCoord2(p * ∆u + u1 , q * ∆v + v1 );


    The state required for evaluators potentially consists of 9 one-dimensional map
specifications and 9 two-dimensional map specifications, as well as corresponding
flags for each specification indicating which are enabled. Each map specifica-
tion consists of one or two orders, an appropriately sized array of control points,

                          Version 1.3 - August 14, 2001
5.2. SELECTION                                                                     187


and a set of two values (for a one-dimensional map) or four values (for a two-
dimensional map) to describe the domain. The maximum possible order, for either
u or v, is implementation dependent (one maximum applies to both u and v), but
must be at least 8. Each control point consists of between one and four floating-
point values (depending on the type of the map). Initially, all maps have order
1 (making them constant maps). All vertex coordinate maps produce the coordi-
nates (0, 0, 0, 1) (or the appropriate subset); all normal coordinate maps produce
(0, 0, 1); RGBA maps produce (1, 1, 1, 1); color index maps produce 1.0; texture
coordinate maps produce (0, 0, 0, 1); In the initial state, all maps are disabled.
A flag indicates whether or not automatic normal generation is enabled for two-
dimensional maps. In the initial state, automatic normal generation is disabled.
Also required are two floating-point values and an integer number of grid divisions
for the one-dimensional grid specification and four floating-point values and two
integer grid divisions for the two-dimensional grid specification. In the initial state,
the bounds of the domain interval for 1-D is 0 and 1.0, respectively; for 2-D, they
are (0, 0) and (1.0, 1.0), respectively. The number of grid divisions is 1 for 1-D and
1 in both directions for 2-D. If any evaluation command is issued when no vertex
map is enabled, nothing happens.


5.2    Selection
Selection is used by a programmer to determine which primitives are drawn into
some region of a window. The region is defined by the current model-view and
perspective matrices.
    Selection works by returning an array of integer-valued names. This array
represents the current contents of the name stack. This stack is controlled with the
commands

      void    InitNames( void );
      void    PopName( void );
      void    PushName( uint name );
      void    LoadName( uint name );

InitNames empties (clears) the name stack. PopName pops one name off the top
of the name stack. PushName causes name to be pushed onto the name stack.
LoadName replaces the value on the top of the stack with name. Loading a name
onto an empty stack generates the error INVALID OPERATION. Popping a name off
of an empty stack generates STACK UNDERFLOW; pushing a name onto a full stack
generates STACK OVERFLOW. The maximum allowable depth of the name stack is
implementation dependent but must be at least 64.

                           Version 1.3 - August 14, 2001
188                                         CHAPTER 5. SPECIAL FUNCTIONS


    In selection mode, no fragments are rendered into the framebuffer. The GL is
placed in selection mode with

      int RenderMode( enum mode );

mode is a symbolic constant: one of RENDER, SELECT, or FEEDBACK. RENDER is
the default, corresponding to rendering as described until now. SELECT specifies
selection mode, and FEEDBACK specifies feedback mode (described below). Use
of any of the name stack manipulation commands while the GL is not in selection
mode has no effect.
    Selection is controlled using

      void SelectBuffer( sizei n, uint *buffer );

buffer is a pointer to an array of unsigned integers (called the selection array) to be
potentially filled with names, and n is an integer indicating the maximum number
of values that can be stored in that array. Placing the GL in selection mode before
SelectBuffer has been called results in an error of INVALID OPERATION as does
calling SelectBuffer while in selection mode.
     In selection mode, if a point, line, polygon, or the valid coordinates produced
by a RasterPos command intersects the clip volume (section 2.11) then this primi-
tive (or RasterPos command) causes a selection hit. In the case of polygons, no hit
occurs if the polygon would have been culled, but selection is based on the polygon
itself, regardless of the setting of PolygonMode. When in selection mode, when-
ever a name stack manipulation command is executed or RenderMode is called
and there has been a hit since the last time the stack was manipulated or Render-
Mode was called, then a hit record is written into the selection array.
     A hit record consists of the following items in order: a non-negative integer
giving the number of elements on the name stack at the time of the hit, a minimum
depth value, a maximum depth value, and the name stack with the bottommost el-
ement first. The minimum and maximum depth values are the minimum and max-
imum taken over all the window coordinate z values of each (post-clipping) vertex
of each primitive that intersects the clipping volume since the last hit record was
written. The minimum and maximum (each of which lies in the range [0, 1]) are
each multiplied by 232 −1 and rounded to the nearest unsigned integer to obtain the
values that are placed in the hit record. No depth offset arithmetic (section 3.5.5)
is performed on these values.
     Hit records are placed in the selection array by maintaining a pointer into that
array. When selection mode is entered, the pointer is initialized to the beginning
of the array. Each time a hit record is copied, the pointer is updated to point at

                           Version 1.3 - August 14, 2001
5.3. FEEDBACK                                                                    189


the array element after the one into which the topmost element of the name stack
was stored. If copying the hit record into the selection array would cause the total
number of values to exceed n, then as much of the record as fits in the array is
written and an overflow flag is set.
    Selection mode is exited by calling RenderMode with an argument value other
than SELECT. Whenever RenderMode is called in selection mode, it returns the
number of hit records copied into the selection array and resets the SelectBuffer
pointer to its last specified value. Values are not guaranteed to be written into the
selection array until RenderMode is called. If the selection array overflow flag
was set, then RenderMode returns −1 and clears the overflow flag. The name
stack is cleared and the stack pointer reset whenever RenderMode is called.
    The state required for selection consists of the address of the selection array
and its maximum size, the name stack and its associated pointer, a minimum and
maximum depth value, and several flags. One flag indicates the current Render-
Mode value. In the initial state, the GL is in the RENDER mode. Another flag is
used to indicate whether or not a hit has occurred since the last name stack ma-
nipulation. This flag is reset upon entering selection mode and whenever a name
stack manipulation takes place. One final flag is required to indicate whether the
maximum number of copied names would have been exceeded. This flag is reset
upon entering selection mode. This flag, the address of the selection array, and its
maximum size are GL client state.


5.3    Feedback
Feedback, like selection, is a GL mode. The mode is selected by calling Ren-
derMode with FEEDBACK. When the GL is in feedback mode, no fragments are
written to the framebuffer. Instead, information about primitives that would have
been rasterized is fed back to the application using the GL.
    Feedback is controlled using

      void FeedbackBuffer( sizei n, enum type, float *buffer );

buffer is a pointer to an array of floating-point values into which feedback in-
formation will be placed, and n is a number indicating the maximum number of
values that can be written to that array. type is a symbolic constant describing
the information to be fed back for each vertex (see Figure 5.2). The error IN-
VALID OPERATION results if the GL is placed in feedback mode before a call to
FeedbackBuffer has been made, or if a call to FeedbackBuffer is made while in
feedback mode.

                          Version 1.3 - August 14, 2001
190                                                 CHAPTER 5. SPECIAL FUNCTIONS


     While in feedback mode, each primitive that would be rasterized (or bitmap
or call to DrawPixels or CopyPixels, if the raster position is valid) generates a
block of values that get copied into the feedback array. If doing so would cause
the number of entries to exceed the maximum, the block is partially written so as
to fill the array (if there is any room left at all). The first block of values gener-
ated after the GL enters feedback mode is placed at the beginning of the feedback
array, with subsequent blocks following. Each block begins with a code indicat-
ing the primitive type, followed by values that describe the primitive’s vertices and
associated data. Entries are also written for bitmaps and pixel rectangles. Feed-
back occurs after polygon culling (section 3.5.1) and PolygonMode interpretation
of polygons (section 3.5.4) has taken place. It may also occur after polygons with
more than three edges are broken up into triangles (if the GL implementation ren-
ders polygons by performing this decomposition). x, y, and z coordinates returned
by feedback are window coordinates; if w is returned, it is in clip coordinates. No
depth offset arithmetic (section 3.5.5) is performed on the z values. In the case
of bitmaps and pixel rectangles, the coordinates returned are those of the current
raster position.
     The texture coordinates and colors returned are those resulting from the clip-
ping operations described in Section 2.13.8. Only coordinates for texture unit TEX-
TURE0 are returned even for implementations which support multiple texture units.
The colors returned are the primary colors.
     The ordering rules for GL command interpretation also apply in feedback
mode. Each command must be fully interpreted and its effects on both GL state
and the values to be written to the feedback buffer completed before a subsequent
command may be executed.
     The GL is taken out of feedback mode by calling RenderMode with an ar-
gument value other than FEEDBACK. When called while in feedback mode, Ren-
derMode returns the number of values placed in the feedback array and resets the
feedback array pointer to be buffer. The return value never exceeds the maximum
number of values passed to FeedbackBuffer.
     If writing a value to the feedback buffer would cause more values to be written
than the specified maximum number of values, then the value is not written and an
overflow flag is set. In this case, RenderMode returns −1 when it is called, after
which the overflow flag is reset. While in feedback mode, values are not guaranteed
to be written into the feedback buffer before RenderMode is called.
     Figure 5.2 gives a grammar for the array produced by feedback. Each primitive
is indicated with a unique identifying value followed by some number of vertices.
A vertex is fed back as some number of floating-point values determined by the
feedback type. Table 5.2 gives the correspondence between feedback buffer and
the number of values returned for each vertex.

                               Version 1.3 - August 14, 2001
5.4. DISPLAY LISTS                                                                 191


                Type             coordinates    color   texture   total values
              2D                 x, y           –       –         2
              3D                 x, y, z        –       –         3
           3D COLOR              x, y, z        k       –         3+k
       3D COLOR TEXTURE          x, y, z        k       4         7+k
       4D COLOR TEXTURE          x, y, z, w     k       4         8+k


Table 5.2: Correspondence of feedback type to number of values per vertex. k is 1
in color index mode and 4 in RGBA mode.

    The command

      void PassThrough( float token );

may be used as a marker in feedback mode. token is returned as if it were a prim-
itive; it is indicated with its own unique identifying value. The ordering of any
PassThrough commands with respect to primitive specification is maintained by
feedback. PassThrough may not occur between Begin and End. It has no effect
when the GL is not in feedback mode.
     The state required for feedback is the pointer to the feedback array, the maxi-
mum number of values that may be placed there, and the feedback type. An over-
flow flag is required to indicate whether the maximum allowable number of feed-
back values has been written; initially this flag is cleared. These state variables are
GL client state. Feedback also relies on the same mode flag as selection to indicate
whether the GL is in feedback, selection, or normal rendering mode.


5.4    Display Lists
A display list is simply a group of GL commands and arguments that has been
stored for subsequent execution. The GL may be instructed to process a particular
display list (possibly repeatedly) by providing a number that uniquely specifies it.
Doing so causes the commands within the list to be executed just as if they were
given normally. The only exception pertains to commands that rely upon client
state. When such a command is accumulated into the display list (that is, when
issued, not when executed), the client state in effect at that time applies to the com-
mand. Only server state is affected when the command is executed. As always,
pointers which are passed as arguments to commands are dereferenced when the
command is issued. (Vertex array pointers are dereferenced when the commands

                           Version 1.3 - August 14, 2001
192                                        CHAPTER 5. SPECIAL FUNCTIONS




feedback-list:
      feedback-item feedback-list             pixel-rectangle:
      feedback-item                                     DRAW PIXEL TOKEN vertex
                                                        COPY PIXEL TOKEN vertex
feedback-item:                                passthrough:
      point                                             PASS THROUGH TOKEN f
      line-segment
      polygon                                 vertex:
      bitmap                                  2D:
      pixel-rectangle                                   ff
      passthrough                             3D:
                                                   fff
point:                                        3D COLOR:
         POINT TOKEN vertex                        f f f color
line-segment:                                 3D COLOR TEXTURE:
         LINE TOKEN vertex vertex                       f f f color tex
         LINE RESET TOKEN vertex vertex       4D COLOR TEXTURE:
polygon:                                                f f f f color tex
         POLYGON TOKEN n polygon-spec
polygon-spec:                                 color:
      polygon-spec vertex                               ffff
      vertex vertex vertex                              f
bitmap:
      BITMAP TOKEN vertex                     tex:
                                                        ffff


Figure 5.2: Feedback syntax. f is a floating-point number. n is a floating-point in-
teger giving the number of vertices in a polygon. The symbols ending with TOKEN
are symbolic floating-point constants. The labels under the “vertex” rule show the
different data returned for vertices depending on the feedback type. LINE TOKEN
and LINE RESET TOKEN are identical except that the latter is returned only when
the line stipple is reset for that line segment.




                          Version 1.3 - August 14, 2001
5.4. DISPLAY LISTS                                                                  193


ArrayElement, DrawArrays, DrawElements, or DrawRangeElements are ac-
cumulated into a display list.)
   A display list is begun by calling

      void NewList( uint n, enum mode );

n is a positive integer to which the display list that follows is assigned, and mode is a
symbolic constant that controls the behavior of the GL during display list creation.
If mode is COMPILE, then commands are not executed as they are placed in the
display list. If mode is COMPILE AND EXECUTE then commands are executed as
they are encountered, then placed in the display list. If n = 0, then the error
INVALID VALUE is generated.
     After calling NewList all subsequent GL commands are placed in the display
list (in the order the commands are issued) until a call to

      void EndList( void );

occurs, after which the GL returns to its normal command execution state. It is
only when EndList occurs that the specified display list is actually associated with
the index indicated with NewList. The error INVALID OPERATION is generated
if EndList is called without a previous matching NewList, or if NewList is called
a second time before calling EndList. The error OUT OF MEMORY is generated if
EndList is called and the specified display list cannot be stored because insufficient
memory is available. In this case GL implementations of revision 1.1 or greater
insure that no change is made to the previous contents of the display list, if any,
and that no other change is made to the GL state, except for the state changed by
execution of GL commands when the display list mode is COMPILE AND EXECUTE.
    Once defined, a display list is executed by calling

      void CallList( uint n );

n gives the index of the display list to be called. This causes the commands saved
in the display list to be executed, in order, just as if they were issued without using
a display list. If n = 0, then the error INVALID VALUE is generated.
     The command

      void CallLists( sizei n, enum type, void *lists );

provides an efficient means for executing a number of display lists. n is an integer
indicating the number of display lists to be called, and lists is a pointer that points

                            Version 1.3 - August 14, 2001
194                                           CHAPTER 5. SPECIAL FUNCTIONS


to an array of offsets. Each offset is constructed as determined by lists as fol-
lows. First, type may be one of the constants BYTE, UNSIGNED BYTE, SHORT, UN-
SIGNED SHORT, INT, UNSIGNED INT, or FLOAT indicating that the array pointed
to by lists is an array of bytes, unsigned bytes, shorts, unsigned shorts, integers, un-
signed integers, or floats, respectively. In this case each offset is found by simply
converting each array element to an integer (floating point values are truncated).
Further, type may be one of 2 BYTES, 3 BYTES, or 4 BYTES, indicating that the
array contains sequences of 2, 3, or 4 unsigned bytes, in which case each integer
offset is constructed according to the following algorithm:

of f set ← 0
for i = 1 to b
    of f set ← of f set shifted left 8 bits
    of f set ← of f set + byte
    advance to next byte in the array

b is 2, 3, or 4, as indicated by type. If n = 0, CallLists does nothing.
     Each of the n constructed offsets is taken in order and added to a display list
base to obtain a display list number. For each number, the indicated display list is
executed. The base is set by calling

      void ListBase( uint base );

to specify the offset.
    Indicating a display list index that does not correspond to any display list has no
effect. CallList or CallLists may appear inside a display list. (If the mode supplied
to NewList is COMPILE AND EXECUTE, then the appropriate lists are executed,
but the CallList or CallLists, rather than those lists’ constituent commands, is
placed in the list under construction.) To avoid the possibility of infinite recursion
resulting from display lists calling one another, an implementation dependent limit
is placed on the nesting level of display lists during display list execution. This
limit must be at least 64.
    Two commands are provided to manage display list indices.

      uint GenLists( sizei s );

returns an integer n such that the indices n, . . . , n+s−1 are previously unused (i.e.
there are s previously unused display list indices starting at n). GenLists also has
the effect of creating an empty display list for each of the indices n, . . . , n + s − 1,
so that these indices all become used. GenLists returns 0 if there is no group of s
contiguous previously unused display list indices, or if s = 0.

                            Version 1.3 - August 14, 2001
5.5. FLUSH AND FINISH                                                              195


      boolean IsList( uint list );

returns TRUE if list is the index of some display list.
    A contiguous group of display lists may be deleted by calling

      void DeleteLists( uint list, sizei range );

where list is the index of the first display list to be deleted and range is the number
of display lists to be deleted. All information about the display lists is lost, and the
indices become unused. Indices to which no display list corresponds are ignored.
If range = 0, nothing happens.
     Certain commands, when called while compiling a display list, are
not compiled into the display list but are executed immediately.                  These
are: IsList, GenLists, DeleteLists, FeedbackBuffer, SelectBuffer, Render-
Mode, VertexPointer, NormalPointer, ColorPointer, IndexPointer, TexCoord-
Pointer, ClientActiveTexture, EdgeFlagPointer, InterleavedArrays, Enable-
ClientState, DisableClientState, PushClientAttrib, PopClientAttrib, ReadPix-
els, PixelStore, GenTextures, DeleteTextures, AreTexturesResident, IsTexture,
Flush, Finish, as well as IsEnabled and all of the Get commands (see Chapter 6).
     TexImage3D, TexImage2D, TexImage1D, Histogram, and Col-
orTable are executed immediately when called with the correspond-
ing proxy arguments PROXY TEXTURE 3D, PROXY TEXTURE 2D or
PROXY TEXTURE CUBE MAP,                PROXY TEXTURE 1D,           PROXY HISTOGRAM,
and PROXY COLOR TABLE, PROXY POST CONVOLUTION COLOR TABLE, or
PROXY POST COLOR MATRIX COLOR TABLE.
     Display lists require one bit of state to indicate whether a GL command should
be executed immediately or placed in a display list. In the initial state, commands
are executed immediately. If the bit indicates display list creation, an index is
required to indicate the current display list being defined. Another bit indicates,
during display list creation, whether or not commands should be executed as they
are compiled into the display list. One integer is required for the current ListBase
setting; its initial value is zero. Finally, state must be maintained to indicate which
integers are currently in use as display list indices. In the initial state, no indices
are in use.


5.5    Flush and Finish
The command

      void Flush( void );

                           Version 1.3 - August 14, 2001
196                                        CHAPTER 5. SPECIAL FUNCTIONS


indicates that all commands that have previously been sent to the GL must complete
in finite time.
     The command

      void Finish( void );

forces all previous GL commands to complete. Finish does not return until all
effects from previously issued commands on GL client and server state and the
framebuffer are fully realized.


5.6    Hints
Certain aspects of GL behavior, when there is room for variation, may be controlled
with hints. A hint is specified using

      void Hint( enum target, enum hint );

target is a symbolic constant indicating the behavior to be controlled, and hint
is a symbolic constant indicating what type of behavior is desired. target may
be one of PERSPECTIVE CORRECTION HINT, indicating the desired quality of
parameter interpolation; POINT SMOOTH HINT, indicating the desired sampling
quality of points; LINE SMOOTH HINT, indicating the desired sampling quality of
lines; POLYGON SMOOTH HINT, indicating the desired sampling quality of poly-
gons; FOG HINT, indicating whether fog calculations are done per pixel or per
vertex; and TEXTURE COMPRESSION HINT, indicating the desired quality and per-
formance of compressing texture images. hint must be one of FASTEST, indicating
that the most efficient option should be chosen; NICEST, indicating that the highest
quality option should be chosen; and DONT CARE, indicating no preference in the
matter.
    For the texture compression hint, a hint of FASTEST indicates that texture im-
ages should be compressed as quickly as possible, while NICEST indicates that
the texture images be compressed with as little image degradation as possible.
FASTEST should be used for one-time texture compression, and NICEST should
be used if the compression results are to be retrieved by GetCompressedTexIm-
age (section 6.1.4) for reuse.
    The interpretation of hints is implementation dependent. An implementation
may ignore them entirely.
    The initial value of all hints is DONT CARE.




                          Version 1.3 - August 14, 2001
Chapter 6

State and State Requests

The state required to describe the GL machine is enumerated in section 6.2. Most
state is set through the calls described in previous chapters, and can be queried
using the calls described in section 6.1.


6.1     Querying GL State
6.1.1    Simple Queries
Much of the GL state is completely identified by symbolic constants. The values
of these state variables can be obtained using a set of Get commands. There are
four commands for obtaining simple state variables:

        void   GetBooleanv( enum value, boolean *data );
        void   GetIntegerv( enum value, int *data );
        void   GetFloatv( enum value, float *data );
        void   GetDoublev( enum value, double *data );

The commands obtain boolean, integer, floating-point, or double-precision state
variables. value is a symbolic constant indicating the state variable to return. data
is a pointer to a scalar or array of the indicated type in which to place the returned
data. In addition

        boolean IsEnabled( enum value );

can be used to determine if value is currently enabled (as with Enable) or disabled.

                                         197
198                              CHAPTER 6. STATE AND STATE REQUESTS


6.1.2   Data Conversions
If a Get command is issued that returns value types different from the type of the
value being obtained, a type conversion is performed. If GetBooleanv is called,
a floating-point or integer value converts to FALSE if and only if it is zero (oth-
erwise it converts to TRUE). If GetIntegerv (or any of the Get commands below)
is called, a boolean value is interpreted as either 1 or 0, and a floating-point value
is rounded to the nearest integer, unless the value is an RGBA color component,
a DepthRange value, a depth buffer clear value, or a normal coordinate. In these
cases, the Get command converts the floating-point value to an integer according
the INT entry of Table 4.7; a value not in [−1, 1] converts to an undefined value.
If GetFloatv is called, a boolean value is interpreted as either 1.0 or 0.0, an in-
teger is coerced to floating-point, and a double-precision floating-point value is
converted to single-precision. Analogous conversions are carried out in the case of
GetDoublev. If a value is so large in magnitude that it cannot be represented with
the requested type, then the nearest value representable using the requested type is
returned.
     Unless otherwise indicated, multi-valued state variables return their multiple
values in the same order as they are given as arguments to the commands that set
them. For instance, the two DepthRange parameters are returned in the order n
followed by f. Similarly, points for evaluator maps are returned in the order that
they appeared when passed to Map1. Map2 returns Rij in the [(uorder)i + j]th
block of values (see page 182 for i, j, uorder, and Rij ).
     Matrices may be queried and returned in transposed form by calling Get-
Booleanv, GetIntegerv, GetFloatv, and GetDoublev with pname set to one of
TRANSPOSE MODELVIEW MATRIX, TRANSPOSE PROJECTION MATRIX, TRANS-
POSE TEXTURE MATRIX, or TRANSPOSE COLOR MATRIX. The effect of

         GetFloatv(TRANSPOSE MODELVIEW MATRIX,m);

is the same as the effect of the command sequence

         GetFloatv(MODELVIEW MATRIX,m);
         m = mT ;

   Similar conversions occur when querying TRANSPOSE PROJECTION MATRIX,
TRANSPOSE TEXTURE MATRIX, and TRANSPOSE COLOR MATRIX.
   Most texture state variables are qualified by the value of ACTIVE TEXTURE
to determine which server texture state vector is queried. Client texture
state variables such as texture coordinate array pointers are qualified by the
value of CLIENT ACTIVE TEXTURE. Tables 6.5, 6.6, 6.8, 6.14, 6.17, and 6.28

                           Version 1.3 - August 14, 2001
6.1. QUERYING GL STATE                                                         199


indicate those state variables which are qualified by ACTIVE TEXTURE or
CLIENT ACTIVE TEXTURE during state queries.


6.1.3    Enumerated Queries
Other commands exist to obtain state variables that are identified by a category
(clip plane, light, material, etc.) as well as a symbolic constant. These are

        void GetClipPlane( enum plane, double eqn[4] );
        void GetLight{if}v( enum light, enum value, T data );
        void GetMaterial{if}v( enum face, enum value, T data );
        void GetTexEnv{if}v( enum env, enum value, T data );
        void GetTexGen{if}v( enum coord, enum value, T data );
        void GetTexParameter{if}v( enum target, enum value,
          T data );
        void GetTexLevelParameter{if}v( enum target, int lod,
          enum value, T data );
        void GetPixelMap{ui us f}v( enum map, T data );
        void GetMap{ifd}v( enum map, enum value, T data );

GetClipPlane always returns four double-precision values in eqn; these are the
coefficients of the plane equation of plane in eye coordinates (these coordinates
are those that were computed when the plane was specified).
    GetLight places information about value (a symbolic constant) for light (also a
symbolic constant) in data. POSITION or SPOT DIRECTION returns values in eye
coordinates (again, these are the coordinates that were computed when the position
or direction was specified).
    GetMaterial, GetTexGen, GetTexEnv, and GetTexParameter are similar to
GetLight, placing information about value for the target indicated by their first
argument into data. The face argument to GetMaterial must be either FRONT or
BACK, indicating the front or back material, respectively. The env argument to
GetTexEnv must currently be TEXTURE ENV. The coord argument to GetTexGen
must be one of S, T, R, or Q. For GetTexGen, EYE LINEAR coefficients are re-
turned in the eye coordinates that were computed when the plane was specified;
OBJECT LINEAR coefficients are returned in object coordinates.
    GetTexParameter parameter target may be one of TEXTURE 1D, TEX-
TURE 2D, TEXTURE 3D, or TEXTURE CUBE MAP, indicating the currently bound
one-, two-, three-dimensional, or cube map texture object. GetTexLevelPa-
rameter parameter target may be one of TEXTURE 1D, TEXTURE 2D, TEX-
TURE 3D, TEXTURE CUBE MAP POSITIVE X, TEXTURE CUBE MAP NEGATIVE X,

                          Version 1.3 - August 14, 2001
200                               CHAPTER 6. STATE AND STATE REQUESTS


TEXTURE CUBE MAP POSITIVE Y,          TEXTURE CUBE MAP NEGATIVE Y,
TEXTURE CUBE MAP POSITIVE Z,
TEXTURE CUBE MAP NEGATIVE Z, PROXY TEXTURE 1D, PROXY TEXTURE 2D,
PROXY TEXTURE 3D, or PROXY TEXTURE CUBE MAP, indicating the one-, two-, or
three-dimensional texture object, or one of the six distinct 2D images making up
the cube map texture object or one-, two-, three-dimensional, or cube map proxy
state vector. Note that TEXTURE CUBE MAP is not a valid target parameter for
GetTexLevelParameter, because it does not specify a particular cube map face.
value is a symbolic value indicating which texture parameter is to be obtained. The
lod argument to GetTexLevelParameter determines which level-of-detail’s state
is returned. If the lod argument is less than zero or if it is larger than the maximum
allowable level-of-detail then the error INVALID VALUE occurs.
     For         texture       images           with           uncompressed         in-
ternal formats, queries of value of TEXTURE RED SIZE, TEXTURE GREEN SIZE,
TEXTURE BLUE SIZE, TEXTURE ALPHA SIZE, TEXTURE LUMINANCE SIZE, and
TEXTURE INTENSITY SIZE return the actual resolutions of the stored image array
components, not the resolutions specified when the image array was defined. For
texture images with a compressed internal format, the resolutions returned specify
the component resolution of an uncompressed internal format that produces an im-
age of roughly the same quality as the compressed image in question. Since the
quality of the implementation’s compression algorithm is likely data-dependent,
the returned component sizes should be treated only as rough approximations.
     Querying
value TEXTURE COMPRESSED IMAGE SIZE returns the size (in ubytes) of the
compressed texture image that would be returned by GetCompressedTexImage
(section 6.1.4). Querying TEXTURE COMPRESSED IMAGE SIZE is not allowed on
texture images with an uncompressed internal format or on proxy targets and will
result in an INVALID OPERATION error if attempted.
     Queries of value TEXTURE WIDTH, TEXTURE HEIGHT, TEXTURE DEPTH, and
TEXTURE BORDER return the width, height, depth, and border as specified when
the image array was created. The internal format of the image array is queried
as TEXTURE INTERNAL FORMAT, or as TEXTURE COMPONENTS for compatibility
with GL version 1.0.
     For GetPixelMap, the map must be a map name from Table 3.3. For GetMap,
map must be one of the map types described in section 5.1, and value must be one
of ORDER, COEFF, or DOMAIN.

6.1.4   Texture Queries
The command

                           Version 1.3 - August 14, 2001
6.1. QUERYING GL STATE                                                           201


      void GetTexImage( enum tex, int lod, enum format,
         enum type, void *img );

is used to obtain texture images. It is somewhat different from the other
get commands; tex is a symbolic value indicating which texture (or tex-
ture face in the case of a cube map texture target name) is to be obtained.
TEXTURE 1D, TEXTURE 2D, and TEXTURE 3D indicate a one-, two-, or three-
dimensional texture respectively, while TEXTURE CUBE MAP POSITIVE X, TEX-
TURE CUBE MAP NEGATIVE X,                        TEXTURE CUBE MAP POSITIVE Y,
TEXTURE CUBE MAP NEGATIVE Y, TEXTURE CUBE MAP POSITIVE Z, and TEX-
TURE CUBE MAP NEGATIVE Z indicate the respective face of a cube map texture.
lod is a level-of-detail number, format is a pixel format from Table 3.6, type is a
pixel type from Table 3.5, and img is a pointer to a block of memory.
    GetTexImage obtains component groups from a texture image with the indi-
cated level-of-detail. The components are assigned among R, G, B, and A ac-
cording to Table 6.1, starting with the first group in the first row, and continuing
by obtaining groups in order from each row and proceeding from the first row to
the last, and from the first image to the last for three-dimensional textures. These
groups are then packed and placed in client memory. No pixel transfer operations
are performed on this image, but pixel storage modes that are applicable to Read-
Pixels are applied.
    For three-dimensional textures, pixel storage operations are applied as if the
image were two-dimensional, except that the additional pixel storage state values
PACK IMAGE HEIGHT and PACK SKIP IMAGES are applied. The correspondence
of texels to memory locations is as defined for TexImage3D in section 3.8.1.
    The row length, number of rows, image depth, and number of images are de-
termined by the size of the texture image (including any borders). Calling Get-
TexImage with lod less than zero or larger than the maximum allowable causes
the error INVALID VALUE . Calling GetTexImage with format of COLOR INDEX,
STENCIL INDEX, or DEPTH COMPONENT causes the error INVALID ENUM.
    The command

      void GetCompressedTexImage( enum target, int lod,
         void *img );

is used to obtain texture images stored in compressed form. The parameters target,
lod, and img are interpreted in the same manner as in GetTexImage. When called,
GetCompressedTexImage writes TEXTURE COMPRESSED IMAGE SIZE ubytes
of compressed image data to the memory pointed to by img. The compressed
image data is formatted according to the definition of the texture’s internal format.

                          Version 1.3 - August 14, 2001
202                                CHAPTER 6. STATE AND STATE REQUESTS


                     Base Internal Format        R     G     B     A
                         ALPHA                   0     0     0     Ai
                     LUMINANCE (or 1)            Li    0     0     1
                  LUMINANCE ALPHA (or 2)         Li    0     0     Ai
                       INTENSITY                 Ii    0     0     1
                        RGB (or 3)               Ri    Gi    Bi    1
                       RGBA (or 4)               Ri    Gi    Bi    Ai


Table 6.1: Texture, table, and filter return values. Ri , Gi , Bi , Ai , Li , and Ii are
components of the internal format that are assigned to pixel values R, G, B, and A.
If a requested pixel value is not present in the internal format, the specified constant
value is used.

All pixel storage and pixel transfer modes are ignored when returning a compressed
texture image.
    Calling GetCompressedTexImage with an lod value less than zero or greater
than the maximum allowable causes an INVALID VALUE error. Calling GetCom-
pressedTexImage with a texture image stored with an uncompressed internal for-
mat causes an INVALID OPERATION error.
    The command

        boolean IsTexture( uint texture );

returns TRUE if texture is the name of a texture object. If texture is zero, or is a non-
zero value that is not the name of a texture object, or if an error condition occurs,
IsTexture returns FALSE. A name returned by GenTextures, but not yet bound, is
not the name of a texture object.


6.1.5    Stipple Query
The command

        void GetPolygonStipple( void *pattern );

obtains the polygon stipple. The pattern is packed into memory according to the
procedure given in section 4.3.2 for ReadPixels; it is as if the height and width
passed to that command were both equal to 32, the type were BITMAP, and the
format were COLOR INDEX.

                            Version 1.3 - August 14, 2001
6.1. QUERYING GL STATE                                                          203


6.1.6    Color Matrix Query
The scale and bias variables are queried using GetFloatv with pname set to
the appropriate variable name. The top matrix on the color matrix stack is
returned by GetFloatv called with pname set to COLOR MATRIX or TRANS-
POSE COLOR MATRIX. The depth of the color matrix stack, and the maximum
depth of the color matrix stack, are queried with GetIntegerv, setting pname
to COLOR MATRIX STACK DEPTH and MAX COLOR MATRIX STACK DEPTH respec-
tively.


6.1.7 Color Table Query
The current contents of a color table are queried using


        void GetColorTable( enum target, enum format, enum type,
           void *table );

target must be one of the regular color table names listed in table 3.4. format and
type accept the same values as do the corresponding parameters of GetTexImage.
The one-dimensional color table image is returned to client memory starting at
table. No pixel transfer operations are performed on this image, but pixel storage
modes that are applicable to ReadPixels are performed. Color components that are
requested in the specified format, but which are not included in the internal format
of the color lookup table, are returned as zero. The assignments of internal color
components to the components requested by format are described in Table 6.1.
    The functions


        void GetColorTableParameter{if}v( enum target,
           enum pname, T params );

are used for integer and floating point query.
    target must be one of the regular or proxy color table names listed
in table 3.4. pname is one of COLOR TABLE SCALE, COLOR TABLE BIAS,
COLOR TABLE FORMAT,           COLOR TABLE WIDTH,     COLOR TABLE RED SIZE,
COLOR TABLE GREEN SIZE,                             COLOR TABLE BLUE SIZE,
COLOR TABLE ALPHA SIZE,                        COLOR TABLE LUMINANCE SIZE,
or COLOR TABLE INTENSITY SIZE. The value of the specified parameter is re-
turned in params.

                          Version 1.3 - August 14, 2001
204                             CHAPTER 6. STATE AND STATE REQUESTS


6.1.8     Convolution Query
The current contents of a convolution filter image are queried with the command

        void GetConvolutionFilter( enum target, enum format,
           enum type, void *image );

target must be CONVOLUTION 1D or CONVOLUTION 2D. format and type accept
the same values as do the corresponding parameters of GetTexImage. The one-
dimensional or two-dimensional images is returned to client memory starting at
image. Pixel processing and component mapping are identical to those of GetTex-
Image.
    The current contents of a separable filter image are queried using

        void GetSeparableFilter( enum target, enum format,
           enum type, void *row, void *column, void *span );

target must be SEPARABLE 2D. format and type accept the same values as do the
corresponding parameters of GetTexImage. The row and column images are re-
turned to client memory starting at row and column respectively. span is currently
unused. Pixel processing and component mapping are identical to those of Get-
TexImage.
    The functions

        void GetConvolutionParameter{if}v( enum target,
           enum pname, T params );

are used for integer and floating point query.     target must be CON-
VOLUTION 1D, CONVOLUTION 2D, or SEPARABLE 2D. pname is one of
CONVOLUTION BORDER COLOR,      CONVOLUTION BORDER MODE,         CONVOLU-
TION FILTER SCALE, CONVOLUTION FILTER BIAS, CONVOLUTION FORMAT,
CONVOLUTION WIDTH, CONVOLUTION HEIGHT, MAX CONVOLUTION WIDTH, or
MAX CONVOLUTION HEIGHT. The value of the specified parameter is returned in
params.

6.1.9     Histogram Query
The current contents of the histogram table are queried using

        void GetHistogram( enum target, boolean reset,
           enum format, enum type, void* values );

                          Version 1.3 - August 14, 2001
6.1. QUERYING GL STATE                                                           205


target must be HISTOGRAM. type and format accept the same values as do the corre-
sponding parameters of GetTexImage. The one-dimensional histogram table im-
age is returned to values. Pixel processing and component mapping are identical
to those of GetTexImage.
    If reset is TRUE, then all counters of all elements of the histogram are reset to
zero. Counters are reset whether returned or not.
    No counters are modified if reset is FALSE.
    Calling
      void ResetHistogram( enum target );
resets all counters of all elements of the histogram table to zero. target must be
HISTOGRAM.
    It is not an error to reset or query the contents of a histogram table with zero
entries.
    The functions
      void GetHistogramParameter{if}v( enum target,
         enum pname, T params );
are used for integer and floating point query. target must be HISTOGRAM or
PROXY HISTOGRAM. pname is one of HISTOGRAM FORMAT, HISTOGRAM WIDTH,
HISTOGRAM RED SIZE, HISTOGRAM GREEN SIZE, HISTOGRAM BLUE SIZE,
HISTOGRAM ALPHA SIZE, or HISTOGRAM LUMINANCE SIZE. pname may be
HISTOGRAM SINK only for target HISTOGRAM. The value of the specified
parameter is returned in params.

6.1.10   Minmax Query
The current contents of the minmax table are queried using
      void GetMinmax( enum target, boolean reset, enum format,
         enum type, void* values );
target must be MINMAX. type and format accept the same values as do the corre-
sponding parameters of GetTexImage. A one-dimensional image of width 2 is
returned to values. Pixel processing and component mapping are identical to those
of GetTexImage.
    If reset is TRUE, then each minimum value is reset to the maximum repre-
sentable value, and each maximum value is reset to the minimum representable
value. All values are reset, whether returned or not.
    No values are modified if reset is FALSE.
    Calling

                          Version 1.3 - August 14, 2001
206                             CHAPTER 6. STATE AND STATE REQUESTS


      void ResetMinmax( enum target );

resets all minimum and maximum values of target to to their maximum and mini-
mum representable values, respectively, target must be MINMAX.
    The functions

      void GetMinmaxParameter{if}v( enum target, enum pname,
         T params );

are used for integer and floating point query. target must be MINMAX. pname is
MINMAX FORMAT or MINMAX SINK. The value of the specified parameter is re-
turned in params.

6.1.11   Pointer and String Queries
The command

      void GetPointerv( enum pname, void **params );

    obtains the pointer or pointers named pname in the array params.
The possible values for pname are SELECTION BUFFER POINTER, FEED-
BACK BUFFER POINTER,             VERTEX ARRAY POINTER,         NOR-
MAL ARRAY POINTER, COLOR ARRAY POINTER, INDEX ARRAY POINTER, TEX-
TURE COORD ARRAY POINTER, and EDGE FLAG ARRAY POINTER. Each returns a
single pointer value.
    Finally,

      ubyte *GetString( enum name );

returns a pointer to a static string describing some aspect of the current GL con-
nection. The possible values for name are VENDOR, RENDERER, VERSION, and EX-
TENSIONS. The format of the RENDERER and VERSION strings is implementation
dependent. The EXTENSIONS string contains a space separated list of extension
names (The extension names themselves do not contain any spaces); the VERSION
string is laid out as follows:

      <version number><space><vendor-specific information>

The version number is either of the form major number.minor number or ma-
jor number.minor number.release number, where the numbers all have one or
more digits. The vendor specific information is optional. However, if it is present

                          Version 1.3 - August 14, 2001
6.1. QUERYING GL STATE                                                            207


then it pertains to the server and the format and contents are implementation de-
pendent.
    GetString returns the version number (returned in the VERSION string) and
the extension names (returned in the EXTENSIONS string) that can be supported
on the connection. Thus, if the client and server support different versions and/or
extensions, a compatible version and list of extensions is returned.

6.1.12    Saving and Restoring State
Besides providing a means to obtain the values of state variables, the GL also
provides a means to save and restore groups of state variables. The PushAttrib,
PushClientAttrib, PopAttrib and PopClientAttrib commands are used for this
purpose. The commands

      void PushAttrib( bitfield mask );
      void PushClientAttrib( bitfield mask );

take a bitwise OR of symbolic constants indicating which groups of state variables
to push onto an attribute stack. PushAttrib uses a server attribute stack while
PushClientAttrib uses a client attribute stack. Each constant refers to a group
of state variables. The classification of each variable into a group is indicated
in the following tables of state variables. The error STACK OVERFLOW is gener-
ated if PushAttrib or PushClientAttrib is executed while the corresponding stack
depth is MAX ATTRIB STACK DEPTH or MAX CLIENT ATTRIB STACK DEPTH re-
spectively. Bits set in mask that do not correspond to an attribute group are ignored.
The special mask values ALL ATTRIB BITS and CLIENT ALL ATTRIB BITS may
be used to push all stackable server and client state, respectively.
    The commands

      void PopAttrib( void );
      void PopClientAttrib( void );

reset the values of those state variables that were saved with the last corresponding
PushAttrib or PopClientAttrib. Those not saved remain unchanged. The er-
ror STACK UNDERFLOW is generated if PopAttrib or PopClientAttrib is executed
while the respective stack is empty.
    Table 6.2 shows the attribute groups with their corresponding symbolic con-
stant names and stacks.
    When PushAttrib is called with TEXTURE BIT set, the priorities, border col-
ors, filter modes, and wrap modes of the currently bound texture objects, as well
as the current texture bindings and enables, are pushed onto the attribute stack.

                           Version 1.3 - August 14, 2001
208                      CHAPTER 6. STATE AND STATE REQUESTS




      Stack        Attribute              Constant
      server    accum-buffer         ACCUM BUFFER BIT
      server     color-buffer        COLOR BUFFER BIT
      server        current              CURRENT BIT
      server    depth-buffer         DEPTH BUFFER BIT
      server        enable               ENABLE BIT
      server          eval                 EVAL BIT
      server          fog                   FOG BIT
      server          hint                 HINT BIT
      server       lighting             LIGHTING BIT
      server          line                 LINE BIT
      server          list                 LIST BIT
      server     multisample         MULTISAMPLE BIT
      server         pixel             PIXEL MODE BIT
      server         point                POINT BIT
      server       polygon               POLYGON BIT
      server   polygon-stipple     POLYGON STIPPLE BIT
      server        scissor              SCISSOR BIT
      server    stencil-buffer      STENCIL BUFFER BIT
      server        texture              TEXTURE BIT
      server      transform            TRANSFORM BIT
      server       viewport             VIEWPORT BIT
      server                          ALL ATTRIB BITS
      client    vertex-array     CLIENT VERTEX ARRAY BIT
      client     pixel-store      CLIENT PIXEL STORE BIT
      client        select        can’t be pushed or pop’d
      client      feedback        can’t be pushed or pop’d
      client                     CLIENT ALL ATTRIB BITS


                    Table 6.2: Attribute groups




                   Version 1.3 - August 14, 2001
6.2. STATE TABLES                                                                  209


(Unbound texture objects are not pushed or restored.) When an attribute set that
includes texture information is popped, the bindings and enables are first restored
to their pushed values, then the bound texture objects’ priorities, border colors,
filter modes, and wrap modes are restored to their pushed values.
     Operations on attribute groups push or pop texture state within that group for
all texture units. When state for a group is pushed, all state corresponding to TEX-
TURE0 is pushed first, followed by state corresponding to TEXTURE1, and so on up
to and including the state corresponding to TEXTUREk where k + 1 is the value of
MAX TEXTURE UNITS. When state for a group is popped, texture state is restored
in the opposite order that it was pushed, starting with state corresponding to TEX-
TUREk and ending with TEXTURE0. Identical rules are observed for client texture
state push and pop operations. Matrix stacks are never pushed or popped with
PushAttrib, PushClientAttrib, PopAttrib, or PopClientAttrib.
     The depth of each attribute stack is implementation dependent but must be at
least 16. The state required for each attribute stack is potentially 16 copies of each
state variable, 16 masks indicating which groups of variables are stored in each
stack entry, and an attribute stack pointer. In the initial state, both attribute stacks
are empty.
     In the tables that follow, a type is indicated for each variable. Table 6.3 ex-
plains these types. The type actually identifies all state associated with the indi-
cated description; in certain cases only a portion of this state is returned. This
is the case with all matrices, where only the top entry on the stack is returned;
with clip planes, where only the selected clip plane is returned, with parameters
describing lights, where only the value pertaining to the selected light is returned;
with textures, where only the selected texture or texture parameter is returned; and
with evaluator maps, where only the selected map is returned. Finally, a “–” in the
attribute column indicates that the indicated value is not included in any attribute
group (and thus can not be pushed or popped with PushAttrib, PushClientAttrib,
PopAttrib, or PopClientAttrib).
     The M and m entries for initial minmax table values represent the maximum
and minimum possible representable values, respectively.


6.2    State Tables
The tables on the following pages indicate which state variables are obtained with
what commands. State variables that can be obtained using any of GetBooleanv,
GetIntegerv, GetFloatv, or GetDoublev are listed with just one of these com-
mands – the one that is most appropriate given the type of the data to be returned.
These state variables cannot be obtained using IsEnabled. However, state vari-

                           Version 1.3 - August 14, 2001
210                        CHAPTER 6. STATE AND STATE REQUESTS




      Type code   Explanation
         B        Boolean
         C        Color (floating-point R, G, B, and A values)
         CI       Color index (floating-point index value)
         T        Texture coordinates (floating-point s, t, r, q val-
                  ues)
         N        Normal coordinates (floating-point x, y, z values)
         V        Vertex, including associated data
         Z        Integer
         Z+       Non-negative integer
      Zk , Zk∗    k-valued integer (k∗ indicates k is minimum)
         R        Floating-point number
         R+       Non-negative floating-point number
        R[a,b]    Floating-point number in the range [a, b]
         Rk       k-tuple of floating-point numbers
         P        Position (x, y, z, w floating-point coordinates)
         D        Direction (x, y, z floating-point coordinates)
        M4        4 × 4 floating-point matrix
          I       Image
         A        Attribute stack entry, including mask
         Y        Pointer (data type unspecified)
      n × type    n copies of type type (n∗ indicates n is minimum)


                     Table 6.3: State variable types




                     Version 1.3 - August 14, 2001
6.2. STATE TABLES                                                          211


ables for which IsEnabled is listed as the query command can also be obtained
using GetBooleanv, GetIntegerv, GetFloatv, and GetDoublev. State variables
for which any other command is listed as the query command can be obtained only
by using that command.
    State table entries which are required only by the imaging subset (see sec-
tion 3.6.2) are typeset against a gray background .




                         Version 1.3 - August 14, 2001
                                                                                                                                                                                                  212




                                                                                                                     Get    Initial
                                                                                                  Get value   Type   Cmnd   Value                   Description               Sec.    Attribute
                                                                                                  –           Z11      –      0       When = 0, indicates begin/end           2.6.1       –
                                                                                                                                      object
                                                                                                  –            V      –       –       Previous vertex in Begin/End line       2.6.1      –
                                                                                                  –            B      –       –       Indicates if line-vertex is the first   2.6.1      –
                                                                                                  –            V      –       –       First vertex of a Begin/End line        2.6.1      –
                                                                                                                                      loop
                                                                                                  –            Z+     –       –       Line stipple counter                     3.4       –
                                                                                                  –           n×V     –       –       Vertices inside of Begin/End            2.6.1      –
                                                                                                                                      polygon
                                                                                                  –            Z+     –       –       Number of polygon-vertices              2.6.1      –
                                                                                                  –           2×V     –       –       Previous two vertices in a              2.6.1      –
                                                                                                                                      Begin/End triangle strip
                                                                                                  –           Z3      –       –       Number of vertices so far in            2.6.1      –
                                                                                                                                      triangle strip: 0, 1, or more




Version 1.3 - August 14, 2001
                                                                                                  –            Z2     –       –       Triangle strip A/B vertex pointer       2.6.1      –
                                                                                                  –           3×V     –       –       Vertices of the quad under              2.6.1      –
                                                                                                                                      construction
                                                                                                  –           Z4      –       –       Number of vertices so far in quad       2.6.1      –
                                                                                                                                      strip: 0, 1, 2, or more




                                Table 6.4. GL Internal begin-end state variables (inaccessible)
                                                                                                                                                                                                  CHAPTER 6. STATE AND STATE REQUESTS
                                                                                                                            Get         Initial
                                                                                            Get value            Type       Cmnd        Value                 Description               Sec.    Attribute
                                                                                                                         GetIntegerv,
                                                                                CURRENT COLOR                     C      GetFloatv      1,1,1,1   Current color                         2.7     current
                                                                                                                         GetIntegerv,
                                                                                CURRENT INDEX                     CI     GetFloatv         1      Current color index                   2.7     current
                                                                                                                                                                                                            6.2. STATE TABLES




                                                                                CURRENT TEXTURE COORDS          2 ∗ ×T    GetFloatv     0,0,0,1   Current texture coordinates           2.7     current
                                                                                CURRENT NORMAL                     N      GetFloatv      0,0,1    Current normal                        2.7     current
                                                                                –                                  C          –            -      Color associated with last vertex     2.6        –
                                                                                –                                 CI          –            -      Color index associated with last      2.6        –
                                                                                                                                                  vertex
                                                                                –                                 T           –            -      Texture coordinates associated with   2.6        –
                                                                                                                                                  last vertex
                                                                                CURRENT RASTER POSITION          R4       GetFloatv     0,0,0,1   Current raster position               2.12    current
                                                                                CURRENT RASTER DISTANCE          R+       GetFloatv        0      Current raster distance               2.12    current
                                                                                                                         GetIntegerv,
                                                                                CURRENT RASTER COLOR              C      GetFloatv      1,1,1,1   Color associated with raster          2.12    current
                                                                                                                                                  position




Version 1.3 - August 14, 2001
                                                                                                                         GetIntegerv,
                                                                                CURRENT RASTER INDEX             CI      GetFloatv        1       Color index associated with raster    2.12    current
                                                                                                                                                  position
                                                                                CURRENT RASTER TEXTURE COORDS   2 ∗ ×T    GetFloatv     0,0,0,1   Texture coordinates associated with   2.12    current




                                Table 6.5. Current Values and Associated Data
                                                                                                                                                  raster position
                                                                                CURRENT RASTER POSITION VALID     B      GetBooleanv     True     Raster position valid bit             2.12    current
                                                                                EDGE FLAG                         B      GetBooleanv     True     Edge flag                             2.6.2   current
                                                                                                                                                                                                            213
                                                                                                                                                                                     214




                                                                                                 Get           Initial
                                                                   Get value           Type      Cmnd          Value                  Description              Sec.    Attribute
                                                               CLIENT ACTIVE TEXTURE   Z2∗    GetIntegerv   TEXTURE0     Client active texture unit selector   2.7    vertex-array
                                                               VERTEX ARRAY             B      IsEnabled       False     Vertex array enable                   2.8    vertex-array
                                                               VERTEX ARRAY SIZE       Z+     GetIntegerv        4       Coordinates per vertex                2.8    vertex-array
                                                               VERTEX ARRAY TYPE        Z4    GetIntegerv     FLOAT      Type of vertex coordinates            2.8    vertex-array
                                                               VERTEX ARRAY STRIDE     Z+     GetIntegerv        0       Stride between vertices               2.8    vertex-array
                                                               VERTEX ARRAY POINTER     Y     GetPointerv        0       Pointer to the vertex array           2.8    vertex-array
                                                               NORMAL ARRAY             B      IsEnabled       False     Normal array enable                   2.8    vertex-array
                                                               NORMAL ARRAY TYPE        Z5    GetIntegerv     FLOAT      Type of normal coordinates            2.8    vertex-array
                                                               NORMAL ARRAY STRIDE     Z+     GetIntegerv        0       Stride between normals                2.8    vertex-array
                                                               NORMAL ARRAY POINTER     Y     GetPointerv        0       Pointer to the normal array           2.8    vertex-array
                                                               COLOR ARRAY              B      IsEnabled       False     Color array enable                    2.8    vertex-array
                                                               COLOR ARRAY SIZE        Z+     GetIntegerv        4       Colors per vertex                     2.8    vertex-array
                                                               COLOR ARRAY TYPE         Z8    GetIntegerv     FLOAT      Type of color components              2.8    vertex-array
                                                               COLOR ARRAY STRIDE      Z+     GetIntegerv        0       Stride between colors                 2.8    vertex-array




Version 1.3 - August 14, 2001
                                Table 6.6. Vertex Array Data
                                                               COLOR ARRAY POINTER      Y     GetPointerv        0       Pointer to the color array            2.8    vertex-array
                                                               INDEX ARRAY              B      IsEnabled       False     Index array enable                    2.8    vertex-array
                                                               INDEX ARRAY TYPE         Z4    GetIntegerv     FLOAT      Type of indices                       2.8    vertex-array
                                                               INDEX ARRAY STRIDE      Z+     GetIntegerv        0       Stride between indices                2.8    vertex-array
                                                               INDEX ARRAY POINTER      Y     GetPointerv        0       Pointer to the index array            2.8    vertex-array
                                                                                                                                                                                     CHAPTER 6. STATE AND STATE REQUESTS
                                                                                                                                                                                                    6.2. STATE TABLES




                                                                                                                   Get         Initial
                                                                               Get value               Type        Cmnd        Value                  Description             Sec.    Attribute
                                                                       TEXTURE COORD ARRAY            2 ∗ ×B     IsEnabled     False     Texture coordinate array enable      2.8    vertex-array
                                                                       TEXTURE COORD ARRAY SIZE      2 ∗ ×Z +   GetIntegerv      4       Coordinates per element              2.8    vertex-array
                                                                       TEXTURE COORD ARRAY TYPE      2 ∗ ×Z4    GetIntegerv   FLOAT      Type of texture coordinates          2.8    vertex-array
                                                                       TEXTURE COORD ARRAY STRIDE    2 ∗ ×Z +   GetIntegerv      0       Stride between texture coordinates   2.8    vertex-array
                                                                       TEXTURE COORD ARRAY POINTER    2 ∗ ×Y    GetPointerv      0       Pointer to the texture coordinate    2.8    vertex-array
                                                                                                                                         array
                                                                       EDGE FLAG ARRAY                 B         IsEnabled     False     Edge flag array enable               2.8    vertex-array
                                                                       EDGE FLAG ARRAY STRIDE          Z+       GetIntegerv      0       Stride between edge flags            2.8    vertex-array
                                                                       EDGE FLAG ARRAY POINTER         Y        GetPointerv      0       Pointer to the edge flag array       2.8    vertex-array




Version 1.3 - August 14, 2001
                                Table 6.7. Vertex Array Data (cont.)
                                                                                                                                                                                                    215
                                                                                                        Get             Initial
                                                                                                                                                                                          216




                                                                    Get value             Type          Cmnd            Value            Description          Sec.        Attribute
                                                      COLOR MATRIX                      2 ∗ ×M 4       GetFloatv       Identity    Color matrix stack         3.6.3           –
                                                      (TRANSPOSE COLOR MATRIX)

                                                      MODELVIEW MATRIX                 32 ∗ ×M 4       GetFloatv       Identity    Model-view matrix stack    2.10.2          –
                                                      (TRANSPOSE MODELVIEW MATRIX)

                                                      PROJECTION MATRIX                 2 ∗ ×M 4       GetFloatv       Identity    Projection matrix stack    2.10.2          –
                                                      (TRANSPOSE PROJECTION MATRIX)

                                                      TEXTURE MATRIX                  2 ∗ ×2 ∗ ×M 4    GetFloatv       Identity    Texture matrix stack       2.10.2          –
                                                      (TRANSPOSE TEXTURE MATRIX)

                                                      VIEWPORT                            4×Z         GetIntegerv     see 2.10.1   Viewport origin & extent   2.10.1      viewport
                                                      DEPTH RANGE                        2 × R+        GetFloatv         0,1       Depth range near & far     2.10.1      viewport
                                                      COLOR MATRIX STACK DEPTH             Z+         GetIntegerv         1        Color matrix stack         3.6.3          –
                                                                                                                                   pointer
                                                      MODELVIEW STACK DEPTH               Z+          GetIntegerv         1        Model-view matrix stack    2.10.2          –
                                                                                                                                   pointer
                                                      PROJECTION STACK DEPTH              Z+          GetIntegerv         1        Projection matrix stack    2.10.2          –
                                                                                                                                   pointer
                                                      TEXTURE STACK DEPTH               2 ∗ ×Z +      GetIntegerv         1        Texture matrix stack       2.10.2          –
                                                                                                                                   pointer




                                  Version 1.3 - August 14, 2001

Table 6.8. Transformation state
                                                      MATRIX MODE                          Z4         GetIntegerv    MODELVIEW     Current matrix mode        2.10.2       transform
                                                      NORMALIZE                            B           IsEnabled        False      Current normal             2.10.3   transform/enable
                                                                                                                                   normalization on/off
                                                      RESCALE NORMAL                       B           IsEnabled        False      Current normal rescaling   2.10.3   transform/enable
                                                                                                                                   on/off
                                                      CLIP PLANEi                       6 ∗ ×R4       GetClipPlane     0,0,0,0     User clipping plane        2.11        transform
                                                                                                                                   coefficients
                                                      CLIP PLANEi                        6 ∗ ×B        IsEnabled        False      ith user clipping plane    2.11     transform/enable
                                                                                                                                   enabled
                                                                                                                                                                                          CHAPTER 6. STATE AND STATE REQUESTS
                                                                                                                                                     6.2. STATE TABLES




                                                                              Get         Initial
                                                      Get value     Type      Cmnd        Value                  Description    Sec.     Attribute
                                                      FOG COLOR      C      GetFloatv     0,0,0,0   Fog color                   3.10        fog
                                                      FOG INDEX      CI     GetFloatv        0      Fog index                   3.10        fog
                                                      FOG DENSITY    R      GetFloatv       1.0     Exponential fog density     3.10        fog
                                                      FOG START      R      GetFloatv       0.0     Linear fog start            3.10        fog
                                                      FOG END        R      GetFloatv       1.0     Linear fog end              3.10        fog
                                                      FOG MODE       Z3    GetIntegerv     EXP      Fog mode                    3.10        fog
                                                      FOG            B      IsEnabled      False    True if fog enabled         3.10    fog/enable




                                Table 6.9. Coloring
                                                      SHADE MODEL   Z+     GetIntegerv   SMOOTH     ShadeModel setting         2.13.7    lighting




Version 1.3 - August 14, 2001
                                                                                                                                                     217
                                                                                                                 Get                  Initial
                                                                                                                                                                                                      218




                                                                                     Get value         Type      Cmnd                 Value              Description        Sec.       Attribute
                                                                           LIGHTING                     B      IsEnabled              False          True if lighting is   2.13.1   lighting/enable
                                                                                                                                                     enabled
                                                                           COLOR MATERIAL               B      IsEnabled              False          True if color         2.13.3   lighting/enable
                                                                                                                                                     tracking is
                                                                                                                                                     enabled
                                                                           COLOR MATERIAL PARAMETER    Z5      GetIntegerv    AMBIENT AND DIFFUSE    Material              2.13.3      lighting
                                                                                                                                                     properties
                                                                                                                                                     tracking current
                                                                                                                                                     color
                                                                           COLOR MATERIAL FACE         Z3      GetIntegerv      FRONT AND BACK       Face(s) affected      2.13.3      lighting
                                                                                                                                                     by color tracking
                                                                           AMBIENT                     2×C    GetMaterialfv      (0.2,0.2,0.2,1.0)   Ambient material      2.13.1      lighting
                                                                                                                                                     color
                                                                           DIFFUSE                     2×C    GetMaterialfv      (0.8,0.8,0.8,1.0)   Diffuse material      2.13.1      lighting
                                                                                                                                                     color
                                                                           SPECULAR                    2×C    GetMaterialfv      (0.0,0.0,0.0,1.0)   Specular material     2.13.1      lighting
                                                                                                                                                     color
                                                                           EMISSION                    2×C    GetMaterialfv      (0.0,0.0,0.0,1.0)   Emissive mat.         2.13.1      lighting




                                           Version 1.3 - August 14, 2001
                                                                                                                                                     color
                                                                           SHININESS                   2×R    GetMaterialfv            0.0           Specular              2.13.1      lighting
                                                                                                                                                     exponent of
                                                                                                                                                     material
                                                                           LIGHT MODEL AMBIENT          C      GetFloatv         (0.2,0.2,0.2,1.0)   Ambient scene         2.13.1      lighting




Table 6.10. Lighting (see also Table 2.7 for defaults)
                                                                                                                                                     color
                                                                           LIGHT MODEL LOCAL VIEWER     B     GetBooleanv             False          Viewer is local       2.13.1      lighting
                                                                           LIGHT MODEL TWO SIDE         B     GetBooleanv             False          Use two-sided         2.13.1      lighting
                                                                                                                                                     lighting
                                                                           LIGHT MODEL COLOR CONTROL   Z2      GetIntegerv       SINGLE COLOR        Color control         2.13.1      lighting
                                                                                                                                                                                                      CHAPTER 6. STATE AND STATE REQUESTS
                                                                                                                                                                                                   6.2. STATE TABLES




                                                                                                    Get                Initial
                                                                    Get value            Type       Cmnd               Value                      Description            Sec.       Attribute
                                                               AMBIENT                  8 ∗ ×C    GetLightfv     (0.0,0.0,0.0,1.0)   Ambient intensity of light i       2.13.1       lighting
                                                               DIFFUSE                  8 ∗ ×C    GetLightfv          see 2.5        Diffuse intensity of light i       2.13.1       lighting
                                                               SPECULAR                 8 ∗ ×C    GetLightfv          see 2.5        Specular intensity of light i      2.13.1       lighting
                                                               POSITION                 8 ∗ ×P    GetLightfv     (0.0,0.0,1.0,0.0)   Position of light i                2.13.1       lighting
                                                               CONSTANT ATTENUATION    8 ∗ ×R+    GetLightfv             1.0         Constant atten. factor             2.13.1       lighting
                                                               LINEAR ATTENUATION      8 ∗ ×R+    GetLightfv             0.0         Linear atten. factor               2.13.1       lighting
                                                               QUADRATIC ATTENUATION   8 ∗ ×R+    GetLightfv             0.0         Quadratic atten. factor            2.13.1       lighting
                                                               SPOT DIRECTION           8 ∗ ×D    GetLightfv       (0.0,0.0,-1.0)    Spotlight direction of light i     2.13.1       lighting
                                                               SPOT EXPONENT           8 ∗ ×R+    GetLightfv             0.0         Spotlight exponent of light i      2.13.1       lighting
                                                               SPOT CUTOFF             8 ∗ ×R+    GetLightfv           180.0         Spot. angle of light i             2.13.1       lighting
                                                               LIGHTi                             IsEnabled            False         True if light i enabled            2.13.1   lighting/enable




Table 6.11. Lighting (cont.)
                                                                                        8 ∗ ×B




                               Version 1.3 - August 14, 2001
                                                               COLOR INDEXES           2×3×R     GetMaterialfv          0,1,1        am , dm , and sm for color index   2.13.1       lighting
                                                                                                                                     lighting
                                                                                                                                                                                                   219
                                                                                                                                                                                         220




                                                                                                   Get           Initial
                                                                 Get value          Type           Cmnd          Value                  Description            Sec.        Attribute
                                                            POINT SIZE              R+           GetFloatv        1.0      Point size                           3.3         point
                                                            POINT SMOOTH             B           IsEnabled       False     Point antialiasing on                3.3     point/enable
                                                            LINE WIDTH              R+           GetFloatv        1.0      Line width                           3.4          line
                                                            LINE SMOOTH              B           IsEnabled       False     Line antialiasing on                 3.4      line/enable
                                                            LINE STIPPLE PATTERN    Z+          GetIntegerv        1’s     Line stipple                        3.4.2         line
                                                            LINE STIPPLE REPEAT     Z+          GetIntegerv         1      Line stipple repeat                 3.4.2         line
                                                            LINE STIPPLE             B           IsEnabled       False     Line stipple enable                 3.4.2     line/enable
                                                            CULL FACE                B           IsEnabled       False     Polygon culling enabled             3.5.1   polygon/enable
                                                            CULL FACE MODE           Z3         GetIntegerv      BACK      Cull front/back facing polygons     3.5.1       polygon
                                                            FRONT FACE               Z2         GetIntegerv       CCW      Polygon frontface CW/CCW            3.5.1       polygon
                                                                                                                           indicator
                                                            POLYGON SMOOTH            B          IsEnabled       False     Polygon antialiasing on              3.5    polygon/enable
                                                            POLYGON MODE            2 × Z3      GetIntegerv      FILL      Polygon rasterization mode (front   3.5.4      polygon
                                                                                                                           & back)
                                                            POLYGON OFFSET FACTOR     R         GetFloatv          0       Polygon offset factor               3.5.5      polygon
                                                            POLYGON OFFSET UNITS      R         GetFloatv          0       Polygon offset units                3.5.5      polygon




                                Table 6.12. Rasterization
Version 1.3 - August 14, 2001
                                                            POLYGON OFFSET POINT      B         IsEnabled        False     Polygon offset enable for POINT     3.5.5   polygon/enable
                                                                                                                           mode rasterization
                                                            POLYGON OFFSET LINE       B         IsEnabled        False     Polygon offset enable for LINE      3.5.5   polygon/enable
                                                                                                                           mode rasterization
                                                            POLYGON OFFSET FILL       B         IsEnabled        False     Polygon offset enable for FILL      3.5.5   polygon/enable
                                                                                                                           mode rasterization
                                                            –                         I      GetPolygonStipple    1’s      Polygon stipple                      3.5    polygon-stipple
                                                            POLYGON STIPPLE           B         IsEnabled        False     Polygon stipple enable              3.5.2   polygon/enable
                                                                                                                                                                                         CHAPTER 6. STATE AND STATE REQUESTS
                                                                                                                                                                                6.2. STATE TABLES




                                                                                                 Get        Initial
                                                                  Get value            Type      Cmnd       Value                  Description     Sec.         Attribute
                                                            MULTISAMPLE                 B      IsEnabled     True     Multisample rasterization    3.2.1   multisample/enable
                                                            SAMPLE ALPHA TO COVERAGE    B      IsEnabled    False     Modify coverage from alpha   4.1.3   multisample/enable
                                                            SAMPLE ALPHA TO ONE         B      IsEnabled    False     Set alpha to maximum         4.1.3   multisample/enable
                                                            SAMPLE COVERAGE             B      IsEnabled    False     Mask to modify coverage      4.1.3   multisample/enable
                                                            SAMPLE COVERAGE VALUE      R+      GetFloatv      1       Coverage mask value          4.1.3      multisample
                                                            SAMPLE COVERAGE INVERT      B     GetBooleanv   False     Invert coverage mask value   4.1.3      multisample




                                Table 6.13. Multisampling
Version 1.3 - August 14, 2001
                                                                                                                                                                                221
                                                                                                                                                                                           222




                                                                                                              Get         Initial
                                                                           Get value            Type          Cmnd        Value               Description         Sec.       Attribute
                                                              TEXTURE xD                    2 ∗ ×3 × B      IsEnabled     False      True if xD texturing is     3.8.13   texture/enable
                                                                                                                                     enabled; x is 1, 2, or 3
                                                              TEXTURE CUBE MAP                2 ∗ ×B        IsEnabled     False      True if cube map            3.8.12   texture/enable
                                                                                                                                     texturing is enabled
                                                              TEXTURE BINDING xD            2 ∗ ×3 × Z +   GetIntegerv      0        Texture object bound to     3.8.11      texture
                                                                                                                                     TEXTURE xD
                                                              TEXTURE BINDING CUBE MAP       2 ∗ ×Z +      GetIntegerv      0        Texture object bound to     3.8.10      texture
                                                                                                                                     TEXTURE CUBE MAP
                                                              TEXTURE xD                       n×I         GetTexImage   see 3.8     xD texture image at          3.8           –
                                                                                                                                     l.o.d. i
                                                              TEXTURE CUBE MAP POSITIVE X      n×I         GetTexImage   see 3.8.1   +x face cube map            3.8.1          –
                                                                                                                                     texture image at l.o.d. i
                                                              TEXTURE CUBE MAP NEGATIVE X      n×I         GetTexImage   see 3.8.1   −x face cube map            3.8.1          –
                                                                                                                                     texture image at l.o.d. i
                                                              TEXTURE CUBE MAP POSITIVE Y      n×I         GetTexImage   see 3.8.1   +y face cube map            3.8.1          –




                                Table 6.14. Texture Objects
Version 1.3 - August 14, 2001
                                                                                                                                     texture image at l.o.d. i
                                                              TEXTURE CUBE MAP NEGATIVE Y      n×I         GetTexImage   see 3.8.1   −y face cube map            3.8.1          –
                                                                                                                                     texture image at l.o.d. i
                                                              TEXTURE CUBE MAP POSITIVE Z      n×I         GetTexImage   see 3.8.1   +z face cube map            3.8.1          –
                                                                                                                                     texture image at l.o.d. i
                                                              TEXTURE CUBE MAP NEGATIVE Z      n×I         GetTexImage   see 3.8.1   −z face cube map            3.8.1          –
                                                                                                                                     texture image at l.o.d. i
                                                                                                                                                                                           CHAPTER 6. STATE AND STATE REQUESTS
                                                                                                                  Get             Initial
                                                                                 Get value       Type             Cmnd            Value            Description          Sec.   Attribute
                                                                      TEXTURE WIDTH             n × Z+     GetTexLevelParameter     0       texture image’s specified   3.8        –
                                                                                                                                            width
                                                                      TEXTURE HEIGHT            n × Z+     GetTexLevelParameter     0       2D/3D texture image’s       3.8       –
                                                                                                                                                                                           6.2. STATE TABLES




                                                                                                                                            specified height
                                                                      TEXTURE DEPTH             n × Z+     GetTexLevelParameter     0       3D texture image’s          3.8       –
                                                                                                                                            specified depth
                                                                      TEXTURE BORDER            n × Z+     GetTexLevelParameter     0       texture image’s specified   3.8       –
                                                                                                                                            border width
                                                                      TEXTURE INTERNAL FORMAT   n × Z42∗   GetTexLevelParameter     1       texture image’s internal    3.8       –
                                                                      (TEXTURE COMPONENTS)                                                  image format
                                                                      TEXTURE RED SIZE          n × Z+     GetTexLevelParameter     0       texture image’s red         3.8       –
                                                                                                                                            resolution
                                                                      TEXTURE GREEN SIZE        n × Z+     GetTexLevelParameter     0       texture image’s green       3.8       –
                                                                                                                                            resolution
                                                                      TEXTURE BLUE SIZE         n × Z+     GetTexLevelParameter     0       texture image’s blue        3.8       –




Version 1.3 - August 14, 2001
                                                                                                                                            resolution
                                                                      TEXTURE ALPHA SIZE                   GetTexLevelParameter     0       texture image’s alpha       3.8       –




                                Table 6.15. Texture Objects (cont.)
                                                                                                n × Z+
                                                                                                                                            resolution
                                                                      TEXTURE LUMINANCE SIZE    n × Z+     GetTexLevelParameter     0       texture image’s             3.8       –
                                                                                                                                            luminance resolution
                                                                      TEXTURE INTENSITY SIZE    n × Z+     GetTexLevelParameter     0       texture image’s intensity   3.8       –
                                                                                                                                            resolution
                                                                                                                                                                                           223
                                                                                                                                                                          224




                                                                                            Get               Initial
                                                   Get value             Type               Cmnd              Value              Description         Sec.     Attribute
                                        TEXTURE COMPRESSED               n×B         GetTexLevelParameter     False      True if texture image has   3.8.3        -
                                                                                                                         a compressed internal
                                                                                                                         format
                                        TEXTURE COMPRESSED IMAGE SIZE    n × Z+      GetTexLevelParameter       0        size (in ubytes) of         3.8.3        -
                                                                                                                         compressed texture
                                                                                                                         image




Table
                                        TEXTURE BORDER COLOR             n×C           GetTexParameter       0,0,0,0     Texture border color         3.8     texture
                                        TEXTURE MIN FILTER               n × Z6        GetTexParameter       see 3.8     Texture minification        3.8.7    texture




    Version
                                                                                                                         function
                                        TEXTURE MAG FILTER                             GetTexParameter       see 3.8     Texture magnification       3.8.8    texture




      6.16. 1.3
                                                                         n × Z2
                                                                                                                         function
                                        TEXTURE WRAP S                                 GetTexParameter      REPEAT       Texcoord s wrap mode         3.8     texture




            Texture
                                                                         n × Z4
                                        TEXTURE WRAP T                   n × Z4        GetTexParameter      REPEAT       Texcoord t wrap mode         3.8     texture




                - August
                                                                                                                         (2D, 3D, cubemap
                                                                                                                         textures only)




                     Objects
                                        TEXTURE WRAP R                   n × Z4        GetTexParameter      REPEAT       Texcoord r wrap mode         3.8     texture




                         14, 2001
                                                                                                                         (3D textures only)
                                        TEXTURE PRIORITY                              GetTexParameterfv         1        Texture object priority     3.8.11   texture




                              (cont.)
                                                                        n × R[0,1]
                                        TEXTURE RESIDENT                  n×B         GetTexParameteriv     see 3.8.11   Texture residency           3.8.11   texture
                                        TEXTURE MIN LOD                   n×R         GetTexParameterfv       -1000      Minimum level of detail       3.8    texture
                                        TEXTURE MAX LOD                   n×R         GetTexParameterfv       1000       Maximum level of detail       3.8    texture
                                        TEXTURE BASE LEVEL               n × Z+       GetTexParameterfv         0        Base texture array            3.8    texture
                                        TEXTURE MAX LEVEL                n × Z+       GetTexParameterfv       1000       Maximum texture array         3.8    texture
                                                                                                                         level
                                                                                                                                                                          CHAPTER 6. STATE AND STATE REQUESTS
                                                                                               Get           Initial
                                                             Get value            Type         Cmnd          Value                    Description              Sec.       Attribute
                                                          ACTIVE TEXTURE           Z2∗      GetIntegerv   TEXTURE0      Active texture unit selector            2.7        texture
                                                          TEXTURE ENV MODE      2 ∗ ×Z6     GetTexEnviv   MODULATE      Texture application function          3.8.12       texture
                                                          TEXTURE ENV COLOR      2 ∗ ×C     GetTexEnvfv      0,0,0,0    Texture environment color             3.8.12       texture
                                                          TEXTURE GEN x       2 ∗ ×4 × B     IsEnabled        False     Texgen enabled (x is S, T, R, or Q)   2.10.4   texture/enable
                                                          EYE PLANE           2 ∗ ×4 × R4   GetTexGenfv    see 2.10.4   Texgen plane equation coefficients    2.10.4       texture
                                                                                                                                                                                        6.2. STATE TABLES




                                                                                                                        (for S, T, R, and Q)
                                                          OBJECT PLANE        2 ∗ ×4 × R4   GetTexGenfv    see 2.10.4   Texgen object linear coefficients     2.10.4      texture
                                                                                                                        (for S, T, R, and Q)
                                                          TEXTURE GEN MODE    2 ∗ ×4 × Z5   GetTexGeniv   EYE LINEAR    Function used for texgen (for S, T,   2.10.4      texture
                                                                                                                        R, and Q
                                                          COMBINE RGB          2 ∗ ×Z8      GetTexEnviv   MODULATE      RGB combiner function                 3.8.12      texture
                                                          COMBINE ALPHA        2 ∗ ×Z6      GetTexEnviv   MODULATE      Alpha combiner function               3.8.12      texture
                                                          SOURCE0 RGB          2 ∗ ×Z3      GetTexEnviv    TEXTURE      RGB source 0                          3.8.12      texture
                                                          SOURCE1 RGB          2 ∗ ×Z3      GetTexEnviv   PREVIOUS      RGB source 1                          3.8.12      texture
                                                          SOURCE2 RGB          2 ∗ ×Z3      GetTexEnviv   CONSTANT      RGB source 2                          3.8.12      texture
                                                          SOURCE0 ALPHA        2 ∗ ×Z3      GetTexEnviv    TEXTURE      Alpha source 0                        3.8.12      texture
                                                          SOURCE1 ALPHA        2 ∗ ×Z3      GetTexEnviv   PREVIOUS      Alpha source 1                        3.8.12      texture




                          Version 1.3 - August 14, 2001
                                                          SOURCE2 ALPHA        2 ∗ ×Z3      GetTexEnviv   CONSTANT      Alpha source 2                        3.8.12      texture
                                                          OPERAND0 RGB         2 ∗ ×Z4      GetTexEnviv   SRC COLOR     RGB operand 0                         3.8.12      texture
                                                          OPERAND1 RGB         2 ∗ ×Z4      GetTexEnviv   SRC COLOR     RGB operand 1                         3.8.12      texture
                                                          OPERAND2 RGB         2 ∗ ×Z4      GetTexEnviv   SRC ALPHA     RGB operand 2                         3.8.12      texture




Table 6.17. Texture Environment and Generation
                                                          OPERAND0 ALPHA       2 ∗ ×Z2      GetTexEnviv   SRC ALPHA     Alpha operand 0                       3.8.12      texture
                                                          OPERAND1 ALPHA       2 ∗ ×Z2      GetTexEnviv   SRC ALPHA     Alpha operand 1                       3.8.12      texture
                                                          OPERAND2 ALPHA       2 ∗ ×Z2      GetTexEnviv   SRC ALPHA     Alpha operand 2                       3.8.12      texture
                                                          RGB SCALE            2 ∗ ×R3      GetTexEnvfv      1.0        RGB post-combiner scaling             3.8.12      texture
                                                          ALPHA SCALE          2 ∗ ×R3      GetTexEnvfv      1.0        Alpha post-combiner scaling           3.8.12      texture
                                                                                                                                                                                        225
                                                                                                                                                                                                     226




                                                                                                          Get          Initial
                                                                        Get value               Type      Cmnd         Value                    Description          Sec.           Attribute
                                                               SCISSOR TEST                       B     IsEnabled       False     Scissoring enabled                 4.1.2      scissor/enable
                                                               SCISSOR BOX                      4×Z    GetIntegerv    see 4.1.2   Scissor box                        4.1.2           scissor
                                                               ALPHA TEST                         B     IsEnabled       False     Alpha test enabled                 4.1.4    color-buffer/enable
                                                               ALPHA TEST FUNC                   Z8    GetIntegerv    ALWAYS      Alpha test function                4.1.4        color-buffer
                                                               ALPHA TEST REF                    R+    GetIntegerv        0       Alpha test reference value         4.1.4        color-buffer
                                                               STENCIL TEST                       B     IsEnabled       False     Stenciling enabled                 4.1.5   stencil-buffer/enable
                                                               STENCIL FUNC                      Z8    GetIntegerv    ALWAYS      Stencil function                   4.1.5       stencil-buffer
                                                               STENCIL VALUE MASK                Z+    GetIntegerv       1’s      Stencil mask                       4.1.5       stencil-buffer
                                                               STENCIL REF                       Z+    GetIntegerv        0       Stencil reference value            4.1.5       stencil-buffer
                                                               STENCIL FAIL                      Z6    GetIntegerv     KEEP       Stencil fail action                4.1.5       stencil-buffer
                                                               STENCIL PASS DEPTH FAIL           Z6    GetIntegerv     KEEP       Stencil depth buffer fail action   4.1.5       stencil-buffer
                                                               STENCIL PASS DEPTH PASS           Z6    GetIntegerv     KEEP       Stencil depth buffer pass action   4.1.5       stencil-buffer
                                                               DEPTH TEST                         B     IsEnabled       False     Depth buffer enabled               4.1.6   depth-buffer/enable
                                                               DEPTH FUNC                        Z8    GetIntegerv     LESS       Depth buffer test function         4.1.6       depth-buffer
                                                               BLEND                              B     IsEnabled       False     Blending enabled                   4.1.7    color-buffer/enable
                                                               BLEND SRC                         Z13   GetIntegerv      ONE       Blending source function           4.1.7        color-buffer




                               Version 1.3 - August 14, 2001
Table 6.18. Pixel Operations
                                                               BLEND DST                         Z12   GetIntegerv     ZERO       Blending destination function      4.1.7        color-buffer
                                                               BLEND EQUATION                    Z5    GetIntegerv   FUNC ADD     Blending equation                  4.1.7        color-buffer
                                                               BLEND COLOR                        C     GetFloatv      0,0,0,0    Constant blend color               4.1.7        color-buffer
                                                               DITHER                             B     IsEnabled       True      Dithering enabled                  4.1.8    color-buffer/enable
                                                               INDEX LOGIC OP (v1.0:LOGIC OP)     B     IsEnabled       False     Index logic op enabled             4.1.9    color-buffer/enable
                                                               COLOR LOGIC OP                     B     IsEnabled       False     Color logic op enabled             4.1.9    color-buffer/enable
                                                               LOGIC OP MODE                     Z16   GetIntegerv     COPY       Logic op function                  4.1.9        color-buffer
                                                                                                                                                                                                     CHAPTER 6. STATE AND STATE REQUESTS
                                                                                                                                                                                         6.2. STATE TABLES




                                                                                                    Get         Initial
                                                                     Get value          Type        Cmnd        Value                   Description             Sec.       Attribute
                                                                  DRAW BUFFER           Z10∗     GetIntegerv   see 4.2.1   Buffers selected for drawing         4.2.1    color-buffer
                                                                  INDEX WRITEMASK        Z+      GetIntegerv      1’s      Color index writemask                4.2.2    color-buffer
                                                                  COLOR WRITEMASK       4×B      GetBooleanv     True      Color write enables; R, G, B, or A   4.2.2    color-buffer
                                                                  DEPTH WRITEMASK        B       GetBooleanv     True      Depth buffer enabled for writing     4.2.2   depth-buffer
                                                                  STENCIL WRITEMASK      Z+      GetIntegerv      1’s      Stencil buffer writemask             4.2.2   stencil-buffer
                                                                  COLOR CLEAR VALUE      C        GetFloatv     0,0,0,0    Color buffer clear value (RGBA       4.2.3    color-buffer
                                                                                                                           mode)
                                                                  INDEX CLEAR VALUE      CI       GetFloatv       0        Color buffer clear value (color      4.2.3   color-buffer
                                                                                                                           index mode)
                                                                  DEPTH CLEAR VALUE       R+     GetIntegerv      1        Depth buffer clear value             4.2.3   depth-buffer




Version 1.3 - August 14, 2001
                                                                  STENCIL CLEAR VALUE     Z+     GetIntegerv      0        Stencil clear value                  4.2.3   stencil-buffer




                                Table 6.19. Framebuffer Control
                                                                  ACCUM CLEAR VALUE     4 × R+    GetFloatv       0        Accumulation buffer clear value      4.2.3   accum-buffer
                                                                                                                                                                                         227
                                                                                                                                                                   228




                                                                                     Get        Initial
                                                         Get value         Type      Cmnd       Value                  Description            Sec.    Attribute
                                                     UNPACK SWAP BYTES      B     GetBooleanv   False     Value of UNPACK SWAP BYTES          4.3    pixel-store
                                                     UNPACK LSB FIRST       B     GetBooleanv   False     Value of UNPACK LSB FIRST           4.3    pixel-store
                                                     UNPACK IMAGE HEIGHT   Z+     GetIntegerv     0       Value of                            4.3    pixel-store
                                                                                                          UNPACK IMAGE HEIGHT
                                                     UNPACK SKIP IMAGES    Z+     GetIntegerv     0       Value of UNPACK SKIP IMAGES         4.3    pixel-store
                                                     UNPACK ROW LENGTH     Z+     GetIntegerv     0       Value of UNPACK ROW LENGTH          4.3    pixel-store
                                                     UNPACK SKIP ROWS      Z+     GetIntegerv     0       Value of UNPACK SKIP ROWS           4.3    pixel-store
                                                     UNPACK SKIP PIXELS    Z+     GetIntegerv     0       Value of UNPACK SKIP PIXELS         4.3    pixel-store
                                                     UNPACK ALIGNMENT      Z+     GetIntegerv     4       Value of UNPACK ALIGNMENT           4.3    pixel-store
                                                     PACK SWAP BYTES       B      GetBooleanv   False     Value of PACK SWAP BYTES            4.3    pixel-store
                                                     PACK LSB FIRST        B      GetBooleanv   False     Value of PACK LSB FIRST             4.3    pixel-store
                                                     PACK IMAGE HEIGHT     Z+     GetIntegerv     0       Value of PACK IMAGE HEIGHT          4.3    pixel-store
                                                     PACK SKIP IMAGES      Z+     GetIntegerv     0       Value of PACK SKIP IMAGES           4.3    pixel-store
                                                     PACK ROW LENGTH       Z+     GetIntegerv     0       Value of PACK ROW LENGTH            4.3    pixel-store




                                Table 6.20. Pixels
                                                     PACK SKIP ROWS        Z+     GetIntegerv     0       Value of PACK SKIP ROWS             4.3    pixel-store
                                                     PACK SKIP PIXELS      Z+     GetIntegerv     0       Value of PACK SKIP PIXELS           4.3    pixel-store




Version 1.3 - August 14, 2001
                                                     PACK ALIGNMENT        Z+     GetIntegerv     4       Value of PACK ALIGNMENT             4.3    pixel-store
                                                     MAP COLOR             B      GetBooleanv   False     True if colors are mapped           4.3       pixel
                                                     MAP STENCIL           B      GetBooleanv   False     True if stencil values are mapped   4.3       pixel
                                                     INDEX SHIFT           Z      GetIntegerv     0       Value of INDEX SHIFT                4.3       pixel
                                                     INDEX OFFSET          Z      GetIntegerv     0       Value of INDEX OFFSET               4.3       pixel
                                                     x SCALE               R       GetFloatv      1       Value of x SCALE; x is RED,         4.3       pixel
                                                                                                          GREEN, BLUE, ALPHA, or DEPTH
                                                     x BIAS                 R      GetFloatv      0       Value of x BIAS                     4.3      pixel
                                                                                                                                                                   CHAPTER 6. STATE AND STATE REQUESTS
                                                                                      Get         Initial
                                         Get value                  Type              Cmnd        Value            Description          Sec.      Attribute
                                COLOR TABLE                          B           IsEnabled        False     True if color table         3.6.3   pixel/enable
                                                                                                            lookup is done
                                POST CONVOLUTION COLOR TABLE          B          IsEnabled        False     True if post convolution    3.6.3   pixel/enable
                                                                                                                                                               6.2. STATE TABLES




                                                                                                            color table lookup is
                                                                                                            done
                                POST COLOR MATRIX COLOR TABLE         B          IsEnabled        False     True if post color matrix   3.6.3   pixel/enable
                                                                                                            color table lookup is




Version
                                                                                                            done
                                COLOR TABLE                         3×I          GetColorTable    empty     Color tables                3.6.3        –




 Table 6.21.
                                COLOR TABLE FORMAT               2 × 3 × Z42     GetColorTable-   RGBA      Color tables’ internal      3.6.3        –
                                                                                 Parameteriv                image format
                                COLOR TABLE WIDTH                2 × 3 × Z+      GetColorTable-     0       Color tables’ specified     3.6.3        –




        1.3 - August
                                                                                 Parameteriv                width
                                COLOR TABLE x SIZE              6 × 2 × 3 × Z+   GetColorTable-     0       Color table component       3.6.3        –
                                                                                 Parameteriv                resolution; x is RED,




              Pixels (cont.)
                     14, 2001
                                                                                                            GREEN, BLUE, ALPHA,
                                                                                                            LUMINANCE, or
                                                                                                            INTENSITY
                                COLOR TABLE SCALE                  3 × R4        GetColorTable-   1,1,1,1   Scale factors applied to    3.6.3      pixel
                                                                                 Parameterfv                color table entries
                                COLOR TABLE BIAS                   3 × R4        GetColorTable-   0,0,0,0   Bias factors applied to     3.6.3      pixel
                                                                                 Parameterfv                color table entries
                                                                                                                                                               229
                                                                                                                                                                                      230




                                                                                                       Get              Initial
                                                                    Get value            Type          Cmnd             Value            Description           Sec.      Attribute
                                                             CONVOLUTION 1D               B       IsEnabled             False     True if 1D convolution is    3.6.3   pixel/enable
                                                                                                                                  done
                                                             CONVOLUTION 2D               B       IsEnabled             False     True if 2D convolution is    3.6.3   pixel/enable
                                                                                                                                  done
                                                             SEPARABLE 2D                 B       IsEnabled             False     True if separable 2D         3.6.3   pixel/enable
                                                                                                                                  convolution is done
                                                             CONVOLUTION                 2×I      GetConvolution-       empty     Convolution filters          3.6.3        –
                                                                                                  Filter
                                                             CONVOLUTION                 2×I      GetSeparable- Fil-    empty     Separable convolution        3.6.3        –
                                                                                                  ter                             filter
                                                             CONVOLUTION BORDER COLOR   3×C       GetConvolution-      0,0,0,0    Convolution border color     4.3        pixel
                                                                                                  Parameterfv
                                                             CONVOLUTION BORDER MODE    3 × Z4    GetConvolution-      REDUCE     Convolution border           4.3        pixel
                                                                                                  Parameteriv                     mode
                                                             CONVOLUTION FILTER SCALE   3 × R4    GetConvolution-      1,1,1,1    Scale factors applied to     3.6.3      pixel
                                                                                                  Parameterfv                     convolution filter entries




                                Table 6.22. Pixels (cont.)


Version 1.3 - August 14, 2001
                                                             CONVOLUTION FILTER BIAS    3 × R4    GetConvolution-      0,0,0,0    Bias factors applied to      3.6.3      pixel
                                                                                                  Parameterfv                     convolution filter entries
                                                             CONVOLUTION FORMAT         3 × Z42   GetConvolution-       RGBA      Convolution filter           4.3          –
                                                                                                  Parameteriv                     internal format
                                                             CONVOLUTION WIDTH          3 × Z+    GetConvolution-         0       Convolution filter width     4.3          –
                                                                                                  Parameteriv
                                                             CONVOLUTION HEIGHT         2 × Z+    GetConvolution-         0       Convolution filter height    4.3          –
                                                                                                  Parameteriv
                                                                                                                                                                                      CHAPTER 6. STATE AND STATE REQUESTS
                                                                                                            Get       Initial
                                                                   Get value                Type            Cmnd      Value            Description         Sec.     Attribute
                                                             POST CONVOLUTION x SCALE        R        GetFloatv         1       Component scale factors    3.6.3     pixel
                                                                                                                                after convolution; x is
                                                                                                                                RED, GREEN, BLUE, or
                                                                                                                                ALPHA
                                                                                                                                                                                  6.2. STATE TABLES




                                                             POST CONVOLUTION x BIAS         R        GetFloatv         0       Component bias factors     3.6.3      pixel
                                                                                                                                after convolution
                                                             POST COLOR MATRIX x SCALE       R        GetFloatv         1       Component scale factors    3.6.3      pixel
                                                                                                                                after color matrix
                                                             POST COLOR MATRIX x BIAS        R        GetFloatv         0       Component bias factors     3.6.3      pixel
                                                                                                                                after color matrix
                                                             HISTOGRAM                       B        IsEnabled       False     True if histogramming is   3.6.3   pixel/enable
                                                                                                                                enabled
                                                             HISTOGRAM                       I        GetHistogram    empty     Histogram table            3.6.3        –
                                                             HISTOGRAM WIDTH              2 × Z+      GetHistogram-     0       Histogram table width      3.6.3        –
                                                                                                      Parameteriv




                                Table 6.23. Pixels (cont.)
                                                             HISTOGRAM FORMAT             2 × Z42     GetHistogram-   RGBA      Histogram table internal   3.6.3        –




Version 1.3 - August 14, 2001
                                                                                                      Parameteriv               format
                                                             HISTOGRAM x SIZE            5 × 2 × Z+   GetHistogram-     0       Histogram table            3.6.3        –
                                                                                                      Parameteriv               component resolution; x
                                                                                                                                is RED, GREEN, BLUE,
                                                                                                                                ALPHA, or LUMINANCE
                                                             HISTOGRAM SINK                  B        GetHistogram-   False     True if histogramming      3.6.3        –
                                                                                                      Parameteriv               consumes pixel groups
                                                                                                                                                                                  231
                                                                                                                                                      232




                                                                   Get             Initial
                                    Get value      Type            Cmnd            Value                 Description           Sec.      Attribute
                                MINMAX              B         IsEnabled            False          True if minmax is            3.6.3   pixel/enable
                                                                                                  enabled
                                MINMAX             Rn         GetMinmax     (M,M,M,M),(m,m,m,m)   Minmax table                 3.6.3        –
                                MINMAX FORMAT      Z42        GetMinmax-           RGBA           Minmax table internal        3.6.3        –
                                                              Parameteriv                         format
                                MINMAX SINK         B         GetMinmax-           False          True if minmax               3.6.3        –




Version
                                                              Parameteriv                         consumes pixel groups
                                ZOOM X               R        GetFloatv             1.0           x zoom factor                4.3        pixel




 Table 6.24.
                                ZOOM Y               R        GetFloatv             1.0           y zoom factor                4.3        pixel
                                x               8 × 32 ∗ ×R   GetPixelMap           0’s           RGBA PixelMap                4.3          –




        1.3 - August
                                                                                                  translation tables; x is a
                                                                                                  map name from
                                                                                                  Table 3.3




              Pixels (cont.)
                                x               2 × 32 ∗ ×Z   GetPixelMap            0’s          Index PixelMap               4.3          –




                     14, 2001
                                                                                                  translation tables; x is a
                                                                                                  map name from
                                                                                                  Table 3.3
                                x SIZE              Z+        GetIntegerv             1           Size of table x              4.3          –
                                READ BUFFER         Z3        GetIntegerv         see 4.3.2       Read source buffer           4.3        pixel
                                                                                                                                                      CHAPTER 6. STATE AND STATE REQUESTS
                                                                                                                             Get        Initial
                                                                                                                                                                                                             6.2. STATE TABLES




                                                                                      Get value                Type          Cmnd       Value                  Description              Sec.    Attribute
                                                                                   ORDER                     9 × Z8∗       GetMapiv       1       1d map order                          5.1         –
                                                                                   ORDER                   9 × 2 × Z8∗     GetMapiv      1,1      2d map orders                         5.1         –
                                                                                   COEFF                  9 × 8 ∗ ×Rn      GetMapfv    see 5.1    1d control points                     5.1         –
                                                                                   COEFF                9 × 8 ∗ ×8 ∗ ×Rn   GetMapfv    see 5.1    2d control points                     5.1         –
                                                                                   DOMAIN                   9×2×R          GetMapfv    see 5.1    1d domain endpoints                   5.1         –
                                                                                   DOMAIN                   9×4×R          GetMapfv    see 5.1    2d domain endpoints                   5.1         –
                                                                                   MAP1 x                     9×B          IsEnabled    False     1d map enables: x is map type         5.1    eval/enable
                                                                                   MAP2 x                     9×B          IsEnabled    False     2d map enables: x is map type         5.1    eval/enable
                                                                                   MAP1 GRID DOMAIN           2×R          GetFloatv     0,1      1d grid endpoints                     5.1       eval
                                                                                   MAP2 GRID DOMAIN           4×R          GetFloatv   0,1;0,1    2d grid endpoints                     5.1       eval
                                                                                   MAP1 GRID SEGMENTS          Z+          GetFloatv      1       1d grid divisions                     5.1       eval




Version 1.3 - August 14, 2001
                                                                                   MAP2 GRID SEGMENTS        2 × Z+        GetFloatv     1,1      2d grid divisions                     5.1       eval
                                                                                   AUTO NORMAL                  B          IsEnabled    False     True if automatic normal generation   5.1    eval/enable
                                                                                                                                                  enabled




                                Table 6.25. Evaluators (GetMap takes a map name)
                                                                                                                                                                                                             233
                                                                                                                                                                         234




                                                                                           Get           Initial
                                                           Get value              Type     Cmnd          Value                 Description            Sec.   Attribute
                                                    PERSPECTIVE CORRECTION HINT    Z3    GetIntegerv   DONT CARE   Perspective correction hint        5.6      hint
                                                    POINT SMOOTH HINT              Z3    GetIntegerv   DONT CARE   Point smooth hint                  5.6      hint
                                                    LINE SMOOTH HINT               Z3    GetIntegerv   DONT CARE   Line smooth hint                   5.6      hint
                                                    POLYGON SMOOTH HINT            Z3    GetIntegerv   DONT CARE   Polygon smooth hint                5.6      hint
                                                    FOG HINT                       Z3    GetIntegerv   DONT CARE   Fog hint                           5.6      hint




                                Table 6.26. Hints
                                                    TEXTURE COMPRESSION HINT       Z3    GetIntegerv   DONT CARE   Texture compression quality hint   5.6      hint




Version 1.3 - August 14, 2001
                                                                                                                                                                         CHAPTER 6. STATE AND STATE REQUESTS
                                                                                                                        Get         Minimum
                                                                                       Get value              Type      Cmnd        Value                     Description             Sec.    Attribute
                                                                              MAX LIGHTS                      Z+      GetIntegerv       8        Maximum number of lights            2.13.1       –
                                                                              MAX CLIP PLANES                 Z+      GetIntegerv       6        Maximum number of user clipping      2.11        –
                                                                                                                                                 planes
                                                                              MAX COLOR MATRIX STACK DEPTH    Z+      GetIntegerv       2        Maximum color matrix stack depth    3.6.3       –
                                                                              MAX MODELVIEW STACK DEPTH       Z+      GetIntegerv      32        Maximum model-view stack depth      2.10.2      –
                                                                                                                                                                                                          6.2. STATE TABLES




                                                                              MAX PROJECTION STACK DEPTH      Z+      GetIntegerv       2        Maximum projection matrix stack     2.10.2      –
                                                                                                                                                 depth
                                                                              MAX TEXTURE STACK DEPTH         Z+      GetIntegerv       2        Maximum number depth of texture     2.10.2      –
                                                                                                                                                 matrix stack
                                                                              SUBPIXEL BITS                   Z+      GetIntegerv       4        Number of bits of subpixel            3         –
                                                                                                                                                 precision in screen xw and yw
                                                                              MAX 3D TEXTURE SIZE             Z+      GetIntegerv      16        Maximum 3D texture image            3.8.1       –
                                                                                                                                                 dimension
                                                                              MAX TEXTURE SIZE                Z+      GetIntegerv      64        Maximum 2D/1D texture image         3.8.1       –
                                                                                                                                                 dimension
                                                                              MAX CUBE MAP TEXTURE SIZE       Z+      GetIntegerv      16        Maximum cube map texture image      3.8.1       –
                                                                                                                                                 dimension




Version 1.3 - August 14, 2001
                                                                              MAX PIXEL MAP TABLE             Z+      GetIntegerv      32        Maximum size of a PixelMap          3.6.3       –
                                                                                                                                                 translation table
                                                                              MAX NAME STACK DEPTH            Z+      GetIntegerv      64        Maximum selection name stack         5.2        –




                                Table 6.27. Implementation Dependent Values
                                                                                                                                                 depth
                                                                              MAX LIST NESTING                Z+      GetIntegerv      64        Maximum display list call nesting    5.4        –
                                                                              MAX EVAL ORDER                  Z+      GetIntegerv      8         Maximum evaluator polynomial         5.1        –
                                                                                                                                                 order
                                                                              MAX VIEWPORT DIMS              2 × Z+   GetIntegerv   see 2.10.1   Maximum viewport dimensions         2.10.1      –
                                                                                                                                                                                                          235
                                                                                                                                                                                                         236




                                                                                                                    Get      Minimum
                                                                                          Get value    Type         Cmnd     Value                       Description                 Sec.    Attribute
                                                      MAX ATTRIB STACK DEPTH                            Z+     GetIntegerv      16     Maximum depth of the server attribute stack     6         –
                                                      MAX CLIENT ATTRIB STACK DEPTH                     Z+     GetIntegerv      16     Maximum depth of the client attribute stack     6         –
                                                      –                                               3 × Z+   -                32     Maximum size of a color table                 3.6.3       –
                                                      –                                                 Z+     -                32     Maximum size of the histogram table           3.6.3       –
                                                      AUX BUFFERS                                       Z+     GetIntegerv       0     Number of auxiliary buffers                   4.2.1       –
                                                      RGBA MODE                                          B     GetBooleanv       –     True if color buffers store rgba               2.7        –
                                                      INDEX MODE                                         B     GetBooleanv       –     True if color buffers store indexes            2.7        –
                                                      DOUBLEBUFFER                                       B     GetBooleanv       –     True if front & back buffers exist            4.2.1       –
                                                      STEREO                                             B     GetBooleanv       –     True if left & right buffers exist              6         –
                                                      ALIASED POINT SIZE RANGE                        2 × R+   GetFloatv        1,1    Range (lo to hi) of aliased point sizes        3.3        –
                                                      SMOOTH POINT SIZE RANGE                         2 × R+   GetFloatv        1,1    Range (lo to hi) of antialiased point sizes    3.3        –
                                                      (v1.1: POINT SIZE RANGE)

                                                      SMOOTH POINT SIZE GRANULARITY                    R+      GetFloatv        –      Antialiased point size granularity            3.3        –
                                                      (v1.1: POINT SIZE GRANULARITY)




                                                          Version 1.3 - August 14, 2001
                                                      ALIASED LINE WIDTH RANGE                        2 × R+   GetFloatv       1,1     Range (lo to hi) of aliased line widths       3.4        –
                                                      SMOOTH LINE WIDTH RANGE                         2 × R+   GetFloatv       1,1     Range (lo to hi) of antialiased line widths   3.4        –
                                                      (v1.1: LINE WIDTH RANGE)

                                                      SMOOTH LINE WIDTH GRANULARITY                    R+      GetFloatv        –      Antialiased line width granularity            3.4        –
                                                      (v1.1: LINE WIDTH GRANULARITY)




Table 6.28. Implementation Dependent Values (cont.)
                                                                                                                                                                                                         CHAPTER 6. STATE AND STATE REQUESTS
                                                                                                           Get         Minimum
                                                                            Get value        Type          Cmnd        Value            Description        Sec.    Attribute
                                                           MAX CONVOLUTION WIDTH            3 × Z+   GetConvolution-       3     Maximum width of          4.3         –
                                                                                                     Parameteriv                 convolution filter
                                                           MAX CONVOLUTION HEIGHT           2 × Z+   GetConvolution-      3      Maximum height of         4.3        –
                                                                                                                                                                               6.2. STATE TABLES




                                                                                                     Parameteriv                 convolution filter
                                                           MAX ELEMENTS INDICES              Z+      GetIntegerv          –      Recommended               2.8        –
                                                                                                                                 maximum number of
                                                                                                                                 DrawRangeEle-
                                                                                                                                 ments indices
                                                           MAX ELEMENTS VERTICES             Z+      GetIntegerv          –      Recommended               2.8        –
                                                                                                                                 maximum number of




Table 6.29. Implementation
                                                                                                                                 DrawRangeEle-
                                                                                                                                 ments vertices




             Version 1.3 - August
                                                           MAX TEXTURE UNITS                 Z+      GetIntegerv          2      Number of texture units   2.6        –
                                                                                                                                 (not to exceed 32)
                                                           SAMPLE BUFFERS                    Z+      GetIntegerv          0      Number of multisample     3.2.1      –




                             Dependent
                                                                                                                                 buffers
                                                           SAMPLES                           Z+      GetIntegerv          0      Coverage mask size        3.2.1      –
                                                           COMPRESSED TEXTURE FORMATS       0×Z      GetIntegerv          -      Enumerated compressed     3.8.3      –
                                                                                                                                 texture formats
                                                           NUM COMPRESSED TEXTURE FORMATS     Z      GetIntegerv          0      Number of enumerated      3.8.3      –




                                  14, 2001Values (cont.)
                                                                                                                                 compressed texture
                                                                                                                                 formats
                                                                                                                                                                               237
                                                                                                                                                                                        238




                                                                                                            Get         Initial
                                                                                    Get value      Type     Cmnd        Value                Description             Sec.   Attribute
                                                                                    x BITS         Z+     GetIntegerv      -      Number of bits in x color buffer    4         –
                                                                                                                                  component; x is one of RED,
                                                                                                                                  GREEN, BLUE, ALPHA, or INDEX
                                                                                    DEPTH BITS     Z+     GetIntegerv     -       Number of depth buffer planes       4        –
                                                                                    STENCIL BITS   Z+     GetIntegerv     -       Number of stencil planes            4        –
                                                                                    ACCUM x BITS   Z+     GetIntegerv     -       Number of bits in x accumulation    4        –
                                                                                                                                  buffer component (x is RED,
                                                                                                                                  GREEN, BLUE, or ALPHA




Version 1.3 - August 14, 2001
                                Table 6.30. Implementation Dependent Pixel Depths
                                                                                                                                                                                        CHAPTER 6. STATE AND STATE REQUESTS
                                                                                                    Get          Initial
                                                                  Get value              Type       Cmnd         Value                  Description           Sec.   Attribute
                                                            LIST BASE                    Z+       GetIntegerv      0       Setting of ListBase                5.4       list
                                                            LIST INDEX                   Z+       GetIntegerv      0       Number of display list under       5.4        –
                                                                                                                                                                                 6.2. STATE TABLES




                                                                                                                           construction; 0 if none
                                                            LIST MODE                     Z+      GetIntegerv      0       Mode of display list under         5.4       –
                                                                                                                           construction; undefined if none
                                                            –                           16 ∗ ×A        –         empty     Server attribute stack              6         –
                                                            ATTRIB STACK DEPTH             Z+     GetIntegerv      0       Server attribute stack pointer      6         –
                                                            –                           16 ∗ ×A        –         empty     Client attribute stack              6         –
                                                            CLIENT ATTRIB STACK DEPTH      Z+     GetIntegerv      0       Client attribute stack pointer      6         –
                                                            NAME STACK DEPTH               Z+     GetIntegerv      0       Name stack depth                   5.2        –
                                                            RENDER MODE                    Z3     GetIntegerv   RENDER     RenderMode setting                 5.2        –
                                                            SELECTION BUFFER POINTER       Y      GetPointerv      0       Selection buffer pointer           5.2      select
                                                            SELECTION BUFFER SIZE          Z+     GetIntegerv      0       Selection buffer size              5.2      select




                                Table 6.31. Miscellaneous
                                                            FEEDBACK BUFFER POINTER        Y      GetPointerv      0       Feedback buffer pointer            5.3    feedback




Version 1.3 - August 14, 2001
                                                            FEEDBACK BUFFER SIZE           Z+     GetIntegerv      0       Feedback buffer size               5.3    feedback
                                                            FEEDBACK BUFFER TYPE           Z5     GetIntegerv     2D       Feedback type                      5.3    feedback
                                                            –                            n × Z8    GetError        0       Current error code(s)              2.5        –
                                                            –                            n×B           –         False     True if there is a corresponding   2.5        –
                                                                                                                           error
                                                                                                                                                                                 239
Appendix A

Invariance

The OpenGL specification is not pixel exact. It therefore does not guarantee an ex-
act match between images produced by different GL implementations. However,
the specification does specify exact matches, in some cases, for images produced
by the same implementation. The purpose of this appendix is to identify and pro-
vide justification for those cases that require exact matches.




A.1     Repeatability

The obvious and most fundamental case is repeated issuance of a series of GL com-
mands. For any given GL and framebuffer state vector, and for any GL command,
the resulting GL and framebuffer state must be identical whenever the command is
executed on that initial GL and framebuffer state.
    One purpose of repeatability is avoidance of visual artifacts when a double-
buffered scene is redrawn. If rendering is not repeatable, swapping between two
buffers rendered with the same command sequence may result in visible changes
in the image. Such false motion is distracting to the viewer. Another reason for
repeatability is testability.
     Repeatability, while important, is a weak requirement. Given only repeata-
bility as a requirement, two scenes rendered with one (small) polygon changed
in position might differ at every pixel. Such a difference, while within the law
of repeatability, is certainly not within its spirit. Additional invariance rules are
desirable to ensure useful operation.

                                        240
A.2. MULTI-PASS ALGORITHMS                                                       241


A.2     Multi-pass Algorithms
Invariance is necessary for a whole set of useful multi-pass algorithms. Such al-
gorithms render multiple times, each time with a different GL mode vector, to
eventually produce a result in the framebuffer. Examples of these algorithms in-
clude:

   • “Erasing” a primitive from the framebuffer by redrawing it, either in a dif-
     ferent color or using the XOR logical operation.

   • Using stencil operations to compute capping planes.

    On the other hand, invariance rules can greatly increase the complexity of high-
performance implementations of the GL. Even the weak repeatability requirement
significantly constrains a parallel implementation of the GL. Because GL imple-
mentations are required to implement ALL GL capabilities, not just a convenient
subset, those that utilize hardware acceleration are expected to alternate between
hardware and software modules based on the current GL mode vector. A strong
invariance requirement forces the behavior of the hardware and software modules
to be identical, something that may be very difficult to achieve (for example, if the
hardware does floating-point operations with different precision than the software).
    What is desired is a compromise that results in many compliant, high-
performance implementations, and in many software vendors choosing to port to
OpenGL.


A.3     Invariance Rules
For a given instantiation of an OpenGL rendering context:

Rule 1 For any given GL and framebuffer state vector, and for any given GL com-
mand, the resulting GL and framebuffer state must be identical each time the com-
mand is executed on that initial GL and framebuffer state.

Rule 2 Changes to the following state values have no side effects (the use of any
other state value is not affected by the change):

Required:

         • Framebuffer contents (all bitplanes)
         • The color buffers enabled for writing
         • The values of matrices other than the top-of-stack matrices

                          Version 1.3 - August 14, 2001
242                                                 APPENDIX A. INVARIANCE


         • Scissor parameters (other than enable)
         • Writemasks (color, index, depth, stencil)
         • Clear values (color, index, depth, stencil, accumulation)
         ◦ Current values (color, index, normal, texture coords, edgeflag)
         ◦ Current raster color, index and texture coordinates.
         ◦ Material properties (ambient, diffuse, specular, emission, shininess)

Strongly suggested:

         • Matrix mode
         • Matrix stack depths
         • Alpha test parameters (other than enable)
         • Stencil parameters (other than enable)
         • Depth test parameters (other than enable)
         • Blend parameters (other than enable)
         • Logical operation parameters (other than enable)
         • Pixel storage and transfer state
         • Evaluator state (except as it affects the vertex data generated by the
           evaluators)
         • Polygon offset parameters (other than enables, and except as they affect
           the depth values of fragments)

Corollary 1 Fragment generation is invariant with respect to the state values
marked with • in Rule 2.

Corollary 2 The window coordinates (x, y, and z) of generated fragments are also
invariant with respect to
Required:

         • Current values (color, color index, normal, texture coords, edgeflag)
         • Current raster color, color index, and texture coordinates
         • Material properties (ambient, diffuse, specular, emission, shininess)

Rule 3 The arithmetic of each per-fragment operation is invariant except with re-
spect to parameters that directly control it (the parameters that control the alpha
test, for instance, are the alpha test enable, the alpha test function, and the alpha
test reference value).

                          Version 1.3 - August 14, 2001
A.4. WHAT ALL THIS MEANS                                                        243


Corollary 3 Images rendered into different color buffers sharing the same frame-
buffer, either simultaneously or separately using the same command sequence, are
pixel identical.


A.4     What All This Means
Hardware accelerated GL implementations are expected to default to software op-
eration when some GL state vectors are encountered. Even the weak repeatability
requirement means, for example, that OpenGL implementations cannot apply hys-
teresis to this swap, but must instead guarantee that a given mode vector implies
that a subsequent command always is executed in either the hardware or the soft-
ware machine.
    The stronger invariance rules constrain when the switch from hardware to soft-
ware rendering can occur, given that the software and hardware renderers are not
pixel identical. For example, the switch can be made when blending is enabled or
disabled, but it should not be made when a change is made to the blending param-
eters.
    Because floating point values may be represented using different formats in dif-
ferent renderers (hardware and software), many OpenGL state values may change
subtly when renderers are swapped. This is the type of state value change that Rule
1 seeks to avoid.




                          Version 1.3 - August 14, 2001
Appendix B

Corollaries

The following observations are derived from the body and the other appendixes of
the specification. Absence of an observation from this list in no way impugns its
veracity.
   1. The CURRENT RASTER TEXTURE COORDS must be maintained correctly at
      all times, including periods while texture mapping is not enabled, and when
      the GL is in color index mode.
   2. When requested, texture coordinates returned in feedback mode are always
      valid, including periods while texture mapping is not enabled, and when the
      GL is in color index mode.
   3. The error semantics of upward compatible OpenGL revisions may change.
      Otherwise, only additions can be made to upward compatible revisions.
   4. GL query commands are not required to satisfy the semantics of the Flush
      or the Finish commands. All that is required is that the queried state be con-
      sistent with complete execution of all previously executed GL commands.
   5. Application specified point size and line width must be returned as specified
      when queried. Implementation dependent clamping affects the values only
      while they are in use.
   6. Bitmaps and pixel transfers do not cause selection hits.
   7. The mask specified as the third argument to StencilFunc affects the operands
      of the stencil comparison function, but has no direct effect on the update of
      the stencil buffer. The mask specified by StencilMask has no effect on the
      stencil comparison function; it limits the effect of the update of the stencil
      buffer.

                                       244
                                                                               245


 8. Polygon shading is completed before the polygon mode is interpreted. If the
    shade model is FLAT, all of the points or lines generated by a single polygon
    will have the same color.

 9. A display list is just a group of commands and arguments, so errors generated
    by commands in a display list must be generated when the list is executed.
    If the list is created in COMPILE mode, errors should not be generated while
    the list is being created.

10. RasterPos does not change the current raster index from its default value
    in an RGBA mode GL context. Likewise, RasterPos does not change the
    current raster color from its default value in a color index GL context. Both
    the current raster index and the current raster color can be queried, however,
    regardless of the color mode of the GL context.

11. A material property that is attached to the current color via ColorMaterial
    always takes the value of the current color. Attempts to change that material
    property via Material calls have no effect.

12. Material and ColorMaterial can be used to modify the RGBA material
    properties, even in a color index context. Likewise, Material can be used to
    modify the color index material properties, even in an RGBA context.

13. There is no atomicity requirement for OpenGL rendering commands, even
    at the fragment level.

14. Because rasterization of non-antialiased polygons is point sampled, poly-
    gons that have no area generate no fragments when they are rasterized in
    FILL mode, and the fragments generated by the rasterization of “narrow”
    polygons may not form a continuous array.

15. OpenGL does not force left- or right-handedness on any of its coordinates
    systems. Consider, however, the following conditions: (1) the object coordi-
    nate system is right-handed; (2) the only commands used to manipulate the
    model-view matrix are Scale (with positive scaling values only), Rotate, and
    Translate; (3) exactly one of either Frustum or Ortho is used to set the pro-
    jection matrix; (4) the near value is less than the far value for DepthRange.
    If these conditions are all satisfied, then the eye coordinate system is right-
    handed and the clip, normalized device, and window coordinate systems are
    left-handed.

16. ColorMaterial has no effect on color index lighting.

                        Version 1.3 - August 14, 2001
246                                              APPENDIX B. COROLLARIES


 17. (No pixel dropouts or duplicates.) Let two polygons share an identical edge
     (that is, there exist vertices A and B of an edge of one polygon, and vertices
     C and D of an edge of the other polygon, and the coordinates of vertex A
     (resp. B) are identical to those of vertex C (resp. D), and the state of the the
     coordinate transfomations is identical when A, B, C, and D are specified).
     Then, when the fragments produced by rasterization of both polygons are
     taken together, each fragment intersecting the interior of the shared edge is
     produced exactly once.

 18. OpenGL state continues to be modified in FEEDBACK mode and in SELECT
     mode. The contents of the framebuffer are not modified.

 19. The current raster position, the user defined clip planes, the spot directions
     and the light positions for LIGHTi, and the eye planes for texgen are trans-
     formed when they are specified. They are not transformed during a PopAt-
     trib, or when copying a context.

 20. Dithering algorithms may be different for different components. In particu-
     lar, alpha may be dithered differently from red, green, or blue, and an imple-
     mentation may choose to not dither alpha at all.

 21. For any GL and framebuffer state, and for any group of GL commands and
     arguments, the resulting GL and framebuffer state is identical whether the
     GL commands and arguments are executed normally or from a display list.




                          Version 1.3 - August 14, 2001
Appendix C

Version 1.1

OpenGL version 1.1 is the first revision since the original version 1.0 was released
on 1 July 1992. Version 1.1 is upward compatible with version 1.0, meaning that
any program that runs with a 1.0 GL implementation will also run unchanged with
a 1.1 GL implementation. Several additions were made to the GL, especially to
the texture mapping capabilities, but also to the geometry and fragment operations.
Following are brief descriptions of each addition.




C.1     Vertex Array

Arrays of vertex data may be transferred to the GL with many fewer commands
than were previously necessary. Six arrays are defined, one each storing vertex
positions, normal coordinates, colors, color indices, texture coordinates, and edge
flags. The arrays may be specified and enabled independently, or one of the pre-
defined configurations may be selected with a single command.
    The primary goal was to decrease the number of subroutine calls required
to transfer non-display listed geometry data to the GL. A secondary goal was to
improve the efficiency of the transfer; especially to allow direct memory access
(DMA) hardware to be used to effect the transfer. The additions match those of
the EXT vertex array extension, except that static array data are not supported
(because they complicated the interface, and were not being used), and the pre-
defined configurations are added (both to reduce subroutine count even further,
and to allow for efficient transfer of array data).

                                        247
248                                                  APPENDIX C. VERSION 1.1


C.2     Polygon Offset
Depth values of fragments generated by the rasterization of a polygon may be
shifted toward or away from the origin, as an affine function of the window coor-
dinate depth slope of the polygon. Shifted depth values allow coplanar geometry,
especially facet outlines, to be rendered without depth buffer artifacts. They may
also be used by future shadow generation algorithms.
    The additions match those of the EXT polygon offset extension, with two
exceptions. First, the offset is enabled separately for POINT, LINE, and FILL ras-
terization modes, all sharing a single affine function definition. (Shifting the depth
values of the outline fragments, instead of the fill fragments, allows the contents of
the depth buffer to be maintained correctly.) Second, the offset bias is specified in
units of depth buffer resolution, rather than in the [0,1] depth range.


C.3     Logical Operation
Fragments generated by RGBA rendering may be merged into the framebuffer us-
ing a logical operation, just as color index fragments are in GL version 1.0. Blend-
ing is disabled during such operation because it is rarely desired, because many sys-
tems could not support it, and to match the semantics of the EXT blend logic op
extension, on which this addition is loosely based.


C.4     Texture Image Formats
Stored texture arrays have a format, known as the internal format, rather than a
simple count of components. The internal format is represented as a single enumer-
ated value, indicating both the organization of the image data (LUMINANCE, RGB,
etc.) and the number of bits of storage for each image component. Clients can use
the internal format specification to suggest the desired storage precision of texture
images. New base formats, ALPHA and INTENSITY, provide new texture environ-
ment operations. These additions match those of a subset of the EXT texture
extension.


C.5     Texture Replace Environment
A common use of texture mapping is to replace the color values of generated
fragments with texture color data. This could be specified only indirectly in GL
version 1.0, which required that client specified “white” geometry be modulated

                           Version 1.3 - August 14, 2001
C.6. TEXTURE PROXIES                                                              249


by a texture. GL version 1.1 allows such replacement to be specified explicitly,
possibly improving performance. These additions match those of a subset of the
EXT texture extension.


C.6     Texture Proxies
Texture proxies allow a GL implementation to advertise different maximum tex-
ture image sizes as a function of some other texture parameters, especially of the
internal image format. Clients may use the proxy query mechanism to tailor their
use of texture resources at run time. The proxy interface is designed to allow such
queries without adding new routines to the GL interface. These additions match
those of a subset of the EXT texture extension, except that implementations re-
turn allocation information consistent with support for complete mipmap arrays.


C.7     Copy Texture and Subtexture
Texture array data can be specified from framebuffer memory, as well as from
client memory, and rectangular subregions of texture arrays can be redefined either
from client or framebuffer memory. These additions match those defined by the
EXT copy texture and EXT subtexture extensions.


C.8     Texture Objects
A set of texture arrays and their related texture state can be treated as a single ob-
ject. Such treatment allows for greater implementation efficiency when multiple
arrays are used. In conjunction with the subtexture capability, it also allows clients
to make gradual changes to existing texture arrays, rather than completely redefin-
ing them. These additions match those of the EXT texture object extension,
with slight additions to the texture residency semantics.


C.9     Other Changes
   1. Color indices may now be specified as unsigned bytes.

   2. Texture coordinates s, t, and r are divided by q during the rasterization of
      points, pixel rectangles, and bitmaps. This division was documented only
      for lines and polygons in the 1.0 version.

                           Version 1.3 - August 14, 2001
250                                                APPENDIX C. VERSION 1.1


   3. The line rasterization algorithm was changed so that vertical lines on pixel
      borders rasterize correctly.

   4. Separate pixel transfer discussions in chapter 3 and chapter 4 were combined
      into a single discussion in chapter 3.

   5. Texture alpha values are returned as 1.0 if there is no alpha channel in the
      texture array. This behavior was unspecified in the 1.0 version, and was
      incorrectly documented in the reference manual.

   6. Fog start and end values may now be negative.

   7. Evaluated color values direct the evaluation of the lighting equation if Col-
      orMaterial is enabled.


C.10     Acknowledgements
OpenGL 1.1 is the result of the contributions of many people, representing a cross
section of the computer industry. Following is a partial list of the contributors,
including the company that they represented at the time of their contribution:
    Kurt Akeley, Silicon Graphics
    Bill Armstrong, Evans & Sutherland
    Andy Bigos, 3Dlabs
    Pat Brown, IBM
    Jim Cobb, Evans & Sutherland
    Dick Coulter, Digital Equipment
    Bruce D’Amora, GE Medical Systems
    John Dennis, Digital Equipment
    Fred Fisher, Accel Graphics
    Chris Frazier, Silicon Graphics
    Todd Frazier, Evans & Sutherland
    Tim Freese, NCD
    Ken Garnett, NCD
    Mike Heck, Template Graphics Software
    Dave Higgins, IBM
    Phil Huxley, 3Dlabs
    Dale Kirkland, Intergraph
    Hock San Lee, Microsoft
    Kevin LeFebvre, Hewlett Packard
    Jim Miller, IBM
    Tim Misner, SunSoft

                          Version 1.3 - August 14, 2001
C.10. ACKNOWLEDGEMENTS                                251


  Jeremy Morris, 3Dlabs
  Israel Pinkas, Intel
  Bimal Poddar, IBM
  Lyle Ramshaw, Digital Equipment
  Randi Rost, Hewlett Packard
  John Schimpf, Silicon Graphics
  Mark Segal, Silicon Graphics
  Igor Sinyak, Intel
  Jeff Stevenson, Hewlett Packard
  Bill Sweeney, SunSoft
  Kelvin Thompson, Portable Graphics
  Neil Trevett, 3Dlabs
  Linas Vepstas, IBM
  Andy Vesper, Digital Equipment
  Henri Warren, Megatek
  Paula Womack, Silicon Graphics
  Mason Woo, Silicon Graphics
  Steve Wright, Microsoft




                      Version 1.3 - August 14, 2001
Appendix D

Version 1.2

OpenGL version 1.2, released on March 16, 1998, is the second revision since the
original version 1.0. Version 1.2 is upward compatible with version 1.1, meaning
that any program that runs with a 1.1 GL implementation will also run unchanged
with a 1.2 GL implementation.
     Several additions were made to the GL, especially to texture mapping capa-
bilities and the pixel processing pipeline. Following are brief descriptions of each
addition.



D.1     Three-Dimensional Texturing

Three-dimensional textures can be defined and used. In-memory formats for three-
dimensional images, and pixel storage modes to support them, are also defined.
The additions match those of the EXT texture3D extension.
    One important application of three-dimensional textures is rendering volumes
of image data.



D.2     BGRA Pixel Formats

BGRA extends the list of host-memory color formats. Specifically, it provides a
component order matching file and framebuffer formats common on Windows plat-
forms. The additions match those of the EXT bgra extension.

                                        252
D.3. PACKED PIXEL FORMATS                                                         253


D.3     Packed Pixel Formats
Packed pixels in host memory are represented entirely by one unsigned byte, one
unsigned short, or one unsigned integer. The fields with the packed pixel are not
proper machine types, but the pixel as a whole is. Thus the pixel storage modes
and their unpacking counterparts all work correctly with packed pixels.
    The additions match those of the EXT packed pixels extension, with the
further addition of reversed component order packed formats.


D.4     Normal Rescaling
Normals may be rescaled by a constant factor derived from the modelview matrix.
Rescaling can operate faster than renormalization in many cases, while resulting in
the same unit normals.
    The additions are based on the EXT rescale normal extension.


D.5     Separate Specular Color
Lighting calculations are modified to produce a primary color consisting of emis-
sive, ambient and diffuse terms of the usual GL lighting equation, and a secondary
color consisting of the specular term. Only the primary color is modified by the
texture environment; the secondary color is added to the result of texturing to pro-
duce a single post-texturing color. This allows highlights whose color is based on
the light source creating them, rather than surface properties.
    The additions match those of the EXT separate specular color exten-
sion.


D.6     Texture Coordinate Edge Clamping
GL normally clamps such that the texture coordinates are limited to exactly the
range [0, 1]. When a texture coordinate is clamped using this algorithm, the texture
sampling filter straddles the edge of the texture image, taking half its sample values
from within the texture image, and the other half from the texture border. It is
sometimes desirable to clamp a texture without requiring a border, and without
using the constant border color.
    A new texture clamping algorithm, CLAMP TO EDGE, clamps texture coordi-
nates at all mipmap levels such that the texture filter never samples a border texel.
The color returned when clamping is derived only from texels at the edge of the
texture image.

                           Version 1.3 - August 14, 2001
254                                                 APPENDIX D. VERSION 1.2


      The additions match those of the SGIS texture edge clamp extension.


D.7      Texture Level of Detail Control
Two constraints related to the texture level of detail parameter λ are added. One
constraint clamps λ to a specified floating point range. The other limits the se-
lection of mipmap image arrays to a subset of the arrays that would otherwise be
considered.
     Together these constraints allow a large texture to be loaded and used initially
at low resolution, and to have its resolution raised gradually as more resolution is
desired or available. Image array specification is necessarily integral, rather than
continuous. By providing separate, continuous clamping of the λ parameter, it is
possible to avoid ”popping” artifacts when higher resolution images are provided.
     The additions match those of the SGIS texture lod extension.


D.8      Vertex Array Draw Element Range
A new form of DrawElements that provides explicit information on the range of
vertices referred to by the index set is added. Implementations can take advantage
of this additional information to process vertex data without having to scan the
index data to determine which vertices are referenced.
    The additions match those of the EXT draw range elements extension.


D.9      Imaging Subset
The remaining new features are primarily intended for advanced image processing
applications, and may not be present in all GL implementations. The are collec-
tively referred to as the imaging subset.

D.9.1     Color Tables
A new RGBA-format color lookup mechanism is defined in the pixel transfer pro-
cess, providing additional lookup capabilities beyond the existing lookup. The key
difference is that the new lookup tables are treated as one-dimensional images with
internal formats, like texture images and convolution filter images. Thus the new
tables can operate on a subset of the components of passing pixel groups. For ex-
ample, a table with internal format ALPHA modifies only the A component of each
pixel group, leaving the R, G, and B components unmodified.

                          Version 1.3 - August 14, 2001
D.9. IMAGING SUBSET                                                             255


    Three independent lookups may be performed: prior to convolution; after con-
volution and prior to color matrix transformation; after color matrix transformation
and prior to gathering pipeline statistics.
    Methods to initialize the color lookup tables from the framebuffer, in addition
to the standard memory source mechanisms, are provided.
    Portions of a color lookup table may be redefined without reinitializing the
entire table. The affected portions may be specified either from host memory or
from the framebuffer.
    The additions match those of the EXT color table and
EXT color subtable extensions.


D.9.2   Convolution
One- or two-dimensional convolution operations are executed following the first
color table lookup in the pixel transfer process. The convolution kernels are them-
selves treated as one- and two-dimensional images, which can be loaded from ap-
plication memory or from the framebuffer.
    The convolution framework is designed to accommodate three-dimensional
convolution, but that API is left for a future extension.
    The additions match those of the EXT convolution and
HP convolution border modes extensions.


D.9.3   Color Matrix
A 4x4 matrix transformation and associated matrix stack are added to the pixel
transfer path. The matrix operates on RGBA pixel groups, using the equation

                                    C = M C,
where
                                       R
                                             
                                     G
                                   C=
                                     B
                                         

                                       A
    and M is the 4 × 4 matrix on the top of the color matrix stack. After the
matrix multiplication, each resulting color component is scaled and biased by a
programmed amount. Color matrix multiplication follows convolution.
    The color matrix can be used to reassign and duplicate color components. It
can also be used to implement simple color space conversions.
    The additions match those of the SGI color matrix extension.

                          Version 1.3 - August 14, 2001
256                                                APPENDIX D. VERSION 1.2


D.9.4   Pixel Pipeline Statistics
Pixel operations that count occurences of specific color component values (his-
togram) and that track the minimum and maximum color component values (min-
max) are performed at the end of the pixel transfer pipeline. An optional mode
allows pixel data to be discarded after the histogram and/or minmax operations are
completed. Otherwise the pixel data continues on to the next operation unaffected.
    The additions match those of the EXT histogram extension.

D.9.5   Constant Blend Color
A constant color that can be used to define blend weighting factors may be defined.
A typical usage is blending two RGB images. Without the constant blend factor,
one image must have an alpha channel with each pixel set to the desired blend
factor.
    The additions match those of the EXT blend color extension.

D.9.6   New Blending Equations
Blending equations other than the normal weighted sum of source and destination
components may be used.
    Two of the new equations produce the minimum (or maximum) color com-
ponents of the source and destination colors. Taking the maximum is useful for
applications such as maximum projection in medical imaging.
    The other two equations are similar to the default blending equation, but pro-
duce the difference of its left and right hand sides, rather than the sum. Image
differences are useful in many image processing applications.
    The additions match those of the EXT blend minmax and
EXT blend subtract extensions.


D.10     Acknowledgements
OpenGL 1.2 is the result of the contributions of many people, representing a cross
section of the computer industry. Following is a partial list of the contributors,
including the company that they represented at the time of their contribution:
    Kurt Akeley, Silicon Graphics
    Bill Armstrong, Evans & Sutherland
    Otto Berkes, Microsoft
    Pierre-Luc Bisaillon, Matrox Graphics
    Drew Bliss, Microsoft

                          Version 1.3 - August 14, 2001
D.10. ACKNOWLEDGEMENTS                                 257


  David Blythe, Silicon Graphics
  Jon Brewster, Hewlett Packard
  Dan Brokenshire, IBM
  Pat Brown, IBM
  Newton Cheung, S3
  Bill Clifford, Digital
  Jim Cobb, Parametric Technology
  Bruce D’Amora, IBM
  Kevin Dallas, Microsoft
  Mahesh Dandapani, Rendition
  Daniel Daum, AccelGraphics
  Suzy Deffeyes, IBM
  Peter Doyle, Intel
  Jay Duluk, Raycer
  Craig Dunwoody, Silicon Graphics
  Dave Erb, IBM
  Fred Fisher, AccelGraphics / Dynamic Pictures
  Celeste Fowler, Silicon Graphics
  Allen Gallotta, ATI
  Ken Garnett, NCD
  Michael Gold, Nvidia / Silicon Graphics
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
  Don Kuo, S3
  Herb Kuta, Quantum 3D

                       Version 1.3 - August 14, 2001
258                                                    APPENDIX D. VERSION 1.2


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
      Matthew Papakipos, Nvidia / Raycer
      Garry Paxinos, Metro Link
      Hanspeter Pfister, Mitsubishi Electric
      Richard Pimentel, Parametric Technology
      Bimal Poddar, IBM / Intel
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
      Kartik Venkataraman, Intel
      Andy Vesper, Digital Equipment

                            Version 1.3 - August 14, 2001
D.10. ACKNOWLEDGEMENTS                                259


  Henri Warren, Digital Equipment / Megatek
  Paula Womack, Silicon Graphics
  Steve Wright, Microsoft
  David Yu, Silicon Graphics
  Randy Zhao, S3




                      Version 1.3 - August 14, 2001
Appendix E

Version 1.2.1

OpenGL version 1.2.1, released on October 14, 1998, introduced ARB extensions
(see Appendix G). The only ARB extension defined in this version is multitexture,
allowing application of multiple textures to a fragment in one rendering pass. Mul-
titexture is based on the SGIS multitexture extension, simplified by removing
the ability to route texture coordinate sets to arbitrary texture units.
     A new corollary discussing display list and immediate mode invariance was
added to Appendix B on April 1, 1999.




                                       260
Appendix F

Version 1.3

OpenGL version 1.3, released on August 14, 2001, is the third revision since the
original version 1.0. Version 1.3 is upward compatible with earlier versions, mean-
ing that any program that runs with a 1.2, 1.1, or 1.0 GL implementation will also
run unchanged with a 1.3 GL implementation.
    Several additions were made to the GL, especially texture mapping capabilities
previously defined by ARB extensions. Following are brief descriptions of each
addition.


F.1    Compressed Textures
Compressing texture images can reduce texture memory utilization and improve
performance when rendering textured primitives. The GL provides a framework
upon which extensions providing specific compressed image formats can be built,
and a set of generic compressed internal formats that allow applications to specify
that texture images should be stored in compressed form without needing to code
for specific compression formats (specific compressed formats, such as S3TC or
FXT1, are supported by extensions).
    Texture        compression         was        promoted         from         the
GL ARB texture compression extension.


F.2    Cube Map Textures
Cube map textures provide a new texture generation scheme for looking up textures
from a set of six two-dimensional images representing the faces of a cube. The
(str) texture coordinates are treated as a direction vector emanating from the center
of a cube. At texture generation time, the interpolated per-fragment (str) selects

                                        261
262                                                  APPENDIX F. VERSION 1.3


one cube face two-dimensional image based on the largest magnitude coordinate
(the major axis). A new (st) is calculated by dividing the two other coordinates
(the minor axes values) by the major axis value, and the new (st) is used to lookup
into the selected two-dimensional texture image face of the cube map.
    Two new texture coordinate generation modes are provided for use in con-
junction with cube map texturing. The REFLECTION MAP mode generates tex-
ture coordinates (str) matching the vertex’s eye-space reflection vector, useful for
environment mapping without the singularity inherent in SPHERE MAP mapping.
The NORMAL MAP mode generates texture coordinates matching the vertex’s trans-
formed eye-space normal, useful for texture-based diffuse lighting models.
    Cube mapping was promoted from the GL ARB texture cube map extension.


F.3    Multisample
Multisampling provides a antialiasing mechanism which samples all primitives
multiple times at each pixel. The color sample values are resolved to a single, dis-
playable color each time a pixel is updated, so antialiasing appears to be automatic
at the application level. Because each sample includes depth and stencil infor-
mation, the depth and stencil functions perform equivalently to the single-sample
mode.
    When multisampling is supported, an additional buffer, called the multisample
buffer, is added to the framebuffer. Pixel sample values, including color, depth, and
stencil values, are stored in this buffer.
    Multisampling is usually an expensive operation, so it is usually not supported
on all contexts. Applications must obtain a multisample-capable context using the
new interfaces provided by GLX 1.4 or by the WGL ARB multisample extension.
    Multisampling was promoted from the GL ARB multisample extension; The
definition of the extension was changed slightly to support both multisampling and
supersampling implementations.


F.4    Multitexture
Multitexture adds support for multiple texture units. The capabilities of the mul-
tiple texture units are identical, except that evaluation and feedback are supported
only for texture unit 0. Each texture unit has its own state vector which includes
texture vertex array specification, texture image and filtering parameters, and tex-
ture environment application.
    The texture environments of the texture units are applied in a pipelined fashion
whereby the output of one texture environment is used as the input fragment color

                          Version 1.3 - August 14, 2001
F.5. TEXTURE ADD ENVIRONMENT MODE                                                  263


for the next texture environment. Changes to texture client state and texture server
state are each routed through one of two selectors which control which instance of
texture state is affected.
    Multitexture was promoted from the GL ARB multitexture extension.


F.5    Texture Add Environment Mode
The TEXTURE ENV MODE texture environment function ADD provides a texture
function to add incoming fragment and texture source colors.
    Texture add mode was promoted from the GL ARB texture env add exten-
sion.


F.6    Texture Combine Environment Mode
The TEXTURE ENV MODE texture environment function COMBINE provides a wide
range of programmable combiner functions using the incoming fragment color,
texture source color, texture constant color, and the result of the previous texture
environment stage as possible parameters.
    Combiner operations include passthrough, multiplication, addition and biased
addition, subtraction, and linear interpolation of specified parameters. Different
combiner operations may be selected for RGB and A components, and the final
result may be scaled by 1, 2, or 4.
    Texture combine was promoted from the GL ARB texture env combine ex-
tension.


F.7    Texture Dot3 Environment Mode
The TEXTURE ENV MODE COMBINE operations also provide three-component dot
products of specified parameters, with the resulting scalar value replicated into the
RGB or RGBA components of the output color. The dot product is performed
using pseudo-signed arithmetic to enable per-pixel lighting computations.
    Texture DOT3 mode was promoted from the GL ARB texture env dot3 ex-
tension.


F.8    Texture Border Clamp
The texture wrap parameter CLAMP TO BORDER mode clamps texture coordinates
at all mipmap levels such that when the texture filter straddles an edge of the texture

                           Version 1.3 - August 14, 2001
264                                                 APPENDIX F. VERSION 1.3


image, the color returned is derived only from border texels. This behavior mirrors
the behavior of the texture edge clamp mode introduced by OpenGL 1.2.
    Texture       border       clamp        was      promoted        from       the
GL ARB texture border clamp extension.


F.9    Transpose Matrix
New functions and tokens are added allowing application matrices stored in row
major order rather than column major order to be transferred to the implementa-
tion. This allows an application to use standard C-language 2-dimensional arrays
and have the array indices match the expected matrix row and column indexes.
These arrays are referred to as transpose matrices since they are the transpose of
the standard matrices passed to OpenGL.
    Transpose matrix adds an interface for transfering data to and from the OpenGL
pipeline. It does not change any OpenGL processing or imply any changes in state
representation.
    Transpose matrix was promoted from the GL ARB transpose matrix exten-
sion.


F.10     Acknowledgements
OpenGL 1.3 is the result of the contributions of many people. Following is a partial
list of the contributors, including the company that they represented at the time of
their contribution:
     Adrian Muntianu, ATI
     Al Reyes, 3dfx
     Alain Bouchard, Matrox
     Alan Commike, SGI
     Alan Heirich, Compaq
     Alex Herrera, SP3D
     Allen Akin, VA Linux
     Allen Gallotta, ATI
     Alligator Descartes, Arcane
     Andy Vesper, MERL
     Andy Wolf, Diamond Multimedia
     Axel Schildan, S3
     Barthold Lichtenbelt, 3Dlabs
     Benj Lipchak, Compaq
     Bill Armstrong, Evans & Sutherland

                          Version 1.3 - August 14, 2001
F.10. ACKNOWLEDGEMENTS                                 265


  Bill Clifford, Intel
  Bill Mannel, SGI
  Bimal Poddar, Intel
  Bob Beretta, Apple
  Brent Insko, NVIDIA
  Brian Goldiez, UCF
  Brian Greenstone, Apple
  Brian Paul, VA Linux
  Brian Sharp, GLSetup
  Bruce D’Amora, IBM
  Bruce Stockwell, Compaq
  Chris Brady, Alt.software
  Chris Frazier, Raycer
  Chris Hall, 3dlabs
  Chris Hecker, GLSetup
  Chris Lane, Intel
  Chris Thornborrow, PixelFusion
  Christopher Fraser, IMG
  Chuck Smith, Intelligraphics
  Craig Dunwoody, SGI
  Dairsie Latimer, PixelFusion
  Dale Kirkland, 3Dlabs / Intergraph
  Dan Brokenshire, IBM
  Dan Ginsburg, ATI
  Dan McCabe, S3
  Dave Aronson, Microsoft
  Dave Gosselin, ATI
  Dave Shreiner, SGI
  Dave Zenz, Dell
  David Aronson, Microsoft
  David Blythe, SGI
  David Kirk, NVIDIA
  David Story, SGI
  David Yu, SGI
  Deanna Hohn, 3dfx
  Dick Coulter, Silicon Magic
  Don Mullis, 3dfx
  Eamon O Dea, PixelFusion
  Edward (Chip) Hill, Pixelfusion
  Eiji Obata, NEC

                       Version 1.3 - August 14, 2001
266                                               APPENDIX F. VERSION 1.3


      Elio Del Giudice, Matrox
      Eric Young, S3
      Evan Hart, ATI
      Fred Fisher, 3dLabs
      Garry Paxinos, Metro Link
      Gary Tarolli, 3dfx
      George Kyriazis, NVIDIA
      Graham Connor, IMG
      Herb Kuta, Quantum3D
      Howard Miller, Apple
      Igor Sinyak, Intel
      Jack Middleton, Sun
      James Bowman, 3dfx
      Jan C. Hardenbergh, MERL
      Jason Mitchell, ATI
      Jeff Weyman, ATI
      Jeffrey Newquist, 3dfx
      Jens Owen, Precision Insight
      Jeremy Morris, 3Dlabs
      Jim Bushnell, Pyramid Peak
      John Dennis, Sharp Eye
      John Metcalfe, IMG
      John Stauffer, Apple
      John Tynan, PixelFusion
      John W. Polick, NEC
      Jon Khazam, Intel
      Jon Leech, SGI
      Jon Paul Schelter, Matrox
      Karl Hilleslad, NVIDIA
      Kelvin Thompson
      Ken Cameron, Pixelfusion
      Ken Dyke, Apple
      Ken Nicholson, SGI
      Kent Lin, Intel
      Kevin Lefebvre, HP
      Kevin Martin, VA Linux
      Kurt Akeley, SGI
      Les Silvern, NEC
      Mahesh Dandipani, Rendition
      Martin Amon, 3dfx

                          Version 1.3 - August 14, 2001
F.10. ACKNOWLEDGEMENTS                                267


  Martina Sourada, ATI
  Matt Lavoie, Pixelfusion
  Matt Russo, Matrox
  Matthew Papakipos, NVIDIA
  Michael Gold, NVIDIA
  Miriam Geller, SGI
  Morgan Von Essen, Metro Link
  Naruki Aruga, PFU
  Nathan Tuck, Raycer Graphics
  Neil Trevett, 3Dlabs
  Newton Cheung, S3
  Nick Triantos, NVIDIA
  Patrick Brown, Intel
  Paul Jensen, 3dfx
  Paul Keller, NVIDIA
  Paul Martz, HP
  Paula Womack, 3dfx
  Peter Doenges, Evans & Sutherland
  Peter Graffagnino, Apple
  Phil Huxley, 3Dlabs
  Ralf Biermann, Elsa AG
  Randi Rost, 3Dlabs
  Renee Rashid, Micron
  Rich Johnson, HP
  Richard Pimentel, PTC
  Richard Schlein, Apple
  Rick Hammerstone, ATI
  Rik Faith, VA Linux
  Rob Glidden, Sun
  Rob Wheeler, 3dfx
  Shari Petersen, Rendition
  Shawn Hopwood, SGI
  Steve Glickman, Silicon Magic
  Steve McGuigan, SGI
  Steve Wright, Microsoft
  Stuart Anderson, Metro Link
  T. C. Zhao, MERL
  Teri Morrison, HP
  Thomas Fox, IBM
  Tim Kelley, Real 3D

                      Version 1.3 - August 14, 2001
268                                               APPENDIX F. VERSION 1.3


      Tom Frisinger, ATI
      Victor Vedovato, Micron
      Vikram Simha, MERL
      Yanjun Zhang, Sun
      Zahid Hussain, TI




                          Version 1.3 - August 14, 2001
Appendix G

ARB Extensions

OpenGL extensions that have been approved by the OpenGL Architectural Review
Board (ARB) are described in this chapter. These extensions are not required to be
supported by a conformant OpenGL implementation, but are expected to be widely
available; they define functionality that is likely to move into the required feature
set in a future revision of the specification.
     In order not to compromise the readability of the core specification, ARB ex-
tensions are not integrated into the core language; instead, they are made available
online in the OpenGL Extension Registry (as are a much larger number of vendor-
specific extensions, as well as extensions to GLX and WGL). Extensions are doc-
umented as changes to the Specification. The Registry is available on the World
Wide Web at URL

                http://oss.sgi.com/projects/ogl-sample/registry/

Brief descriptions of ARB extensions are provided below.


G.1     Naming Conventions
To distinguish ARB extensions from core OpenGL features and from vendor-
specific extensions, the following naming conventions are used:

   • A unique name string of the form "GL ARB name" is associated with each
     extension. If the extension is supported by an implementation, this string
     will be present in the EXTENSIONS string described in section 6.1.11.

   • All functions defined by the extension will have names of the form Func-
     tionARB

                                        269
270                                         APPENDIX G. ARB EXTENSIONS


   • All enumerants defined by the extension will have names of the form
     NAME ARB.



G.2     Promoting Extensions to Core Features
ARB extensions can be promoted to required core features in later revisions of
OpenGL. When this occurs, the extension specifications are merged into the core
specification. Functions and enumerants that are part of such promoted extensions
will have the ARB affix removed
     GL implementations of such later revisions should continue to export the name
strings of promoted extensions in the EXTENSIONS string, and continue to support
the ARB-affixed versions of functions and enumerants as a transition aid.


G.3     Multitexture
The name string for multitexture is GL ARB multitexture.
   Multitexture was promoted to a core feature in OpenGL 1.3 (see appendix F).


G.4     Transpose Matrix
The name string for transpose matrix is GL ARB transpose matrix.
   Transpose matrix was promoted to a core feature in OpenGL 1.3 (see ap-
pendix F).


G.5     Multisample
The name string for multisample is GL ARB multisample.
    Multisample was promoted to a core feature in OpenGL 1.3, and is described
in appendix F.


G.6 Texture Add Environment Mode
The name string for texture add mode is GL ARB texture env add.
   Texture add mode was promoted to a core feature in OpenGL 1.3 (see ap-
pendix F).

                          Version 1.3 - August 14, 2001
G.7. CUBE MAP TEXTURES                                                            271


G.7     Cube Map Textures
The name string for cube mapping is GL ARB texture cube map.
   Cube mapping was promoted to a core feature in OpenGL 1.3 (see appendix F).


G.8     Compressed Textures
The name string for compressed textures is GL ARB texture compression.
   Compressed texture was promoted to a core feature in OpenGL 1.3 (see ap-
pendix F).


G.9     Texture Border Clamp
The name string for texture border clamp is GL ARB texture border clamp.
   Border clamp was promoted to a core feature in OpenGL 1.3 (see appendix F).


G.10      Point Parameters
Point parameters supports additional geometric characteristics of points, allowing
the size of a point to be affected by linear or quadratic distance attenuation, and
increasing control of the mapping from point size to raster point area and point
transparency.
    The name string for point parameters is GL ARB point parameters.


G.11      Vertex Blend
Vertex blending replaces the single modelview transformation with multiple vertex
units. Each unit has its own transform matrix and an associated current weight.
Vertices are transformed by all the enabled units, scaled by their respective weights,
and summed to create the eye-space vertex. Normals are similarly transformed by
the inverse transpose of the modelview matrices.
    The name string for vertex blend is GL ARB vertex blend.


G.12      Matrix Palette
Matrix palette extends vertex blending to include a palette of modelview matrices.
Each vertex may be transformed by a different set of matrices chosen from the
palette.

                           Version 1.3 - August 14, 2001
272                                          APPENDIX G. ARB EXTENSIONS


      The name string for matrix palette is GL ARB matrix palette.


G.13       Texture Combine Environment Mode
The name string for texture combine mode is GL ARB texture env combine.
   Texture combine was promoted to a core feature in OpenGL 1.3 (see ap-
pendix F).


G.14       Texture Crossbar Environment Mode
Texture crossbar extends the texture combine environment mode by allowing use
of the texture color from different texture units as sources to the texture combine
function.
    The       name      string      for      texture     crossbar       mode      is
GL ARB texture env crossbar.


G.15       Texture Dot3 Environment Mode
The name string for DOT3 is GL ARB texture env dot3.
   DOT3 was promoted to a core feature in OpenGL 1.3 (see appendix F).




                          Version 1.3 - August 14, 2001
Index of OpenGL Commands

x BIAS, 82, 228                               ALWAYS, 159–161, 226
x SCALE, 82, 228                              AMBIENT, 51, 52, 54
2D, 191, 192, 239                             AMBIENT AND DIFFUSE, 51, 52, 54
2 BYTES, 194                                  AND, 166
3D, 191, 192                                  AND INVERTED, 166
3D COLOR, 191, 192                            AND REVERSE, 166
3D COLOR TEXTURE, 191, 192                    Antialiasing, 72
3 BYTES, 194                                  AreTexturesResident, 145, 146, 195
4D COLOR TEXTURE, 191, 192                    ArrayElement, 19, 23–25, 193
4 BYTES, 194                                  AUTO NORMAL, 184
                                              AUXi, 168
1, 117, 125, 126, 143, 202, 222               AUXn, 168, 175
2, 117, 125, 126, 202, 222                    AUX0, 168, 175
3, 117, 125, 126, 202, 222
4, 117, 125, 126, 202                         BACK, 50, 51, 53, 73, 76, 168, 175, 199,
                                                       220
ACCUM, 172                                    BACK LEFT, 168, 175
Accum, 172                                    BACK RIGHT, 168, 175
ACCUM BUFFER BIT, 170, 208                    Begin, 12, 13, 15–19, 24, 25, 28, 56, 66,
ACTIVE TEXTURE, 20, 35, 42, 146,                       70, 73, 76, 185, 186, 191
         183, 198, 199                        BGR, 95, 176, 177
ActiveTexture, 35, 152                        BGRA, 95, 97, 101, 176, 252
ADD, 147, 149, 150, 172, 263                  BindTexture, 144, 145
ADD SIGNED, 150                               BITMAP, 75, 83, 86, 93, 94, 101, 114,
ALL ATTRIB BITS, 207, 208                              177, 202
ALPHA, 82, 95, 106, 107, 118–120,             Bitmap, 114
         147–149, 176, 177, 202, 228,         BITMAP TOKEN, 192
         229, 231, 238, 248, 254              BLEND, 147, 149, 162, 166
ALPHA12, 119                                  BlendColor, 81, 162
ALPHA16, 119                                  BlendEquation, 81, 162, 163
ALPHA4, 119                                   BlendFunc, 81, 162, 163
ALPHA8, 119                                   BLUE, 82, 95, 176, 177, 228, 229, 231,
ALPHA BIAS, 104                                        238
ALPHA SCALE, 104, 147                         BLUE BIAS, 104
ALPHA TEST, 159                               BLUE SCALE, 104
AlphaFunc, 159                                BYTE, 22, 94, 177, 178, 194

                                        273
274                                                                        INDEX


C3F V3F, 26, 27                              COLOR    TABLE BLUE SIZE, 203
C4F N3F V3F, 26, 27                          COLOR    TABLE FORMAT, 203
C4UB V2F, 26, 27                             COLOR    TABLE GREEN SIZE, 203
C4UB V3F, 26, 27                             COLOR    TABLE INTENSITY SIZE,
CallList, 19, 193, 194                                 203
CallLists, 19, 193, 194                      COLOR TABLE LUMINANCE SIZE,
CCW, 50, 220                                           203
CLAMP, 133, 134, 138                         COLOR TABLE RED SIZE, 203
CLAMP TO BORDER, 133, 134, 263               COLOR TABLE SCALE, 83–85, 203
CLAMP TO EDGE, 133, 134, 138, 253            COLOR TABLE WIDTH, 203
CLEAR, 166                                   ColorMask, 169, 170
Clear, 170, 171                              ColorMaterial, 51, 53, 54, 184, 245, 250
ClearAccum, 171                              ColorPointer, 19, 22, 23, 26, 195
ClearColor, 170                              ColorSubTable, 85
ClearDepth, 171                              ColorTable, 82, 84–86, 110, 111, 195
ClearIndex, 170                              ColorTableParameter, 84
ClearStencil, 171                            ColorTableParameterfv, 83
CLIENT ACTIVE TEXTURE, 23, 198,              Colorub, 57
           199                               Colorui, 57
CLIENT ALL ATTRIB BITS, 207, 208             Colorus, 57
CLIENT PIXEL STORE BIT, 208                  COMBINE, 147, 150, 152, 263
CLIENT VERTEX ARRAY BIT, 208                 COMBINE ALPHA, 147, 150–152
ClientActiveTexture, 23, 195                 COMBINE RGB, 147, 150–152
CLIP PLANEi, 40                              COMPILE, 193, 245
CLIP PLANE0, 40                              COMPILE AND EXECUTE, 193, 194
ClipPlane, 40                                COMPRESSED ALPHA, 120
COEFF, 200                                   COMPRESSED INTENSITY, 120
COLOR, 31, 35, 85, 88, 89, 125, 180          COMPRESSED LUMINANCE, 120
Color, 19, 21, 44, 57                        COMPRESSED LUMINANCE ALPHA,
Color3, 21                                             120
Color4, 21                                   COMPRESSED RGB, 120
COLOR ARRAY, 23, 26                          COMPRESSED RGBA, 120
COLOR ARRAY POINTER, 206                     COMPRESSED TEXTURE FORMATS,
COLOR BUFFER BIT, 170, 171, 208                        117
COLOR INDEX, 75, 83, 86, 93, 95,             CompressedTexImage, 131
           105, 114, 176, 180, 201, 202      CompressedTexImage1D, 129–131
COLOR INDEXES, 52, 55                        CompressedTexImage2D, 129–131
COLOR LOGIC OP, 166                          CompressedTexImage3D, 129–131
COLOR MATERIAL, 51, 54                       CompressedTexSubImage1D, 130–132
COLOR MATRIX, 203                            CompressedTexSubImage2D, 130–132
COLOR MATRIX STACK DEPTH,                    CompressedTexSubImage3D, 130–132
           203                               CONSTANT, 149, 151, 225
COLOR TABLE, 83, 86, 105                     CONSTANT ALPHA, 81, 163, 164
COLOR TABLE ALPHA SIZE, 203                  CONSTANT ATTENUATION, 52
COLOR TABLE BIAS, 83, 84, 203                CONSTANT BORDER, 108, 109

                           Version 1.3 - August 14, 2001
INDEX                                                                         275


CONSTANT COLOR, 81, 163, 164               DECAL, 147, 148
CONVOLUTION 1D, 87, 89, 106, 122,          DECR, 160
          204                              DeleteLists, 195
CONVOLUTION 2D, 86–88, 106, 122,           DeleteTextures, 145, 195
          204                              DEPTH, 180, 228
CONVOLUTION BORDER COLOR,                  DEPTH BIAS, 82, 104
          108, 204                         DEPTH BUFFER BIT, 170, 171, 208
CONVOLUTION BORDER MODE,                   DEPTH COMPONENT, 83, 86, 93, 95,
          108, 204                                   116, 173, 176, 180, 201
CONVOLUTION FILTER BIAS,                   DEPTH SCALE, 82, 104
          86–88, 204                       DEPTH TEST, 161
CONVOLUTION FILTER SCALE,                  DepthFunc, 161
          86–89, 204                       DepthMask, 169, 170
CONVOLUTION FORMAT, 204                    DepthRange, 30, 198, 245
CONVOLUTION HEIGHT, 204                    DIFFUSE, 51, 52
CONVOLUTION WIDTH, 204                     Disable, 36, 39, 40, 46, 51, 62, 63, 66,
ConvolutionFilter1D, 87–89                           69, 73, 75, 77, 110–112, 149,
ConvolutionFilter2D, 86–89                           154, 158–162, 165, 166, 183,
ConvolutionParameter, 87, 108                        184
ConvolutionParameterfv, 86, 87, 108        DisableClientState, 19, 22, 23, 26, 28,
ConvolutionParameteriv, 88, 108                      195
COPY, 166, 226                             DITHER, 165
COPY INVERTED, 166                         DOMAIN, 200
COPY PIXEL TOKEN, 192                      DONT CARE, 196, 234
CopyColorSubTable, 85                      DOT3 RGB, 150
CopyColorTable, 84, 85                     DOT3 RGBA, 150
CopyConvolutionFilter1D, 89                DOUBLE, 22
CopyConvolutionFilter2D, 88                DRAW PIXEL TOKEN, 192
CopyPixels, 79, 81, 84, 85, 88, 89, 106,   DrawArrays, 24, 193
          125, 173, 177, 179, 180, 190     DrawBuffer, 167–171
CopyTexImage1D, 106, 125, 127, 140         DrawElements, 24, 25, 193, 254
CopyTexImage2D, 106, 125, 127, 140         DrawPixels, 75, 79–81, 83, 86, 92–96,
CopyTexImage3D, 127                                  101, 103, 106, 113, 114, 116,
CopyTexSubImage1D, 106, 126–129                      173, 177, 180, 190
CopyTexSubImage2D, 106, 126–129            DrawRangeElements, 25, 193, 237
CopyTexSubImage3D, 106, 126, 127,          DST ALPHA, 164
          129                              DST COLOR, 164
CULL FACE, 73
CullFace, 73, 78                           EDGE FLAG ARRAY, 23, 26
CURRENT BIT, 208                           EDGE FLAG ARRAY POINTER, 206
CURRENT RASTER TEXTURE COORDS,             EdgeFlag, 18, 19
          42, 244                          EdgeFlagPointer, 19, 22, 23, 195
CURRENT TEXTURE COORDS, 20                 EdgeFlagv, 18
CW, 50                                     EMISSION, 51, 52

                        Version 1.3 - August 14, 2001
276                                                                           INDEX


Enable, 36, 39, 40, 46, 51, 62, 63, 66, 69,     EXTENSIONS, 81, 206, 207, 269, 270
          73, 75, 77, 110–112, 149, 154,        EYE LINEAR, 38, 39, 199, 225
          158–161, 165, 166, 183, 184,          EYE PLANE, 38
          197
ENABLE BIT, 208                                 FALSE, 18, 47, 49, 79, 80, 82, 90, 91,
EnableClientState, 19, 22, 23, 26, 28,                    101, 104, 112, 113, 143, 146,
          195                                             159, 175, 198, 202, 205
End, 12, 13, 15–19, 24, 25, 28, 56, 66,         FASTEST, 196
          73, 76, 185, 186, 191                 FEEDBACK, 188–190, 246
EndList, 193                                    FEEDBACK BUFFER POINTER, 206
EQUAL, 159–161                                  FeedbackBuffer, 189, 190, 195
EQUIV, 166                                      FILL, 76–79, 185, 220, 245, 248
EVAL BIT, 208                                   Finish, 195, 196, 244
EvalCoord, 19, 183, 184                         FLAT, 56, 245
EvalCoord1, 184–186                             FLOAT, 22, 26–28, 94, 177, 178, 194,
EvalCoord1d, 185                                          214, 215
EvalCoord1f, 185                                Flush, 195, 244
EvalCoord2, 184–186                             FOG, 154
EvalMesh1, 185                                  Fog, 154, 155
EvalMesh2, 185, 186                             FOG BIT, 208
EvalPoint, 19                                   FOG COLOR, 155
EvalPoint1, 186                                 FOG DENSITY, 154
EvalPoint2, 186                                 FOG END, 154
EXP, 154, 155, 217                              FOG HINT, 196
EXP2, 154                                       FOG INDEX, 155
EXT bgra, 252                                   FOG MODE, 154, 155
EXT blend color, 256                            FOG START, 154
EXT blend logic op, 248                         FRONT, 50, 51, 54, 73, 76, 168, 175,
EXT blend minmax, 256                                     199
EXT blend subtract, 256                         FRONT AND BACK, 50, 51, 53, 54,
EXT color subtable, 255                                   73, 76, 168
EXT color table, 255                            FRONT LEFT, 168, 175
EXT convolution, 255                            FRONT RIGHT, 168, 175
EXT copy texture, 249                           FrontFace, 50, 73
EXT draw range elements, 254                    Frustum, 33, 34, 245
EXT histogram, 256                              FUNC ADD, 162, 163, 165, 226
EXT packed pixels, 253                          FUNC REVERSE SUBTRACT, 163
EXT polygon offset, 248                         FUNC SUBTRACT, 162
EXT rescale normal, 253
EXT separate specular color, 253                GenLists, 194, 195
EXT subtexture, 249                             GenTextures, 145, 195, 202
EXT texture, 248, 249                           GEQUAL, 159–161
EXT texture3D, 252                              Get, 20, 31, 42, 195, 197, 198
EXT texture object, 249                         GetBooleanv, 159, 197, 198, 209, 211
EXT vertex array, 247                           GetClipPlane, 199

                              Version 1.3 - August 14, 2001
INDEX                                                                            277


GetColorTable, 86, 175, 203                   GL ARB texture env crossbar, 272
GetColorTableParameter, 203                   GL ARB texture env dot3, 263, 272
GetCompressedTexImage,         130–132,       GL ARB transpose matrix, 264, 270
          196, 200–202                        GL ARB vertex blend, 271
GetConvolutionFilter, 175, 204                GREATER, 159–161
GetConvolutionParameter, 204                  GREEN, 82, 95, 176, 177, 228, 229, 231,
GetConvolutionParameteriv, 87                        238
GetDoublev, 197, 198, 209, 211                GREEN BIAS, 104
GetError, 11                                  GREEN SCALE, 104
GetFloatv, 159, 197, 198, 203, 209, 211
GetHistogram, 91, 175, 204                    Hint, 196
GetHistogramParameter, 205                    HINT BIT, 208
GetIntegerv, 25, 35, 62, 197, 198, 203,       HISTOGRAM, 90, 91, 112, 205
          209, 211                            Histogram, 90, 91, 112, 195
GetLight, 199                                 HISTOGRAM ALPHA SIZE, 205
GetMap, 199, 200                              HISTOGRAM BLUE SIZE, 205
GetMaterial, 199                              HISTOGRAM FORMAT, 205
GetMinmax, 175, 205                           HISTOGRAM GREEN SIZE, 205
GetMinmaxParameter, 206                       HISTOGRAM LUMINANCE SIZE,
GetPixelMap, 199, 200                                   205
GetPointerv, 206                              HISTOGRAM RED SIZE, 205
GetPolygonStipple, 202                        HISTOGRAM SINK, 205
GetSeparableFilter, 175, 204                  HISTOGRAM WIDTH, 205
GetString, 206, 207                           HP convolution border modes, 255
GetTexEnv, 199
GetTexGen, 199                                INCR, 160
GetTexImage, 106, 144, 201, 203–205           INDEX, 238
GetTexImage1D, 175                            Index, 19, 21
GetTexImage2D, 175                            INDEX ARRAY, 23, 26
GetTexImage3D, 175                            INDEX ARRAY POINTER, 206
GetTexLevelParameter, 199, 200                INDEX LOGIC OP, 166
GetTexParameter, 199                          INDEX OFFSET, 82, 104, 228
GetTexParameterfv, 144, 146                   INDEX SHIFT, 82, 104, 228
GetTexParameteriv, 144, 146                   IndexMask, 169, 170
GL ARB matrix palette, 272                    IndexPointer, 19, 22, 23, 195
GL ARB multisample, 262, 270                  InitNames, 187
GL ARB multitexture, 263, 270                 INT, 22, 94, 177, 178, 194
GL ARB point parameters, 271                  INTENSITY, 90, 91, 106, 107, 118–120,
GL ARB texture border clamp,        264,                148, 149, 202, 229, 248
          271                                 INTENSITY12, 90, 91, 119
GL ARB texture compression, 261, 271          INTENSITY16, 90, 91, 119
GL ARB texture cube map, 262, 271             INTENSITY4, 90, 91, 119
GL ARB texture env add, 263, 270              INTENSITY8, 90, 91, 119
GL ARB texture env combine,         263,      InterleavedArrays, 19, 26, 27, 195
          272                                 INTERPOLATE, 150

                            Version 1.3 - August 14, 2001
278                                                                         INDEX


INVALID ENUM, 12, 23, 35, 38, 39,             LINEAR ATTENUATION, 52
          50, 80, 86, 90, 91, 93, 125,        LINEAR MIPMAP LINEAR, 133, 139,
          129, 131, 144, 201                            140
INVALID OPERATION, 12, 19, 80, 93,            LINEAR MIPMAP NEAREST, 133,
          97, 129–132, 144, 168, 172,                   139, 140
          173, 175, 176, 183, 187–189,        LINES, 15, 70
          193, 200, 202                       LineStipple, 69
INVALID VALUE, 12, 22, 25, 31, 34,            LineWidth, 66
          51, 63, 66, 79, 81, 82, 84, 85,     LIST BIT, 208
          87, 90, 117, 120–122, 125–          ListBase, 194, 195
          128, 130, 131, 140, 146, 154,       LOAD, 172
          158, 170, 182, 183, 185, 193,       LoadIdentity, 32
          200–202                             LoadMatrix, 31, 32
INVERT, 160, 166                              LoadMatrix[fd], 32
IsEnabled, 158, 195, 197, 209, 211            LoadName, 187
IsList, 195                                   LoadTransposeMatrix, 32
IsTexture, 195, 202                           LoadTransposeMatrix[fd], 32
                                              LOGIC OP, 166
KEEP, 160, 161, 226                           LogicOp, 166
                                              LUMINANCE, 95, 102, 106, 107, 117–
LEFT, 168, 175                                          120, 148, 149, 176, 177, 202,
LEQUAL, 159–161                                         229, 231, 248
LESS, 159–161, 226                            LUMINANCE12, 119
Light, 50–52                                  LUMINANCE12 ALPHA12, 119
LIGHTi, 50, 51, 246                           LUMINANCE12 ALPHA4, 119
LIGHT0, 50                                    LUMINANCE16, 119
LIGHT MODEL AMBIENT, 52                       LUMINANCE16 ALPHA16, 119
LIGHT MODEL COLOR CONTROL,                    LUMINANCE4, 119
          52                                  LUMINANCE4 ALPHA4, 119
LIGHT MODEL LOCAL VIEWER,                     LUMINANCE6 ALPHA2, 119
          52                                  LUMINANCE8, 119
LIGHT MODEL TWO SIDE, 52                      LUMINANCE8 ALPHA8, 119
LIGHTING, 46                                  LUMINANCE ALPHA, 95, 102, 106,
LIGHTING BIT, 208                                       107, 117–120, 148, 149, 176,
LightModel, 50, 52                                      177, 202
LINE, 76–78, 185, 186, 220, 248
LINE BIT, 208                                 Map1, 181–183, 198
LINE LOOP, 15                                 MAP1 COLOR 4, 182
LINE RESET TOKEN, 192                         MAP1 INDEX, 182
LINE SMOOTH, 66, 72                           MAP1 NORMAL, 182
LINE SMOOTH HINT, 196                         MAP1 TEXTURE COORD          1, 182, 184
LINE STIPPLE, 69                              MAP1 TEXTURE COORD          2, 182, 184
LINE STRIP, 15, 185                           MAP1 TEXTURE COORD          3, 182
LINE TOKEN, 192                               MAP1 TEXTURE COORD          4, 182
LINEAR, 133, 138, 140, 141, 143, 154          MAP1 VERTEX 3, 182

                            Version 1.3 - August 14, 2001
INDEX                                                                279


MAP1 VERTEX 4, 182                     MultiTexCoord, 20, 23, 35
Map2, 182, 183, 198                    MultMatrix, 31–33
MAP2 VERTEX 3, 184                     MultMatrix[fd], 32
MAP2 VERTEX 4, 184                     MultTransposeMatrix, 32
MAP COLOR, 82, 104, 105                MultTransposeMatrix[fd], 32
MAP STENCIL, 82, 105
MAP VERTEX 3, 184                      N3F V3F, 26, 27
MAP VERTEX 4, 184                      NAND, 166
Map{12}, 183                           NEAREST, 133, 137, 140, 141
MapGrid1, 185                          NEAREST MIPMAP LINEAR, 133,
MapGrid2, 185                                   139–141, 143
Material, 19, 50–52, 55, 245           NEAREST MIPMAP NEAREST, 133,
MatrixMode, 31                                  139–141
MAX, 163                               NEVER, 159–161
MAX 3D TEXTURE SIZE, 121               NewList, 193, 194
MAX ATTRIB STACK DEPTH, 207            NICEST, 196
MAX CLIENT ATTRIB STACK DEPTH,         NO ERROR, 11
          207                          NONE, 167–169, 171
MAX COLOR MATRIX STACK DEPTH,          NOOP, 166
          203                          NOR, 166
MAX CONVOLUTION HEIGHT, 87,            Normal, 19, 20
          204                          Normal3, 8, 20
MAX CONVOLUTION WIDTH, 87,             Normal3d, 8
          204                          Normal3dv, 8
MAX CUBE MAP TEXTURE SIZE,             Normal3f, 8
          121                          Normal3fv, 8
MAX ELEMENTS INDICES, 25               NORMAL ARRAY, 23, 28
MAX ELEMENTS VERTICES, 25              NORMAL ARRAY POINTER, 206
MAX EVAL ORDER, 182, 183               NORMAL MAP, 38, 39, 262
MAX PIXEL MAP TABLE, 82, 104           NORMALIZE, 36
MAX TEXTURE SIZE, 121                  NormalPointer, 19, 22, 23, 28, 195
MAX TEXTURE UNITS, 13, 20, 21,         NOTEQUAL, 159–161
          28, 209                      NUM COMPRESSED TEXTURE FORMATS,
MIN, 163                                        117
MINMAX, 91, 112, 205, 206
Minmax, 91, 113                        OBJECT LINEAR, 38, 39, 199
MINMAX FORMAT, 206                     OBJECT PLANE, 38
MINMAX SINK, 206                       ONE, 164, 165, 226
MODELVIEW, 31, 35                      ONE MINUS CONSTANT ALPHA,
MODELVIEW MATRIX, 198                          81, 163, 164
MODULATE, 147–150, 225                 ONE MINUS CONSTANT COLOR,
MULT, 172                                      81, 163, 164
MULTISAMPLE, 62, 66, 72, 78, 113,      ONE MINUS DST ALPHA, 164
          115, 158, 167                ONE MINUS DST COLOR, 164
MULTISAMPLE BIT, 208                   ONE MINUS SRC ALPHA, 151, 164

                     Version 1.3 - August 14, 2001
280                                                                INDEX


ONE MINUS SRC COLOR, 151, 164              POLYGON BIT, 208
OPERANDn ALPHA, 147, 151, 152              POLYGON OFFSET FILL, 77, 78
OPERANDn RGB, 147, 151, 152                POLYGON OFFSET LINE, 77, 78
OR, 166                                    POLYGON OFFSET POINT, 77
OR INVERTED, 166                           POLYGON SMOOTH, 73, 78
OR REVERSE, 166                            POLYGON SMOOTH HINT, 196
ORDER, 200                                 POLYGON STIPPLE, 75
Ortho, 33, 34, 245                         POLYGON STIPPLE BIT, 208
OUT OF MEMORY, 11, 12, 193                 POLYGON TOKEN, 192
                                           PolygonMode, 71, 76, 78, 188, 190
PACK ALIGNMENT, 175, 228                   PolygonOffset, 77
PACK IMAGE HEIGHT, 175, 201, 228           PolygonStipple, 75
PACK LSB FIRST, 175, 228                   PopAttrib, 207, 209, 246
PACK ROW LENGTH, 175, 228                  PopClientAttrib, 19, 195, 207, 209
PACK SKIP IMAGES, 175, 201, 228            PopMatrix, 35
PACK SKIP PIXELS, 175, 228                 PopName, 187
PACK SKIP ROWS, 175, 228                   POSITION, 52, 199
PACK SWAP BYTES, 175, 228                  POST COLOR MATRIX x BIAS, 82
PASS THROUGH TOKEN, 192                    POST COLOR MATRIX x SCALE,
PassThrough, 191                                    82
PERSPECTIVE CORRECTION HINT,               POST COLOR MATRIX ALPHA BIAS,
          196                                       111
PIXEL MAP A TO A, 83, 104                  POST COLOR MATRIX ALPHA SCALE,
PIXEL MAP B TO B, 83, 104                           111
PIXEL MAP G TO G, 83, 104                  POST COLOR MATRIX BLUE BIAS,
PIXEL MAP I TO A, 83, 105                           111
PIXEL MAP I TO B, 83, 105                  POST COLOR MATRIX BLUE SCALE,
PIXEL MAP I TO G, 83, 105                           111
PIXEL MAP I TO I, 83, 105                  POST COLOR MATRIX COLOR TABLE,
PIXEL MAP I TO R, 83, 105                           83, 111
PIXEL MAP R TO R, 83, 104                  POST COLOR MATRIX GREEN BIAS,
PIXEL MAP S TO S, 83, 105                           111
PIXEL MODE BIT, 208                        POST COLOR MATRIX GREEN SCALE,
PixelMap, 79, 81–83, 180                            111
PixelStore, 19, 79–81, 175, 180, 195       POST COLOR MATRIX RED BIAS,
PixelTransfer, 79, 81, 82, 110, 180                 111
PixelZoom, 103, 113                        POST COLOR MATRIX RED SCALE,
POINT, 76–78, 185, 186, 220, 248                    111
POINT BIT, 208                             POST CONVOLUTION x BIAS, 82
POINT SMOOTH, 63, 66                       POST CONVOLUTION x SCALE, 82
POINT SMOOTH HINT, 196                     POST CONVOLUTION ALPHA BIAS,
POINT TOKEN, 192                                    110
POINTS, 15, 185                            POST CONVOLUTION ALPHA SCALE,
PointSize, 63                                       110
POLYGON, 16, 18                            POST CONVOLUTION BLUE BIAS,

                         Version 1.3 - August 14, 2001
INDEX                                                                  281


           110                      RasterPos2, 42
POST CONVOLUTION BLUE SCALE,        RasterPos3, 42
           110                      RasterPos4, 42
POST CONVOLUTION COLOR TABLE,       ReadBuffer, 175, 180
           83, 110                  ReadPixels, 79, 81, 94–96, 106, 173–
POST CONVOLUTION GREEN BIAS,                   177, 180, 195, 201–203
           110                      Rect, 28, 73
POST CONVOLUTION GREEN SCALE,       RED, 82, 95, 176, 177, 228, 229, 231,
           110                                 238
POST CONVOLUTION RED BIAS,          RED BIAS, 104
           110                      RED SCALE, 104
POST CONVOLUTION RED SCALE,         REDUCE, 108, 110, 230
           110                      REFLECTION MAP, 38, 39, 262
PREVIOUS, 149, 151, 225             RENDER, 188, 189, 239
PRIMARY COLOR, 151                  RENDERER, 206
PrioritizeTextures, 146             RenderMode, 188–190, 195
PROJECTION, 31, 35                  REPEAT, 133, 134, 137, 138, 143, 224
PROXY COLOR TABLE, 83, 86, 195      REPLACE, 147, 148, 150, 160
PROXY HISTOGRAM, 90, 91, 195,       REPLICATE BORDER, 108, 109
           205
                                    RESCALE NORMAL, 36
PROXY POST COLOR MATRIX COLOR TABLE,
                                    ResetHistogram, 205
           83, 195
                                    ResetMinmax, 206
PROXY POST CONVOLUTION COLOR TABLE,
                                    RETURN, 172
           83, 195
                                    RGB, 95, 97, 101, 106, 107, 117–120,
PROXY TEXTURE 1D, 122, 144, 195,
                                               147–149, 176, 177, 202, 248
           200
                                    RGB10, 119
PROXY TEXTURE 2D, 121, 144, 195,
           200                      RGB10 A2, 119
PROXY TEXTURE 3D, 116, 143, 144,    RGB12, 119
           195, 200                 RGB16, 119
PROXY TEXTURE CUBE MAP, 121,        RGB4, 119
           144, 195, 200            RGB5,   119
PushAttrib, 207, 209                RGB5   A1,  119
PushClientAttrib, 19, 195, 207, 209 RGB8,   119
PushMatrix, 35                      RGB SCALE, 147
PushName, 187                       RGBA, 85, 89–91, 95, 97, 101, 106, 107,
                                               117–120, 148, 149, 176, 180,
Q, 37–39, 199                                  202, 229–232
QUAD STRIP, 17                      RGBA12,    119
QUADRATIC ATTENUATION, 52           RGBA16,    119
QUADS, 18                           RGBA2,    119
                                    RGBA4, 119
R, 37, 38, 199                      RGBA8, 119
R3 G3 B2, 119                       RIGHT, 168, 175
RasterPos, 42, 188, 245             Rotate, 33, 245

                       Version 1.3 - August 14, 2001
282                                                                        INDEX


S, 37, 38, 199                               STACK UNDERFLOW, 12, 35, 187,
SAMPLE ALPHA TO COVERAGE,                             207
           158                               STENCIL, 180
SAMPLE ALPHA TO ONE, 158, 159                STENCIL BUFFER BIT, 170, 171, 208
SAMPLE BUFFERS, 62, 66, 72, 78,              STENCIL INDEX, 83, 86, 93, 95, 103,
           113, 115, 158, 167, 170, 175               116, 173, 175, 176, 180, 201
SAMPLE COVERAGE, 158, 159                    STENCIL TEST, 160
SAMPLE COVERAGE INVERT, 158,                 StencilFunc, 160, 244
           159                               StencilMask, 169, 170, 173, 244
SAMPLE COVERAGE VALUE, 158,                  StencilOp, 160, 161
           159                               SUBTRACT, 150
SampleCoverage, 159
SAMPLES, 62                                  T, 37, 199
Scale, 33, 245                               T2F C3F V3F, 26, 27
Scissor, 158                                 T2F C4F N3F V3F, 26, 27
SCISSOR BIT, 208                             T2F C4UB V3F, 26, 27
SCISSOR TEST, 158                            T2F N3F V3F, 26, 27
SELECT, 188, 189, 246                        T2F V3F, 26, 27
SelectBuffer, 188, 189, 195                  T4F C4F N3F V4F, 26, 27
SELECTION BUFFER POINTER, 206                T4F V4F, 26, 27
                                             TABLE TOO LARGE, 12, 84, 90
SEPARABLE 2D, 88, 106, 122, 204
                                             TexCoord, 19, 20
SeparableFilter2D, 88
                                             TexCoord1, 20
SEPARATE SPECULAR COLOR, 48
                                             TexCoord2, 20
SET, 166
                                             TexCoord3, 20
SGI color matrix, 255
                                             TexCoord4, 20
SGIS multitexture, 260
                                             TexCoordPointer, 19, 22, 23, 26, 195
SGIS texture edge clamp, 254
                                             TexEnv, 147, 152
SGIS texture lod, 254
                                             TexGen, 37–39
ShadeModel, 56                               TexImage, 127
SHININESS, 52                                TexImage1D, 80, 106, 108, 118, 122,
SHORT, 22, 94, 177, 178, 194                           123, 125, 126, 129, 140, 144,
SINGLE COLOR, 47, 48, 218                              195
SMOOTH, 56, 217                              TexImage2D, 80, 90, 91, 106, 108, 118,
SOURCEn ALPHA, 147, 151, 152                           121–123, 125, 126, 129, 140,
SOURCEn RGB, 147, 151, 152                             144, 195
SPECULAR, 51, 52                             TexImage3D, 80, 116, 118, 120–123,
SPHERE MAP, 38, 39, 262                                126, 129, 140, 143, 144, 195,
SPOT CUTOFF, 52                                        201
SPOT DIRECTION, 52, 199                      TexParameter, 132
SPOT EXPONENT, 52                            TexParameter[if], 136, 140
SRC ALPHA, 149, 151, 164, 225                TexParameterf, 146
SRC ALPHA SATURATE, 164                      TexParameterfv, 146
SRC COLOR, 149, 151, 164, 225                TexParameteri, 146
STACK OVERFLOW, 12, 35, 187, 207             TexParameteriv, 146

                           Version 1.3 - August 14, 2001
INDEX                                                                      283


TexSubImage, 127                                    201
TexSubImage1D, 106, 126, 128, 129,        TEXTURE CUBE MAP POSITIVE Y,
        131                                         121, 125, 126, 135, 200, 201
TexSubImage2D, 106, 126, 128, 129,        TEXTURE CUBE MAP POSITIVE Z,
        131                                         121, 125, 126, 135, 200, 201
TexSubImage3D, 126, 127, 129, 131         TEXTURE DEPTH, 130–132, 200
TEXTURE, 31, 34, 35, 149, 151, 225        TEXTURE ENV, 147, 199
TEXTUREi, 20                              TEXTURE ENV COLOR, 147
TEXTURE0, 20, 35, 183, 190, 209, 214,     TEXTURE ENV MODE, 147, 152, 263
        225                               TEXTURE GEN MODE, 38, 39
TEXTURE1, 209                             TEXTURE GEN Q, 39
TEXTURE xD, 222                           TEXTURE GEN R, 39
TEXTURE 1D, 106, 122, 125, 126, 132,      TEXTURE GEN S, 39
        144, 145, 149, 199, 201           TEXTURE GEN T, 39
TEXTURE 2D, 121, 125, 126, 132, 144,      TEXTURE GREEN SIZE, 200
        145, 149, 199, 201                TEXTURE HEIGHT, 130–132, 200
TEXTURE 3D, 116, 126, 132, 143–145,       TEXTURE INTENSITY SIZE, 200
        149, 199, 201                     TEXTURE INTERNAL FORMAT,
TEXTURE ALPHA SIZE, 200                             130, 131, 200
TEXTURE BASE LEVEL, 123, 132,             TEXTURE LUMINANCE SIZE, 200
        133, 140, 143                     TEXTURE MAG FILTER, 133, 141,
TEXTURE BIT, 207, 208                               143
TEXTURE BLUE SIZE, 200                    TEXTURE MAX LEVEL, 132, 133,
TEXTURE BORDER, 130, 132, 200                       140, 143
TEXTURE BORDER COLOR,             132,    TEXTURE MAX LOD, 132, 133, 136,
        133, 139, 143                               143
TEXTURE COMPONENTS, 200                   TEXTURE MIN FILTER, 133, 137–
TEXTURE COMPRESSED IMAGE SIZE,                      139, 141–143
        130, 131, 200, 201                TEXTURE MIN LOD, 132, 133, 136,
TEXTURE COMPRESSION HINT,                           143
        196                               TEXTURE PRIORITY, 133, 143, 146
TEXTURE COORD ARRAY, 23, 26               TEXTURE RED SIZE, 200
TEXTURE COORD ARRAY POINTER,              TEXTURE RESIDENT, 143, 146
        206                               TEXTURE WIDTH, 130–132, 200
TEXTURE CUBE MAP, 122, 132, 144,          TEXTURE WRAP R, 133, 134, 138
        145, 149, 199, 200, 222           TEXTURE WRAP S, 133, 134, 137,
TEXTURE CUBE MAP *, 122                             138
TEXTURE CUBE MAP NEGATIVE X,              TEXTURE WRAP T, 133, 134, 138
        121, 125, 126, 135, 199, 201      TEXTUREn, 152
TEXTURE CUBE MAP NEGATIVE Y,              TRANSFORM BIT, 208
        121, 125, 126, 135, 200, 201      Translate, 33, 245
TEXTURE CUBE MAP NEGATIVE Z,              TRANSPOSE COLOR MATRIX, 198,
        121, 125, 126, 135, 200, 201                203
TEXTURE CUBE MAP POSITIVE X,              TRANSPOSE MODELVIEW MATRIX,
        121, 122, 125, 126, 135, 199,               198

                        Version 1.3 - August 14, 2001
284                                                                           INDEX


TRANSPOSE PROJECTION MATRIX,                  UNSIGNED SHORT 1 5         5 5 REV, 94,
        198                                         96, 97, 99, 178
TRANSPOSE TEXTURE MATRIX,                     UNSIGNED SHORT 4 4         4 4, 94, 96,
        198                                         97, 99, 178
TRIANGLE FAN, 16                              UNSIGNED SHORT 4 4         4 4 REV, 94,
TRIANGLE STRIP, 16                                  96, 97, 99, 178
TRIANGLES, 16, 18                             UNSIGNED SHORT 5 5         5 1, 94, 96,
TRUE, 18, 19, 41, 47, 49, 79, 80, 82, 90,           97, 99, 178
        91, 146, 159, 169, 175, 195,          UNSIGNED SHORT 5 6         5, 94, 96, 97,
        198, 202, 205                               99, 178
                                              UNSIGNED SHORT 5 6         5 REV,    94,
                                                    96, 97, 99, 178
UNPACK ALIGNMENT, 80, 96, 116,
      228                                     V2F, 26, 27
UNPACK IMAGE HEIGHT, 80, 116,                 V3F, 26, 27
      228                                     VENDOR, 206
UNPACK LSB FIRST, 80, 101, 228                VERSION, 206, 207
UNPACK ROW LENGTH, 80, 93, 96,                Vertex, 7, 19, 42, 184
      116, 228                                Vertex2, 19, 28
UNPACK SKIP IMAGES, 80, 116,                  Vertex2sv, 7
      122, 228                                Vertex3, 19
UNPACK SKIP PIXELS, 80, 96, 101,              Vertex3f, 7
      228                                     Vertex4, 19
UNPACK SKIP ROWS, 80, 96, 101,                VERTEX ARRAY, 23, 28
      228                                     VERTEX ARRAY POINTER, 206
UNPACK SWAP BYTES, 80, 93, 95,                VertexPointer, 19, 22, 23, 28, 195
      228                                     Viewport, 30
UNSIGNED BYTE, 22, 24, 27, 94, 98,            VIEWPORT BIT, 208
      177, 178, 194
UNSIGNED BYTE 2 3 3 REV,        94,           WGL ARB multisample, 262
      96–98, 178
                                              XOR, 166
UNSIGNED BYTE 3 3 2, 94, 96–98,
      178                                     ZERO, 160, 164, 165, 226
UNSIGNED INT, 22, 24, 94, 100, 177,
      178, 194
UNSIGNED INT 10 10 10 2, 94, 97,
      100, 178
UNSIGNED INT 2 10 10 10 REV, 94,
      97, 100, 178
UNSIGNED INT 8 8 8 8, 94, 96, 97,
      100, 178
UNSIGNED INT 8 8 8 8 REV, 94, 96,
      97, 100, 178
UNSIGNED SHORT, 22, 24, 94, 99,
      177, 178, 194

                            Version 1.3 - August 14, 2001
