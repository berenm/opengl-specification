OpenGL R ES 1.1 Extension Pack Specification
             Version 1.03 (Annotated)


              Editor : Aaftab Munshi
            Copyright (c) 2002-2005 The Khronos Group Inc. All Rights Reserved.

This specification is protected by copyright laws and contains material proprietary to the Khronos
Group, Inc. It or any components may not be reproduced, republished, distributed, transmitted,
displayed, broadcast or otherwise exploited in any manner without the express prior written per-
mission of Khronos Group. You may use this specification for implementing the functionality
therein, without altering or removing any trademark, copyright or other notice from the specifi-
cation, but the receipt or possession of this specification does not convey any rights to reproduce,
disclose, or distribute its contents, or to manufacture, use, or sell anything that it may describe,
in whole or in part.
Khronos Group grants express permission to any current Promoter, Contributor or Adopter mem-
ber of Khronos to copy and redistribute UNMODIFIED versions of this specification in any fash-
ion, provided that NO CHARGE is made for the specification and the latest available update of
the specification for any version of the API is used whenever possible. Such distributed speci-
fication may be re-formatted AS LONG AS the contents of the specification are not changed in
any way. The specification may be incorporated into a product that is sold as long as such prod-
uct includes significant independent work developed by the seller. A link to the current version
of this specification on the Khronos Group web-site should be included whenever possible with
specification distributions.
Khronos Group makes no, and expressly disclaims any, representations or warranties, express
or implied, regarding this specification, including, without limitation, any implied warranties of
merchantability or fitness for a particular purpose or non-infringement of any intellectual prop-
erty. Khronos Group makes no, and expressly disclaims any, warranties, express or implied,
regarding the correctness, accuracy, completeness, timeliness, and reliability of the specification.
Under no circumstances will the Khronos Group, or any of its Promoters, Contributors or Mem-
bers or their respective partners, officers, directors, employees, agents or representatives be liable
for any damages, whether direct, indirect, special or consequential damages for lost revenues,
lost profits, or otherwise, arising from or in connection with these materials.
Khronos is a trademark of The Khronos Group Inc. OpenGL is a registered trademark, and
OpenGL ES is a trademark, of Silicon Graphics, Inc.
Contents

1   Overview                                                                                             1

2   Texture Environment Crossbar                                                                         2

3   Mirrored Texture Addressing                                                                          4

4   Cube Maps                                                                                            5
    4.1 Coordinate Transformations . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .     5
    4.2 Texture Addressing Modes . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .     6
    4.3 Texture Completeness . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .   6

5   Blending Extensions                                                                                  8

6   Stencil Extensions                                                                                   10

7   Extended Matrix Palette                                                                              11

8   Framebuffer Objects                                                                                  14




                                                     i
Chapter 1

Overview

This specification describes the OpenGL ES 1.1 Extension Pack specification. The OpenGL ES 1.1 Exten-
sion Pack is a collection of optional extensions added to OpenGL ES 1.1 that include features that are in
OpenGL 1.5 but not in OpenGL ES 1.1. The functionality implemented by this extension pack brings a
significant improvement in image quality and performance that can be leveraged by handheld 3D applica-
tions. It is the intent of the OpenGL ES working group that OpenGL ES 1.2 will make the list of features /
extensions defined by this extension pack mandatory.
    In addition to the optional extensions, OpenGL ES implementations that plan to support the
Extension Pack are recommended to support a stencil bit depth of four or higher and an EGL config
with a depth and stencil buffer, where stencil bit- depth is four or higher. This recommendation will
become a mandatory requirement in OpenGL ES 1.2.

   The extension strings that identify the OpenGL ES 1.1 Extension Pack are given by the following table:

                                 Extension Name
                                 GL   OES   texture env crossbar
                                 GL   OES   textured mirrored repeat
                                 GL   OES   texture cube map
                                 GL   OES   blend subtract
                                 GL   OES   blend func separate
                                 GL   OES   blend equation separate
                                 GL   OES   stencil wrap
                                 GL   OES   extended matrix palette
                                 GL   OES   framebuffer object


   The OpenGL ES 1.1 specification is written against the OpenGL 1.5 specification. Since the GL OES -
texture env crossbar, GL OES textured mirrored repeat, GL OES texture cube map, GL OES -
blend subtract, GL OES blend func separate, and GL OES stencil wrap extensions describe func-
tionality that is already part of the OpenGL 1.5 specification, the corresponding OES extensions will only
give an overview, and describe any new tokens and/or functions added by these extensions. Please refer to
the OpenGL 1.5 specification for detailed description of how these features work.




                                                    1
Chapter 2

Texture Environment Crossbar

The OES texture env crossbar extension adds the capability to use the texture color from other texture
units as sources to the COMBINE environment function. OpenGL ES 1.1 defined texture combine functions
which could use the color from the current texture unit as a source. This extension adds the ability to use
the color from any texture unit as a source.
    The tables that define arguments for COMBINE RGB and COMBINE ALPHA functions are extended to
include TEXTUREn

                        SRCn RGB            OPERANDn RGB                Argument
                        TEXTURE             SRC   COLOR                 Cs
                                            ONE   MINUS   SRC COLOR     1 − Cs
                                            SRC   ALPHA                 As
                                            ONE   MINUS   SRC ALPHA     1 − As
                        TEXTUREn            SRC   COLOR                 Cs n
                                            ONE   MINUS   SRC COLOR     1 − Cs n
                                            SRC   ALPHA                 As n
                                            ONE   MINUS   SRC ALPHA     1 − As n
                        CONSTANT            SRC   COLOR                 Cc
                                            ONE   MINUS   SRC COLOR     1 − Cc
                                            SRC   ALPHA                 Ac
                                            ONE   MINUS   SRC ALPHA     1 − Ac
                        PRIMARY COLOR       SRC   COLOR                 Cf
                                            ONE   MINUS   SRC COLOR     1 − Cf
                                            SRC   ALPHA                 Af
                                            ONE   MINUS   SRC ALPHA     1 − Af
                        PREVIOUS            SRC   COLOR                 Cp
                                            ONE   MINUS   SRC COLOR     1 − Cp
                                            SRC   ALPHA                 Ap
                                            ONE   MINUS   SRC ALPHA     1 − Ap

                           Table 2.1: Arguments for COMBINE RGB functions.




                                                    2
Texture Environment Crossbar                                                 3




                      SRCn ALPHA        OPERANDn ALPHA            Argument
                      TEXTURE           SRC   ALPHA               As
                                        ONE   MINUS   SRC ALPHA   1 − As
                      TEXTUREn          SRC   ALPHA               As n
                                        ONE   MINUS   SRC ALPHA   1 − As n
                      CONSTANT          SRC   ALPHA               Ac
                                        ONE   MINUS   SRC ALPHA   1 − Ac
                      PRIMARY COLOR     SRC   ALPHA               Af
                                        ONE   MINUS   SRC ALPHA   1 − Af
                      PREVIOUS          SRC   ALPHA               Ap
                                        ONE   MINUS   SRC ALPHA   1 − Ap

                        Table 2.2: Arguments for COMBINE ALPHA functions.
Chapter 3

Mirrored Texture Addressing

The OES texture mirrored repeat extension extends the set of texture wrap modes to include a mode
(GL MIRRORED REPEAT) that effectively uses a texture map twice as large as the original image in which
the additional half, for each coordinate, of the new image is a mirror image of the original image.
    This new mode relaxes the need to generate images whose opposite edges match by using the original
image to generate a matching ”mirror image”.
    Wrap modes REPEAT, CLAMP TO EDGE and MIRRORED REPEAT are now supported.




                                                  4
Chapter 4

Cube Maps

The OES texture cube map extension provides a new texture generation scheme for cube map textures.
Instead of the current texture providing a 2D lookup into a 2D texture image, the texture is a set of six
2D images representing the faces of a cube. The (s,t,r) texture coordinates are treated as a direction vector
emanating from the center of a cube. At texture generation time, the interpolated per-fragment (s,t,r) selects
one cube face 2D image based on the largest magnitude coordinate (the major axis). A new 2D (s,t) is
calculated by dividing the two other coordinates (the minor axes values) by the major axis value. Then the
new (s,t) is used to lookup into the selected 2D texture image face of the cube map.
     Unlike a standard 2D texture that have just one target, a cube map texture has six targets, one for each
of its six 2D texture image cube faces. All these targets must be consistent, complete, and have equal width
and height (ie, square dimensions).
     This extension also provides two new texture coordinate generation modes for use in conjunction with
cube map texturing. The reflection map mode generates texture coordinates (s,t,r) matching the vertex’s
eye-space reflection vector. The reflection map mode is useful for environment mapping without the sin-
gularity inherent in sphere mapping. The normal map mode generates texture coordinates (s,t,r) matching
the vertex’s transformed eye-space normal. The normal map mode is useful for sophisticated cube map
texturing-based diffuse lighting models.
     The intent of the new texgen functionality is that an application using cube map texturing can use the
new texgen modes to automatically generate the reflection or normal vectors used to look up into the cube
map texture.
     The following texgen modes are supported: REFLECTION MAP and NORMAL MAP. SPHERE -
MAP, OBJECT LINEAR, and EYE LINEAR texgen modes are not supported. Texgen supports a new
coord value STR. This allows the application to specify the texgen mode for the appropriate coordinates in
a single call. Texgen with coord values of S, T, R and Q are not supported.


4.1    Coordinate Transformations

 OpenGL 1.5                                                                    Common       Common-Lite
 TexGen{ifx}[v](enum coord, enum pname,             T params)
   pname = TEXTURE GEN MODE, params =               OBJECT LINEAR                  –               –
   pname = TEXTURE GEN MODE, params =               EYE LINEAR                     –               –
   pname = TEXTURE GEN MODE, params =               SPHERE MAP                     –               –
   pname = TEXTURE GEN MODE, params =               REFLECTION MAP                 ♦               †


                                                      5
6                                                                                                  Cube Maps


    OpenGL 1.5                                                                  Common         Common-Lite
      pname = TEXTURE GEN MODE, params = NORMAL MAP                               ♦                †
      pname = OBJECT PLANE                                                         –               –
      pname = EYE PLANE                                                            –               –
    TexGen{d}[v](enum coord, enum pname, T param)                                  –               –
    GetTexGen{d}v(enum coord, enum pname, T *params)                               –               –
    GetTexGen{ifx}v(enum coord, enum pname, T *params)
    Enable/Disable(TEXTURE GEN {STR})
    Enable/Disable(TEXTURE GEN S,T,R,Q)                                              –              –


4.2     Texture Addressing Modes
For cubemaps, the only allowed texture addressing mode is CLAMP TO EDGE.


4.3     Texture Completeness
For cube map textures, a texture is cube complete if the following conditions all hold true:

     • the base level arrays of each of the six texture images making up the cube map have identical, positive,
       and square dimensions.

     • the base level arrays were specified with the same type.

    Finally, a cube map texture is mipmap cube complete if, in addition to being cube complete, each of the
six texture images considered individually is complete.

    OpenGL 1.5                                                                  Common         Common-Lite
    TexImage2D(enum target, int level, int internalFormat, sizei width, sizei
    height, int border, enum format, enum type, const void *pixels)
      target = TEXTURE CUBE MAP POSITIVE X, border = 0           ‡           ‡

      target = TEXTURE CUBE MAP POSITIVE Y, border = 0           ‡           ‡

      target = TEXTURE CUBE MAP POSITIVE Z, border = 0           ‡           ‡

      target = TEXTURE CUBE MAP NEGATIVE X, border = 0           ‡           ‡

      target = TEXTURE CUBE MAP NEGATIVE Y, border = 0           ‡           ‡

      target = TEXTURE CUBE MAP NEGATIVE Z, border = 0           ‡           ‡

    CompressedTexImage2D(enum target, int level, enum internalformat, sizei
    width, sizei height, int border, sizei imageSize, const void *data)
      target = TEXTURE CUBE MAP POSITIVE X, border = 0           ‡           ‡

      target = TEXTURE CUBE MAP POSITIVE Y, border = 0           ‡           ‡

      target = TEXTURE CUBE MAP POSITIVE Z, border = 0           ‡           ‡

      target = TEXTURE CUBE MAP NEGATIVE X, border = 0           ‡           ‡

      target = TEXTURE CUBE MAP NEGATIVE Y, border = 0           ‡           ‡

      target = TEXTURE CUBE MAP NEGATIVE Z, border = 0           ‡           ‡

    TexParameter{if}[v](enum target, enum pname, T param)
      target = TEXTURE CUBE MAP,                                            †
Cube Maps                                                                                           7


 OpenGL 1.5                                                            Common         Common-Lite
 BindTexture(enum target, uint texture)
   target = TEXTURE CUBE MAP
 Enable/Disable(enum cap)
   cap = TEXTURE CUBE MAP
 GetTexGen{ifx}v(enum env, enum pname, T *params)                             ♦             †
 GetTexGen{d}v(enum env, enum pname, T *params)                               –             –


                                                                   Common          Common-Lite
     State                              Exposed    Queriable
                                                                     Get                Get
     TEXTURE   CUBE MAP                                           IsEnabled          IsEnabled
     TEXTURE   BINDING CUBE MAP                                  GetIntegerv        GetIntegerv
     TEXTURE   CUBE MAP POSITIVE   X                   –              –                  –
     TEXTURE   CUBE MAP NEGATIVE   X                   –              –                  –
     TEXTURE   CUBE MAP POSITIVE   Y                   –              –                  –
     TEXTURE   CUBE MAP NEGATIVE   Y                   –              –                  –
     TEXTURE   CUBE MAP POSITIVE   Z                   –              –                  –
     TEXTURE   CUBE MAP NEGATIVE   Z                   –              –                  –

                                   Table 4.3: Texture Objects



                                                                 Common           Common-Lite
      State                            Exposed    Queriable
                                                                    Get                Get
      MAX CUBE MAP TEXTURE SIZE                                 GetIntegerv        GetIntegerv

                         Table 4.4: Implementation Dependent Values
Chapter 5

Blending Extensions

The OES blend subtract extension adds two additional blending equations FUNC SUBTRACT and FUNC -
REVERSE SUBTRACT

 OpenGL 1.5                                                                   Common      Common-Lite
 BlendEquation(enum mode)
   mode = FUNC SUBTRACT
   mode = FUNC REVERSE SUBTRACT

    The OES blend func separate extension extends the blending capability by defining a function that
allows independent setting of the RGB and alpha blend factors for blend operations that require source and
destination blend factors. It is not always desired that the blending used for RGB is also applied to alpha.

 OpenGL 1.5                                                                   Common      Common-Lite
 BlendFuncSeparate(enum srcRGB, enum dstRGB, enum
 srcAlpha, enum dstAlpha)


                                                                         Common         Common-Lite
    State                                      Exposed     Queriable
                                                                            Get              Get
    BLEND   SRC   RGB (v1.1 BLEND SRC)                                  GetIntegerv      GetIntegerv
    BLEND   DST   RGB (v1.1 BLEND DST)                                  GetIntegerv      GetIntegerv
    BLEND   SRC   ALPHA                                                 GetIntegerv      GetIntegerv
    BLEND   DST   ALPHA                                                 GetIntegerv      GetIntegerv

                                        Table 5.3: Pixel Operations


   The OES blend equation separate extension provides a separate blend equation for RGB and al-
pha to match the generality available for blend factors.

 OpenGL 1.5                                                                   Common      Common-Lite
 BlendEquationSeparate(enum modeRGB, enum modeAlpha)




                                                     8
Blending Extensions                                                                   9




                                                          Common       Common-Lite
         State                  Exposed    Queriable
                                                             Get            Get
         BLEND EQUATION RGB                              GetIntegerv    GetIntegerv
         BLEND EQUATION ALPHA                            GetIntegerv    GetIntegerv

                                Table 5.5: Pixel Operations
Chapter 6

Stencil Extensions

The OES stencil wrap extension extends the StencilOp functions to support INCR WRAP and DECR WRAP
modes.

 OpenGL 1.5                                                           Common     Common-Lite
 StencilOp(enum fail, enum zfail, enum zpass)
   fail, zfail, zpass = INCR WRAP
   fail, zfail, zpass = DECR WRAP




                                               10
Chapter 7

Extended Matrix Palette

Name

   OES_extended_matrix_palette

Name Strings

   GL_OES_extended_matrix_palette

Contact

   Aaftab Munshi (amunshi@ati.com)

Status

   Ratified by the Khronos BOP, July 22, 2005.

Version


Number


Dependencies

   OES_matrix_palette is required
   OpenGL ES 1.1 is required.

Overview

   The OES_matrix_palette extension added the ability to support vertex skinning
   in OpenGL ES. One issue with OES_matrix_palette is that the minimum size of
   the matrix palette is very small. This leads to applications having to break
   geometry into smaller primitive sets called via. glDrawElements. This has an
   impact on the overall performance of the OpenGL ES implementation. In general,
   hardware implementations prefer primitive packets with as many triangles as
   possible. The default minimum size defined in OES_matrix_palette is not
   sufficient to allow this. The OES_extended_matrix_palette extension increases

                                     11
12                                                             Extended Matrix Palette


     this minimum from 9 to 32.

Another issue is that it is very difficult for ISVs to handle different
size matrix palettes as it affects how they store their geometry
in the database - may require multiple representations which is
not really feasible. So the minimum size is going to be what most ISVs
will use.

By extending the minimum size of the matrix palette, we remove this
fragmentation and allow applications to render geometry with minimal
number of calls to glDrawElements or glDrawArrays. The OpenGL ES
implementation can support this without requiring any additional hardware
by breaking the primitive, plus it gives implementations the flexibility
to accelerate with a bigger matrix palette if they choose to do so.

Additionally, feedback has also been received to increase the number of
matrices that are blend per vertex from 3 to 4. The OES_extended_matrix_palette
extension increases the minium number of matrices / vertex to 4.

IP Status

     None.

Issues

     None

New Procedures and Functions

     None

New Tokens

     No new tokens added except that the default values for
     MAX_PALETTE_MATRICES_OES and MAX_VERTEX_UNITS_OES are 32 and 4 respectively.

Additions to Chapter 2 of the OpenGL ES 1.0 Specification

     None

Errors

     None

New State

Get Value                   Type   Command       Value     Description
---------                   ----   -------       -------   -----------

MAX_PALETTE_MATRICES_OES    Z+     GetIntegerv   32        size of matrix palette
MAX_VERTEX_UNITS_OES        Z+     GetIntegerv   4         number of matrices per vertex
Extended Matrix Palette                                              13


Revision History

     Feb 03, 2005         Aaftab Munshi   First draft of extension
Chapter 8

Framebuffer Objects

Name

   OES_framebuffer_object

Name Strings

   GL_OES_framebuffer_object

Contact

   Aaftab Munshi (amunshi@ati.com)

IP Status

   None.

Status

   Ratified by the Khronos BOP, July 22, 2005.

Version

   Last Modified Date:      July 18, 2005


Number


Dependencies

   OpenGL ES 1.0 is required.

   EXT_framebuffer_object is required.

Overview

   This extension defines a simple interface for drawing to rendering

                                       14
Framebuffer Objects                                                           15


     destinations other than the buffers provided to the GL by the
     window-system. OES_framebuffer_object is a simplified version
     of EXT_framebuffer_object with modifications to match the needs of
     OpenGL ES.

     In this extension, these newly defined rendering destinations are
     known collectively as "framebuffer-attachable images". This
     extension provides a mechanism for attaching framebuffer-attachable
     images to the GL framebuffer as one of the standard GL logical
     buffers: color, depth, and stencil. When a framebuffer-attachable
     image is attached to the framebuffer, it is used as the source and
     destination of fragment operations as described in Chapter 4.

     By allowing the use of a framebuffer-attachable image as a rendering
     destination, this extension enables a form of "offscreen" rendering.
     Furthermore, "render to texture" is supported by allowing the images
     of a texture to be used as framebuffer-attachable images. A
     particular image of a texture object is selected for use as a
     framebuffer-attachable image by specifying the mipmap level, cube
     map face (for a cube map texture) that identifies the image.
     The "render to texture" semantics of this extension are similar to
     performing traditional rendering to the framebuffer, followed
     immediately by a call to CopyTexSubImage. However, by using this
     extension instead, an application can achieve the same effect,
     but with the advantage that the GL can usually eliminate the data copy
     that would have been incurred by calling CopyTexSubImage.

     This extension also defines a new GL object type, called a
     "renderbuffer", which encapsulates a single 2D pixel image. The
     image of renderbuffer can be used as a framebuffer-attachable image
     for generalized offscreen rendering and it also provides a means to
     support rendering to GL logical buffer types which have no
     corresponding texture format (stencil etc). A renderbuffer
     is similar to a texture in that both renderbuffers and textures can
     be independently allocated and shared among multiple contexts. The
     framework defined by this extension is general enough that support
     for attaching images from GL objects other than textures and
     renderbuffers could be added by layered extensions.

     To facilitate efficient switching between collections of
     framebuffer-attachable images, this extension introduces another new
     GL object, called a framebuffer object. A framebuffer object
     contains the state that defines the traditional GL framebuffer,
     including its set of images. Prior to this extension, it was the
     window-system which defined and managed this collection of images,
     traditionally by grouping them into a "drawable". The window-system
     API’s would also provide a function (i.e., eglMakeCurrent) to bind a
     drawable with a GL context. In this extension however, this
     functionality is subsumed by the GL and the GL provides the function
     BindFramebufferOES to bind a framebuffer object to the current context.
     Later, the context can bind back to the window-system-provided framebuffer
     in order to display rendered content.
16                                                             Framebuffer Objects



     Previous extensions that enabled rendering to a texture have been
     much more complicated. One example is the combination of
     ARB_pbuffer and ARB_render_texture, both of which are window-system
     extensions. This combination requires calling MakeCurrent, an
     operation that may be expensive, to switch between the window and
     the pbuffer drawables. An application must create one pbuffer per
     renderable texture in order to portably use ARB_render_texture. An
     application must maintain at least one GL context per texture
     format, because each context can only operate on a single
     pixelformat or FBConfig. All of these characteristics make
     ARB_render_texture both inefficient and cumbersome to use.

     OES_framebuffer_object, on the other hand, is both simpler to use
     and more efficient than ARB_render_texture. The
     OES_framebuffer_object API is contained wholly within the GL API and
     has no (non-portable) window-system components. Under
     OES_framebuffer_object, it is not necessary to create a second GL
     context when rendering to a texture image whose format differs from
     that of the window. Finally, unlike the pbuffers of
     ARB_render_texture, a single framebuffer object can facilitate
     rendering to an unlimited number of texture objects.

     Please refer to the EXT_framebuffer_object extension for a
     detailed explaination of how framebuffer objects are supposed to work,
     the issues and their resolution. This extension can be found at
     http://oss.sgi.com/projects/ogl-sample/registry/EXT/framebuffer_object.txt

New Tokens

     Accepted by the <internalformat> parameter of RenderbufferStorageOES

        RGB565_OES                0x8D62


New Procedures and Functions

     boolean IsRenderbufferOES(uint renderbuffer);
     void BindRenderbufferOES(enum target, uint renderbuffer);
     void DeleteRenderbuffersOES(sizei n, const uint *renderbuffers);
     void GenRenderbuffersOES(sizei n, uint *renderbuffers);

     void RenderbufferStorageOES(enum target, enum internalformat,
                                 sizei width, sizei height);

     void GetRenderbufferParameterivOES(enum target, enum pname, int* params);

     boolean IsFramebufferOES(uint framebuffer);
     void BindFramebufferOES(enum target, uint framebuffer);
     void DeleteFramebuffersOES(sizei n, const uint *framebuffers);
     void GenFramebuffersOES(sizei n, uint *framebuffers);
Framebuffer Objects                                                           17


     enum CheckFramebufferStatusOES(enum target);

     void FramebufferTexture2DOES(enum target, enum attachment,
                                  enum textarget, uint texture,
                                  int level);

     void FramebufferRenderbufferOES(enum target, enum attachment,
                                     enum renderbuffertarget, uint renderbuffer);

     void GetFramebufferAttachmentParameterivOES(enum target, enum attachment,
                                                 enum pname, int *params);

     void GenerateMipmapOES(enum target);


OES_framebuffer_object implements the functionality defined by EXT_framebuffer_object
with the following limitations:

     - there is no support for DrawBuffer{s}, ReadBuffer{s}.

     - FramebufferTexture2DOES can be used to render
       directly into the base level of a texture image only.   Rendering to any
       mip-level other than the base level is not supported.

     - FramebufferTexture3DOES is not supported as OpenGL ES 1.1 and 2.0 does
       not support 3D textures. Support for 3D textures in OpenGL ES 2.0 is
       provided by the OES_texture_3D optional extension. FramebufferTexture3DOES
       has been moved to this extension specification.

     - section 4.4.2.1 of the EXT_framebuffer_object spec describes the function
       RenderbufferStorageEXT. This function establishes the data storage, format,
       and dimensions of a renderbuffer object’s image. <target> must be
       RENDERBUFFER_EXT. <internalformat> must be one of the internal formats
       from table 3.16 or table 2.nnn which has a base internal format of RGB, RGBA,
       DEPTH_COMPONENT, or STENCIL_INDEX.

       The above paragraph is modified by OES_framebuffer_object and states thus:

       "This function establishes the data storage, format, and
       dimensions of a renderbuffer object’s image. <target> must be RENDERBUFFER_OES.
       <internalformat> must be one of the sized internal formats from the following
       table which has a base internal format of RGB, RGBA, DEPTH_COMPONENT,
       or STENCIL_INDEX"

        The following formats are required:

                      Sized             Base
                      Internal Format   Internal format
                      ---------------   ---------------
                      RGB565_OES        RGB
                      RGBA4             RGBA
                      RGB5_A1           RGBA
18                                                             Framebuffer Objects


                  DEPTH_COMPONENT_16   DEPTH_COMPONENT

        The following formats are optional:

                  Sized                Base
                  Internal Format      Internal format
                  ---------------      ---------------
                  RGBA8                RGBA
                  RGB8                 RGB
                  DEPTH_COMPONENT_24   DEPTH_COMPONENT
                  DEPTH_COMPONENT_32   DEPTH_COMPONENT
                  STENCIL_INDEX1_OES   STENCIL_INDEX
                  STENCIL_INDEX4_OES   STENCIL_INDEX
                  STENCIL_INDEX8_OES   STENCIL_INDEX


       The optional formats are described by the OES_rgb8_rgba8, OES_depth24,
       OES_depth32, OES_stencil1, OES_stencil4, and OES_stencil8 extensions.
       Even though these formats are optional in this extension, the OpenGL ES
       APIs (1.x and 2.x versions) can mandate some or all of these optional formats.

       If RenderbufferStorageOES is called with an <internalformat> value that is
       not supported by the OpenGL ES implementation, an INVALID_ENUM error will
       be generated.

Revision History

     02/25/2005    Aaftab Munshi   First draft of extension
     04/27/2005    Aaftab Munshi   Added additional limitations to simplify
                                   OES_framebuffer_object implementations
     07/06/2005    Aaftab Munshi   Added GetRenderbufferStorageFormatsOES
                                   removed limitations that were added to OES
                                   version of RenderbufferStorage,
                                   and FramebufferTexture2DOES.
     07/07/2005    Aaftab Munshi   Removed GetRenderbufferStorageFormatsOES
                                   after discussions with Jeremy Sandmel,
                                   and added specific extensions for the
                                   optional renderbuffer storage foramts
     07/18/2005    Aaftab Munshi   Added comment that optional formats can
                                   be mandated by OpenGL ES APIs.
