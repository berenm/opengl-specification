                               R
             OpenGL ES
Common/Common-Lite Profile Specification
   Version 1.1.12 (Full Specification)
             April 24, 2008

            Editor (version 1.0): David Blythe
     Editors (version 1.1): Aaftab Munshi, Jon Leech
     Copyright c 2002-2007 The Khronos Group Inc. All Rights Reserved.

This specification is protected by copyright laws and contains material proprietary
to the Khronos Group, Inc. It or any components may not be reproduced, repub-
lished, distributed, transmitted, displayed, broadcast or otherwise exploited in any
manner without the express prior written permission of Khronos Group. You may
use this specification for implementing the functionality therein, without altering or
removing any trademark, copyright or other notice from the specification, but the
receipt or possession of this specification does not convey any rights to reproduce,
disclose, or distribute its contents, or to manufacture, use, or sell anything that it
may describe, in whole or in part.
Khronos Group grants express permission to any current Promoter, Contributor
or Adopter member of Khronos to copy and redistribute UNMODIFIED versions
of this specification in any fashion, provided that NO CHARGE is made for the
specification and the latest available update of the specification for any version
of the API is used whenever possible. Such distributed specification may be re-
formatted AS LONG AS the contents of the specification are not changed in any
way. The specification may be incorporated into a product that is sold as long as
such product includes significant independent work developed by the seller. A link
to the current version of this specification on the Khronos Group web-site should
be included whenever possible with specification distributions.
Khronos Group makes no, and expressly disclaims any, representations or war-
ranties, express or implied, regarding this specification, including, without limita-
tion, any implied warranties of merchantability or fitness for a particular purpose
or non-infringement of any intellectual property. Khronos Group makes no, and
expressly disclaims any, warranties, express or implied, regarding the correctness,
accuracy, completeness, timeliness, and reliability of the specification. Under no
circumstances will the Khronos Group, or any of its Promoters, Contributors or
Members or their respective partners, officers, directors, employees, agents or rep-
resentatives be liable for any damages, whether direct, indirect, special or conse-
quential damages for lost revenues, lost profits, or otherwise, arising from or in
connection with these materials.
Khronos is a trademark of The Khronos Group Inc. OpenGL is a registered trade-
mark, and OpenGL ES is a trademark, of Silicon Graphics, Inc.
                  Copyright c 1992-2006 Silicon Graphics, Inc.


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
Contents

1   Introduction                                                                                              1
    1.1 Formatting of Optional Features . . . . . .           .   .   .   .   .   .   .   .   .   .   .   .   1
    1.2 What is the OpenGL ES Graphics System?                .   .   .   .   .   .   .   .   .   .   .   .   1
    1.3 OpenGL ES Profiles . . . . . . . . . . . .            .   .   .   .   .   .   .   .   .   .   .   .   2
    1.4 Programmer’s View of OpenGL ES . . . .                .   .   .   .   .   .   .   .   .   .   .   .   2
    1.5 Implementor’s View of OpenGL ES . . . .               .   .   .   .   .   .   .   .   .   .   .   .   3
    1.6 Our View . . . . . . . . . . . . . . . . . .          .   .   .   .   .   .   .   .   .   .   .   .   3

2   OpenGL ES Operation                                                                                        4
    2.1 OpenGL ES Fundamentals . . . . . . .          .   .   .   .   .   .   .   .   .   .   .   .   .   .    4
         2.1.1 Numeric Computation . . . . .          .   .   .   .   .   .   .   .   .   .   .   .   .   .    6
    2.2 GL State . . . . . . . . . . . . . . . . .    .   .   .   .   .   .   .   .   .   .   .   .   .   .    7
    2.3 GL Command Syntax . . . . . . . . . .         .   .   .   .   .   .   .   .   .   .   .   .   .   .    8
    2.4 Basic GL Operation . . . . . . . . . . .      .   .   .   .   .   .   .   .   .   .   .   .   .   .    9
    2.5 GL Errors . . . . . . . . . . . . . . . .     .   .   .   .   .   .   .   .   .   .   .   .   .   .   12
    2.6 Primitives and Vertices . . . . . . . . .     .   .   .   .   .   .   .   .   .   .   .   .   .   .   13
         2.6.1 Primitive Types . . . . . . . . .      .   .   .   .   .   .   .   .   .   .   .   .   .   .   14
    2.7 Current Vertex State . . . . . . . . . . .    .   .   .   .   .   .   .   .   .   .   .   .   .   .   18
    2.8 Vertex Arrays . . . . . . . . . . . . . .     .   .   .   .   .   .   .   .   .   .   .   .   .   .   19
    2.9 Buffer Objects . . . . . . . . . . . . . .    .   .   .   .   .   .   .   .   .   .   .   .   .   .   22
         2.9.1 Vertex Arrays in Buffer Objects        .   .   .   .   .   .   .   .   .   .   .   .   .   .   25
         2.9.2 Array Indices in Buffer Objects        .   .   .   .   .   .   .   .   .   .   .   .   .   .   26
    2.10 Coordinate Transformations . . . . . .       .   .   .   .   .   .   .   .   .   .   .   .   .   .   26
         2.10.1 Controlling the Viewport . . . .      .   .   .   .   .   .   .   .   .   .   .   .   .   .   28
         2.10.2 Matrices . . . . . . . . . . . . .    .   .   .   .   .   .   .   .   .   .   .   .   .   .   29
         2.10.3 Normal Transformation . . . . .       .   .   .   .   .   .   .   .   .   .   .   .   .   .   33
    2.11 Clipping . . . . . . . . . . . . . . . . .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   35
    2.12 Colors and Coloring . . . . . . . . . . .    .   .   .   .   .   .   .   .   .   .   .   .   .   .   37
         2.12.1 Lighting . . . . . . . . . . . . .    .   .   .   .   .   .   .   .   .   .   .   .   .   .   37


                                         i
CONTENTS                                                                                               ii


         2.12.2   Lighting Parameter Specification . . . .     .   .   .   .   .   .   .   .   .   .   41
         2.12.3   Color Material Tracking . . . . . . . .      .   .   .   .   .   .   .   .   .   .   44
         2.12.4   Lighting State . . . . . . . . . . . . . .   .   .   .   .   .   .   .   .   .   .   44
         2.12.5   Clamping . . . . . . . . . . . . . . . .     .   .   .   .   .   .   .   .   .   .   44
         2.12.6   Flatshading . . . . . . . . . . . . . . .    .   .   .   .   .   .   .   .   .   .   44
         2.12.7   Color and Texture Coordinate Clipping        .   .   .   .   .   .   .   .   .   .   45
         2.12.8   Final Color Processing . . . . . . . . .     .   .   .   .   .   .   .   .   .   .   46

3   Rasterization                                                                                      47
    3.1 Invariance . . . . . . . . . . . . . . . . . . . . . . . . . .                 .   .   .   .   48
    3.2 Antialiasing . . . . . . . . . . . . . . . . . . . . . . . . .                 .   .   .   .   48
         3.2.1 Multisampling . . . . . . . . . . . . . . . . . . .                     .   .   .   .   49
    3.3 Points . . . . . . . . . . . . . . . . . . . . . . . . . . . .                 .   .   .   .   51
         3.3.1 Basic Point Rasterization . . . . . . . . . . . . . .                   .   .   .   .   52
         3.3.2 Point Rasterization State . . . . . . . . . . . . . .                   .   .   .   .   56
         3.3.3 Point Multisample Rasterization . . . . . . . . . .                     .   .   .   .   56
    3.4 Line Segments . . . . . . . . . . . . . . . . . . . . . . .                    .   .   .   .   57
         3.4.1 Basic Line Segment Rasterization . . . . . . . . .                      .   .   .   .   57
         3.4.2 Other Line Segment Features . . . . . . . . . . . .                     .   .   .   .   60
         3.4.3 Line Rasterization State . . . . . . . . . . . . . .                    .   .   .   .   62
         3.4.4 Line Multisample Rasterization . . . . . . . . . .                      .   .   .   .   62
    3.5 Polygons . . . . . . . . . . . . . . . . . . . . . . . . . .                   .   .   .   .   62
         3.5.1 Basic Polygon Rasterization . . . . . . . . . . . .                     .   .   .   .   62
         3.5.2 Depth Offset . . . . . . . . . . . . . . . . . . . .                    .   .   .   .   64
         3.5.3 Polygon Multisample Rasterization . . . . . . . .                       .   .   .   .   65
         3.5.4 Polygon Rasterization State . . . . . . . . . . . .                     .   .   .   .   65
    3.6 Pixel Rectangles . . . . . . . . . . . . . . . . . . . . . . .                 .   .   .   .   65
         3.6.1 Pixel Storage Modes . . . . . . . . . . . . . . . .                     .   .   .   .   66
         3.6.2 Transfer of Pixel Rectangles . . . . . . . . . . . .                    .   .   .   .   66
    3.7 Texturing . . . . . . . . . . . . . . . . . . . . . . . . . .                  .   .   .   .   72
         3.7.1 Texture Image Specification . . . . . . . . . . . .                     .   .   .   .   72
         3.7.2 Alternate Texture Image Specification Commands                          .   .   .   .   76
         3.7.3 Compressed Texture Images . . . . . . . . . . . .                       .   .   .   .   78
         3.7.4 Compressed Paletted Textures . . . . . . . . . . .                      .   .   .   .   80
         3.7.5 Texture Parameters . . . . . . . . . . . . . . . . .                    .   .   .   .   82
         3.7.6 Texture Wrap Modes . . . . . . . . . . . . . . . .                      .   .   .   .   83
         3.7.7 Texture Minification . . . . . . . . . . . . . . . .                    .   .   .   .   83
         3.7.8 Texture Magnification . . . . . . . . . . . . . . .                     .   .   .   .   87
         3.7.9 Texture Completeness . . . . . . . . . . . . . . .                      .   .   .   .   88
         3.7.10 Texture State . . . . . . . . . . . . . . . . . . . .                  .   .   .   .   88

                          Version 1.1.12 (April 24, 2008)
CONTENTS                                                                                                            iii


         3.7.11 Texture Objects . . . . . . . . . . . . . . . .                        .   .   .   .   .   .   .    89
         3.7.12 Texture Environments and Texture Functions                             .   .   .   .   .   .   .    90
         3.7.13 Texture Application . . . . . . . . . . . . . .                        .   .   .   .   .   .   .    95
    3.8 Fog . . . . . . . . . . . . . . . . . . . . . . . . . .                        .   .   .   .   .   .   .    97
    3.9 Antialiasing Application . . . . . . . . . . . . . . .                         .   .   .   .   .   .   .    98
    3.10 Multisample Point Fade . . . . . . . . . . . . . . . .                        .   .   .   .   .   .   .    98

4   Per-Fragment Operations and the Framebuffer                                                                     99
    4.1 Per-Fragment Operations . . . . . . . . . . . . . . .                          .   .   .   .   .   .   .    99
         4.1.1 Pixel Ownership Test . . . . . . . . . . . . .                          .   .   .   .   .   .   .   100
         4.1.2 Scissor Test . . . . . . . . . . . . . . . . . .                        .   .   .   .   .   .   .   100
         4.1.3 Multisample Fragment Operations . . . . . .                             .   .   .   .   .   .   .   101
         4.1.4 Alpha Test . . . . . . . . . . . . . . . . . .                          .   .   .   .   .   .   .   102
         4.1.5 Stencil Test . . . . . . . . . . . . . . . . . .                        .   .   .   .   .   .   .   103
         4.1.6 Depth Buffer Test . . . . . . . . . . . . . . .                         .   .   .   .   .   .   .   104
         4.1.7 Blending . . . . . . . . . . . . . . . . . . .                          .   .   .   .   .   .   .   104
         4.1.8 Dithering . . . . . . . . . . . . . . . . . . .                         .   .   .   .   .   .   .   106
         4.1.9 Logical Operation . . . . . . . . . . . . . .                           .   .   .   .   .   .   .   107
         4.1.10 Additional Multisample Fragment Operations                             .   .   .   .   .   .   .   107
    4.2 Whole Framebuffer Operations . . . . . . . . . . . .                           .   .   .   .   .   .   .   109
         4.2.1 Selecting a Buffer for Writing . . . . . . . .                          .   .   .   .   .   .   .   109
         4.2.2 Fine Control of Buffer Updates . . . . . . .                            .   .   .   .   .   .   .   109
         4.2.3 Clearing the Buffers . . . . . . . . . . . . .                          .   .   .   .   .   .   .   110
    4.3 Reading Pixels . . . . . . . . . . . . . . . . . . . .                         .   .   .   .   .   .   .   111
         4.3.1 Reading Pixels . . . . . . . . . . . . . . . .                          .   .   .   .   .   .   .   111
         4.3.2 Pixel Draw/Read State . . . . . . . . . . . .                           .   .   .   .   .   .   .   114

5   Special Functions                                                           115
    5.1 Flush and Finish . . . . . . . . . . . . . . . . . . . . . . . . . . . 115
    5.2 Hints . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 115

6   State and State Requests                                                                                       117
    6.1 Querying GL State . . . . . . . .      .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   117
          6.1.1 Simple Queries . . . . . .     .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   117
          6.1.2 Data Conversions . . . . .     .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   118
          6.1.3 Enumerated Queries . . .       .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   119
          6.1.4 Texture Queries . . . . . .    .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   119
          6.1.5 Pointer and String Queries     .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   120
          6.1.6 Buffer Object Queries . .      .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   120
    6.2 State Tables . . . . . . . . . . . .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   121


                         Version 1.1.12 (April 24, 2008)
CONTENTS                                                                                                                      iv


A Invariance                                                                                                                 146
  A.1 Repeatability . . . . .    .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   146
  A.2 Multi-pass Algorithms      .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   147
  A.3 Invariance Rules . . . .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   147
  A.4 What All This Means .      .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   149

B Corollaries                                                                                                                150

C Profiles                                                                                                                   152
  C.1 Accuracy Requirements . . . . . . . . . . . . . . . .                                      .   .   .   .   .   .   .   152
  C.2 Floating-Point and Fixed-Point Commands and State                                          .   .   .   .   .   .   .   152
  C.3 Core Additions and Extensions . . . . . . . . . . . .                                      .   .   .   .   .   .   .   153
        C.3.1 Byte Coordinates . . . . . . . . . . . . . . .                                     .   .   .   .   .   .   .   155
        C.3.2 Fixed Point . . . . . . . . . . . . . . . . . .                                    .   .   .   .   .   .   .   155
        C.3.3 Single-precision Commands . . . . . . . . .                                        .   .   .   .   .   .   .   155
        C.3.4 Compressed Paletted Texture . . . . . . . . .                                      .   .   .   .   .   .   .   156
        C.3.5 Read Format . . . . . . . . . . . . . . . . .                                      .   .   .   .   .   .   .   156
        C.3.6 Matrix Palette . . . . . . . . . . . . . . . . .                                   .   .   .   .   .   .   .   156
        C.3.7 Point Sprites . . . . . . . . . . . . . . . . .                                    .   .   .   .   .   .   .   156
        C.3.8 Point Size Array . . . . . . . . . . . . . . .                                     .   .   .   .   .   .   .   157
        C.3.9 Matrix Get . . . . . . . . . . . . . . . . . .                                     .   .   .   .   .   .   .   157
        C.3.10 Draw Texture . . . . . . . . . . . . . . . . .                                    .   .   .   .   .   .   .   157
  C.4 Packaging . . . . . . . . . . . . . . . . . . . . . . .                                    .   .   .   .   .   .   .   157
  C.5 Acknowledgements . . . . . . . . . . . . . . . . . .                                       .   .   .   .   .   .   .   158
  C.6 Document History . . . . . . . . . . . . . . . . . . .                                     .   .   .   .   .   .   .   160

D Version 1.1                                                                                                                162
  D.1 Changes From OpenGL 1.5 . . . . . . . . .                              .   .   .   .   .   .   .   .   .   .   .   .   162
       D.1.1 Automatic Mipmap Generation . .                                 .   .   .   .   .   .   .   .   .   .   .   .   162
       D.1.2 Buffer Objects . . . . . . . . . . .                            .   .   .   .   .   .   .   .   .   .   .   .   163
       D.1.3 Static and Dynamic State Queries .                              .   .   .   .   .   .   .   .   .   .   .   .   163
       D.1.4 User-defined Clip Planes . . . . . .                            .   .   .   .   .   .   .   .   .   .   .   .   163
  D.2 Enhanced Texture Processing . . . . . . . .                            .   .   .   .   .   .   .   .   .   .   .   .   163
  D.3 New Core Additions and Profile Extensions                              .   .   .   .   .   .   .   .   .   .   .   .   163




                        Version 1.1.12 (April 24, 2008)
List of Figures

 2.1   Block diagram of the GL. . . . . . . . . . . . . . . . . . . . . . .             11
 2.2   Creation of a processed vertex from vertex array coordinates and
       current values. . . . . . . . . . . . . . . . . . . . . . . . . . . . .          14
 2.3   Primitive assembly and processing. . . . . . . . . . . . . . . . . .             14
 2.4   Triangle strips, fans, and independent triangles. . . . . . . . . . .            17
 2.5   Vertex transformation sequence. . . . . . . . . . . . . . . . . . .              26
 2.6   Processing of RGBA colors. . . . . . . . . . . . . . . . . . . . .               37

 3.1   Rasterization. . . . . . . . . . . . . . . . . . . . . . . . .   .   .   .   .   47
 3.2   Rasterization of non-antialiased wide points. . . . . . . . .    .   .   .   .   53
 3.3   Rasterization of antialiased wide points. . . . . . . . . . .    .   .   .   .   53
 3.4   Visualization of Bresenham’s algorithm. . . . . . . . . . .      .   .   .   .   58
 3.5   Rasterization of non-antialiased wide lines. . . . . . . . .     .   .   .   .   60
 3.6   The region used in rasterizing an antialiased line segment.      .   .   .   .   61
 3.7   Transfer of pixel rectangles to the GL. . . . . . . . . . . .    .   .   .   .   66
 3.8   A texture image and the coordinates used to access it. . . .     .   .   .   .   74
 3.9   Multitexture pipeline. . . . . . . . . . . . . . . . . . . . .   .   .   .   .   95

 4.1   Per-fragment operations. . . . . . . . . . . . . . . . . . . . . . . 100
 4.2   Operation of ReadPixels. . . . . . . . . . . . . . . . . . . . . . . 111




                                       v
List of Tables

 2.1    GL command suffixes . . . . . . . . . . . . . . . . . . .        .   .   .   .   .    9
 2.2    GL data types . . . . . . . . . . . . . . . . . . . . . . .      .   .   .   .   .   10
 2.3    Summary of GL errors . . . . . . . . . . . . . . . . . .         .   .   .   .   .   13
 2.4    Vertex array sizes (values per vertex) and data types . . .      .   .   .   .   .   20
 2.5    Buffer object parameters and their values. . . . . . . . .       .   .   .   .   .   23
 2.6    Buffer object initial state. . . . . . . . . . . . . . . . . .   .   .   .   .   .   24
 2.7    Component conversions . . . . . . . . . . . . . . . . . .        .   .   .   .   .   38
 2.8    Summary of lighting parameters. . . . . . . . . . . . . .        .   .   .   .   .   39
 2.9    Correspondence of lighting parameter symbols to names.           .   .   .   .   .   43
 2.10   Triangle flatshading color selection. . . . . . . . . . . .      .   .   .   .   .   45

 3.1    PixelStore parameters. . . . . . . . . . . . . . . . . . . . . . . .                 66
 3.2    TexImage2D and ReadPixels types. . . . . . . . . . . . . . . . .                     68
 3.3    TexImage2D and ReadPixels formats. . . . . . . . . . . . . . . .                     68
 3.4    Valid pixel format and type combinations. . . . . . . . . . . . . .                  69
 3.5    Packed pixel formats. . . . . . . . . . . . . . . . . . . . . . . . .                70
 3.6    UNSIGNED SHORT formats . . . . . . . . . . . . . . . . . . . . .                     70
 3.7    Packed pixel field assignments. . . . . . . . . . . . . . . . . . . .                71
 3.8    Conversion from RGBA pixel components to internal texture com-
        ponents. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .               73
 3.9    CopyTexImage internal format/color buffer combinations. . . . .                      77
 3.10   Specific compressed texture formats. . . . . . . . . . . . . . . . .                 79
 3.11   Palette entry pixel formats. . . . . . . . . . . . . . . . . . . . . .               81
 3.12   Texel data formats for compressed paletted textures. . . . . . . . .                 81
 3.13   Texture parameters and their values. . . . . . . . . . . . . . . . .                 82
 3.14   Correspondence of filtered texture components. . . . . . . . . . .                   91
 3.15   Texture functions REPLACE, MODULATE, and DECAL . . . . . . . .                       92
 3.16   Texture functions BLEND and ADD. . . . . . . . . . . . . . . . . .                   92
 3.17   COMBINE texture functions. . . . . . . . . . . . . . . . . . . . . .                 93


                                         vi
LIST OF TABLES                                                                           vii


  3.18 Arguments for COMBINE RGB functions. . . . . . . . . . . . . . .                   94
  3.19 Arguments for COMBINE ALPHA functions. . . . . . . . . . . . .                     94

  4.1    Blending functions. . . . . . . . . . . . . . . . . . . . . . . . . .           106
  4.2    Arguments to LogicOp and their corresponding operations. . . . .                108
  4.3    PixelStore parameters. . . . . . . . . . . . . . . . . . . . . . . .            112
  4.4    ReadPixels GL data types and reversed component conversion for-
         mulas. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .          114

  6.1    State variable types . . . . . . . . . . . . . . . . . . . . . .    .   .   .   122
  6.2    GL Internal primitive assembly state variables (inaccessible)       .   .   .   123
  6.3    Current Values and Associated Data . . . . . . . . . . . . .        .   .   .   124
  6.4    Vertex Array Data . . . . . . . . . . . . . . . . . . . . . . .     .   .   .   125
  6.5    Vertex Array Data (cont.) . . . . . . . . . . . . . . . . . . .     .   .   .   126
  6.6    Buffer Object State . . . . . . . . . . . . . . . . . . . . . .     .   .   .   127
  6.7    Transformation state . . . . . . . . . . . . . . . . . . . . .      .   .   .   128
  6.8    Coloring . . . . . . . . . . . . . . . . . . . . . . . . . . . .    .   .   .   129
  6.9    Lighting (see also Table 2.8 for defaults) . . . . . . . . . . .    .   .   .   130
  6.10   Lighting (cont.) . . . . . . . . . . . . . . . . . . . . . . . .    .   .   .   131
  6.11   Rasterization . . . . . . . . . . . . . . . . . . . . . . . . .     .   .   .   132
  6.12   Multisampling . . . . . . . . . . . . . . . . . . . . . . . . .     .   .   .   133
  6.13   Textures (state per texture unit and binding point) . . . . . .     .   .   .   134
  6.14   Textures (state per texture object) . . . . . . . . . . . . . . .   .   .   .   135
  6.15   Texture Environment and Generation . . . . . . . . . . . . .        .   .   .   136
  6.16   Pixel Operations . . . . . . . . . . . . . . . . . . . . . . . .    .   .   .   137
  6.17   Framebuffer Control . . . . . . . . . . . . . . . . . . . . .       .   .   .   138
  6.18   Pixels . . . . . . . . . . . . . . . . . . . . . . . . . . . . .    .   .   .   139
  6.19   Hints . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .   .   .   .   140
  6.20   Implementation Dependent Values . . . . . . . . . . . . . .         .   .   .   141
  6.21   Implementation Dependent Values (cont.) . . . . . . . . . .         .   .   .   142
  6.22   Implementation Dependent Values (cont.) . . . . . . . . . .         .   .   .   143
  6.23   Implementation Dependent Pixel Depths . . . . . . . . . . .         .   .   .   144
  6.24   Miscellaneous . . . . . . . . . . . . . . . . . . . . . . . . .     .   .   .   145

  C.1 Common and Common-Lite commands. . . . . . . . . . . . . . . 154
  C.2 OES Extension Disposition . . . . . . . . . . . . . . . . . . . . . 155




                         Version 1.1.12 (April 24, 2008)
Chapter 1

Introduction

This document describes the OpenGL ES graphics system: what it is, how it acts,
and what is required to implement it. We assume that the reader has at least a
rudimentary understanding of computer graphics. This means familiarity with the
essentials of computer graphics algorithms as well as familiarity with basic graph-
ics hardware and associated terms.


1.1    Formatting of Optional Features
Some features in the specification are considered optional; an OpenGL ES imple-
mentation may or may not choose to provide them. Portions of the specification
which are optional are so described where the optional features are first defined.
State table entries which are optional are typeset against a gray background .


1.2    What is the OpenGL ES Graphics System?
OpenGL ES is a software interface to graphics hardware. The interface consists of
a set of procedures and functions that allow a programmer to specify the objects
and operations involved in producing high-quality graphical images, specifically
color images of three-dimensional objects.
    Most of OpenGL ES requires that the graphics hardware contain a framebuffer.
Many OpenGL ES calls pertain to drawing objects such as points, lines and poly-
gons, but the way that some of this drawing occurs (such as when antialiasing or
texturing is enabled) relies on the existence of a framebuffer. Further, some of
OpenGL ES is specifically concerned with framebuffer manipulation.
    OpenGL ES 1.1 is based on the OpenGL 1.5 graphics system, but is designed
primarily for graphics hardware running on embedded and mobile devices. It re-

                                        1
1.3. OPENGL ES PROFILES                                                            2


moves a great deal of redundant and legacy functionality, while adding a few new
features. The differences between OpenGL ES and OpenGL are not described in
detail in this specification; however, they are summarized in a companion docu-
ment titled OpenGL ES Common/Common-Lite Profile Specification (Difference
Specification).


1.3    OpenGL ES Profiles
This specification described two profiles for OpenGL ES : Common and Common-
Lite. While many commands are shared by both profiles, some commands are only
supported by one profile.
    The Common-Lite profile differs from the Common profile primarily in be-
ing targeted at a simpler class of graphics system not supporting high-performance
floating-point calculations. The Common-Lite profile supports only commands
taking fixed-point arguments, while the Common profile also includes many equiv-
alent commands taking floting-point arguments.
    Specific differences between the two profiles, including a summary of com-
mands only supported in the Common profile, are documented in Appendix C and
in appropriate sections of the specification.


1.4    Programmer’s View of OpenGL ES
To the programmer, OpenGL ES is a set of commands that allow the specification
of geometric objects in two or three dimensions, together with commands that
control how these objects are rendered into the framebuffer. OpenGL ES provides
an immediate-mode interface, meaning that specifying an object causes it to be
drawn.
    A typical program that uses OpenGL ES begins with calls to open a window
into the framebuffer into which the program will draw. Then, calls are made to
allocate an OpenGL ES context and associate it with the window. These steps may
be performed using a companion API such as the Khronos Native Platform Graph-
ics Interface (EGL), and are documented separately. Once a context is allocated,
the programmer is free to issue OpenGL ES commands. Some calls are used to
draw simple geometric objects (i.e. points, line segments, and polygons), while
others affect the rendering of these primitives including how they are lit or colored
and how they are mapped from the user’s two- or three-dimensional model space
to the two-dimensional screen. There are also calls which operate directly on the
framebuffer, such as reading pixels.



                          Version 1.1.12 (April 24, 2008)
1.5. IMPLEMENTOR’S VIEW OF OPENGL ES                                             3


1.5    Implementor’s View of OpenGL ES
To the implementor, OpenGL ES is a set of commands that affect the operation of
graphics hardware. If the hardware consists only of an addressable framebuffer,
then OpenGL ES must be implemented almost entirely on the host CPU. More
typically, the graphics hardware may comprise varying degrees of graphics accel-
eration, from a raster subsystem capable of rendering two-dimensional lines and
polygons to sophisticated floating-point processors capable of transforming and
computing on geometric data. The OpenGL ES implementor’s task is to provide
the CPU software interface while dividing the work for each OpenGL ES com-
mand between the CPU and the graphics hardware. This division must be tailored
to the available graphics hardware to obtain optimum performance in carrying out
OpenGL ES calls.
    OpenGL ES maintains a considerable amount of state information. This state
controls how objects are drawn into the framebuffer. Some of this state is directly
available to the user: he or she can make calls to obtain its value. Some of it,
however, is visible only by the effect it has on what is drawn. One of the main
goals of this specification is to make OpenGL ES state information explicit, to
elucidate how it changes, and to indicate what its effects are.


1.6    Our View
We view OpenGL ES as a state machine that controls a set of specific drawing
operations. This model should engender a specification that satisfies the needs of
both programmers and implementors. It does not, however, necessarily provide a
model for implementation. An implementation must produce results conforming
to those produced by the specified methods, but there may be ways to carry out a
particular computation that are more efficient than the one specified.




                         Version 1.1.12 (April 24, 2008)
Chapter 2

OpenGL ES Operation

2.1    OpenGL ES Fundamentals
OpenGL ES (henceforth, the “GL”) is concerned only with rendering into a frame-
buffer (and reading values stored in that framebuffer). There is no support for
other peripherals sometimes associated with graphics hardware, such as mice and
keyboards. Programmers must rely on other mechanisms, such as the Khronos
OpenKODE API, to obtain user input.
    The GL draws primitives subject to a number of selectable modes. Each primi-
tive is a point, line segment, or triangle. Each mode may be changed independently;
the setting of one does not affect the settings of others (although many modes may
interact to determine what eventually ends up in the framebuffer). Modes are set,
primitives specified, and other GL operations described by sending commands in
the form of function or procedure calls.
    Primitives are defined by a group of one or more vertices. A vertex defines a
point, an endpoint of an edge, or a corner of a triangle where two edges meet. Data
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


                                         4
2.1. OPENGL ES FUNDAMENTALS                                                       5


viously invoked GL commands. In general, the effects of a GL command on either
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
cessed by the GL (the server). A server may maintain a number of GL contexts,
each of which is an encapsulation of current GL state. A client may choose to con-
nect to any one of these contexts. Issuing GL commands when the program is not
connected to a context results in undefined behavior.
     The effects of GL commands on the framebuffer are ultimately controlled by
the window system that allocates framebuffer resources. It is the window system
that determines which portions of the framebuffer the GL may access at any given
time and that communicates to the GL how those portions are structured. There-
fore, there are no GL commands to configure the framebuffer or initialize the GL.
Similarly, display of framebuffer contents on a monitor or LCD panel (including
the transformation of individual framebuffer values by such techniques as gamma
correction) is not addressed by the GL. Framebuffer configuration occurs outside
of the GL in conjunction with the window system; the initialization of a GL con-
text occurs when the window system allocates a window for GL rendering. The
EGL API defines a portable mechanism for creating GL contexts and windows for
rendering into, which may be used in conjunction with different native platform
window systems.
     The GL is designed to be run on a range of graphics platforms with varying
graphics capabilities and performance. To accommodate this variety, we specify
ideal behavior instead of actual behavior for certain GL operations. In cases where
deviation from the ideal is allowed, we also specify the rules that an implemen-
tation must obey if it is to approximate the ideal behavior usefully. This allowed
variation in GL behavior implies that two distinct GL implementations may not

                         Version 1.1.12 (April 24, 2008)
2.1. OPENGL ES FUNDAMENTALS                                                        6


agree pixel for pixel when presented with the same input even when run on identi-
cal framebuffer configurations.
    Finally, command names, constants, and types are prefixed in the GL (by gl,
GL , and GL, respectively in C) to reduce name clashes with other packages. The
prefixes are omitted in this document for clarity.

2.1.1   Numeric Computation
The GL must perform a number of numeric computations during the course of its
operation.
     Implementations of the Common profile will normally perform computations
in floating-point, and must meet the range and precision requirements defined un-
der ”Floating-Point Computation” below.
     Implementations of the Common-Lite profile will normally perform computa-
tions in fixed-point, and must meet the more relaxed range and precision require-
ments defined under ”Fixed-Point Computation” below. However, Common-Lite
implementations are free to use floating-point computation if they wish.

    Floating-Point Computation

    We do not specify how floating-point numbers are to be represented or how
operations on them are to be performed. We require simply that numbers’ floating-
point parts contain enough bits and that their exponent fields are large enough
so that individual results of floating-point operations are accurate to about 1 part
in 105 . The maximum representable magnitude of a floating-point number used
to represent positional or normal coordinates must be at least 232 ; the maximum
representable magnitude for colors or texture coordinates must be at least 210 . The
maximum representable magnitude for all other floating-point values must be at
least 232 . x · 0 = 0 · x = 0. 1 · x = x · 1 = x. x + 0 = 0 + x = x. 00 =
1. (Occasionally further requirements will be specified.) Most single-precision
floating-point formats meet these requirements.
    Any representable floating-point value is legal as input to a GL command that
requires floating-point data. The result of providing a value that is not a floating-
point number to such a command is unspecified, but must not lead to GL interrup-
tion or termination. In IEEE arithmetic, for example, providing a negative zero or
a denormalized number to a GL command yields predictable results, while provid-
ing a NaN or an infinity yields unspecified results. The identities specified above
do not hold if the value of x is not a floating-point number.

    Fixed-Point Computation


                          Version 1.1.12 (April 24, 2008)
2.2. GL STATE                                                                      7


     Internal computations can use either fixed-point or floating-point arithmetic.
Fixed-point computations must be accurate to within ±2−15 . The maximum repre-
sentable magnitude for a fixed-point number used to represent positional or normal
coordinates must be at least 215 ; the maximum representable magnitude for colors
or texture coordinates must be at least 210 . The maximum representable magnitude
for all other fixed-point values must be at least 215 . x·0 = 0·x = 0. 1·x = x·1 = x.
x + 0 = 0 + x = x. 00 = 1. Fixed-point computations may lead to overflows or
underflows. The results of such computations are undefined, but must not lead to
GL interruption or termination.

    General Requirements

    The following constraints must be met by all implementations, whether using
floating- or fixed-point computation.
    Let the notation 16.16 indicate a 32-bit two’s-complement fixed-point num-
ber with 16 bits of fraction. If an incoming vertex is representable using 16.16,
the modelview and projection matrices are representable in 16.16, and the re-
sulting eye-space and NDC-space vertices (see section 2.10) are representable
in 16.16 (when computed using intermediate representations with sufficient dy-
namic range), then the transformation pipeline must compute the eye-space and
NDC-space vertices to some reasonable accuracy (i.e., overflow is not acceptable).
    Some calculations require division. In such cases (including implied divisions
required by vector normalizations), a division by zero produces an unspecified re-
sult but must not lead to GL interruption or termination.


2.2    GL State
The GL maintains considerable state. This document enumerates each state vari-
able and describes how each variable can be changed. For purposes of discussion,
state variables are categorized somewhat arbitrarily by their function. Although we
describe the operations that the GL performs on the framebuffer, the framebuffer
is not a part of GL state.
    We distinguish two types of state. The first type of state, called GL server
state, resides in the GL server. The majority of GL state falls into this category.
The second type of state, called GL client state, resides in the GL client. Unless
otherwise specified, all state referred to in this document is GL server state; GL
client state is specifically identified. Each instance of a GL context implies one
complete set of GL server state; each connection from a client to a server implies
a set of both GL client state and GL server state.


                          Version 1.1.12 (April 24, 2008)
2.3. GL COMMAND SYNTAX                                                                          8


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
or character pair indicates the specific type of the arguments: 8-bit integer, 32-bit
integer, 32-bit fixed-point, or single-precision floating-point. The final character, if
present, is v, indicating that the command takes a pointer to an array (a vector) of
values rather than a series of individual arguments. Two specific examples:

       void Color4f( float r, float g, float b, float a );

and

       void GetFloatv( enum value, float *data );

    These examples show the ANSI C declarations for these commands. In general,
a command declaration has the form1

       rtype Name{ 1234}{ i x f ub ui}{ v}
                       ( [args ,] T arg1 , . . . , T argN [, args] );

rtype is the return type of the function. The braces ({}) enclose a series of char-
acters (or character pairs) of which one is selected. indicates no character. The
arguments enclosed in brackets ([args ,] and [, args]) may or may not be present.
The N arguments arg1 through argN have type T, which corresponds to one of the
type letters or letter pairs as indicated in Table 2.1 (if there are no letters, then the
arguments’ type is given explicitly). If the final character is not v, then N is given
by the digit 1, 2, 3, or 4 (if there is no digit, then the number of arguments is fixed).
    1
      The declarations shown in this document apply to ANSI C. Languages such as C++ and Ada
that allow passing of argument type information admit simpler declarations and fewer entry points.


                              Version 1.1.12 (April 24, 2008)
2.4. BASIC GL OPERATION                                                            9


                         Letter   Corresponding GL Type
                           i      int
                           x      fixed
                           f      float
                          ub      ubyte
                          ui      uint

Table 2.1: Correspondence of command suffix letters to GL argument types. Refer
to Table 2.2 for definitions of the GL types.


If the final character is v, then only arg1 is present and it is an array of N values
of the indicated type. Finally, we indicate an unsigned type by the shorthand of
prepending a u to the beginning of the type name (so that, for instance, unsigned
int is abbreviated uint).
     For example,

      void Normal3{xf}( T arg );

indicates the two declarations

      void Normal3f( float arg1, float arg2, float arg3 );
      void Normal3x( fixed arg1, fixed arg2, fixed arg3 );

    Arguments whose type is fixed (i.e. not indicated by a suffix on the command)
are of one of the 13 types (or pointers to one of these) summarized in Table 2.2.
    The mapping of GL data types to data types of a specific language binding are
part of the language binding definition and may be platform-dependent. Type con-
version and type promotion behavior when mixing actual and formal arguments of
different data types are specific to the language binding and platform. For exam-
ple, the C language includes automatic conversion between integer and floating-
point data types, but does not include automatic conversion between the int and
fixed, or float and fixed GL types since the fixed data type is not a dis-
tinct built-in type. Regardless of language binding, the enum type converts to
fixed-point without scaling, and integer types are converted to fixed-point by mul-
tiplying by 216 .


2.4    Basic GL Operation
Figure 2.1 shows a schematic diagram of the GL. Commands enter the GL on the
left. Some commands specify geometric objects to be drawn while others control

                          Version 1.1.12 (April 24, 2008)
2.4. BASIC GL OPERATION                                                         10




        GL Type        Minimum      Description
                       Bit Width
        boolean            1        Boolean
        byte               8        Signed binary integer
        ubyte              8        Unsigned binary integer
        short              16       Signed 2’s complement binary integer
        ushort             16       Unsigned binary integer
        int                32       Signed 2’s complement binary integer
        uint               32       Unsigned binary integer
        fixed              32       Signed 2’s complement 16.16 scaled
                                    integer
        clampx             32       16.16 scaled integer clamped to [0, 1]
        sizei              32       Non-negative binary integer size
        enum               32       Enumerated binary integer value
        intptr           ptrbits    Signed 2’s complement binary integer
        sizeiptr         ptrbits    Non-negative binary integer size
        bitfield           32       Bit field
        float              32       Floating-point value
        clampf             32       Floating-point value clamped to [0, 1]

Table 2.2: GL data types. GL types are not C types. Thus, for example, GL
type int is referred to as GLint outside this document, and is not necessarily
equivalent to the C type int. An implementation may use more bits than the
number indicated in the table to represent a GL type. Correct interpretation of
integer values outside the minimum range is not required, however.
ptrbits is the number of bits required to represent a pointer type; in other words,
types intptr and sizeiptr must be sufficiently large as to store any address.




                         Version 1.1.12 (April 24, 2008)
2.4. BASIC GL OPERATION                                                           11




                    Per-Vertex
                    Operations
                                                   Per-Fragment
                                   Rasterization                   Framebuffer
                     Primitive                      Operations
                     Assembly




                                     Texture
                                     Memory




                      Pixel
                    Operations




   Figure 2.1. Block diagram of the GL.




how the objects are handled by the various stages.
    The first stage operates on geometric primitives described by vertices: points,
line segments, and triangles. In this stage vertices are transformed and lit, and
primitives are clipped to a viewing volume in preparation for the next stage, ras-
terization. The rasterizer produces a series of framebuffer addresses and values
using a two-dimensional description of a point, line segment, or triangle. Each
fragment so produced is fed to the next stage that performs operations on individ-
ual fragments before they finally alter the framebuffer. These operations include
conditional updates into the framebuffer based on incoming and previously stored
depth values (to effect depth buffering), blending of incoming fragment colors with
stored colors, as well as masking and other logical operations on fragment values.
    Values may also be read back from the framebuffer or copied from one portion
of the framebuffer to another. These transfers may include some type of decoding
or encoding.
    This ordering is meant only as a tool for describing the GL, not as a strict rule
of how the GL is implemented, and we present it only as a means to organize the
various operations of the GL.



                           Version 1.1.12 (April 24, 2008)
2.5. GL ERRORS                                                                      12


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
error INVALID ENUM results. This is the case even if the argument is a pointer to
a symbolic constant if that value is not allowable for the given command. Using
a symbolic constant in one of the Common or Common-Lite profiles when that
constant is only defined to be accepted by the other profile will also result in the
error INVALID ENUM.
     Second, if a negative number is provided where an argument of type sizei is
specified, the error INVALID VALUE results.


                          Version 1.1.12 (April 24, 2008)
2.6. PRIMITIVES AND VERTICES                                                      13


 Error                      Description                           Offending com-
                                                                  mand ignored?
 INVALID ENUM               enum argument out of range            Yes
 INVALID VALUE              Numeric argument out of range         Yes
 INVALID OPERATION          Operation illegal in current state    Yes
 STACK OVERFLOW             Command would cause a stack           Yes
                            overflow
 STACK UNDERFLOW            Command would cause a stack           Yes
                            underflow
 OUT OF MEMORY              Not enough memory left to exe-        Unknown
                            cute command


                         Table 2.3: Summary of GL errors


    Finally, if memory is exhausted as a side effect of the execution of a command,
the error OUT OF MEMORY may be generated. Otherwise errors are generated only
for conditions that are explicitly described in this specification.


2.6      Primitives and Vertices
In the GL, geometric objects are drawn by specifying a series of coordinate sets
that include vertices and optionally normals, texture coordinates, and colors. Co-
ordinate sets are specified using vertex arrays (see section 2.8). There are seven
geometric objects that are drawn this way: points (including point sprites), con-
nected line segments (line strips), line segment loops, separated line segments,
triangle strips, triangle fans, and separated triangles.
    Each vertex is specified with two, three, or four coordinates. In addition, a
current normal, multiple current texture coordinate sets, and current color may be
used in processing each vertex. Normals are used by the GL in lighting calcula-
tions; the current normal is a three-dimensional vector that may be set by sending
three coordinates that specify it. Texture coordinates determine how a texture im-
age is mapped onto a primitive. Multiple sets of texture coordinates may be used
to specify how multiple texture images are mapped onto a primitive. The number
of texture units supported is implementation dependent but must be at least two.
The number of texture units supported can be obtained by querying the value of
MAX TEXTURE UNITS.
    A color is associated with each vertex. This color is either based on the current
color or produced by lighting, depending on whether or not lighting is enabled.


                          Version 1.1.12 (April 24, 2008)
2.6. PRIMITIVES AND VERTICES                                                         14


Texture coordinates are similarly associated with each vertex. Multiple sets of
texture coordinates may be associated with a vertex. Figure 2.2 summarizes the as-
sociation of auxiliary data with a transformed vertex to produce a processed vertex.
     The current values are part of GL state. Vertices, normals, and texture co-
ordinates are transformed. Color may be affected or replaced by lighting. The
processing indicated for each current value is applied for each vertex that is sent to
the GL.
     The methods by which vertices, normals, texture coordinates, and color are sent
to the GL, as well as how normals are transformed and how vertices are mapped to
the two-dimensional screen, are discussed later.
     Before color has been assigned to a vertex, the state required by a vertex is the
vertex’s coordinates, its normal, the current material properties (see section 2.12.2),
and its multiple texture coordinate sets. Because color assignment is done vertex-
by-vertex, a processed vertex comprises the vertex’s coordinates, its assigned color,
and its multiple texture coordinate sets.
     Figure 2.3 shows the sequence of operations that builds a primitive (point, line
segment, or triangle) from a sequence of vertices. After a primitive is formed, it
is clipped to a viewing volume. This may alter the primitive by altering vertex
coordinates, texture coordinates, and color. In the case of line and triangle primi-
tives, clipping may insert new vertices into the primitive. The vertices defining a
primitive to be rasterized have texture coordinates and color associated with them.

2.6.1   Primitive Types
A sequence of vertices is passed to the GL using the commands DrawArrays or
DrawElements (see section 2.8). There is no limit to the number of vertices that
may be specified, other than the size of the vertex arrays.
     The mode parameter of these commands determines the type of primitives to
be drawn using these coordinate sets. The types, and the corresponding mode
parameters, are:
     Points. A series of individual points may be specified with mode POINTS.
Each vertex defines a separate point or point sprite.
     Line Strips. A series of one or more connected line segments may be specified
with mode LINE STRIP. At least two vertices must be provided. In this case, the
first vertex specifies the first segment’s start point while the second vertex specifies
the first segment’s endpoint and the second segment’s start point. In general, the
ith vertex (for i > 1) specifies the beginning of the ith segment and the end of the
i − 1st. The last vertex specifies the end of the last segment. If only one vertex is
specified, then no primitive is generated.



                           Version 1.1.12 (April 24, 2008)
2.6. PRIMITIVES AND VERTICES                                                               15




      Vertex Array Coordinates
      and Current Values In

        VERTEX_ARRAY


                                            Vertex / Normal        Transformed
        NORMAL_ARRAY
                               Current      Transformation         Coordinates
        Normal3f               Normal




                                                                              Processed
                                                                              Vertex Out




        COLOR_ARRAY             Current
                                Colors        Lighting            Associated Data
        Color4f, Materialf
                              & Materials                           (Colors and
                                                                      Texture
                                                                   Coordinates)



                                Current
        TEXTURE_COORD_ARRAY
                                              Texture
                               Texture
        MultiTexCoord4f                       Matrix 0
                              Coord Set 0




                                Current
        TEXTURE_COORD_ARRAY
                                              Texture
                               Texture
        MultiTexCoord4f                       Matrix 1
                              Coord Set 1




  Figure 2.2. Creation of a processed vertex from vertex array coordinates and current
  values. Two texture units are shown; however, multitexturing may support a greater
  number of units depending on the implementation.




                                Version 1.1.12 (April 24, 2008)
2.6. PRIMITIVES AND VERTICES                                                           16




                                                      Point culling;
             Coordinates
                                                      Line Segment
                                                       or Triangle
                                      Point,             Clipping
                                Line Segment, or
       Processed
                                    Triangle                           Rasterization
       Vertices
                                   (Primitive)
            Associated Data        Assembly
                                                          Color
                                                       Processing




                                  Primitive type
                              (from DrawArrays or
                              DrawElements mode)




  Figure 2.3. Primitive assembly and processing.




                                 Version 1.1.12 (April 24, 2008)
2.6. PRIMITIVES AND VERTICES                                                                  17




    2               4                 2                          2
                                                  3                                      6
                                                                           4
                                                      4

                                                          5                          5
    1           3            5        1                          1             3

             (a)                            (b)                                (c)


   Figure 2.4. (a) A triangle strip. (b) A triangle fan. (c) Independent triangles. The
   numbers give the sequencing of the vertices in order within the vertex arrays. Note
   that in (a) and (b) triangle edge ordering is determined by the first triangle, while in
   (c) the order of each triangle’s edges is independent of the other triangles.




     The required state consists of the processed vertex produced from the preceding
vertex that was passed (so that a line segment can be generated from it to the current
vertex), and a boolean flag indicating if the current vertex is the first vertex.
     Line Loops. Line loops may be specified with mode LINE LOOP. Loops are
the same as line strips except that a final segment is added from the final specified
vertex to the first vertex.
     The required state consists of the processed first vertex, in addition to the state
required for line strips.
     Separate Lines. Individual line segments, each specified by a pair of vertices,
may be specified with mode LINES. The first two vertices passed define the first
segment, with subsequent pairs of vertices each defining one more segment. If the
number of specified vertices is odd, then the last one is ignored. The required state
is the same as for line strips but it is used differently: a processed vertex holding
the first endpoint of the current segment, and a boolean flag indicating whether the
current vertex is odd or even (a segment start or end).
     Triangle strips. A triangle strip is a series of triangles connected along
shared edges, specified by giving a series of defining vertices with mode
TRIANGLE STRIP. In this case, the first three vertices define the first triangle (and
their order is significant). Each subsequent vertex defines a new triangle using
that point along with two vertices from the previous triangle. If fewer than three
vertices are specified, no primitives are produced. See Figure 2.4.


                            Version 1.1.12 (April 24, 2008)
2.7. CURRENT VERTEX STATE                                                                   18


     The required state to support triangle strips consists of a flag indicating if the
first triangle has been completed, two stored processed vertices, (called vertex A
and vertex B), and a one bit pointer indicating which stored vertex will be replaced
with the next vertex. The pointer is initialized to point to vertex A. Each successive
vertex toggles the pointer. Therefore, the first vertex is stored as vertex A, the
second stored as vertex B, the third stored as vertex A, and so on. Any vertex after
the second one sent forms a triangle from vertex A, vertex B, and the current vertex
(in that order).
     Triangle fans. A triangle fan is the same as a triangle strip with one excep-
tion: each vertex after the first always replaces vertex B of the two stored vertices.
Triangle fans are specified with mode TRIANGLE FAN.
     Separate Triangles. Separate triangles are specified with mode TRIANGLES.
In this case, The 3i + 1st, 3i + 2nd, and 3i + 3rd vertices (in that order) determine
a triangle for each i = 0, 1, . . . , n − 1, where there are 3n + k vertices drawn. k is
either 0, 1, or 2; if k is not zero, the final k vertices are ignored. For each triangle,
vertex A is vertex 3i and vertex B is vertex 3i + 1. Otherwise, separate triangles
are the same as a triangle strip.
     The order of the vertices in a triangle generated from a triangle strip, triangle
fan, or separate triangles is significant in lighting and polygon rasterization (see
sections 2.12.1 and 3.5.1).


2.7     Current Vertex State
Current values are used in associating auxiliary data with a vertex when a vertex
array defining that data is not enabled, as described in section 2.8. A current value
may be changed at any time by issuing an appropriate command.
    The current RGBA color is set using the commands

      void Color4{xf}( T red, T green, T blue, T alpha );
      void Color4ub( ubyte red, ubyte green, ubyte blue,
         ubyte alpha );

    The conversion of integer color components (R, G, B, and A) to floating-point
values is discussed in section 2.12.
    Color4f and Color4x accept values nominally between 0.0 and 1.0. 0.0 corre-
sponds to the minimum while 1.0 corresponds to the maximum (machine depen-
dent) value that a component may take on in the framebuffer (see section 2.12 on
colors and coloring). Values outside [0, 1] are not clamped.
    The current normal is set using the commands


                               Version 1.1.12 (April 24, 2008)
2.8. VERTEX ARRAYS                                                                  19


      void Normal3{xf}( T nx, T ny, T nz );

    The current homogeneous texture cordinates are set using the commands

      void MultiTexCoord4{xf}( enum texture, T s, T t, T r, T q );

The current coordinate set to be modified is given by the texture parameter, and
the s, t, r, and q coordinates are set as specified. texture is a symbolic con-
stant of the form TEXTUREi, indicating that texture coordinate set i is to be mod-
ified. The constants obey TEXTUREi = TEXTURE0 + i (i is in the range 0 to
k − 1, where k is the implementation-dependent number of texture units defined
by MAX TEXTURE UNITS).
     Gets of CURRENT TEXTURE COORDS return the texture coordinate set defined
by the value of ACTIVE TEXTURE (see section 2.8).
     Specifying an invalid texture coordinate set for the texture argument of Multi-
TexCoord4 results in undefined behavior.
     The state required to support vertex specification consists of four values to
store the current RGBA color, three values to store the current normal, and four
values for each of the texture units supported by the implementation to store the
current texture coordinates s, t, r, and q. The initial current color is (R, G, B, A) =
(1, 1, 1, 1). The initial current normal has coordinates (0, 0, 1). The initial values
of s, t, and r of the current texture coordinates for each texture unit are zero, and
the initial value of q is one.


2.8    Vertex Arrays
Vertex data is placed into arrays stored in the client’s address space (described
here) or in the server’s address space (described in section 2.9). Blocks of data in
these arrays may then be used to specify multiple geometric primitives through the
execution of a single GL command. The client may specify up to four plus the value
of MAX TEXTURE UNITS arrays: one each to store vertex coordinates, normals,
colors, point sizes, and one or more texture coordinate sets. The commands

      void VertexPointer( int size, enum type, sizei stride,
         void *pointer );

      void NormalPointer( enum type, sizei stride,
         void *pointer );

      void ColorPointer( int size, enum type, sizei stride,
         void *pointer );

                          Version 1.1.12 (April 24, 2008)
2.8. VERTEX ARRAYS                                                                         20


     Command                     Sizes   Types
     VertexPointer               2,3,4   byte, short, fixed, float
     NormalPointer                 3     byte, short, fixed, float
     ColorPointer                  4     ubyte, fixed, float
     PointSizePointerOES           1     fixed, float
     TexCoordPointer             2,3,4   byte, short, fixed, float

          Table 2.4: Vertex array sizes (values per vertex) and data types.



      void PointSizePointerOES( enum type, sizei stride,
         void *pointer );

      void TexCoordPointer( int size, enum type, sizei stride,
         void *pointer );

describe the locations and organizations of these arrays. For each command, type
specifies the data type of the values stored in the array. size, when present, indicates
the number of values per vertex that are stored in the array. Because normals are
always specified with three values and point sizes are always specified with one
value, NormalPointer and PointSizePointerOES have no size argument. Table
2.4 indicates the allowable values for size and type (when present). For type the
values BYTE, UNSIGNED BYTE, SHORT, FIXED, and FLOAT, indicate types byte,
ubyte, short, fixed, and float, respectively. The error INVALID VALUE is
generated if size is specified with a value other than that indicated in the table.
     The one, two, three, or four values in an array that correspond to a single vertex
comprise an array element. The values within each array element are stored se-
quentially in memory. If stride is specified as zero, then array elements are stored
sequentially as well. The error INVALID VALUE is generated if stride is negative.
Otherwise pointers to the ith and (i + 1)st elements of an array differ by stride
basic machine units (typically unsigned bytes), the pointer to the (i + 1)st element
being greater. For each command, pointer specifies the location in memory of the
first value of the first element of the array being specified.
     An individual array is enabled or disabled by calling one of

      void EnableClientState( enum array );
      void DisableClientState( enum array );

with array set to VERTEX ARRAY, NORMAL ARRAY, COLOR ARRAY,
POINT SIZE ARRAY OES, or TEXTURE COORD ARRAY, for the vertex, normal,
color, point size, or texture coordinate array, respectively.

                               Version 1.1.12 (April 24, 2008)
2.8. VERTEX ARRAYS                                                                     21


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
tion 2.7.

    Transferring Array Elements

     When an array element i is transferred to the GL by the DrawArrays or
DrawElements commands, each enabled array is treated differently.
     For the vertex array, if size is two then the x and y coordinates of the vertex are
specified by the array; the z and w coordinates are implicitly set to zero and one,
respectively. If size is three then x, y, and z are specified and w is implicitly set to
one. If size is four then all coordinates are specified, allowing the definition of an
arbitrary point in projective space.
     For the color array, all four components are always specified. If the color array
is not enabled, then the current color defined by the Color commands is used.
     For the normal array, all three coordinates are always specified. Byte, short,
or integer values are converted to floating-point values as indicated for the corre-
sponding (signed) type in table 2.7. If the normal array is not enabled, then the
current normal defined by the Normal commands is used.
     For the point size array, the single size is always specified. If the point size ar-
ray is not enabled, then the current point size defined by PointSize (see section 3.3)
is used.
     For the texture coordinate arrays, if size is two then the s and t coordinates are
specified and the r and q coordinates are implicitly set to zero and one, respectively.
If size is three then s, t, and r are specified and q is implicitly set to one. If size is
four then all coordinates are specified. If a texture coordinate array is not enabled,
then the current texture coordinate defined by the MultiTexCoord commands is
used.
     The command


                           Version 1.1.12 (April 24, 2008)
2.9. BUFFER OBJECTS                                                                 22


      void DrawArrays( enum mode, int first, sizei count );
constructs a sequence of geometric primitives by successively transferring ele-
ments f irst through f irst + count − 1 of each enabled array to the GL. mode
specifies what kind of primitives are constructed, as defined in section 2.6.1.
    The current color, normal, point size, and texture coordinates each become
indeterminate after the execution of DrawArrays, if the corresponding array is
enabled. Current values corresponding to disabled arrays are not modified by the
execution of DrawArrays.
    Specifying f irst < 0 results in undefined behavior. Generating the error
INVALID VALUE is recommended in this case.
    The command
      void DrawElements( enum mode, sizei count, enum type,
         void *indices );
constructs a sequence of geometric primitives by successively transferring the
count elements whose indices are stored in indices to the GL. The ith element
transferred by DrawElements will be taken from element indices[i] of each en-
abled array. type must be one of UNSIGNED BYTE or UNSIGNED SHORT, indicating
that the values in indices are indices of GL type ubyte or ushort, respectively.
mode specifies what kind of primitives are constructed; it accepts the same values
as the mode parameter of DrawArrays.
     The current color, normal, point size, and texture coordinates are each indeter-
minate after the execution of DrawElements, if the corresponding array is enabled.
Current values corresponding to disabled arrays are not modified by the execution
of DrawElements.
     If the number of supported texture units (the value of MAX TEXTURE UNITS) is
k, then the client state required to implement vertex arrays consists of an integer for
the client active texture unit selector, 4 + k boolean values, 4 + k memory pointers,
4 + k integer stride values, 4 + k symbolic constants representing array types, and
2 + k integers representing values per element. In the initial state, the client active
texture unit selector is TEXTURE0, the boolean values are each false, the memory
pointers are each null, the strides are each zero, and the integers representing values
per element are each four. The array types are each FLOAT for the Common profile
and FIXED for the Common-Lite profile.


2.9    Buffer Objects
The vertex data arrays described in section 2.8 are stored in client memory. It is
sometimes desirable to store frequently used client data, such as vertex array data,

                          Version 1.1.12 (April 24, 2008)
2.9. BUFFER OBJECTS                                                               23


  Name               Type        Initial Value   Legal Values
  BUFFER SIZE        integer           0         any non-negative integer
  BUFFER USAGE       enum      STATIC DRAW       STATIC DRAW, DYNAMIC DRAW

               Table 2.5: Buffer object parameters and their values.


in high-performance server memory. GL buffer objects provide a mechanism that
clients can use to allocate, initialize, and render from such memory.
    The name space for buffer objects is the unsigned integers, with zero re-
served for the GL. A buffer object is created by binding an unused name to
ARRAY BUFFER. The binding is effected by calling

      void BindBuffer( enum target, uint buffer );

with target set to ARRAY BUFFER and buffer set to the unused name. The resulting
buffer object is a new state vector, initialized with a zero-sized memory buffer, and
comprising the state values listed in Table 2.5.
    BindBuffer may also be used to bind an existing buffer object. If the bind is
successful no change is made to the state of the newly bound buffer object, and any
previous binding to target is broken.
    While a buffer object is bound, GL operations on the target to which it is bound
affect the bound buffer object, and queries of the target to which a buffer object is
bound return state from the bound object.
    In the initial state the reserved name zero is bound to ARRAY BUFFER. There
is no buffer object corresponding to the name zero, so client attempts to modify
or query buffer object state for the target ARRAY BUFFER while zero is bound will
generate GL errors.
    Buffer objects are deleted by calling

      void DeleteBuffers( sizei n, const uint *buffers );

buffers contains n names of buffer objects to be deleted. After a buffer object is
deleted it has no contents, and its name is again unused. Unused names in buffers
are silently ignored, as is the value zero.
    The command

      void GenBuffers( sizei n, uint *buffers );

returns n previously unused buffer object names in buffers. These names are
marked as used, for the purposes of GenBuffers only, but they acquire buffer state
only when they are first bound, just as if they were unused.

                          Version 1.1.12 (April 24, 2008)
2.9. BUFFER OBJECTS                                                                24


                              Name                Value
                              BUFFER SIZE         size
                              BUFFER USAGE        usage

                        Table 2.6: Buffer object initial state.



    While a buffer object is bound, any GL operations on that object affect any
other bindings of that object. If a buffer object is deleted while it is bound, all
bindings to that object in the current context (i.e. in the thread that called Delete-
Buffers) are reset to zero. Bindings to that buffer in other contexts and other
threads are not affected, but attempting to use a deleted buffer in another thread
produces undefined results, including but not limited to possible GL errors and
rendering corruption. Using a deleted buffer in another context or thread may not,
however, result in program termination.
    The data store of a buffer object is created and initialized by calling

      void BufferData( enum target, sizeiptr size, const
         void *data, enum usage );

with target set to ARRAY BUFFER, size set to the size of the data store in basic
machine units, and data pointing to the source data in client memory. If data is
non-null, then the source data is copied to the buffer object’s data store. If data is
null, then the contents of the buffer object’s data store are undefined.
    usage is specified as one of two enumerated values, indicating the expected
application usage pattern of the data store. The values are:

STATIC DRAW The data store contents will be specified once by the application,
      and used many times as the source for GL drawing commands.

DYNAMIC DRAW The data store contents will be respecified repeatedly by the ap-
      plication, and used many times as the source for GL drawing commands.

    usage is provided as a performance hint only. The specified usage value does
not constrain the actual usage pattern of the data store.
    BufferData deletes any existing data store, and sets the values of the buffer
object’s state variables as shown in table 2.6.
    Clients must align data elements consistent with the requirements of the client
platform, with an additional base-level requirement that an offset within a buffer to
a datum comprising N basic machine units be a multiple of N .


                          Version 1.1.12 (April 24, 2008)
2.9. BUFFER OBJECTS                                                                         25


       If the GL is unable to create a data store of the requested size, the error
OUT OF MEMORY is generated.
    To modify some or all of the data contained in a buffer object’s data store, the
client may use the command

         void BufferSubData( enum target, intptr offset,
            sizeiptr size, const void *data );

with target set to ARRAY BUFFER. offset and size indicate the range of data in the
buffer object that is to be replaced, in terms of basic machine units. data specifies a
region of client memory size basic machine units in length, containing the data that
replace the specified buffer range. An INVALID VALUE error is generated if offset
or size is less than zero, or if offset + size is greater than the value of BUFFER SIZE.

2.9.1      Vertex Arrays in Buffer Objects
Blocks of vertex array data may be stored in buffer objects with the same format
and layout options supported for client-side vertex arrays.
    The client state associated with each vertex array type includes a buffer object
binding point. The commands that specify the locations and organizations of vertex
arrays copy the buffer object name that is bound to ARRAY BUFFER to the binding
point corresponding to the vertex array of the type being specified. For example,
the NormalPointer command copies the value of ARRAY BUFFER BINDING (the
queriable name of the buffer binding corresponding to the target ARRAY BUFFER)
to the client state variable NORMAL ARRAY BUFFER BINDING.
    Rendering commands DrawArrays and DrawElements operate as previously
defined, except that data for enabled vertex arrays are sourced from buffers if the
array’s buffer binding is non-zero. When an array is sourced from a buffer object,
the pointer value of that array is used to compute an offset, in basic machine units,
into the data store of the buffer object. This offset is computed by subtracting a
null pointer from the pointer value, where both pointers are treated as pointers to
basic machine units2 .
    It is acceptable for vertex arrays to be sourced from any combination of client
memory and various buffer objects during a single rendering operation.
   2
     To resume using client-side vertex arrays after a buffer object has been bound, call Bind-
Buffer(ARRAY BUFFER,0) and then specify the client vertex array pointer using the appropriate
command from section 2.8.




                             Version 1.1.12 (April 24, 2008)
2.10. COORDINATE TRANSFORMATIONS                                                 26


2.9.2   Array Indices in Buffer Objects
Blocks of array indices may be stored in buffer objects with the same format op-
tions that are supported for client-side index arrays. Initially zero is bound to
ELEMENT ARRAY BUFFER, indicating that DrawElements is to source its indices
from arrays passed as the indices parameters.
    A buffer object is bound to ELEMENT ARRAY BUFFER by calling BindBuffer
with target set to ELEMENT ARRAY BUFFER, and buffer set to the name of the buffer
object. If no corresponding buffer object exists, one is initialized as defined in
section 2.9.
    The commands BufferData and BufferSubData may be used with target
set to ELEMENT ARRAY BUFFER. In such event, these commands operate in the
same fashion as described in section 2.9, but on the buffer currently bound to the
ELEMENT ARRAY BUFFER target.
    While a non-zero buffer object name is bound to ELEMENT ARRAY BUFFER,
DrawElements sources its indices from that buffer object, using its indices pa-
rameter as offsets into the buffer object in the same fashion as described in sec-
tion 2.9.1.
    Buffer objects created by binding an unused name to ARRAY BUFFER and to
ELEMENT ARRAY BUFFER are formally equivalent, but the GL may make different
choices about storage implementation based on the initial binding. In some cases
performance will be optimized by storing indices and array data in separate buffer
objects, and by creating those buffer objects with the corresponding binding points.


2.10     Coordinate Transformations
Vertices, normals, and texture coordinates are transformed before their coordinates
are used to produce an image in the framebuffer. We begin with a description of
how vertex coordinates are transformed and how this transformation is controlled.
    Figure 2.5 diagrams the sequence of transformations that are applied to ver-
tices. The vertex coordinates that are presented to the GL are termed object co-
ordinates. The model-view matrix is applied to these coordinates to yield eye co-
ordinates. Then another matrix, called the projection matrix, is applied to eye
coordinates to yield clip coordinates. A perspective division is carried out on clip
coordinates to yield normalized device coordinates. A final viewport transforma-
tion is applied to convert these coordinates into window coordinates.
    Object coordinates, eye coordinates, and clip coordinates are four-dimensional,
consisting of x, y, z, and w coordinates (in that order). The model-view and pro-
jection matrices are thus 4 × 4.



                         Version 1.1.12 (April 24, 2008)
2.10. COORDINATE TRANSFORMATIONS                                                                         27



                                                                                           Normalized
      Object      Model−View      Eye        Projection          Clip        Perspective     Device
    Coordinates                Coordinates                    Coordinates     Division     Coordinates
                   Matrix                        Matrix




                                                                               Viewport     Window
                                                                            Transformation Coordinates




   Figure 2.5. Vertex transformation sequence.



                                                    xo
                                                                       
                                                   yo 
    If a vertex in object coordinates is given by 
                                                   zo  and the model-view matrix
                                                       

                                                    wo
is M , then the vertex’s eye coordinates are found as

                                       xe          xo
                                                                
                                      ye        yo 
                                      z e  = M  zo  .
                                                   

                                       we          wo

Similarly, if P is the projection matrix, then the vertex’s clip coordinates are

                                       xc         xe
                                                               
                                      yc       ye 
                                      zc  = P  z e  .
                                                   

                                       wc         we

The vertex’s normalized device coordinates are then
                                      xd       xc /wc
                                                                
                                     yd  =  yc /wc  .
                                      zd       zc /wc




                               Version 1.1.12 (April 24, 2008)
2.10. COORDINATE TRANSFORMATIONS                                                       28


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

      void DepthRangef( clampf n, clampf f );
      void DepthRangex( clampx n, clampx f );

Each of n and f are clamped to lie within [0, 1], as are all arguments of type clampf
or clampx. zw is taken to be represented in fixed-point with at least as many bits
as there are in the depth buffer of the framebuffer. We assume that the fixed-point
representation used represents each value k/(2m − 1), where k ∈ {0, 1, . . . , 2m −
1}, as k (e.g. 1.0 is represented in binary as a string of all ones).
    Viewport transformation parameters are specified using

      void Viewport( int x, int y, sizei w, sizei h );

where x and y give the x and y window coordinates of the viewport’s lower left
corner and w and h give the viewport’s width and height, respectively. The viewport
parameters shown in the above equations are found from these values as ox =
x + w/2 and oy = y + h/2; px = w, py = h.
    Viewport width and height are clamped to implementation-dependent maxi-
mums when specified. The maximum width and height may be found by issuing
an appropriate Get command (see Chapter 6). The maximum viewport dimen-
sions must be greater than or equal to the visible dimensions of the display being
rendered to. INVALID VALUE is generated if either w or h is negative.
    The state required to implement the viewport transformation is four integers
and two clamped floating-point values. In the initial state, w and h are set to the
width and height, respectively, of the window into which the GL is to do its ren-
dering. ox and oy are set to w/2 and h/2, respectively. n and f are set to 0.0 and
1.0, respectively.



                           Version 1.1.12 (April 24, 2008)
2.10. COORDINATE TRANSFORMATIONS                                                 29


2.10.2   Matrices
The projection matrix and model-view matrix are set and modified with a variety
of commands. The affected matrix is determined by the current matrix mode. The
current matrix mode is set with

      void MatrixMode( enum mode );

which takes one of the pre-defined constants TEXTURE, MODELVIEW, or
PROJECTION as the argument value. TEXTURE is described later in section 2.10.2.
If the current matrix mode is MODELVIEW, then matrix operations apply to the
model-view matrix; if PROJECTION, then they apply to the projection matrix.
    The two basic commands for affecting the current matrix are

      void LoadMatrix{xf}( T m[16] );
      void MultMatrix{xf}( T m[16] );

LoadMatrix takes a pointer to a 4 × 4 matrix stored in column-major order as 16
consecutive fixed- or floating-point values, i.e. as

                               a1    a5   a9    a13
                                                  
                              a2    a6   a10   a14 
                                                   .
                              a3    a4   a11   a15 
                               a4    a8   a12   a16
(This differs from the standard row-major C ordering for matrix elements. If the
standard ordering is used, all of the subsequent transformation equations are trans-
posed, and the columns representing vectors become rows.)
     The specified matrix replaces the current matrix with the one pointed to. Mult-
Matrix takes the same type argument as LoadMatrix, but multiplies the current
matrix by the one pointed to and replaces the current matrix with the product. If C
is the current matrix and M is the matrix pointed to by MultMatrix’s argument,
then the resulting current matrix, C , is

                                    C = C · M.

   The command

      void LoadIdentity( void );

effectively calls LoadMatrix with the identity matrix:



                         Version 1.1.12 (April 24, 2008)
2.10. COORDINATE TRANSFORMATIONS                                                 30



                                  1       0   0    0
                                                   
                                0        1   0    0
                                                    .
                                0        0   1    0
                                  0       0   0    1
    There are a variety of other commands that manipulate matrices. Rotate,
Translate, Scale, Frustum, and Ortho manipulate the current matrix. Each com-
putes a matrix and then invokes MultMatrix with this matrix. In the case of

       void Rotate{xf}( T θ, T x, T y, T z );

θ gives an angle of rotation in degrees; the coordinates of a vector v are given by
v = (x y z)T . The computed matrix is a counter-clockwise rotation about the line
through the origin with the specified axis when that axis is pointing up (i.e. the
right-hand rule determines the sense of the rotation angle). The matrix is thus

                                                   0
                                                   
                                
                                         R        0.
                                                  0
                                    0     0   0    1
Let u = v/||v|| = ( x    y    z )T . If

                                 0            −z      y
                                                         

                             S= z             0     −x 
                                −y            x       0

then
                      R = uuT + cos θ(I − uuT ) + sin θS.
   The arguments to

       void Translate{xf}( T x, T y, T z );

give the coordinates of a translation vector as (x y z)T . The resulting matrix is a
translation by the specified vector:

                                  1       0   0    x
                                                   
                                0        1   0    y
                                                    .
                                0        0   1    z
                                  0       0   0    1

       void Scale{xf}( T x, T y, T z );

                         Version 1.1.12 (April 24, 2008)
2.10. COORDINATE TRANSFORMATIONS                                                     31


produces a general scaling along the x-, y-, and z- axes. The corresponding matrix
is
                                  x 0 0 0
                                               
                               0 y 0 0
                               0 0 z 0.
                                               

                                  0 0 0 1
    For

      void Frustum{xf}( T l, T r, T b, T t, T n, T f );

the coordinates (l b − n)T and (r t − n)T specify the points on the near clipping
plane that are mapped to the lower left and upper right corners of the window,
respectively (assuming that the eye is located at (0 0 0)T ). f gives the distance
from the eye to the far clipping plane. If either n or f is less than or equal to zero,
l is equal to r, b is equal to t, or n is equal to f , the error INVALID VALUE results.
The corresponding matrix is
                           2n             r+l
                                    0                 0
                                                             
                             r−l           r−l
                           0       2n     t+b
                                   t−b     t−b        0    
                                                           .
                                                          
                                          − ff +n   − 2f n 
                          
                           0       0          −n     f −n
                              0     0      −1         0

      void Ortho{xf}( T l, T r, T b, T t, T n, T f );

describes a matrix that produces parallel projection. (l b − n)T and (r t − n)T
specify the points on the near clipping plane that are mapped to the lower left and
upper right corners of the window, respectively. f gives the distance from the eye
to the far clipping plane. If l is equal to r, b is equal to t, or n is equal to f , the
error INVALID VALUE results. The corresponding matrix is
                           2                          r+l
                                    0       0       − r−l
                                                             
                             r−l
                                    2                  t+b 
                           0
                                   t−b      0       − t−b 
                                                            .
                          
                                              2
                                                    − ff +n
                          
                           0       0     − f −n         −n
                                                            
                              0     0       0          1
   For each texture unit, a 4 × 4 matrix is applied to the corresponding texture
coordinates. This matrix is applied as

                           m1      m5    m9     m13     s
                                                     
                          m2      m6    m10    m14   t 
                                                     
                                                         ,
                          m3      m7    m11    m15   r 
                           m4      m8    m12    m16     q

                           Version 1.1.12 (April 24, 2008)
2.10. COORDINATE TRANSFORMATIONS                                                   32


where the left matrix is the current texture matrix. The matrix is applied to the
current texture coordinates, and the resulting transformed coordinates become the
texture coordinates associated with a vertex. Setting the matrix mode to TEXTURE
causes the already described matrix operations to apply to the texture matrix.
    There is also a corresponding texture matrix stack for each texture unit. To
change the stack affected by matrix operations, set the active texture unit selector
by calling

      void ActiveTexture( enum texture );

The selector also affects calls modifying texture environment state, texture coordi-
nate generation state, texture binding state, and queries of all these state values as
well as current texture coordinates.
     Specifying an invalid texture generates the error INVALID ENUM. Valid values
of texture are the same as for the MultiTexCoord commands described in sec-
tion 2.7.
     There is a stack of matrices for each of matrix modes MODELVIEW and
PROJECTION, and for each texture unit. For MODELVIEW mode, the stack depth
is at least 16 (that is, there is a stack of at least 16 model-view matrices). For the
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
    The state required to implement transformations consists of an integer for the
active texture unit selector, a four-valued integer indicating the current matrix
mode, one stack of at least two 4 × 4 matrices for each of PROJECTION and each
texture unit, TEXTURE; and a stack of at least 16 4 × 4 matrices for MODELVIEW.

                          Version 1.1.12 (April 24, 2008)
2.10. COORDINATE TRANSFORMATIONS                                                                 33


Each matrix stack has an associated stack pointer. Initially, there is only one matrix
on each stack, and all matrices are set to the identity. The initial active texture unit
selector is TEXTURE0, and the initial matrix mode is MODELVIEW.

2.10.3     Normal Transformation
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
nates by: 3

                  ( nx     ny     nz     q ) = ( nx      ny     nz    q ) · M −1
            x
                
          y
           z  are the associated vertex coordinates, then
where, if    

            w           
                        
                        
                        
                           0,                         w = 0,
                                              x
                                            
                        
                   q=      −( nx ny nz ) y                                                   (2.1)
                        
                        
                        
                                             z
                        
                                      w           , w=0
    Implementations may choose instead to transform ( nx                  ny    nz ) to eye coor-
dinates using

                       ( nx     ny     nz ) = ( nx      ny     nz ) · Mu −1
   3
     Here, normals are treated as row vectors and transformed by postmultiplication by the inverse of
the transformation matrix. If normals are treated as column vectors, then the transformation would
instead be performed by premultiplying the normal by the inverse transpose, M −T .


                                Version 1.1.12 (April 24, 2008)
2.10. COORDINATE TRANSFORMATIONS                                                   34


where Mu is the upper leftmost 3x3 matrix taken from M .
   Rescale multiplies the transformed normals by a scale factor

                    ( nx     ny    nz ) = f ( nx            ny          nz )
If rescaling is disabled, then f = 1. If rescaling is enabled, then f is computed as
                                               1
                           f=√           2
                                   m31       + m32 2 + m33 2
mij denotes the matrix element in row i and column j of M −1 , numbering the
topmost row of the matrix as row 1 and the leftmost column as column 1.
    Note that if the normals sent to GL were unit length and the model-view matrix
uniformly scales space, then rescale makes the transformed normals unit length.
    Alternatively, an implementation may choose f as
                                                1
                             f=
                                    nx + ny 2 + nz
                                         2                      2


recomputing f for each normal. This makes all non-zero length normals unit length
regardless of their input length and the nature of the model-view matrix.
    After rescaling, the final transformed normal used in lighting, nf , is computed
as

                            nf = m ( nx         ny        nz )
If normalization is disabled, then m = 1. Otherwise
                                                1
                            m=
                                         2           2              2
                                    nx       + ny        + nz
    Because we specify neither the floating-point format nor the means for matrix
inversion, we cannot specify behavior in the case of a poorly-conditioned (nearly
singular) model-view matrix M . In case of an exactly singular matrix, the trans-
formed normal is undefined. If the GL implementation determines that the model-
view matrix is uninvertible, then the entries in the inverted matrix are arbitrary. In
any case, neither normal transformation nor use of the transformed normal may
lead to GL interruption or termination.




                           Version 1.1.12 (April 24, 2008)
2.11. CLIPPING                                                                    35


2.11     Clipping
Primitives are clipped to the clip volume. In clip coordinates, the view volume is
defined by
                                 −wc ≤ xc ≤ wc
                                  −wc ≤ yc ≤ wc .
                                  −wc ≤ zc ≤ wc
This view volume may be further restricted by as many as n client-defined clip
planes to generate the clip volume. (n is an implementation dependent maximum
that must be at least 1.) Each client-defined plane specifies a half-space. The
clip volume is the intersection of all such half-spaces with the view volume (if no
client-defined clip planes are enabled, the clip volume is the view volume).
    A client-defined clip plane is specified with

       void ClipPlane{xf}( enum p, const T eqn[4] );

The value of the first argument, p, is a symbolic constant, CLIP PLANEi, where i
is an integer between 0 and n − 1, indicating one of n client-defined clip planes.
eqn is an array of four values. These are the coefficients of a plane equation in
object coordinates: p1 , p2 , p3 , and p4 (in that order). The inverse of the current
model-view matrix is applied to these coefficients, at the time they are specified,
yielding
                 ( p1 p2 p3 p4 ) = ( p1 p2 p3 p4 ) M −1
(where M is the current model-view matrix; the resulting plane equation is unde-
fined if M is singular and may be inaccurate if M is poorly-conditioned) to obtain
the plane equation coefficients in eye coordinates. All points with eye coordinates
( xe ye ze we )T that satisfy

                                                 xe
                                                   
                                                ye 
                         ( p1   p2   p3         ze  ≥ 0
                                          p4 )     

                                                 we

lie in the half-space defined by the plane; points that do not satisfy this condition
do not lie in the half-space.
     Client-defined clip planes are enabled with the generic Enable command and
disabled with the Disable command. The value of the argument to either com-
mand is CLIP PLANEi where i is an integer between 0 and n; specifying a value
of i enables or disables the plane equation with index i. The constants obey
CLIP PLANEi = CLIP PLANE0 + i.


                          Version 1.1.12 (April 24, 2008)
2.11. CLIPPING                                                                       36


     If the primitive under consideration is a point, then clipping passes it un-
changed if it lies within the clip volume; otherwise, it is discarded.
     If the primitive is a line segment, then clipping does nothing to it if it lies en-
tirely within the clip volume and discards it if it lies entirely outside the volume.
If part of the line segment lies in the volume and part lies outside, then the line
segment is clipped and new vertex coordinates are computed for one or both ver-
tices. A clipped line segment endpoint lies on both the original line segment and
the boundary of the clip volume.
     This clipping produces a value, 0 ≤ t ≤ 1, for each clipped vertex. If the
coordinates of a clipped vertex are P and the original vertices’ coordinates are P1
and P2 , then t is given by

                               P = tP1 + (1 − t)P2 .

The value of t is used in color and texture coordinate clipping (section 2.12.7).
     If the primitive is a triangle, then it is passed if every one of its edges lies
entirely inside the clip volume and either clipped or discarded otherwise. Clip-
ping may cause triangle edges to be clipped, but because connectivity must be
maintained, these clipped edges are connected by new edges that lie along the clip
volume’s boundary. Thus, clipping may require the introduction of new vertices
into a triangle, creating a more general polygon.
     If it happens that a triangle intersects an edge of the clip volume’s boundary,
then the clipped triangle must include a point on this boundary edge.
     A line segment or triangle whose vertices have wc values of differing signs may
generate multiple connected components after clipping. GL implementations are
not required to handle this situation. That is, only the portion of the primitive that
lies in the region of wc > 0 need be produced by clipping.
     Primitives rendered with clip planes must satisfy a complementarity crite-
rion. Suppose a single clip plane with coefficients ( p1 p2 p3 p4 ) (or a num-
ber of similarly specified clip planes) is enabled and a series of primitives are
drawn. Next, suppose that the original clip plane is respecified with coefficients
( −p1 −p2 −p3 −p4 ) (and correspondingly for any other clip planes) and
the primitives are drawn again (and the GL is otherwise in the same state). In this
case, primitives must not be missing any pixels, nor may any pixels be drawn twice
in regions where those primitives are cut by the clip planes.
     The state required for clipping is at least one set of plane equations (each set
consisting of four coefficients) and at least one corresponding bit indicating which
of these client-defined plane equations are enabled. In the initial state, all client-
defined plane equation coefficients are zero and all planes are disabled.



                           Version 1.1.12 (April 24, 2008)
2.12. COLORS AND COLORING                                                                 37




       [0,2k−1]     Convert to
                     [0.0,1.0]             Current
                                           RGBA                              Clamp to
                                            Color        Lighting            [0.0, 1.0]
                    Convert to
    [−2k,2k−1]
                    [−1.0,1.0]
         float
                                                      Color
                                                     Clipping


                              Convert to                              Flatshade?
                             fixed−point
                                                     Primitive
                                                     Clipping




   Figure 2.6. Processing of colors. See Table 2.7 for the interpretation of k.




2.12      Colors and Coloring
Figure 2.6 diagrams the processing of colors before rasterization. Incoming colors
arrive in one of several formats. Table 2.7 summarizes the conversions that take
place on R, G, B, and A components depending on which version of the Color
command was invoked to specify the components. As a result of limited precision,
some converted values will not be represented exactly.
     Next, lighting, if enabled, produces a color. If lighting is disabled, the current
color is used in further processing. After lighting, colors are clamped to the range
[0, 1]. After clamping, a primitive may be flatshaded, indicating that all vertices
of the primitive are to have the same colors. Finally, if a primitive is clipped, then
colors (and texture coordinates) must be computed at the vertices introduced or
modified by clipping.

2.12.1     Lighting
GL lighting computes colors for each vertex sent to the GL. This is accomplished
by applying an equation defined by a client-specified lighting model to a collection
of parameters that can include the vertex coordinates, the coordinates of one or
more light sources, the current normal, and parameters defining the characteristics
of the light sources and a current material.
    Lighting is turned on or off using the generic Enable or Disable commands


                            Version 1.1.12 (April 24, 2008)
2.12. COLORS AND COLORING                                                         38


                          GL Type         Conversion
                          ubyte           c/(28 − 1)
                          byte        (2c + 1)/(28 − 1)
                          ushort          c/(216 − 1)
                          short       (2c + 1)/(216 − 1)
                          fixed              c/216
                          float                c

Table 2.7: Component conversions. Color and normal components (c) are con-
verted to an internal floating-point representation (f ), using the equations in this
table. All arithmetic is done in the internal floating-point format. These conver-
sions apply to components specified as parameters to GL commands and to com-
ponents in pixel data. The equations remain the same even if the implemented
ranges of the GL data types are greater than the minimum required ranges. (Refer
to table 2.2)



with the symbolic value LIGHTING. If lighting is off, the current color is assigned
to the vertex color. If lighting is on, the color computed from the current lighting
parameters is assigned to the vertex color.

Lighting Operation
A lighting parameter is of one of five types: color, position, direction, real, or
boolean. A color parameter consists of four floating-point values, one for each of
R, G, B, and A, in that order. There are no restrictions on the allowable values for
these parameters. A position parameter consists of four floating-point coordinates
(x, y, z, and w) that specify a position in object coordinates (w may be zero,
indicating a point at infinity in the direction given by x, y, and z). A direction
parameter consists of three floating-point coordinates (x, y, and z) that specify a
direction in object coordinates. A real parameter is one floating-point value. The
various values and their types are summarized in Table 2.8. The result of a lighting
computation is undefined if a value for a parameter is specified that is outside the
range given for that parameter in the table.
    There are n light sources, indexed by i = 0, . . . , n−1. (n is an implementation
dependent maximum that must be at least 8.) Note that the default values for dcli
and scli differ for i = 0 and i > 0.
    Before specifying the way that lighting computes colors, we introduce oper-
ators and notation that simplify the expressions involved. If c1 and c2 are col-
ors without alpha where c1 = (r1 , g1 , b1 ) and c2 = (r2 , g2 , b2 ), then define

                          Version 1.1.12 (April 24, 2008)
2.12. COLORS AND COLORING                                                          39




 Parameter      Type         Default Value        Description
 Material Parameters
    acm         color      (0.2, 0.2, 0.2, 1.0)   ambient color of material
    dcm         color      (0.8, 0.8, 0.8, 1.0)   diffuse color of material
    scm         color      (0.0, 0.0, 0.0, 1.0)   specular color of material
    ecm         color      (0.0, 0.0, 0.0, 1.0)   emissive color of material
    srm          real              0.0            specular exponent (range:
                                                  [0.0, 128.0])
 Light Source Parameters
      acli       color     (0.0, 0.0, 0.0, 1.0)   ambient intensity of light i
 dcli (i = 0)    color     (1.0, 1.0, 1.0, 1.0)   diffuse intensity of light 0
 dcli (i > 0)    color     (0.0, 0.0, 0.0, 1.0)   diffuse intensity of light i
 scli (i = 0)    color     (1.0, 1.0, 1.0, 1.0)   specular intensity of light 0
 scli (i > 0)    color     (0.0, 0.0, 0.0, 1.0)   specular intensity of light i
     Ppli      position    (0.0, 0.0, 1.0, 0.0)   position of light i
      sdli     direction    (0.0, 0.0, −1.0)      direction of spotlight for light i
      srli        real             0.0            spotlight exponent for light i
                                                  (range: [0.0, 128.0])
     crli         real           180.0            spotlight cutoff angle for light i
                                                  (range: [0.0, 90.0], 180.0)
     k0i          real             1.0            constant attenuation factor for
                                                  light i (range: [0.0, ∞))
     k1i          real             0.0            linear attenuation factor for
                                                  light i (range: [0.0, ∞))
     k2i          real             0.0            quadratic attenuation factor for
                                                  light i (range: [0.0, ∞))
 Lighting Model Parameters
    acs         color    (0.2, 0.2, 0.2, 1.0)     ambient color of scene
     tbs      boolean          FALSE              use two-sided lighting mode

Table 2.8: Summary of lighting parameters. The range of individual color compo-
nents is (−∞, +∞).




                         Version 1.1.12 (April 24, 2008)
2.12. COLORS AND COLORING                                                               40


c1 ∗ c2 = (r1 r2 , g1 g2 , b1 b2 ). Addition of colors is accomplished by addition of
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
P2 − P1 .
                                             ˆ be the unit vector in d’s direction. Let
    If d is an arbitrary direction, then let d
 P1 P2 be the distance between P1 and P2 . Finally, let V be the point corre-
sponding to the vertex being lit, and n be the corresponding normal.
    Lighting produces a color c. The equation to compute c is


               c = ecm
                   + acm ∗ acs
                       n−1
                   +          (atti )(spoti ) [acm ∗ acli
                                                   −−→
                        i=0             + (n VPpli )dcm ∗ dcli
                                        + (fi )(n h     ˆ i )srm scm ∗ scli ]

    where
                          −−→
                   1, n VPpli = 0,
      fi =                                                                            (2.2)
                   0, otherwise,



           −−→
      hi = VPpli + ( 0             0   1 )T                                           (2.3)



                                  1
               
                                                             2,   if Ppli ’s w = 0,
               
                   k0i + k1i VPpli + k2i VPpli
               
    atti =                                                                            (2.4)
               
               
                                         1.0,                     otherwise.

                          Version 1.1.12 (April 24, 2008)
2.12. COLORS AND COLORING                                                                     41

                −−−→                                     −−−→
                (Ppli V
                             ˆsdli )srli , crli = 180.0, Ppli V   ˆsdli ≥ cos(crli ),
                                                          −−−→
   spoti =                 0.0,             crli = 180.0, Ppli V   ˆsdli < cos(crli ),(2.5)
               
               
                           1.0,             crli = 180.0.
All computations are carried out in eye coordinates. Lighting is computed for a
viewer situated at (0, 0, − ∞); the OpenGL ES lighting model does not support
a local viewer.
    The value of A produced by lighting is the alpha value associated with dcm .
    Results of lighting are undefined if the we coordinate (w in eye coordinates) of
V is zero.
    Lighting may operate in two-sided mode (tbs = TRUE), in which a front color
and a back color are computed using the same material parameters (there is no
way to specify different front and back material parameters in OpenGL ES ), but
replacing n with −n in the case of the back color. If tbs = FALSE, then the back
color and front color are both assigned the color computed using n.
    The selection between back color and front color depends on the primitive of
which the vertex being lit is a part. If the primitive is a point or a line segment,
the front color is always selected. If it is a polygon, then the selection is based on
the sign of the (clipped or unclipped) polygon’s signed area computed in window
coordinates. One way to compute this area is

                                 1 n−1 i i⊕1    i⊕1 i
                            a=        x y    − xw  yw                                (2.6)
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

2.12.2    Lighting Parameter Specification
Lighting parameters are divided into three categories: material parameters, light
source parameters, and lighting model parameters (see Table 2.8). Sets of lighting
parameters are specified with

                               Version 1.1.12 (April 24, 2008)
2.12. COLORS AND COLORING                                                           42


      void    Material{xf}( enum face, enum pname, T param );
      void    Material{xf}v( enum face, enum pname, T params );
      void    Light{xf}( enum light, enum pname, T param );
      void    Light{xf}v( enum light, enum pname, T params );
      void    LightModel{xf}( enum pname, T param );
      void    LightModel{xf}v( enum pname, T params );

pname is a symbolic constant indicating which parameter is to be set (see Ta-
ble 2.9). In the vector versions of the commands, params is a pointer to a group
of values to which to set the indicated parameter. The number of values pointed to
depends on the parameter being set. In the non-vector versions, param is a value
to which to set a single-valued parameter. (If param corresponds to a multi-valued
parameter, the error INVALID ENUM results.) For the Material command, face
must be FRONT AND BACK, indicating that the property name of both the front and
back material, should be set. In the case of Light, light is a symbolic constant of
the form LIGHTi, indicating that light i is to have the specified parameter set. The
constants obey LIGHTi = LIGHT0 + i.
    Table 2.9 gives, for each of the three parameter groups, the correspondence
between the pre-defined constant names and their names in the lighting equa-
tions, along with the number of values that must be specified with each. Color
parameters specified with Material and Light are converted to floating-point val-
ues (if specified as integers) as indicated in Table 2.7 for signed integers. The error
INVALID VALUE occurs if a specified lighting parameter lies outside the allowable
range given in Table 2.8. (The symbol “∞” indicates the maximum representable
magnitude for the indicated type.)
    The current model-view matrix is applied to the position parameter indicated
with Light for a particular light source when that position is specified. These
transformed values are the values used in the lighting equation.
    The spotlight direction is transformed when it is specified using only the upper
leftmost 3x3 portion of the model-view matrix. That is, if Mu is the upper left 3x3
matrix taken from the current model-view matrix M , then the spotlight direction

                                          dx
                                            
                                         dy 
                                          dz

is transformed to
                                 dx         dx
                                                 
                                d  = Mu  dy  .
                                  y
                                 dz         dz



                          Version 1.1.12 (April 24, 2008)
2.12. COLORS AND COLORING                                           43




         Parameter              Name            Number of values
         Material Parameters (Material)
            acm                AMBIENT                4
            dcm                DIFFUSE                4
         acm , dcm      AMBIENT AND DIFFUSE           4
            scm               SPECULAR                4
            ecm               EMISSION                4
            srm               SHININESS               1
         Light Source Parameters (Light)
            acli               AMBIENT                4
            dcli               DIFFUSE                4
            scli              SPECULAR                4
            Ppli              POSITION                4
            sdli          SPOT DIRECTION              3
            srli           SPOT EXPONENT              1
            crli            SPOT CUTOFF               1
             k0        CONSTANT ATTENUATION           1
             k1         LINEAR ATTENUATION            1
             k2       QUADRATIC ATTENUATION           1
         Lighting Model Parameters (LightModel)
            acs         LIGHT MODEL AMBIENT           4
             tbs       LIGHT MODEL TWO SIDE           1


Table 2.9:    Correspondence of lighting parameter symbols to names.
AMBIENT AND DIFFUSE is used to set acm and dcm to the same value.




                       Version 1.1.12 (April 24, 2008)
2.12. COLORS AND COLORING                                                         44


   An individual light is enabled or disabled by calling Enable or Disable with the
symbolic value LIGHTi (i is in the range 0 to n − 1, where n is the implementation-
dependent number of lights). If light i is disabled, the ith term in the lighting
equation is effectively removed from the summation.

2.12.3   Color Material Tracking
It is possible to attach the ambient and diffuse material properties to the current
color, so that they continuously track its component values.
     Color material tracking is enabled and disabled by calling Enable or Disable
with the symbolic value COLOR MATERIAL. When enabled, both the ambient (acm )
and diffuse (dcm ) properties of both the front and back material are immediately
set to the value of the current color, and will track changes to the current color
resulting from either the Color commands or drawing vertex arrays with the color
array enabled.
     The replacements made to material properties are permanent; the replaced val-
ues remain until changed by either sending a new color or by setting a new material
value when COLOR MATERIAL is not currently enabled, to override that particular
value.

2.12.4   Lighting State
The state required for lighting consists of all of the lighting parameters (front and
back material parameters, lighting model parameters, and at least 8 sets of light pa-
rameters), a bit indicating whether a back color distinct from the front color should
be computed, at least 8 bits to indicate which lights are enabled, a bit indicating
whether or not COLOR MATERIAL is enabled, and a single bit to indicate whether
lighting is enabled or disabled. In the initial state, all lighting parameters have
their default values. Back color evaluation does not take place, and both lighting
and COLOR MATERIAL are disabled.

2.12.5   Clamping
After lighting (whether enabled or not), all components of the color are clamped to
the range [0, 1].

2.12.6   Flatshading
A primitive may be flatshaded, meaning that all vertices of the primitive are as-
signed the same color. This color is the color of the vertex that spawned the prim-
itive. For a point, it is the color associated with the point. For a line segment, it

                          Version 1.1.12 (April 24, 2008)
2.12. COLORS AND COLORING                                                                     45


                       Primitive type of triangle i              Vertex
                       triangle strip                            i+2
                       triangle fan                              i+2
                       independent triangle                        3i


Table 2.10: Triangle flatshading color selection. The colors used for flatshading
the ith triangle generated by the indicated primitive mode are derived from the
current color (if lighting is disabled) in effect when the indicated vertex is specified.
If lighting is enabled, the colors are produced by lighting the indicated vertex.
Vertices are numbered 1 through n, where n is the number of vertices specified by
the DrawArrays or DrawElements command.


is the color of the second (final) vertex of the segment. For a triangle, it comes
from a selected vertex depending on how the triangle was generated. Table 2.10
summarizes the possibilities.
     Flatshading is controlled by

       void ShadeModel( enum mode );

mode value must be either of the symbolic constants SMOOTH or FLAT. If mode is
SMOOTH (the initial state), vertex colors are treated individually. If mode is FLAT,
flatshading is turned on. ShadeModel thus requires one bit of state.

2.12.7     Color and Texture Coordinate Clipping
After lighting, clamping, and possible flatshading, colors are clipped. The color
associated with a vertex that lies within the clip volume is unaffected by clipping. If
a primitive is clipped, however, the colors assigned to vertices produced by clipping
are clipped colors.
    Let the colors assigned to the two vertices P1 and P2 of an unclipped edge be
c1 and c2 . The value of t (section 2.11) for a clipped point P is used to obtain the
color associated with P as4

                                    c = tc1 + (1 − t)c2 .
(Multiplying a color by a scalar means multiplying each of R, G, B, and A by
the scalar.) Polygon clipping may create a clipped vertex along an edge of the
   4
     Since this computation is performed in clip space before division by wc , clipped colors and
texture coordinates are perspective-correct.



                             Version 1.1.12 (April 24, 2008)
2.12. COLORS AND COLORING                                                          46


clip volume’s boundary. This situation is handled by noting that polygon clipping
proceeds by clipping against one plane of the clip volume’s boundary at a time.
Color clipping is done in the same way, so that clipped points always occur at the
intersection of polygon edges (possibly already clipped) with the clip volume’s
boundary.
    Texture coordinates must also be clipped when a primitive is clipped. The
method is exactly analogous to that used for color clipping.

2.12.8    Final Color Processing
Each color component (which lies in [0, 1]) is converted (by rounding to nearest)
to a fixed-point value with m bits. We assume that the fixed-point representation
used represents each value k/(2m − 1), where k ∈ {0, 1, . . . , 2m − 1}, as k (e.g.
1.0 is represented in binary as a string of all ones). m must be at least as large as
the number of bits in the corresponding component of the framebuffer. m must be
at least 2 for A if the framebuffer does not contain an A component, or if there is
only 1 bit of A in the framebuffer.
     Because a number of the form k/(2m − 1) may not be represented exactly as
a limited-precision floating-point quantity, we place a further requirement on the
fixed-point conversion of color components. Suppose that lighting is disabled, the
color associated with a vertex has not been clipped, and the color was specified with
unsigned byte or integer values. When these conditions are satisfied, an RGBA
component must convert to a value that matches the component as specified in
the command defining it: if m is less than the number of bits b with which the
component was specified, then the converted value must equal the most significant
m bits of the specified value; otherwise, the most significant b bits of the converted
value must equal the specified value.




                          Version 1.1.12 (April 24, 2008)
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
     A grid square along with its parameters of assigned colors, z (depth), and tex-
ture coordinates is called a fragment; the parameters are collectively dubbed the
fragment’s associated data. A fragment is located by its lower left corner, which
lies on integer grid coordinates. Rasterization operations also refer to a fragment’s
center, which is offset by (1/2, 1/2) from its lower left corner (and so lies on
half-integer coordinates).
     Grid squares need not actually be square in the GL. Rasterization rules are not
affected by the actual aspect ratio of the grid squares. Display of non-square grids,
however, will cause rasterized points and line segments to appear fatter in one
direction than the other. We assume that fragments are square, since it simplifies
antialiasing and texturing.
     Several factors affect rasterization. Points may be given differing diameters
and line segments differing widths. A point or line segment may be antialiased
using pixel coverage values (see section 3.2), but polygon antialiasing using cov-
erage values is not supported. Multisampling must be used to rasterize antialiased
polygons (see section 3.2.1).




                                         47
3.1. INVARIANCE                                                                    48




                                    Point
                                Rasterization




              From
                                    Line
            Primitive                                 Texturing
                                Rasterization
            Assembly




                                  Triangle
                                                        Fog        Fragments
                                Rasterization




   Figure 3.1. Rasterization.




3.1    Invariance
Consider a primitive p obtained by translating a primitive p through an offset (x, y)
in window coordinates, where x and y are integers. As long as neither p nor p is
clipped, it must be the case that each fragment f produced from p is identical to
a corresponding fragment f from p except that the center of f is offset by (x, y)
from the center of f .


3.2    Antialiasing
Antialiasing of a point or line is effected as follows: the R, G, and B values of the
rasterized fragment are left unaffected, but the A value is multiplied by a floating-
point value in the range [0, 1] that describes a fragment’s screen pixel coverage. The
per-fragment stage of the GL can be set up to use the A value to blend the incoming
fragment with the corresponding pixel already present in the framebuffer.
    The details of how antialiased fragment coverage values are computed are dif-
ficult to specify in general. The reason is that high-quality antialiasing may take
into account perceptual issues as well as characteristics of the monitor on which
the contents of the framebuffer are displayed. Such details cannot be addressed
within the scope of this document. Further, the coverage value computed for a
fragment of some primitive may depend on the primitive’s relationship to a num-


                           Version 1.1.12 (April 24, 2008)
3.2. ANTIALIASING                                                                 49


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
by providing GL hints (section 5.2), allowing a user to make an image quality
versus speed tradeoff.

3.2.1   Multisampling
Multisampling is a mechanism to antialias all GL primitives: points, lines, and tri-
angles. The technique is to sample all primitives multiple times at each pixel. The
color sample values are resolved to a single, displayable color each time a pixel
is updated, so the antialiasing appears to be automatic at the application level.
Because each sample includes color, depth, and stencil information, the color (in-
cluding texture operation), depth, and stencil functions perform equivalently to the
single-sample mode.

                          Version 1.1.12 (April 24, 2008)
3.2. ANTIALIASING                                                                   50


    An additional buffer, called the multisample buffer, is added to the framebuffer.
Pixel sample values, including color, depth, and stencil values, are stored in this
buffer. When the framebuffer includes a multisample buffer, it does not include
depth or stencil buffers, even if the multisample buffer does not store depth or
stencil values. The color buffer coexists with the multisample buffer, however.
    Multisample antialiasing is most valuable for rendering triangles, because it re-
quires no sorting for hidden surface elimination, and it correctly handles adjacent
triangles, object silhouettes, and even intersecting triangles. If only points or lines
are being rendered, the “smooth” antialiasing mechanism provided by the base GL
may result in a higher quality image. This mechanism is designed to allow multi-
sample and smooth antialiasing techniques to be alternated during the rendering of
a single scene.
    If the value of SAMPLE BUFFERS is one, the rasterization of all primi-
tives is changed, and is referred to as multisample rasterization. Otherwise,
primitive rasterization is referred to as single-sample rasterization. The value
of SAMPLE BUFFERS is queried by calling GetIntegerv with pname set to
SAMPLE BUFFERS.
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

                          Version 1.1.12 (April 24, 2008)
3.3. POINTS                                                                       51


    If MULTISAMPLE is enabled, multisample rasterization of all primitives differs
substantially from single-sample rasterization. It is understood that each pixel in
the framebuffer has SAMPLES locations associated with it. These locations are
exact positions, rather than regions or areas, and each is referred to as a sample
point. The sample points associated with a pixel may be located inside or outside
of the unit square that is considered to bound the pixel. Furthermore, the relative
locations of sample points may be identical for each pixel in the framebuffer, or
they may differ.
    If the sample locations differ per pixel, they should be aligned to window, not
screen, boundaries. Otherwise rendering results will be window-position specific.
The invariance requirement described in section 3.1 is relaxed for all multisample
rasterization, because the sample locations may be a function of pixel location.
    It is not possible to query the actual sample locations of a pixel.


3.3    Points
The rasterization of points is controlled with

      void PointSize( float size );
      void PointSizex( fixed size );

size specifies the requested size of a point. The default value is 1.0. A value less
than or equal to zero results in the error INVALID VALUE.
    The requested point size is multiplied with a distance attenuation factor,
clamped to a point size range specified with PointParameter (see below), and
further clamped to the implementation-dependent point size range to produce the
derived point size:

                                                             size
      derived size = impl clamp user clamp √
                                                        a + b ∗ d + c ∗ d2
where d is the eye-coordinate distance from the eye, (0, 0, 0, 1) in eye coordinates,
to the vertex, and a, b, and c are distance attenuation function coefficients.
     Point sprites are enabled or disabled by calling Enable or Disable with the
symbolic constant POINT SPRITE OES. The default state is for point sprites to be
disabled. When point sprites are enabled, the state of the point antialiasing enable
is ignored.
     The point sprite texture coordinate replacement mode is set with the commands

      void TexEnv{ixf}( enum target, enum pname, T param );

                          Version 1.1.12 (April 24, 2008)
3.3. POINTS                                                                         52


        void TexEnv{ixf}v( enum target, enum pname, T params );

where target is POINT SPRITE OES and pname is COORD REPLACE OES. The pos-
sible values for param are FALSE and TRUE. The default value for each texture unit
is for point sprite texture coordinate replacement to be disabled.
     If multisampling is not enabled, the derived size is passed on to rasterization as
the point width.
     If multisampling is enabled, an implementation may optionally fade the point
alpha (see section 3.10) instead of allowing the point width to go below a given
threshold. In this case, the width of the rasterized point is

                          derived size derived size ≥ threshold
            width =                                                              (3.1)
                          threshold    otherwise
and the fade factor is computed as follows:
                      
                       1                      derived size ≥ threshold
            f ade =         derived size
                                           2                                     (3.2)
                      
                             threshold         otherwise
    The distance attenuation function coefficients a, b, and c, the bounds of the first
point size range clamp, and the point fade threshold, are specified with

        void PointParameter{xf}( enum pname, T param );
        void PointParameter{xf}v( enum pname, const T params );

     If pname is POINT SIZE MIN or POINT SIZE MAX, then param speci-
fies, or params points to the lower or upper bound respectively to which
the derived point size is clamped.           If the lower bound is greater than
the upper bound, the point size after clamping is undefined. If pname is
POINT DISTANCE ATTENUATION, then params points to the coefficients a, b,
and c. If pname is POINT FADE THRESHOLD SIZE, then param specifies,
or params points to the point fade threshold. Values of POINT SIZE MIN,
POINT SIZE MAX, or POINT FADE THRESHOLD SIZE less than zero result in the
error INVALID VALUE.
     Point antialiasing is enabled or disabled by calling Enable or Disable with the
symbolic constant POINT SMOOTH. The default state is for point antialiasing to be
disabled.

3.3.1    Basic Point Rasterization
In the default state, a point is rasterized by truncating its xw and yw coordinates
(recall that the subscripts indicate that these are x and y window coordinates) to

                            Version 1.1.12 (April 24, 2008)
3.3. POINTS                                                                         53


integers. This (x, y) address, along with data derived from the data associated
with the vertex corresponding to the point, is sent as a single fragment to the per-
fragment stage of the GL.
     The effect of a point width other than 1.0 depends on the state of point an-
tialiasing and point sprites.

    Non-Antialiased Points

     If antialiasing and point sprites are disabled, the actual width is deter-
mined by rounding the supplied width to the nearest integer, then clamp-
ing it to the implementation-dependent maximum non-antialiased point width.
This implementation-dependent value must be no less than the implementation-
dependent maximum antialiased point width, rounded to the nearest integer value,
and in any event no less than 1. If rounding the specified width results in the value
0, then it is as if the value were 1. If the resulting width is odd, then the point
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
    All fragments produced in rasterizing a non-antialiased point are assigned the
same associated data, which are those of the vertex corresponding to the point, with
texture coordinates s, t, and r replaced with s/q, t/q, and r/q, respectively. If q is
less than or equal to zero, the results are undefined.

    Antialiased Points

    If antialiasing is enabled and point sprites are disabled, then point rasterization
produces a fragment for each fragment square that intersects the region lying within
the circle having diameter equal to the current point width and centered at the
point’s (xw , yw ) (figure 3.3). The coverage value for each fragment is the window
coordinate area of the intersection of the circular region with the corresponding
fragment square (but see section 3.2). This value is saved and used in the final
step of rasterization (section 3.9). Other associated data for each fragment are
determined in the same fashion as for non-antialiased points.

                          Version 1.1.12 (April 24, 2008)
3.3. POINTS                                                                                          54




                                                  5.5

                                                  4.5
                                




                                




                                                  3.5                ¡    ¡    ¡




                                                                     ¡    ¡    ¡




                                                  2.5

                                                  1.5

                                                  0.5

        0.5   1.5   2.5       3.5     4.5   5.5          0.5   1.5       2.5       3.5   4.5   5.5

               Odd Width                                        Even Width


   Figure 3.2. Rasterization of non-antialiased wide points. The crosses show fragment
   centers produced by rasterization for any point that lies within the shaded region.
   The dotted grid lines lie on half-integer coordinates.




    Not all widths need be supported when point antialiasing is on, but the width
1.0 must be provided. If an unsupported width is requested, the nearest supported
width is used instead. The range of supported widths and the width of evenly-
spaced gradations within that range are implementation dependent. The range and
gradations may be obtained using the query mechanism described in Chapter 6. If,
for instance, the width range is from 0.1 to 2.0 and the gradation width is 0.1, then
the widths 0.1, 0.2, . . . , 1.9, 2.0 are supported.

    Point Sprites

     When point sprites are enabled, then point rasterization produces a fragment
for each framebuffer pixel whose center lies inside a square centered at the point’s
(xw , yw ), with side length equal to the current point size.
     Associated data for each fragment are determined in the same fash-
ion as for non-antialiased points. However, for each texture unit where
COORD REPLACE OES is TRUE, texture coordinates are replaced with point sprite
texture coordinates. The s coordinate varies from 0 to 1 across the point horizon-
tally left-to-right, while the t coordinate varies from 0 to 1 vertically top-to-bottom.
The r and q coordinates are replaced with the constants 0 and 1, respectively.

                                    Version 1.1.12 (April 24, 2008)
3.3. POINTS                                                                                                        55




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




                             Version 1.1.12 (April 24, 2008)
3.3. POINTS                                                                         56


    The following formula is used to evaluate the s and t coordinates:

                                    1 xf + 21 − xw
                               s=     +
                                    2     size
                                    1 yf + 21 − yw
                               t=     −
                                    2       size
    where size is the point’s size, xf and yf are the (integral) window coordinates
of the fragment, and xw and yw are the exact, unrounded window coordinates of
the vertex for the point.
    The widths supported for point sprites must be a superset of those supported
for antialiased points. There is no requirement that these widths must be equally
spaced. If an unsupported width is requested, the nearest supported width is used
instead.

3.3.2   Point Rasterization State
The state required to control point rasterization consists of one floating-point value
specifying the point width, three floating-point values specifying the minimum and
maximum point size and the point fade threshold size, three floating-point values
specifying the distance attenuation coefficients, a bit indicating whether or not an-
tialiasing is enabled, a a bit indicating whether or not point sprites are enabled, and
a bit for the point sprite texture coordinate replacement mode for each texture unit.

3.3.3   Point Multisample Rasterization
If MULTISAMPLE is enabled, and the value of SAMPLE BUFFERS is one, then points
are rasterized using the following algorithm, regardless of whether point antialias-
ing (POINT SMOOTH) is enabled or disabled. Point rasterization produces a frag-
ment for each framebuffer pixel with one or more sample points that intersect a
region centered at the point’s (xw , yw ). This region is a circle having diameter
equal to the current point width if POINT SPRITE OES is disabled, or a square with
side equal to the current point width if POINT SPRITE OES is enabled. Coverage
bits that correspond to sample points that intersect the region are 1, other coverage
bits are 0. All data associated with each sample for the fragment are the data as-
sociated with the point being rasterized, with the exception of texture coordinates
when POINT SPRITE OES is enabled; these texture coordinates are computed as
described in section 3.3.
    Point size range and number of gradations are equivalent to those supported
for antialiased points when POINT SPRITE OES is disabled. The set of point



                          Version 1.1.12 (April 24, 2008)
3.4. LINE SEGMENTS                                                                   57


sizes supported is equivalent to those for point sprites without multisample when
POINT SPRITE OES is enabled.


3.4     Line Segments
A line segment results from a line strip, a line loop, or a series of separate line
segments. Line segment rasterization is controlled by several variables. Line width,
which may be set by calling

        void LineWidth( float width );
        void LineWidthx( fixed width );

with an appropriate positive width, controls the width of rasterized line segments.
The default width is 1.0. Values less than or equal to 0.0 generate the error
INVALID VALUE. Antialiasing is controlled with Enable and Disable using the
symbolic constant LINE SMOOTH.

3.4.1    Basic Line Segment Rasterization
Line segment rasterization begins by characterizing the segment as either x-major
or y-major. x-major line segments have slope in the closed interval [−1, 1]; all
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


                           Version 1.1.12 (April 24, 2008)
3.4. LINE SEGMENTS                                                                                                          58


                        ©   ©   ©   ©      ©                                          $      $   $   $   $




                        ©   ©   ©   ©      ©                                          $      $   $   $   $




                        ©   ©   ©   ©      ©                                          $      $   $   $   $




                        ©   ©   ©   ©      ©                                          $      $   $   $   $




                        ¨   ¨   ¨   ¨      ¨                                          #      #   #   #   #




                        ¨   ¨   ¨   ¨      ¨                                          #      #   #   #   #




                        ¨   ¨   ¨   ¨      ¨                                          #      #   #   #   #




                        ¨   ¨   ¨   ¨      ¨                                          #      #   #   #   #




                        §   §   §   §      §            ¡      ¡   ¡   ¡      ¡            "      "   "   "   "




                        §   §   §   §      §            ¡      ¡   ¡   ¡      ¡            "      "   "   "   "




                        §   §   §   §      §            ¡      ¡   ¡   ¡      ¡            "      "   "   "   "




                        §   §   §   §      §            ¡      ¡   ¡   ¡      ¡            "      "   "   "   "




                        ¦   ¦   ¦   ¦       ¦               ¢       ¢   ¢   ¢      ¢            !      !   !   !   !




                        ¦   ¦   ¦   ¦       ¦               ¢       ¢   ¢   ¢      ¢            !      !   !   !   !




                        ¦   ¦   ¦   ¦       ¦               ¢       ¢   ¢   ¢      ¢            !      !   !   !   !




                        ¦   ¦   ¦   ¦       ¦               ¢       ¢   ¢   ¢      ¢            !      !   !   !   !




                        ¥   ¥   ¥   ¥   ¤   ¥   ¤   ¤   ¤   £   ¤   £   £   £      £                




                        ¥   ¥   ¥   ¥   ¤   ¥   ¤   ¤   ¤   £   ¤   £   £   £      £                




                        ¥   ¥   ¥   ¥   ¤   ¥   ¤   ¤   ¤   £   ¤   £   £   £      £                




                        ¥   ¥   ¥   ¥   ¤   ¥   ¤   ¤   ¤   £   ¤   £   £   £      £                




   Figure 3.4. Visualization of Bresenham’s algorithm. A portion of a line segment is
   shown. A diamond shaped region of height 1 is placed around each fragment center;
   those regions that the line segment exits cause rasterization to produce correspond-
   ing fragments.




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


                                Version 1.1.12 (April 24, 2008)
3.4. LINE SEGMENTS                                                                   59


      window-coordinate column (for a y-major line, no two fragments may ap-
      pear in the same row).

   4. If two line segments share a common endpoint, and both segments are either
      x-major (both left-to-right or both right-to-left) or y-major (both bottom-to-
      top or both top-to-bottom), then rasterizing both segments may not produce
      duplicate fragments, nor may any fragments be omitted so as to interrupt
      continuity of the connected segments.

    Next we must specify how the data associated with each rasterized fragment
are obtained. Let the window coordinates of a produced fragment center be given
by pr = (xd , yd ) and let pa = (xa , ya ) and pb = (xb , yb ). Set

                                  (pr − pa ) · (pb − pa )
                             t=                           .                       (3.3)
                                        pb − pa 2
(Note that t = 0 at pa and t = 1 at pb .) The value of an associated datum f for the
fragment, whether it be an R, G, B, or A color component or the s, t, or r texture
coordinate (the depth value, window z, must be found using equation 3.5, below),
is found as

                                  (1 − t)fa /wa + tfb /wb
                           f=                                                     (3.4)
                                  (1 − t)αa /wa + tαb /wb
where fa and fb are the data associated with the starting and ending endpoints of
the segment, respectively; wa and wb are the clip w coordinates of the starting
and ending endpoints of the segments, respectively. αa = αb = 1 for all data
except texture coordinates, in which case αa = qa and αb = qb (qa and qb are
the homogeneous texture coordinates at the starting and ending endpoints of the
segment; results are undefined if either of these is less than or equal to 0). Note
that linear interpolation would use

                            f = (1 − t)fa /αa + tfb /αb .                         (3.5)

The reason that this formula is incorrect (except for the depth value) is that it inter-
polates a datum in window space, which may be distorted by perspective. What is
actually desired is to find the corresponding value when interpolated in clip space,
which equation 3.4 does. A GL implementation may choose to approximate equa-
tion 3.4 with 3.5, but this will normally lead to unacceptable distortion effects when
interpolating texture coordinates.




                           Version 1.1.12 (April 24, 2008)
3.4. LINE SEGMENTS                                                                       60




                     width = 2                              width = 3




   Figure 3.5. Rasterization of non-antialiased wide lines. x-major line segments are
   shown. The heavy line segment is the one specified to be rasterized; the light seg-
   ment is the offset segment used for rasterization. x marks indicate the fragment
   centers produced by rasterization.




3.4.2   Other Line Segment Features
We have just described the rasterization of non-antialiased line segments of width
one. We now describe the rasterization of line segments for general values of the
line segment rasterization parameters.

Wide Lines
The actual width of non-antialiased lines is determined by rounding the supplied
width to the nearest integer, then clamping it to the implementation-dependent
maximum non-antialiased line width. This implementation-dependent value must
be no less than the implementation-dependent maximum antialiased line width,
rounded to the nearest integer value, and in any event no less than 1. If rounding
the specified width results in the value 0, then it is as if the value were 1.
     Non-antialiased line segments of width other than one are rasterized by off-
setting them in the minor direction (for an x-major line, the minor direction is
y, and for a y-major line, the minor direction is x) and replicating fragments in
the minor direction (see figure 3.5). Let w be the width rounded to the nearest
integer (if w = 0, then it is as if w = 1). If the line segment has endpoints


                            Version 1.1.12 (April 24, 2008)
3.4. LINE SEGMENTS                                                                                        61




                                                                                                       




                                                                                                       




                                                                                                       




                                                                                                       




                                                                                                       




                                                                                                       




                                                                                                       




                                                                                                       




                                                                                                       




                                                                                                       




                                                                                                       




                                                                                                       




                                                                                                       




                                                                                                       




   Figure 3.6. The region used in rasterizing and finding corresponding coverage val-
   ues for an antialiased line segment (an x-major line segment is shown).




given by (x0 , y0 ) and (x1 , y1 ) in window coordinates, the segment with endpoints
(x0 , y0 − (w − 1)/2) and (x1 , y1 − (w − 1)/2) is rasterized, but instead of a single
fragment, a column of fragments of height w (a row of fragments of length w for
a y-major segment) is produced at each x (y for y-major) location. The lowest
fragment of this column is the fragment that would be produced by rasterizing the
segment of width 1 with the modified coordinates.

Antialiasing
Rasterized antialiased line segments produce fragments whose fragment squares
intersect a rectangle centered on the line segment. Two of the edges are parallel to
the specified line segment; each is at a distance of one-half the current width from
that segment: one above the segment and one below it. The other two edges pass
through the line endpoints and are perpendicular to the direction of the specified
line segment. Coverage values are computed for each fragment by computing the
area of the intersection of the rectangle with the fragment square (see figure 3.6;
see also section 3.2). Equation 3.4 is used to compute associated data values just as
with non-antialiased lines; equation 3.3 is used to find the value of t for each frag-
ment whose square is intersected by the line segment’s rectangle. Not all widths
need be supported for line segment antialiasing, but width 1.0 antialiased segments
must be provided. As with the point width, a GL implementation may be queried
for the range and number of gradations of available antialiased line widths.


                              Version 1.1.12 (April 24, 2008)
3.5. POLYGONS                                                                       62


3.4.3    Line Rasterization State
The state required for line rasterization consists of the floating-point line width and
a bit indicating whether line antialiasing is on or off. The initial value of the line
width is 1.0 and the initial state of line segment antialiasing is disabled.

3.4.4    Line Multisample Rasterization
If MULTISAMPLE is enabled, and the value of SAMPLE BUFFERS is one, then lines
are rasterized using the following algorithm, regardless of whether line antialiasing
(LINE SMOOTH) is enabled or disabled. Line rasterization produces a fragment for
each framebuffer pixel with one or more sample points that intersect the rectangular
region that is described in the Antialiasing portion of section 3.4.2 (Other Line
Segment Features).
    Coverage bits that correspond to sample points that intersect a retained rectan-
gle are 1, other coverage bits are 0. Each color, depth, and set of texture coordinates
is produced by substituting the corresponding sample location into equation 3.3,
then using the result to evaluate equation 3.4. An implementation may choose to
assign the same color value and the same set of texture coordinates to more than
one sample. The color value and the set of texture coordinates need not be evalu-
ated at the same location.
    Line width range and number of gradations are equivalent to those supported
for antialiased lines.


3.5     Polygons
A polygon results from a triangle strip, triangle fan, or series of separate trian-
gles. Like points and line segments, polygon rasterization is controlled by several
variables.

3.5.1    Basic Polygon Rasterization
The first step of polygon rasterization is to determine if the polygon is back facing
or front facing. This determination is made by examining the sign of the area com-
puted by equation 2.6 of section 2.12.1 (including the possible reversal of this sign
as indicated by the last call to FrontFace). If this sign is positive, the polygon is
front facing; otherwise, it is back facing. This determination is used in conjunction
with the CullFace enable bit and mode value to decide whether or not a particular
polygon is rasterized. The CullFace mode is set by calling

        void CullFace( enum mode );

                          Version 1.1.12 (April 24, 2008)
3.5. POLYGONS                                                                          63


mode is a symbolic constant: one of FRONT, BACK or FRONT AND BACK. Culling
is enabled or disabled with Enable or Disable using the symbolic constant
CULL FACE. Front facing polygons are rasterized if either culling is disabled or
the CullFace mode is BACK while back facing polygons are rasterized only if ei-
ther culling is disabled or the CullFace mode is FRONT. The initial setting of the
CullFace mode is BACK. Initially, culling is disabled.
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
                          f=                                                       (3.6)
                                aαa /wa + bαb /wb + cαc /wc
where wa , wb and wc are the clip w coordinates of pa , pb , and pc , respectively.
a, b, and c are the barycentric coordinates of the fragment for which the data are
produced. αa = αb = αc = 1 except for texture s, t, and r coordinates, for which
αa = qa , αb = qb , and αc = qc (if any of qa , qb , or qc are less than or equal
to zero, results are undefined). a, b, and c must correspond precisely to the exact
coordinates of the center of the fragment. Another way of saying this is that the
data associated with a fragment must be sampled at the fragment’s center.

                            Version 1.1.12 (April 24, 2008)
3.5. POLYGONS                                                                     64


    Just as with line segment rasterization, equation 3.6 may be approximated by

                         f = afa /αa + bfb /αb + cfc /αc ;

this may yield acceptable results for color values (it must be used for depth val-
ues), but will normally lead to unacceptable distortion effects if used for texture
coordinates.

3.5.2    Depth Offset
The depth values of all fragments generated by the rasterization of a polygon may
be offset by a single value that is computed for that polygon. The function that
determines this value is specified by calling

        void PolygonOffset( float factor, float units );
        void PolygonOffsetx( fixed factor, fixed units );

factor scales the maximum depth slope of the polygon, and units scales an im-
plementation dependent constant that relates to the usable resolution of the depth
buffer. The resulting values are summed to produce the polygon offset value. Both
factor and units may be either positive or negative.
    The maximum depth slope m of a triangle is

                                           2             2
                                     ∂zw           ∂zw
                           m=                  +                                (3.7)
                                     ∂xw           ∂yw

where (xw , yw , zw ) is a point on the triangle. m may be approximated as

                                         ∂zw   ∂zw
                           m = max           ,           .                      (3.8)
                                         ∂xw   ∂yw
    The minimum resolvable difference r is an implementation-dependent con-
stant. It is the smallest difference in window coordinate z values that is guaranteed
to remain distinct throughout polygon rasterization and in the depth buffer. All
pairs of fragments generated by the rasterization of two polygons with otherwise
identical vertices, but zw values that differ by r, will have distinct depth values.
    The offset value o for a polygon is

                           o = m ∗ f actor + r ∗ units.                         (3.9)

m is computed as described above, as a function of depth values in the range [0,1],
and o is applied to depth values in the same range.

                          Version 1.1.12 (April 24, 2008)
3.6. PIXEL RECTANGLES                                                             65


    Boolean state value POLYGON OFFSET FILL determines whether o is applied
during the rasterization of polygons. This boolean state value is enabled and dis-
abled using the commands Enable and Disable. If POLYGON OFFSET FILL is en-
abled, o is added to the depth value of each fragment produced by the rasterization
of a polygon.
    Fragment depth values are always limited to the range [0,1], either by clamping
after offset addition is performed (preferred), or by clamping the vertex values used
in the rasterization of the polygon.

3.5.3   Polygon Multisample Rasterization
If MULTISAMPLE is enabled and the value of SAMPLE BUFFERS is one, then poly-
gons are rasterized using the following algorithm. Polygon rasterization produces
a fragment for each framebuffer pixel with one or more sample points that satisfy
the point sampling criteria described in section 3.5.1, including the special treat-
ment for sample points that lie on a polygon boundary edge. If a polygon is culled,
based on its orientation and the CullFace mode, then no fragments are produced
during rasterization.
    Coverage bits that correspond to sample points that satisfy the point sampling
criteria are 1, other coverage bits are 0. Each color, depth, and set of texture co-
ordinates is produced by substituting the corresponding sample location into the
barycentric equations described in section 3.5.1, using equation 3.6 or its approx-
imation that omits w components. An implementation may choose to assign the
same color value and the same set of texture coordinates to more than one sample
by barycentric evaluation using any location within the pixel including the frag-
ment center or one of the sample locations. The color value and the set of texture
coordinates need not be evaluated at the same location.

3.5.4   Polygon Rasterization State
The state required for polygon rasterization consists of the factor and bias values
of the polygon offset equation. The initial polygon offset factor and bias values are
both 0; initially polygon offset is disabled.


3.6     Pixel Rectangles
Rectangles of color values may be specified to the GL using TexImage2D and
related commands described in section 3.7.1. Some of the parameters and opera-
tions governing the operation of TexImage2D are shared by ReadPixels (used to
obtain pixel values from the framebuffer); the discussion of ReadPixels, however,

                          Version 1.1.12 (April 24, 2008)
3.6. PIXEL RECTANGLES                                                             66


           Parameter Name           Type     Initial Value   Valid Range
           UNPACK ALIGNMENT        integer         4           1,2,4,8

Table 3.1: PixelStore parameters pertaining to one or more of TexImage2D, and
TexSubImage2D.



is deferred until section 4.3, after the framebuffer has been discussed in detail.
Nevertheless, we note in this section when parameters and state pertaining to Tex-
Image2D also pertain to ReadPixels.
    This section describes only how these rectangles are defined in client memory,
and the steps involved in transferring pixel rectangles from client memory to the
GL or vice-versa.
    Parameters controlling the encoding of pixels in client memory (for reading
and writing) are set with the command PixelStorei.

3.6.1    Pixel Storage Modes
Pixel storage modes affect the operation of TexImage2D and ReadPixels (as well
as other commands; see section 3.7) when one of these commands is issued. Pixel
storage modes are set with the command

        void PixelStorei( enum pname, T param );

pname is a symbolic constant indicating a parameter to be set, and param is the
value to set it to. Table 3.1 summarizes the pixel storage parameters, their types,
their initial values, and their allowable ranges. Setting a parameter to a value out-
side the given range results in the error INVALID VALUE.

3.6.2    Transfer of Pixel Rectangles
The process of transferring pixels encoded in host memory to the GL is dia-
grammed in figure 3.7. We describe the stages of this process in the order in which
they occur.
    Commands accepting or returning pixel rectangles take the following argu-
ments (as well as additional arguments specific to their function):
    format is a symbolic constant indicating what the values in memory represent.
    width and height are the width and height, respectively, of the pixel rectangle
to be drawn.



                          Version 1.1.12 (April 24, 2008)
3.6. PIXEL RECTANGLES                                                          67




          byte, short, or packed
      pixel component data stream


                                Unpack



                                               Pixel Storage
                            Convert to Float
                                                Operations

                           Convert L to RGB




                             Clamp to [0,1]
                                                 Final
                                               Conversion
                RGBA pixel data out




  Figure 3.7. Transfer of pixel rectangles to the GL. Output is RGBA pixels.




                           Version 1.1.12 (April 24, 2008)
3.6. PIXEL RECTANGLES                                                            68


          type Parameter                 Corresponding          Special
          Token Name                     GL Data Type        Interpretation
          UNSIGNED    BYTE                  ubyte                 No
          UNSIGNED    SHORT 5 6 5          ushort                 Yes
          UNSIGNED    SHORT 4 4 4 4        ushort                 Yes
          UNSIGNED    SHORT 5 5 5 1        ushort                 Yes

Table 3.2: TexImage2D and ReadPixels type parameter values and the corre-
sponding GL data types. Refer to table 2.2 for definitions of GL data types. Special
interpretations are described near the end of section 3.6.2. ReadPixels accepts only
a subset of these types (see section 4.3.1).


       Format Name             Element Meaning and Order        Target Buffer
       ALPHA                               A                       Color
       RGB                              R, G, B                    Color
       RGBA                            R, G, B, A                  Color
       LUMINANCE                      Luminance                    Color
       LUMINANCE ALPHA               Luminance, A                  Color

Table 3.3: TexImage2D and ReadPixels formats. The second column gives a de-
scription of and the number and order of elements in a group. ReadPixels accepts
only a subset of these formats (see section 4.3.1).



    data is a pointer to the data to be drawn. These data are represented with one
of two GL data types, specified by type. The correspondence between the four type
token values and the GL data types they indicate is given in table 3.2.

Unpacking
Data are taken from host memory as a sequence of unsigned bytes or unsigned
shorts (GL data types ubyte and ushort). These elements are grouped into
sets of one, two, three, or four values, depending on the format, to form a group.
Table 3.3 summarizes the format of groups obtained from memory.
    The values of each GL data type are interpreted as they would be specified in
the language of the client’s GL binding.
    Not all combinations of format and type are valid. The combinations accepted
by the GL are defined in table 3.4. Additional restrictions may be imposed by
specific commands.


                           Version 1.1.12 (April 24, 2008)
3.6. PIXEL RECTANGLES                                                                  69


       Format                    Type                            Bytes per Pixel
       RGBA                      UNSIGNED    BYTE                       4
       RGB                       UNSIGNED    BYTE                       3
       RGBA                      UNSIGNED    SHORT 4 4 4 4              2
       RGBA                      UNSIGNED    SHORT 5 5 5 1              2
       RGB                       UNSIGNED    SHORT 5 6 5                2
       LUMINANCE ALPHA           UNSIGNED    BYTE                       2
       LUMINANCE                 UNSIGNED    BYTE                       1
       ALPHA                     UNSIGNED    BYTE                       1

                Table 3.4: Valid pixel format and type combinations.



     The groups in memory are treated as being arranged in a rectangle. This rect-
angle consists of a series of rows, with the first element of the first group of the first
row pointed to by the data pointer passed to TexImage2D. The number of groups
in a row is width; If p indicates the location in memory of the first element of the
first row, then the first element of the N th row is indicated by

                                        p + Nk                                     (3.10)
    where N is the row number (counting from zero) and k is defined as

                                    nl              s ≥ a,
                            k=                                                     (3.11)
                                    a/s snl/a       s<a
    where n is the number of elements in a group, l is the number of groups in
the row, a is the value of UNPACK ALIGNMENT, and s is the size, in units of GL
ubytes, of an element. If the number of bits per element is not 1, 2, 4, or 8 times
the number of bits in a GL ubyte, then k = nl for all values of a.
    A type of UNSIGNED SHORT 5 6 5, UNSIGNED SHORT 4 4 4 4, or
UNSIGNED SHORT 5 5 5 1 is a special case in which all the components of
each group are packed into a single unsigned short. The number of components
per packed pixel is fixed by the type, and must match the number of components
per group indicated by the format parameter, as listed in table 3.5. The error
INVALID OPERATION is generated if a mismatch occurs. This constraint also
holds for all other functions that accept or return pixel data using type and format
parameters to define the type and format of that data.
    Bitfield locations of the first, second, third, and fourth components of each
packed pixel type are illustrated in table 3.6. Each bitfield is interpreted as an un-


                           Version 1.1.12 (April 24, 2008)
3.6. PIXEL RECTANGLES                                                                                               70


        type Parameter                               GL Data             Number of           Matching
        Token Name                                    Type              Components         Pixel Formats
        UNSIGNED SHORT 5 6 5                         ushort                 3                     RGB
        UNSIGNED SHORT 4 4 4 4                       ushort                 4                    RGBA
        UNSIGNED SHORT 5 5 5 1                       ushort                 4                    RGBA

                                    Table 3.5: Packed pixel formats.



signed integer value. If the base GL type is supported with more than the minimum
precision (e.g. a 9-bit byte) the packed components are right-justified in the pixel.
    Components are packed with the first component in the most significant bits
of the bitfield, and successive component occupying progressively less significant
locations. The most significant bit of each component is packed in the most signif-
icant bit location of its location in the bitfield.
UNSIGNED SHORT 5 6 5:
   15     14       13     12   11     10         9   8          7   6          5   4   3     2            1   0

            1st Component                                 2nd                                 3rd




UNSIGNED SHORT 4 4 4 4:
   15     14       13     12   11     10         9   8          7   6          5   4   3     2            1   0

         1st Component                     2nd                           3rd                        4th




UNSIGNED SHORT 5 5 5 1:
   15     14       13     12   11     10         9    8         7   6          5   4   3      2           1   0

               1st Component                          2nd                              3rd                    4th


                               Table 3.6: UNSIGNED SHORT formats




                                    Version 1.1.12 (April 24, 2008)
3.6. PIXEL RECTANGLES                                                             71


        Format       First         Second          Third           Fourth
                   Component      Component      Component       Component
        RGB           red           green          blue
        RGBA          red           green          blue            alpha

                    Table 3.7: Packed pixel field assignments.



    The assignment of component to fields in the packed pixel is as described in
table 3.7
    The above discussions of row length and image extraction are valid for packed
pixels, if “group” is substituted for “component” and the number of components
per group is understood to be one.

Conversion to floating-point
Each element in a group is converted to a floating-point value according to the ap-
propriate formula in table 2.7 (section 2.12). For packed pixel types, each element
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
Each group is converted to a group of 4 elements as follows: if a group does not
contain an A element, then A is added and set to 1.0. If any of R, G, or B is missing
from the group, each missing element is added and assigned a value of 0.0.




                          Version 1.1.12 (April 24, 2008)
3.7. TEXTURING                                                                                72


3.7     Texturing
Texturing maps a portion of one or more specified images onto each primitive for
which texturing is enabled. This mapping is accomplished by using the color of
an image at the location indicated by a fragment’s (s, t) coordinates to modify the
fragment’s RGBA color.
     An implementation may support texturing using more than one image at a time.
In this case the fragment carries multiple sets of texture coordinates (s, t) which
are used to index separate images to produce color values which are collectively
used to modify the fragment’s RGBA color. The following subsections (up to
and including section 3.7.7) specify the GL operation with a single texture and
section 3.7.13 specifies the details of how multiple texture units interact.
     The GL provides a means to specify the details of how texturing of a primitive
is effected. These details include specification of the image to be texture mapped,
the means by which the image is filtered when applied to the primitive, and the
function that determines what RGBA value is produced given a fragment color and
an image value.

3.7.1    Texture Image Specification
The command

        void TexImage2D( enum target, int level,
           int internalformat, sizei width, sizei height,
           int border, enum format, enum type, void *data );

is used to specify a texture image. target must be TEXTURE 2D. format, type, and
data specify the format of the image data, the type of those data, and a pointer to
the image data in host memory, as described in section 3.6.2.
     The groups in memory are treated as being arranged in a rectangle. The rectan-
gle is an image, whose size and organization are specified by the width and height
parameters to TexImage2D.
     The selected groups are processed as described in section 3.6.2, stopping after
final expansion to RGBA. Each R, G, B, or A value so generated is clamped to
[0, 1].
     Components are then selected from the resulting R, G, B, or A values to obtain
a texture with the base internal format specified by internalformat, which must
match format; no conversions between formats are supported during texture im-
age processing.1 Table 3.8 summarizes the mapping of R, G, B, and A values to
   1
    When a non-RGBA format and internalformat are specified, implementations are not required to
actually create and then discard unnecessary R, G, B, or A components. The abstract model defined


                             Version 1.1.12 (April 24, 2008)
3.7. TEXTURING                                                                    73


               Base Internal Format          RGBA           Internal Components
               ALPHA                         A              A
               LUMINANCE                     R              L
               LUMINANCE ALPHA               R,A            L,A
               RGB                           R,G,B          R,G,B
               RGBA                          R,G,B,A        R,G,B,A

Table 3.8: Conversion from RGBA pixel components to internal texture compo-
nents. See section 3.7.12 for a description of the texture components R, G, B, A,
and L.


texture components, as a function of the base internal format of the texture image.
internalformat may be one of the five internal format symbolic constants listed in
table 3.8. Specifying a value for internalformat that is not one of the above values
generates the error INVALID VALUE. If internalformat does not match format, the
error INVALID OPERATION is generated.
     The GL stores the resulting texture with internal component resolutions of its
own choosing. The allocation of internal component resolution may vary based
on any TexImage2D parameter (except target), but the allocation must not be a
function of any other state and cannot be changed once established. Allocation
must be invariant; the same allocation must be chosen each time a texture image is
specified with the same parameter values.
     The image itself (pointed to by data) is a sequence of groups of values. The
first group is the lower left corner of the texture image. Subsequent groups fill
out rows of width width from left to right; height rows are stacked from bottom
to top forming the image. When the final R, G, B, and A components have been
computed for a group, they are assigned to components of a texel as described by
table 3.8. Counting from zero, each resulting N th texel is assigned internal integer
coordinates (i, j), where

                                      i = (N mod width)
                                    N
                                 j=(      mod height)
                                  width
Thus the last row of the image is indexed with the highest value of j.
    Each color component is converted (by rounding to nearest) to a fixed-point
value with n bits, where n is the number of bits of storage allocated to that com-
ponent in the image array. We assume that the fixed-point representation used
by section 3.6.2 is used only for consistency and ease of description.


                               Version 1.1.12 (April 24, 2008)
3.7. TEXTURING                                                                       74


represents each value k/(2n − 1), where k ∈ {0, 1, . . . , 2n − 1}, as k (e.g. 1.0 is
represented in binary as a string of all ones).
    The level argument to TexImage2D is an integer level-of-detail number. Levels
of detail are discussed below, under Mipmapping. The main texture image has a
level of detail number of 0. If a level-of-detail less than zero is specified, the error
INVALID VALUE is generated.
    If the border argument to TexImage2D is not zero, then the error
INVALID VALUE is generated.
    For non-zero width and height, it must be the case that

                                       ws = 2n                                   (3.12)


                                       hs = 2m                                   (3.13)
for some integers n and m, where ws and hs are the specified image width
and height. If any one of these relationships cannot be satisfied, then the error
INVALID VALUE is generated.
    An image with zero width or height indicates the null texture. If the null texture
is specified for level-of-detail zero, it is as if texturing were disabled.
    The maximum allowable width and height of a texture image must be at
least 2k for image arrays of level 0 through k, where k is the log base 2 of
MAX TEXTURE SIZE.
    An implementation may allow an image array of level 0 to be created only if
that single image array can be supported. Additional constraints on the creation of
image arrays of level 1 or greater are described in more detail in section 3.7.9.
    The image indicated to the GL by the image pointer is decoded and copied into
the GL’s internal memory.
    We shall refer to the decoded image as the texture array. A texture array has
width and height

                                       wt = 2n
                                       ht = 2m
where n and m are defined in equations 3.12 and 3.13.
    An element (i, j) of the texture array is called a texel. The texture value used in
texturing a fragment is determined by that fragment’s associated (s, t) coordinates,
but does not necessarily correspond to any actual texel. See figure 3.8.
    If the data argument of TexImage2D is a null pointer (a zero-valued pointer
in the C implementation), a texture array is created with the specified target, level,
internalformat, width, and height, but with unspecified image contents. In this

                           Version 1.1.12 (April 24, 2008)
3.7. TEXTURING                                                                           75




             1.0 4.0
                       3

                                       α
                       2
              t   v    j                   β
                       1


                       0
             0.0 0.0
                             0     1       2   3   i 4   5     6    7

                       0.0                         u                    8.0

                       0.0                         s                    1.0




  Figure 3.8. A texture image and the coordinates used to access it. This is a texture
  with n = 3 and m = 2. α and β, values used in blending adjacent texels to obtain a
  texture value, are also shown.




                             Version 1.1.12 (April 24, 2008)
3.7. TEXTURING                                                                        76


case no pixel values are accessed in client memory, and no pixel processing is
performed. Errors are generated, however, exactly as though the data pointer were
valid.

3.7.2    Alternate Texture Image Specification Commands
Texture images may also be specified using image data taken directly from the
framebuffer, and rectangular subregions of existing texture images may be respec-
ified.
     The command

        void CopyTexImage2D( enum target, int level,
           enum internalformat, int x, int y, sizei width,
           sizei height, int border );

defines a texture array in exactly the manner of TexImage2D, except that the image
data are taken from the framebuffer rather than from client memory. target must
be TEXTURE 2D, x, y, width, and height correspond precisely to the corresponding
arguments to ReadPixels (refer to section 4.3.1); they specify the image’s width
and height, and the lower left (x, y) coordinates of the framebuffer region to be
copied. The image is taken from the color buffer of the framebuffer exactly as
if these arguments were passed to ReadPixels with argument format set to RGBA,
stopping after conversion of RGBA values. Subsequent processing is identical
to that described for TexImage2D, beginning with clamping of the R, G, B, and
A values from the resulting pixel groups. Parameters level, internalformat, and
border are specified using the same values, with the same meanings, as the equiv-
alent arguments of TexImage2D. internalformat is further constrained such that
color buffer components can be dropped during the conversion to internalformat,
but new components cannot be added. For example, an RGB color buffer can be
used to create LUMINANCE or RGB textures, but not ALPHA, LUMINANCE ALPHA, or
RGBA textures. Table 3.9 summarizes the allowable framebuffer and base internal
format combinations. If the framebuffer format is not compatible with the base tex-
ture format, an INVALID OPERATION error is generated. The constraints on width,
height, and border are exactly those for the equivalent arguments of TexImage2D.
     Two additional commands,

        void TexSubImage2D( enum target, int level, int xoffset,
           int yoffset, sizei width, sizei height, enum format,
           enum type, void *data );



                             Version 1.1.12 (April 24, 2008)
3.7. TEXTURING                                                                    77


                                         Texture Format
                  Color Buffer    A    L LA RGB RGBA
                  A                    –   –      –     –
                  L                –       –      –     –
                  LA                              –     –
                  RGB              –       –            –
                  RGBA

      Table 3.9: CopyTexImage internal format/color buffer combinations.



      void CopyTexSubImage2D( enum target, int level,
         int xoffset, int yoffset, int x, int y, sizei width,
         sizei height );

respecify only a rectangular subregion of an existing texture array. No change
is made to the internalformat, width, or height, parameters of the specified tex-
ture array, nor is any change made to texel values outside the specified subre-
gion. The target arguments of TexSubImage2D and CopyTexSubImage2D must
be TEXTURE 2D. The level parameter of each command specifies the level of the
texture array that is modified. If level is less than zero or greater than the base 2
logarithm of the maximum texture width or height, the error INVALID VALUE is
generated.
    TexSubImage2D arguments width, height, format, type, and data match the
corresponding arguments to TexImage2D, meaning that they are specified using
the same values, and have the same meanings.
    CopyTexSubImage2D arguments x, y, width, and height match the corre-
sponding arguments to CopyTexImage2D. Each of the TexSubImage commands
interprets and processes pixel groups in exactly the manner of its TexImage coun-
terpart, except that the assignment of R, G, B, and A pixel group values to the
texture components is controlled by the internalformat of the texture array, not
by an argument to the command. The same constraints and errors apply to the
TexSubImage commands’ argument format and the internalformat of the texture
array being respecified as apply to the format and internalformat arguments of its
TexImage counterparts.
    Arguments xoffset and yoffset of TexSubImage2D and CopyTexSubImage2D
specify the lower left texel coordinates of a width-wide by height-high rectangular
subregion of the texture array, address as in figure 3.8. Taking ws and hs to be
the specified width and height of the texture array, and taking x, y, w, and h to
be the xoffset, yoffset, width, and height argument values, any of the following

                          Version 1.1.12 (April 24, 2008)
3.7. TEXTURING                                                                     78


relationships generates the error INVALID VALUE:

                                       x<0
                                    x + w > ws
                                       y<0
                                    y + h > hs
Counting from zero, the nth pixel group is assigned to the texel with internal integer
coordinates [i, j], where

                                i = x + (n mod w)
                                         n
                              j =y+(        mod h)
                                         w

3.7.3    Compressed Texture Images
Texture images may also be specified or modified using image data already stored
in a known compressed image format. The GL defines some specific com-
pressed formats, and others may be defined by GL extensions. There is a mech-
anism to obtain token values for compressed formats; the number of specific
compressed internal formats supported can be obtained by querying the value
of NUM COMPRESSED TEXTURE FORMATS. The set of specific compressed inter-
nal formats supported by the renderer can be obtained by querying the value
of COMPRESSED TEXTURE FORMATS. The only values returned by this query are
those corresponding to internalformat parameters accepted by CompressedTex-
Image2D and suitable for general-purpose usage. The renderer will not enumerate
formats with restrictions that need to be specifically understood prior to use.
    The command

        void CompressedTexImage2D( enum target, int level,
           enum internalformat, sizei width, sizei height,
           int border, sizei imageSize, void *data );

defines a texture image, with incoming data stored in a specific compressed image
format. The target, level, internalformat, width, height, and border parameters
have the same meaning as in TexImage2D. data points to compressed image data
stored in the compressed image format corresponding to internalformat.
    For all compressed internal formats, the compressed image will be decoded ac-
cording to the definition of internalformat. Compressed texture images are treated
as an array of imageSize ubytes beginning at address data. All pixel storage and

                          Version 1.1.12 (April 24, 2008)
3.7. TEXTURING                                                                           79


pixel transfer modes are ignored when decoding a compressed texture image. If the
imageSize parameter is not consistent with the format, dimensions, and contents of
the compressed image, an INVALID VALUE error results. If the compressed image
is not encoded according to the defined image format, the results of the call are
undefined.
    Specific compressed internal formats may impose format-specific restrictions
on the use of the compressed image specification calls or parameters. For example,
the compressed image format might not allow width or height values that are not a
multiple of 4. Any such restrictions will be documented in the extension specifica-
tion defining the compressed internal format; violating these restrictions will result
in an INVALID OPERATION error.
    Any restrictions imposed by specific compressed internal formats will be in-
variant with respect to image contents, meaning that if the GL accepts and stores
a texture image in compressed form, CompressedTexImage2D will accept any
properly encoded compressed texture image of the same width, height, compressed
image size, and compressed internal format for storage at the same texture level.
    The specific compressed texture formats supported by CompressedTexIm-
age2D, and the corresponding base internal format for each specific format, are
defined in table 3.10.

               Compressed Texture Format        Base Internal Format
               PALETTE4    RGB8 OES             RGB
               PALETTE4    RGBA8 OES            RGBA
               PALETTE4    R5 G6 B5 OES         RGB
               PALETTE4    RGBA4 OES            RGBA
               PALETTE4    RGB5 A1 OES          RGBA
               PALETTE8    RGB8 OES             RGB
               PALETTE8    RGBA8 OES            RGBA
               PALETTE8    R5 G6 B5 OES         RGB
               PALETTE8    RGBA4 OES            RGBA
               PALETTE8    RGB5 A1 OES          RGBA

                 Table 3.10: Specific compressed texture formats.




Respecifying Subimages of Compressed Textures
The command



                              Version 1.1.12 (April 24, 2008)
3.7. TEXTURING                                                                    80


        void CompressedTexSubImage2D( enum target, int level,
           int xoffset, int yoffset, sizei width, sizei height,
           enum format, sizei imageSize, void *data );

respecifies only a rectangular region of an existing texture array, with incoming
data stored in a known compressed image format. The target, level, xoffset, yoffset,
width, height, and format parameters have the same meaning as in TexSubIm-
age2D. data points to compressed image data stored in the compressed image for-
mat corresponding to format.
    The image pointed to by data and the imageSize parameter is interpreted as
though it was provided to CompressedTexImage2D. This command does not pro-
vide for image format conversion, so an INVALID OPERATION error results if for-
mat does not match the internal format of the texture image being modified. If the
imageSize parameter is not consistent with the format, dimensions, and contents
of the compressed image (too little or too much data), an INVALID VALUE error
results.
    As with CompressedTexImage calls, compressed internal formats may have
additional restrictions on the use of the compressed image specification calls or
parameters. Any such restrictions will be documented in the specification defin-
ing the compressed internal format; violating these restrictions will result in an
INVALID OPERATION error.
    Any restrictions imposed by specific compressed internal formats will be in-
variant with respect to image contents, meaning that if the GL accepts and stores a
texture image in compressed form, CompressedTexSubImage2D will accept any
properly encoded compressed texture image of the same width, height, compressed
image size, and compressed internal format for storage at the same texture level.
    Calling CompressedTexSubImage2D will result in an INVALID OPERATION
error if xoffset or yoffset is not equal to zero, or if width and height do not match
the width and height of the texture, respectively. The contents of any texel outside
the region modified by the call are undefined. These restrictions may be relaxed
for specific compressed internal formats whose images are easily modified.

3.7.4    Compressed Paletted Textures
If internalformat is PALETTE4 RGB8, PALETTE4 RGBA8, PALETTE4 R5 G6 B5,
PALETTE4 RGBA4, PALETTE4 RGB5 A1, PALETTE8 RGB8, PALETTE8 RGBA8,
PALETTE8 R5 G6 B5, PALETTE8 RGBA4, or PALETTE8 RGB5 A1, the com-
pressed texture is a compressed paletted texture. data contains the palette data
followed by the mipmap levels, where the number of mipmap levels stored is given



                          Version 1.1.12 (April 24, 2008)
3.7. TEXTURING                                                                                                       81


by |level| + 1. The number of bits that represent a texel is 4 bits if internalformat
is PALETTE4 * and is 8 bits if internalformat is PALETTE8 *.
    The palette data is formatted as an image containing 16 (for PALETTE4 *) or
256 (for PALETTE8 *) palette entries (pixels). The equivalent format and type of
each palette entry is shown in table 3.11.

    Compressed Texture Format                   Palette entry      Palette entry
                                                format             type
    PALETTE4          RGB8 OES                  RGB                UNSIGNED            BYTE
    PALETTE4          RGBA8 OES                 RGBA               UNSIGNED            BYTE
    PALETTE4          R5 G6 B5 OES              RGB                UNSIGNED            SHORT        565
    PALETTE4          RGBA4 OES                 RGBA               UNSIGNED            SHORT        4444
    PALETTE4          RGB5 A1 OES               RGBA               UNSIGNED            SHORT        5551
    PALETTE8          RGB8 OES                  RGB                UNSIGNED            BYTE
    PALETTE8          RGBA8 OES                 RGBA               UNSIGNED            BYTE
    PALETTE8          R5 G6 B5 OES              RGB                UNSIGNED            SHORT        565
    PALETTE8          RGBA4 OES                 RGBA               UNSIGNED            SHORT        4444
    PALETTE8          RGB5 A1 OES               RGBA               UNSIGNED            SHORT        5551

                          Table 3.11: Palette entry pixel formats.


    Image data immediately follows the palette image. Each mipmap level im-
age present in the image data immediately follows the previous level, starting
with mipmap level zero and proceeding through the number of levels defined by
|level| + 1. Texels within each mipmap level image are formatted as shown in
table 3.12 and are packed contiguously starting at the lower left.
PALETTE4 *:
                           7    6         5      4     3   2         1     0

                                    1st texel                  2nd texel




PALETTE8 *:
  31 30 29 28 27 26 25 24 23 22 21 20 19 18 17 16 15 14 13 12 11 10 9          8   7   6   5   4     3   2   1   0

          1st texel                   2nd                         3rd                              4th


         Table 3.12: Texel data formats for compressed paletted textures.


    If a compressed paletted texture is specified with a positive level argument to

                               Version 1.1.12 (April 24, 2008)
3.7. TEXTURING                                                                  82


     Name                        Type     Legal Values
     TEXTURE WRAP S             integer   CLAMP TO EDGE, REPEAT
     TEXTURE WRAP T             integer   CLAMP TO EDGE, REPEAT
     TEXTURE MIN FILTER         integer   NEAREST,
                                          LINEAR,
                                          NEAREST MIPMAP NEAREST,
                                          NEAREST MIPMAP LINEAR,
                                          LINEAR MIPMAP NEAREST,
                                          LINEAR MIPMAP LINEAR,
     TEXTURE MAG FILTER         integer   NEAREST,
                                          LINEAR
     GENERATE MIPMAP           boolean    TRUE or FALSE

                 Table 3.13: Texture parameters and their values.



TexImage2D, an INVALID VALUE error is generated.
    Subimages may not be specified for compressed paletted textures. Calling
CompressedTexSubImage2D with any of the PALETTE* arguments in table 3.11
will generate an INVALID OPERATION error.

3.7.5    Texture Parameters
Various parameters control how the texture array is treated when specified or
changed, and when applied to a fragment. Each parameter is set by calling

        void TexParameter{ixf}( enum target, enum pname,
           T param );
        void TexParameter{ixf}v( enum target, enum pname,
           T params );

target is the target, which must be TEXTURE 2D. pname is a symbolic constant indi-
cating the parameter to be set; the possible constants and corresponding parameters
are summarized in table 3.13. In the first form of the command, param is a value
to which to set a single-valued parameter; in the second form of the command,
params is an array of parameters whose type depends on the parameter being set.
    If the value of texture parameter GENERATE MIPMAP is TRUE, specifying or
changing texture arrays may have side effects, which are discussed in the Auto-
matic Mipmap Generation discussion of section 3.7.7.



                         Version 1.1.12 (April 24, 2008)
3.7. TEXTURING                                                                      83


3.7.6   Texture Wrap Modes
Wrap modes defined by the values of TEXTURE WRAP S or TEXTURE WRAP T re-
spectively affect the interpretation of s and t texture coordinates. The effect of each
mode is described below.

Wrap Mode REPEAT
Wrap mode REPEAT ignores the integer part of texture coordinates, using only the
fractional part. (For a number f , the fractional part is f − f , regardless of the
sign of f ; recall that the function truncates towards −∞.)
    REPEAT is the default behavior for all texture coordinates.

Wrap Mode CLAMP TO EDGE
Wrap mode CLAMP TO EDGE clamps texture coordinates at all mipmap levels such
that the texture filter never samples outside the texture image. The color returned
when clamping is derived only from texels at the edge of the texture image.
    Texture coordinates are clamped to the range [min, max]. The minimum value
is defined as
                                            1
                                     min =
                                           2N
where N is the size of the texture image in the direction of clamping. The maxi-
mum value is defined as

                                  max = 1 − min
so that clamping is always symmetric about the [0, 1] mapped range of a texture
coordinate.

3.7.7   Texture Minification
Applying a texture to a primitive implies a mapping from texture image space to
framebuffer image space. In general, this mapping involves a reconstruction of
the sampled texture image, followed by a homogeneous warping implied by the
mapping to framebuffer space, then a filtering, followed finally by a resampling
of the filtered, warped, reconstructed image before applying it to a fragment. In
the GL this mapping is approximated by one of two simple filtering schemes. One
of these schemes is selected based on whether the mapping from texture space to
framebuffer space is deemed to magnify or minify the texture image.


                          Version 1.1.12 (April 24, 2008)
3.7. TEXTURING                                                                           84


Scale Factor and Level of Detail
The choice is governed by a scale factor ρ(x, y) and the level of detail parameter
λ(x, y), defined as

                                λ(x, y) = log2 [ρ(x, y)]
    If λ(x, y) is less than or equal to the constant c (described below in sec-
tion 3.7.8) the texture is said to be magnified; if it is greater, the texture is minified.
    Let s(x, y) be the function that associates an s texture coordinate with each set
of window coordinates (x, y) that lie within a primitive; define t(x, y) analogously.
Let u(x, y) = 2n s(x, y) and v(x, y) = 2m t(x, y), where n and m are as defined by
equations 3.12 and 3.13 with ws and hs equal to the width and height of the image
array whose level is zero. For a polygon, ρ is given at a fragment with window
coordinates (x, y) by
                                                                                
                                    2               2               2            2
                              ∂u           ∂v                 ∂u           ∂v
             ρ = max                    +               ,               +             (3.14)
                              ∂x           ∂x                 ∂y           ∂y   

where ∂u/∂x indicates the derivative of u with respect to window x, and similarly
for the other derivatives.
    For a line, the formula is

                                            2                                2
                       ∂u      ∂u                           ∂v      ∂v
              ρ=          ∆x +    ∆y            +              ∆x +    ∆y        l,   (3.15)
                       ∂x      ∂y                           ∂x      ∂y
where ∆x = x2 − x1 and ∆y = y2 − y1 with (x1 , y1 ) and (x2 , y2 ) being the
segment’s window coordinate endpoints and l = ∆x2 + ∆y 2 . For a point or
point sprite, ρ ≡ 1.
    While it is generally agreed that equations 3.14 and 3.15 give the best results
when texturing, they are often impractical to implement. Therefore, an imple-
mentation may approximate the ideal ρ with a function f (x, y) subject to these
conditions:

   1. f (x, y) is continuous and monotonically increasing in each of |∂u/∂x|,
      |∂u/∂y|, |∂v/∂x|, |∂v/∂y|,

   2. Let
                                                        ∂u ∂u
                                  mu = max                ,
                                                        ∂x ∂y

                                                        ∂v   ∂v
                                  mv = max                 ,
                                                        ∂x ∂y

                            Version 1.1.12 (April 24, 2008)
3.7. TEXTURING                                                                     85


       Then max{mu , mv } ≤ f (x, y) ≤ mu + mv .

    When λ indicates minification, the value assigned to TEXTURE MIN FILTER
is used to determine how the texture value for a fragment is selected. When
TEXTURE MIN FILTER is NEAREST, the texel in the image array of level zero that
is nearest (in Manhattan distance) to that specified by (s, t) is obtained. This means
the texel at location (i, j) becomes the texture value, with i given by

                                      u ,    s<1
                              i=                                               (3.16)
                                     2n − 1, s = 1
(Recall that if TEXTURE WRAP S is REPEAT, then 0 ≤ s < 1.) Similarly, j is found
as

                                      v ,   t<1
                             j=       m                                        (3.17)
                                     2 − 1, t = 1
    When TEXTURE MIN FILTER is LINEAR, a 2 × 2 square of texels in the image
array of level zero is selected. This square is obtained by first wrapping texture
coordinates as described in section 3.7.6, then computing

                    u − 1/2 mod 2n , TEXTURE WRAP S is REPEAT
           i0 =
                    u − 1/2 ,        otherwise

and

                    v − 1/2 mod 2m , TEXTURE WRAP T is REPEAT
          j0 =
                    v − 1/2 ,        otherwise

Then

                    (i0 + 1) mod 2n , TEXTURE WRAP S is REPEAT
            i1 =
                    i0 + 1,           otherwise

and

                    (j0 + 1) mod 2m , TEXTURE WRAP T is REPEAT
           j1 =
                    j0 + 1,           otherwise

Let
                                α = frac(u − 1/2)
                                 β = frac(v − 1/2)


                          Version 1.1.12 (April 24, 2008)
3.7. TEXTURING                                                                 86


where frac(x) denotes the fractional part of x.
   The texture value τ is found as


   τ = (1 − α)(1 − β)τi0 j0 + α(1 − β)τi1 j0 + (1 − α)βτi0 j1 + αβτi1 j1   (3.18)

where τij is the texel at location (i, j) in the texture image.

Mipmapping
TEXTURE MIN FILTER          values          NEAREST MIPMAP NEAREST,
NEAREST MIPMAP LINEAR,          LINEAR MIPMAP NEAREST,          and
LINEAR MIPMAP LINEAR each require the use of a mipmap. A mipmap is
an ordered set of arrays representing the same image; each array has a resolution
lower than the previous one. If the image array of level zero has dimensions
2n × 2m , then there are max{n, m} + 1 image arrays in the mipmap. Each array
subsequent to the array of level zero has dimensions

                                σ(i − 1) × σ(j − 1)
where the dimensions of the previous array are

                                     σ(i) × σ(j)
and
                                           2x x > 0
                               σ(x) =
                                           1 x≤0

until the last array is reached with dimension 1 × 1.
    Each array in a mipmap is defined using TexImage2D or CopyTexImage2D;
the array being set is indicated with the level-of-detail argument level. Level-
of-detail numbers proceed from zero for the original texture array through q =
max{n, m} with each unit increase indicating an array of half the dimensions of
the previous one as already described. All arrays from zero through q must be
defined, as discussed in section 3.7.9.
    The mipmap is used in conjunction with the level of detail to approximate the
application of an appropriately filtered texture to a fragment. Let c be the value
of λ at which the transition from minification to magnification occurs (since this
discussion pertains to minification, we are concerned only with values of λ where
λ > c).
    For         mipmap          filters     NEAREST MIPMAP NEAREST            and
LINEAR MIPMAP NEAREST, the dth mipmap array is selected, where


                           Version 1.1.12 (April 24, 2008)
3.7. TEXTURING                                                                      87


                         
                          0,
                                            λ ≤ 12
                                   1
                    d=        λ+   2    − 1, λ > 12 , λ ≤ q +   1
                                                                2               (3.19)
                                             λ > q + 12
                         
                          q,

    The rules for NEAREST or LINEAR filtering are then applied to the selected
array.
    For mipmap filters NEAREST MIPMAP LINEAR and LINEAR MIPMAP LINEAR,
the level d1 and d2 mipmap arrays are selected, where

                                        q,   λ≥q
                            d1 =                                                (3.20)
                                         λ , otherwise

                                       q,      λ≥q
                           d2 =                                                 (3.21)
                                       d1 + 1, otherwise
    The rules for NEAREST or LINEAR filtering are then applied to each of the
selected arrays, yielding two corresponding texture values τ1 and τ2 . The final
texture value is then found as

                         τ = [1 − frac(λ)]τ1 + frac(λ)τ2 .

Automatic Mipmap Generation
If the value of texture parameter GENERATE MIPMAP is TRUE, making any change
to the texels of the zero level array of a mipmap will also compute a complete set
of mipmap arrays (as defined in section 3.7.9) derived from the modified zero level
array. Array levels 1 through q are replaced with the derived arrays, regardless of
their previous contents. The zero level array is left unchanged by this computation.
     The internal formats of the derived mipmap arrays all match those of the zero
level array, and the dimensions of the derived arrays follow the requirements de-
scribed in section 3.7.9.
     The contents of the derived arrays are computed by repeated, filtered reduction
of the zero level array. No particular filter algorithm is required, though a 2 × 2 box
filter is recommended as the default filter. In some implementations, filter quality
may be affected by hints (section 5.2).
     Automatic mipmap generation is not performed when the zero level array is
stored in a compressed internal format.




                          Version 1.1.12 (April 24, 2008)
3.7. TEXTURING                                                                    88


3.7.8   Texture Magnification
When λ indicates magnification, the value assigned to TEXTURE MAG FILTER
determines how the texture value is obtained. There are two possible values
for TEXTURE MAG FILTER: NEAREST and LINEAR. NEAREST behaves exactly as
NEAREST for TEXTURE MIN FILTER (equations 3.16 and 3.17 are used); LINEAR
behaves exactly as LINEAR for TEXTURE MIN FILTER (equation 3.18 is used).
The level-of-detail zero texture array is always used for magnification.
     Finally, there is the choice of c, the minification vs. magnification switch-
over point. If the magnification filter is given by LINEAR and the minification
filter is given by NEAREST MIPMAP NEAREST or NEAREST MIPMAP LINEAR, then
c = 0.5. This is done to ensure that a minified texture does not appear “sharper”
than a magnified texture. Otherwise c = 0.

3.7.9   Texture Completeness
A texture is said to be complete if all the image arrays and texture parameters
required to utilize the texture for texture application is consistently defined.
    A texture is complete if the following conditions all hold true:

   • The set of mipmap arrays zero through q (where q is defined in the Mipmap-
     ping discussion of section 3.7.7) were each specified with the same internal
     format.

   • The dimensions of the arrays follow the sequence described in the Mipmap-
     ping discussion of section 3.7.7.

   • Each dimension of the zero level array is positive.

Effects of Completeness on Texture Application
If texturing is enabled for a texture unit at the time a primitive is rasterized, if
TEXTURE MIN FILTER is one that requires a mipmap, and if the texture image
bound to the enabled texture target is not complete, then it is as if texture mapping
were disabled for that texture unit.

Effects of Completeness on Texture Image Specification
An implementation may allow a texture image array of level 1 or greater to be
created only if a complete set of image arrays consistent with the requested array
can be supported.



                          Version 1.1.12 (April 24, 2008)
3.7. TEXTURING                                                                             89


3.7.10    Texture State
The state necessary for texture can be divided into two categories. First, there is
the set of mipmap arrays and their number. Each array has associated with it a
width and height, an integer describing the internal format of the image, six integer
values describing the resolutions of each of the red, green, blue, alpha, luminance,
and intensity components of the image, a boolean describing whether the image is
compressed or not, and an integer size of a compressed image. Each initial texture
array is null (zero width and height, internal format 1, with the compressed flag
set to FALSE, a zero compressed size, and zero-sized components). Next, there
are the two sets of texture properties; each consists of the selected minification
and magnification filters, the wrap modes for s and t, and a boolean indicating
whether automatic mipmap generation should be performed. In the initial state,
the value assigned to TEXTURE MIN FILTER is NEAREST MIPMAP LINEAR, and
the value for TEXTURE MAG FILTER is LINEAR. s and t wrap modes are both set
to REPEAT. The value of GENERATE MIPMAP is false.

3.7.11    Texture Objects
In addition to the default texture TEXTURE 2D, named texture objects can be cre-
ated and operated upon. The name space for texture objects is the unsigned inte-
gers, with zero reserved by the GL.
    A texture object is created by binding an unused name to TEXTURE 2D. The
binding is effected by calling

      void BindTexture( enum target, uint texture );

with target set to TEXTURE 2D and texture set to the unused name. The result-
ing texture object is a new state vector, comprising all the state values listed in
section 3.7.10, set to the same initial values.
    BindTexture may also be used to bind an existing texture object to
TEXTURE 2D. If the bind is successful no change is made to the state of the bound
texture object, and any previous binding to target is broken.
    While a texture object is bound, GL operations on the target to which it is
bound affect the bound object, and queries of the target to which it is bound return
state from the bound object. If texture mapping is enabled, the state of the bound
texture object directs the texturing operation.
    TEXTURE 2D has a texture state vector associated with it. In order that access
to this initial texture not be lost, it is treated as a texture object whose names is 0.
The initial texture is therefore operated upon, queried, and applied as TEXTURE 2D
while 0 is bound to the corresponding targets.

                               Version 1.1.12 (April 24, 2008)
3.7. TEXTURING                                                                        90


    Texture objects are deleted by calling

      void DeleteTextures( sizei n, uint *textures );

textures contains n names of texture objects to be deleted. After a texture object
is deleted, it has no contents, and its name is again unused. If a texture that is
currently bound to the target TEXTURE 2D is deleted, it is as though BindTexture
had been executed with the same target and texture zero. Unused names in textures
are silently ignored, as is the value zero.
    The command

      void GenTextures( sizei n, uint *textures );

returns n previously unused texture object names in textures. These names are
marked as used, for the purposes of GenTextures only, but they acquire texture
state only when they are first bound, just as if they were unused.
    The texture object name space, including the initial texture object, is shared
among all texture units. A texture object may be bound to more than one texture
unit simultaneously. After a texture object is bound, any GL operations on that tar-
get object affect any other texture units to which the same texture object is bound.
    Texture binding is affected by the setting of the state ACTIVE TEXTURE.
    If a texture object is deleted, it is as if all texture units which are bound to that
texture object are rebound to texture object zero.

3.7.12    Texture Environments and Texture Functions
The command

      void TexEnv{ixf}( enum target, enum pname, T param );
      void TexEnv{ixf}v( enum target, enum pname, T params );

sets parameters of the texture environment that specifies how texture values are
interpreted when texturing a fragment.
    target must be TEXTURE ENV. pname is a symbolic constant indicating the pa-
rameter to be set. In the first form of the command, param is a value to which to
set a single-valued parameter; in the second form, params is a pointer to an array
of parameters: either a single symbolic constant or a value or group of values to
which the parameter should be set.
    The possible environment parameters are TEXTURE ENV MODE,
TEXTURE ENV COLOR, COMBINE RGB, COMBINE ALPHA, RGB SCALE, and
ALPHA SCALE. TEXTURE ENV MODE may be set to one of REPLACE, MODULATE,


                           Version 1.1.12 (April 24, 2008)
3.7. TEXTURING                                                                                     91


                        Texture Base                Texture source color
                        Internal Format                   Cs        As
                        ALPHA                         (0, 0, 0)     At
                        LUMINANCE                   (Lt , Lt , Lt )  1
                        LUMINANCE ALPHA             (Lt , Lt , Lt ) At
                        RGB                         (Rt , Gt , Bt )  1
                        RGBA                        (Rt , Gt , Bt ) At

Table 3.14: Correspondence of filtered texture components to texture source com-
ponents.



DECAL, BLEND, ADD, or COMBINE. TEXTURE ENV COLOR is set to an RGBA color
by providing four values in the range [0, 1] (values outside this range are clamped
to it). RGB SCALE and ALPHA SCALE may only be set to 1.0, 2.0, or 4.0; other
values will generate an INVALID VALUE error.
     If integer values are provided for TEXTURE ENV COLOR, RGB SCALE, or
ALPHA SCALE, then they are converted to floating-point as specified in table 2.7
for signed integers.
     The value of TEXTURE ENV MODE specifies a texture function. The result of
this function depends on the fragment and the texture array value. The precise
form of the function depends on the base internal formats of the texture arrays that
were last specified.
     Cf and Af 2 are the primary color components of the incoming fragment; Cs
and As are the components of the texture source color, derived from the filtered
texture values Rt , Gt , Bt , At , Lt , and It as shown in table 3.14; Cc and Ac are
the components of the texture environment color; Cp and Ap are the components
resulting from the previous texture environment (for texture environment 0, Cp and
Ap are identical to Cf and Af , respectively); and Cv and Av are the primary color
components computed by the texture function.
     All of these color values are in the range [0, 1]. The texture functions are spec-
ified in tables 3.15, 3.16, and 3.17.
     If the value of TEXTURE ENV MODE is COMBINE, the form of the texture func-
tion depends on the values of COMBINE RGB and COMBINE ALPHA, according to
table 3.17. The RGB and ALPHA results of the texture function are then multi-
   2
     In the remainder of section 3.7.12, the notation Cx is used to denote each of the three components
Rx , Gx , and Bx of a color specified by x. Operations on Cx are performed independently for each
color component. The A component of colors is usually operated on in a different fashion, and is
therefore denoted separately by Ax .



                               Version 1.1.12 (April 24, 2008)
3.7. TEXTURING                                                                   92




 Texture Base            REPLACE     MODULATE      DECAL
 Internal Format         Function    Function      Function
 ALPHA                   Cv = Cp     Cv = Cp       undefined
                         Av = As     Av = Ap As
 LUMINANCE               Cv = Cs     Cv = Cp Cs    undefined
 (or 1)                  Av = Ap     Av = Ap
 LUMINANCE ALPHA         Cv = Cs     Cv = Cp Cs    undefined
 (or 2)                  Av = As     Av = Ap As
 RGB                     Cv = Cs     Cv = Cp Cs    Cv   = Cs
 (or 3)                  Av = Ap     Av = Ap       Av   = Ap
 RGBA                    Cv = Cs     Cv = Cp Cs    Cv   = Cp (1 − As ) + Cs As
 (or 4)                  Av = As     Av = Ap As    Av   = Ap

          Table 3.15: Texture functions REPLACE, MODULATE, and DECAL.




       Texture Base          BLEND                         ADD
       Internal Format       Function                      Function
       ALPHA                 Cv = Cp                       Cv = Cp
                             Av = Ap As                    Av = Ap As
       LUMINANCE             Cv = Cp (1 − Cs ) + Cc Cs     Cv = Cp + Cs
       (or 1)                Av = Ap                       Av = Ap
       LUMINANCE ALPHA       Cv = Cp (1 − Cs ) + Cc Cs     Cv = Cp + Cs
       (or 2)                Av = Ap As                    Av = Ap As
       RGB                   Cv = Cp (1 − Cs ) + Cc Cs     Cv = Cp + Cs
       (or 3)                Av = Ap                       Av = Ap
       RGBA                  Cv = Cp (1 − Cs ) + Cc Cs     Cv = Cp + Cs
       (or 4)                Av = Ap As                    Av = Ap As

                  Table 3.16: Texture functions BLEND and ADD.




                         Version 1.1.12 (April 24, 2008)
3.7. TEXTURING                                                                    93


            COMBINE RGB        Texture Function
            REPLACE            Arg0
            MODULATE           Arg0 ∗ Arg1
            ADD                Arg0 + Arg1
            ADD SIGNED         Arg0 + Arg1 − 0.5
            INTERPOLATE        Arg0 ∗ Arg2 + Arg1 ∗ (1 − Arg2)
            SUBTRACT           Arg0 − Arg1
            DOT3 RGB           4 × ((Arg0r − 0.5) ∗ (Arg1r − 0.5)+
                                    (Arg0g − 0.5) ∗ (Arg1g − 0.5)+
                                     (Arg0b − 0.5) ∗ (Arg1b − 0.5))
            DOT3 RGBA          4 × ((Arg0r − 0.5) ∗ (Arg1r − 0.5)+
                                    (Arg0g − 0.5) ∗ (Arg1g − 0.5)+
                                     (Arg0b − 0.5) ∗ (Arg1b − 0.5))


             COMBINE ALPHA        Texture Function
             REPLACE              Arg0
             MODULATE             Arg0 ∗ Arg1
             ADD                  Arg0 + Arg1
             ADD SIGNED           Arg0 + Arg1 − 0.5
             INTERPOLATE          Arg0 ∗ Arg2 + Arg1 ∗ (1 − Arg2)
             SUBTRACT             Arg0 − Arg1

Table 3.17: COMBINE texture functions. The scalar expression computed for the
DOT3 RGB and DOT3 RGBA functions is placed into each of the 3 (RGB) or 4 (RGBA)
components of the output. The result generated from COMBINE ALPHA is ignored
for DOT3 RGBA.


plied by the values of RGB SCALE and ALPHA SCALE, respectively. The results are
clamped to [0, 1].
    The arguments Arg0, Arg1, and Arg2 are determined by the values of
SRCn RGB, SRCn ALPHA, OPERANDn RGB and OPERANDn ALPHA, where n = 0,
1, or 2, as shown in tables 3.18 and 3.19.
    The state required for the current texture environment, for each texture unit,
consists of a six-valued integer indicating the texture function, an eight-valued in-
teger indicating the RGB combiner function and a six-valued integer indicating the
ALPHA combiner function, six four-valued integers indicating the combiner RGB
and ALPHA source arguments, three four-valued integers indicating the combiner


                          Version 1.1.12 (April 24, 2008)
3.7. TEXTURING                                                  94




        SRCn RGB          OPERANDn RGB               Argument
        TEXTURE           SRC   COLOR                Cs
                          ONE   MINUS   SRC COLOR    1 − Cs
                          SRC   ALPHA                As
                          ONE   MINUS   SRC ALPHA    1 − As
        CONSTANT          SRC   COLOR                Cc
                          ONE   MINUS   SRC COLOR    1 − Cc
                          SRC   ALPHA                Ac
                          ONE   MINUS   SRC ALPHA    1 − Ac
        PRIMARY COLOR     SRC   COLOR                Cf
                          ONE   MINUS   SRC COLOR    1 − Cf
                          SRC   ALPHA                Af
                          ONE   MINUS   SRC ALPHA    1 − Af
        PREVIOUS          SRC   COLOR                Cp
                          ONE   MINUS   SRC COLOR    1 − Cp
                          SRC   ALPHA                Ap
                          ONE   MINUS   SRC ALPHA    1 − Ap

          Table 3.18: Arguments for COMBINE RGB functions.




        SRCn ALPHA        OPERANDn ALPHA             Argument
        TEXTURE           SRC   ALPHA                As
                          ONE   MINUS   SRC ALPHA    1 − As
        CONSTANT          SRC   ALPHA                Ac
                          ONE   MINUS   SRC ALPHA    1 − Ac
        PRIMARY COLOR     SRC   ALPHA                Af
                          ONE   MINUS   SRC ALPHA    1 − Af
        PREVIOUS          SRC   ALPHA                Ap
                          ONE   MINUS   SRC ALPHA    1 − Ap

         Table 3.19: Arguments for COMBINE ALPHA functions.




                   Version 1.1.12 (April 24, 2008)
3.7. TEXTURING                                                                      95


RGB operands, three two-valued integers indicating the combiner ALPHA operands,
four floating-point environment color values, and two three-valued floating-point
scale factors. In the initial state, the texture and combiner functions are each
MODULATE, the combiner RGB and ALPHA sources are each TEXTURE, PREVIOUS,
and CONSTANT for sources 0, 1, and 2 respectively, the combiner RGB operands for
sources 0 and 1 are each SRC COLOR, the combiner RGB operand for source 2, as
well as for the combiner ALPHA operands, are each SRC ALPHA, the environment
color is (0, 0, 0, 0), and RGB SCALE and ALPHA SCALE are each 1.0.

3.7.13    Texture Application
Texturing is enabled or disabled using the generic Enable and Disable commands,
with the symbolic constant TEXTURE 2D to enable or disable texturing, respec-
tively. If texturing is disabled, a rasterized fragment is passed on unaltered to the
next stage of the GL (although its texture coordinates may be discarded). Other-
wise, a texture value is found according to the parameter values of the currently
bound texture image using the rules given in sections 3.7.6 through 3.7.8. This
texture value is used along with the incoming fragment in computing the texture
function indicated by the currently bound texture environment. The result of this
function replaces the incoming fragment’s primary R, G, B, and A values. These
are the color values passed to subsequent operations. Other data associated with
the incoming fragment remain unchanged, except that the texture coordinates may
be discarded.
    Each texture unit is paired with an environment function, as shown in figure 3.9.
The second texture function is computed using the texture value from the second
texture, the fragment resulting from the first texture function computation and the
second texture unit’s environment function. If there is a third texture, the fragment
resulting from the second texture function is combined with the third texture value
using the third texture unit’s environment function and so on. The texture unit se-
lected by ActiveTexture determines which texture unit’s environment is modified
by TexEnv calls.
    If the value of TEXTURE ENV MODE is COMBINE, the texture function associated
with a given texture unit is computed using the values specified by SRCn RGB,
SRCn ALPHA, OPERANDn RGB and OPERANDn ALPHA.
    Texturing is enabled and disabled individually for each texture unit. If texturing
is disabled for one of the units, then the fragment resulting from the previous unit
is passed unaltered to the following unit.
    The required state, per texture unit, is one bit indicating whether texturing is
enabled or disabled. In the initial state, texturing is disabled for all texture units.



                          Version 1.1.12 (April 24, 2008)
3.7. TEXTURING                                                                           96




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




  Figure 3.9. Multitexture pipeline. Four texture units are shown; however, multitex-
  turing may support a different number of units depending on the implementation.
  The input fragment color is successively combined with each texture according to
  the state of the corresponding texture environment, and the resulting fragment color
  passed as input to the next texture unit in the pipeline.




                          Version 1.1.12 (April 24, 2008)
3.8. FOG                                                                           97


3.8    Fog
If enabled, fog blends a fog color with a rasterized fragment’s post-texturing color
using a blending factor f . Fog is enabled and disabled with the Enable and Disable
commands using the symbolic constant FOG.
    This factor f is computed according to one of three equations:

                                 f = exp(−d · c),                              (3.22)


                              f = exp(−(d · c)2 ), or                          (3.23)

                                          e−c
                                     f=                                        (3.24)
                                          e−s
c is the eye-coordinate distance from the eye, (0, 0, 0, 1) in eye coordinates, to the
fragment center. The equation, along with either d or e and s, is specified with

      void Fog{xf}( enum pname, T param );
      void Fog{xf}v( enum pname, T params );

If pname is FOG MODE, then param must be, or params must point to an inte-
ger that is one of the symbolic constants EXP, EXP2, or LINEAR, in which case
equation 3.22, 3.23, or 3.24, respectively, is selected for the fog calculation (if,
when 3.24 is selected, e = s, results are undefined). If pname is FOG DENSITY,
FOG START, or FOG END, then param is or params points to a value that is d, s, or
e, respectively. If d is specified less than zero, the error INVALID VALUE results.
     An implementation may choose to approximate the eye-coordinate distance
from the eye to each fragment center by |ze |. Further, f need not be computed at
each fragment, but may be computed at each vertex and interpolated as other data
are.
     No matter which equation and approximation is used to compute f , the result
is clamped to [0, 1] to obtain the final f .
     If Cr represents a rasterized fragment’s R, G, or B value, then the correspond-
ing value produced by fog is

                              C = f Cr + (1 − f )Cf .

(The rasterized fragment’s A value is not changed by fog blending.) The R, G, B,
and A values of Cf are specified by calling Fog with pname equal to FOG COLOR;
in this case params points to four values comprising Cf . If these are not floating-
point values, then they are converted to floating-point using the conversion given

                          Version 1.1.12 (April 24, 2008)
3.9. ANTIALIASING APPLICATION                                                      98


in table 2.7 for signed integers. Each component of Cf is clamped to [0, 1] when
specified.
     The state required for fog consists of a three-valued integer to select the fog
equation, three floating-point values d, e, and s, an RGBA fog color, and a single
bit to indicate whether or not fog is enabled. In the initial state, fog is disabled,
FOG MODE is EXP, d = 1.0, e = 1.0, and s = 0.0; Cf = (0, 0, 0, 0) and if = 0.


3.9    Antialiasing Application
Finally, if antialiasing is enabled for the primitive from which a rasterized fragment
was produced, then the computed coverage value is applied to the fragment. The
value is multiplied by the fragment’s alpha (A) value to yield a final alpha value.


3.10     Multisample Point Fade
If multisampling is enabled and the rasterized fragment results from a point prim-
itive, then the computed fade factor from equation 3.2 is applied to the fragment.
The fade factor is multiplied by the fragment’s alpha value to yield a final alpha
value.




                          Version 1.1.12 (April 24, 2008)
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
are grouped into several logical buffers. These are the color, depth, and stencil
buffers. The color buffer consists of either or both of a front (single) buffer and
a back buffer. Typically the contents of the front buffer are displayed on a color
monitor while the contents of the back buffer are invisible. The color buffers must
have the same number of bitplanes, although a context may not provide both types
of buffers. Further, an implementation or context may not provide depth or stencil
buffers.
    Color buffers consist of R, G, B, and, optionally, A unsigned integer values.
The number of bitplanes in each of the color buffers, the depth buffer, and the
stencil buffer is fixed and window dependent.
    The initial state of all provided bitplanes is undefined.


4.1    Per-Fragment Operations
A fragment produced by rasterization with window coordinates of (xw , yw ) mod-
ifies the pixel in the framebuffer at that location based on a number of parameters



                                         99
4.1. PER-FRAGMENT OPERATIONS                                                                    100




        Fragment
                             Pixel                                 Multisample
            +                                  Scissor
                           Ownership                                Fragment
        Associated                              Test
                             Test                                  Operations
           Data




                          Depth Buffer          Stencil                 Alpha
                             Test                Test                   Test


                      Framebuffer          Framebuffer




                                                                                      To
                               Blending       Dithering                 Logicop
                                                                                  Framebuffer


                 Framebuffer                              Framebuffer




   Figure 4.1. Per-fragment operations.



and conditions. We describe these modifications and tests, diagrammed in Fig-
ure 4.1, in the order in which they are performed.

4.1.1     Pixel Ownership Test
The first test is to determine if the pixel at location (xw , yw ) in the framebuffer
is currently owned by the GL (more precisely, by this GL context). If it is not,
the window system decides the fate of the incoming fragment. Possible results are
that the fragment is discarded or that some subset of the subsequent per-fragment
operations are applied to the fragment. This test allows the window system to
control the GL’s behavior, for instance, when a GL window is obscured.

4.1.2     Scissor Test
The scissor test determines if (xw , yw ) lies within the scissor rectangle defined by
four values. These values are set with
        void Scissor( int left, int bottom, sizei width,
           sizei height );

                                   Version 1.1.12 (April 24, 2008)
4.1. PER-FRAGMENT OPERATIONS                                                      101


If left ≤ xw < left + width and bottom ≤ yw < bottom + height, then the scissor
test passes. Otherwise, the test fails and the fragment is discarded. The test is
enabled or disabled using Enable or Disable using the constant SCISSOR TEST.
When disabled, it is as if the scissor test always passes. If either width or height
is less than zero, then the error INVALID VALUE is generated. The state required
consists of four integer values and a bit indicating whether the test is enabled or
disabled. In the initial state lef t = bottom = 0; width and height are determined
by the size of the GL window. Initially, the scissor test is disabled.

4.1.3   Multisample Fragment Operations
This step modifies fragment alpha and coverage values based on the values
of SAMPLE ALPHA TO COVERAGE, SAMPLE ALPHA TO ONE, SAMPLE COVERAGE,
SAMPLE COVERAGE VALUE, and SAMPLE COVERAGE INVERT. No changes to the
fragment alpha or coverage values are made at this step if MULTISAMPLE is dis-
abled, or if SAMPLE BUFFERS is not a value of one.
     SAMPLE ALPHA TO COVERAGE,                  SAMPLE ALPHA TO ONE,              and
SAMPLE COVERAGE are enabled and disabled by calling Enable and Disable
with cap specified as one of the three token values. All three values are
queried by calling IsEnabled with cap set to the desired token value. If
SAMPLE ALPHA TO COVERAGE is enabled, a temporary coverage value is gen-
erated where each bit is determined by the alpha value at the corresponding
sample location. The temporary coverage value is then ANDed with the fragment
coverage value. Otherwise the fragment coverage value is unchanged at this point.
     No specific algorithm is required for converting the sample alpha values to a
temporary coverage value. It is intended that the number of 1’s in the temporary
coverage be proportional to the set of alpha values for the fragment, with all 1’s
corresponding to the maximum of all alpha values, and all 0’s corresponding to
all alpha values being 0. It is also intended that the algorithm be pseudo-random
in nature, to avoid image artifacts due to regular coverage sample locations. The
algorithm can and probably should be different at different pixel locations. If it
does differ, it should be defined relative to window, not screen, coordinates, so that
rendering results are invariant with respect to window position.
     Next, if SAMPLE ALPHA TO ONE is enabled, each alpha value is replaced by the
maximum representable alpha value. Otherwise, the alpha values are not changed.
     Finally, if SAMPLE COVERAGE is enabled, the fragment coverage is ANDed
with another temporary coverage.            This temporary coverage is generated
in the same manner as the one described above, but as a function of
the value of SAMPLE COVERAGE VALUE. The function need not be identical,
but it must have the same properties of proportionality and invariance. If


                          Version 1.1.12 (April 24, 2008)
4.1. PER-FRAGMENT OPERATIONS                                                       102


SAMPLE COVERAGE INVERT is TRUE, the temporary coverage is inverted (all bit
values are inverted) before it is ANDed with the fragment coverage.
    The values of SAMPLE COVERAGE VALUE and SAMPLE COVERAGE INVERT
are specified by calling

        void SampleCoverage( clampf value, boolean invert );
        void SampleCoveragex( clampx value, boolean invert );

with value set to the desired coverage value, and invert set to TRUE or FALSE.
value is clamped to [0,1] before being stored as SAMPLE COVERAGE VALUE.
SAMPLE COVERAGE VALUE is queried by calling GetFloatv with pname set to
SAMPLE COVERAGE VALUE. SAMPLE COVERAGE INVERT is queried by calling
GetBooleanv with pname set to SAMPLE COVERAGE INVERT.

4.1.4    Alpha Test
The alpha test discards a fragment conditional on the outcome of a comparison be-
tween the incoming fragment’s alpha value and a constant value. The comparison
is enabled or disabled with the generic Enable and Disable commands using the
symbolic constant ALPHA TEST. When disabled, it is as if the comparison always
passes. The test is controlled with

        void AlphaFunc( enum func, clampf ref );
        void AlphaFuncx( enum func, clampx ref );

func is a symbolic constant indicating the alpha test function; ref is a reference
value. ref is clamped to lie in [0, 1], and then converted to a fixed-point value ac-
cording to the rules given for an A component in section 2.12.8. For purposes
of the alpha test, the fragment’s alpha value is also rounded to the nearest inte-
ger. The possible constants specifying the test function are NEVER, ALWAYS, LESS,
LEQUAL, EQUAL, GEQUAL, GREATER, or NOTEQUAL, meaning pass the fragment
never, always, if the fragment’s alpha value is less than, less than or equal to, equal
to, greater than or equal to, greater than, or not equal to the reference value, respec-
tively.
     The required state consists of the floating-point reference value, an eight-
valued integer indicating the comparison function, and a bit indicating if the com-
parison is enabled or disabled. The initial state is for the reference value to be 0
and the function to be ALWAYS. Initially, the alpha test is disabled.




                           Version 1.1.12 (April 24, 2008)
4.1. PER-FRAGMENT OPERATIONS                                                       103


4.1.5    Stencil Test
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
to zero, replacing with the reference value, incrementing with saturation, decre-
menting with saturation, and bitwise inverting it.
     For purposes of increment and decrement, the stencil bits are considered as an
unsigned integer. Incrementing or decrementing with saturation clamps the stencil
value at 0 and the maximum representable value.
     The same symbolic values are given to indicate the stencil action if the depth
buffer test (below) fails (dpfail), or if it passes (dppass).
     If the stencil test fails, the incoming fragment is discarded. The state required
consists of the most recent values passed to StencilFunc and StencilOp, and a
bit indicating whether stencil testing is enabled or disabled. In the initial state,
stenciling is disabled, the stencil reference value is zero, the stencil comparison
function is ALWAYS, and the stencil mask is all ones. Initially, all three stencil
operations are KEEP. If there is no stencil buffer, no stencil modification can occur,
and it is as if the stencil tests always pass, regardless of any calls to StencilOp.



                           Version 1.1.12 (April 24, 2008)
4.1. PER-FRAGMENT OPERATIONS                                                      104


4.1.6    Depth Buffer Test
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
Blending combines the incoming source fragment’s R, G, B, and A values with
the destination R, G, B, and A values stored in the framebuffer at the fragment’s
(xw , yw ) location.
    Source and destination values are combined according to quadruplets of source
and destination weighting factors determined by the blend function to obtain a new
set of R, G, B, and A values, as described below. Each of these floating-point
values is clamped to [0, 1] and converted back to a fixed-point value in the manner
described in section 2.12.8. The resulting four values are sent to the next operation.


                          Version 1.1.12 (April 24, 2008)
4.1. PER-FRAGMENT OPERATIONS                                                    105


    Blending is dependent on the incoming fragment’s alpha value and that of the
corresponding currently stored pixel. Blending is enabled or disabled using En-
able or Disable with the symbolic constant BLEND. If it is disabled, or if logical
operation on color values is enabled (section 4.1.9), proceed to the next operation.

Blend Equation
Blending is controlled by the equation

                                C = Cs S + Cd D
where C refers to the new color resulting from blending, Cs refers to the source
color for an incoming fragment and Cd refers to the destination color at the corre-
sponding framebuffer location. Individual RGBA components of these colors are
denoted by subscripts of s and d respectively. S and D are quadruplets of weight-
ing factors determined by the blend function described below.
    Destination (framebuffer) components are taken to be fixed-point values rep-
resented according to the scheme given in section 2.12.8 (Final Color Processing),
as are source (fragment) components.
    Prior to blending, each fixed-point color component undergoes an implied con-
version to floating point. This conversion must leave the values 0 and 1 invariant.
Blending computations are treated as if carried out in floating point.
    The blend equation is evaluated separately for each color component and the
corresponding weighting factors.

Blend Functions
The weighting factors used by the blend equation are determined by the blend
function. The blend function is specified with the command

      void BlendFunc( enum src, enum dst );

    BlendFunc argument src determines the source (S) blend factors, and dst
determines the destination (D) blend factors for each color component. The
possible source and destination blend functions and their corresponding com-
puted blend factors are summarized in Table 4.1. The functions DST COLOR,
ONE MINUS DST COLOR, and SRC ALPHA SATURATE are valid only for src, and
the functions SRC COLOR and ONE MINUS SRC COLOR are valid only for dst. All
other functions are valid for either src or dst.




                         Version 1.1.12 (April 24, 2008)
4.1. PER-FRAGMENT OPERATIONS                                                        106


         Function                    Blend Factors
                                     (Sr , Sg , Sb , Sa ) or (Dr , Dg , Db , Da )
         ZERO                        (0, 0, 0, 0)
         ONE                         (1, 1, 1, 1)
         SRC COLOR                   (Rs , Gs , Bs , As )
         ONE MINUS    SRC COLOR      (1, 1, 1, 1) − (Rs , Gs , Bs , As )
         DST COLOR                   (Rd , Gd , Bd , Ad )
         ONE MINUS    DST COLOR      (1, 1, 1, 1) − (Rd , Gd , Bd , Ad )
         SRC ALPHA                   (As , As , As , As )
         ONE MINUS    SRC ALPHA      (1, 1, 1, 1) − (As , As , As , As )
         DST ALPHA                   (Ad , Ad , Ad , Ad )
         ONE MINUS    DST ALPHA      (1, 1, 1, 1) − (Ad , Ad , Ad , Ad )
         SRC ALPHA    SATURATE       (f, f, f, 1)1

Table 4.1: RGB and ALPHA source and destination blending functions and the cor-
responding blend factors. Addition and subtraction is performed component-wise.
1 f = min(A , 1 − A ).
             s       d




Blending State
The state required for blending is two integers indicating the source and destination
blending and a bit indicating whether blending is enabled or disabled. The initial
blending functions are ONE for the source functions and ZERO for the destination
functions. Initially, blending is disabled.
    Blending uses the color buffer selected for writing (see section 4.2.1) using that
buffer’s color for Cd . If a color buffer has no A value, then Ad is taken to be 1.

4.1.8   Dithering
Dithering selects between two color values. Consider the value of any of the color
components as a fixed-point value with m bits to the left of the binary point, where
m is the number of bits allocated to that component in the framebuffer; call each
such value c. For each c, dithering selects a value c1 such that c1 ∈ {max{0, c −
1}, c } (after this selection, treat c1 as a fixed point value in [0,1] with m bits).
This selection may depend on the xw and yw coordinates of the pixel. c must not
be larger than the maximum value representable in the framebuffer for either the
component or the index, as appropriate.
    Many dithering algorithms are possible, but a dithered value produced by any
algorithm must depend only the incoming value and the fragment’s x and y window


                          Version 1.1.12 (April 24, 2008)
4.1. PER-FRAGMENT OPERATIONS                                                       107


coordinates. If dithering is disabled, then each color component is truncated to a
fixed-point value with as many bits as there are in the corresponding component in
the framebuffer.
    Dithering is enabled with Enable and disabled with Disable using the symbolic
constant DITHER. The state required is thus a single bit. Initially, dithering is
enabled.

4.1.9    Logical Operation
Finally, a logical operation is applied between the incoming fragment’s color and
the color stored at the corresponding location in the framebuffer. The result re-
places the values in the framebuffer at the fragment’s (xw , yw ) coordinates. Logical
operation on color values is enabled or disabled with Enable or Disable using the
symbolic constant COLOR LOGIC OP. If the logical operation is enabled for color
values, it is as if blending were disabled, regardless of the value of BLEND.
    The logical operation is selected by

        void LogicOp( enum op );

op is a symbolic constant; the possible constants and corresponding operations are
enumerated in Table 4.2. In this table, s is the value of the incoming fragment and
d is the value stored in the framebuffer.
    Logical operations are performed independently for each red, green, blue, and
alpha value of each color buffer that is selected for writing. The required state is an
integer indicating the logical operation, and two bits indicating whether the logical
operation is enabled or disabled. The initial state is for the logic operation to be
given by COPY, and to be disabled.

4.1.10    Additional Multisample Fragment Operations
If MULTISAMPLE is enabled, and the value of SAMPLE BUFFERS is one, the alpha
test, stencil test, depth test, blending, and dithering operations are performed for
each pixel sample, rather than just once for each fragment. Failure of the alpha,
stencil, or depth test results in termination of the processing of that sample, rather
than discarding of the fragment. All operations are performed on the color, depth,
and stencil values stored in the multisample buffer (to be described in a following
section). The contents of the color buffer are not modified at this point.
     Stencil, depth, blending, and dithering operations are performed for a pixel
sample only if that sample’s fragment coverage bit is a value of 1. If the corre-
sponding coverage bit is 0, no operations are performed for that sample.


                          Version 1.1.12 (April 24, 2008)
4.1. PER-FRAGMENT OPERATIONS                                                       108


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

      Table 4.2: Arguments to LogicOp and their corresponding operations.



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
ten into the color buffer selected for writing (see section 4.2.1). An implementa-
tion may defer the writing of the color buffer until a later time, but the state of the
framebuffer must behave as if the color buffer was updated as each fragment was
processed. The method of combination is not specified, though a simple average
computed independently for each color component is recommended.



                          Version 1.1.12 (April 24, 2008)
4.2. WHOLE FRAMEBUFFER OPERATIONS                                                  109


4.2     Whole Framebuffer Operations
The preceding sections described the operations that occur as individual fragments
are sent to the framebuffer. This section describes operations that control or affect
the whole framebuffer.

4.2.1    Selecting a Buffer for Writing
Color values are written into the front buffer for single buffered contexts, or into
the back buffer for back buffered contexts. The type of context is determined when
creating a GL context.

4.2.2    Fine Control of Buffer Updates
Four commands are used to mask the writing of bits to each of the logical frame-
buffers after all per-fragment operations have been performed. The command

        void ColorMask( boolean r, boolean g, boolean b,
           boolean a );

controls the writing of R, G, B and A values to the color buffer. r, g, b, and a
indicate whether R, G, B, or A values, respectively, are written or not (a value of
TRUE means that the corresponding value is written). In the initial state, all color
values are enabled for writing.
    The depth buffer can be enabled or disabled for writing zw values using

        void DepthMask( boolean mask );

If mask is non-zero, the depth buffer is enabled for writing; otherwise, it is disabled.
In the initial state, the depth buffer is enabled for writing.
    The command

        void StencilMask( uint mask );

controls the writing of particular bits into the stencil planes. The least significant s
bits of mask comprise an integer mask (s is the number of bits in the stencil buffer).
The initial state is for the stencil plane mask to be all ones.
     The state required for the masking operations is an integer for stencil values
and a bit for depth values. A set of four bits is also required indicating which color
components of an RGBA value should be written. In the initial state, the stencil
mask is all ones, as are the bits controlling depth value and RGBA component
writing.

                           Version 1.1.12 (April 24, 2008)
4.2. WHOLE FRAMEBUFFER OPERATIONS                                                  110


Fine Control of Multisample Buffer Updates
When the value of SAMPLE BUFFERS is one, ColorMask, DepthMask, and Sten-
cilMask control the modification of values in the multisample buffer. The color
mask has no effect on modifications to the color buffer. If the color mask is entirely
disabled, the color sample values must still be combined (as described above) and
the result used to replace values of the color buffer.

4.2.3    Clearing the Buffers
The GL provides a means for setting portions of every pixel in a particular buffer
to the same value. The argument to

        void Clear( bitfield buf );

is the bitwise OR of a number of values indicating which buffers are to
be cleared. The values are COLOR BUFFER BIT, DEPTH BUFFER BIT, and
STENCIL BUFFER BIT, indicating the color buffer, the depth buffer, and the sten-
cil buffer, respectively. The value to which each buffer is cleared depends on the
setting of the clear value for that buffer. If the mask is not a bitwise OR of the
specified values, then the error INVALID VALUE is generated.

        void ClearColor( clampf r, clampf g, clampf b,
           clampf a );
        void ClearColorx( clampx r, clampx g, clampx b,
           clampx a );

sets the clear value for the color buffer. Each of the specified components is
clamped to [0, 1] and converted to fixed-point according to the rules of sec-
tion 2.12.8.

        void ClearDepthf( clampf d );
        void ClearDepthx( clampx d );

takes a value that is clamped to the range [0, 1] and converted to fixed-point accord-
ing to the rules for a window z value given in section 2.10.1. Similarly,

        void ClearStencil( int s );

takes a single integer argument that is the value to which to clear the stencil buffer.
s is masked to the number of bitplanes in the stencil buffer.


                          Version 1.1.12 (April 24, 2008)
4.3. READING PIXELS                                                                111


    When Clear is called, the only per-fragment operations that are applied (if
enabled) are the pixel ownership test, the scissor test, and dithering. The masking
operations described in the last section (4.2.2) are also effective. If a buffer is not
present, then a Clear directed at that buffer has no effect.
    The state required for clearing is a clear value for each of the color buffer,
the depth buffer, and the stencil buffer. Initially, the RGBA color clear value is
(0,0,0,0), the stencil buffer clear value is 0, and the depth buffer clear value is 1.0.

Clearing the Multisample Buffer
The color samples of the multisample buffer are cleared when the color buffer is
cleared, as specified by the Clear mask bit COLOR BUFFER BIT.
    If the Clear mask bits DEPTH BUFFER BIT or STENCIL BUFFER BIT are set,
then the corresponding depth or stencil samples, respectively, are cleared.


4.3     Reading Pixels
Pixels may be read from the framebuffer to client memory using the ReadPixels
commands, as described below. Pixels may also be copied from client memory or
the framebuffer to texture images in the GL using the TexImage2D and CopyTex-
Image2D commands, as described in section 3.7.1.

4.3.1    Reading Pixels
The method for reading pixels from the framebuffer and placing them in client
memory is diagrammed in Figure 4.2. We describe the stages of the pixel reading
process in the order in which they occur.
   Pixels are read using

        void ReadPixels( int x, int y, sizei width, sizei height,
           enum format, enum type, void *data );

The arguments after x and y to ReadPixels are those described in section 3.6.2
defining pixel rectangles. Only two combinations of format and type are ac-
cepted. The first is format RGBA and type UNSIGNED BYTE. The second is an
implementation-chosen format from among those defined in table 3.4. The val-
ues of format and type for this format may be determined by calling GetIntegerv
with the symbolic constants IMPLEMENTATION COLOR READ FORMAT OES and
IMPLEMENTATION COLOR READ TYPE OES, respectively. The implementation-
chosen format may vary depending on the format of the currently bound rendering


                           Version 1.1.12 (April 24, 2008)
4.3. READING PIXELS                                                                  112




         RGBA pixel data in


                              Convert to float



                                                   Pixel Storage
                              Clamp to [0,1]
                                                    Operations

                                      Pack


            byte, short, or packed
        pixel component data stream




   Figure 4.2. Operation of ReadPixels. Operations in dashed boxes may be enabled
   or disabled.



            Parameter Name                Type     Initial Value   Valid Range
            PACK ALIGNMENT               integer         4           1,2,4,8

            Table 4.3: PixelStore parameters pertaining to ReadPixels.



surface. The pixel storage modes that apply to ReadPixels are summarized in
Table 4.3.

Obtaining Pixels from the Framebuffer
The buffer from which values are obtained is the color buffer used for writing (see
section 4.2.1).
    ReadPixels obtains values from the color buffer (with lower left hand corner
at (0, 0)) for each pixel (x + i, y + j) for 0 ≤ i < width and 0 ≤ j < height;
this pixel is said to be the ith pixel in the jth row. If any of these pixels lies outside
of the window allocated to the current GL context, the values obtained for those
pixels are undefined. Results are also undefined for individual pixels that are not
owned by the current context. Otherwise, ReadPixels obtains values from the color


                              Version 1.1.12 (April 24, 2008)
4.3. READING PIXELS                                                              113


       type Parameter                 GL Data Type      Component
                                                        Conversion Formula
       UNSIGNED    BYTE                   ubyte         c = (28 − 1)f
       UNSIGNED    SHORT 5 6 5           ushort         c = (2N − 1)f
       UNSIGNED    SHORT 4 4 4 4         ushort         c = (2N − 1)f
       UNSIGNED    SHORT 5 5 5 1         ushort         c = (2N − 1)f

Table 4.4: Reversed component conversions, used when component data are be-
ing returned to client memory. Color components are converted from the internal
floating-point representation (f ) to a datum of the specified GL data type (c) using
the specified equation. All arithmetic is done in the internal floating point format.
These conversions apply to component data returned by GL query commands and
to components of pixel data returned to client memory. The equations remain the
same even if the implemented ranges of the GL data types are greater than the
minimum required ranges. (See Table 2.2.) Equations with N as the exponent are
performed for each bitfield of the packed data type, with N set to the number of
bits in the bitfield.


buffer, regardless of how those values were placed there.
    If format is RGBA, then red, green, blue, and alpha values are obtained from
the selected buffer at each pixel location. If the framebuffer does not support alpha
values then the A that is obtained is 1.0.

Conversion of RGBA values
The R, G, B, and A values form a group of elements. Each element is taken to
be a fixed-point value in [0, 1] with m bits, where m is the number of bits in the
corresponding color component of the selected buffer (see section 2.12.8).

Final Conversion
Each component is first clamped to [0, 1]. Then the appropriate conversion formula
from table 4.4 is applied to the component.

Placement in Client Memory
Groups of elements are placed in memory just as they are taken from memory for
TexImage2D. That is, the ith group of the jth row (corresponding to the ith pixel
in the jth row) is placed in memory just where the ith group of the jth row would


                          Version 1.1.12 (April 24, 2008)
4.3. READING PIXELS                                                             114


be taken from for TexImage2D. See Unpacking under section 3.6.2. The only
difference is that the storage mode parameters whose names begin with PACK are
used instead of those whose names begin with UNPACK . If format is ALPHA or
LUMINANCE, only the corresponding single element is written. Likewise if format
is LUMINANCE ALPHA or RGB, only the corresponding two or three elements are
written. Otherwise all the elements of each group are written.

4.3.2   Pixel Draw/Read State
The state required for pixel operations consists of the parameters that are set with
PixelStore. This state has been summarized in tables 3.1. State set with PixelStore
is GL client state.




                         Version 1.1.12 (April 24, 2008)
Chapter 5

Special Functions

This chapter describes additional GL functionality that does not fit easily into any
of the preceding chapters: flushing and finishing (used to synchronize the GL com-
mand stream), and hints.


5.1    Flush and Finish
The command

      void Flush( void );

indicates that all commands that have previously been sent to the GL must complete
in finite time.
     The command

      void Finish( void );

forces all previous GL commands to complete. Finish does not return until all
effects from previously issued commands on GL client and server state and the
framebuffer are fully realized.


5.2    Hints
Certain aspects of GL behavior, when there is room for variation, may be controlled
with hints. A hint is specified using

      void Hint( enum target, enum hint );


                                        115
5.2. HINTS                                                                       116


target is a symbolic constant indicating the behavior to be controlled, and hint is a
symbolic constant indicating what type of behavior is desired. target may be one
of PERSPECTIVE CORRECTION HINT, indicating the desired quality of parame-
ter interpolation; POINT SMOOTH HINT, indicating the desired sampling quality
of points; LINE SMOOTH HINT, indicating the desired sampling quality of lines;
FOG HINT, indicating whether fog calculations are done per pixel or per vertex;
and GENERATE MIPMAP HINT, indicating the desired quality and performance of
automatic mipmap level generation. hint must be one of FASTEST, indicating that
the most efficient option should be chosen; NICEST, indicating that the highest
quality option should be chosen; and DONT CARE, indicating no preference in the
matter.
    The interpretation of hints is implementation dependent. An implementation
may ignore them entirely.
    The initial value of all hints is DONT CARE.




                          Version 1.1.12 (April 24, 2008)
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
        void   GetFixedv( enum value, fixed *data );
        void   GetFloatv( enum value, float *data );

The commands obtain boolean, integer, fixed-point, or floating-point state vari-
ables. value is a symbolic constant indicating the state variable to return. data is a
pointer to a scalar or array of the indicated type in which to place the returned data.
In addition

        boolean IsEnabled( enum value );

can be used to determine if value is currently enabled (as with Enable) or disabled.




                                         117
6.1. QUERYING GL STATE                                                                           118


6.1.2     Data Conversions
If a Get command is issued that returns value types different from the type of the
value being obtained, a type conversion is performed.
     If GetBooleanv is called, a floating-point, fixed-point, or integer value converts
to FALSE if and only if it is zero (otherwise it converts to TRUE).
     If GetIntegerv (or any of the Get commands below) is called, a boolean
value is interpreted as either 1 or 0, and a floating-point or fixed-point value
is rounded to the nearest integer, unless the value is an RGBA color compo-
nent, a DepthRange value, a depth buffer clear value, or a normal coordi-
nate. In these cases, the Get command converts the floating-point or fixed-
point value to an integer according the INT entry of Table 4.4; a value not in
[−1, 1] converts to an undefined value. Additionally, if the target of GetInte-
gerv is one of the special values MODELVIEW MATRIX FLOAT AS INT BITS OES,
PROJECTION MATRIX FLOAT AS INT BITS OES,
or TEXTURE MATRIX FLOAT AS INT BITS OES, then the corresponding floating-
point matrix elements are returned in an array of integers, according to the IEEE
754 floating point “single format” bit layout1 2 .
     If GetFixedv is called, a boolean value is interpreted as either 1.0 or 0.0. Inte-
ger values are converted to fixed-point by multiplying by 216 , as described in sec-
tion 2.3. Enumerated values are converted to fixed-point without scaling. Floating-
point values are multiplied by 216 , converted to an integer representation, and then
converted to fixed-point without further scaling, to preserve fractional parts of such
values.
     If GetFloatv is called, a boolean value is interpreted as either 1.0 or 0.0, and
an integer, enumerated, or fixed-point value is coerced to floating-point.
     If a value is so large in magnitude that it cannot be represented with the re-
quested type, then the nearest value representable using the requested type is re-
turned.
     Unless otherwise indicated, multi-valued state variables return their multiple
values in the same order as they are given as arguments to the commands that set
them. For instance, the two DepthRange parameters are returned in the order n
followed by f.
     Most texture state variables are qualified by the value of ACTIVE TEXTURE
   1
      This functionality exists for applications using the Common-Lite profile which nonetheless
need access to the full accuracy of the internal matrix representation, but is available in the Common
profile as well.
   2
       IEEE 1987.       IEEE Standard 754-1985 for Binary Floating-Point Arithmetic, IEEE.
Reprinted in SIGPLAN 22, 2, 9-25.              Also see the IEEE 754 Working Group Page at
http://grouper.ieee.org/groups/754/.



                               Version 1.1.12 (April 24, 2008)
6.1. QUERYING GL STATE                                                         119


to determine which server texture state vector is queried. Client texture
state variables such as texture coordinate array pointers are qualified by the
value of CLIENT ACTIVE TEXTURE. Tables 6.3, 6.4, 6.7, 6.13, 6.15, and 6.21
indicate those state variables which are qualified by ACTIVE TEXTURE or
CLIENT ACTIVE TEXTURE during state queries.


6.1.3    Enumerated Queries
Other commands exist to obtain state variables that are identified by a category
(clip plane, light, material, etc.) as well as a symbolic constant. These are

        void GetClipPlane{xf}( enum plane, T eqn[4] );
        void GetLight{xf}v( enum light, enum value, T data );
        void GetMaterial{xf}v( enum face, enum value, T data );
        void GetTexEnv{ixf}v( enum env, enum value, T data );
        void GetTexParameter{ixf}v( enum target, enum value,
           T data );
        void GetBufferParameteriv( enum target, enum value,
           T data );

GetClipPlane always returns four values in eqn; these are the coefficients of the
plane equation of plane in eye coordinates (these coordinates are those that were
computed when the plane was specified).
    GetLight places information about value (a symbolic constant) for light (also a
symbolic constant) in data. POSITION or SPOT DIRECTION returns values in eye
coordinates (again, these are the coordinates that were computed when the position
or direction was specified).
    GetMaterial, GetTexEnv, GetTexParameter, and GetBufferParameter are
similar to GetLight, placing information about value for the target indicated by
their first argument into data. The face argument to GetMaterial must be either
FRONT or BACK, indicating the front or back material, respectively. The env argu-
ment to GetTexEnv must be TEXTURE ENV.
    GetTexParameter parameter target must be TEXTURE 2D, indicating the cur-
rently bound texture object. value is a symbolic value indicating which texture
parameter is to be obtained. For GetTexParameter, value must be one of the
symbolic values in table 3.13.

6.1.4    Texture Queries
The command


                         Version 1.1.12 (April 24, 2008)
6.1. QUERYING GL STATE                                                              120


        boolean IsTexture( uint texture );
returns TRUE if texture is the name of a texture object. If texture is zero, or is a non-
zero value that is not the name of a texture object, or if an error condition occurs,
IsTexture returns FALSE. A name returned by GenTextures, but not yet bound, is
not the name of a texture object.

6.1.5    Pointer and String Queries
The command
        void GetPointerv( enum pname, void **params );
    obtains the pointer or pointers named pname in the array params. The possible
values for pname are VERTEX ARRAY POINTER, NORMAL ARRAY POINTER,
COLOR ARRAY POINTER,                TEXTURE COORD ARRAY POINTER,             and
POINT SIZE ARRAY POINTER OES. Each returns a single pointer value.
    Finally,
        ubyte *GetString( enum name );
returns a pointer to a static string describing some aspect of the current GL con-
nection. The possible values for name are VENDOR, RENDERER, VERSION, and
EXTENSIONS. The format of the RENDERER and VENDOR strings is implementation
dependent. The EXTENSIONS string contains a space separated list of extension
names (the extension names themselves do not contain any spaces); the VERSION
string has the format
     "OpenGL ES-XX N.M"
     where XX is a two-character profile identifier, either CM for the Common profile
or CL for the Common-List profile, and N.M are the major and minor version num-
bers of the OpenGL ES implementation, separated by a period (currently 1.1).
     GetString returns the version number (returned in the VERSION string) and
the extension names (returned in the EXTENSIONS string) that can be supported
on the connection. Thus, if the client and server support different versions and/or
extensions, a compatible version and list of extensions is returned.

6.1.6    Buffer Object Queries
The command
        boolean IsBuffer( uint buffer );
returns TRUE if buffer is the name of an buffer object. If buffer is zero, or if buffer
is a non-zero value that is not the name of an buffer object, IsBuffer return FALSE.

                           Version 1.1.12 (April 24, 2008)
6.2. STATE TABLES                                                                  121


6.2    State Tables
The tables on the following pages indicate which state variables are obtained with
what commands. State variables that can be obtained using any of GetBooleanv,
GetIntegerv, GetFixedv, or GetFloatv are listed with just one of these commands
– the one that is most appropriate given the type of the data to be returned. These
state variables cannot be obtained using IsEnabled. However, state variables for
which IsEnabled is listed as the query command can also be obtained using Get-
Booleanv, GetIntegerv, GetFixedv, and GetFloatv. State variables for which any
other command is listed as the query command can be obtained only by using that
command.
     In the Common-Lite profile, GetFixedv should be used wherever GetFloatv is
listed in the state tables.
     State table entries which are required only by optional extensions are type-
set against a gray background .
     A type is also indicated for each variable. Table 6.1 explains these types. The
type actually identifies all state associated with the indicated description; in certain
cases only a portion of this state is returned. This is the case with all matrices,
where only the top entry on the stack is returned; with clip planes, where only the
selected clip plane is returned, with parameters describing lights, where only the
value pertaining to the selected light is returned; and with textures, where only the
selected texture or texture parameter is returned.




                           Version 1.1.12 (April 24, 2008)
6.2. STATE TABLES                                                         122




       Type code    Explanation
          B         Boolean
        BM U        Basic machine units
          C         Color (floating-point R, G, B, and A values)
          T         Texture coordinates (floating-point s, t, r, q val-
                    ues)
          N         Normal coordinates (floating-point x, y, z values)
          V         Vertex, including associated data
          Z         Integer
          Z+        Non-negative integer
       Zk , Zk∗     k-valued integer (k∗ indicates k is minimum)
          R         Floating-point number
          R+        Non-negative floating-point number
         R[a,b]     Floating-point number in the range [a, b]
          Rk        k-tuple of floating-point numbers
          Rk        k-valued floating-point number
          P         Position (x, y, z, w floating-point coordinates)
          D         Direction (x, y, z floating-point coordinates)
         M4         4 × 4 floating-point matrix
           I        Image
          Y         Pointer (data type unspecified)
       n × type     n copies of type type (n∗ indicates n is minimum)


                       Table 6.1: State variable types




                      Version 1.1.12 (April 24, 2008)
                                                                                                                                                                                                             6.2. STATE TABLES




                                                                                                                                Get    Initial
                                                                                                             Get value   Type   Cmnd   Value                   Description               Sec.    Attribute
                                                                                                             –            V       –      –       Previous vertex in a line segment       2.6.1       –
                                                                                                             –            B       –      –       Indicates if line-vertex is the first   2.6.1       –
                                                                                                             –            V       –      –       First vertex of a line loop             2.6.1       –
                                                                                                             –           2×V      –      –       Previous two vertices in a triangle     2.6.1       –
                                                                                                                                                 strip
                                                                                                             –            Z3     –       –       Number of vertices so far in            2.6.1      –
                                                                                                                                                 triangle strip: 0, 1, or more
                                                                                                             –            Z2     –       –       Triangle strip A/B vertex pointer       2.6.1      –




Version 1.1.12 (April 24, 2008)
                                  Table 6.2. GL Internal primitive assembly state variables (inaccessible)
                                                                                                                                                                                                             123
                                                                                                                                                                                                      6.2. STATE TABLES




                                                                                                                       Get         Initial
                                                                                       Get value            Type       Cmnd        Value                 Description               Sec.   Attribute
                                                                                                                    GetIntegerv,
                                                                                  CURRENT COLOR               C     GetFloatv      1,1,1,1   Current color                         2.7    current
                                                                                  CURRENT TEXTURE COORDS   2 ∗ ×T    GetFloatv     0,0,0,1   Current texture coordinates           2.7    current
                                                                                  CURRENT NORMAL              N      GetFloatv      0,0,1    Current normal                        2.7    current
                                                                                  –                           C          –            -      Color associated with last vertex     2.6       –
                                                                                  –                           T          –            -      Texture coordinates associated with   2.6       –
                                                                                                                                             last vertex




Version 1.1.12 (April 24, 2008)
                                  Table 6.3. Current Values and Associated Data
                                                                                                                                                                                                      124
                                                                                                   Get          Initial
                                                                      Get value          Type      Cmnd         Value                  Description              Sec.    Attribute
                                                                                                                                                                                      6.2. STATE TABLES




                                                                 CLIENT ACTIVE TEXTURE   Z2∗    GetIntegerv   TEXTURE0    Client active texture unit selector   2.7    vertex-array
                                                                 VERTEX ARRAY             B      IsEnabled      False     Vertex array enable                   2.8    vertex-array
                                                                 VERTEX ARRAY SIZE       Z+     GetIntegerv       4       Coordinates per vertex                2.8    vertex-array
                                                                 VERTEX ARRAY TYPE        Z4    GetIntegerv    FLOAT      Type of vertex coordinates            2.8    vertex-array
                                                                 VERTEX ARRAY STRIDE     Z+     GetIntegerv       0       Stride between vertices               2.8    vertex-array
                                                                 VERTEX ARRAY POINTER     Y     GetPointerv       0       Pointer to the vertex array           2.8    vertex-array
                                                                 NORMAL ARRAY             B      IsEnabled      False     Normal array enable                   2.8    vertex-array
                                                                 NORMAL ARRAY TYPE        Z5    GetIntegerv    FLOAT      Type of normal coordinates            2.8    vertex-array
                                                                 NORMAL ARRAY STRIDE     Z+     GetIntegerv       0       Stride between normals                2.8    vertex-array
                                                                 NORMAL ARRAY POINTER     Y     GetPointerv       0       Pointer to the normal array           2.8    vertex-array
                                                                 COLOR ARRAY              B      IsEnabled      False     Color array enable                    2.8    vertex-array
                                                                 COLOR ARRAY SIZE        Z+     GetIntegerv       4       Color components per vertex           2.8    vertex-array




                                  Table 6.4. Vertex Array Data




Version 1.1.12 (April 24, 2008)
                                                                 COLOR ARRAY TYPE         Z8    GetIntegerv    FLOAT      Type of color components              2.8    vertex-array
                                                                 COLOR ARRAY STRIDE      Z+     GetIntegerv       0       Stride between colors                 2.8    vertex-array
                                                                 COLOR ARRAY POINTER      Y     GetPointerv       0       Pointer to the color array            2.8    vertex-array
                                                                                                                                                                                      125
                                                                                                                             Get         Initial
                                                                                     Get value                   Type        Cmnd        Value                  Description             Sec.     Attribute
                                                                         TEXTURE COORD ARRAY                    2 ∗ ×B     IsEnabled     False     Texture coordinate array enable      2.8     vertex-array
                                                                                                                                                                                                               6.2. STATE TABLES




                                                                         TEXTURE COORD ARRAY SIZE              2 ∗ ×Z +   GetIntegerv      4       Coordinates per element              2.8     vertex-array
                                                                         TEXTURE COORD ARRAY TYPE              2 ∗ ×Z4    GetIntegerv   FLOAT      Type of texture coordinates          2.8     vertex-array
                                                                         TEXTURE COORD ARRAY STRIDE            2 ∗ ×Z +   GetIntegerv      0       Stride between texture coordinates   2.8     vertex-array
                                                                         TEXTURE COORD ARRAY POINTER            2 ∗ ×Y    GetPointerv      0       Pointer to the texture coordinate    2.8     vertex-array
                                                                                                                                                   array
                                                                         POINT SIZE ARRAY OES                      B       IsEnabled     False     Point size array enable               2.8    vertex-array
                                                                         POINT SIZE ARRAY TYPE OES                Z2      GetIntegerv   FLOAT      Type of point sizes                   2.8    vertex-array
                                                                         POINT SIZE ARRAY STRIDE OES              Z+      GetIntegerv      0       Stride between point sizes            2.8    vertex-array
                                                                         POINT SIZE ARRAY POINTER OES              Y      GetPointerv      0       Pointer to the point size array       2.8    vertex-array
                                                                         ARRAY BUFFER BINDING                     Z+      GetIntegerv      0       current buffer binding                2.9    vertex-array
                                                                         VERTEX ARRAY BUFFER BINDING              Z+      GetIntegerv      0       vertex array buffer binding           2.9    vertex-array
                                                                         NORMAL ARRAY BUFFER BINDING              Z+      GetIntegerv      0       normal array buffer binding           2.9    vertex-array




Version 1.1.12 (April 24, 2008)
                                                                         COLOR ARRAY BUFFER BINDING               Z+      GetIntegerv      0       color array buffer binding            2.9    vertex-array




                                  Table 6.5. Vertex Array Data (cont.)
                                                                         TEXTURE COORD ARRAY BUFFER BINDING    2 ∗ ×Z +   GetIntegerv      0       texcoord array buffer binding         2.9    vertex-array
                                                                         POINT SIZE ARRAY BUFFER BINDING OES      Z+      GetIntegerv      0       point size array buffer binding       2.9    vertex-array
                                                                         ELEMENT ARRAY BUFFER BINDING             Z+      GetIntegerv      0       element array buffer binding         2.9.2   vertex-array
                                                                                                                                                                                                               126
                                                                                                                                                                                6.2. STATE TABLES




                                                                                                    Get                 Initial
                                                                   Get value         Type           Cmnd                Value                  Description   Sec.   Attribute
                                                                                  n × BM U            –                    -      buffer data                2.9        -
                                                                   BUFFER SIZE     n × Z+    GetBufferParameteriv         0       buffer data size           2.9        -
                                                                   BUFFER USAGE     n × Z9   GetBufferParameteriv   STATIC DRAW   buffer usage pattern       2.9        -




Version 1.1.12 (April 24, 2008)
                                  Table 6.6. Buffer Object State
                                                                                                                                                                                127
                                                                                          Get             Initial
                                                 Get value                   Type         Cmnd            Value             Description          Sec.       Attribute
                                   MODELVIEW MATRIX                       16 ∗ ×M 4      GetFloatv       Identity    Model-view matrix stack    2.10.2          –
                                   PROJECTION MATRIX                       2 ∗ ×M 4      GetFloatv       Identity    Projection matrix stack    2.10.2          –
                                   TEXTURE MATRIX                       2 ∗ ×2 ∗ ×M 4    GetFloatv       Identity    Texture matrix stack       2.10.2          –
                                   MODELVIEW MATRIX FLOAT AS INT BITS OES 4 × 4 × Z     GetIntegerv      Identity    Alias of                   2.10.2          –
                                                                                                                     MODELVIEW MATRIX
                                                                                                                     in integer encoding
                                                                                                                                                                            6.2. STATE TABLES




                                   PROJECTION MATRIX FLOAT AS INT BITS OES   4×4×Z      GetIntegerv      Identity    Alias of                   2.10.2          –
                                                                                                                     PROJECTION MATRIX
                                                                                                                     in integer encoding




Table
                                   TEXTURE MATRIX FLOAT AS INT BITS OES      4×4×Z      GetIntegerv      Identity    Alias of                   2.10.2          –
                                                                                                                     TEXTURE MATRIX in
                                                                                                                     integer encoding
                                   VIEWPORT                                   4×Z       GetIntegerv     see 2.10.1   Viewport origin & extent   2.10.1      viewport
                                   DEPTH RANGE                               2 × R+      GetFloatv         0,1       Depth range near & far     2.10.1      viewport
                                   MODELVIEW STACK DEPTH                       Z+       GetIntegerv         1        Model-view matrix stack    2.10.2         –
                                                                                                                     pointer
                                   PROJECTION STACK DEPTH                      Z+       GetIntegerv         1        Projection matrix stack    2.10.2          –
                                                                                                                     pointer




 Version 1.1.12 (April 24, 2008)
                                   TEXTURE STACK DEPTH                       2 ∗ ×Z +   GetIntegerv         1        Texture matrix stack       2.10.2          –




      6.7. Transformation state
                                                                                                                     pointer
                                   MATRIX MODE                                 Z4       GetIntegerv    MODELVIEW     Current matrix mode        2.10.2       transform
                                   NORMALIZE                                   B         IsEnabled        False      Current normal             2.10.3   transform/enable
                                                                                                                     normalization on/off
                                   RESCALE NORMAL                               B        IsEnabled        False      Current normal rescaling   2.10.3   transform/enable
                                                                                                                     on/off
                                   CLIP PLANEi                               1 ∗ ×R4    GetClipPlane     0,0,0,0     User clipping plane        2.11        transform
                                                                                                                     coefficients
                                   CLIP PLANEi
                                                                                                                                                                            128




                                                                             1 ∗ ×B      IsEnabled        False      ith user clipping plane    2.11     transform/enable
                                                                                                                     enabled
                                                                                                                                                      6.2. STATE TABLES




                                                                                Get         Initial
                                                        Get value     Type      Cmnd        Value                Description     Sec.     Attribute
                                                        FOG COLOR      C      GetFloatv     0,0,0,0   Fog color                  3.8         fog
                                                        FOG DENSITY    R      GetFloatv       1.0     Exponential fog density    3.8         fog
                                                        FOG START      R      GetFloatv       0.0     Linear fog start           3.8         fog
                                                        FOG END        R      GetFloatv       1.0     Linear fog end             3.8         fog
                                                        FOG MODE       Z3    GetIntegerv     EXP      Fog mode                   3.8         fog
                                                        FOG            B      IsEnabled      False    True if fog enabled        3.8     fog/enable




                                  Table 6.8. Coloring
                                                        SHADE MODEL   Z+     GetIntegerv   SMOOTH     ShadeModel setting        2.12.6    lighting




Version 1.1.12 (April 24, 2008)
                                                                                                                                                      129
                                                                                                                           Get               Initial
                                                                                               Get value         Type      Cmnd              Value              Description        Sec.       Attribute
                                                                                          LIGHTING                B      IsEnabled           False          True if lighting is   2.12.1   lighting/enable
                                                                                                                                                            enabled
                                                                                                                                                                                                             6.2. STATE TABLES




                                                                                          COLOR MATERIAL          B      IsEnabled           False          True if color         2.12.3   lighting/enable
                                                                                                                                                            tracking is
                                                                                                                                                            enabled
                                                                                          AMBIENT                2×C    GetMaterialfv   (0.2,0.2,0.2,1.0)   Ambient material      2.12.1      lighting
                                                                                                                                                            color
                                                                                          DIFFUSE                2×C    GetMaterialfv   (0.8,0.8,0.8,1.0)   Diffuse material      2.12.1      lighting
                                                                                                                                                            color
                                                                                          SPECULAR               2×C    GetMaterialfv   (0.0,0.0,0.0,1.0)   Specular material     2.12.1      lighting
                                                                                                                                                            color
                                                                                          EMISSION               2×C    GetMaterialfv   (0.0,0.0,0.0,1.0)   Emissive mat.         2.12.1      lighting
                                                                                                                                                            color
                                                                                          SHININESS              2×R    GetMaterialfv         0.0           Specular              2.12.1      lighting




Version 1.1.12 (April 24, 2008)
                                                                                                                                                            exponent of
                                                                                                                                                            material
                                                                                          LIGHT MODEL AMBIENT     C      GetFloatv      (0.2,0.2,0.2,1.0)   Ambient scene         2.12.1      lighting
                                                                                                                                                            color
                                                                                          LIGHT MODEL TWO SIDE    B     GetBooleanv          False          Use two-sided         2.12.1      lighting




                                  Table 6.9. Lighting (see also Table 2.8 for defaults)
                                                                                                                                                            lighting
                                                                                                                                                                                                             130
                                                                                                                                                                                                6.2. STATE TABLES




                                                                                                     Get              Initial
                                                                      Get value            Type      Cmnd             Value                      Description          Sec.       Attribute
                                                                 AMBIENT                  8 ∗ ×C   GetLightfv   (0.0,0.0,0.0,1.0)   Ambient intensity of light i     2.12.1       lighting
                                                                 DIFFUSE                  8 ∗ ×C   GetLightfv        see 2.5        Diffuse intensity of light i     2.12.1       lighting
                                                                 SPECULAR                 8 ∗ ×C   GetLightfv        see 2.5        Specular intensity of light i    2.12.1       lighting
                                                                 POSITION                 8 ∗ ×P   GetLightfv   (0.0,0.0,1.0,0.0)   Position of light i              2.12.1       lighting
                                                                 CONSTANT ATTENUATION    8 ∗ ×R+   GetLightfv          1.0          Constant atten. factor           2.12.1       lighting
                                                                 LINEAR ATTENUATION      8 ∗ ×R+   GetLightfv          0.0          Linear atten. factor             2.12.1       lighting
                                                                 QUADRATIC ATTENUATION   8 ∗ ×R+   GetLightfv          0.0          Quadratic atten. factor          2.12.1       lighting
                                                                 SPOT DIRECTION           8 ∗ ×D   GetLightfv     (0.0,0.0,-1.0)    Spotlight direction of light i   2.12.1       lighting
                                                                 SPOT EXPONENT           8 ∗ ×R+   GetLightfv          0.0          Spotlight exponent of light i    2.12.1       lighting
                                                                 SPOT CUTOFF             8 ∗ ×R+   GetLightfv         180.0         Spot. angle of light i           2.12.1       lighting




                                  Table 6.10. Lighting (cont.)


Version 1.1.12 (April 24, 2008)
                                                                 LIGHTi                   8 ∗ ×B   IsEnabled          False         True if light i enabled          2.12.1   lighting/enable
                                                                                                                                                                                                131
                                                                                                      Get         Initial
                                                                      Get value             Type      Cmnd        Value                  Description           Sec.      Attribute
                                                              POINT SIZE                    R+      GetFloatv      1.0      Point size                         3.3         point
                                                                                                                                                                                        6.2. STATE TABLES




                                                              POINT SMOOTH                   B      IsEnabled     False     Point antialiasing on              3.3      point/enable
                                                              POINT SIZE MIN                R+      GetFloatv      0.0      Attenuated minimum point size      3.3         point
                                                                                                                    1
                                                              POINT SIZE MAX                R+      GetFloatv               Attenuated maximum point size. 1   3.3         point
                                                                                                                            Max. of the impl. dependent max.
                                                                                                                            aliased and smooth point sizes.
                                                              POINT FADE THRESHOLD SIZE      R+      GetFloatv     1.0      Threshold for alpha attenuation     3.3         point
                                                              POINT DISTANCE ATTENUATION   3 × R+    GetFloatv    1,0,0     Attenuation coefficients            3.3         point
                                                              POINT SPRITE OES                B      IsEnabled    False     Point sprites enabled               3.3         point
                                                              LINE WIDTH                     R+      GetFloatv     1.0      Line width                          3.4          line
                                                              LINE SMOOTH                     B      IsEnabled    False     Line antialiasing on                3.4      line/enable
                                                              CULL FACE                       B      IsEnabled    False     Polygon culling enabled            3.5.1   polygon/enable
                                                              CULL FACE MODE                 Z3     GetIntegerv   BACK      Cull front/back facing polygons    3.5.1       polygon




                                  Table 6.11. Rasterization




Version 1.1.12 (April 24, 2008)
                                                              FRONT FACE                     Z2     GetIntegerv   CCW       Polygon frontface CW/CCW           3.5.1       polygon
                                                                                                                            indicator
                                                              POLYGON OFFSET FACTOR          R      GetFloatv       0       Polygon offset factor              3.5.2      polygon
                                                              POLYGON OFFSET UNITS           R      GetFloatv       0       Polygon offset units               3.5.2      polygon
                                                              POLYGON OFFSET FILL            B      IsEnabled     False     Polygon offset enable              3.5.2   polygon/enable
                                                                                                                                                                                        132
                                                                                                                                                                                  6.2. STATE TABLES




                                                                                                   Get        Initial
                                                                    Get value            Type      Cmnd       Value                  Description     Sec.         Attribute
                                                              MULTISAMPLE                 B      IsEnabled     True     Multisample rasterization    3.2.1   multisample/enable
                                                              SAMPLE ALPHA TO COVERAGE    B      IsEnabled    False     Modify coverage from alpha   4.1.3   multisample/enable
                                                              SAMPLE ALPHA TO ONE         B      IsEnabled    False     Set alpha to maximum         4.1.3   multisample/enable
                                                              SAMPLE COVERAGE             B      IsEnabled    False     Mask to modify coverage      4.1.3   multisample/enable
                                                              SAMPLE COVERAGE VALUE      R+      GetFloatv      1       Coverage mask value          4.1.3      multisample
                                                              SAMPLE COVERAGE INVERT      B     GetBooleanv   False     Invert coverage mask value   4.1.3      multisample




                                  Table 6.12. Multisampling




Version 1.1.12 (April 24, 2008)
                                                                                                                                                                                  133
                                                                                                                                                                                                                    6.2. STATE TABLES




                                                                                                                                          Get         Initial
                                                                                                                 Get value    Type        Cmnd        Value              Description       Sec.       Attribute
                                                                                                    TEXTURE 2D               2 ∗ ×B     IsEnabled     False     True if 2D texturing is   3.7.13   texture/enable
                                                                                                                                                                enabled
                                                                                                    TEXTURE BINDING 2D       2 ∗ ×Z +   GetIntegerv     0       Texture object bound to   3.7.11      texture
                                                                                                                                                                TEXTURE 2D
                                                                                                    TEXTURE 2D                n×I           –         see 3.7   2D texture image at        3.7           –
                                                                                                                                                                l.o.d. i




Version 1.1.12 (April 24, 2008)
                                  Table 6.13. Textures (state per texture unit and binding point)
                                                                                                                                                                                                                    134
                                                                                                                                                                                             6.2. STATE TABLES




                                                                                                                         Get           Initial
                                                                                               Get value    Type         Cmnd          Value            Description      Sec.    Attribute
                                                                                    TEXTURE MIN FILTER     n × Z6   GetTexParameter   see 3.7    Texture minification    3.7.7    texture
                                                                                                                                                 function
                                                                                    TEXTURE MAG FILTER     n × Z2   GetTexParameter   see 3.7    Texture magnification   3.7.8   texture
                                                                                                                                                 function
                                                                                    TEXTURE WRAP S         n × Z2   GetTexParameter   REPEAT     Texcoord s wrap mode    3.7.6   texture
                                                                                    TEXTURE WRAP T         n × Z2   GetTexParameter   REPEAT     Texcoord t wrap mode    3.7.6   texture
                                                                                    GENERATE MIPMAP        n×B      GetTexParameter    FALSE     Automatic mipmap        3.7.7   texture
                                                                                                                                                 generation




Version 1.1.12 (April 24, 2008)
                                  Table 6.14. Textures (state per texture object)
                                                                                                                                                                                             135
                                                                                                                    Get          Initial
                                                                                      Get value          Type       Cmnd         Value                 Description         Sec.    Attribute
                                                                                   ACTIVE TEXTURE        Z2∗     GetIntegerv   TEXTURE0    Active texture unit selector     2.7     texture
                                                                                   TEXTURE ENV MODE    2 ∗ ×Z6   GetTexEnviv   MODULATE    Texture application function   3.7.12    texture
                                                                                   TEXTURE ENV COLOR   2 ∗ ×C    GetTexEnvfv     0,0,0,0   Texture environment color      3.7.12    texture
                                                                                                                                                                                               6.2. STATE TABLES




                                                                                   COORD REPLACE OES   2 ∗ ×B    GetTexEnviv      False    Point coordinate replacement     3.3     texture
                                                                                                                                           enabled
                                                                                   COMBINE RGB         2 ∗ ×Z8   GetTexEnviv   MODULATE    RGB combiner function          3.7.12   texture
                                                                                   COMBINE ALPHA       2 ∗ ×Z6   GetTexEnviv   MODULATE    Alpha combiner function        3.7.12   texture
                                                                                   SRC0 RGB            2 ∗ ×Z3   GetTexEnviv    TEXTURE    RGB source 0                   3.7.12   texture
                                                                                   SRC1 RGB            2 ∗ ×Z3   GetTexEnviv   PREVIOUS    RGB source 1                   3.7.12   texture
                                                                                   SRC2 RGB            2 ∗ ×Z3   GetTexEnviv   CONSTANT    RGB source 2                   3.7.12   texture
                                                                                   SRC0 ALPHA          2 ∗ ×Z3   GetTexEnviv    TEXTURE    Alpha source 0                 3.7.12   texture
                                                                                   SRC1 ALPHA          2 ∗ ×Z3   GetTexEnviv   PREVIOUS    Alpha source 1                 3.7.12   texture
                                                                                   SRC2 ALPHA          2 ∗ ×Z3   GetTexEnviv   CONSTANT    Alpha source 2                 3.7.12   texture
                                                                                   OPERAND0 RGB        2 ∗ ×Z4   GetTexEnviv   SRC COLOR   RGB operand 0                  3.7.12   texture
                                                                                   OPERAND1 RGB        2 ∗ ×Z4   GetTexEnviv   SRC COLOR   RGB operand 1                  3.7.12   texture




Version 1.1.12 (April 24, 2008)
                                                                                   OPERAND2 RGB        2 ∗ ×Z4   GetTexEnviv   SRC ALPHA   RGB operand 2                  3.7.12   texture
                                                                                   OPERAND0 ALPHA      2 ∗ ×Z2   GetTexEnviv   SRC ALPHA   Alpha operand 0                3.7.12   texture
                                                                                   OPERAND1 ALPHA      2 ∗ ×Z2   GetTexEnviv   SRC ALPHA   Alpha operand 1                3.7.12   texture
                                                                                   OPERAND2 ALPHA      2 ∗ ×Z2   GetTexEnviv   SRC ALPHA   Alpha operand 2                3.7.12   texture




                                  Table 6.15. Texture Environment and Generation
                                                                                   RGB SCALE           2 ∗ ×R3   GetTexEnvfv      1.0      RGB post-combiner scaling      3.7.12   texture
                                                                                   ALPHA SCALE         2 ∗ ×R3   GetTexEnvfv      1.0      Alpha post-combiner scaling    3.7.12   texture
                                                                                                                                                                                               136
                                                                                                     Get         Initial
                                                                      Get value            Type      Cmnd        Value                    Description          Sec.           Attribute
                                                                 SCISSOR TEST                B     IsEnabled      False     Scissoring enabled                 4.1.2      scissor/enable
                                                                 SCISSOR BOX               4×Z    GetIntegerv   see 4.1.2   Scissor box                        4.1.2           scissor
                                                                                                                                                                                               6.2. STATE TABLES




                                                                 ALPHA TEST                  B     IsEnabled      False     Alpha test enabled                 4.1.4    color-buffer/enable
                                                                 ALPHA TEST FUNC            Z8    GetIntegerv   ALWAYS      Alpha test function                4.1.4        color-buffer
                                                                 ALPHA TEST REF             R+    GetIntegerv       0       Alpha test reference value         4.1.4        color-buffer
                                                                 STENCIL TEST                B     IsEnabled      False     Stenciling enabled                 4.1.5   stencil-buffer/enable
                                                                 STENCIL FUNC               Z8    GetIntegerv   ALWAYS      Stencil function                   4.1.5       stencil-buffer
                                                                 STENCIL VALUE MASK         Z+    GetIntegerv      1’s      Stencil mask                       4.1.5       stencil-buffer
                                                                 STENCIL REF                Z+    GetIntegerv       0       Stencil reference value            4.1.5       stencil-buffer
                                                                 STENCIL FAIL               Z6    GetIntegerv    KEEP       Stencil fail action                4.1.5       stencil-buffer
                                                                 STENCIL PASS DEPTH FAIL    Z6    GetIntegerv    KEEP       Stencil depth buffer fail action   4.1.5       stencil-buffer
                                                                 STENCIL PASS DEPTH PASS    Z6    GetIntegerv    KEEP       Stencil depth buffer pass action   4.1.5       stencil-buffer
                                                                 DEPTH TEST                  B     IsEnabled      False     Depth buffer enabled               4.1.6   depth-buffer/enable
                                                                 DEPTH FUNC                 Z8    GetIntegerv    LESS       Depth buffer test function         4.1.6       depth-buffer




                                  Table 6.16. Pixel Operations



Version 1.1.12 (April 24, 2008)
                                                                 BLEND                       B     IsEnabled      False     Blending enabled                   4.1.7    color-buffer/enable
                                                                 BLEND SRC                  Z9    GetIntegerv     ONE       Blending source function           4.1.7        color-buffer
                                                                 BLEND DST                  Z8    GetIntegerv    ZERO       Blending dest. function            4.1.7        color-buffer
                                                                 DITHER                      B     IsEnabled      True      Dithering enabled                  4.1.8    color-buffer/enable
                                                                 COLOR LOGIC OP              B     IsEnabled      False     Color logic op enabled             4.1.9    color-buffer/enable
                                                                 LOGIC OP MODE              Z16   GetIntegerv    COPY       Logic op function                  4.1.9        color-buffer
                                                                                                                                                                                               137
                                                                                                                                                                                       6.2. STATE TABLES




                                                                                                    Get        Initial
                                                                        Get value         Type      Cmnd       Value                  Description             Sec.       Attribute
                                                                    COLOR WRITEMASK       4×B    GetBooleanv    True     Color write enables; R, G, B, or A   4.2.2    color-buffer
                                                                    DEPTH WRITEMASK        B     GetBooleanv    True     Depth buffer enabled for writing     4.2.2   depth-buffer
                                                                    STENCIL WRITEMASK      Z+    GetIntegerv     1’s     Stencil buffer writemask             4.2.2   stencil-buffer
                                                                    COLOR CLEAR VALUE      C      GetFloatv    0,0,0,0   Color buffer clear value (RGBA       4.2.3    color-buffer
                                                                                                                         mode)
                                                                    DEPTH CLEAR VALUE     R+     GetIntegerv     1       Depth buffer clear value             4.2.3   depth-buffer
                                                                    STENCIL CLEAR VALUE   Z+     GetIntegerv     0       Stencil clear value                  4.2.3   stencil-buffer




Version 1.1.12 (April 24, 2008)
                                  Table 6.17. Framebuffer Control
                                                                                                                                                                                       138
                                                                                                                                                           6.2. STATE TABLES




                                                                                   Get         Initial
                                                          Get value       Type     Cmnd        Value                Description      Sec.     Attribute
                                                       UNPACK ALIGNMENT   Z+     GetIntegerv     4       Value of UNPACK ALIGNMENT   3.6.1   pixel-store
                                                       PACK ALIGNMENT     Z+     GetIntegerv     4       Value of PACK ALIGNMENT     4.3.1   pixel-store




                                  Table 6.18. Pixels




Version 1.1.12 (April 24, 2008)
                                                                                                                                                           139
                                                                                                                                                                      6.2. STATE TABLES




                                                                                             Get           Initial
                                                                 Get value          Type     Cmnd          Value                 Description       Sec.   Attribute
                                                      PERSPECTIVE CORRECTION HINT    Z3    GetIntegerv   DONT CARE   Perspective correction hint   5.2      hint
                                                      POINT SMOOTH HINT              Z3    GetIntegerv   DONT CARE   Point smooth hint             5.2      hint
                                                      LINE SMOOTH HINT               Z3    GetIntegerv   DONT CARE   Line smooth hint              5.2      hint
                                                      FOG HINT                       Z3    GetIntegerv   DONT CARE   Fog hint                      5.2      hint
                                                      GENERATE MIPMAP HINT           Z3    GetIntegerv   DONT CARE   Mipmap generation hint        5.2      hint




                                  Table 6.19. Hints




Version 1.1.12 (April 24, 2008)
                                                                                                                                                                      140
                                                                                                                                                                                                        6.2. STATE TABLES




                                                                                                                        Get         Minimum
                                                                                        Get value             Type      Cmnd        Value                     Description           Sec.    Attribute
                                                                                MAX LIGHTS                    Z+      GetIntegerv       8        Maximum number of lights          2.12.1       –
                                                                                MAX CLIP PLANES               Z+      GetIntegerv       1        Maximum number of user clipping    2.11        –
                                                                                                                                                 planes
                                                                                MAX MODELVIEW STACK DEPTH     Z+      GetIntegerv      16        Maximum model-view stack depth    2.10.2      –
                                                                                MAX PROJECTION STACK DEPTH    Z+      GetIntegerv       2        Maximum projection matrix stack   2.10.2      –
                                                                                                                                                 depth
                                                                                MAX TEXTURE STACK DEPTH       Z+      GetIntegerv       2        Maximum number depth of texture   2.10.2      –
                                                                                                                                                 matrix stack
                                                                                SUBPIXEL BITS                 Z+      GetIntegerv       4        Number of bits of subpixel          3         –
                                                                                                                                                 precision in screen xw and yw
                                                                                MAX TEXTURE SIZE




Version 1.1.12 (April 24, 2008)
                                                                                                               Z+     GetIntegerv       64       Maximum texture image dimension    3.7.1      –
                                                                                MAX VIEWPORT DIMS            2 × Z+   GetIntegerv   see 2.10.1   Maximum viewport dimensions       2.10.1      –




                                  Table 6.20. Implementation Dependent Values
                                                                                                                                                                                                        141
                                                                                                                                                                                                   6.2. STATE TABLES




                                                                                                                                 Get    Minimum
                                                                                                    Get value       Type         Cmnd   Value             Description           Sec.   Attribute
                                                                                        ALIASED POINT SIZE RANGE   2 × R+   GetFloatv      1,1    Range (lo to hi) of aliased   3.3        –
                                                                                                                                                  point sizes
                                                                                        SMOOTH POINT SIZE RANGE    2 × R+   GetFloatv     1,1     Range (lo to hi) of           3.3       –
                                                                                        (POINT SIZE RANGE)                                        antialiased point sizes
                                                                                        ALIASED LINE WIDTH RANGE   2 × R+   GetFloatv     1,1     Range (lo to hi) of aliased   3.4       –
                                                                                                                                                  line widths
                                                                                        SMOOTH LINE WIDTH RANGE    2 × R+   GetFloatv     1,1     Range (lo to hi) of           3.4       –
                                                                                        (v1.1: LINE WIDTH RANGE)                                  antialiased line widths




Version 1.1.12 (April 24, 2008)
                                  Table 6.21. Implementation Dependent Values (cont.)
                                                                                                                                                                                                   142
                                                                                                                                                                                                        6.2. STATE TABLES




                                                                                                                                        Get     Minimum
                                                                                                         Get value        Type          Cmnd    Value            Description        Sec.    Attribute
                                                                                        MAX TEXTURE UNITS                 Z+      GetIntegerv       2     Number of texture units   2.6         –
                                                                                                                                                          (not to exceed 32)
                                                                                        SAMPLE BUFFERS                    Z+      GetIntegerv      0      Number of multisample     3.2.1      –
                                                                                                                                                          buffers
                                                                                        SAMPLES                            Z+     GetIntegerv      0      Coverage mask size        3.2.1      –
                                                                                        COMPRESSED TEXTURE FORMATS       10 × Z   GetIntegerv      -      Enumerated compressed     3.7.3      –
                                                                                                                                                          texture formats
                                                                                        NUM COMPRESSED TEXTURE FORMATS     Z      GetIntegerv     10      Number of enumerated      3.7.3      –
                                                                                                                                                          compressed texture




Version 1.1.12 (April 24, 2008)
                                                                                                                                                          formats




                                  Table 6.22. Implementation Dependent Values (cont.)
                                                                                                                                                                                                        143
                                                                                                                                                                                          6.2. STATE TABLES




                                                                                                              Get         Initial
                                                                                      Get value      Type     Cmnd        Value                Description             Sec.   Attribute
                                                                                      x BITS         Z+     GetIntegerv      -      Number of bits in x color buffer    4         –
                                                                                                                                    component; x is one of RED,
                                                                                                                                    GREEN, BLUE, or ALPHA
                                                                                      DEPTH BITS     Z+     GetIntegerv     -       Number of depth buffer planes       4        –
                                                                                      STENCIL BITS   Z+     GetIntegerv     -       Number of stencil planes            4        –




Version 1.1.12 (April 24, 2008)
                                  Table 6.23. Implementation Dependent Pixel Depths
                                                                                                                                                                                          144
                                                                                                                                                              6.2. STATE TABLES




                                                                                    Get       Initial
                                                              Get value    Type     Cmnd      Value                  Description           Sec.   Attribute
                                                              –           n × Z8   GetError     0       Current error code(s)              2.5        –
                                                              –           n×B         –       False     True if there is a corresponding   2.5        –
                                                                                                        error




                                  Table 6.24. Miscellaneous




Version 1.1.12 (April 24, 2008)
                                                                                                                                                              145
Appendix A

Invariance

The OpenGL ES specification is not pixel exact. It therefore does not guarantee an
exact match between images produced by different GL implementations. However,
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




                                        146
A.2. MULTI-PASS ALGORITHMS                                                       147


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
OpenGL ES .


A.3     Invariance Rules
For a given instantiation of an OpenGL rendering context:

Rule 1 For any given GL and framebuffer state vector, and for any given GL com-
mand, the resulting GL and framebuffer state must be identical each time the com-
mand is executed on that initial GL and framebuffer state.

Rule 2 Changes to the following state values have no side effects (the use of any
other state value is not affected by the change):

Required:

         • Framebuffer contents (all bitplanes)
         • The values of matrices other than the top-of-stack matrices
         • Scissor parameters (other than enable)




                          Version 1.1.12 (April 24, 2008)
A.3. INVARIANCE RULES                                                            148


         • Writemasks (color, depth, stencil)
         • Clear values (color, depth, stencil)
         • Current values (color, normal, texture coords)
         • Material properties (ambient, diffuse, specular, emission, shininess)

Strongly suggested:

         • Matrix mode
         • Matrix stack depths
         • Alpha test parameters (other than enable)
         • Stencil parameters (other than enable)
         • Depth test parameters (other than enable)
         • Blend parameters (other than enable)
         • Logical operation parameters (other than enable)
         • Pixel storage
         • Polygon offset parameters (other than enables, and except as they affect
           the depth values of fragments)

Corollary 1 Fragment generation is invariant with respect to the state values
marked with • in Rule 2.

Corollary 2 The window coordinates (x, y, and z) of generated fragments are also
invariant with respect to

Required:

         • Current values (color, normal, texture coords)
         • Material properties (ambient, diffuse, specular, emission, shininess)

Rule 3 The arithmetic of each per-fragment operation is invariant except with re-
spect to parameters that directly control it (the parameters that control the alpha
test, for instance, are the alpha test enable, the alpha test function, and the alpha
test reference value).

Corollary 3 Images rendered into different color buffers sharing the same frame-
buffer, either simultaneously or separately using the same command sequence, are
pixel identical.




                           Version 1.1.12 (April 24, 2008)
A.4. WHAT ALL THIS MEANS                                                      149


A.4     What All This Means
Hardware accelerated GL implementations are expected to default to software op-
eration when some GL state vectors are encountered. Even the weak repeatability
requirement means, for example, that OpenGL ES implementations cannot apply
hysteresis to this swap, but must instead guarantee that a given mode vector im-
plies that a subsequent command always is executed in either the hardware or the
software machine.
    The stronger invariance rules constrain when the switch from hardware to soft-
ware rendering can occur, given that the software and hardware renderers are not
pixel identical. For example, the switch can be made when blending is enabled or
disabled, but it should not be made when a change is made to the blending param-
eters.
    Because floating point values may be represented using different formats in
different renderers (hardware and software), many OpenGL ES state values may
change subtly when renderers are swapped. This is the type of state value change
that Rule 1 seeks to avoid.




                         Version 1.1.12 (April 24, 2008)
Appendix B

Corollaries

The following observations are derived from the body and the other appendixes of
the specification. Absence of an observation from this list in no way impugns its
veracity.

   1. The error semantics of upward compatible OpenGL ES revisions may
      change. Otherwise, only additions can be made to upward compatible re-
      visions.

   2. GL query commands are not required to satisfy the semantics of the Flush
      or the Finish commands. All that is required is that the queried state be con-
      sistent with complete execution of all previously executed GL commands.

   3. Application specified point size and line width must be returned as specified
      when queried. Implementation dependent clamping affects the values only
      while they are in use.

   4. The mask specified as the third argument to StencilFunc affects the operands
      of the stencil comparison function, but has no direct effect on the update of
      the stencil buffer. The mask specified by StencilMask has no effect on the
      stencil comparison function; it limits the effect of the update of the stencil
      buffer.

   5. A material property that is attached to the current color (by enabling
      COLOR MATERIAL) always takes the value of the current color. Attempts
      to change that material property via Material calls have no effect.

   6. There is no atomicity requirement for OpenGL ES rendering commands,
      even at the fragment level.




                                       150
                                                                                151


 7. Because rasterization of non-antialiased polygons is point sampled, poly-
    gons that have no area generate no fragments when they are rasterized, and
    the fragments generated by the rasterization of “narrow” polygons may not
    form a continuous array.

 8. OpenGL ES does not force left- or right-handedness on any of its coordinates
    systems. Consider, however, the following conditions: (1) the object coordi-
    nate system is right-handed; (2) the only commands used to manipulate the
    model-view matrix are Scale (with positive scaling values only), Rotate, and
    Translate; (3) exactly one of either Frustum or Ortho is used to set the pro-
    jection matrix; (4) the near value is less than the far value for DepthRange.
    If these conditions are all satisfied, then the eye coordinate system is right-
    handed and the clip, normalized device, and window coordinate systems are
    left-handed.

 9. (No pixel dropouts or duplicates.) Let two polygons share an identical edge
    (that is, there exist vertices A and B of an edge of one polygon, and vertices
    C and D of an edge of the other polygon, and the coordinates of vertex A
    (resp. B) are identical to those of vertex C (resp. D), and the state of the the
    coordinate transfomations is identical when A, B, C, and D are specified).
    Then, when the fragments produced by rasterization of both polygons are
    taken together, each fragment intersecting the interior of the shared edge is
    produced exactly once.

10. The user defined clip planes, the spot directions, and the light positions for
    LIGHTi are transformed when they are specified. They are not transformed
    when copying a context.

11. Dithering algorithms may be different for different components. In particu-
    lar, alpha may be dithered differently from red, green, or blue, and an imple-
    mentation may choose to not dither alpha at all.




                        Version 1.1.12 (April 24, 2008)
Appendix C

Profiles

The body of the OpenGL ES specification describes both the Common and
Common-Lite profiles. This appendix provides more information about the con-
tents of profiles and the differences between them, including numeric precision
issues, supported commands, OpenGL ES -specific extensions, and packaging is-
sues.


C.1     Accuracy Requirements
As described in section 2.1.1, the Common-Lite (CL) profile has more relaxed
requirements on arithmetic range and precision than the Common profile. This
allows CL implementations to use fixed-point arithmetic internally, although they
are not required to do so.


C.2     Floating-Point and Fixed-Point Commands and State
The CL profile does not support any of the commands taking floating-point argu-
ments, such as Normal3f. Alternate versions of those commands taking fixed-point
arguments are provided instead. The fixed-point commands are also supported in
the Common profile to allow Common-Lite applications to run unchanged in that
profile. A complete list of the floating-point functions found only in the Common
profile is in table C.1.
    Similarly, the CL profile does not support floating-point data (format FLOAT)
in vertex arrays or images in client memory. The FIXED format should be used
instead. The FIXED format is also supported in the Common profile.
    Finally, the CL profile is not required to store internal GL state in floating-
point. When the specification or state tables (see section 6.2) indicate state is stored




                                         152
C.3. CORE ADDITIONS AND EXTENSIONS                                              153


in floating-point, the CL profile may always store it in fixed-point instead. Appli-
cations using the CL profile must call the GetFixedv command, or the equivalent
fixed-point versions of enumerated queries, such as GetLightxv, to query such
state.


C.3     Core Additions and Extensions
An OpenGL ES profile consists of two parts: a subset of the full OpenGL pipeline,
and some extended functionality that is drawn from a set of OpenGL ES -specific
extensions to the full OpenGL specification. Each extension is pruned to match
the profile’s command subset and added to the profile as either a core addition
or a profile extension. Core additions differ from profile extensions in that the
commands and tokens do not include extension suffixes in their names.
     Profile extensions are further divided into required (mandatory) and optional
extensions. Required extensions must be implemented as part of a conforming im-
plementation, whereas the implementation of optional extensions is left to the dis-
cretion of the implementor. Both types of extensions use extension suffixes as part
of their names, are present in the EXTENSIONS string, and participate in function
address queries defined in the platform embedding layer. Required extensions have
the additional packaging constraint, that commands defined as part of a required
extension must also be available as part of a static binding if core commands are
also available in a static binding. The commands comprising an optional extension
may optionally be included as part of a static binding.
     From an API perspective, commands and tokens comprising a core addition are
indistinguishable from the original OpenGL subset. However, to increase applica-
tion portability, an implementation may also implement a core addition as an ex-
tension by including suffixed versions of commands and tokens in the appropriate
dynamic and optional static bindings and the extension name in the EXTENSIONS
string.
     The      Common         and     Common-Lite        profiles    add    subsets
of the OES byte coordinates, OES fixed point, OES single precision
and      OES matrix get          OpenGL       ES     -specific    extensions     as
core additions, and OES read format, OES compressed paletted texture,
OES point size array and OES point sprite as required profile extensions.
All of these extensions are incorporated into the body of the specification. The
OES matrix palette and OES draw texture are added as optional profile ex-
tensions, and specified separately in the Khronos Extension Registry, on the web
at URL http://www.khronos.org/registry/gles.
     The OES query matrix optional extension in OpenGL ES 1.0 has been dep-




                         Version 1.1.12 (April 24, 2008)
C.3. CORE ADDITIONS AND EXTENSIONS                                   154


 Floating-point commands only           Equivalent fixed-point commands
 supported in the Common profile        support in both Common and Common-List
 AlphaFunc                              AlphaFuncx
 ClearColor                             ClearColorx
 ClearDepthf                            ClearDepthx
 ClipPlanef                             ClipPlanex
 Color4f                                Color4x
 DepthRangef                            DepthRangex
 Fogf, Fogfv                            Fogx, Fogxv
 Frustumf                               Frustumx
 GetClipPlanef                          GetClipPlanex
 GetFloatv                              GetFixedv
 GetLightfv                             GetLightxv
 GetMaterialfv                          GetMaterialxv
 GetTexEnvfv                            GetTexEnvxv
 GetTexParameterfv                      GetTexParameterxv
 LightModelf, LightModelfv              LightModelx, LightModelxv
 Lightf, Lightfv                        Lightx, Lightxv
 LineWidth                              LineWidthx
 LoadMatrixf                            LoadMatrixx
 Materialf, Materialfv                  Materialx, Materialxv
 MultMatrixf                            MultMatrixx
 MultiTexCoord4f                        MultiTexCoord4x
 Normal3f                               Normal3x
 Orthof                                 Orthox
 PointParameterf, PointParameterfv      PointParameterx, PointParameterxv
 PointSize                              PointSizex
 PolygonOffset                          PolygonOffsetx
 Rotatef                                Rotatex
 SampleCoverage                         SampleCoveragex
 Scalef                                 Scalex
 TexEnvf, TexEnvfv                      TexEnvx, TexEnvxv
 TexParameterf, TexParameterfv          TexParameterx, TexParameterxv
 Translatef                             Translatex
 Vertex array commands (ColorPointer,   Use type FIXED instead
 NormalPointer, TexCoordPointer,
 and VertexPointer) with type FLOAT

             Table C.1: Common and Common-Lite commands.




                      Version 1.1.12 (April 24, 2008)
C.3. CORE ADDITIONS AND EXTENSIONS                                          155


recated in OpenGL ES 1.1. The various matrices in GL can be obtained by calling
GetFixedv or GetFloatv, or by using the OES matrix get core extension.

 Extension Name                                Common             Common-Lite
 OES    byte coordinates                      core addition        core addition
 OES    fixed point                           core addition        core addition
 OES    single precision                      core addition             n/a
 OES    matrix get                            core addition        core addition
 OES    read format                        required extension   required extension
 OES    compressed paletted texture        required extension   required extension
 OES    point size array                   required extension   required extension
 OES    point sprite                       required extension   required extension
 OES matrix palette                        optional extension   optional extension
 OES draw texture                          optional extension   optional extension


                     Table C.2: OES Extension Disposition


C.3.1    Byte Coordinates
The OES byte coordinates extension allows byte data types to be used as
vertex and texture coordinates. The Common/Common-Lite profile supports byte
coordinates in vertex array commands, as described in section 2.8.

C.3.2    Fixed Point
The OES fixed point extension defines an integer fixed-point data type for ver-
tex attributes and command parameters. The extension specification includes
commands that parallel all OpenGL 1.5 commands with floating-point parame-
ters (including commands that support a single parameter type version such as
DepthRange, PointSize, and LineWidth). The subset of commands included in
the Common and Common-Lite profiles matches exactly the subset of floating-
point commands included in the Common profile (see section C.2).

C.3.3    Single-precision Commands
The OES single precision commands extension creates new single-precision
parameter command variants of commands that have no such variants
(DepthRange, Frustum, Ortho, etc.). Only the subset matching the profile feature
set is included in the Common profile.




                        Version 1.1.12 (April 24, 2008)
C.3. CORE ADDITIONS AND EXTENSIONS                                                156



              DepthRangef(clampf n, clampf f)
              Frustumf(float l, float r, float b, float t, float n, float f)
              Orthof(float l, float r, float b, float t, float n, float f)
              ClearDepthf(clampf depth)
              GetClipPlanef(enum pname, float eqn[4])

C.3.4    Compressed Paletted Texture
The OES compressed paletted texture extension provides a method for
specifying a compressed texture image as a color index image accompanied by
a palette. The extension adds ten new texture internal formats to specify different
combinations of index width and palette color format, as described in section 3.7.3.

C.3.5    Read Format
The OES read format extension allows implementation-specific pixel type and
format parameters to be queried by an application and used in ReadPixels com-
mands, as described in section 4.3.1.

C.3.6    Matrix Palette
The optional OES matrix palette extension adds the ability to support vertex
skinning in OpenGL ES. This extension allow OpenGL ES to support a palette of
matrices. The matrix palette defines a set of matrices that can be used to transform
a vertex. The matrix palette is not part of the model view matrix stack and is
enabled by setting the MATRIX MODE to MATRIX PALETTE OES.
    The n vertex units use a palette of m modelview matrices (where n and m are
constrained to implementation defined maxima). Each vertex has a set of n indices
into the palette, and a corresponding set of n weights. Matrix indices and weights
can be changed for each vertex.
    When this extension is utilized, the enabled units transform each vertex by the
modelview matrices specified by the vertices’ respective indices. These results are
subsequently scaled by the weights of the respective units and then summed to
create the eyespace vertex.

C.3.7    Point Sprites
The OES point sprite extension provides a method for application to draw par-
ticles using points instead of quads, as described in section 3.3. This extension also




                          Version 1.1.12 (April 24, 2008)
C.4. PACKAGING                                                                    157


allows an app to specify texture coordinates that are interpolated across the point
instead of the same texture coordinate used by traditional GL points.

C.3.8    Point Size Array
This OES point size array extension extends how points and point sprites are
rendered by allowing an array of point sizes instead of a fixed input point size given
by PointSize. This provides flexibility for applications to do particle effects.
    Vertex arrays are extended to include a point size array, as described in sec-
tion 2.8.

C.3.9    Matrix Get
Many applications require the ability to be able to read the GL matrices. OpenGL
ES 1.1 allows applications to read matrices using the GetFloatv command for the
common profile and the GetFixedv command for the common-lite profile.
    In cases where the common-lite implementation stores matrices and performs
matrix operations internally using floating point (an example would be OpenGL
ES implementations that support JSR184), the GL cannot return the floating-point
matrix elements, since the float data type is not supported by the common-lite
profile. Using GetFixedv to read matrix data will result in a loss of information.
    To         address        this       issue,         the        new        targets
MODELVIEW MATRIX FLOAT AS INT BITS OES, PROJECTION MATRIX FLOAT AS INT BITS OES,
and TEXTURE MATRIX FLOAT AS INT BITS OES are accepted by GetIntegerv,
as described in section 6.1.2. These tokens allow the GL to return a representation
of the floating-point matrix elements as an array of integers, according to the IEEE
754 floating-point “single format” bit layout.

C.3.10    Draw Texture
This OES draw texture extension defines a mechanism for writing pixel rectan-
gles from one or more textures to a rectangular region of the screen. This capability
is useful for fast rendering of background paintings, bitmapped font glyphs, and 2D
framing elements in games


C.4      Packaging
The Khronos API Implementers Guide, a separate document linked from the
Khronos Extension Registry at




                          Version 1.1.12 (April 24, 2008)
C.5. ACKNOWLEDGEMENTS                                                          158


                       https://www.khronos.org/registry/

describes recommended and required practice for implementing OpenGL ES , in-
cluding names of header files and libraries making up the implementation, and links
to standard versions of the header files defining interfaces for the core OpenGL ES
API (gl.h and glplatform.h) as well as a separate header (glext.h) defin-
ing interfaces for Khronos-approved and vendor extensions.
     Preprocessor tokens VERSION ES CM n m and VERSION ES CL n m, where n
and m are the major and minor version numbers as described in section 6.1.5, are
included in gl.h. These tokens respectively indicate the OpenGL ES Common
and Common-Lite profile versions supported at compile-time.
     For backwards compatibility purposes, implementations supporting EGL may
provide two link libraries, one including EGL entry points and one not, as defined
in the Implementers Guide.
     Availability of static and dynamic function bindings is platform dependent.
Rules regarding the export of bindings for core additions, required profile exten-
sions, and optional platform extensions are described in section C.3.


C.5     Acknowledgements
The OpenGL ES Common and Common-Lite profiles are the result of the con-
tributions of many people, representing a cross section of the desktop, hand-held,
and embedded computer industry. Following is a partial list of the contributors,
including the company that they represented at the time of their contribution:

Aaftab Munshi, ATI
Andy Methley, Panasonic
Axel Mamode, Sony Computer Entertainment
Barthold Lichtenbelt, 3Dlabs
Benji Bowman, Imagination Technologies
Borgar Ljosland, Falanx
Brian Murray, Motorola
Bryce Johnstone, Texas Instruments
Carlos Sarria, Imagination Technologies
Chris Tremblay, Motorola
Claude Knaus, Esmertec




                          Version 1.1.12 (April 24, 2008)
C.5. ACKNOWLEDGEMENTS                                       159


Clay Montgomery, Nokia
Dan Petersen, Sun
Dan Rice, Sun
David Blythe, 3d4w and HI
David Yoder, Motorola
Doug Twilleager, Sun
Ed Plowman, ARM
Graham Connor, Imagination Technologies
Greg Stoner, Motorola
Hannu Napari, Hybrid
Harri Holopainen, Hybrid
Jacob Str¨om, Ericsson
Jani Vaarala, Nokia
Jerry Evans, Sun
John Metcalfe, Imagination Technologies
Jon Leech, Silicon Graphics
Kari Pulli, Nokia
Lane Roberts, Symbian
Madhukar Budagavi, Texas Instruments
Mathias Agopian, PalmSource
Mark Callow, HI
Mark Tarlton, Motorola
Mike Olivarez, Motorola
Neil Trevett, 3Dlabs
Nick Triantos, Nvidia
Petri Kero, Hybrid
Petri Nordlund, Bitboys
Phil Huxley, Tao Group
Remi Arnaud, Sony Computer Entertainment
Robert Simpson, Bitboys




                          Version 1.1.12 (April 24, 2008)
C.6. DOCUMENT HISTORY                                                          160


Tero Sarkkinen, Futuremark
Timo Suoranta, Futuremark
Thomas Tannert, Silicon Graphics
Tomi Aarnio, Nokia
Tom McReynolds, Nvidia
Tom Olson, Texas Instruments
Ville Miettinen, Hybrid Graphics


C.6    Document History
version 1.1.12, draft of 2008/04/24

   • Changed description of GetFixedv in section 6.1.2 to refer to section 2.3 and
     describe queries of integer state prior to enumerated state (bug 3123).

   • Noted in section 3.7.7 that automatic mipmap generation is not performed
     for compressed textures (bug 2893).

version 1.1.12, draft of 2008/04/14

   • Remove discussion of unsupported three-component form of Color com-
     mands in section 2.8 (bug 3066).

   • Finished specifying the restriction of RGB SCALE and ALPHA SCALE to val-
     ues of 1.0, 2.0, or 4.0 in section 3.7.12 (bug 1096).

   • Clarified numeric conversion rules in section 6.1.2 when querying non-fixed-
     point values with GetFixedv (bug 3123).

   • Modify section C.4 to refer to separate API Implementers Guide to eliminate
     redundancy in header and library naming (bug 3184).

version 1.1.12, draft of 2008/01/20

   • Update 1.1.10 diff specification in section 3.8.4 to specify texture complete-
     ness as requiring the same internal format, rather than the same type (bug
     1411), and to use corrected versions of the texture environment functions in
     section 3.8.6 (bug 1919).




                         Version 1.1.12 (April 24, 2008)
C.6. DOCUMENT HISTORY                                                       161


   • Fix definition of ONE in full spec table 4.1 to be consistent with diff and
     desktop specs (bug 2437).

   • Remove unsupported GetBufferSubData query command from state table
     entry in table 6.6 (bug 2659).

   • Bring version numbers of full and diff specifications into sync.

   • Add appendix D describing differences from OpenGL ES 1.0 (bug 1545).

version 1.1.10, April 4, 2007 Final revision of the full specification, based on
the 1.1.09 difference specification.




                        Version 1.1.12 (April 24, 2008)
Appendix D

Version 1.1

OpenGL ES version 1.1 is the first revision since the original version 1.0. Version
1.1 is upward compatible with earlier versions, meaning that any program that
runs with a 1.0 OpenGL ES implementation will also run unchanged with a 1.1
implementation.
    OpenGL ES 1.1 now includes a Full Specification document, which is a self-
contained description of the API. OpenGL ES 1.0 only has a Difference Specifica-
tion which must be read relative to the OpenGL 1.3 Specification.
    OpenGL ES 1.1 also includes a Difference Specification relative to the OpenGL
1.5 Specification. However, the Full Specification is now considered the canoni-
cal reference, and the Difference Specification is maintained primarily as a quick
reference for those familiar with desktop OpenGL.


D.1     Changes From OpenGL 1.5
Some new functionality in OpenGL ES 1.1 is based on corresponding features in
OpenGL 1.5, and described below.

D.1.1   Automatic Mipmap Generation
Setting the texture parameter GENERATE MIPMAP to TRUE introduces a side effect
to any modification of the base level of a mipmap array, wherein all higher levels
of the mipmap pyramid are recomputed automatically by successive filtering of the
base level array.




                                       162
D.2. ENHANCED TEXTURE PROCESSING                                                163


D.1.2    Buffer Objects
Buffer objects allow vertex array and element index data to be cached in high-
performance graphics memory, increasing the rate of data transfers to the GL.

D.1.3    Static and Dynamic State Queries
State queries are supported for static and dynamic state explicitly defined in the
profile. This enables OpenGL ES to be used in a sophisticated, layered software
environment.

D.1.4    User-defined Clip Planes
User clip planes allow efficient early culling of non-visible polygons.


D.2     Enhanced Texture Processing
A minimum of two textures must be supported. Texture combiner functionality
is supported, allowing effects such as bump-mapping and per-pixel lighting. All
OpenGL 1.5 texture environments except for the texture crossbar are supported.


D.3     New Core Additions and Profile Extensions
In addition to functionality derived from OpenGL 1.5, subsets of certain OES ex-
tensions are also added to OpenGL ES 1.1, and other OES extensions may be sup-
ported as optional profile extensions. These extensions are described in more detail
in appendix C.3.




                          Version 1.1.12 (April 24, 2008)
Index of OpenGL ES Commands

1, 89                                           Clear, 110, 111
                                                ClearColor, 110, 154
ACTIVE TEXTURE, 19, 90, 118, 119                ClearColorx, 110, 154
ActiveTexture, 32, 95                           ClearDepthf, 110, 154, 156
ADD, 90, 92, 93                                 ClearDepthx, 110, 154
ADD SIGNED, 93                                  ClearStencil, 110
ALPHA, 68, 69, 73, 76, 91, 92, 95, 106,         CLIENT ACTIVE TEXTURE, 21, 119
         113, 144                               ClientActiveTexture, 21
ALPHA SCALE, 90, 91, 95, 160                    CLIP PLANEi, 35
ALPHA TEST, 102                                 CLIP PLANE0, 35
AlphaFunc, 102, 154                             ClipPlane, 35
AlphaFuncx, 102, 154                            ClipPlanef, 154
ALWAYS, 102–104, 137                            ClipPlanex, 154
AMBIENT, 43                                     Color, 21, 37, 44, 160
AMBIENT AND DIFFUSE, 43                         Color4, 18
AND, 108                                        Color4f, 8, 18, 154
AND INVERTED, 108                               Color4ub, 18
AND REVERSE, 108                                Color4x, 18, 154
ARRAY BUFFER, 23–26                             COLOR ARRAY, 20
ARRAY BUFFER BINDING, 25                        COLOR ARRAY POINTER, 120
                                                COLOR BUFFER BIT, 110, 111
BACK, 63, 119, 132                              COLOR LOGIC OP, 107
BindBuffer, 23, 25, 26                          COLOR MATERIAL, 44, 150
BindTexture, 89                                 ColorMask, 109, 110
BLEND, 90, 92, 105, 107                         ColorPointer, 19, 20, 154
BlendFunc, 105                                  COMBINE, 90, 91, 93, 95
BLUE, 144                                       COMBINE ALPHA, 90, 91, 93, 94
BUFFER SIZE, 23–25                              COMBINE RGB, 90, 91, 93, 94
BUFFER USAGE, 23, 24                            COMPRESSED TEXTURE FORMATS,
BufferData, 24, 26                                        78
BufferSubData, 25, 26                           CompressedTexImage, 80
BYTE, 20                                        CompressedTexImage2D, 78–80
                                                CompressedTexSubImage2D, 80, 82
CCW, 41, 132
                                                CONSTANT, 94, 95, 136
CLAMP TO EDGE, 82, 83
                                                CONSTANT ATTENUATION, 43
CLEAR, 108




                                          164
INDEX                                                                             165


COORD REPLACE OES, 52, 54                      EXTENSIONS, 120, 153
COPY, 107, 108, 137
COPY INVERTED, 108                             FALSE, 39, 41, 52, 82, 89, 102, 118,
CopyTexImage, 77                                         120, 135
CopyTexImage2D, 76, 77, 86, 111                FASTEST, 116
CopyTexSubImage2D, 77                          Finish, 115, 150
CULL FACE, 63                                  FIXED, 20, 22, 152, 154
CullFace, 62, 63, 65                           FLAT, 45
CURRENT TEXTURE COORDS, 19                     FLOAT, 20, 22, 125, 126, 152, 154
CW, 41                                         Flush, 115, 150
                                               FOG, 97
DECAL, 90, 92                                  Fog, 97, 98
DECR, 103                                      FOG COLOR, 98
DeleteBuffers, 23, 24                          FOG DENSITY, 97
DeleteTextures, 89                             FOG END, 97
DEPTH BUFFER BIT, 110, 111                     FOG HINT, 116
DEPTH TEST, 104                                FOG MODE, 97, 98
DepthFunc, 104                                 FOG START, 97
DepthMask, 109, 110                            Fogf, 154
DepthRange, 118, 151, 155                      Fogfv, 154
DepthRangef, 28, 154, 156                      Fogx, 154
DepthRangex, 28, 154                           Fogxv, 154
DIFFUSE, 43                                    FRONT, 63, 119
Disable, 33, 35, 37, 44, 50–52, 57, 63,        FRONT AND BACK, 42, 63
          65, 95, 97, 101–105, 107             FrontFace, 41, 62
DisableClientState, 20, 21                     Frustum, 30, 31, 151, 155
DITHER, 107                                    Frustumf, 154, 156
DONT CARE, 116, 140                            Frustumx, 154
DOT3 RGB, 93
DOT3 RGBA, 93                                  GenBuffers, 23
DrawArrays, 14, 21, 22, 25, 45                 GENERATE MIPMAP, 82, 87, 89, 162
DrawElements, 14, 21, 22, 25, 26, 45           GENERATE MIPMAP HINT, 116
DST ALPHA, 106                                 GenTextures, 90, 120
DST COLOR, 105, 106                            GEQUAL, 102–104
DYNAMIC DRAW, 23, 24                           Get, 19, 28, 117, 118
                                               GetBooleanv, 102, 117, 118, 121
ELEMENT ARRAY BUFFER, 26                       GetBufferParameter, 119
EMISSION, 43                                   GetBufferParameteriv, 119
Enable, 33, 35, 37, 44, 50–52, 57, 63, 65,     GetClipPlane, 119
          95, 97, 101–105, 107, 117            GetClipPlanef, 154, 156
EnableClientState, 20, 21                      GetClipPlanex, 154
EQUAL, 102–104                                 GetError, 12
EQUIV, 108                                     GetFixedv, 117, 118, 121, 153–155, 157,
EXP, 97, 98, 129                                         160
EXP2, 97




                            Version 1.1.12 (April 24, 2008)
INDEX                                                                     166


GetFloatv, 8, 102, 117, 118, 121, 154,    LIGHT MODEL AMBIENT, 43
          155, 157                        LIGHT MODEL TWO SIDE, 43
GetIntegerv, 50, 111, 117, 118, 121, 157  Lightf, 154
GetLight, 119                             Lightfv, 154
GetLightfv, 154                           LIGHTING, 38
GetLightxv, 153, 154                      LightModel, 42, 43
GetMaterial, 119                          LightModelf, 154
GetMaterialfv, 154                        LightModelfv, 154
GetMaterialxv, 154                        LightModelx, 154
GetPointerv, 120                          LightModelxv, 154
GetString, 120                            Lightx, 154
GetTexEnv, 119                            Lightxv, 154
GetTexEnvfv, 154                          LINE LOOP, 17
GetTexEnvxv, 154                          LINE SMOOTH, 57, 62
GetTexParameter, 119                      LINE SMOOTH HINT, 116
GetTexParameterfv, 154                    LINE STRIP, 14
GetTexParameterxv, 154                    LINEAR, 82, 85–89, 97
GREATER, 102–104                          LINEAR ATTENUATION, 43
GREEN, 144                                LINEAR MIPMAP LINEAR, 82, 86,
                                                    87
Hint, 115                                 LINEAR MIPMAP NEAREST, 82, 86
                                          LINES, 17
IMPLEMENTATION COLOR READ FORMATLineWidth, OES,       57, 154, 155
          111                             LineWidthx, 57, 154
IMPLEMENTATION COLOR READ TYPE OES,       LoadIdentity, 29
          111                             LoadMatrix, 29
INCR, 103                                 LoadMatrixf, 154
INTERPOLATE, 93                           LoadMatrixx, 154
INVALID ENUM, 12, 13, 21, 32, 42          LogicOp, 107, 108
INVALID OPERATION, 13, 69, 73, 76,        LUMINANCE, 68, 69, 71, 73, 76, 91,
          79, 80, 82                                92, 113
INVALID VALUE, 12, 13, 20, 22, 25,        LUMINANCE ALPHA, 68, 69, 71, 73,
          28, 31, 42, 51, 52, 57, 66, 73,           76, 91, 92, 113
          74, 77–80, 82, 90, 97, 101, 110
INVERT, 103, 108                          m, 158
IsBuffer, 120                             Material, 42, 43, 150
IsEnabled, 101, 117, 121                  Materialf, 154
IsTexture, 120                            Materialfv, 154
                                          Materialx, 154
KEEP, 103, 137
                                          Materialxv, 154
LEQUAL, 102–104                           MATRIX MODE, 156
LESS, 102–104, 137                        MATRIX     PALETTE OES, 156
Light, 42, 43                             MatrixMode,   29
LIGHTi, 42, 44, 151                       MAX    TEXTURE     SIZE, 74
LIGHT0, 42                                MAX    TEXTURE     UNITS, 13, 19, 22




                           Version 1.1.12 (April 24, 2008)
INDEX                                                                167


MODELVIEW, 29, 32, 33                 OES fixed point, 153, 155
MODELVIEW MATRIX, 128                 OES matrix get, 153, 155
MODELVIEW MATRIX FLOAT AS INT BITSOES  OES,matrix palette, 153, 155, 156
         118, 157                     OES point size array, 153, 155, 157
MODULATE, 90, 92, 93, 95, 136         OES point sprite, 153, 155, 156
MULTISAMPLE, 50, 51, 56, 62, 65,      OES query matrix, 153
         101, 107, 108                OES read format, 153, 155, 156
MultiTexCoord, 21, 32                 OES single precision, 153, 155
MultiTexCoord4, 19                    OES single precision commands, 155
MultiTexCoord4f, 154                  ONE, 106, 137, 161
MultiTexCoord4x, 154                  ONE MINUS DST ALPHA, 106
MultMatrix, 29, 30                    ONE MINUS DST COLOR, 105, 106
MultMatrixf, 154                      ONE MINUS SRC ALPHA, 94, 106
MultMatrixx, 154                      ONE MINUS SRC COLOR, 94, 105,
                                                106
n, 158                                OPERANDn ALPHA, 91, 94, 95
NAND, 108                             OPERANDn RGB, 91, 94, 95
NEAREST, 82, 85–87                    OR, 108
NEAREST MIPMAP LINEAR, 82, 86–        OR INVERTED, 108
         89                           OR REVERSE, 108
NEAREST MIPMAP NEAREST, 82,           Ortho, 30, 31, 151, 155
         86, 88                       Orthof, 154, 156
NEVER, 102–104                        Orthox, 154
NICEST, 116                           OUT OF MEMORY, 12, 13, 25
NO ERROR, 12
NOOP, 108                             PACK ALIGNMENT, 112, 139
NOR, 108                              PALETTE*, 82
Normal, 21                            PALETTE4 *, 81
Normal3, 9, 19                        PALETTE4 R5 G6 B5, 80
Normal3f, 9, 152, 154                 PALETTE4 R5 G6 B5 OES, 79, 81
Normal3x, 9, 154                      PALETTE4 RGB5 A1, 80
NORMAL ARRAY, 20                      PALETTE4 RGB5 A1 OES, 79, 81
NORMAL ARRAY BUFFER BINDING,          PALETTE4 RGB8, 80
         25                           PALETTE4 RGB8 OES, 79, 81
NORMAL ARRAY POINTER, 120             PALETTE4 RGBA4, 80
NORMALIZE, 33                         PALETTE4 RGBA4 OES, 79, 81
NormalPointer, 19, 20, 25, 154        PALETTE4 RGBA8, 80
NOTEQUAL, 102–104                     PALETTE4 RGBA8 OES, 79, 81
NUM COMPRESSED TEXTURE FORMATS, PALETTE8 *, 81
         78                           PALETTE8 R5 G6 B5, 80
                                      PALETTE8 R5 G6 B5 OES, 79, 81
OES byte coordinates, 153, 155        PALETTE8 RGB5 A1, 80
OES compressed paletted texture, 153, PALETTE8 RGB5 A1 OES, 79, 81
         155, 156                     PALETTE8 RGB8, 80
OES draw texture, 153, 155, 157       PALETTE8 RGB8 OES, 79, 81




                      Version 1.1.12 (April 24, 2008)
INDEX                                                                       168


PALETTE8 RGBA4, 80                       RENDERER, 120
PALETTE8 RGBA4 OES, 79, 81               REPEAT, 82, 83, 85, 89, 135
PALETTE8 RGBA8, 80                       REPLACE, 90, 92, 93, 103
PALETTE8 RGBA8 OES, 79, 81               RESCALE NORMAL, 33
PERSPECTIVE CORRECTION HINT,             RGB, 68–71, 73, 76, 79, 81, 91, 92, 95,
          116                                      106, 113
PixelStore, 66, 112, 114                 RGB SCALE, 90, 91, 95, 160
PixelStorei, 66                          RGBA, 68–71, 73, 76, 79, 81, 91, 92,
POINT DISTANCE ATTENUATION,                        111, 113
          52                             Rotate, 30, 151
POINT FADE THRESHOLD SIZE, 52            Rotatef, 154
POINT SIZE ARRAY OES, 20                 Rotatex, 154
POINT SIZE ARRAY POINTER OES,
          120                            SAMPLE ALPHA TO COVERAGE,
POINT SIZE MAX, 52                                 101
POINT SIZE MIN, 52                       SAMPLE     ALPHA TO ONE, 101
POINT SMOOTH, 52, 56                     SAMPLE     BUFFERS, 50, 56, 62, 65,
POINT SMOOTH HINT, 116                             101, 107, 108, 110
POINT SPRITE OES, 51, 52, 56, 57         SAMPLE COVERAGE, 101
PointParameter, 51, 52                   SAMPLE COVERAGE INVERT, 101,
PointParameterf, 154                               102
PointParameterfv, 154                    SAMPLE COVERAGE VALUE, 101,
PointParameterx, 154                               102
PointParameterxv, 154                    SampleCoverage, 102, 154
POINTS, 14                               SampleCoveragex, 102, 154
PointSize, 21, 51, 154, 155, 157         SAMPLES, 50, 51
PointSizePointerOES, 20                  Scale, 30, 151
PointSizex, 51, 154                      Scalef, 154
POLYGON OFFSET FILL, 65                  Scalex, 154
PolygonOffset, 64, 154                   Scissor, 100
PolygonOffsetx, 64, 154                  SCISSOR TEST, 101
PopMatrix, 32                            SET, 108
POSITION, 43, 119                        ShadeModel, 45
PREVIOUS, 94, 95, 136                    SHININESS, 43
PRIMARY COLOR, 94                        SHORT, 20
PROJECTION, 29, 32                       SMOOTH, 45, 129
PROJECTION MATRIX, 128                   SPECULAR, 43
PROJECTION MATRIX FLOAT AS INT BITSSPOT   OES, CUTOFF, 43
          118, 157                       SPOT DIRECTION, 43, 119
PushMatrix, 32                           SPOT EXPONENT, 43
                                         SRC ALPHA, 94, 95, 106, 136
QUADRATIC ATTENUATION, 43                SRC ALPHA SATURATE, 105, 106
                                         SRC COLOR, 94, 95, 105, 106, 136
ReadPixels, 65, 66, 68, 76, 111–113, 156 SRCn ALPHA, 91, 94, 95
RED, 144                                 SRCn RGB, 91, 94, 95




                        Version 1.1.12 (April 24, 2008)
INDEX                                                                       169


STACK OVERFLOW, 13, 32                   Translatef, 154
STACK UNDERFLOW, 13, 32                  Translatex, 154
STATIC DRAW, 23, 24                      TRIANGLE FAN, 18
STENCIL BUFFER BIT, 110, 111             TRIANGLE STRIP, 17
STENCIL TEST, 103                        TRIANGLES, 18
StencilFunc, 103, 150                    TRUE, 41, 52, 54, 82, 87, 102, 109, 118,
StencilMask, 109, 110, 150                         120, 162
StencilOp, 103
SUBTRACT, 93                             UNPACK ALIGNMENT, 66, 69, 139
                                         UNSIGNED BYTE, 20, 22, 68, 69, 81,
TexCoordPointer, 20, 21, 154                   111, 114
TexEnv, 51, 52, 90, 95                   UNSIGNED SHORT, 22, 70
TexEnvf, 154                             UNSIGNED SHORT 4 4 4 4, 68–70,
TexEnvfv, 154                                  81, 114
TexEnvx, 154                             UNSIGNED SHORT 5 5 5 1, 68–70,
TexEnvxv, 154                                  81, 114
TexImage, 77                             UNSIGNED SHORT 5 6 5, 68–70, 81,
TexImage2D, 65, 66, 68, 69, 72–74, 76–         114
          78, 82, 86, 111, 113
TexParameter, 82                       VENDOR, 120
TexParameterf, 154                     VERSION, 120
TexParameterfv, 154                    VERSION ES CL n m, 158
TexParameterx, 154                     VERSION ES CM n m, 158
TexParameterxv, 154                    VERTEX ARRAY, 20
TexSubImage, 77                        VERTEX ARRAY POINTER, 120
TexSubImage2D, 66, 76, 77, 80          VertexPointer, 19, 20, 154
TEXTURE, 29, 32, 94, 95, 136           Viewport, 28
TEXTUREi, 19
TEXTURE0, 19, 22, 33, 125, 136         XOR, 108
TEXTURE 2D, 72, 76, 77, 82, 89, 95,
                                       ZERO, 103, 106, 137
          119, 134
TEXTURE COORD ARRAY, 20, 21
TEXTURE COORD ARRAY POINTER,
          120
TEXTURE ENV, 90, 119
TEXTURE ENV COLOR, 90
TEXTURE ENV MODE, 90, 91, 95
TEXTURE MAG FILTER, 82, 87, 89
TEXTURE MATRIX, 128
TEXTURE MATRIX FLOAT AS INT BITS OES,
          118, 157
TEXTURE MIN FILTER, 82, 85–89
TEXTURE WRAP S, 82, 83, 85
TEXTURE WRAP T, 82, 83, 85
Translate, 30, 151




                      Version 1.1.12 (April 24, 2008)
