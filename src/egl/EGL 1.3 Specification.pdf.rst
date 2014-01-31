Khronos Native Platform Graphics Interface
           (EGL Version 1.3)
          (December 4, 2006)

               Editor: Jon Leech
2


     Copyright (c) 2002-2006 The Khronos Group Inc. All Rights Reserved.

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
                                                    R
This document is a derivative work of ”OpenGL Graphics with the X Window
System (Version 1.4)”. Silicon Graphics, Inc. owns, and reserves all rights in, the
latter document.
Khronos is a trademark of The Khronos Group Inc. OpenGL is a registered trade-
mark, and OpenGL ES is a trademark, of Silicon Graphics, Inc.


                          Version 1.3 - December 4, 2006
Contents

1   Overview                                                                                              1

2   EGL Operation                                                                                         2
    2.1 Native Window System and Rendering APIs          .   .   .   .   .   .   .   .   .   .   .   .    2
        2.1.1 Scalar Types . . . . . . . . . . . .       .   .   .   .   .   .   .   .   .   .   .   .    2
        2.1.2 Displays . . . . . . . . . . . . . .       .   .   .   .   .   .   .   .   .   .   .   .    3
    2.2 Rendering Contexts and Drawing Surfaces .        .   .   .   .   .   .   .   .   .   .   .   .    3
        2.2.1 Using Rendering Contexts . . . . .         .   .   .   .   .   .   .   .   .   .   .   .    4
        2.2.2 Rendering Models . . . . . . . . .         .   .   .   .   .   .   .   .   .   .   .   .    4
        2.2.3 Interaction With Native Rendering .        .   .   .   .   .   .   .   .   .   .   .   .    5
    2.3 Direct Rendering and Address Spaces . . .        .   .   .   .   .   .   .   .   .   .   .   .    6
    2.4 Shared State . . . . . . . . . . . . . . . . .   .   .   .   .   .   .   .   .   .   .   .   .    6
        2.4.1 OpenGL ES Texture Objects . . . .          .   .   .   .   .   .   .   .   .   .   .   .    7
        2.4.2 OpenGL ES Vertex Buffer Objects .          .   .   .   .   .   .   .   .   .   .   .   .    7
    2.5 Multiple Threads . . . . . . . . . . . . . .     .   .   .   .   .   .   .   .   .   .   .   .    7
    2.6 Power Management . . . . . . . . . . . . .       .   .   .   .   .   .   .   .   .   .   .   .    8

3   EGL Functions and Errors                                                                              9
    3.1 Errors . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .                            9
    3.2 Initialization . . . . . . . . . . . . . . . . . . . . . . . . . . . . .                         11
    3.3 EGL Versioning . . . . . . . . . . . . . . . . . . . . . . . . . . .                             12
    3.4 Configuration Management . . . . . . . . . . . . . . . . . . . . .                               13
        3.4.1 Querying Configurations . . . . . . . . . . . . . . . . . .                                19
        3.4.2 Lifetime of Configurations . . . . . . . . . . . . . . . . .                               23
        3.4.3 Querying Configuration Attributes . . . . . . . . . . . . .                                23
    3.5 Rendering Surfaces . . . . . . . . . . . . . . . . . . . . . . . . .                             24
        3.5.1 Creating On-Screen Rendering Surfaces . . . . . . . . . .                                  24
        3.5.2 Creating Off-Screen Rendering Surfaces . . . . . . . . . .                                 25
        3.5.3 Binding Off-Screen Rendering Surfaces To Client Buffers                                    28

                                          i
ii                                                                         CONTENTS


          3.5.4 Creating Native Pixmap Rendering Surfaces . . .        .   .   .   .   .   30
          3.5.5 Destroying Rendering Surfaces . . . . . . . . .        .   .   .   .   .   31
          3.5.6 Surface Attributes . . . . . . . . . . . . . . . .     .   .   .   .   .   31
     3.6 Rendering to Textures . . . . . . . . . . . . . . . . . . .   .   .   .   .   .   34
          3.6.1 Binding a Surface to a OpenGL ES Texture . . .         .   .   .   .   .   34
          3.6.2 Releasing a Surface from an OpenGL ES Texture          .   .   .   .   .   36
          3.6.3 Implementation Caveats . . . . . . . . . . . . .       .   .   .   .   .   37
     3.7 Rendering Contexts . . . . . . . . . . . . . . . . . . . .    .   .   .   .   .   37
          3.7.1 Creating Rendering Contexts . . . . . . . . . . .      .   .   .   .   .   38
          3.7.2 Destroying Rendering Contexts . . . . . . . . .        .   .   .   .   .   39
          3.7.3 Binding Contexts and Drawables . . . . . . . . .       .   .   .   .   .   40
          3.7.4 Context Queries . . . . . . . . . . . . . . . . .      .   .   .   .   .   42
     3.8 Synchronization Primitives . . . . . . . . . . . . . . . .    .   .   .   .   .   44
     3.9 Posting the Color Buffer . . . . . . . . . . . . . . . . .    .   .   .   .   .   45
          3.9.1 Posting to a Window . . . . . . . . . . . . . . .      .   .   .   .   .   45
          3.9.2 Copying to a Native Pixmap . . . . . . . . . . .       .   .   .   .   .   46
          3.9.3 Posting Semantics . . . . . . . . . . . . . . . .      .   .   .   .   .   46
          3.9.4 Posting Errors . . . . . . . . . . . . . . . . . .     .   .   .   .   .   47
     3.10 Obtaining Extension Function Pointers . . . . . . . . . .    .   .   .   .   .   48
     3.11 Releasing Thread State . . . . . . . . . . . . . . . . . .   .   .   .   .   .   49

4    Extending EGL                                                                         50

5    EGL Versions, Header Files, and Enumerants                                            51
     5.1 Header Files . . . . . . . . . . . . . . . . . . . . . . . . . . . . .            51
     5.2 Compile-Time Version Detection . . . . . . . . . . . . . . . . . .                52
     5.3 Enumerant Values and Header Portability . . . . . . . . . . . . .                 52

6    Glossary                                                                              53

A Version 1.0                                                                              55
  A.1 Acknowledgements . . . . . . . . . . . . . . . . . . . . . . . . .                   55

B Version 1.1                                                                              57
  B.1 Revision 1.1.2 . . . . . . . . . . . . . . . . . . . . . . . . . . . .               57
  B.2 Acknowledgements . . . . . . . . . . . . . . . . . . . . . . . . .                   57

C Version 1.2                                                                              59
  C.1 Acknowledgements . . . . . . . . . . . . . . . . . . . . . . . . .                   59

                          Version 1.3 - December 4, 2006
CONTENTS                                                                   iii


D Version 1.3                                                              61
  D.1 Acknowledgements . . . . . . . . . . . . . . . . . . . . . . . . .   61

   Index of EGL Commands                                                   64




                       Version 1.3 - December 4, 2006
List of Tables

 3.1   EGLConfig attributes. . . . . . . . . . . . . . . . . . . . .     .   .   .   14
 3.2   Types of surfaces supported by an EGLConfig . . . . . . .         .   .   .   16
 3.3   Types of client APIs supported by an EGLConfig . . . . .          .   .   .   17
 3.4   Default values and match criteria for EGLConfig attributes.       .   .   .   22
 3.5   Queryable surface attributes and types. . . . . . . . . . . . .   .   .   .   32
 3.6   Size of texture components . . . . . . . . . . . . . . . . . .    .   .   .   35

 D.1 Renamed tokens . . . . . . . . . . . . . . . . . . . . . . . . . . .            62




                                      iv
Chapter 1

Overview

This document describes EGL, an interface between rendering APIs such as
OpenGL ES or OpenVG (referred to collectively as client APIs ) and an underlying
native platform window system. It refers to concepts discussed in the OpenGL ES
and OpenVG specifications, and should be read together with those documents.
EGL uses OpenGL ES conventions for naming entry points and macros.
    EGL provides mechanisms for creating rendering surfaces onto which client
APIs can draw, creating graphics contexts for client APIs , and synchronizing
drawing by client APIs as well as native platform rendering APIs. EGL does not
explicitly support remote or indirect rendering, unlike the similar GLX API.




                                       1
Chapter 2

EGL Operation

2.1     Native Window System and Rendering APIs

EGL is intended to be implementable on multiple operating systems (such as Sym-
bian, embedded Linux, Unix, and Windows) and native window systems (such as
X and Microsoft Windows). Implementations may also choose to allow rendering
into specific types of EGL surfaces via other supported native rendering APIs, such
as Xlib or GDI. Native rendering is described in more detail in section 2.2.3.
    To the extent possible, EGL itself is independent of definitions and concepts
specific to any native window system or rendering API. However, there are a few
places where native concepts must be mapped into EGL-specific concepts, includ-
ing the definition of the display on which graphics are drawn, and the definition of
native windows and pixmaps which can also support client API rendering.



2.1.1   Scalar Types

EGLBoolean is an integral type representing a boolean value, and should only
take on the values EGL TRUE (1) and EGL FALSE (0). If boolean parameters passed
to EGL take on other values, behavior is undefined, although typically any non-zero
value will be interpreted as EGL TRUE.
    EGLint is an integral type used because EGL may need to represent scalar
values larger than the native platform ”int” type. All legal attribute names and
values, whether their type is boolean, bitmask, enumerant (symbolic constant),
integer, handle, or other, may be converted to and from EGLint without loss of
information.

                                         2
2.2. RENDERING CONTEXTS AND DRAWING SURFACES                                        3


2.1.2    Displays
Most EGL calls include an EGLDisplay parameter. This represents the abstract
display on which graphics are drawn. In most environments a display corresponds
to a single physical screen. The initialization routines described in section 3.2
include a method for querying a default display, and platform-specific EGL exten-
sions may be defined to obtain other displays.


2.2      Rendering Contexts and Drawing Surfaces
The OpenGL ES and OpenVG specifications are intentionally vague on how a ren-
dering context (e.g. the state machine defined by a client API ) is created. One
of the purposes of EGL is to provide a means to create client API rendering con-
texts (henceforth simply referred to as contexts), and associate them with drawing
surfaces.
    EGL defines several types of drawing surfaces collectively referred to as
EGLSurfaces. These include windows, used for onscreen rendering; pbuffers,
used for offscreen rendering; and pixmaps, used for offscreen rendering into buffers
that may be accessed through native APIs. EGL windows and pixmaps are tied to
native window system windows and pixmaps.
    EGLSurfaces are created with respect to an EGLConfig. The EGLConfig
describes the depth of the color buffer components and the types, quantities and
sizes of the ancillary buffers (i.e., the depth, multisample, and stencil buffers).
    Ancillary buffers are associated with an EGLSurface, not with a context. If
several contexts are all writing to the same surface, they will share those buffers.
Rendering operations to one window never affect the unobscured pixels of another
window, or the corresponding pixels of ancillary buffers of that window.
    Contexts for different client APIs all share the color buffer of a surface, but
ancillary buffers are not necessarily meaningful for every client API . In particular,
depth, multisample, and stencil buffers are currently used only by OpenGL ES .
    A context can be used with any EGLSurface that it is compatible with (sub-
ject to the restrictions discussed in the section on address space). A surface and
context are compatible if

   • They support the same type of color buffer (RGB or luminance).

   • They have color buffers and ancillary buffers of the same depth.
        Depth is measured per-component. For example, color buffers in RGB565
        and RGBA4444 formats have the same aggregate depth of 16 bits/pixel, but
        are not compatible because their per-component depths are different.

                          Version 1.3 - December 4, 2006
4                                                CHAPTER 2. EGL OPERATION


        Ancillary buffers not meaningful to a client API do not affect compatibility;
        for example, a surface with both color and stencil buffers will be compat-
        ible with an OpenVG context so long as the color buffers associated with
        the contexts are of the same depth. The stencil buffer is irrelevant because
        OpenVG does not use it.

    • The surface was created with respect to an EGLConfig supporting client
      API rendering of the same type as the API type of the context (in environ-
      ments supporting multiple client APIs ).

    • They were created with respect to the same EGLDisplay (in environments
      supporting multiple displays).

     As long as the compatibility constraint and the address space requirement are
satisfied, clients can render into the same EGLSurface using different contexts.
It is also possible to use a single context to render into multiple EGLSurfaces.

2.2.1    Using Rendering Contexts
OpenGL ES defines both client state and server state. Thus an OpenGL ES context
consists of two parts: one to hold the client state and one to hold the server state.
OpenVG does not separate client and server state.
    Both the OpenGL ES and OpenVG client APIs rely on an implicit context used
by all entry points, rather than passing an explicit context parameter. The implicit
context for each API is set with EGL calls (see section 3.7.3). The implicit contexts
used by these APIs are called current contexts.
    Each thread can have at most one current rendering context for each supported
client API ; for example, there may be both a current OpenGL ES context and
a current OpenVG context in an implementation supporting both of these APIs.
In addition, a context can be current to only one thread at a time. The client is
responsible for creating contexts and surfaces.

2.2.2    Rendering Models
EGL and OpenGL ES supports two rendering models: back buffered and single
buffered.
    Back buffered rendering is used by window and pbuffer surfaces. Memory for
the color buffer used during rendering is allocated and owned by EGL. When the
client is finished drawing a frame, the back buffer may be copied to a visible win-
dow using eglSwapBuffers. Pbuffer surfaces have a back buffer but no associated
window, so the back buffer need not be copied.

                           Version 1.3 - December 4, 2006
2.2. RENDERING CONTEXTS AND DRAWING SURFACES                                      5


     Single buffered rendering is used by pixmap surfaces. Memory for the color
buffer is specified at surface creation time in the form of a native pixmap, and
client APIs are required to use that memory during rendering. When the client
is finished drawing a frame, the native pixmap contains the final image. Pixmap
surfaces typically do not support multisampling, since the native pixmap used as
the color buffer is unlikely to provide space to store multisample information.
     Some client APIs , such as OpenVG , also support single buffered rendering
to window surfaces. This behavior can be selected when creating the window sur-
face, as defined in section 3.5.1. When mixing use of client APIs which do not
support single buffered rendering into windows, like OpenGL ES , with client
APIs which do support it, back color buffers and visible window contents must
be kept consistent when binding window surfaces to contexts for each API type
(see section 3.7.3).
     Both back and single buffered surfaces may also be copied to a specified native
pixmap using eglCopyBuffers.


Window Resizing

EGL window surfaces need to be resized when their corresponding native window
is resized. Implementations typically use hooks into the OS and native window
system to perform this resizing on demand, transparently to the client. Some imple-
mentations may instead define an EGL extension giving explicit control of surface
resizing.
    Implementations which cannot resize EGL window surfaces on demand must
instead respond to native window size changes in eglSwapBuffers (see sec-
tion 3.9.3).


2.2.3   Interaction With Native Rendering
Native rendering will always be supported by pixmap surfaces (to the extent that
native rendering APIs can draw to native pixmaps). Pixmap surfaces are typically
used when mixing native and client API rendering is desirable, since there is no
need to move data between the back buffer visible to the client APIs and the native
pixmap visible to native rendering APIs. However, pixmap surfaces may, for the
same reason, have restricted capabilities and performance relative to window and
pbuffer surfaces.
    Native rendering will not be supported by pbuffer surfaces, since the color
buffers of pbuffers are allocated internally by EGL and are not accessible through
any other means.

                         Version 1.3 - December 4, 2006
6                                                 CHAPTER 2. EGL OPERATION


    Native rendering may be supported by window surfaces, but only if the native
window system has a compatible rendering model allowing it to share the back
color buffer, or if single buffered rendering to the window surface is being done.
    When both native rendering APIs and client APIs are drawing into the same
underlying surface, no guarantees are placed on the relative order of completion
of operations in the different rendering streams other than those provided by the
synchronization primitives discussed in section 3.8.
    Some state is shared between client APIs and the underlying native window
system and rendering APIs, including color buffer values in window and pixmap
surfaces.


2.3    Direct Rendering and Address Spaces
EGL is assumed to support only direct rendering, unlike similar APIs such as GLX.
EGL objects and related context state cannot be used outside of the address space
in which they are created. In a single-threaded environment, each process has its
own address space. In a multi-threaded environment, all threads may share the
same virtual address space; however, this capability is not required, and imple-
mentations may choose to restrict their address space to be per-thread even in an
environment supporting multiple application threads.
    Context state, including both the client and server state of OpenGL ES contexts,
exists in the client’s address space; this state cannot be shared by a client in another
process.
    Support of indirect rendering (in those environments where this concept makes
sense) may have the effect of relaxing these limits on sharing. However, such
support is beyond the scope of this document.


2.4    Shared State
Most context state is small. However, some types are of state are potentially large
and/or expensive to copy, in which case it may be desirable for multiple contexts
to share such state rather than replicating it in each context. Such state may only
be shared between different contexts of the same API type; that is, two OpenGL
ES contexts may share state, or two OpenVG contexts, but an OpenGL ES context
and an OpenVG context cannot share state.
    EGL provides for sharing certain types of context state among contexts existing
in a single address space. OpenGL ES contexts may share texture objects, shader
and program objects, and vertex buffer objects. OpenVG contexts may share im-
ages, paint objects, and paths. Additional types of state may be shared in future

                          Version 1.3 - December 4, 2006
2.5. MULTIPLE THREADS                                                              7


revisions of client APIs where such types of state (for example, display lists) are
defined and where such sharing makes sense.


2.4.1   OpenGL ES Texture Objects
OpenGL ES texture state can be encapsulated in a named texture object. A tex-
ture object is created by binding an unused name to one of the supported tex-
ture targets (GL TEXTURE 2D, GL TEXTURE 3D, or GL TEXTURE CUBE MAP) of an
OpenGL ES context. When a texture object is bound, OpenGL ES operations on
the target to which it is bound affect the bound texture object, and queries of the
target to which it is bound return state from the bound texture object.
    OpenGL ES makes no attempt to synchronize access to texture objects. If a
texture object is bound to more than one context, then it is up to the programmer to
ensure that the contents of the object are not being changed via one context while
another context is using the texture object for rendering. The results of changing a
texture object while another context is using it are undefined.
    All modifications to shared context state as a result of executing glBindTexture
are atomic. Also, a texture object will not be deleted while it is still bound to any
context.


2.4.2   OpenGL ES Vertex Buffer Objects
Vertex buffer objects (VBOs) were introduced in OpenGL ES 1.1. If a VBO is
bound to more than one context, then it is up to the programmer to ensure that the
contents of the object are not being changed via one context while another context
is using the VBO for rendering. The results of changing a VBO while another
context is using it are undefined.
    All modifications to shared context state as a result of executing glBindBuffer
are atomic. Also, a VBO will not be deleted while it is still bound to any context.


2.5     Multiple Threads
EGL and its client APIs must be threadsafe. Interrupt routines may not share a
context with their main thread.
   EGL guarantees sequentiality within a command stream for each of its client
APIs such as OpenGL ES and OpenVG , but not between these APIs and native
APIs which may also be rendering into the same surface. It is possible, for ex-
ample, that a native drawing command issued by a single threaded client after an
OpenGL ES command might be executed before that OpenGL ES command.

                          Version 1.3 - December 4, 2006
8                                                CHAPTER 2. EGL OPERATION


    Client API commands are not guaranteed to be atomic. Some such commands
might otherwise impair interactive use of the windowing system by the user. For
instance, rendering a large texture mapped polygon on a system with no graphics
hardware, or drawing a large OpenGL ES vertex array, could prevent a user from
popping up a menu soon enough to be usable.
    Synchronization is in the hands of the client. It can be maintained at moderate
cost with the judicious use of commands such as glFinish, vgFinish, eglWait-
Client, and eglWaitNative, as well as (if they exist) synchronization commands
present in native rendering APIs. Client API and native rendering can be done
in parallel so long as the client does not preclude it with explicit synchronization
calls.
    Some performance degradation may be experienced if needless switching be-
tween client APIs and native rendering is done.


2.6    Power Management
Power management events can occur asynchronously while an application is
running. When the system returns from the power management event the
EGLContext will be invalidated, and all subsequent client API calls will have
no effect (as if no context is bound).
     Following a power management event, calls to eglSwapBuffers, eglCopy-
Buffers, or eglMakeCurrent will indicate failure by returning EGL FALSE. The
error EGL CONTEXT LOST will be returned if a power management event has oc-
curred.
     On detection of this error, the application must destroy all contexts (by calling
eglDestroyContext for each context). To continue rendering the application must
recreate any contexts it requires, and subsequently restore any client API state and
objects it wishes to use.
     Any EGLSurfaces that the application has created need not be destroyed
following a power management event, but their contents will be invalid.
     Note that not all implementations can be made to generate power management
events, and developers should continue to refer to platform-specific documentation
in this area. We expected continued work in platform-specific extensions to enable
more control over power management issues, including event detection, scope and
nature of resource loss, behavior of EGL and client API calls under resource loss,
and recommended techniques for recovering from events. Future versions of EGL
may incorporate additional functionality in this area.




                          Version 1.3 - December 4, 2006
Chapter 3

EGL Functions and Errors

3.1       Errors
Where possible, when an EGL function fails it has no side effects.
    EGL functions usually return an indicator of success or failure; either an
EGLBoolean EGL TRUE or EGL FALSE value, or in the form of an out-of-band
return value indicating failure, such as returning EGL NO CONTEXT instead of a re-
quested context handle. Additional information about the success or failure of the
most recent EGL function called in a specific thread, in the form of an error code,
can be obtained by calling

         EGLint eglGetError();

       The error codes that may be returned from eglGetError, and their meanings,
are:

 EGL SUCCESS
         Function succeeded.

 EGL NOT INITIALIZED
         EGL is not initialized, or could not be initialized, for the specified display.

 EGL BAD ACCESS
         EGL cannot access a requested resource (for example, a context is bound in
         another thread).

 EGL BAD ALLOC
         EGL failed to allocate resources for the requested operation.

                                             9
10                             CHAPTER 3. EGL FUNCTIONS AND ERRORS


 EGL BAD ATTRIBUTE
      An unrecognized attribute or attribute value was passed in an attribute list.

 EGL BAD CONTEXT
      An EGLContext argument does not name a valid EGLContext.

 EGL BAD CONFIG
      An EGLConfig argument does not name a valid EGLConfig.

 EGL BAD CURRENT SURFACE
      The current surface of the calling thread is a window, pbuffer, or pixmap that
      is no longer valid.

 EGL BAD DISPLAY
      An EGLDisplay argument does not name a valid EGLDisplay; or, EGL
      is not initialized on the specified EGLDisplay.

 EGL BAD SURFACE
      An EGLSurface argument does not name a valid surface (window, pbuffer,
      or pixmap) configured for rendering.

 EGL BAD MATCH
      Arguments are inconsistent; for example, an otherwise valid context requires
      buffers (e.g. depth or stencil) not allocated by an otherwise valid surface.

 EGL BAD PARAMETER
      One or more argument values are invalid.

 EGL BAD NATIVE PIXMAP
      An EGLNativePixmapType argument does not refer to a valid native
      pixmap.

 EGL BAD NATIVE WINDOW
      An EGLNativeWindowType argument does not refer to a valid native
      window.

 EGL CONTEXT LOST
      A power management event has occurred. The application must destroy all
      contexts and reinitialise client API state and objects to continue rendering,
      as described in section 2.6.

    When there is no status to return (in other words, when eglGetError is called
as the first EGL call in a thread, or immediately after calling eglReleaseThread),
EGL SUCCESS will be returned.


                         Version 1.3 - December 4, 2006
3.2. INITIALIZATION                                                                11


     Some specific error codes that may be generated by a failed EGL func-
tion, and their meanings, are described together with each function. However,
not all possible errors are described with each function. Errors whose mean-
ings are identical across many functions (such as returning EGL BAD DISPLAY or
EGL NOT INITIALIZED for an unsuitable EGLDisplay argument) may not be
described repeatedly.
     EGL normally checks the validity of objects passed into it, but detecting invalid
native objects (pixmaps, windows, and displays) may not always be possible. Spec-
ifying such invalid handles may result in undefined behavior, although implemen-
tations should generate EGL BAD NATIVE PIXMAP and EGL BAD NATIVE WINDOW
errors if possible.


3.2    Initialization
Initialization must be performed once for each display prior to calling most other
EGL or client API functions. A display can be obtained by calling

      EGLDisplay eglGetDisplay(EGLNativeDisplayType
         display id);

The type and format of display id are implementation-specific, and it describes a
specific display provided by the system EGL is running on. For example, an EGL
implementation under X windows would require display id to be an X Display,
while an implementation under Microsoft Windows would require display id to be
a Windows Device Context. If display id is EGL DEFAULT DISPLAY, a default
display is returned.
    If no display matching display id is available, EGL NO DISPLAY is returned;
no error condition is raised in this case.
    EGL may be initialized on a display by calling

      EGLBoolean eglInitialize(EGLDisplay dpy, EGLint
         *major, EGLint *minor);

EGL TRUE is returned on success, and major and minor are updated with the major
and minor version numbers of the EGL implementation (for example, in an EGL
1.2 implementation, the values of *major and *minor would be 1 and 2, respec-
tively). major and minor are not updated if they are specified as NULL.
    EGL FALSE is returned on failure and major and minor are not updated. An
EGL BAD DISPLAY error is generated if the dpy argument does not refer to a valid


                          Version 1.3 - December 4, 2006
12                               CHAPTER 3. EGL FUNCTIONS AND ERRORS


EGLDisplay. An EGL NOT INITIALIZED error is generated if EGL cannot be
initialized for an otherwise valid dpy.
     Initializing an already-initialized display is allowed, but the only effect of such
a call is to return EGL TRUE and update the EGL version numbers. An initialized
display may be used from other threads in the same address space without being
initalized again in those threads.
     To release resources associated with use of EGL and client APIs on a display,
call

      EGLBoolean eglTerminate(EGLDisplay dpy);

Termination marks all EGL-specific resources associated with the specified display
for deletion. If contexts or surfaces created with respect to dpy are current (see
section 3.7.3) to any thread, then they are not actually released while they remain
current. Such contexts and surfaces will be destroyed, and all future references to
them will become invalid, as soon as any otherwise valid eglMakeCurrent call is
made from the thread they are bound to.
     eglTerminate returns EGL TRUE on success.
     If the dpy argument does not refer to a valid EGLDisplay, EGL FALSE is
returned, and an EGL BAD DISPLAY error is generated.
     Termination of a display that has already been terminated, or has not yet been
initialized, is allowed, but the only effect of such a call is to return EGL TRUE, since
there are no EGL resources associated with the display to release. A terminated
display may be re-initialized by calling eglInitialize again. When re-initializing
a terminated display, resources which were marked for deletion as a result of the
earlier termination remain so marked, and references to them are not valid.


3.3    EGL Versioning
      const char *eglQueryString(EGLDisplay dpy, EGLint
        name);

eglQueryString returns a pointer to a static, zero-terminated string describ-
ing some aspect of the EGL implementation running on the specified display.
name may be one of EGL CLIENT APIS, EGL EXTENSIONS, EGL VENDOR, or
EGL VERSION.
    The EGL CLIENT APIS string describes which client rendering APIs are sup-
ported. It is zero-terminated and contains a space-separated list of API names,
which must include at least one of ‘‘OpenGL ES’’ or ‘‘OpenVG’’.

                          Version 1.3 - December 4, 2006
3.4. CONFIGURATION MANAGEMENT                                                    13


     The EGL EXTENSIONS string describes which EGL extensions are supported
by the EGL implementation running on the specified display. The string is zero-
terminated and contains a space-separated list of extension names; extension names
themselves do not contain spaces. If there are no extensions to EGL, then the empty
string is returned.
     The format and contents of the EGL VENDOR string is implementation depen-
dent.
     The format of the EGL VERSION string is:

      <major version.minor version><space><vendor specific info>

Both the major and minor portions of the version number are numeric. Their values
must match the major and minor values returned by eglInitialize (see section 3.2).
The vendor-specific information is optional; if present, its format and contents are
implementation specific.
    On failure, NULL is returned. An EGL NOT INITIALIZED error is generated if
EGL is not initialized for dpy. An EGL BAD PARAMETER error is generated if name
is not one of the values described above.


3.4    Configuration Management
An EGLConfig describes the format, type and size of the color buffers and an-
cillary buffers for an EGLSurface. If the EGLSurface is a window, then the
EGLConfig describing it may have an associated native visual type.
     Names of EGLConfig attributes are shown in Table 3.1. These names may
be passed to eglChooseConfig to specify required attribute properties.
     EGL CONFIG ID is a unique integer identifying different EGLConfigs. Con-
figuration IDs must be small positive integers starting at 1 and ID assignment
should be compact; that is, if there are N EGLConfigs defined by the EGL im-
plementation, their configuration IDs should be in the range [1, N ]. Small gaps
in the sequence are allowed, but should only occur when removing configurations
defined in previous revisions of an EGL implementation.

Buffer Descriptions and Attributes

    Attributes controlling the creation of the various buffers that may be con-
tained by an EGLSurface are described below. Attribute values include the
depth of these buffers, expressed in bits/pixel component. If the depth of a buffer
in an EGLConfig is zero, then an EGLSurface created with respect to that
EGLConfig will not contain the corresponding buffer.

                         Version 1.3 - December 4, 2006
14                             CHAPTER 3. EGL FUNCTIONS AND ERRORS


             Attribute                  Type      Notes
          EGL BUFFER SIZE              integer    depth of the color buffer
             EGL RED SIZE              integer    bits of Red in the color buffer
           EGL GREEN SIZE              integer    bits of Green in the color buffer
            EGL BLUE SIZE              integer    bits of Blue in the color buffer
        EGL LUMINANCE SIZE             integer    bits of Luminance in the color buffer
           EGL ALPHA SIZE              integer    bits of Alpha in the color buffer
        EGL ALPHA MASK SIZE            integer    bits of Alpha Mask in the mask buffer
      EGL BIND TO TEXTURE RGB          boolean    True if bindable to RGB textures.
     EGL BIND TO TEXTURE RGBA          boolean    True if bindable to RGBA textures.
       EGL COLOR BUFFER TYPE            enum      color buffer type
         EGL CONFIG CAVEAT              enum      any caveats for the configuration
            EGL CONFIG ID              integer    unique EGLConfig identifier
          EGL CONFORMANT               bitmask    whether contexts created with this
                                                  config are conformant
          EGL DEPTH SIZE               integer    bits of Z in the depth buffer
            EGL LEVEL                  integer    frame buffer level
      EGL MAX PBUFFER WIDTH            integer    maximum width of pbuffer
     EGL MAX PBUFFER HEIGHT            integer    maximum height of pbuffer
     EGL MAX PBUFFER PIXELS            integer    maximum size of pbuffer
      EGL MAX SWAP INTERVAL            integer    maximum swap interval
      EGL MIN SWAP INTERVAL            integer    minimum swap interval
     EGL NATIVE RENDERABLE             boolean    EGL TRUE if native rendering
                                                  APIs can render to surface
      EGL NATIVE VISUAL ID              integer   handle of corresponding
                                                  native visual
     EGL NATIVE VISUAL TYPE             integer   native visual type of the
                                                  associated visual
       EGL RENDERABLE TYPE             bitmask    which client rendering
                                                  APIs are supported.
       EGL SAMPLE BUFFERS              integer    number of multisample buffers
           EGL SAMPLES                 integer    number of samples per pixel
        EGL STENCIL SIZE               integer    bits of Stencil in the stencil buffer
        EGL SURFACE TYPE               bitmask    which types of EGL surfaces
                                                  are supported.
     EGL TRANSPARENT TYPE                enum     type of transparency supported
   EGL TRANSPARENT RED VALUE            integer   transparent red value
 EGL TRANSPARENT GREEN VALUE            integer   transparent green value
  EGL TRANSPARENT BLUE VALUE            integer   transparent blue value

                         Table 3.1: EGLConfig attributes.
                          Version 1.3 - December 4, 2006
3.4. CONFIGURATION MANAGEMENT                                                      15


    With the exception of the color buffer, most buffers are used only by one client
API . The depth, multisample, and stencil buffers are specific to OpenGL ES ,
while the alpha mask buffer is specific to OpenVG . To conserve resources, imple-
mentations may delay creation of buffers until they are needed by EGL or a client
API . For example, if an EGLConfig describes an alpha mask buffer with depth
greater than zero, that buffer need not be allocated by a surface until an OpenVG
context is bound to that surface.
    The color buffer is shared by all client APIs rendering to a surface, and contains
pixel color values.
    EGL COLOR BUFFER TYPE indicates the color buffer type, and must be either
EGL RGB BUFFER for an RGB color buffer, or EGL LUMINANCE BUFFER for a
luminance color buffer. For an RGB buffer, EGL RED SIZE, EGL GREEN SIZE,
EGL BLUE SIZE must be non-zero, and EGL LUMINANCE SIZE must be zero. For
a luminance buffer, EGL RED SIZE, EGL GREEN SIZE, EGL BLUE SIZE must be
zero, and EGL LUMINANCE SIZE must be non-zero. For both RGB and luminance
color buffers, EGL ALPHA SIZE may be zero or non-zero (the latter indicates the
existence of a destination alpha buffer).
    If OpenGL ES rendering is supported for a luminance color buffer (as described
by the value of the EGL RENDERABLE TYPE attribute, described below), it is treated
as RGB rendering with the value of GL RED BITS equal to EGL LUMINANCE SIZE
and the values of GL GREEN BITS and GL BLUE BITS equal to zero. The red com-
ponent of fragments is written to the luminance channel of the color buffer, the
green and blue components are discarded, and the alpha component is written to
the alpha channel of the color buffer (if present).
    EGL BUFFER SIZE gives the total depth of the color buffer in bits. For an
RGB color buffer, the depth is the sum of EGL RED SIZE, EGL GREEN SIZE,
EGL BLUE SIZE, and EGL ALPHA SIZE. For a luminance color buffer, the depth is
the sum of EGL LUMINANCE SIZE and EGL ALPHA SIZE.
    The alpha mask buffer is used only by OpenVG . EGL ALPHA MASK SIZE in-
dicates the depth of this buffer.
    The depth buffer is used only by OpenGL ES . It contains fragment depth (Z)
information generated during rasterization. EGL DEPTH SIZE indicates the depth
of this buffer in bits.
    The stencil buffer is used only by OpenGL ES . It contains fragment stencil in-
formation generated during rasterization. EGL STENCIL SIZE indicates the depth
of this buffer in bits.
    The multisample buffer is used only by OpenGL ES . It contains multisam-
ple information (color values, and possibly stencil and depth values) generated by
multisample rasterization. The format of the multisample buffer is not specified,
and its contents are not directly accessible. Only the existence of the multisample

                          Version 1.3 - December 4, 2006
16                             CHAPTER 3. EGL FUNCTIONS AND ERRORS


             EGL Token Name                             Description
             EGL WINDOW BIT                  EGLConfig supports windows
             EGL PIXMAP BIT                   EGLConfig supports pixmaps
            EGL PBUFFER BIT                   EGLConfig supports pbuffers
     EGL VG COLORSPACE LINEAR BIT            EGLConfig supports OpenVG
                                               rendering in linear colorspace
      EGL VG ALPHA FORMAT PRE BIT            EGLConfig supports OpenVG
                                            rendering with premultiplied alpha

            Table 3.2: Types of surfaces supported by an EGLConfig



buffer, together with the number of samples it contains, are exposed by EGL.
    EGL SAMPLE BUFFERS indicates the number of multisample buffers, which
must be zero or one. EGL SAMPLES gives the number of samples per pixel;
if EGL SAMPLE BUFFERS is zero, then EGL SAMPLES will also be zero. If
EGL SAMPLE BUFFERS is one, then the number of color, depth, and stencil bits
for each sample in the multisample buffer are as specified by the EGL * SIZE at-
tributes.
    There are no single-sample depth or stencil buffers for a multisample
EGLConfig; the only depth and stencil buffers are those in the multisample
buffer. If the color samples in the multisample buffer store fewer bits than are
stored in the color buffers, this fact will not be reported accurately. Presumably a
compression scheme is being employed, and is expected to maintain an aggregate
resolution equal to that of the color buffers.

Other EGLConfig Attribute Descriptions

     EGL SURFACE TYPE is a mask indicating the surface types that can be created
with the corresponding EGLConfig (the config is said to support these surface
types). The valid bit settings are shown in Table 3.2.
     For example, an EGLConfig for which the value of the EGL SURFACE TYPE
attribute is
     EGL WINDOW BIT | EGL PIXMAP BIT | EGL PBUFFER BIT
can be used to create any type of EGL surface, while an EGLConfig for which this
attribute value is EGL WINDOW BIT cannot be used to create a pbuffer or pixmap.
     If EGL VG COLORSPACE LINEAR BIT is set in EGL SURFACE TYPE, then the
EGL VG COLORSPACE attribute may be set to EGL VG COLORSPACE LINEAR when
creating a window, pixmap, or pbuffer surface (see section 3.5).
     If EGL VG ALPHA FORMAT PRE BIT is set in EGL SURFACE TYPE, then the

                         Version 1.3 - December 4, 2006
3.4. CONFIGURATION MANAGEMENT                                                       17


              EGL Token Name           Client API and Version Supported
           EGL OPENGL ES BIT                   OpenGL ES 1.x
           EGL OPENGL ES2 BIT                  OpenGL ES 2.x
             EGL OPENVG BIT                      OpenVG 1.x

          Table 3.3: Types of client APIs supported by an EGLConfig



EGL VG ALPHA FORMAT attribute may be set to EGL VG ALPHA FORMAT PRE when
creating a window, pixmap, or pbuffer surface (see section 3.5).
     EGL RENDERABLE TYPE is a mask indicating which client APIs can render into
a surface created with respect to an EGLConfig. The valid bit settings are shown
in Table 3.3.
     Creation of a client API context based on an EGLConfig will fail unless the
EGLConfig’s EGL RENDERABLE TYPE attribute include the bit corresponding to
that API and version.
     EGL NATIVE RENDERABLE is an EGLBoolean indicating whether the native
window system can be used to render into a surface created with the EGLConfig.
Constraints on native rendering are discussed in more detail in sections 2.2.2
and 2.2.3.
     If an EGLConfig supports windows then it may have an associated na-
tive visual. EGL NATIVE VISUAL ID specifies an identifier for this visual, and
EGL NATIVE VISUAL TYPE specifies its type. If an EGLConfig does not sup-
port windows, or if there is no associated native visual type, then querying
EGL NATIVE VISUAL ID will return 0 and querying EGL NATIVE VISUAL TYPE
will return EGL NONE.
     The interpretation of the native visual identifier and type is platform-dependent.
For example, if the native window system is X, then the identifier will be the XID
of an X Visual.
     The EGL CONFIG CAVEAT attribute may be set to one of the following val-
ues: EGL NONE, EGL SLOW CONFIG or EGL NON CONFORMANT CONFIG. If the
attribute is set to EGL NONE then the configuration has no caveats; if it is
set to EGL SLOW CONFIG then rendering to a surface with this configuration
may run at reduced performance (for example, the hardware may not sup-
port the color buffer depths described by the configuration); if it is set to
EGL NON CONFORMANT CONFIG then rendering to a surface with this config-
uration will not pass the required OpenGL ES conformance tests (note that
EGL NON CONFORMANT CONFIG is obsolete, and the same information can be ob-
tained from the EGL CONFORMANT attribute on a per-client-API basis, not just for

                          Version 1.3 - December 4, 2006
18                                CHAPTER 3. EGL FUNCTIONS AND ERRORS


OpenGL ES ).
     OpenGL ES conformance requires that a set of EGLConfigs supporting cer-
tain defined minimum attributes (such as the number, type, and depth of supported
buffers) be supplied by any conformant implementation. Those requirements are
documented only in the conformance specification.
     EGL CONFORMANT is a mask indicating if a client API context created with
respect to the corresponding EGLConfig will pass the required conformance tests
for that API. The valid bit settings are the same as for EGL RENDERABLE TYPE, as
defined in table 3.3, but the presence or absence of each client API bit determines
whether the corresponding context will be conformant or non-conformant. 1
     EGL TRANSPARENT TYPE indicates whether or not a configuration sup-
ports transparency. If the attribute is set to EGL NONE then windows cre-
ated with the EGLConfig will not have any transparent pixels. If the at-
tribute is EGL TRANSPARENT RGB, then the EGLConfig supports transparency;
a transparent pixel will be drawn when the red, green and blue values which
are read from the framebuffer are equal to EGL TRANSPARENT RED VALUE,
EGL TRANSPARENT GREEN VALUE and EGL TRANSPARENT BLUE VALUE, re-
spectively.
     If EGL TRANSPARENT TYPE is EGL NONE, then the values for
EGL TRANSPARENT RED VALUE,              EGL TRANSPARENT GREEN VALUE,            and
EGL TRANSPARENT BLUE VALUE are undefined. Otherwise, they are interpreted
as integer framebuffer values between 0 and the maximum framebuffer value for
the component. For example, EGL TRANSPARENT RED VALUE will range between
0 and 2EGL RED SIZE − 1.
     EGL MAX PBUFFER WIDTH and EGL MAX PBUFFER HEIGHT indicate the max-
imum width and height that can be passed into eglCreatePbufferSurface, and
EGL MAX PBUFFER PIXELS indicates the maximum number of pixels (width times
height) for a pbuffer surface. Note that an implementation may return a value
for EGL MAX PBUFFER PIXELS that is less than the maximum width times the
maximum height. The value for EGL MAX PBUFFER PIXELS is static and as-
sumes that no other pbuffers or native resources are contending for the framebuffer
memory. Thus it may not be possible to allocate a pbuffer of the size given by
EGL MAX PBUFFER PIXELS.
     EGL MAX SWAP INTERVAL is the maximum value that can be passed to
eglSwapInterval, and indicates the number of swap intervals that will elapse be-
fore a buffer swap takes place after calling eglSwapBuffers. Larger values will be
silently clamped to this value.
     1
   Most EGLConfigs should be conformant for all supported client APIs . Conformance require-
ments limit the number of non-conformant configs that an implementation can define.


                            Version 1.3 - December 4, 2006
3.4. CONFIGURATION MANAGEMENT                                                      19


    EGL MIN SWAP INTERVAL is the minimum value that can be passed to
eglSwapInterval, and indicates the number of swap intervals that will elapse be-
fore a buffer swap takes place after calling eglSwapBuffers. Smaller values will
be silently clamped to this value.
    EGL BIND TO TEXTURE RGB and EGL BIND TO TEXTURE RGBA are booleans
indicating whether the color buffers of a pbuffer created with the EGLConfig can
be bound to an OpenGL ES RGB or RGBA texture respectively. Currently only
pbuffers can be bound as textures, so these attributes may only be EGL TRUE if
the value of the EGL SURFACE TYPE attribute includes EGL PBUFFER BIT. It is
possible to bind a RGBA visual to a RGB texture, in which case the values in the
alpha component of the visual are ignored when the color buffer is used as a RGB
texture.
    Implementations may choose not to support EGL BIND TO TEXTURE RGB for
RGBA visuals.


3.4.1    Querying Configurations
Use

        EGLBoolean eglGetConfigs(EGLDisplay dpy,
           EGLConfig *configs, EGLint config size,
           EGLint *num config);

to get the list of all EGLConfigs that are available on the specified display. configs
is a pointer to a buffer containing config size elements. On success, EGL TRUE is
returned. The number of configurations is returned in num config, and elements 0
through num conf ig − 1 of configs are filled in with the valid EGLConfigs. No
more than config size EGLConfigs will be returned even if more are available on
the specified display. However, if eglGetConfigs is called with configs = NULL,
then no configurations are returned, but the total number of configurations available
will be returned in num config.
     On failure, EGL FALSE is returned. An EGL NOT INITIALIZED error is gen-
erated if EGL is not initialized on dpy. An EGL BAD PARAMETER error is generated
if num config is NULL.
     Use

        EGLBoolean eglChooseConfig(EGLDisplay dpy, const
           EGLint *attrib list, EGLConfig *configs,
           EGLint config size, EGLint *num config);

                          Version 1.3 - December 4, 2006
20                              CHAPTER 3. EGL FUNCTIONS AND ERRORS


to get EGLConfigs that match a list of attributes. The return value and the mean-
ing of configs, config size, and num config are the same as for eglGetConfigs.
However, only configurations matching attrib list, as discussed below, will be re-
turned.
     On failure, EGL FALSE is returned. An EGL BAD ATTRIBUTE error is gener-
ated if attrib list contains an undefined EGL attribute or an attribute value that is
unrecognized or out of range.
     All attribute names in attrib list are immediately followed by the corresponding
desired value. The list is terminated with EGL NONE. If an attribute is not specified
in attrib list, then the default value (listed in Table 3.4) is used (it is said to be
specified implicitly). If EGL DONT CARE is specified as an attribute value, then the
attribute will not be checked. EGL DONT CARE may be specified for all attributes
except EGL LEVEL. If attrib list is NULL or empty (first attribute is EGL NONE),
then selection and sorting of EGLConfigs is done according to the default criteria
in Tables 3.4 and 3.1, as described below under Selection and Sorting.

Selection of EGLConfigs

    Attributes are matched in an attribute-specific manner, as shown in the ”Selec-
tion Critera” column of table 3.4. The criteria listed in the table have the following
meanings:

 AtLeast Only EGLConfigs with an attribute value that meets or exceeds the
     specified value are selected.

 Exact Only EGLConfigs whose attribute value equals the specified value are
     matched.

 Mask Only EGLConfigs for which the bits set in the attribute value include all
     the bits that are set in the specified value are selected (additional bits might
     be set in the attribute value).

 Special As described for the specific attribute.

     Some of the attributes must match the specified value exactly; others, such as
EGL RED SIZE, must meet or exceed the specified minimum values.
     To retrieve an EGLConfig given its unique integer ID, use the
EGL CONFIG ID attribute. When EGL CONFIG ID is specified, all other attributes
are ignored, and only the EGLConfig with the given ID is returned.
    If           EGL MAX PBUFFER WIDTH,                EGL MAX PBUFFER HEIGHT,
EGL MAX PBUFFER PIXELS, or EGL NATIVE VISUAL ID are specified in
attrib list, then they are ignored (however, if present, these attributes must still be

                          Version 1.3 - December 4, 2006
3.4. CONFIGURATION MANAGEMENT                                                                      21


followed by an attribute value in attrib list). If EGL SURFACE TYPE is specified
in attrib list and the mask that follows does not have EGL WINDOW BIT set, or if
there are no native visual types, then the EGL NATIVE VISUAL TYPE attribute is
ignored.
    If EGL TRANSPARENT TYPE is set to EGL NONE in attrib list, then
the EGL TRANSPARENT RED VALUE, EGL TRANSPARENT GREEN VALUE, and
EGL TRANSPARENT BLUE VALUE attributes are ignored.
    If EGL MATCH NATIVE PIXMAP is specified in attrib list, it must be fol-
lowed by an attribute value which is the handle of a valid native pixmap. Only
EGLConfigs which support rendering to that pixmap will match this attribute2 .
    If no EGLConfig matching the attribute list exists, then the call succeeds, but
num config is set to 0.

Sorting of EGLConfigs

     If more than one matching EGLConfig is found, then a list of EGLConfigs
is returned. The list is sorted by proceeding in ascending order of the ”Sort Pri-
ority” column of table 3.4. That is, configurations that are not ordered by a lower
numbered rule are sorted by the next higher numbered rule.
     Sorting for each rule is either numerically Smaller or Larger as described in the
”Sort Order” column, or a Special sort order as described for each sort rule below:

   1. Special: by EGL CONFIG CAVEAT where the precedence is EGL NONE,
      EGL SLOW CONFIG, EGL NON CONFORMANT CONFIG.

   2. Special:
      by EGL COLOR BUFFER TYPE where the precedence is EGL RGB BUFFER,
      EGL LUMINANCE BUFFER.

   3. Special: by larger total number of color bits (for an RGB color buffer,
      this is the sum of EGL RED SIZE, EGL GREEN SIZE, EGL BLUE SIZE,
      and EGL ALPHA SIZE; for a luminance color buffer, the sum of
      EGL LUMINANCE SIZE and EGL ALPHA SIZE) 3 . If the requested number
      of bits in attrib list for a particular color component is 0 or EGL DONT CARE,
      then the number of bits for that component is not considered.
   2
       The special match criteria for EGL MATCH NATIVE PIXMAP was introduced due to the
difficulty of determining an EGLConfig equivalent to a native pixmap using only color component
depths.
    3
      This rule places configs with deeper color buffers first in the list returned by eglChooseConfig.
Applications may find this counterintuitive, and need to perform additional processing on the list of
configs to find one best matching their requirements. For example, specifying RGBA depths of 5651
could return a list whose first config has a depth of 8888.


                               Version 1.3 - December 4, 2006
22                             CHAPTER 3. EGL FUNCTIONS AND ERRORS




              Attribute                       Default         Selection       Sort     Sort
                                                               Criteria       Order   Priority

            EGL BUFFER SIZE                      0             AtLeast    Smaller        4
               EGL RED SIZE                      0             AtLeast    Special        3
             EGL GREEN SIZE                      0             AtLeast    Special        3
              EGL BLUE SIZE                      0             AtLeast    Special        3
         EGL LUMINANCE SIZE                      0             AtLeast    Special        3
             EGL ALPHA SIZE                      0             AtLeast    Special        3
        EGL ALPHA MASK SIZE                      0             AtLeast    Smaller        9
     EGL BIND TO TEXTURE RGB              EGL DONT CARE         Exact      None
    EGL BIND TO TEXTURE RGBA              EGL DONT CARE         Exact      None
      EGL COLOR BUFFER TYPE              EGL RGB BUFFER         Exact      None          2
          EGL CONFIG CAVEAT               EGL DONT CARE         Exact     Special        1
              EGL CONFIG ID               EGL DONT CARE         Exact     Smaller     11 (last)
            EGL CONFORMANT                       0              Mask       None
             EGL DEPTH SIZE                      0             AtLeast    Smaller        7
                EGL LEVEL                        0              Exact      None
    EGL MATCH NATIVE PIXMAP                 EGL NONE           Special     None
      EGL MAX SWAP INTERVAL              EGL DONT CARE          Exact      None
      EGL MIN SWAP INTERVAL              EGL DONT CARE          Exact      None
      EGL NATIVE RENDERABLE              EGL DONT CARE          Exact      None
     EGL NATIVE VISUAL TYPE              EGL DONT CARE          Exact     Special        10
        EGL RENDERABLE TYPE            EGL OPENGL ES BIT        Mask       None
         EGL SAMPLE BUFFERS                      0             AtLeast    Smaller        5
               EGL SAMPLES                       0             AtLeast    Smaller        6
           EGL STENCIL SIZE                      0             AtLeast    Smaller        8
           EGL SURFACE TYPE              EGL WINDOW BIT         Mask       None
       EGL TRANSPARENT TYPE                 EGL NONE            Exact      None
   EGL TRANSPARENT RED VALUE              EGL DONT CARE         Exact      None
 EGL TRANSPARENT GREEN VALUE              EGL DONT CARE         Exact      None
  EGL TRANSPARENT BLUE VALUE              EGL DONT CARE         Exact      None

     Table 3.4: Default values and match criteria for EGLConfig attributes.




                          Version 1.3 - December 4, 2006
3.4. CONFIGURATION MANAGEMENT                                                   23


   4. Smaller EGL BUFFER SIZE.

   5. Smaller EGL SAMPLE BUFFERS.

   6. Smaller EGL SAMPLES.

   7. Smaller EGL DEPTH SIZE.

   8. Smaller EGL STENCIL SIZE.

   9. Smaller EGL ALPHA MASK SIZE.

 10. Special: by EGL NATIVE VISUAL TYPE (the actual sort order is
     implementation-defined, depending on the meaning of native visual types).

 11. Smaller EGL CONFIG ID (this is always the last sorting rule, and guarantees
     a unique ordering).

   EGLConfigs        are     not   sorted   with   respect   to   the   parameters
EGL   BIND TO TEXTURE RGB, EGL BIND TO TEXTURE RGBA, EGL CONFORMANT,
EGL   LEVEL,     EGL NATIVE RENDERABLE,       EGL MAX SWAP INTERVAL,
EGL   MIN SWAP INTERVAL,    EGL RENDERABLE TYPE,   EGL SURFACE TYPE,
EGL   TRANSPARENT TYPE,                  EGL TRANSPARENT RED VALUE,
EGL   TRANSPARENT GREEN VALUE, and EGL TRANSPARENT BLUE VALUE.


3.4.2    Lifetime of Configurations
Configuration handles (EGLConfigs) returned by eglGetConfigs and egl-
ChooseConfig remain valid so long as the EGLDisplay from which the handles
were obtained is not terminated. Implementations supporting a large number of dif-
ferent configurations, where it might be burdensome to instantiate data structures
for each configuration so queried (but never used), may choose to return handles
encoding sufficient information to instantiate the corresponding configurations dy-
namically, when needed to create EGL resources or query configuration attributes.

3.4.3    Querying Configuration Attributes
To get the value of an EGLConfig attribute, use

        EGLBoolean eglGetConfigAttrib(EGLDisplay dpy,
           EGLConfig config, EGLint attribute, EGLint
          *value);

                           Version 1.3 - December 4, 2006
24                              CHAPTER 3. EGL FUNCTIONS AND ERRORS


If eglGetConfigAttrib succeeds then it returns EGL TRUE and the value for the
specified attribute is returned in value. Otherwise it returns EGL FALSE. If attribute
is not a valid attribute then EGL BAD ATTRIBUTE is generated.
    Refer to Table 3.1 and Table 3.4 for a list of valid EGL attributes.


3.5     Rendering Surfaces
3.5.1    Creating On-Screen Rendering Surfaces
To create an on-screen rendering surface, first create a native platform window
with attributes corresponding to the desired EGLConfig (e.g. with the same color
depth, with other constraints specific to the platform). Using the platform-specific
type EGLNativeWindowType, which is the type of a handle to that native win-
dow, then call:

        EGLSurface eglCreateWindowSurface(EGLDisplay dpy,
          EGLConfig config, EGLNativeWindowType win,
          const EGLint *attrib list);

eglCreateWindowSurface creates an onscreen EGLSurface and returns a han-
dle to it. Any EGL context created with a compatible EGLConfig can be used to
render into this surface.
     attrib list specifies a list of attributes for the window. The list has the
same structure as described for eglChooseConfig. Attributes that can be
specified in attrib list include EGL RENDER BUFFER, EGL VG COLORSPACE, and
EGL VG ALPHA FORMAT.
     It is possible that some platforms will define additional attributes specific to
those environments, as an EGL extension.
     attrib list may be NULL or empty (first attribute is EGL NONE), in which case
all attributes assumes their default value as described below.
     EGL RENDER BUFFER specifies which buffer should be used for client API
rendering to the window, as described in section 2.2.2.              If its value is
EGL SINGLE BUFFER, then client APIs should render directly into the visible win-
dow. If its value is EGL BACK BUFFER, then all client APIs should render into the
back buffer. The default value of EGL RENDER BUFFER is EGL BACK BUFFER.
     Client APIs may not be able to respect the requested rendering buffer. To
determine the actual buffer being rendered to by a context, call eglQueryContext
(see section 3.7.4).
     EGL VG COLORSPACE specifies the color space used by OpenVG when ren-
dering                                       to                                   the

                          Version 1.3 - December 4, 2006
3.5. RENDERING SURFACES                                                          25


surface. If its value is EGL VG COLORSPACE sRGB, then a non-linear, perceptu-
ally uniform color space is assumed, with a corresponding VGImageFormat of
form VG s*. If its value is EGL VG COLORSPACE LINEAR, then a linear color space
is assumed, with a corresponding VGImageFormat of form VG l*. The default
value of EGL VG COLORSPACE is EGL VG COLORSPACE sRGB.
     EGL VG ALPHA FORMAT specifies how alpha values are interpreted by OpenVG
when rendering to the surface. If its value is EGL VG ALPHA FORMAT NONPRE,
then alpha values are not premultipled. If its value is EGL VG ALPHA FORMAT PRE,
then alpha values are premultiplied. The default value of EGL VG ALPHA FORMAT
is EGL VG ALPHA FORMAT NONPRE.
     Note that the EGL VG COLORSPACE and EGL VG ALPHA FORMAT attributes are
used only by OpenVG . EGL itself, and other client APIs such as OpenGL ES , do
not distinguish multiple colorspace models. Refer to section 11.2 of the OpenVG
1.0 specification for more information.
     On failure eglCreateWindowSurface returns EGL NO SURFACE. If the at-
tributes of win do not correspond to config, then an EGL BAD MATCH error is gen-
erated. If config does not support rendering to windows (the EGL SURFACE TYPE
attribute does not contain EGL WINDOW BIT), an EGL BAD MATCH error is gener-
ated. If config does not support the colorspace or alpha format attributes speci-
fied in attrib list (as defined for eglCreateWindowSurface), an EGL BAD MATCH
error is generated. If config is not a valid EGLConfig, an EGL BAD CONFIG
error is generated. If win is not a valid native window handle, then an
EGL BAD NATIVE WINDOW error should be generated. If there is already an
EGLConfig associated with win (as a result of a previous eglCreateWindow-
Surface call), then an EGL BAD ALLOC error is generated. Finally, if the imple-
mentation cannot allocate resources for the new EGL window, an EGL BAD ALLOC
error is generated.

3.5.2   Creating Off-Screen Rendering Surfaces
EGL supports off-screen rendering surfaces in pbuffers. Pbuffers differ from win-
dows in the following ways:

   1. Pbuffers are typically allocated in offscreen (non-visible) graphics memory
      and are intended only for accelerated offscreen rendering. Allocation can fail
      if there are insufficient graphics resources (implementations are not required
      to virtualize framebuffer memory). Clients should deallocate pbuffers when
      they are no longer in use, since graphics memory is often a scarce resource.
   2. Pbuffers are EGL resources and have no associated native window or na-
      tive window type. It may not be possible to render to pbuffers using native

                         Version 1.3 - December 4, 2006
26                               CHAPTER 3. EGL FUNCTIONS AND ERRORS


       rendering APIs.

     To create a pbuffer, call

       EGLSurface eglCreatePbufferSurface(EGLDisplay dpy,
         EGLConfig config, const EGLint
         *attrib list);

This creates a single pbuffer surface and returns a handle to it.
     attrib list specifies a list of attributes for the pbuffer. The list has the same
structure as described for eglChooseConfig.              Attributes that can be spec-
ified in attrib list include EGL WIDTH, EGL HEIGHT, EGL LARGEST PBUFFER,
EGL TEXTURE FORMAT,              EGL TEXTURE TARGET,           EGL MIPMAP TEXTURE,
EGL VG COLORSPACE, and EGL VG ALPHA FORMAT.
     It is possible that some platforms will define additional attributes specific to
those environments, as an EGL extension.
     attrib list may be NULL or empty (first attribute is EGL NONE), in which case
all the attributes assume their default values as described below.
     EGL WIDTH and EGL HEIGHT specify the pixel width and height of the rectan-
gular pbuffer. If the value of EGLConfig attribute EGL TEXTURE FORMAT is not
EGL NO TEXTURE, then the pbuffer width and height specify the size of the level
zero texture image. The default values for EGL WIDTH and EGL HEIGHT are zero.
     EGL TEXTURE FORMAT specifies the format of the OpenGL ES texture that
will be created when a pbuffer is bound to a texture map. It can be set to
EGL TEXTURE RGB, EGL TEXTURE RGBA, or EGL NO TEXTURE. The default value
of EGL TEXTURE FORMAT is EGL NO TEXTURE.
     EGL TEXTURE TARGET specifies the target for the OpenGL ES tex-
ture that will be created when the pbuffer is created with a texture
format of EGL TEXTURE RGB or EGL TEXTURE RGBA. The target can
be set to EGL NO TEXTURE or EGL TEXTURE 2D. The default value of
EGL TEXTURE TARGET is EGL NO TEXTURE.
     EGL MIPMAP TEXTURE indicates whether storage for OpenGL ES mipmaps
should be allocated. Space for mipmaps will be set aside if the attribute value is
EGL TRUE and EGL TEXTURE FORMAT is not EGL NO TEXTURE. The default value
for EGL MIPMAP TEXTURE is EGL FALSE.
     Use EGL LARGEST PBUFFER to get the largest available pbuffer when the al-
location of the pbuffer would otherwise fail. The width and height of the al-
located pbuffer will never exceed the values of EGL WIDTH and EGL HEIGHT,
respectively. If the pbuffer will be used as a OpenGL ES texture (i.e.,
the value of EGL TEXTURE TARGET is EGL TEXTURE 2D, and the value of

                           Version 1.3 - December 4, 2006
3.5. RENDERING SURFACES                                                          27


EGL TEXTURE FORMAT is EGL TEXTURE RGB or EGL TEXTURE RGBA), then the
aspect ratio will be preserved and the new width and height will be valid sizes
for the texture target (e.g. if the underlying OpenGL ES implementation does not
support non-power-of-two textures, both the width and height will be a power of
2). Use eglQuerySurface to retrieve the dimensions of the allocated pbuffer. The
default value of EGL LARGEST PBUFFER is EGL FALSE.
    EGL VG COLORSPACE and EGL VG ALPHA FORMAT have the same meaning
and default values as when used with eglCreateWindowSurface.
    The resulting pbuffer will contain color buffers and ancillary buffers as speci-
fied by config.
    The contents of the depth and stencil buffers may not be preserved when ren-
dering an OpenGL ES texture to the pbuffer and switching which image of the
texture is rendered to (e.g., switching from rendering one mipmap level to render-
ing another).
    On failure eglCreatePbufferSurface returns EGL NO SURFACE. If the pbuffer
could not be created due to insufficient resources, then an EGL BAD ALLOC error
is generated. If config is not a valid EGLConfig, an EGL BAD CONFIG error is
generated. If the value specified for either EGL WIDTH or EGL HEIGHT is less
than zero, an EGL BAD PARAMETER error is generated. If config does not support
pbuffers, an EGL BAD MATCH error is generated. In addition, an EGL BAD MATCH
error is generated if any of the following conditions are true:


   • The EGL TEXTURE FORMAT attribute is not EGL NO TEXTURE, and
     EGL WIDTH and/or EGL HEIGHT specify an invalid size (e.g., the texture size
     is not a power of two, and the underlying OpenGL ES implementation does
     not support non-power-of-two textures).


   • The    EGL TEXTURE FORMAT attribute is EGL NO TEXTURE, and
      EGL TEXTURE TARGET is something other than EGL NO TEXTURE; or,
      EGL TEXTURE FORMAT is something other than EGL NO TEXTURE, and
      EGL TEXTURE TARGET is EGL NO TEXTURE.


   Finally,  an EGL BAD ATTRIBUTE error is generated if any of the
EGL TEXTURE FORMAT, EGL TEXTURE TARGET, or EGL MIPMAP TEXTURE at-
tributes are specified, but config does not support OpenGL ES rendering
(e.g. the EGL RENDERABLE TYPE attribute does not include at least one of
EGL OPENGL ES BIT or EGL OPENGL ES2 BIT.


                         Version 1.3 - December 4, 2006
28                              CHAPTER 3. EGL FUNCTIONS AND ERRORS


3.5.3    Binding Off-Screen Rendering Surfaces To Client Buffers
Pbuffers may also be created by binding renderable buffers created in client APIs to
EGL. Currently, the only client API resources which may be bound in this fashion
are OpenVG VGImage objects.
    To bind a client API renderable buffer to a pbuffer, call
        EGLSurface eglCreatePbufferFromClient-
          Buffer(EGLDisplay dpy, EGLenum buftype,
          EGLClientBuffer buffer, EGLConfig config,
          const EGLint *attrib list);
This creates a single pbuffer surface bound to the specified buffer for part or all of
its buffer storage, and returns a handle to it. The width and height of the pbuffer
are determined by the width and height of buffer.
     buftype specifies the type of buffer to be bound. The only allowed value of
buftype is EGL OPENVG IMAGE.
     buffer is a client API reference to the buffer to be bound. When buftype is
EGL OPENVG IMAGE, buffer must be a valid VGImage handle, cast into the type
EGLClientBuffer.
     attrib list specifies a list of attributes for the pbuffer. The list has the
same structure as described for eglChooseConfig. Attributes that can be
specified in attrib list include EGL TEXTURE FORMAT, EGL TEXTURE TARGET,
and EGL MIPMAP TEXTURE. The meaning of these attributes is as de-
scribed above for eglCreatePbufferSurface.              The EGL VG COLORSPACE
and EGL VG ALPHA FORMAT attributes of the surface are determined by the
VGImageFormat of buffer.
     attrib list may be NULL or empty (first attribute is EGL NONE), in which case
all the attributes assume their default values as described above for eglCreateP-
bufferSurface.
     The resulting pbuffer will contain color and ancillary buffers as specified by
config. Buffers which are present in buffer (normally, just the color buffer) will be
bound to EGL. Buffers which are not present in buffer (such as depth and stencil,
if config includes those buffers) will be allocated by EGL in the same fashion as
for a surface created with eglCreatePbufferSurface
     On failure eglCreatePbufferFromClientBuffer returns EGL NO SURFACE. In
addition to the errors described above for eglCreatePbufferSurface, eglCreateP-
bufferFromClientBuffer may fail and generate errors for the following reasons:
     • If buftype is not a recognized client API resource type, or if buffer is not
       a valid handle or name of a client API resource of the specified type, an
       EGL BAD PARAMETER error is generated.


                          Version 1.3 - December 4, 2006
3.5. RENDERING SURFACES                                                           29


   • If the buffers contained in buffer do not correspond to a proper subset
     of the buffers described by config, and match the bit depths for those
     buffers specified in config, then an EGL BAD MATCH error is generated. For
     example, a VGImage with pixel format VG lRGBA 8888 corresponds to
     an EGLConfig with EGL RED SIZE, EGL GREEN SIZE, EGL BLUE SIZE,
     and EGL ALPHA SIZE values of 8.
   • There may be additional constraints on which types of buffers may be bound
     to EGL surfaces, as described in client API specifications. If those con-
     straints are violated, then an EGL BAD MATCH error is generated.
   • If buffer is already bound to another pbuffer, or is in use by a client API as
     discussed below, an EGL BAD ACCESS error is generated.

Lifetime and Usage of Bound Buffers
Binding client API buffers to EGL pbuffers create the possibility of race conditions,
and of buffers being deleted through one API while still in use in another API. To
avoid these problems, a number of constraints apply to bound client API buffers:
   • Bound buffers may be used exclusively by either EGL, or the client API that
     originally created them.
      For example, if a VGImage is bound to a pbuffer, and that pbuffer is bound
      to any client API rendering context, then the VGImage may not be used as
      the explicit source or destination of any OpenVG operation. Errors resulting
      from such use are described in client API specifications.
      Similarly, while a VGImage is in use by OpenVG , the pbuffer it is bound
      to may not be made current to any client API context, as described in sec-
      tion 3.7.3.
   • Binding a buffer creates an additional reference to it, and implementations
     must respect outstanding references when destroying objects.
      For example, if a VGImage is bound to a pbuffer, destroying the image with
      vgDestroyImage will not free the underlying buffer, because it is still in
      use by EGL. However, following vgDestroyImage the buffer may only be
      referred to via the EGL pbuffer handle, since the OpenVG handle to that
      buffer no longer exists.
      Similarly, destroying the pbuffer with eglDestroySurface will not free the
      underlying buffer, because it is still in use by OpenVG . However, follow-
      ing eglDestroySurface the buffer may only be referred to via the OpenVG
      VGImage handle, since the EGL pbuffer handle no longer exists.

                          Version 1.3 - December 4, 2006
30                              CHAPTER 3. EGL FUNCTIONS AND ERRORS


3.5.4    Creating Native Pixmap Rendering Surfaces
EGL also supports rendering surfaces whose color buffers are stored in native
pixmaps. Pixmaps differ from windows in that they are typically allocated in off-
screen (non-visible) graphics or CPU memory. Pixmaps differ from pbuffers in
that they do have an associated native pixmap and native pixmap type, and it may
be possible to render to pixmaps using APIs other than client APIs .
    To create a pixmap rendering surface, first create a native platform pixmap,
then select an EGLConfig matching the pixel format of that pixmap (calling
eglChooseConfig with an attribute list including EGL MATCH NATIVE PIXMAP re-
turns only EGLConfigs matching the pixmap specified in the attribute list - see
section 3.4.1).
    Using the platform-specific type EGLNativePixmapType, which is the
type of a handle to that native pixmap, then call:

        EGLSurface eglCreatePixmapSurface(EGLDisplay dpy,
          EGLConfig config, EGLNativePixmapType
          pixmap, const EGLint *attrib list);

eglCreatePixmapSurface creates an offscreen EGLSurface and returns a han-
dle to it. Any EGL context created with a compatible EGLConfig can be used to
render into this surface.
     attrib list specifies a list of attributes for the pixmap. The list has the same
structure as described for eglChooseConfig. Attributes that can be specified in
attrib list include EGL VG COLORSPACE and EGL VG ALPHA FORMAT.
     It is possible that some platforms will define additional attributes specific to
those environments, as an EGL extension.
     attrib list may be NULL or empty (first attribute is EGL NONE), in which case
all attributes assumes their default value.
     EGL VG COLORSPACE and EGL VG ALPHA FORMAT have the same meaning
and default values as when used with eglCreateWindowSurface.
     The resulting pixmap surface will contain color and ancillary buffers as speci-
fied by config. Buffers which are present in pixmap (normally, just the color buffer)
will be bound to EGL. Buffers which are not present in pixmap (such as depth and
stencil, if config includes those buffers) will be allocated by EGL in the same fash-
ion as for a surface created with eglCreatePbufferSurface.
     On failure eglCreatePixmapSurface returns EGL NO SURFACE. If the at-
tributes of pixmap do not correspond to config, then an EGL BAD MATCH
error is generated.          If config does not support rendering to pixmaps
(the EGL SURFACE TYPE attribute does not contain EGL PIXMAP BIT), an

                          Version 1.3 - December 4, 2006
3.5. RENDERING SURFACES                                                            31


EGL BAD MATCH error is generated. If config does not support the colorspace or al-
pha format attributes specified in attrib list (as defined for eglCreateWindowSur-
face), an EGL BAD MATCH error is generated. If config is not a valid EGLConfig,
an EGL BAD CONFIG error is generated. If pixmap is not a valid native pixmap
handle, then an EGL BAD NATIVE PIXMAP error should be generated. If there
is already an EGLSurface associated with pixmap (as a result of a previous
eglCreatePixmapSurface call), then a EGL BAD ALLOC error is generated. Fi-
nally, if the implementation cannot allocate resources for the new EGL pixmap, an
EGL BAD ALLOC error is generated.


3.5.5    Destroying Rendering Surfaces
An EGLSurface of any type (window, pbuffer, or pixmap) is destroyed by calling

        EGLBoolean eglDestroySurface(EGLDisplay dpy,
           EGLSurface surface);

All resources associated with surface which were allocated by EGL are marked for
deletion as soon as possible. If surface is current to any thread (see section 3.7.3),
resources are not actually released while the surface remains current. Future ref-
erences to surface remain valid only so long as it is current; it will be destroyed,
and all future references to it will become invalid, as soon as any otherwise valid
eglMakeCurrent call is made from the thread it is bound to.
     Resources associated with surface but not allocated by EGL, such as native
windows, native pixmaps, or client API buffers, are not affected when the surface
is destroyed. Only storage actually allocated by EGL is marked for deletion.
     Furthermore, resources associated with a pbuffer surface are not released until
all color buffers of that pbuffer bound to a OpenGL ES texture object have been
released.
     eglDestroySurface returns EGL FALSE on failure. An EGL BAD SURFACE er-
ror is generated if surface is not a valid rendering surface.


3.5.6    Surface Attributes
To set an attribute for an EGLSurface, call

        EGLBoolean eglSurfaceAttrib(EGLDisplay dpy,
           EGLSurface surface, EGLint attribute,
           EGLint value);

                          Version 1.3 - December 4, 2006
32                            CHAPTER 3. EGL FUNCTIONS AND ERRORS


             Attribute                Type                    Description
       EGL VG ALPHA FORMAT            enum            Alpha format for OpenVG
        EGL VG COLORSPACE             enum            Color space for OpenVG
          EGL CONFIG ID              integer             ID of EGLConfig
                                                       surface was created with
         EGL HEIGHT                 integer                Height of surface
 EGL HORIZONTAL RESOLUTION          integer              Horizontal dot pitch
    EGL LARGEST PBUFFER             boolean    If true, create largest pbuffer possible
     EGL MIPMAP TEXTURE             boolean          True if texture has mipmaps
      EGL MIPMAP LEVEL              integer           Mipmap level to render to
   EGL PIXEL ASPECT RATIO           integer              Display aspect ratio
     EGL RENDER BUFFER               enum                    Render buffer
     EGL SWAP BEHAVIOR               enum               Buffer swap behavior
     EGL TEXTURE FORMAT              enum              Format of texture: RGB,
                                                         RGBA, or no texture
        EGL TEXTURE TARGET            enum        Type of texture: 2D or no texture
     EGL VERTICAL RESOLUTION         integer               Vertical dot pitch
             EGL WIDTH               integer               Width of surface

               Table 3.5: Queryable surface attributes and types.



    The specified attribute of surface is set to value. Currently only the
EGL MIPMAP LEVEL attribute can be set.
    For OpenGL ES mipmap textures, the EGL MIPMAP LEVEL attribute indicates
which level of the mipmap should be rendered. If the value of this attribute is
outside the range of supported mipmap levels, the closest valid mipmap level is
selected for rendering. The default value of this attribute is 0.
    If the value of pbuffer attribute EGL TEXTURE FORMAT is EGL NO TEXTURE, if
the value of attribute EGL TEXTURE TARGET is EGL NO TEXTURE, or if surface is
not a pbuffer, then attribute EGL MIPMAP LEVEL may be set, but has no effect.
    If OpenGL ES rendering is not supported by surface, then trying to set
EGL MIPMAP LEVEL will cause an EGL BAD PARAMETER error.
    To query an attribute associated with an EGLSurface call:


       EGLBoolean eglQuerySurface(EGLDisplay dpy,
         EGLSurface surface, EGLint attribute,
         EGLint *value);

                         Version 1.3 - December 4, 2006
3.5. RENDERING SURFACES                                                          33


eglQuerySurface returns in value the value of attribute for surface. attribute must
be set to one of the attributes in table 3.5.
     Querying EGL CONFIG ID returns the ID of the EGLConfig with respect to
which the surface was created.
     Querying EGL LARGEST PBUFFER for a pbuffer surface returns the same at-
tribute value specified when the surface was created with eglCreatePbufferSur-
face. For a window or pixmap surface, the contents of value are not modified.
     Querying EGL WIDTH and EGL HEIGHT returns respectively the width and
height, in pixels, of the surface. For a window or pixmap surface, these values are
initially equal to the width and height of the native window or pixmap with respect
to which the surface was created. If a native window is resized, the corresponding
window surface will eventually be resized by the implementation to match (as dis-
cussed in section 3.9.1). If there is a discrepancy because EGL has not yet resized
the window surface, the size returned by eglQuerySurface will always be that of
the EGL surface, not the corresponding native window.
     For a pbuffer, they will be the actual allocated size of the pbuffer (which may
be less than the requested size if EGL LARGEST PBUFFER is EGL TRUE).
     Querying EGL HORIZONTAL RESOLUTION and EGL VERTICAL RESOLUTION
returns respectively the horizontal and vertical dot pitch of the display on which a
window surface is visible. The values returned are equal to the actual dot pitch, in
pixels/meter, multiplied by the constant value EGL DISPLAY SCALING (10000).
     Querying EGL PIXEL ASPECT RATIO returns the ratio of pixel width to pixel
height, multiplied by EGL DISPLAY SCALING. For almost all displays, the re-
turned value will be EGL DISPLAY SCALING, indicating an aspect ratio of one
(square pixels).
     For an offscreen (pbuffer or pixmap) surface, or a surface whose pixel dot
pitch or aspect ratio are unknown, querying EGL HORIZONTAL RESOLUTION,
EGL VERTICAL RESOLUTION, and EGL PIXEL ASPECT RATIO will return the
constant value EGL UNKNOWN (-1).
     Querying EGL RENDER BUFFER returns the buffer which client API render-
ing is requested to use. For a window surface, this is the same attribute value
specified when the surface was created. For a pbuffer surface, it is always
EGL BACK BUFFER. For a pixmap surface, it is always EGL SINGLE BUFFER. To
determine the actual buffer being rendered to by a context, call eglQueryContext
(see section 3.7.4).
     Querying EGL SWAP BEHAVIOR describes the effect on the color buffer
when posting a surface with eglSwapBuffers (see section 3.9). A value of
EGL BUFFER PRESERVED indicates that color buffer contents are unaffected, while
a value of EGL BUFFER DESTROYED indicates that color buffer contents may be
destroyed or changed by the operation.

                         Version 1.3 - December 4, 2006
34                              CHAPTER 3. EGL FUNCTIONS AND ERRORS


   Querying       EGL TEXTURE FORMAT,           EGL TEXTURE TARGET,
EGL MIPMAP TEXTURE, or EGL MIPMAP LEVEL for a non-pbuffer surface is not
an error, but value is not modified.
    eglQuerySurface returns EGL FALSE on failure and value is not updated. If
attribute is not a valid EGL surface attribute, then an EGL BAD ATTRIBUTE error
is generated. If surface is not a valid EGLSurface then an EGL BAD SURFACE
error is generated.


3.6     Rendering to Textures
This section describes how to render to an OpenGL ES texture using a pbuffer
surface configured for this operation. If a pbuffer surface does not support
OpenGL ES rendering, or if OpenGL ES is not implemented on a platform,
then calling eglBindTexImage or eglReleaseTexImage will always generate
EGL BAD SURFACE errors.


3.6.1    Binding a Surface to a OpenGL ES Texture
The command

        EGLBoolean eglBindTexImage(EGLDisplay dpy,
          EGLSurface surface, EGLint buffer);

defines a two-dimensional texture image. The texture image consists of the image
data in buffer for the specified surface, and need not be copied. Currently the only
value accepted for buffer is EGL BACK BUFFER, which indicates the buffer into
which OpenGL ES rendering is taking place (this is true even when using a single-
buffered surface, such as a pixmap). In future versions of EGL, additional buffer
values may be allowed to bind textures to other buffers in an EGLSurface.
     The texture target, the texture format and the size of the texture components
are derived from attributes of the specified surface, which must be a pbuffer sup-
porting one of the EGL BIND TO TEXTURE RGB or EGL BIND TO TEXTURE RGBA
attributes.
     Note that any existing images associated with the different mipmap levels of
the texture object are freed (it is as if glTexImage was called with an image of zero
width).
     The pbuffer attribute EGL TEXTURE FORMAT determines the base internal for-
mat of the texture. The component sizes are also determined by pbuffer attributes
as shown in table 3.6:

                          Version 1.3 - December 4, 2006
3.6. RENDERING TO TEXTURES                                                        35


                     Texture Component              Size
                              R               EGL RED SIZE
                              G             EGL GREEN SIZE
                              B              EGL BLUE SIZE
                              A             EGL ALPHA SIZE

                      Table 3.6: Size of texture components



    The texture target is derived from the EGL TEXTURE TARGET attribute of sur-
face. If the attribute value is EGL TEXTURE 2D, then buffer defines a texture for
the two-dimensional texture object which is bound to the current context (hereafter
referred to as the current texture object).
    If dpy and surface are the display and surface for the calling thread’s cur-
rent context, eglBindTexImage performs an implicit glFlush. For other surfaces,
eglBindTexImage waits for all effects from previously issued client API com-
mands drawing to the surface to complete before defining the texture image, as
though glFinish were called on the last context to which that surface were bound.
    After eglBindTexImage is called, the specified surface is no longer available
for reading or writing. Any read operation, such as glReadPixels or eglCopy-
Buffers, which reads values from any of the surface’s color buffers or ancillary
buffers will produce indeterminate results. In addition, draw operations that are
done to the surface before its color buffer is released from the texture produce in-
determinate results. Specifically, if the surface is current to a context and thread
then rendering commands will be processed and the context state will be updated,
but the surface may or may not be written. eglSwapBuffers has no effect if it is
called on a bound surface.
    Client APIs other than OpenGL ES may be used to render into a surface later
bound as a texture. The effects of binding a surface as an OpenGL ES texture when
the surface is current to a client API context other than OpenGL ES are generally
similar those described above, but there may be additional restrictions. Applica-
tions using mixed-mode render-to-texture in this fashion should unbind surfaces
from all client API contexts before binding those surfaces as OpenGL ES textures.
    Note that the color buffer is bound to a texture object. If the texture object is
shared between contexts, then the color buffer is also shared. If a texture object is
deleted before eglReleaseTexImage is called, then the color buffer is released and
the surface is made available for reading and writing.
    Texture mipmap levels are automatically generated when all of the following
conditions are met while calling eglBindTexImage:

                          Version 1.3 - December 4, 2006
36                               CHAPTER 3. EGL FUNCTIONS AND ERRORS


     • The EGL MIPMAP TEXTURE attribute of the pbuffer being bound is
       EGL TRUE.

     • The OpenGL ES texture parameter GL GENERATE MIPMAP is GL TRUE for
       the currently bound texture.
     • The value of the EGL MIPMAP LEVEL attribute of the pbuffer being bound is
       equal to the value of the texture parameter GL TEXTURE BASE LEVEL.

    In this case, additional mipmap levels are generated as described in section 3.8
of the OpenGL ES 1.1 Specification.
    It is not an error to call glTexImage2D or glCopyTexImage2D to replace an
image of a texture object that has a color buffer bound to it. However, these calls
will cause the color buffer to be released back to the surface and new memory will
be allocated for the texture. Note that the color buffer is released even if the image
that is being defined is a mipmap level that was not defined by the color buffer.
    If eglBindTexImage is called and the surface attribute EGL TEXTURE FORMAT
is set to EGL NO TEXTURE, then an EGL BAD MATCH error is returned. If buffer is
already bound to a texture then an EGL BAD ACCESS error is returned. If buffer is
not a valid buffer, then an EGL BAD PARAMETER error is generated. If surface is
not a valid EGLSurface, or is not a pbuffer surface supporting texture binding,
then an EGL BAD SURFACE error is generated.
    eglBindTexImage is ignored if there is no current rendering context.

3.6.2    Releasing a Surface from an OpenGL ES Texture
To release a color buffer that is being used as a texture, call

        EGLBoolean eglReleaseTexImage(EGLDisplay dpy,
          EGLSurface surface, EGLint buffer);

The specified color buffer is released back to the surface. The surface is made
available for reading and writing when it no longer has any color buffers bound as
textures.
    The contents of the color buffer are undefined when it is first released. In par-
ticular, there is no guarantee that the texture image is still present. However, the
contents of other color buffers are unaffected by this call. Also, the contents of the
depth and stencil buffers are not affected by eglBindTexImage and eglRelease-
TexImage.
    If the specified color buffer is no longer bound to a texture (e.g., because the
texture object was deleted) then eglReleaseTexImage has no effect. No error is
generated.

                          Version 1.3 - December 4, 2006
3.7. RENDERING CONTEXTS                                                                         37


     After a color buffer is released from a texture (either explicitly by calling
eglReleaseTexImage or implicitly by calling a routine such as glTexImage2D),
all texture images that were defined by the color buffer become NULL (it is as if
glTexImage was called with an image of zero width).
     If eglReleaseTexImage is called and the value of surface attribute
EGL TEXTURE FORMAT is EGL NO TEXTURE, then an EGL BAD MATCH error is re-
turned. If buffer is not a valid buffer (currently only EGL BACK BUFFER may be
specified), then an EGL BAD PARAMETER error is generated. If surface is not a
valid EGLSurface, or is not a bound pbuffer surface, then an EGL BAD SURFACE
error is returned.


3.6.3    Implementation Caveats

Developers should note that conformant OpenGL ES implementations are not re-
quired to support render to texture; that is, there may be no EGLConfigs support-
ing the EGL BIND TO TEXTURE RGB or EGL BIND TO TEXTURE RGBA attributes.
Render to texture is functionally subsumed by the newer framebuffer object exten-
sion to OpenGL ES , and may eventually be deprecated.



3.7     Rendering Contexts
EGL provides functions to create and destroy rendering contexts for each supported
client API ; to query information about rendering contexts; and to bind rendering
contexts to surfaces, making them current.
     At most one context for each supported client API may be current to a particular
thread at a given time, and at most one context may be bound to a particular surface
at a given time. 4 The minimum number of current contexts that must be supported
by an EGL implementation is one for each supported client API . 5
     Only one OpenGL ES context may be current to a particular thread, even if the
implementation supports both OpenGL ES 1.x and OpenGL ES 2.x in the same
runtime 6 .
   4
     Note that this implies that implementations must allow (for example) both an OpenGL ES and an
OpenVG context to be current to the same thread, so long as they are drawing to different surfaces.
   5
     This constraint allows valid implementations which are restricted to supporting only one active
rendering thread in a thread group.
   6
     This restriction is necessary because many entry points are shared by both versions of OpenGL
ES . Determining which library version of OpenGL ES to call into is based on properties of the
current OpenGL ES context.


                              Version 1.3 - December 4, 2006
38                                  CHAPTER 3. EGL FUNCTIONS AND ERRORS


    Some of the functions described in this section make use of the current render-
ing API, which is set on a per-thread basis 7 by calling

           EGLBoolean eglBindAPI(EGLenum api);

api must specify one of the supported client APIs , either EGL OPENVG API or
EGL OPENGL ES API.
    eglBindAPI returns EGL FALSE on failure. If api is not one of the values
specified above, or if the client API specified by api is not supported by the imple-
mentation, an EGL BAD PARAMETER error is generated.
    To obtain the value of the current rendering API, call

           EGLenum eglQueryAPI();

         The value returned will be one of the valid api parameters to eglBindAPI, or
EGL NONE.
    The initial value of the current rendering API is EGL OPENGL ES API, unless
OpenGL ES is not supported by an implementation, in which case the initial value
is EGL NONE. Applications using multiple client APIs are responsible for ensur-
ing the current rendering API is correct before calling the functions eglCreate-
Context, eglGetCurrentContext, eglGetCurrentDisplay, eglGetCurrentSur-
face, eglMakeCurrent (when its ctx parameter is EGL NO CONTEXT), eglWait-
Client, or eglWaitNative.

3.7.1        Creating Rendering Contexts
To create a rendering context for the current rendering API, call

           EGLContext eglCreateContext(EGLDisplay dpy,
             EGLConfig config, EGLContext share context,
             const EGLint *attrib list);

    If eglCreateContext succeeds, it initializes the context to the initial state de-
fined for the current rendering API, and returns a handle to it. The context can be
used to render to any compatible EGLSurface.
    Although contexts are specific to a single client API , all contexts created in
EGL exist in a single namespace. This allows many EGL calls which manage
contexts to avoid use of the current rendering API.
     7
    Note that the current rendering API is set on a per-thread basis, but not on a per-EGLDisplay
basis. This is because current contexts are bound in the same manner.


                             Version 1.3 - December 4, 2006
3.7. RENDERING CONTEXTS                                                            39


     If share context is not EGL NO CONTEXT, then all shareable data, as defined by
the client API (note that for OpenGL ES , shareable data excludes texture objects
named 0) will be shared by share context, all other contexts share context already
shares with, and the newly created context. An arbitrary number of EGLContexts
can share data in this fashion. The OpenGL ES server context state for all shar-
ing contexts must exist in a single address space or an EGL BAD MATCH error is
generated.
     attrib list specifies a list of attributes for the context. The list has the same
structure as described for eglChooseConfig. The only attribute that can be speci-
fied in attrib list is EGL CONTEXT CLIENT VERSION, and this attribute may only
be specified when creating a OpenGL ES context (e.g. when the current rendering
API is EGL OPENGL ES API).
     attrib list may be NULL or empty (first attribute is EGL NONE), in which case
attributes assume their default values as described below.
     EGL CONTEXT CLIENT VERSION determines which version of an OpenGL ES
context to create. An attribute value of 1 specifies creation of an OpenGL ES 1.x
context. An attribute value of 2 specifies creation of an OpenGL ES 2.x context.
The default value for EGL CONTEXT CLIENT VERSION is 1.
     On failure eglCreateContext returns EGL NO CONTEXT. If the current render-
ing api is EGL NONE, then an EGL BAD MATCH error is generated (this situation can
only arise in an implementation which does not support OpenGL ES , and prior to
the first call to eglBindAPI). If share context is neither zero nor a valid context of
the same client API type as the newly created context, then an EGL BAD CONTEXT
error is generated.
     If config is not a valid EGLConfig, or does not support the requested client
API , then an EGL BAD CONFIG error is generated (this includes requesting creation
of an OpenGL ES 1.x context when the EGL RENDERABLE TYPE attribute of config
does not contain EGL OPENGL ES BIT, or creation of an OpenGL ES 2.x context
when the attribute does not contain EGL OPENGL ES2 BIT).
     If the OpenGL ES server context state for share context exists in an address
space that cannot be shared with the newly created context, if share context was
created on a different display than the one referenced by config, or if the contexts
are otherwise incompatible (for example, one context being associated with a hard-
ware device driver and the other with a software renderer), then an EGL BAD MATCH
error is generated. If the server does not have enough resources to allocate the new
context, then an EGL BAD ALLOC error is generated.

3.7.2   Destroying Rendering Contexts
A rendering context is destroyed by calling

                          Version 1.3 - December 4, 2006
40                                CHAPTER 3. EGL FUNCTIONS AND ERRORS


        EGLBoolean eglDestroyContext(EGLDisplay dpy,
          EGLContext ctx);

All resources associated with ctx are marked for deletion as soon as possible. If ctx
is current to any thread (see section 3.7.3), resources are not actually released while
the context remains current. Future references to ctx remain valid only so long as
it is current; it will be destroyed, and all future references to it will become invalid,
as soon as any otherwise valid eglMakeCurrent call is made from the thread it is
bound to).
     eglDestroyContext returns EGL FALSE on failure. An EGL BAD CONTEXT er-
ror is generated if ctx is not a valid context.

3.7.3    Binding Contexts and Drawables
To make a context current, call

        EGLBoolean eglMakeCurrent(EGLDisplay dpy,
          EGLSurface draw, EGLSurface read,
          EGLContext ctx);

eglMakeCurrent binds ctx to the current rendering thread and to the draw and
read surfaces.
     For an OpenGL ES context, draw is used for all OpenGL ES operations except
for any pixel data read back, which is taken from the frame buffer values of read.
Note that the same EGLSurface may be specified for both draw and read.
     For an OpenVG context, the same EGLSurface must be specified for both
draw and read.
     If the calling thread already has a current context of the same client API type as
ctx, then that context is flushed and marked as no longer current. ctx is then made
the current context for the calling thread.
     eglMakeCurrent returns EGL FALSE on failure. Errors generated may in-
clude:

     • If draw or read are not compatible with ctx, then an EGL BAD MATCH error
       is generated.

     • If ctx is current to some other thread, or if either draw or read are bound to
       contexts in another thread, an EGL BAD ACCESS error is generated.

     • If either draw or read are pbuffers created with eglCreatePbufferFrom-
       ClientBuffer, and the underlying bound client API buffers are in use by the
       client API that created them, an EGL BAD ACCESS error is generated.

                           Version 1.3 - December 4, 2006
3.7. RENDERING CONTEXTS                                                           41


   • If ctx is not a valid context, an EGL BAD CONTEXT error is generated.

   • If either draw or read are not valid EGL surfaces, an EGL BAD SURFACE
     error is generated.

   • If a native window underlying either draw or read is no longer valid, an
     EGL BAD NATIVE WINDOW error is generated.

   • If draw and read cannot fit into graphics memory simultaneously, an
     EGL BAD MATCH error is generated.

   • If the previous context of the calling thread has unflushed commands, and the
     previous surface is no longer valid, an EGL BAD CURRENT SURFACE error is
     generated.

   • If the ancillary buffers for draw and read cannot be allocated, an
     EGL BAD ALLOC error is generated.

   • If a power management event has occurred, an EGL CONTEXT LOST error is
     generated.

    Other errors may arise when the context state is inconsistent with the surface
state, as described in the following paragraphs.
    If draw is destroyed after eglMakeCurrent is called, then subsequent render-
ing commands will be processed and the context state will be updated, but the sur-
face contents become undefined. If read is destroyed after eglMakeCurrent then
pixel values read from the framebuffer (e.g., as result of calling glReadPixels) are
undefined. If a native window or pixmap underlying the draw or read surfaces is
destroyed, rendering and readback are handled as above.
    To release the current context without assigning a new one, set ctx to
EGL NO CONTEXT and set draw and read to EGL NO SURFACE. The currently
bound context for the client API specified by the current rendering API is flushed
and marked as no longer current, and there will be no current context for that client
API after eglMakeCurrent returns. This is the only case in which eglMakeCur-
rent respects the current rendering API. In all other cases, the client API affected
is determined by ctx.
    If ctx is EGL NO CONTEXT and draw and read are not EGL NO SURFACE, or if
draw or read are set to EGL NO SURFACE and ctx is not EGL NO CONTEXT, then an
EGL BAD MATCH error will be generated.
    The first time an OpenGL ES context is made current the viewport and scissor
dimensions are set to the size of the draw surface (as though glViewport(0, 0, w,
h) and glScissor(0, 0, w, h) were called, where w and h are the width and height

                          Version 1.3 - December 4, 2006
42                              CHAPTER 3. EGL FUNCTIONS AND ERRORS


of the surface, respectively). However, the viewport and scissor dimensions are
not modified when ctx is subsequently made current. The client is responsible for
resetting the viewport and scissor in this case.
     Implementations may delay allocation of auxiliary buffers for a surface un-
til they are required by a context (which may result in the EGL BAD ALLOC error
described above). Once allocated, however, auxiliary buffers and their contents
persist until a surface is deleted.
     When rendering to a surface containing multisample buffers (created with re-
spect to an EGLConfig whose EGL SAMPLE BUFFERS attribute has a value of
one), multisample information may be lost when switching rendering between
client APIs . Some client APIs may interpret multisample information in differ-
ent fashions, and some may not perform multisample rendering, even when multi-
sample buffers are available. When multisample information is lost, lower quality
images may result. For this reason, applications mixing rendering by multiple
client APIs onto the same surface should minimize switching between client APIs
. Ideally, each client API rendering to a surface should be made current only once
for each frame being rendered.

3.7.4    Context Queries
Several queries exist to return information about contexts.
   To get the current context for the current rendering API, call

        EGLContext eglGetCurrentContext();

If there is no current context for the current rendering API, or if the current render-
ing API is EGL NONE, then EGL NO CONTEXT is returned (this is not an error).
     To get the surfaces used for rendering by a current context, call

        EGLSurface eglGetCurrentSurface(EGLint readdraw);

readdraw is either EGL READ or EGL DRAW, to return respectively the read or draw
surfaces bound to the current context in the calling thread, for the current rendering
API.
    If there is no current context for the current rendering API, then
EGL NO SURFACE is returned (this is not an error).                   If readdraw is
neither EGL READ nor EGL DRAW, EGL NO SURFACE is returned and an
EGL BAD PARAMETER error is generated.
    To get the display associated with a current context, call

        EGLDisplay eglGetCurrentDisplay(void);

                          Version 1.3 - December 4, 2006
3.7. RENDERING CONTEXTS                                                            43


The display for the current context in the calling thread, for the current render-
ing API, is returned. If there is no current context for the current rendering API,
EGL NO DISPLAY is returned (this is not an error).
    To obtain the value of context attributes, use

      EGLBoolean eglQueryContext(EGLDisplay dpy,
         EGLContext ctx, EGLint attribute, EGLint
         *value);

eglQueryContext        returns      in    value     the     value    of      attribute
for ctx. attribute must be set to EGL CONFIG ID, EGL CONTEXT CLIENT TYPE,
EGL CONTEXT CLIENT VERSION, or EGL RENDER BUFFER.
    Querying EGL CONFIG ID returns the ID of the EGLConfig with respect to
which the context was created.
    Querying EGL CONTEXT CLIENT TYPE returns the type of client API this con-
text supports (the value of the api parameter to eglBindAPI).
    Querying EGL CONTEXT CLIENT VERSION returns the version of the client
API this context supports, as specified at context creation time. The resulting value
is only meaningful for an OpenGL ES context.
    Querying EGL RENDER BUFFER returns the buffer which client API rendering
via this context will use. The value returned depends on properties of both the
context, and the surface to which the context is bound:

   • If the context is bound to a pixmap surface, then EGL SINGLE BUFFER will
     be returned.

   • If the context is bound to a pbuffer surface, then EGL BACK BUFFER will be
     returned.

   • If the context is bound to a window surface, then either EGL BACK BUFFER
     or EGL SINGLE BUFFER may be returned. The value returned depends on
     both the buffer requested by the setting of the EGL RENDER BUFFER property
     of the surface (which may be queried by calling eglQuerySurface - see
     section 3.5.6), and on the client API (not all client APIs support single-
     buffer rendering to window surfaces).

   • If the context is not bound to a surface, then EGL NONE will be returned.

    eglQueryContext returns EGL FALSE on failure and value is not updated. If
attribute is not a valid EGL context attribute, then an EGL BAD ATTRIBUTE error
is generated. If ctx is invalid, an EGL BAD CONTEXT error is generated.

                          Version 1.3 - December 4, 2006
44                              CHAPTER 3. EGL FUNCTIONS AND ERRORS


3.8    Synchronization Primitives
To prevent native rendering API functions from executing until any outstanding
client API rendering affecting the same surface is complete, call

      EGLBoolean eglWaitClient();

All rendering calls for the currently bound context, for the current rendering API,
made prior to eglWaitClient, are guaranteed to be executed before native render-
ing calls made after eglWaitClient which affect the surface associated with that
context.
    The same result can be achieved using client API -specific calls such as glFin-
ish or vgFinish.
    Clients rendering to single buffered surfaces (e.g. pixmap surfaces) should call
eglWaitClient before accessing the native pixmap from the client.
    eglWaitClient returns EGL TRUE on success. If there is no current context for
the current rendering API, the function has no effect but still returns EGL TRUE. If
the surface associated with the calling thread’s current context is no longer valid,
EGL FALSE is returned and an EGL BAD CURRENT SURFACE error is generated.
    For backwards compatibility, the function

      EGLBoolean eglWaitGL(void);

is equivalent to

          EGLenum api = eglQueryAPI();
          eglBindAPI(EGL OPENGL ES API);
          eglWaitClient();
          eglBindAPI(api);


    To prevent a client API command sequence from executing until any outstand-
ing native rendering affecting the same surface is complete, call

      EGLBoolean eglWaitNative(EGLint engine);

Native rendering calls made with the specified marking engine, and which affect
the surface associated with the calling thread’s current context, for the current ren-
dering API, are guaranteed to be executed before client API rendering calls made
after eglWaitNative. The same result may be (but is not necessarily) achievable
using native synchronization calls.

                          Version 1.3 - December 4, 2006
3.9. POSTING THE COLOR BUFFER                                                   45


    engine denotes a particular marking engine (another drawing API, such as GDI
or Xlib) to be waited on. Valid values of engine are defined by EGL extensions
specific to implementations, but implementations will always recognize the sym-
bolic constant EGL CORE NATIVE ENGINE, which denotes the most commonly
used marking engine other then a client API .
    eglWaitNative returns EGL TRUE on success. If there is no current context,
the function has no effect but still returns EGL TRUE. If the surface does not sup-
port native rendering (e.g. pbuffer and in most cases window surfaces), the func-
tion has no effect but still returns EGL TRUE. If the surface associated with the
calling thread’s current context is no longer valid, EGL FALSE is returned and an
EGL BAD CURRENT SURFACE error is generated. If engine does not denote a recog-
nized marking engine, EGL FALSE is returned and an EGL BAD PARAMETER error
is generated.


3.9     Posting the Color Buffer
After completing rendering, the contents of the color buffer can be made visible in
a native window, or copied to a native pixmap.

3.9.1    Posting to a Window
To post the color buffer to a window, call

        EGLBoolean eglSwapBuffers(EGLDisplay dpy,
           EGLSurface surface);

    If surface is a back-buffered window surface, then the color buffer is copied
to the native window associated with that surface. If surface is a single-buffered
window, pixmap, or pbuffer surface, eglSwapBuffers has no effect.
    The contents of the color buffer of surface may be affected by eglSwapBuffers,
depending on the value of the EGL SWAP BEHAVIOR attribute of surface (see sec-
tion 3.5.6).

Native Window Resizing
If the native window corresponding to surface has been resized prior to the swap,
surface must be resized to match. surface will normally be resized by the EGL
implementation at the time the native window is resized. If the implementation
cannot do this transparently to the client, then eglSwapBuffers must detect the
change and resize surface prior to copying its pixels to the native window.

                         Version 1.3 - December 4, 2006
46                             CHAPTER 3. EGL FUNCTIONS AND ERRORS


    If surface shrinks as a result of resizing, some rendered pixels are lost. If
surface grows, the newly allocated buffer contents are undefined. The resizing
behavior described here only maintains consistency of EGL surfaces and native
windows; clients are still responsible for detecting window size changes (using
platform-specific means) and changing their viewport and scissor regions accord-
ingly.

3.9.2    Copying to a Native Pixmap
To copy the color buffer to a native pixmap, call

        EGLBoolean eglCopyBuffers(EGLDisplay dpy,
          EGLSurface surface, EGLNativePixmapType
          target);

    The color buffer is copied to the specified target, which must be a valid native
pixmap handle.
    The mapping of pixels in the color buffer to pixels in the pixmap is platform-
dependent, since the native platform pixel coordinate system may differ from that
of OpenGL ES .
    The color buffer of surface is left unchanged after calling eglCopyBuffers.

3.9.3    Posting Semantics
surface must be bound to the calling thread’s current context, for the current ren-
dering API. This restriction may be lifted in future EGL revisions.
    If dpy and surface are the display and surface for the calling thread’s current
context, eglSwapBuffers and eglCopyBuffers perform an implicit flush operation
on the context (glFlush for an OpenGL ES context, vgFlush for an OpenVG con-
text). Subsequent client API commands can be issued immediately, but will not be
executed until posting is completed.
    The destination of a posting operation (a visible window, for eglSwapBuffers,
or a native pixmap, for eglCopyBuffers) should have the same number of compo-
nents and component sizes as the color buffer it’s being copied from.
    In the specific case of a luminance color buffer being posted to an RGB destina-
tion, the luminance component value will normally be replicated in each of the red,
green, and blue components of the destination. Some implementations may use al-
ternate color-space conversion algorithms to map luminance to red, green, and blue
values, so long as the perceptual result is unchanged. Such alternate conversions
should be documented by the implementation.

                         Version 1.3 - December 4, 2006
3.9. POSTING THE COLOR BUFFER                                                           47


    In other cases where this compatibility constraint is not met by the surface
and posting destination, implementations may choose to relax the constraint by
converting data to the destination format. If they do so, they should define an EGL
extension specifying which destination formats are supported, and specifying the
conversion arithmetic used.
    The function

        EGLBoolean eglSwapInterval(EGLDisplay dpy, EGLint
           interval);

    specifies the minimum number of video frame periods per buffer swap for
the window associated with the current context. The interval takes effect when
eglSwapBuffers is first called subsequent to the eglSwapInterval call. The swap
interval has no effect on eglCopyBuffers.
    The parameter interval specifies the minimum number of video frames that are
displayed before a buffer swap will occur. The interval specified by the function
applies to the draw surface bound to the context that is current on the calling thread.
    If interval is set to a value of 0, buffer swaps are not synchronized to a
video frame, and the swap happens as soon as all rendering commands out-
standing for the current context are complete. interval is silently clamped to
minimum and maximum implementation dependent values before being stored;
these values are defined by EGLConfig attributes EGL MIN SWAP INTERVAL and
EGL MAX SWAP INTERVAL respectively.
    The default swap interval is 1.


3.9.4    Posting Errors
eglSwapBuffers and eglCopyBuffers return EGL FALSE on failure. If surface is
not a valid EGL surface, an EGL BAD SURFACE error is generated. If surface is not
bound to the calling thread’s current context, an EGL BAD SURFACE error is gener-
ated. If target is not a valid native pixmap handle, an EGL BAD NATIVE PIXMAP
error should be generated. If the format of target is not compatible with the color
buffer, or if the size of target is not the same as the size of the color buffer, and there
is no defined conversion between the source and target formats, an EGL BAD MATCH
error is generated. If called after a power management event has occurred, a
EGL CONTEXT LOST error is generated. If eglSwapBuffers is called and the native
window associated with surface is no longer valid, an EGL BAD NATIVE WINDOW
error is generated. If eglCopyBuffers is called and the implementation does not
support native pixmaps, an EGL BAD NATIVE PIXMAP error is generated.

                           Version 1.3 - December 4, 2006
48                              CHAPTER 3. EGL FUNCTIONS AND ERRORS


    eglSwapInterval returns EGL FALSE on failure. If there is no current context
on the calling thread, a EGL BAD CONTEXT error is generated. If there is no surface
bound to the current context, a EGL BAD SURFACE error is generated.


3.10      Obtaining Extension Function Pointers
The client API and EGL extensions which are available to a client may vary at
runtime, depending on factors such as the rendering path being used (hardware
or software), resources available to the implementation, or updated device drivers.
Therefore, the address of extension functions may be queried at runtime. The
function

       void (*eglGetProcAddress(const char
         *procname))();

returns the address of the extension function named by procName. procName must
be a NULL-terminated string. The pointer returned should be cast to a function
pointer type matching the extension function’s definition in that extension specifi-
cation. A return value of NULL indicates that the specified function does not exist
for the implementation.
    A non-NULL return value for eglGetProcAddress does not guarantee that an
extension function is actually supported at runtime. The client must also make a
corresponding query, such as glGetString(GL EXTENSIONS) for OpenGL ES ex-
tensions; vgGetString(VG EXTENSIONS) for OpenVG extensions; or eglQueryS-
tring(dpy, EGL EXTENSIONS) for EGL extensions, to determine if an extension is
supported by a particular client API context.
    Function pointers returned by eglGetProcAddress are independent of the dis-
play and the currently bound context, and may be used by any context which sup-
ports the extension.
    eglGetProcAddress may be queried for all of the following functions:

     • All EGL and client API extension functions supported by the implementa-
       tion (whether those extensions are supported by the current context or not).
       This includes any mandatory OpenGL ES extensions.

    eglGetProcAddress may not be queried for core (non-extension) functions in
EGL or client APIs . For functions that are queryable with eglGetProcAddress,
implementations may choose to also export those functions statically from the ob-
ject libraries implementing those functions. However, portable clients cannot rely
on this behavior.

                          Version 1.3 - December 4, 2006
3.11. RELEASING THREAD STATE                                                      49


3.11     Releasing Thread State
EGL maintains a small amount of per-thread state, including the error sta-
tus returned by eglGetError, the currently bound rendering API defined by
eglBindAPI, and the current contexts for each supported client API . The overhead
of maintaining this state may be objectionable in applications which create and de-
stroy many threads, but only call EGL or client APIs in a few of those threads at
any given time.
    To return EGL to its state at thread initialization, call
       EGLBoolean eglReleaseThread(void);
EGL TRUE is returned on success, and the following actions are taken:

   • For each client API supported by EGL, if there is a currently bound context,
     that context is released. This is equivalent to calling eglMakeCurrent with
     ctx set to EGL NO CONTEXT and both draw and read set to EGL NO SURFACE
     (see section 3.7.3).
   • The current rendering API is reset to its value at thread initialization (see
     section 3.7).
   • Any additional implementation-dependent per-thread state maintained by
     EGL is marked for deletion as soon as possible.
    eglReleaseThread may be called in any thread at any time, and may be called
more than once in a single thread. The initialization status of EGL (see section 3.2)
is not affected by releasing the thread; only per-thread state is affected.
    Resources explicitly allocated by calls to EGL, such as contexts, surfaces, and
configuration lists, are not affected by eglReleaseThread. Such resources belong
not to the thread, but to the EGL implementation as a whole.
    Applications may call other EGL routines from a thread following eglRe-
leaseThread, but any such call may reallocate the EGL state previously released.
In particular, calling eglGetError immediately following a successful call to
eglReleaseThread should not be done. Such a call will return EGL SUCCESS -
but will also result in reallocating per-thread state.
    eglReleaseThread returns EGL FALSE on failure. There are no defined con-
ditions under which failure will occur. Even if EGL is not initialized on any
EGLDisplay, eglReleaseThread should succeed. However, platform-dependent
failures may be signaled through the value returned from eglGetError. Unless the
platform-dependent behavior is known, a failed call to eglReleaseThread should
be assumed to leave the current rendering API, and the currently bound contexts
for each supported client API , in an unknown state.

                          Version 1.3 - December 4, 2006
Chapter 4

Extending EGL

EGL implementors may extend EGL by adding new commands or additional enu-
merated values for existing EGL commands.
     New names for EGL functions and enumerated types must clearly indicate
whether some particular feature is in the core EGL or is vendor specific. To make
a vendor-specific name, append a company identifier (in upper case) and any ad-
ditional vendor-specific tags (e.g. machine names). For instance, SGI might add
new commands and manifest constants of the form eglNewCommandSGI and
EGL NEW DEFINITION SGI. If two or more vendors agree in good faith to im-
plement the same extension, and to make the specification of that extension pub-
licly available, the procedures and tokens that are defined by the extension can be
suffixed by EXT. Extensions approved by supra-vendor organizations use similar
identifiers, such as KHR for extensions approved by the Khronos Group).
     It is critically important for interoperability that enumerants and entry point
names be unique across vendors. The Khronos API Registrar maintains a registry
of enumerants, and all shipping enumerant values must be determined by request-
ing blocks of enumerants from the registry. See

                        http://www.opengl.org/registry/

   for more information on defining extensions.




                                        50
Chapter 5

EGL Versions, Header Files, and
Enumerants

Each version of EGL supports specified client API versions, and all prior versions
of those APIs up to that version. For OpenGL ES , such support includes both
Common and Common-Lite profiles. EGL 1.0 supports OpenGL ES 1.0, EGL 1.1
supports OpenGL ES 1.1, and EGL 1.2 supports OpenGL ES 2.0 and OpenVG 1.0.
    Whether a particular client API is actually available at runtime may depend
on additional factors. In most cases, EGL and each client API are provided in
separate libraries, and applications must link to the EGL library and to each of the
client APIs used by the application. However, details of this procedure vary, and
developers must refer to platform-specific documentation.


5.1     Header Files
The EGL specification defines an ISO C language binding. This binding may
also be used from C++ code. In these environments, the EGL header file
<EGL/egl.h> provides prototypes for all the EGL entry points, and C prepro-
cessor symbols for all the EGL tokens. C and C++ source code should #include
<EGL/egl.h> before using any EGL entry points or symbols. 1
    Languages other than C and C++ will define the EGL interfaces using other
methods, not described in this specification.
    The Khronos Implementer’s Guidelines describe recommended practice, out-
line platform-specific issues, and provide other recommendations to people writing
EGL implementations. For more details refer to the developer area at:
   1
   For backwards compatibility, implementations supporting OpenGL ES 1.x must also support the
EGL header on the path <GLES/egl.h>.


                                             51
52         CHAPTER 5. EGL VERSIONS, HEADER FILES, AND ENUMER . . .


                               http://www.khronos.org/


5.2      Compile-Time Version Detection
To allow code to be written portably against future EGL versions, the compile-time
environment must make it possible to determine which EGL version interfaces
are available. The details of such detection are language-specific and should be
specified in the language binding documents for each language. For C and C++
code, the <EGL/egl.h> header defines C preprocessor symbols corresponding
to all versions of EGL supported by the implementation:

         #define    EGL   VERSION      1   0   1
         #define    EGL   VERSION      1   1   1
         #define    EGL   VERSION      1   2   1
         #define    EGL   VERSION      1   3   1

   Future versions of EGL will define additional preprocessor symbols corre-
sponding to the major and minor numbers of those versions.


5.3      Enumerant Values and Header Portability
Enumerant values for EGL tokens are required to be common across all implemen-
tations. A reference version of the egl.h header file, including defined values for
all EGL enumerants, accompanies this specification and can be downloaded from

                               http://www.khronos.org/

    All platform-specific types, values, and macros used in egl.h are partitioned
into a platform header, eglplatform.h, which is automatically included by
egl.h. A copy of eglplatform.h providing definitions suitable for many
platforms is included along with egl.h. Implementers should need to modify
only eglplatform.h, never egl.h. 2




     2
     Please submit any additions to eglplatform.h made to support new platforms for inclusion
in the reference copy.


                            Version 1.3 - December 4, 2006
Chapter 6

Glossary

Address Space the set of objects or memory locations accessible through a single
     name space. In other words, it is a data region that one or more threads may
     share through pointers.

Client an application, which communicates with the underlying EGL implemen-
      tation and underlying native window system by some path. The application
      program is referred to as a client of the window system server. To the server,
      the client is the communication path itself. A program with multiple connec-
      tions is viewed as multiple clients to the server. The resource lifetimes are
      controlled by the connection lifetimes, not the application program lifetimes.

Client API one of the rendering APIs supported by EGL. At present client APIs
      include only OpenGL ES and OpenVG , but other clients are expected to be
      added in future versions of EGL. Context creation / management, rendering
      semantics, and interaction between client APIs are all well-defined by EGL.
      There is (considerably more limited) support for rendering to EGL surfaces
      by non-client (native) rendering APIs, and the semantics of such support are
      more implementation-dependent.

Compatible an OpenGL ES rendering context is compatible with (may be used to
    render into) a surface if they meet the constraints specified in section 2.2.

Connection a bidirectional byte stream that carries the X (and EGL) protocol be-
    tween the client and the server. A client typically has only one connection to
    a server.

(Rendering) Context an OpenGL ES rendering context. This is a virtual OpenGL
     ES machine. All OpenGL ES rendering is done with respect to a context.

                                        53
54                                                     CHAPTER 6. GLOSSARY


      The state maintained by one rendering context is not affected by another
      except in case of state that may be explicitly shared at context creation time,
      such as textures.

Current Context an implicit context used by OpenGL ES and OpenVG , rather
     than passing a context parameter to each API entry point. The current
     OpenGL ES and OpenVG contexts are set as defined in section 3.7.3.

EGLContext a handle to a rendering context. OpenGL ES rendering contexts
    consist of client side state and server side state. Other client APIs do not
    distinguish between the two types of state.

(Drawing) Surface an onscreen or offscreen buffer where pixel values resulting
     from rendering through OpenGL ES or other APIs are written.

Thread one of a group of execution units all sharing the same address space. Typ-
     ically, each thread will have its own program counter and stack pointer, but
     the text and data spaces are visible to each of the threads. A thread that is
     the only member of its group is equivalent to a process.




                         Version 1.3 - December 4, 2006
Appendix A

Version 1.0

EGL version 1.0, approved on July 23, 2003, is the original version of EGL. EGL
was loosely based on GLX 1.3, generalized to be implementable on many differ-
ent operating systems and window systems and simplified to reflect the needs of
embedded devices running OpenGL ES .


A.1     Acknowledgements
EGL 1.0 is the result of the contributions of many people, representing a cross
section of the desktop, hand-held, and embedded computer industry. Following
is a partial list of contributors, including the company that they represented at the
time of their contribution:
     Aaftab Munshi, ATI
     Andy Methley, Panasonic
     Carl Korobkin, 3d4W
     Chris Hall, Seaweed Systems
     Claude Knaus, Silicon Graphics
     David Blythe, 3d4W
     Ed Plowman, ARM
     Graham Connor, Imagination Technologies
     Harri Holopainen, Hybrid Graphics
     Jacob Str¨om, Ericsson
     Jani Vaarala, Nokia
     Jon Leech, Silicon Graphics
     Justin Couch, Yumetech
     Kari Pulli, Nokia
     Lane Roberts, Symbian

                                         55
56                                               APPENDIX A. VERSION 1.0


     Mark Callow, HI
     Mark Tarlton, Motorola
     Mike Olivarez, Motorola
     Neil Trevett, 3Dlabs
     Phil Huxley, Tao Group
     Tom Olson, Texas Instruments
     Ville Miettinen, Hybrid Graphics




                         Version 1.3 - December 4, 2006
Appendix B

Version 1.1

EGL version 1.1, approved on August 5, 2004, is the second release of EGL. It
adds power management and swap control functionality based on vendor exten-
sions from Imagination Technologies, and optional render-to-texture functional-
ity based on the WGL ARB render texture extension defined by the OpenGL
ARB for desktop OpenGL.


B.1     Revision 1.1.2
EGL version 1.1.2 (revision 2 of EGL 1.1), approved on November 10, 2004, clar-
ified that vertex buffer objects are shared among contexts in the same fashion as
texture objects.


B.2     Acknowledgements
EGL 1.1 is the result of the contributions of many people, representing a cross
section of the desktop, hand-held, and embedded computer industry. Following
is a partial list of contributors, including the company that they represented at the
time of their contribution:
     Aaftab Munshi, ATI
     Andy Methley, Panasonic
     Axel Mamode, Sony
     Barthold Lichtenbelt, 3Dlabs
     Benji Bowman, Imagination Technologies
     Borgar Ljosland, Falanx
     Brian Murray, Motorola
     Bryce Johnstone, Texas Instruments

                                         57
58                                              APPENDIX B. VERSION 1.1


     Carlos Sarria, Imagination Technologies
     Chris Tremblay, Motorola
     Claude Knaus, Esmertec
     Clay Montgomery, Nokia
     Dan Petersen, Sun
     Dan Rice, Sun
     David Blythe, HI
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
     Remi Arnaud, Sony
     Robert Simpson, Bitboys
     Tero Sarkkinen, Futuremark
     Timo Suoranta, Futuremark
     Thomas Tannert, Silicon Graphics
     Tomi Aarnio, Nokia
     Tom McReynolds, Nvidia
     Tom Olson, Texas Instruments
     Ville Miettinen, Hybrid Graphics

                        Version 1.3 - December 4, 2006
Appendix C

Version 1.2

EGL version 1.2, approved on July 8, 2005, is the third release of EGL. It adds
support for the OpenVG 2D client API , in addition to support for OpenGL ES ,
and generalizes EGL concepts to enable supporting other client APIs in the future.


C.1     Acknowledgements
EGL 1.2 is the result of the contributions of many people, representing a cross
section of the desktop, hand-held, and embedded computer industry. Following
is a partial list of contributors, including the company that they represented at the
time of their contribution:
     Aaftab Munshi, ATI
     Anu Ramanathan, TI
     Daniel Rice, Sun Microsystems
     Espen Aamodt, Falanx
     Jani Vaarala, Nokia
     Jon Leech, SGI
     Jussi R¨as¨anen, Hybrid Graphics
     Koichi Mori, Nokia
     Mark Callow, HI Corporation
     Members of the Khronos OpenGL ES Working Group
     Members of the Khronos OpenVG Working Group
     Michael.Nonweiler, ARM
     Neil Trevett, 3Dlabs / NVIDIA
     Petri Kero, Hybrid Graphics
     Robert Simpson, Bitboys
     Simon Fenney, PowerVR

                                         59
60                                           APPENDIX C. VERSION 1.2


     Tom Olson, TI




                     Version 1.3 - December 4, 2006
Appendix D

Version 1.3

EGL version 1.3 was voted out of the OpenKODE Working Group on De-
cember 4, 2006, and formally approval by the Khronos Board of Pro-
moters on February 8, 2007.           EGL 1.3 is the fourth release of EGL.
It adds support for separate OpenGL ES 1.x and 2.x contexts with
the EGL CONTEXT CLIENT VERSION attribute to eglCreateContext and the
EGL OPENGL ES2 BIT in the EGL RENDERABLE TYPE attribute, and adds the
EGL MATCH NATIVE PIXMAP pseudo-attribute to eglChooseConfig, to allow se-
lecting configs matching specific native pixmaps. The EGL CONFORMANT at-
tribute was added to indicate if client API contexts will pass the required con-
formance tests, and the EGL SURFACE TYPE attribute was extended with the
EGL VG COLORSPACE LINEAR BIT and EGL VG ALPHA FORMAT PRE BIT bit-
fields to define whether or not linear colorspace and premultiplied alpha format
are supported by the OpenVG implementation. For naming consistency, some to-
kens from EGL 1.2 have been renamed as shown in table D.1. The old names
are also retained for backwards compatibility. The specification adds a number of
clarifications (but not behavior changes) regarding config sorting, surface resource
ownership, multiple client API context versions, and SDK issues.
     Finally, the eglplatform.h header is defined to accompany the reference
egl.h header provided by Khronos.


D.1     Acknowledgements
EGL 1.3 is the result of the contributions of many people, representing a cross
section of the desktop, hand-held, and embedded computer industry. Following is
a list of contributors, including the company that they represented at the time of
their contribution:

                                        61
62                                             APPENDIX D. VERSION 1.3


           EGL 1.2 Token Name              EGL 1.3 Token Name
             EGL COLORSPACE               EGL VG COLORSPACE
         EGL COLORSPACE LINEAR        EGL VG COLORSPACE LINEAR
          EGL COLORSPACE sRGB          EGL VG COLORSPACE sRGB
            EGL ALPHA FORMAT             EGL VG ALPHA FORMAT
          EGL ALPHA FORMAT PRE         EGL VG ALPHA FORMAT PRE
        EGL ALPHA FORMAT NONPRE      EGL VG ALPHA FORMAT NONPRE
          NativeDisplayType            EGLNativeDisplayType
          NativePixmapType             EGLNativePixmapType
          NativeWindowType             EGLNativeWindowType

                        Table D.1: Renamed tokens



     Aaftab Munshi, ATI
     Daniel Rice, Sun Microsystems
     Espen Aamodt, Falanx
     Gary King, NVIDIA
     Jani Vaarala, Nokia
     Jasin Bushnaief, Hybrid Graphics
     Jay Abbott, TAO
     Jon Kennedy, 3Dlabs
     Jon Leech
     Jussi R¨as¨anen, Hybrid Graphics
     Kalle Raita, Hybrid Graphics
     Kari Pulli, Nokia
     Koichi Mori, Nokia
     Leonardo Estevez, TI
     Mark Callow, HI Corporation
     Members of the Khronos OpenGL ES Working Group
     Members of the Khronos OpenKODE Working Group
     Members of the Khronos OpenVG Working Group
     Neil Trevett, NVIDIA
     Petri Kero, Hybrid Graphics
     Remi Arnaud, Sony Computer Entertainment
     Robert J. Simpson, Bitboys
     Robert Palmer, Symbian
     Sampo Lappalainen, Hybrid Graphics
     Simon Fenney, Imagination Technologies

                       Version 1.3 - December 4, 2006
D.1. ACKNOWLEDGEMENTS                                 63


  Sven Gothel, ATI
  Teemu Rantalaiho, Hybrid Graphics
  Tom Olson, TI




                     Version 1.3 - December 4, 2006
Index of EGL Commands

EGL   * SIZE, 16                               EGL   BUFFER DESTROYED, 33
EGL   ALPHA FORMAT, 62                         EGL   BUFFER PRESERVED, 33
EGL   ALPHA FORMAT NONPRE, 62                  EGL   BUFFER SIZE, 14, 15, 21, 22
EGL   ALPHA FORMAT PRE, 62                     EGL   CLIENT APIS, 12
EGL   ALPHA MASK SIZE, 14, 15, 22,             EGL   COLOR BUFFER TYPE, 14, 15,
          23                                            21, 22
EGL   ALPHA SIZE, 14, 15, 21, 22, 29,          EGL   COLORSPACE, 62
          35                                   EGL   COLORSPACE LINEAR, 62
EGL   BACK BUFFER, 24, 33, 34, 37,             EGL   COLORSPACE sRGB, 62
          43                                   EGL   CONFIG CAVEAT, 14, 17, 21, 22
EGL   BAD ACCESS, 9, 29, 36, 40                EGL   CONFIG ID, 13, 14, 20, 22, 23,
EGL   BAD ALLOC, 9, 25, 27, 31, 39,                     32, 43
          41                                   EGL   CONFORMANT, 14, 17, 18, 22,
EGL   BAD ATTRIBUTE, 10, 20, 23, 27,                    23, 61
          34, 43                               EGL   CONTEXT CLIENT TYPE, 43
EGL   BAD CONFIG, 10, 25, 27, 30, 39           EGL   CONTEXT CLIENT VERSION,
EGL   BAD CONTEXT, 10, 39, 40, 43,                      39, 43, 61
          47                                   EGL   CONTEXT LOST, 8, 10, 41, 47
EGL   BAD CURRENT SURFACE, 10,                 EGL   CORE NATIVE ENGINE, 44
          41, 44, 45                           EGL   DEPTH SIZE, 14, 15, 22, 23
EGL   BAD DISPLAY, 10–12                       EGL   DISPLAY SCALING, 33
EGL   BAD MATCH, 10, 25, 27–30, 36–            EGL   DONT CARE, 20–22
          41, 47                               EGL   DRAW, 42
EGL   BAD NATIVE PIXMAP, 10, 11,               EGL   EXTENSIONS, 12, 13, 48
          31, 47                               EGL   FALSE, 2, 8, 9, 11, 19, 20, 23, 26,
EGL   BAD NATIVE WINDOW, 10, 11,                        27, 31, 34, 38, 40, 43–45, 47,
          25, 41, 47                                    49
EGL   BAD PARAMETER, 10, 13, 19,               EGL   GREEN SIZE, 14, 15, 21, 22, 29,
          27, 28, 32, 36–38, 42, 45                     35
EGL   BAD SURFACE, 10, 31, 34, 36,             EGL   HEIGHT, 26, 27, 32, 33
          37, 40, 47                           EGL   HORIZONTAL RESOLUTION,
EGL   BIND TO TEXTURE RGB, 14,                          32, 33
          19, 22, 23, 34, 37                   EGL   LARGEST PBUFFER, 26, 27, 32,
EGL   BIND TO TEXTURE RGBA, 14,                         33
          19, 22, 23, 34, 37                   EGL   LEVEL, 14, 20, 22, 23
EGL   BLUE SIZE, 14, 15, 21, 22, 29, 35        EGL   LUMINANCE BUFFER, 15, 21


                                          64
INDEX                                                                       65


EGL LUMINANCE SIZE, 14, 15, 21,                  35
       22                                 EGL RENDER BUFFER, 24, 32, 33, 43
EGL MATCH NATIVE PIXMAP, 21,              EGL RENDERABLE TYPE, 14, 15,
       22, 30, 61                                17, 18, 22, 23, 27, 39, 61
EGL MAX PBUFFER HEIGHT, 14,               EGL RGB BUFFER, 15, 21, 22
       18, 20                             EGL SAMPLE BUFFERS, 14, 16, 22,
EGL MAX PBUFFER PIXELS, 14, 18,                  23, 42
       20                                 EGL SAMPLES, 14, 16, 22, 23
EGL MAX PBUFFER WIDTH, 14, 18,            EGL SINGLE BUFFER, 24, 33, 43
       20                                 EGL SLOW CONFIG, 17, 21
EGL MAX SWAP INTERVAL, 14, 18,            EGL STENCIL SIZE, 14, 15, 22, 23
       22, 23, 47                         EGL SUCCESS, 9, 10, 49
EGL MIN SWAP INTERVAL, 14, 18,            EGL SURFACE TYPE, 14, 16, 19, 20,
       22, 23, 47                                22, 23, 25, 30, 61
EGL MIPMAP LEVEL, 31–33, 36               EGL SWAP BEHAVIOR, 32, 33, 45
EGL MIPMAP TEXTURE, 26–28, 32,            EGL TEXTURE 2D, 26, 34
       33, 35                             EGL TEXTURE FORMAT, 26–28, 32–
EGL NATIVE RENDERABLE, 14, 17,                   34, 36, 37
       22, 23                             EGL TEXTURE RGB, 26
EGL NATIVE VISUAL ID, 14, 17, 20          EGL TEXTURE RGBA, 26
EGL NATIVE VISUAL TYPE, 14, 17,           EGL TEXTURE TARGET, 26–28, 32–
       21–23                                     34
EGL NEW DEFINITION SGI, 50                EGL TRANSPARENT BLUE VALUE,
EGL NO CONTEXT, 9, 38, 39, 41, 42,               14, 18, 21–23
       49                                 EGL TRANSPARENT GREEN VALUE,
EGL NO DISPLAY, 11, 42                           14, 18, 21–23
EGL NO SURFACE, 25, 27, 28, 30, 41,       EGL TRANSPARENT RED VALUE,
       42, 49                                    14, 18, 21–23
EGL NO TEXTURE, 26, 27, 32, 36, 37        EGL TRANSPARENT RGB, 18
EGL NON CONFORMANT CONFIG,                EGL TRANSPARENT TYPE, 14, 18,
       17, 21                                    21–23
EGL NONE, 17, 18, 20–22, 24, 26, 28,      EGL TRUE, 2, 9, 11, 12, 14, 19, 23, 26,
       30, 38, 39, 42, 43                        33, 35, 44, 45, 49
EGL NOT INITIALIZED, 9, 11–13, 19         EGL UNKNOWN, 33
EGL OPENGL ES2 BIT, 17, 27, 39, 61        EGL VENDOR, 12, 13
EGL OPENGL ES API, 38, 39, 44             EGL VERSION, 12, 13
EGL OPENGL ES BIT, 17, 22, 27, 39         EGL VERTICAL RESOLUTION, 32,
EGL OPENVG API, 38                               33
EGL OPENVG BIT, 17                        EGL VG ALPHA FORMAT, 17, 24–
EGL OPENVG IMAGE, 28                             28, 30, 32, 62
EGL PBUFFER BIT, 16, 19                   EGL VG ALPHA FORMAT NONPRE,
EGL PIXEL ASPECT RATIO, 32, 33                   25, 62
EGL PIXMAP BIT, 16, 30                    EGL VG ALPHA FORMAT PRE, 17,
EGL READ, 42                                     25, 62
EGL RED SIZE, 14, 15, 18, 20–22, 29,      EGL VG ALPHA FORMAT PRE BIT,


                        Version 1.3 - December 4, 2006
66                                                                          INDEX


           16, 61                            eglQuerySurface, 27, 32, 33, 43
EGL VG COLORSPACE, 16, 24–28,                eglReleaseTexImage, 34–37
           30, 32, 62                        eglReleaseThread, 10, 49
EGL VG COLORSPACE LINEAR, 16,                EGLSurface, 3, 4, 8, 10, 13, 24, 30–32,
           24, 62                                     34, 36–38, 40
EGL VG COLORSPACE LINEAR BIT,                eglSurfaceAttrib, 31
           16, 61                            eglSwapBuffers, 4, 5, 8, 18, 19, 33, 35,
EGL VG COLORSPACE sRGB, 24, 62                        45–47
EGL WIDTH, 26, 27, 32, 33                    eglSwapInterval, 18, 19, 46, 47
EGL WINDOW BIT, 16, 20, 22, 25               eglTerminate, 12
eglBindAPI, 38, 39, 43, 44, 48               eglWaitClient, 8, 38, 44
eglBindTexImage, 34–36                       eglWaitGL, 44
EGLBoolean, 2, 9, 17                         eglWaitNative, 8, 38, 44
eglChooseConfig, 13, 19, 21, 23, 24, 26,
           28, 30, 39, 61                    GL BLUE BITS, 15
EGLClientBuffer, 28                          GL EXTENSIONS, 48
EGLConfig, 3, 4, 10, 13–27, 29, 30, 32,      GL GENERATE MIPMAP, 35
           37, 39, 42, 43, 47                GL GREEN BITS, 15
EGLContext, 8, 10, 38                        GL RED BITS, 15
eglCopyBuffers, 5, 8, 35, 46, 47             GL TEXTURE 2D, 7
eglCreateContext, 38, 39, 61                 GL TEXTURE 3D, 7
eglCreatePbufferFromClientBuffer, 28,        GL TEXTURE BASE LEVEL, 36
           40                                GL TEXTURE CUBE MAP, 7
eglCreatePbufferSurface, 18, 26–28, 30,      GL TRUE, 35
           33                                glBindBuffer, 7
eglCreatePixmapSurface, 30, 31               glBindTexture, 7
eglCreateWindowSurface, 24, 25, 27, 30       glCopyTexImage2D, 36
eglDestroyContext, 8, 39, 40                 glFinish, 8, 35, 44
eglDestroySurface, 29, 31                    glFlush, 35, 46
EGLDisplay, 3, 4, 10–12, 23, 37, 49          glGetString, 48
eglGetConfigAttrib, 23                       glReadPixels, 35, 41
eglGetConfigs, 19, 23                        glScissor, 41
eglGetCurrentContext, 38, 42                 glTexImage, 34, 37
eglGetCurrentDisplay, 38, 42                 glTexImage2D, 36
eglGetCurrentSurface, 38, 42                 glViewport, 41
eglGetDisplay, 11
eglGetError, 9, 10, 48, 49                   VG EXTENSIONS, 48
eglGetProcAddress, 48                        VG l*, 24
eglInitialize, 11–13                         VG lRGBA 8888, 28
EGLint, 2                                    VG s*, 24
eglMakeCurrent, 8, 12, 31, 38, 40, 41, 49    vgDestroyImage, 29
eglNewCommandSGI, 50                         vgFinish, 8, 44
eglQueryAPI, 38, 44                          vgFlush, 46
eglQueryContext, 24, 33, 43                  vgGetString, 48
eglQueryString, 12, 48                       VGImage, 27–29


                           Version 1.3 - December 4, 2006
INDEX                                                    67


VGImageFormat, 24, 28




                        Version 1.3 - December 4, 2006
