The OpenGL Graphics System Utility Library
             R


            Version 1.3

                    Norman Chin
                     Chris Frazier
                       Paul Ho
                     Zicheng Liu
                    Kevin P. Smith
          Editor version 1.3: Jon Leech




         Version 1.3 - 4 November 1998
             Copyright c 1992-1998 Silicon Graphics, Inc.

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




                              Version 1.3 - 4 November 1998
Contents
1 Overview                                                                                                                  1
2 Initialization                                                                                                            2
3 Mipmapping                                                                                                                4
   3.1 Image Scaling . . . . . . . . . . . . . . . . . . . . . . . . . . .                                                  4
   3.2 Automatic Mipmapping . . . . . . . . . . . . . . . . . . . . .                                                       5
4 Matrix Manipulation                                                                                                       7
   4.1 Matrix Setup . . . . . . . . . . . . . . . . . . . . . . . . . . .                                                   7
   4.2 Coordinate Projection . . . . . . . . . . . . . . . . . . . . . .                                                    9
5 Polygon Tessellation                                                                                                     10
   5.1 The Tessellation Object . . . . . . . . . . . . . . . . . .                                             .   .   .   10
   5.2 Polygon De nition . . . . . . . . . . . . . . . . . . . . .                                             .   .   .   11
   5.3 Callbacks . . . . . . . . . . . . . . . . . . . . . . . . . .                                           .   .   .   12
   5.4 Control Over Tessellation . . . . . . . . . . . . . . . . .                                             .   .   .   14
   5.5 CSG Operations . . . . . . . . . . . . . . . . . . . . . .                                              .   .   .   16
       5.5.1 UNION . . . . . . . . . . . . . . . . . . . . . . .                                               .   .   .   17
       5.5.2 INTERSECTION two polygons at a time only                                                        .   .   .   17
       5.5.3 DIFFERENCE . . . . . . . . . . . . . . . . . . .                                                  .   .   .   17
   5.6 Performance . . . . . . . . . . . . . . . . . . . . . . . . .                                           .   .   .   17
   5.7 Backwards Compatibility . . . . . . . . . . . . . . . . .                                               .   .   .   18
6 Quadrics                                                                                                                 20
   6.1   The Quadrics Object .     .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   20
   6.2   Callbacks . . . . . . .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   20
   6.3   Rendering Styles . . .    .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   21
   6.4   Quadrics Primitives .     .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   22
                                               i



                              Version 1.3 - 4 November 1998
ii                                                                                                         CONTENTS

7 NURBS                                                                                                                        24
     7.1   The NURBS Object        .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   24
     7.2   Callbacks . . . . . .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   25
     7.3   NURBS Curves . . .      .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   27
     7.4   NURBS Surfaces . .      .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   27
     7.5   Trimming . . . . . .    .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   28
     7.6   NURBS Properties .      .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   .   29
8 Errors                                                                                                                       33
9 GLU Versions                                                                                                                 34
     9.1 GLU 1.1 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 34
     9.2 GLU 1.2 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 35
     9.3 GLU 1.3 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 35
     Index of GLU Commands                                                                                                     36




                     Version 1.3 - 4 November 1998
Chapter 1

Overview
The GL Utilities GLU library is a set of routines designed to comple-
ment the OpenGL graphics system by providing support for mipmapping,
matrix manipulation, polygon tessellation, quadrics, NURBS, and error han-
dling. Mipmapping routines include image scaling and automatic mipmap
generation. A variety of matrix manipulation functions build projection and
viewing matrices, or project vertices from one coordinate system to another.
Polygon tessellation routines convert concave polygons into triangles for easy
rendering. Quadrics support renders a few basic quadrics such as spheres
and cones. NURBS code maps complicated NURBS curves and trimmed
surfaces into simpler OpenGL evaluators. Lastly, an error lookup routine
translates OpenGL and GLU error codes into strings. GLU library rou-
tines may call OpenGL library routines. Thus, an OpenGL context should
be made current before calling any GLU functions. Otherwise an OpenGL
error may occur.
    All GLU routines, except for the initialization routines listed in Section 2,
may be called during display list creation. This will cause any OpenGL com-
mands that are issued as a result of the call to be stored in the display list.
The result of calling the intialization routines after glNewList is unde ned.




                                       1



                               Version 1.3 - 4 November 1998
Chapter 2

Initialization
To get the GLU version number or supported GLU extensions call:
     const GLubyte     *gluGetString GLenum name ;
    If name is GLU VERSION or GLU EXTENSIONS, then a pointer to a static
zero-terminated string that describes the version or available extensions re-
spectively is returned; otherwise NULL is returned.
    The version string is laid out as follows:
      version number space vendor-speci c information
version number is either of the form major number.minor number or ma-
jor number.minor number.release number, where the numbers all have one
or more digits. The version number determines which interfaces are pro-
vided by the GLU client library. If the underlying OpenGL implementation
is an older version than that corresponding to this version of GLU, some of
the GL calls made by GLU may fail. Chapter 9 describes how GLU versions
and OpenGL versions correspond.
    The vendor speci c information is optional. However, if it is present the
format and contents are implementation dependent.
    The extension string is a space separated list of extensions to the GLU
library. The extension names themselves do not contain any spaces. To
determine if a speci c extension name is present in the extension string, call
     GLboolean    gluCheckExtension char *extName,
        const GLubyte     *extString ;
where extName is the extension name to check, and extString is the exten-
sion string. GL TRUE is returned if extName is present in extString, GL FALSE
                                      2



                   Version 1.3 - 4 November 1998
                                                                           3

otherwise. gluCheckExtension correctly handles boundary cases where
one extension name is a substring of another. It may also be used to check-
ing for the presence of OpenGL or GLX extensions by passing the extension
strings returned by glGetString or glXGetClientString, instead of the
GLU extension string.
    gluGetString is not available in GLU 1.0. One way to determine
whether this routine is present when using the X Window System is to
query the GLX version. If the client version is 1.1 or greater then this rou-
tine is available. Operating system dependent methods may also be used to
check for the existence of this function.




                              Version 1.3 - 4 November 1998
Chapter 3

Mipmapping
GLU provides image scaling and automatic mipmapping functions to sim-
plify the creation of textures. The image scaling function can scale any
image to a legal texture size. The resulting image can then be passed to
OpenGL as a texture. The automatic mipmapping routines will take an in-
put image, create mipmap textures from it, and pass them to OpenGL. With
this interface, the user need only supply an image and the rest is automatic.

3.1 Image Scaling
The following routine magni es or shrinks an image:
     int   gluScaleImage  GLenum format, GLsizei widthin,
        GLsizei heightin, GLenum typein, const void *datain,
        GLsizei widthout, GLsizei heightout, GLenum typeout,
        void *dataout ;

   gluScaleImage will scale an image using the appropriate pixel store
modes to unpack data from the input image and pack the result into the
output image. format speci es the image format used by both images. The
input image is described by widthin, heightin, typein, and datain, where
widthin and heightin specify the size of the image, typein speci es the data
type used, and datain is a pointer to the image data in memory. The output
image is similarly described by widthout, heightout, typeout, and dataout,
where widthout and heightout specify the desired size of the image, typeout
speci es the desired data type, and dataout points to the memory location
where the image is to be stored. The pixel formats and types supported are
                                      4



                   Version 1.3 - 4 November 1998
3.2. AUTOMATIC MIPMAPPING                                                 5

the same as those supported by glDrawPixels for the underlying OpenGL
implementation.
    gluScaleImage reconstructs the input image by linear interpolation,
convolves it with a one-pixel-square box kernel, and then samples the result
to produce the output image.
    A return value of 0 indicates success. Otherwise the return value is a
GLU error code indicating the cause of the problem see gluErrorString
below.

3.2 Automatic Mipmapping
These routines will automatically generate mipmaps for any image provided
by the user and then pass them to OpenGL:
     int  gluBuild1DMipmaps     GLenum target,
        GLint internalFormat, GLsizei width, GLenum          format,
        GLenum type, const void *data ;

     int  gluBuild2DMipmaps     GLenum target,
        GLint internalFormat, GLsizei width, GLsizei height,
        GLenum format, GLenum type, const void *data ;

     int  gluBuild3DMipmaps     GLenum target,
        GLint internalFormat, GLsizei width, GLsizei          height,
        GLsizei depth, GLenum format, GLenum type,
        const void *data ;

   gluBuild1DMipmaps,        gluBuild2DMipmaps,            and
gluBuild3DMipmaps all take an input image and derive from it a
pyramid of scaled images suitable for use as mipmapped textures. The
resulting textures are then passed to glTexImage1D, glTexImage2D,
or glTexImage3D as appropriate. target, internalFormat, format, type,
width, height, depth, and data de ne the level 0 texture, and have the same
meaning as the corresponding arguments to glTexImage1D, glTexIm-
age2D, and glTexImage3D. Note that the image size does not need to be
a power of 2, because the image will be automatically scaled to the nearest
power of 2 size if necessary.
    To load only a subset of mipmap levels, call
     int  gluBuild1DMipmapLevels GLenum target,
        GLint   internalFormat, GLsizei width, GLenum format,




                             Version 1.3 - 4 November 1998
6                                            CHAPTER 3. MIPMAPPING

         GLenum type, GLint level, GLint    base, GLint max,
         const void *data ;

     int   gluBuild2DMipmapLevels     GLenum target,
        GLint internalFormat, GLsizei width, GLsizei height,
        GLenum format, GLenum type, GLint level, GLint base,
        GLint max, const void *data ;

     int   gluBuild3DMipmapLevels    GLenum target,
        GLint internalFormat, GLsizei width, GLsizei height,
        GLsizei depth, GLenum format, GLenum type, GLint level,
        GLint base, GLint max, const void *data ;

     level speci es the mipmap level of the input image. base and
max determine the minimum and maximum mipmap levels which will
be passed to glTexImagexD. Other parameters are the same as for
gluBuildxDMipmaps. If level base, base 0, max base, or max
is larger than the highest mipmap level for a texture of the speci ed size, no
mipmap levels will be loaded, and the calls will return GLU INVALID VALUE.
     A return value of 0 indicates success. Otherwise the return value is a
GLU error code indicating the cause of the problem.




                   Version 1.3 - 4 November 1998
Chapter 4

Matrix Manipulation
The GLU library includes support for matrix creation and coordinate pro-
jection transformation. The matrix routines create matrices and multiply
the current OpenGL matrix by the result. They are used for setting projec-
tion and viewing parameters. The coordinate projection routines are used
to transform object space coordinates into screen coordinates or vice-versa.
This makes it possible to determine where in the window an object is being
drawn.

4.1 Matrix Setup
The following routines create projection and viewing matrices and apply
them to the current matrix using glMultMatrix. With these routines, a
user can construct a clipping volume and set viewing parameters to render
a scene.
    gluOrtho2D and gluPerspective build commonly-needed projection
matrices.
     void   gluOrtho2D GLdouble left, GLdouble right,
        GLdouble   bottom, GLdouble top ;
   sets up a two dimensional orthographic viewing region. The pa-
rameters de ne the bounding box of the region to be viewed. Call-
ing gluOrtho2Dleft, right, bottom, top is equivalent to calling
glOrtholeft, right, bottom, top, ,1, 1.
     void   gluPerspective GLdouble fovy, GLdouble aspect,
        GLdouble   near, GLdouble far ;

                                     7



                             Version 1.3 - 4 November 1998
8                               CHAPTER 4. MATRIX MANIPULATION

    sets up a perspective viewing volume. fovy de nes the eld-of-view angle
in degrees in the y direction. aspect is the aspect ratio used to determine
the eld-of-view in the x direction. It is the ratio of x width to y height.
near and far de ne the near and far clipping planes as positive distances
from the eye point.
    gluLookAt creates a commonly-used viewing matrix:
      void  gluLookAt GLdouble eyex, GLdouble eyey,
         GLdouble   eyez, GLdouble centerx, GLdouble centery,
         GLdouble   centerz, GLdouble upx, GLdouble upy,
         GLdouble   upz ;

    The viewing matrix created is based on an eye point eyex,eyey,eyez,
a reference point that represents the center of the scene cen-
terx,centery,centerz, and an up vector upx,upy,upz. The matrix is de-
signed to map the center of the scene to the negative Z axis, so that when
a typical projection matrix is used, the center of the scene will map to the
center of the viewport. Similarly, the projection of the up vector on the
viewing plane is mapped to the positive Y axis so that it will point upward
in the viewport. The up vector must not be parallel to the line-of-sight from
the eye to the center of the scene.
    gluPickMatrix is designed to simplify selection by creating a matrix
that restricts drawing to a small region of the viewport. This is typically used
to determine which objects are being drawn near the cursor. First restrict
drawing to a small region around the cursor, then rerender the scene with
selection mode turned on. All objects that were being drawn near the cursor
will be selected and stored in the selection bu er.

      void  gluPickMatrix   GLdouble x, GLdouble y,
         GLdouble deltax, GLdouble deltay,
         const GLint viewport 4 ;


    gluPickMatrix should be called just before applying a projection ma-
trix to the stack e ectively pre-multiplying the projection matrix by the
selection matrix. x and y specify the center of the selection bounding
box in pixel coordinates; deltax and deltay specify its width and height
in pixels. viewport should specify the current viewport's x, y, width, and
height. A convenient way to obtain this information is to call glGetInte-
gervGL VIEWPORT, viewport.




                    Version 1.3 - 4 November 1998
4.2. COORDINATE PROJECTION                                                9

4.2 Coordinate Projection
Two routines are provided to project coordinates back and forth from ob-
ject space to screen space. gluProject projects from object space to screen
space, and gluUnProject does the reverse. gluUnProject4 should be
used instead of gluUnProject when a nonstandard glDepthRange is in
e ect, or when a clip-space w coordinate other than 1 needs to be spec-
i ed, as for vertices in the OpenGL glFeedbackBu er when data type
GL 4D COLOR TEXTURE is returned.

      int gluProject GLdouble objx, GLdouble objy,
          GLdouble objz, const GLdouble modelMatrix 16 ,
          const GLdouble projMatrix 16 , const GLint viewport 4 ,
          GLdouble *winx, GLdouble *winy, GLdouble *winz ;

    gluProject performs the projection with the given modelMatrix, pro-
jectionMatrix, and viewport. The format of these arguments is the same as
if they were obtained from glGetDoublev and glGetIntegerv. A return
value of GL TRUE indicates success, and GL FALSE indicates failure.
      int gluUnProject GLdouble winx, GLdouble winy,
          GLdouble winz, const GLdouble modelMatrix 16 ,
          const GLdouble projMatrix 16 , const GLint viewport 4 ,
          GLdouble *objx, GLdouble *objy, GLdouble *objz ;

    gluUnProject uses the given modelMatrix, projectionMatrix, and view-
port to perform the projection. A return value of GL TRUE indicates success,
and GL FALSE indicates failure.
      int gluUnProject4 GLdouble winx, GLdouble winy,
          GLdouble winz, GLdouble clipw,
          const GLdouble modelMatrix 16 ,
          const GLdouble projMatrix 16 , const GLint viewport 4 ,
          GLclampd near, GLclampd far, GLdouble *objx,
          GLdouble *objy, GLdouble *objz, GLdouble *objw ;

    gluUnProject4 takes three additional parameters and returns one ad-
ditional parameter clipw is the clip-space w coordinate of the screen-space
vertex e.g. the wc value computed by OpenGL; normally, clipw = 1. near
and far correspond to the current glDepthRange; normally, near = 0 and
far = 1. The object-space w value of the unprojected vertex is returned in
objw. Other parameters are the same as for gluUnProject.




                             Version 1.3 - 4 November 1998
Chapter 5

Polygon Tessellation
The polygon tessellation routines triangulate concave polygons with one or
more closed contours. Several winding rules are supported to determine
which parts of the polygon are on the interior". In addition, boundary
extraction is supported: instead of tessellating the polygon, a set of closed
contours separating the interior from the exterior are generated.
    To use these routines, rst create a tessellation object. Second, de ne the
callback routines and the tessellation parameters. The callback routines are
used to process the triangles generated by the tessellator. Finally, specify
the concave polygon to be tessellated.
    Input contours can be intersecting, self-intersecting, or degenerate. Also,
polygons with multiple coincident vertices are supported.

5.1 The Tessellation Object
A new tessellation object is created with gluNewTess:
     GLUtesselator *tessobj;
     tessobj =    gluNewTessvoid;
   gluNewTess returns a new tessellation object, which is used by the
other tessellation functions. A return value of 0 indicates an out-of-memory
error. Several tessellator objects can be used simultaneously.
    When a tessellation object is no longer needed, it should be deleted with
gluDeleteTess:
      void gluDeleteTess GLUtesselator *tessobj ;

    This will destroy the object and free any memory used by it.
                                          10



                   Version 1.3 - 4 November 1998
5.2. POLYGON DEFINITION                                                            11

5.2 Polygon De nition
The input contours are speci ed with the following routines:

      void  gluTessBeginPolygon     GLUtesselator *tess,
         void *polygon data ;
      void  gluTessBeginContour     GLUtesselator *tess ;
      void  gluTessVertex   GLUtesselator *tess,
         GLdouble coords 3 , void *vertex data ;
      void  gluTessEndContour     GLUtesselator *tess ;
      void  gluTessEndPolygon     GLUtesselator *tess ;

    Within each gluTessBeginPolygon gluTessEndPolygon pair,
there must be one or more calls to gluTessBeginContour gluTessEnd-
Contour. Within each contour, there are zero or more calls to gluTessVer-
tex. The vertices specify a closed contour the last vertex of each contour
is automatically linked to the rst.
    polygon data is a pointer to a user-de ned data structure. If the appro-
priate callbacks are speci ed see section 5.3, then this pointer is returned
to the callback functions. Thus, it is a convenient way to store per-polygon
information.
    coords give the coordinates of the vertex in 3-space. For useful results,
all vertices should lie in some plane, since the vertices are projected onto a
plane before tessellation. vertex data is a pointer to a user-de ned vertex
structure, which typically contains other vertex information such as color,
texture coordinates, normal, etc. It is used to refer to the vertex during
rendering.
    When gluTessEndPolygon is called, the tessellation algorithm deter-
mines which regions are interior to the given contours, according to one
of several winding rules" described below. The interior regions are then
tessellated, and the output is provided as callbacks.
    gluTessBeginPolygon indicates the start of a polygon, and it must
be called rst. It is an error to call gluTessBeginContour outside of a
gluTessBeginPolygon gluTessEndPolygon pair; it is also an error to
call gluTessVertex outside of a gluTessBeginContour gluTessEnd-
Contour pair. In addition, gluTessBeginPolygon gluTessEndPoly-
gon and gluTessBeginContour gluTessEndContour calls must pair
up.




                               Version 1.3 - 4 November 1998
12                            CHAPTER 5. POLYGON TESSELLATION

5.3 Callbacks
Callbacks are speci ed with gluTessCallback:
     void   gluTessCallback GLUtesselator *tessobj,
        GLenum   which, void *fn ;
    This routine replaces the callback selected by which with the function
speci ed by fn. If fn is equal to NULL, then any previously de ned call-
back is discarded and becomes unde ned. Any of the callbacks may be left
unde ned; if so, the corresponding information will not be supplied during
rendering. Note that, under some conditions, it is an error to leave the
combine callback unde ned. See the description of this callback below for
details.
    It is legal to leave any of the callbacks unde ned. However, the informa-
tion that they would have provided is lost.
    which may be one of GLU TESS BEGIN, GLU TESS EDGE FLAG,
GLU TESS VERTEX,        GLU TESS END,     GLU TESS ERROR,     GLU TESS COMBINE,
GLU TESS BEGIN DATA,        GLU TESS EDGE FLAG DATA,      GLU TESS VERTEX DATA,
GLU TESS END DATA, GLU TESS ERROR DATA or GLU TESS COMBINE DATA. The
twelve callbacks have the following prototypes:
     void   begin GLenum type ;
     void   edgeFlag  GLboolean ag ;
     void   vertex void *vertex data ;
     void   end
               void ;
     void   error
                 GLenum errno ;
     void   combine  GLdouble coords 3 , void *vertex data 4 ,
        GLfloat weight 4 , void **outData ;
     void   beginData    GLenum type, void *polygon data ;
     void   edgeFlagData      GLboolean ag, void *polygon data ;
     void   endData   void *polygon data ;
     void   vertexData    void *vertex data, void *polygon data ;
     void   errorData   GLenum errno, void *polygon data ;
     void   combineData      GLdouble coords 3 ,
        void *vertex data 4 , GLfloat weight 4 , void **outDatab,
        void *polygon data ;

   Note that there are two versions of each callback: one with user-speci ed
polygon data and one without. If both versions of a particular callback are




                   Version 1.3 - 4 November 1998
5.3. CALLBACKS                                                                13

speci ed then the callback with polygon data will be used. Note that poly-
gon data is a copy of the pointer that was speci ed when gluTessBegin-
Polygon was called.
     The begin callbacks indicate the start of a primitive. type is one of
GL TRIANGLE FAN, GL TRIANGLE STRIP, or GL TRIANGLES but see the description
of the edge ag callbacks below and the notes on boundary extraction in
section 5.4 where the GLU TESS BOUNDARY ONLY property is described.
     It is followed by any number of vertex callbacks, which supply the ver-
tices in the same order as expected by the corresponding glBegin call. ver-
tex data is a copy of the pointer that the user provided when the vertex was
speci ed see gluTessVertex. After the last vertex of a given primitive,
the end or endData callback is called.
     If one of the edge ag callbacks is provided, no triangle fans or strips will
be used. When edgeFlag or edgeFlagData is called, if ag is GL TRUE, then
each vertex which follows begins an edge which lies on the polygon boundary
i.e., an edge which separates an interior region from an exterior one. If
  ag is GL FALSE, each vertex which follows begins an edge which lies in the
polygon interior. The edge ag callback will be called before the rst call
to the vertex callback.
     The error or errorData callback is invoked when an error is encoun-
tered. The errno will be set to one of GLU TESS MISSING BEGIN POLYGON,
GLU TESS MISSING END POLYGON,                 GLU TESS MISSING BEGIN CONTOUR,
GLU TESS MISSING END CONTOUR,             GLU TESS COORD TOO LARGE,           or
GLU TESS NEED COMBINE CALLBACK.
     The rst four errors are self-explanatory. The GLU library will recover
from these errors by inserting the missing calls. GLU TESS COORD TOO LARGE
says that some vertex coordinate exceeded the prede ned constant
GLU TESS MAX COORD TOO LARGE in absolute value, and that the value has been
clamped. Coordinate values must be small enough so that two can be
multiplied together without over ow. GLU TESS NEED COMBINE CALLBACK says
that the algorithm detected an intersection between two edges in the input
data, and the combine callback below was not provided. No output will
be generated.
     The combine or combineData callback is invoked to create a new ver-
tex when the algorithm detects an intersection, or wishes to merge features.
The vertex is de ned as a linear combination of up to 4 existing vertices, ref-
erenced by vertex data 0..3 . The coe cients of the linear combination are
given by weight 0..3 ; these weights always sum to 1.0. All vertex pointers
are valid even when some of the weights are zero. coords gives the location
of the new vertex.




                               Version 1.3 - 4 November 1998
14                                CHAPTER 5. POLYGON TESSELLATION

    The user must allocate another vertex, interpolate parameters using ver-
tex data and weights, and return the new vertex pointer in outData. This
handle is supplied during rendering callbacks. For example, if the polygon
lies in an arbitrary plane in 3-space, and we associate a color with each
vertex, the combine callback might look like this:
      void MyCombineGLdouble coords 3 , VERTEX *d 4 ,
           GLfloat w 4 , VERTEX **dataOut;
      f
            VERTEX *new = new vertex;

            new-   x   =   coords   0   ;
            new-   y   =   coords   1   ;
            new-   z   =   coords   2   ;
            new-   r   =   w 0 *d   0   -   r   +   w   1   *d   1   -   r +
                           w 2 *d   2   -   r   +   w   3   *d   3   -   r;
            new- g =       w 0 *d   0   -   g   +   w   1   *d   1   -   g +
                           w 2 *d   2   -   g   +   w   3   *d   3   -   g;
            new- b =       w 0 *d   0   -   b   +   w   1   *d   1   -   b +
                           w 2 *d   2   -   b   +   w   3   *d   3   -   b;
            new- a =       w 0 *d   0   -   a   +   w   1   *d   1   -   a +
                           w 2 *d   2   -   a   +   w   3   *d   3   -   a;
            *dataOut       = new;
      g

   If the algorithm detects an intersection, then the combine or com-
bineData callback must be de ned, and it must write a non-NULL pointer
into dataOut. Otherwise the GLU TESS NEED COMBINE CALLBACK error occurs,
and no output is generated. This is the only error that can occur during
tessellation and rendering.

5.4 Control Over Tessellation
The properties associated with a tessellator object a ect the way the poly-
gons are interpreted and rendered. The properties are set by calling:
     void   gluTessProperty GLUtesselator tess, GLenum which,
        GLdouble       value ;




                   Version 1.3 - 4 November 1998
5.4. CONTROL OVER TESSELLATION                                            15

    which indicates the property to be modi ed and must be set to one of
GLU TESS WINDING RULE, GLU TESS BOUNDARY ONLY,    or GLU TESS TOLERANCE.
    value speci es the new property
    The GLU TESS WINDING RULE property determines which parts of
the polygon are on the interior. It is an enumerated value; the
possible values are: GLU TESS WINDING ODD, GLU TESS WINDING NONZERO,
GLU TESS WINDING NEGATIVE,            GLU TESS WINDING POSITIVE           and
GLU TESS WINDING ABS GEQ TWO.
    To understand how the winding rule works rst consider that the input
contours partition the plane into regions. The winding rule determines which
of these regions are inside the polygon.
    For a single contour C , the winding number of a point x is simply the
signed number of revolutions we make around x as we travel once around
C , where counter-clockwise CCW is positive. When there are several
contours, the individual winding numbers are summed. This procedure as-
sociates a signed integer value with each point x in the plane. Note that the
winding number is the same for all points in a single region.
    The winding rule classi es a region as inside if its winding number be-
longs to the chosen category odd, nonzero, positive, negative, or absolute
value of at least two. The previous GLU tessellator prior to GLU 1.2
used the odd rule. The nonzero rule is another common way to de ne the
interior. The other three rules are useful for polygon CSG operations see
below.
    The GLU TESS BOUNDARY ONLY property is a boolean value value should
be set to GL TRUE or GL FALSE. When set to GL TRUE, a set of closed con-
tours separating the polygon interior and exterior are returned instead of a
tessellation. Exterior contours are oriented CCW with respect to the nor-
mal, interior contours are oriented clockwise CW. The GLU TESS BEGIN and
GLU TESS BEGIN DATA callbacks use the type GL LINE LOOP for each contour.
    GLU TESS TOLERANCE speci es a tolerance for merging features to reduce
the size of the output. For example, two vertices which are very close to
each other might be replaced by a single vertex. The tolerance is multiplied
by the largest coordinate magnitude of any input vertex; this speci es the
maximum distance that any feature can move as the result of a single merge
operation. If a single feature takes part in several merge operations, the
total distance moved could be larger.
    Feature merging is completely optional; the tolerance is only a hint. The
implementation is free to merge in some cases and not in others, or to never
merge features at all. The default tolerance is zero.




                              Version 1.3 - 4 November 1998
16                            CHAPTER 5. POLYGON TESSELLATION

    The current implementation merges vertices only if they are exactly co-
incident, regardless of the current tolerance. A vertex is spliced into an edge
only if the implementation is unable to distinguish which side of the edge the
vertex lies on.Two edges are merged only when both endpoints are identical.
    Property values can also be queried by calling
     void   gluGetTessProperty GLUtesselator tess,
        GLenum   which, GLdouble *value ;
to load value with the value of the property speci ed by which.
    To supply the polygon normal call:
     void   gluTessNormal GLUtesselator           tess, GLdouble x,
        GLdouble y, GLdouble z ;

     All input data will be projected into a plane perpendicular to the nor-
mal before tessellation and all output triangles will be oriented CCW with
respect to the normal CW orientation can be obtained by reversing the
sign of the supplied normal. For example, if you know that all polygons
lie in the x-y plane, call gluTessNormaltess,0.0,0.0,1.0 before rendering
any polygons.
     If the supplied normal is 0,0,0 the default value, the normal is de-
termined as follows. The direction of the normal, up to its sign, is found
by tting a plane to the vertices, without regard to how the vertices are
connected. It is expected that the input data lies approximately in plane;
otherwise projection perpendicular to the computed normal may substan-
tially change the geometry. The sign of the normal is chosen so that the
sum of the signed areas of all input contours is non-negative where a CCW
contour has positive area.
     The supplied normal persists until it is changed by another call to
gluTessNormal.

5.5 CSG Operations
The features of the tessellator make it easy to nd the union, di erence, or
intersection of several polygons.
    First, assume that each polygon is de ned so that the winding number is
0 for each exterior region, and 1 for each interior region. Under this model,
CCW contours de ne the outer boundary of the polygon, and CW contours




                   Version 1.3 - 4 November 1998
5.6. PERFORMANCE                                                           17

de ne holes. Contours may be nested, but a nested contour must be oriented
oppositely from the contour that contains it.
    If the original polygons do not satisfy this description, they can
be converted to this form by rst running the tessellator with the
GLU TESS BOUNDARY ONLY property turned on. This returns a list of contours
satisfying the restriction above. By allocating two tessellator objects, the
callbacks from one tessellator can be fed directly to the input of another.
    Given two or more polygons of the form above, CSG operations can be
implemented as follows:

5.5.1 UNION
Draw all the input contours as a single polygon. The winding number
of each resulting region is the number of original polygons which cover
it. The union can be extracted using the GLU TESS WINDING NONZERO or
GLU TESS WINDING POSITIVE winding rules. Note that with the nonzero rule,
we would get the same result if all contour orientations were reversed.

5.5.2 INTERSECTION two polygons at a time only
Draw a single polygon using the contours from both input polygons. Extract
the result using GLU TESS WINDING ABS GEQ TWO. Since this winding rule looks
at the absolute value, reversing all contour orientations does not change the
result.

5.5.3 DIFFERENCE
Suppose we want to compute A , B C D. Draw a single polygon
consisting of the unmodi ed contours from A, followed by the contours
of B , C , and D with the vertex order reversed this changes the wind-
ing number of the interior regions to -1. To extract the result, use the
GLU TESS WINDING POSITIVE rule.
    If B , C , and D are the result of a GLU TESS BOUNDARY ONLY call, an al-
ternative to reversing the vertex order is to reverse the sign of the supplied
normal. For example in the x-y plane, call gluTessNormaltess, 0, 0, -1.

5.6 Performance
The tessellator is not intended for immediate-mode rendering; when possible
the output should be cached in a user structure or display list. General




                              Version 1.3 - 4 November 1998
18                            CHAPTER 5. POLYGON TESSELLATION

polygon tessellation is an inherently di cult problem, especially given the
goal of extreme robustness.
    Single-contour input polygons are rst tested to see whether they can be
rendered as a triangle fan with respect to the rst vertex to avoid running
the full decomposition algorithm on convex polygons. Non-convex polygons
may be rendered by this fast path" as well, if the algorithm gets lucky in
its choice of a starting vertex.
    For best performance follow these guidelines:
     supply the polygon normal, if available, using gluTessNormal. For
     example, if all polygons lie in the x-y plane, use gluTessNormaltess,
     0, 0, 1.
     render many polygons using the same tessellator object, rather than
     allocating a new tessellator for each one. In a multi-threaded, multi-
     processor environment you may get better performance using several
     tessellators.

5.7 Backwards Compatibility
The polygon tessellation routines described previously are new in version 1.2
of the GLU library. For backwards compatibility, earlier versions of these
routines are still supported:

     void   gluBeginPolygon GLUtesselator *tess ;
     void   gluNextContour GLUtesselator *tess,
        GLenum   type ;

     void   gluEndPolygon GLUtesselator *tess ;
   gluBeginPolygon indicates the start of the polygon and gluEndPoly-
gon de nes the end of the polygon. gluNextContour is called once before
each contour; however it does not need to be called when specifying a poly-
gon with one contour. type is ignored by the GLU tessellator. type is one of
GLU EXTERIOR, GLU INTERIOR, GLU CCW, GLU CW or GLU UNKNOWN.
    Calls to gluBeginPolygon, gluNextContour and gluEndPolygon
are mapped to the new tessellator interface as follows:




                   Version 1.3 - 4 November 1998
5.7. BACKWARDS COMPATIBILITY                                               19

    gluBeginPolygon ! gluTessBeginPolygon
                      gluTessBeginContour
    gluNextContour ! gluTessEndContour
                      gluTessBeginContour
    gluEndPolygon ! gluTessEndContour
                      gluTessEndPolygon
    Constants and data structures used in the previous versions of the tessel-
lator are also still supported. GLU BEGIN, GLU VERTEX, GLU END, GLU ERROR and
GLU EDGE FLAG are de ned as synonyms for GLU TESS BEGIN, GLU TESS VERTEX,
GLU TESS END, GLU TESS ERROR and GLU TESS EDGE FLAG. GLUtriangulatorObj
is de ned to be the same as GLUtesselator.
    The preferred interface for polygon tessellation is the one described in
sections 5.1-5.4. The routines described in this section are provided for
backward compatibility only.




                              Version 1.3 - 4 November 1998
Chapter 6

Quadrics
The GLU library quadrics routines will render spheres, cylinders and disks in
a variety of styles as speci ed by the user. To use these routines, rst create a
quadrics object. This object contains state indicating how a quadric should
be rendered. Second, modify this state using the function calls described be-
low. Finally, render the desired quadric by invoking the appropriate quadric
rendering routine.

6.1 The Quadrics Object
A quadrics object is created with gluNewQuadric:
      GLUquadricObj *quadobj;
            gluNewQuadricvoid;
      quadobj =
   gluNewQuadric returns a new quadrics object. This object contains
state describing how a quadric should be constructed and rendered. A return
value of 0 indicates an out-of-memory error.
    When the object is no longer needed, it should be deleted with
gluDeleteQuadric:
      void   gluDeleteQuadric GLUquadricObj *quadobj ;
   This will delete the quadrics object and any memory used by it.

6.2 Callbacks
To associate a callback with the quadrics object, use gluQuadricCallback:
                                      20



                    Version 1.3 - 4 November 1998
6.3. RENDERING STYLES                                                           21

     void   gluQuadricCallback GLUquadricObj *quadobj,
        GLenum   which, void *fn ;
    The only callback provided for quadrics is the GLU ERROR callback iden-
tical to the polygon tessellation callback described above. This callback
takes an error code as its only argument. To translate the error code to an
error message, see gluErrorString below.

6.3 Rendering Styles
A variety of variables control how a quadric will be drawn. These are nor-
mals, textureCoords, orientation, and drawStyle. normals indicates if surface
normals should be generated, and if there should be one normal per vertex
or one normal per face. textureCoords determines whether texture coordi-
nates should be generated. orientation describes which side of the quadric
should be the outside". Lastly, drawStyle indicates if the quadric should
be drawn as a set of polygons, lines, or points.
    To specify the kind of normals desired, use gluQuadricNormals:
     void   gluQuadricNormals GLUquadricObj *quadobj,
        GLenum   normals ;
    normals is either GLU NONE no normals, GLU FLAT one normal per face
or GLU SMOOTH one normal per vertex. The default is GLU SMOOTH.
    Texture coordinate generation can be turned on and o with
gluQuadricTexture:
     void   gluQuadricTexture GLUquadricObj *quadobj,
        GLboolean    textureCoords ;
   If textureCoords is GL TRUE, then texture coordinates will be generated
when a quadric is rendered. Note that how texture coordinates are generated
depends upon the speci c quadric. The default is GL FALSE.
   An orientation can be speci ed with gluQuadricOrientation:
     void   gluQuadricOrientation GLUquadricObj *quadobj,
        GLenum   orientation ;
   If orientation is GLU OUTSIDE then quadrics will be drawn with normals
pointing outward. If orientation is GLU INSIDE then the normals will point
inward faces are rendered counter-clockwise with respect to the normals.




                              Version 1.3 - 4 November 1998
22                                                   CHAPTER 6. QUADRICS

Note that outward" and inward" are de ned by the speci c quadric. The
default is GLU OUTSIDE.
   A drawing style can be chosen with gluQuadricDrawStyle:
       void  gluQuadricDrawStyle GLUquadricObj *quadobj,
          GLenum   drawStyle ;
    drawStyle is one of GLU FILL, GLU LINE, GLU POINT or GLU SILHOUETTE. In
GLU FILL mode, the quadric is rendered as a set of polygons, in GLU LINE mode
as a set of lines, and in GLU POINT mode as a set of points. GLU SILHOUETTE
mode is similar to GLU LINE mode except that edges separating coplanar
faces are not drawn. The default style is GLU FILL.

6.4 Quadrics Primitives
The four supported quadrics are spheres, cylinders, disks, and partial disks.
Each of these quadrics may be subdivided into arbitrarily small pieces.
   A sphere can be created with gluSphere:
       void  gluSphere GLUquadricObj *quadobj,
          GLdouble   radius, GLint slices, GLint stacks ;
    This renders a sphere of the given radius centered around the origin. The
sphere is subdivided along the Z axis into the speci ed number of stacks,
and each stack is then sliced evenly into the given number of slices. Note
that the globe is subdivided in an analogous fashion, where lines of latitude
represent stacks, and lines of longitude represent slices.
    If texture coordinate generation is enabled then coordinates are com-
puted so that t ranges from 0.0 at Z = -radius to 1.0 at Z = radius t
increases linearly along longitudinal lines, and s ranges from 0.0 at the +Y
axis, to 0.25 at the +X axis, to 0.5 at the -Y axis, to 0.75 at the -X axis,
and back to 1.0 at the +Y axis.
    A cylinder is speci ed with gluCylinder:
       void  gluCylinder GLUquadricObj *quadobj,
          GLdouble   baseRadius, GLdouble topRadius,
          GLdouble   height, GLint slices, GLint stacks ;
     gluCylinder draws a frustum of a cone centered on the Z axis with the
base at Z = 0 and the top at Z = height. baseRadius speci es the radius at Z




                     Version 1.3 - 4 November 1998
6.4. QUADRICS PRIMITIVES                                                        23

= 0, and topRadius speci es the radius at Z = height. If baseRadius equals
topRadius, the result is a conventional cylinder. Like a sphere, a cylinder is
subdivided along the Z axis into stacks, and each stack is further subdivided
into slices. When textured, t ranges linearly from 0.0 to 1.0 along the Z
axis, and s ranges from 0.0 to 1.0 around the Z axis in the same manner as
it does for a sphere.
    A disk is created with gluDisk:
      void   gluDisk  GLUquadricObj *quadobj,
         GLdouble innerRadius, GLdouble outerRadius,
         GLint slices, GLint loops ;

    This renders a disk on the Z=0 plane. The disk has the given outer-
Radius, and if innerRadius 0:0 then it will contain a central hole with
the given innerRadius. The disk is subdivided into the speci ed number of
slices similar to cylinders and spheres, and also into the speci ed number
of loops concentric rings about the origin. With respect to orientation, the
+Z side of the disk is considered to be outside".
    When textured, coordinates are generated in a linear grid such that the
value of s,t at outerRadius,0,0 is 1,0.5, at 0,outerRadius,0 it is 0.5,1,
at -outerRadius,0,0 it is 0,0.5, and at 0,-outerRadius,0 it is 0.5,0. This
allows a 2D texture to be mapped onto the disk without distortion.
    A partial disk is speci ed with gluPartialDisk:
      void   gluPartialDisk  GLUquadricObj *quadobj,
         GLdouble innerRadius, GLdouble outerRadius,
         GLint slices, GLint loops, GLdouble startAngle,
         GLdouble sweepAngle ;

    This function is identical to gluDisk except that only the subset of the
disk from startAngle through startAngle + sweepAngle is included where
0 degrees is along the +Y axis, 90 degrees is along the +X axis, 180 is along
the -Y axis, and 270 is along the -X axis. In the case that drawStyle is set
to either GLU FILL or GLU SILHOUETTE, the edges of the partial disk separating
the included area from the excluded arc will be drawn.




                                Version 1.3 - 4 November 1998
Chapter 7

NURBS
NURBS curves and surfaces are converted to OpenGL primitives by the
functions in this section. The interface employs a NURBS object to describe
the curves and surfaces and to specify how they should be rendered. Basic
trimming support is included to allow more exible de nition of surfaces.
    There are two ways to handle a NURBS object curve or surface, to
either render or to tessellate. In rendering mode, the objects are converted
or tessellated to a sequence of OpenGL evaluators and sent to the OpenGL
pipeline for rendering. In tessellation mode, objects are converted to a se-
quence of triangles and triangle strips and returned back to the application
through a callback interface for further processing. The decomposition algo-
rithm used for rendering and for returning tessellations are not guaranteed
to produce identical results.

7.1 The NURBS Object
A NURBS object is created with gluNewNurbsRenderer:
     GLUnurbsObj *nurbsObj;
     nurbsObj =   gluNewNurbsRenderervoid;
    nurbsObj is an opaque pointer to all of the state information needed to
tessellate and render a NURBS curve or surface. Before any of the other
routines in this section can be used, a NURBS object must be created. A
return value of 0 indicates an out of memory error.
    When a NURBS object is no longer needed, it should be deleted with
gluDeleteNurbsRenderer:
                                     24



                   Version 1.3 - 4 November 1998
7.2. CALLBACKS                                                           25

        void   gluDeleteNurbsRenderer GLUnurbsObj *nurbsObj ;
   This will destroy all state contained in the object, and free any memory
used by it.

7.2 Callbacks
To de ne a callback for a NURBS object, use:
        void   gluNurbsCallback GLUnurbsObj *nurbsObj,
           GLenum   which, void *fn ;
      The parameter which can be one of the following: GLU NURBS BEGIN,
GLU   NURBS VERTEX, GLU NORMAL, GLU NURBS COLOR, GLU NURBS TEXTURE COORD,
GLU   END, GLU NURBS BEGIN DATA, GLU NURBS VERTEX DATA, GLU NORMAL DATA,
GLU   NURBS COLOR DATA, GLU NURBS TEXTURE COORD DATA, GLU END DATA and
GLU   ERROR.
      These callbacks have the following prototypes:
        void   begin GLenum type ;
        void   vertex GLfloat *vertex ;
        void   normal GLfloat *normal ;
        void   color GLfloat *color ;
        void   texCoord GLfloat *tex coord ;
        void   end void ;
        void   beginData GLenum type, void *userData ;
        void   vertexData GLfloat *vertex, void *userData ;
        void   normalData GLfloat *normal, void *userData ;
        void   colorData GLfloat *color, void *userData ;
        void   texCoordData GLfloat *tex coord, void *userData ;
        void   endData void *userData ;
        void   error GLenum errno ;
   The rst 12 callbacks are for the user to get the primitives back from
the NURBS tessellator when NURBS property GLU NURBS MODE is set to
GLU NURBS TESSELLATOR see section 7.6. These callbacks have no e ect when
GLU NURBS MODE is GLU NURBS RENDERER.
   There are two forms of each callback: one with a pointer to application
supplied data and one without. If both versions of a particular callback are
speci ed then the callback with application data will be used. userData is
speci ed by calling




                                Version 1.3 - 4 November 1998
26                                                  CHAPTER 7. NURBS

     void   gluNurbsCallbackData GLUnurbsObj *nurbsObj,
        void   *userData ;

The value of userData passed to callback functions for a speci c NURBS
object is the value speci ed by the last call to gluNurbsCallbackData.
    All callback functions can be set to NULL even when GLU NURBS MODE is
set to GLU NURBS TESSELLATOR. When a callback function is set to NULL, this
callback function will not get invoked and the related data, if any, will be
lost.
    The begin callback indicates the start of a primitive. type is one of
GL LINES, GL LINE STRIPS, GL TRIANGLE FAN, GL TRIANGLE STRIP, GL TRIANGLES
or GL QUAD STRIP. The default begin callback function is NULL.
    The vertex callback indicates a vertex of the primitive. The coordinates
of the vertex are stored in the parameter vertex. All the generated vertices
have dimension 3; that is, homogeneous coordinates have been transformed
into a ne coordinates. The default vertex callback function is NULL.
    The normal callback is invoked as the vertex normal is generated. The
components of the normal are stored in the parameter normal. In the case
of a NURBS curve, the callback function is e ective only when the user
provides a normal map GL MAP1 NORMAL. In the case of a NURBS surface,
if a normal map GL MAP2 NORMAL is provided, then the generated normal
is computed from the normal map. If a normal map is not provided then
a surface normal is computed in a manner similar to that described for
evaluators when GL AUTO NORMAL is enabled. The default normal callback
function is NULL.
    The color callback is invoked as the color of a vertex is generated. The
components of the color are stored in the parameter color. This callback
is e ective only when the user provides a color map GL MAP1 COLOR 4 or
GL MAP2 COLOR 4. color contains four components: R,G,B,A. The default
color callback function is NULL.
    The texture callback is invoked as the texture coordinates of a vertex
are generated. These coordinates are stored in the parameter tex coord. The
number of texture coordinates can be 1, 2, 3 or 4 depending on which type of
texture map is speci ed GL MAP* TEXTURE COORD 1, GL MAP* TEXTURE COORD 2,
GL MAP* TEXTURE COORD 3, GL MAP* TEXTURE COORD 4 where * can be either 1 or
2. If no texture map is speci ed, this callback function will not be called.
The default texture callback function is NULL.
    The end callback is invoked at the end of a primitive. The default end
callback function is NULL.




                   Version 1.3 - 4 November 1998
7.3. NURBS CURVES                                                          27

   The error callback is invoked when a NURBS function detects an error
condition. There are 37 errors speci c to NURBS functions, and they are
named GLU NURBS ERROR1 through GLU NURBS ERROR37. Strings describing the
meaning of these error codes can be retrieved with gluErrorString.

7.3 NURBS Curves
NURBS curves are speci ed with the following routines:
     void   gluBeginCurve GLUnurbsObj *nurbsObj ;
     void   gluNurbsCurve   GLUnurbsObj *nurbsObj,
        GLint nknots, GLfloat *knot, GLint stride,
        GLfloat *ctlarray, GLint order, GLenum type ;

     void   gluEndCurve GLUnurbsObj *nurbsObj ;
    gluBeginCurve and gluEndCurve delimit a curve de nition. After
the gluBeginCurve and before the gluEndCurve, a series of gluNurb-
sCurve calls specify the attributes of the curve. type can be any of the one
dimensional evaluators such as GL MAP1 VERTEX 3. knot points to an array
of monotonically increasing knot values, and nknots tells how many knots
are in the array. ctlarray points to an array of control points, and order
indicates the order of the curve. The number of control points in ctlarray
will be equal to nknots - order. Lastly, stride indicates the o set expressed
in terms of single precision values between control points.
    The NURBS curve attribute de nitions must include either a
GL MAP1 VERTEX3 description or a GL MAP1 VERTEX4 description.
    At the point that gluEndCurve is called, the curve will be tessellated
into line segments and rendered with the aid of OpenGL evaluators. gl-
PushAttrib and glPopAttrib are used to preserve the previous evaluator
state during rendering.

7.4 NURBS Surfaces
NURBS surfaces are described with the following routines:
     void   gluBeginSurface GLUnurbsObj *nurbsObj ;




                              Version 1.3 - 4 November 1998
28                                                   CHAPTER 7. NURBS

       void   gluNurbsSurface   GLUnurbsObj *nurbsObj,
          GLint sknot count, GLfloat *sknot, GLint tknot      count,
          GLfloat *tknot, GLint s stride, GLint t stride,
          GLfloat *ctlarray, GLint sorder, GLint torder,
          GLenum type ;

       void   gluEndSurface GLUnurbsObj *nurbsObj ;
     The surface description is almost identical to the curve description.
gluBeginSurface and gluEndSurface delimit a surface de nition. Af-
ter the gluBeginSurface, and before the gluEndSurface, a series of
gluNurbsSurface calls specify the attributes of the surface. type can be
any of the two dimensional evaluators such as GL MAP2 VERTEX 3. sknot
and tknot point to arrays of monotonically increasing knot values, and
sknot count and tknot count indicate how many knots are in each array.
ctlarray points to an array of control points, and sorder and torder indicate
the order of the surface in both the s and t directions. The number of control
points in ctlarray will be equal to sknot count , sorder  tknot count ,
torder. Finally, s stride and t stride indicate the o set in single precision
values between control points in the s and t directions.
    The NURBS surface, like the NURBS curve, must include an attribute
de nition of type GL MAP2 VERTEX3 or GL MAP2 VERTEX4.
    When gluEndSurface is called, the NURBS surface will be tessellated
and rendered with the aid of OpenGL evaluators. The evaluator state is
preserved during rendering with glPushAttrib and glPopAttrib.

7.5 Trimming
A trimming region de nes a subset of the NURBS surface domain to be
evaluated. By limiting the part of the domain that is evaluated, it is possible
to create NURBS surfaces that contain holes or have smooth boundaries.
    A trimming region is de ned by a set of closed trimming loops in the
parameter space of a surface. When a loop is oriented counter-clockwise, the
area within the loop is retained, and the part outside is discarded. When
the loop is oriented clockwise, the area within the loop is discarded, and the
rest is retained. Loops may be nested, but a nested loop must be oriented
oppositely from the loop that contains it. The outermost loop must be
oriented counter-clockwise.
    A trimming loop consists of a connected sequence of NURBS curves and
piecewise linear curves. The last point of every curve in the sequence must




                    Version 1.3 - 4 November 1998
7.6. NURBS PROPERTIES                                                      29

be the same as the rst point of the next curve, and the last point of the last
curve must be the same as the rst point of the rst curve. Self-intersecting
curves are not allowed.
    To de ne trimming loops, use the following routines:
     void   gluBeginTrim GLUnurbsObj *nurbsObj ;
     void   gluPwlCurve GLUnurbsObj *nurbsObj, GLint count,
        GLfloat   *array, GLint stride, GLenum type ;
     void   gluNurbsCurve   GLUnurbsObj *nurbsObj,
        GLint nknots, GLfloat *knot, GLint stride,
        GLfloat *ctlarray, GLint order, GLenum type ;

     void   gluEndTrim GLUnurbsObj *nurbsObj ;
    A NURBS trimming curve is very similar to a regular NURBS curve,
with the major di erence being that a NURBS trimming curve exists in the
parameter space of a NURBS surface.
    gluPwlCurve de nes a piecewise linear curve. count indicates how
many points are on the curve, and array points to an array containing the
curve points. stride indicates the o set in single precision values between
curve points.
    type for both gluPwlCurve and gluNurbsCurve can be either
GLU MAP1 TRIM 2 or GLU MAP1 TRIM 3. GLU MAP1 TRIM 2 curves de ne trimming
regions in two dimensional s and t parameter space. The GLU MAP1 TRIM 3
curves de ne trimming regions in two dimensional homogeneous s, t and q
parameter space.
    Note that the trimming loops must be de ned at the same time that the
surface is de ned between gluBeginSurface and gluEndSurface.

7.6 NURBS Properties
A set of properties associated with a NURBS object a ects the way that
NURBS are rendered or tessellated. These properties can be adjusted by
the user.
     void   gluNurbsProperty GLUnurbsObj *nurbsObj,
        GLenum   property, GLfloat value ;




                              Version 1.3 - 4 November 1998
30                                                   CHAPTER 7. NURBS

   allows the user to set one of the following properties: GLU CULLING,
GLU SAMPLING TOLERANCE, GLU SAMPLING METHOD, GLU PARAMETRIC TOLERANCE,
GLU DISPLAY MODE, GLU AUTO LOAD MATRIX, GLU U STEP, GLU V STEP and
GLU NURBS MODE. property indicates the property to be modi ed, and value
speci es the new value.
    GLU NURBS MODE should be set to either GLU NURBS RENDERER or
GLU NURBS TESSELLATOR. When set to GLU NURBS RENDERER, NURBS objects
are tessellated into OpenGL evaluators and sent to the pipeline for render-
ing. When set to GLU NURBS TESSELLATOR, NURBS objects are tessellated
into a sequence of primitives such as lines, triangles and triangle strips, but
the vertices, normals, colors, and or textures are retrieved back through
a callback interface as speci ed in Section 7.2. This allows the user to
cache the tessellated results for further processing. The default value is
GLU NURBS RENDERER
   The GLU CULLING property is a boolean value value should be set to either
GL TRUE or GL FALSE. When set to GL TRUE, it indicates that a NURBS curve
or surface should be discarded prior to tessellation if its control polyhedron
lies outside the current viewport. The default is GL FALSE.
    GLU SAMPLING METHOD speci es how a NURBS surface should
be tessellated.       value may be set to one of GLU PATH LENGTH,
GLU PARAMETRIC ERROR, GLU DOMAIN DISTANCE, GLU OBJECT PATH LENGTH or
GLU OBJECT PARAMETRIC ERROR. When set to GLU PATH LENGTH, the surface is
rendered so that the maximum length, in pixels, of the edges of the tessella-
tion polygons is no greater than what is speci ed by GLU SAMPLING TOLERANCE.
GLU PARAMETRIC ERROR speci es that the surface is rendered in such a way
that the value speci ed by GLU PARAMETRIC TOLERANCE describes the maxi-
mum distance, in pixels, between the tessellation polygons and the surfaces
they approximate. GLU DOMAIN DISTANCE allows users to specify, in paramet-
ric coordinates, how many sample points per unit length are taken in u,
v dimension. GLU OBJECT PATH LENGTH is similar to GLU PATH LENGTH except
that it is view independent; that is, it speci es that the surface is rendered
so that the maximum length, in object space, of edges of the tessellation
polygons is no greater than what is speci ed by GLU SAMPLING TOLERANCE.
GLU OBJECT PARAMETRIC ERROR is similar to GLU PARAMETRIC ERROR except
that the surface is rendered in such a way that the value speci ed by
GLU PARAMETRIC TOLERANCE describes the maximum distance, in object space,
between the tessellation polygons and the surfaces they approximate. The
default value of GLU SAMPLING METHOD is GLU PATH LENGTH.
    GLU SAMPLING TOLERANCE speci es the maximum length, in pixels or in
object space length unit, to use when the sampling method is set to




                   Version 1.3 - 4 November 1998
7.6. NURBS PROPERTIES                                                       31

GLU PATH LENGTH or GLU OBJECT PATH LENGTH. The default value is 50.0.
   GLU PARAMETRIC TOLERANCE speci es the maximum distance, in pixels         or
in object space length unit, to use when the sampling method is set to
GLU PARAMETRIC ERROR or GLU OBJECT PARAMETRIC ERROR. The default value for
GLU PARAMETRIC TOLERANCE is 0.5.
    GLU U STEP speci es the number of sample points per unit length taken
along the u dimension in parametric coordinates. It is needed when
GLU SAMPLING METHOD is set to GLU DOMAIN DISTANCE. The default value is 100.
    GLU V STEP speci es the number of sample points per unit length taken
along the v dimension in parametric coordinates. It is needed when
GLU SAMPLING METHOD is set to GLU DOMAIN DISTANCE. The default value is 100.
    GLU AUTO LOAD MATRIX is a boolean value. When it is set to GL TRUE, the
NURBS code will download the projection matrix, the model view matrix,
and the viewport from the OpenGL server in order to compute sampling and
culling matrices for each curve or surface that is rendered. These matrices
are required to tessellate a curve or surface and to cull it if it lies outside
the viewport. If this mode is turned o , then the user needs to provide a
projection matrix, a model view matrix, and a viewport that the NURBS
code can use to construct sampling and culling matrices. This can be done
with the gluLoadSamplingMatrices function:
      void gluLoadSamplingMatrices GLUnurbsObj *nurbsObj,
          const GLfloat modelMatrix 16 ,
          const GLfloat projMatrix 16 , const GLint viewport 4 ;

    Until the GLU AUTO LOAD MATRIX property is turned back on, the NURBS
routines will continue to use whatever sampling and culling matrices are
stored in the NURBS object. The default for GLU AUTO LOAD MATRIX is
GL TRUE.
    You may get unexpected results when GLU AUTO LOAD MATRIX is enabled
and the results of the NURBS tesselation are being stored in a display list,
since the OpenGL matrices which are used to create the sampling and culling
matrices will be those that are in e ect when the list is created, not those
in e ect when it is executed.
    GLU DISPLAY MODE speci es how a NURBS surface should be rendered.
value may be set to one of GLU FILL, GLU OUTLINE POLY or GLU OUTLINE PATCH.
When GLU NURBS MODE is set to be GLU NURBS RENDERER, value de nes how a
NURBS surface should be rendered. When set to GLU FILL, the surface
is rendered as a set of polygons. GLU OUTLINE POLY instructs the NURBS
library to draw only the outlines of the polygons created by tessella-
tion. GLU OUTLINE PATCH will cause just the outlines of patches and trim




                               Version 1.3 - 4 November 1998
32                                                   CHAPTER 7. NURBS

curves de ned by the user to be drawn. When GLU NURBS MODE is set to
be GLU NURBS TESSELLATOR, value de nes how a NURBS surface should be
tessellated. When GLU DISPLAY MODE is set to GLU FILL or GLU OUTLINE POLY,
the NURBS surface is tessellated into OpenGL triangle primitives which
can be retrieved back through callback functions. If value is set to
GLU OUTLINE PATCH, only the outlines of the patches and trim curves are gen-
erated as a sequence of line strips and can be retrieved back through callback
functions. The default is GLU FILL.
    Property values can be queried by calling
     void   gluGetNurbsProperty GLUnurbsObj *nurbsObj,
        GLenum   property, GLfloat *value ;
The speci ed property is returned in value.




                   Version 1.3 - 4 November 1998
Chapter 8

Errors
Calling
     const GLubyte    *gluErrorString GLenum errorCode ;
produces an error string corresponding to a GL or GLU error code.
The error string is in ISO Latin 1 format. The standard GLU error
codes are GLU INVALID ENUM, GLU INVALID VALUE, GLU INVALID OPERATION and
GLU OUT OF MEMORY. There are also speci c error codes for polygon tessella-
tion, quadrics, and NURBS as described in their respective sections.
    If an invalid call to the underlying OpenGL implementation is made
by GLU, either GLU or OpenGL errors may be generated, depending on
where the error is detected. This condition may occur only when making
a GLU call introduced in a later version of GLU than that correspond-
ing to the OpenGL implementation see Chapter 9; for example, calling
gluBuild3DMipmaps or passing packed pixel types to gluScaleImage
when the underlying OpenGL version is earlier than 1.2.




                                    33



                             Version 1.3 - 4 November 1998
Chapter 9

GLU Versions
Each version of GLU corresponds to the OpenGL version shown in Table 9.1;
GLU features introduced in a particular version of GLU may not be usable
if the underlying OpenGL implementation is an earlier version.
    All versions of GLU are upward compatible with earlier versions, mean-
ing that any program that runs with the earlier implementation will run
unchanged with any later GLU implementation.


9.1 GLU 1.1
In GLU 1.1, gluGetString was added allowing the GLU version num-
ber and GLU extensions to be queried. Also, the NURBS properties
GLU SAMPLING METHOD, GLU PARAMETRIC TOLERANCE, GLU U STEP and GLU V STEP
were added providing support for di erent tesselation methods. In GLU 1.0,
the only sampling method supported was GLU PATH LENGTH.

                 GLU Version Corresponding OpenGL
                                    Version
                  GLU 1.0         OpenGL 1.0
                  GLU 1.1         OpenGL 1.0
                  GLU 1.2         OpenGL 1.1
                  GLU 1.3         OpenGL 1.2
          Table 9.1: Relationship of OpenGL and GLU versions.

                                    34



                  Version 1.3 - 4 November 1998
9.2. GLU 1.2                                                          35

9.2 GLU 1.2
A new polygon tesselation interface was added in GLU 1.2. See section 5.7
for more information on the API changes.
    A new NURBS callback interface and object space sampling methods
was also added in GLU 1.2. See sections 7.2 and 7.6 for API changes.

9.3 GLU 1.3
The gluCheckExtension utility function was introduced.
    gluScaleImage and gluBuildxDMipmaps support the new packed
pixel formats and types introduced by OpenGL 1.2.
    gluBuild3DMipmaps was added to support 3D textures, introduced
by OpenGL 1.2.
    gluBuildxDMipmapLevels was added to support OpenGL 1.2's abil-
ity to load only a subset of mipmap levels.
    gluUnproject4 was added for use when non-default depth range or w
values other than 1 need to be speci ed.
    New gluNurbsCallback callbacks and the GLU NURBS MODE NURBS
property were introduced to allow applications to capture NURBS tes-
selations. These features exactly match corresponding features of the
GLU EXT nurbs tessellator GLU extension, and may be used interchange-
ably with the extension.
    New values of the GLU SAMPLING METHOD NURBS property were introduced
to support object-space sampling criteria. These features exactly match
corresponding features of the GLU EXT object space tess GLU extension,
and may be used interchangeably with the extension.




                            Version 1.3 - 4 November 1998
Index of GLU Commands
begin, 12, 25                         GL MAP2 VERTEX4, 28
beginData, 12, 25                     GL MAP2 VERTEX 3, 28
                                      GL QUAD STRIP, 26
color, 25                             GL TRIANGLE FAN,13, 26
colorData, 25                         GL TRIANGLE STRIP,13, 26
combine, 12                           GL TRIANGLES,13, 26
combineData, 12                       GL TRUE,2,9,13,15,21,30, 31
edgeFlag, 12                          GL VIEWPORT, 8
edgeFlagData, 12                      glBegin, 13
end, 12, 25                           glDepthRange, 9
endData, 12, 25                       glDrawPixels, 5
error, 12, 25                         glFeedbackBu er, 9
errorData, 12                         glGetDoublev, 9
                                      glGetIntegerv, 8, 9
GL 4D COLOR TEXTURE, 9                glGetString, 3
GL AUTO NORMAL, 26                    glMultMatrix, 7
GL FALSE,2,9,13,15,21, 30             glNewList, 1
GL LINE LOOP, 15                      glOrtho, 7
GL LINE STRIPS, 26                    glPopAttrib, 27, 28
GL LINES, 26                          glPushAttrib, 27, 28
GL MAP TEXTURE COORD 1,              glTexImage1D, 5
          26                          glTexImage2D, 5
GL MAP TEXTURE COORD 2,              glTexImage3D, 5
          26                          glTexImagexD, 6
GL MAP TEXTURE COORD 3,              GLU AUTO LOAD MATRIX,30, 31
          26                          GLU BEGIN, 19
GL MAP TEXTURE COORD 4,              GLU CCW, 18
          26                          GLU CULLING, 30
GL MAP1 COLOR 4, 26                   GLU CW, 18
GL MAP1 NORMAL, 26                    GLU DISPLAY MODE, 30 32
GL MAP1 VERTEX3, 27                   GLU DOMAIN DISTANCE,30, 31
GL MAP1 VERTEX4, 27                   GLU EDGE FLAG, 19
GL MAP1 VERTEX 3, 27                  GLU END,19, 25
GL MAP2 COLOR 4, 26                   GLU END DATA, 25
GL MAP2 NORMAL, 26                    GLU ERROR,19,21, 25
GL MAP2 VERTEX3, 28                   GLU EXTENSIONS, 2

                                36



              Version 1.3 - 4 November 1998
INDEX                                                        37

GLU EXTERIOR, 18                    GLU POINT, 22
GLU FILL,22,23,31, 32               GLU SAMPLING METHOD,30,31,
GLU FLAT, 21                               34, 35
GLU INSIDE, 21                      GLU SAMPLING TOLERANCE,
GLU INTERIOR, 18                           30
GLU INVALID ENUM, 33                GLU SILHOUETTE,22, 23
GLU INVALID OPERATION, 33           GLU SMOOTH, 21
GLU INVALID VALUE,6, 33             GLU TESS BEGIN,12,15, 19
GLU LINE, 22                        GLU TESS BEGIN DATA,12, 15
GLU MAP1 TRIM 2, 29                 GLU TESS BOUNDARY ONLY,13,
GLU MAP1 TRIM 3, 29                        15, 17
GLU NONE, 21                        GLU TESS COMBINE, 12
GLU NORMAL, 25                      GLU TESS COMBINE DATA, 12
GLU NORMAL DATA, 25                 GLU TESS COORD TOO LARGE,
GLU NURBS BEGIN, 25                        13
GLU NURBS BEGIN DATA, 25            GLU TESS EDGE FLAG,12, 19
GLU NURBS COLOR, 25                 GLU TESS EDGE FLAG DATA, 12
GLU NURBS COLOR DATA, 25            GLU TESS END,12, 19
GLU NURBS ERROR1, 27                GLU TESS END DATA, 12
GLU NURBS ERROR37, 27               GLU TESS ERROR,12, 19
GLU NURBS MODE,25,26,30--32,        GLU TESS ERROR DATA, 12
       35                           GLU TESS MAX COORD TOO
GLU NURBS RENDERER,25,30,                  LARGE, 13
       31                           GLU TESS MISSING BEGIN
GLU NURBS TESSELLATOR,25,                  CONTOUR, 13
       26,30, 32                    GLU TESS MISSING BEGIN
GLU NURBS TEXTURE COORD,                   POLYGON, 13
       25                           GLU TESS MISSING END
GLU NURBS TEXTURE COORD                    CONTOUR, 13
       DATA, 25                     GLU TESS MISSING END
GLU NURBS VERTEX, 25                       POLYGON, 13
GLU NURBS VERTEX DATA, 25           GLU TESS NEED COMBINE
GLU OBJECT PARAMETRIC                      CALLBACK,13, 14
       ERROR,30, 31                 GLU TESS TOLERANCE, 15
GLU OBJECT PATH LENGTH,30,          GLU TESS TOLERANCE., 15
       31                           GLU TESS VERTEX,12, 19
GLU OUT OF MEMORY, 33               GLU TESS VERTEX DATA, 12
GLU OUTLINE PATCH,31, 32            GLU TESS WINDING ABS GEQ
GLU OUTLINE POLY,31, 32                    TWO,15, 17
GLU OUTSIDE,21, 22                  GLU TESS WINDING NEGATIVE,
GLU PARAMETRIC ERROR,30,                   15
       31                           GLU TESS WINDING NONZERO,
GLU PARAMETRIC                             15, 17
       TOLERANCE,30,31, 34          GLU TESS WINDING ODD, 15
GLU PATH LENGTH,30,31, 34           GLU TESS WINDING POSITIVE,




                        Version 1.3 - 4 November 1998
38                                                                   INDEX

         15, 17                           gluPartialDisk, 23
GLU TESS WINDING RULE, 15                 gluPerspective, 7
GLU U STEP,30,31, 34                      gluPickMatrix, 8
GLU UNKNOWN, 18                           gluProject, 9
GLU V STEP,30,31, 34                      gluPwlCurve, 29
GLU VERSION, 2                            gluQuadricCallback, 20, 21
GLU VERTEX, 19                            gluQuadricDrawStyle, 22
gluBeginCurve, 27                         gluQuadricNormals, 21
gluBeginPolygon, 18, 19                   gluQuadricOrientation, 21
gluBeginSurface, 27 29                    gluQuadricTexture, 21
gluBeginTrim, 29                          gluScaleImage, 4, 5, 33, 35
gluBuild1DMipmapLevels, 5                 gluSphere, 22
gluBuild1DMipmaps, 5                      gluTessBeginContour, 11, 19
gluBuild2DMipmapLevels, 6                 gluTessBeginPolygon, 11, 13, 19
gluBuild2DMipmaps, 5                      gluTessCallback, 12
gluBuild3DMipmapLevels, 6                 gluTessEndContour, 11, 19
gluBuild3DMipmaps, 5, 33, 35              gluTessEndPolygon, 11, 19
gluBuildxDMipmapLevels, 35                gluTessNormal, 16 18
gluBuildxDMipmaps, 6, 35                  gluTessProperty, 14
gluCheckExtension, 2, 3, 35               gluTessVertex, 11, 13
gluCylinder, 22                           gluUnProject, 9
gluDeleteNurbsRenderer, 24, 25            gluUnProject4, 9
gluDeleteQuadric, 20                      gluUnproject4, 35
gluDeleteTess, 10                         glXGetClientString, 3
gluDisk, 23
gluEndCurve, 27                           normal, 25
gluEndPolygon, 18, 19                     normalData, 25
gluEndSurface, 28, 29                     texCoord, 25
gluEndTrim, 29                            texCoordData, 25
gluErrorString, 5, 21, 27, 33
gluGetNurbsProperty, 32                   vertex, 12, 25
gluGetString, 2, 3, 34                    vertexData, 12, 25
gluGetTessProperty, 16
gluLoadSamplingMatrices, 31
gluLookAt, 8
gluNewNurbsRenderer, 24
gluNewQuadric, 20
gluNewTess, 10
gluNextContour, 18, 19
gluNurbsCallback, 25, 35
gluNurbsCallbackData, 26
gluNurbsCurve, 27, 29
gluNurbsProperty, 29
gluNurbsSurface, 28
gluOrtho2D, 7




                  Version 1.3 - 4 November 1998
