OpenGL Graphics with the X Window System
         R                                                  R


              Version 1.3

  Document Editors version 1.3: Paula Womack, Jon Leech




             Version 1.3 - October 19, 1998
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




                              Version 1.3 - October 19, 1998
Contents
1 Overview                                                                                         1
2 GLX Operation                                                                                    2
  2.1   Rendering Contexts and Drawing Surfaces        .   .   .   .   .   .   .   .   .   .   .   2
  2.2   Using Rendering Contexts . . . . . . . . .     .   .   .   .   .   .   .   .   .   .   .   3
  2.3   Direct Rendering and Address Spaces . .        .   .   .   .   .   .   .   .   .   .   .   4
  2.4   OpenGL Display Lists . . . . . . . . . . .     .   .   .   .   .   .   .   .   .   .   .   5
  2.5   Texture Objects . . . . . . . . . . . . . .    .   .   .   .   .   .   .   .   .   .   .   6
  2.6   Aligning Multiple Drawables . . . . . . .      .   .   .   .   .   .   .   .   .   .   .   7
  2.7   Multiple Threads . . . . . . . . . . . . . .   .   .   .   .   .   .   .   .   .   .   .   7
3 Functions and Errors                                                                             9
  3.1 Errors . . . . . . . . . . . . . . . . . . . . . . . . . .               .   .   .   .   .    9
  3.2 Events . . . . . . . . . . . . . . . . . . . . . . . . . .               .   .   .   .   .   10
  3.3 Functions . . . . . . . . . . . . . . . . . . . . . . . .                .   .   .   .   .   10
      3.3.1 Initialization . . . . . . . . . . . . . . . . . .                 .   .   .   .   .   10
      3.3.2 GLX Versioning . . . . . . . . . . . . . . . .                     .   .   .   .   .   11
      3.3.3 Con guration Management . . . . . . . . . .                        .   .   .   .   .   12
      3.3.4 On Screen Rendering . . . . . . . . . . . . . .                    .   .   .   .   .   21
      3.3.5 O Screen Rendering . . . . . . . . . . . . . .                     .   .   .   .   .   21
      3.3.6 Querying Attributes . . . . . . . . . . . . . .                    .   .   .   .   .   25
      3.3.7 Rendering Contexts . . . . . . . . . . . . . .                     .   .   .   .   .   25
      3.3.8 Events . . . . . . . . . . . . . . . . . . . . . .                 .   .   .   .   .   31
      3.3.9 Synchronization Primitives . . . . . . . . . .                     .   .   .   .   .   33
      3.3.10 Double Bu ering . . . . . . . . . . . . . . . .                   .   .   .   .   .   33
      3.3.11 Access to X Fonts . . . . . . . . . . . . . . .                   .   .   .   .   .   34
  3.4 Backwards Compatibility . . . . . . . . . . . . . . .                    .   .   .   .   .   35
      3.4.1 Using Visuals for Con guration Management                          .   .   .   .   .   35
      3.4.2 O Screen Rendering . . . . . . . . . . . . . .                     .   .   .   .   .   39
                                      i



                              Version 1.3 - October 19, 1998
ii                                                                         CONTENTS

     3.5 Rendering Contexts . . . . . . . . . . . . . . . . . . . . . . . 40
4 Encoding on the X Byte Stream                                                                42
     4.1   Requests that hold a single extension request . .       .   .   .   .   .   .   .   42
     4.2   Request that holds multiple OpenGL commands             .   .   .   .   .   .   .   43
     4.3   Wire representations and byte swapping . . . . .        .   .   .   .   .   .   .   44
     4.4   Sequentiality . . . . . . . . . . . . . . . . . . . .   .   .   .   .   .   .   .   44
5 Extending OpenGL                                                                             47
6 GLX Versions                                                                                 49
     6.1 New Commands in GLX Version 1.1 . . . . . . . . . . . . . . 49
     6.2 New Commands in GLX Version 1.2 . . . . . . . . . . . . . . 49
     6.3 New Commands in GLX Version 1.3 . . . . . . . . . . . . . . 50
7 Glossary                                                                                     51
  Index of GLX Commands                                                                        53




                      Version 1.3 - October 19, 1998
List of Figures
 2.1 Direct and Indirect Rendering Block Diagram. . . . . . . . .     4
 4.1 GLX byte stream. . . . . . . . . . . . . . . . . . . . . . . . . 43




                                  iii



                           Version 1.3 - October 19, 1998
List of Tables
 3.1   GLXFBConfig   attributes. . . . . . . . . . . . . . . . . . . . . .   13
 3.2   Types of Drawables Supported by GLXFBConfig . . . . . . . .           14
 3.3   Mapping of Visual Types to GLX tokens. . . . . . . . . . . .          14
 3.4   Default values and match criteria for GLXFBConfig attributes.         19
 3.5   Context attributes. . . . . . . . . . . . . . . . . . . . . . . . .   30
 3.6   Masks identifying clobbered bu ers. . . . . . . . . . . . . . .       32
 3.7   GLX attributes for Visuals. . . . . . . . . . . . . . . . . . . .     36
 3.8   Defaults and selection criteria used by glXChooseVisual. .            38
 6.1 Relationship of OpenGL and GLX versions. . . . . . . . . . . 49




                                     iv



                  Version 1.3 - October 19, 1998
Chapter 1

Overview
This document describes GLX, the OpenGL extension to the X Window
System. It refers to concepts discussed in the OpenGL speci cation, and
may be viewed as an X speci c appendix to that document. Parts of the
document assume some acquaintance with both OpenGL and X.
    In the X Window System, OpenGL rendering is made available as an
extension to X in the formal X sense: connection and authentication are
accomplished with the normal X mechanisms. As with other X extensions,
there is a de ned network protocol for the OpenGL rendering commands
encapsulated within the X byte stream.
    Since performance is critical in 3D rendering, there is a way for OpenGL
rendering to bypass the data encoding step, the data copying, and inter-
pretation of that data by the X server. This direct rendering is possible
only when a process has direct access to the graphics pipeline. Allowing
for parallel rendering has a ected the design of the GLX interface. This
has resulted in an added burden on the client to explicitly prevent parallel
execution when such execution is inappropriate.
    X and OpenGL have di erent conventions for naming entry points and
macros. The GLX extension adopts those of OpenGL.




                                      1



                              Version 1.3 - October 19, 1998
Chapter 2

GLX Operation
2.1 Rendering Contexts and Drawing Surfaces
The OpenGL speci cation is intentionally vague on how a rendering context
an abstract OpenGL state machine is created. One of the purposes of
GLX is to provide a means to create an OpenGL context and associate it
with a drawing surface.
    In X, a rendering surface is called a Drawable. X provides two types
of Drawables: Windows which are located onscreen and Pixmaps which are
maintained o screen. The GLX equivalent to a Window is a GLXWindow
and the GLX equivalent to a Pixmap is a GLXPixmap. GLX introduces
a third type of drawable, called a GLXPbuffer, for which there is no X
equivalent. GLXPbuffers are used for o screen rendering but they have
di erent semantics than GLXPixmaps that make it easier to allocate them in
non-visible frame bu er memory.
    GLXWindows, GLXPixmaps and GLXPbuffers are created with respect to
a GLXFBConfig; the GLXFBConfig describes the depth of the color bu er
components and the types, quantities and sizes of the ancillary bu ers i.e.,
the depth, accumulation, auxiliary, and stencil bu ers. Double bu ering
and stereo capability is also xed by the GLXFBConfig.
    Ancillary bu ers are associated with a GLXDrawable, not with a ren-
dering context. If several rendering contexts are all writing to the same
window, they will share those bu ers. Rendering operations to one window
never a ect the unobscured pixels of another window, or the corresponding
pixels of ancillary bu ers of that window. If an Expose event is received
by the client, the values in the ancillary bu ers and in the back bu ers for
regions corresponding to the exposed region become unde ned.
                                       2



                   Version 1.3 - October 19, 1998
2.2. USING RENDERING CONTEXTS                                               3

    A rendering context can be used with any GLXDrawable that it is com-
patible with subject to the restrictions discussed in the section on address
space and the restrictions discussed under glXCreatePixmap. A draw-
able and context are compatible if they
     support the same type of rendering e.g., RGBA or color index
     have color bu ers and ancillary bu ers of the same depth. For exam-
     ple, a GLXDrawable that has a front left bu er and a back left bu er
     with red, green and blue sizes of 4 would not be compatible with a
     context that was created with a visual or GLXFBConfig that has only
     a front left bu er with red, green and blue sizes of 8. However, it would
     be compatible with a context that was created with a GLXFBConfig
     that has only a front left bu er if the red, green and blue sizes are 4.
     were created with respect to the same X screen
    As long as the compatibility constraint is satis ed and the address
space requirement is satis ed, applications can render into the same
GLXDrawable, using di erent rendering contexts. It is also possible to use a
single context to render into multiple GLXDrawables.
    For backwards compatibility with GLX versions 1.2 and earlier, a render-
ing context can also be used to render into a Window. Thus, a GLXDrawable
is the union fGLXWindow, GLXPixmap, GLXPbuffer, Windowg. In X, Windows
are associated with a Visual. In GLX the de nition of Visual has been ex-
tended to include the types, quantities and sizes of the ancillary bu ers and
information indicating whether or not the Visual is double bu ered. For
backwards compatibility, a GLXPixmap can also be created using a Visual.

2.2 Using Rendering Contexts
OpenGL de nes both client state and server state. Thus a rendering context
consists of two parts: one to hold the client state and one to hold the server
state.
    Each thread can have at most one current rendering context. In addition,
a rendering context can be current for only one thread at a time. The client
is responsible for creating a rendering context and a drawable.
    Issuing OpenGL commands may cause the X bu er to be ushed. In
particular, calling glFlush when indirect rendering is occurring, will ush
both the X and OpenGL rendering streams.




                               Version 1.3 - October 19, 1998
4                                                  CHAPTER 2. GLX OPERATION


                         Application
                         and Toolkit
    GLX Client                    GLX
                           Xlib (client state)


                                                       Direct GL
                                                       Renderer
                                                        (server state)




                       Dispatch

     X Server                  X Renderer
                             GL Renderer
                                  (server state)




                                                                     Framebuffer

    Figure 2.1. Direct and Indirect Rendering Block Diagram.


    Some state is shared between the OpenGL and X. The pixel values in
the X frame bu er are shared. The X double bu er extension DBE has a
de nition for which bu er is currently the displayed bu er. This information
is shared with GLX. The state of which bu er is displayed tracks in both
extensions, independent of which extension initiates a bu er swap.

2.3 Direct Rendering and Address Spaces
One of the basic assumptions of the X protocol is that if a client can name
an object, then it can manipulate that object. GLX introduces the notion
of an Address Space. A GLX object cannot be used outside of the address
space in which it exists.
    In a classic UNIX environment, each process is in its own address space.
In a multi-threaded environment, each of the threads will share a virtual
address space which references a common data region.




                     Version 1.3 - October 19, 1998
2.4. OPENGL DISPLAY LISTS                                                     5

    An OpenGL client that is rendering to a graphics engine directly con-
nected to the executing CPU may avoid passing the tokens through the X
server. This generalization is made for performance reasons. The model de-
scribed here speci cally allows for such optimizations, but does not mandate
that any implementation support it.
    When direct rendering is occurring, the address space of the OpenGL
implementation is that of the direct process; when direct rendering is not
being used i.e., when indirect rendering is occurring, the address space
of the OpenGL implementation is that of the X server. The client has the
ability to reject the use of direct rendering, but there may be a performance
penalty in doing so.
    In order to use direct rendering, a client must create a direct rendering
context see gure 2.1. Both the client context state and the server context
state of a direct rendering context exist in the client's address space; this
state cannot be shared by a client in another process. With indirect render-
ing contexts, the client context state is kept in the client's address space and
the server context state is kept in the address space of the X server. In this
case the server context state is stored in an X resource; it has an associated
XID and may potentially be used by another client process.
    Although direct rendering support is optional, all implementations are
required to support indirect rendering.

2.4 OpenGL Display Lists
Most OpenGL state is small and easily retrieved using the glGet* com-
mands. This is not true of OpenGL display lists, which are used, for ex-
ample, to encapsulate a model of some physical object. First, there is no
mechanism to obtain the contents of a display list from the rendering con-
text. Second, display lists may be large and numerous. It may be desirable
for multiple rendering contexts to share display lists rather than replicating
that information in each context.
    GLX provides for limited sharing of display lists. Since the lists are part
of the server context state they can be shared only if the server state for the
sharing contexts exists in a single address space. Using this mechanism, a
single set of lists can be used, for instance, by a context that supports color
index rendering and a context that supports RGBA rendering.
    When display lists are shared between OpenGL contexts, the sharing
extends only to the display lists themselves and the information about which
display list numbers have been allocated. In particular, the value of the base




                               Version 1.3 - October 19, 1998
6                                          CHAPTER 2. GLX OPERATION

set with glListBase is not shared.
    Note that the list named in a glNewList call is not created or superseded
until glEndList is called. Thus if one rendering context is sharing a display
list with another, it will continue to use the existing de nition while the
second context is in the process of re-de ning it. If one context deletes
a list that is being executed by another context, the second context will
continue executing the old contents of the list until it reaches the end.
    A group of shared display lists exists until the last referencing rendering
context is destroyed. All rendering contexts have equal access to using lists
or de ning new lists. Implementations sharing display lists must handle
the case where one rendering context is using a display list when another
rendering context destroys that list or rede nes it.
    In general, OpenGL commands are not guaranteed to be atomic. The
operation of glEndList and glDeleteLists are exceptions: modi ca-
tions to the shared context state as a result of executing glEndList or
glDeleteLists are atomic.


2.5 Texture Objects
OpenGL texture state can be encapsulated in a named texture object. A
texture object is created by binding an unused name to one of the texture
targets GL TEXTURE 1D, GL TEXTURE 2D or GL TEXTURE 3D of a rendering con-
text. When a texture object is bound, OpenGL operations on the target to
which it is bound a ect the bound texture object, and queries of the target
to which it is bound return state from the bound texture object.
     Texture objects may be shared by rendering contexts, as long as the
server portion of the contexts share the same address space. Like display
lists, texture objects are part of the server context state. OpenGL makes
no attempt to synchronize access to texture objects. If a texture object is
bound to more than one context, then it is up to the programmer to ensure
that the contents of the object are not being changed via one context while
another context is using the texture object for rendering. The results of
changing a texture object while another context is using it are unde ned.
     All modi cations to shared context state as a result of executing glBind-
Texture are atomic. Also, a texture object will not be deleted until it is no
longer bound to any rendering context.




                    Version 1.3 - October 19, 1998
2.6. ALIGNING MULTIPLE DRAWABLES                                             7

2.6 Aligning Multiple Drawables
A client can create one window in the overlay planes and a second in the
main planes and then move them independently or in concert to keep them
aligned. To keep the overlay and main plane windows aligned, the client can
use the following paradigm:
     Make the windows which are to share the same screen area children
     of a single window that will never be written. Size and position
     the children to completely occlude their parent. When the window
     combination must be moved or resized, perform the operation on the
     parent.
     Make the subwindows have a background of None so that the X server
     will not paint into the shared area when you restack the children.
     Select for device-related events on the parent window, not on the chil-
     dren. Since device-related events with the focus in one of the child
     windows will be inherited by the parent, input dispatching can be
     done directly without reference to the child on top.

2.7 Multiple Threads
It is possible to create a version of the client side library that is protected
against multiple threads attempting to access the same connection. This
is accomplished by having appropriate de nitions for LockDisplay and
UnlockDisplay. Since there is some performance penalty for doing the
locking, it is implementation-dependent whether a thread safe version, a
non-safe version, or both versions of the library are provided. Interrupt
routines may not share a connection and hence a rendering context with
the main thread. An application may be written as a set of co-operating
processes.
    X has atomicity between clients and sequentiality within a single
client requirements that limit the amount of parallelism achievable when
interpreting the command streams. GLX relaxes these requirements. Se-
quentiality is still guaranteed within a command stream, but not between
the X and the OpenGL command streams. It is possible, for example, that
an X command issued by a single threaded client after an OpenGL command
might be executed before that OpenGL command.
    The X speci cation requires that commands are atomic:




                               Version 1.3 - October 19, 1998
8                                         CHAPTER 2. GLX OPERATION

      If a server is implemented with internal concurrency, the overall
      e ect must be as if individual requests are executed to comple-
      tion in some serial order, and requests from a given connection
      must be executed in delivery order that is, the total execution
      order is a shu e of the individual streams.
OpenGL commands are not guaranteed to be atomic. Some OpenGL ren-
dering commands might otherwise impair interactive use of the windowing
system by the user. For instance calling a deeply nested display list or
rendering a large texture mapped polygon on a system with no graphics
hardware could prevent a user from popping up a menu soon enough to be
usable.
    Synchronization is in the hands of the client. It can be maintained
with moderate cost with the judicious use of the glFinish, glXWaitGL,
glXWaitX, and XSync commands. OpenGL and X rendering can be done
in parallel as long as the client does not preclude it with explicit synchro-
nization calls. This is true even when the rendering is being done by the
X server. Thus, a multi-threaded X server implementation may execute
OpenGL rendering commands in parallel with other X requests.
    Some performance degradation may be experienced if needless switching
between OpenGL and X rendering is done. This may involve a round trip
to the server, which can be costly.




                   Version 1.3 - October 19, 1998
Chapter 3

Functions and Errors
3.1 Errors
Where possible, as in X, when a request terminates with an error, the request
has no side e ects.
   The error codes that may be generated by a request are described with
that request. The following table summarizes the GLX-speci c error codes
that are visible to applications:
 GLXBadContext A   value for a Context argument does not name a Context.
 GLXBadContextState An attempt was made to switch to another rendering
     context while the current context was in glRenderMode GL FEEDBACK
     or GL SELECT, or a call to glXMakeCurrent was made between a
     glBegin and the corresponding call to glEnd.
 GLXBadCurrentDrawable The current Drawable of the calling thread is a
     window or pixmap that is no longer valid.
 GLXBadCurrentWindow The current Window of the calling thread is a win-
     dow that is no longer valid. This error is being deprecated in favor of
     GLXBadCurrentDrawable.

 GLXBadDrawable The Drawable argument does not name a Drawable con-
      gured for OpenGL rendering.
 GLXBadFBConfig The GLXFBConfig argument does not name a
     GLXFBConfig.

 GLXBadPbuffer The GLXPbuffer argument does not name a GLXPbuffer.


                                      9



                              Version 1.3 - October 19, 1998
10                            CHAPTER 3. FUNCTIONS AND ERRORS

 GLXBadPixmap   The Pixmap argument does not name a Pixmap that is ap-
     propriate for OpenGL rendering.
 GLXUnsupportedPrivateRequest May be returned in response to either
     a glXVendorPrivate request or a glXVendorPrivateWithReply
     request.
 GLXBadWindow   The GLXWindow argument does not name a GLXWindow.
    The following error codes may be generated by a faulty GLX implemen-
tation, but would not normally be visible to clients:
 GLXBadContextTag   A rendering request contains an invalid context tag.
     Context tags are used to identify contexts in the protocol.
 GLXBadRenderRequest     A glXRender request is ill-formed.
 GLXBadLargeRequest    A glXRenderLarge request is ill-formed.

3.2 Events
GLX introduces one new event:
 GLX PbufferClobber The given pbu     er has been removed from framebu er
     memory and may no longer be valid. These events are generated as a
     result of con icts in the framebu er allocation between two drawables
     when one or both of the drawables are pbu ers.

3.3 Functions
GLX functions should not be called between glBegin and glEnd operations.
If a GLX function is called within a glBegin glEnd pair, then the result
is unde ned; however, no error is reported.

3.3.1 Initialization
To ascertain if the GLX extension is de ned for an X server, use
     Bool  glXQueryExtension Display *dpy, int
        *error base, int *event base;




                   Version 1.3 - October 19, 1998
3.3. FUNCTIONS                                                             11

dpy speci es the connection to the X server. False is returned if the exten-
sion is not present. error base is used to return the value of the rst error
code and event base is used to return the value of the rst event code. The
constant error codes and event codes should be added to these base values
to get the actual value.
    The GLX de nition exists in multiple versions. Use
     Bool   glXQueryVersionDisplay          *dpy, int *major, int
        *minor;

to discover which version of GLX is available. Upon success, major and
minor are lled in with the major and minor versions of the extension im-
plementation. If the client and server both have the same major version
number then they are compatible and the minor version that is returned is
the minimum of the two minor version numbers.
    major and minor do not return values if they are speci ed as NULL.
    glXQueryVersion returns True if it succeeds and False if it fails. If
it fails, major and minor are not updated.
3.3.2 GLX Versioning
The following functions are available only if the GLX version is 1.1 or later:
     const char *   glXQueryExtensionsStringDisplay            *dpy,
        int screen;

glXQueryExtensionsString returns a pointer to a string describing which
GLX extensions are supported on the connection. The string is zero-
terminated and contains a space-seperated list of extension names. The
extension names themselves do not contain spaces. If there are no exten-
sions to GLX, then the empty string is returned.
     const char *   glXGetClientStringDisplay           *dpy, int
        name;

glXGetClientString returns a pointer to a static, zero-terminated string
describing some aspect of the client library. The possible values for name
are GLX VENDOR, GLX VERSION, and GLX EXTENSIONS. If name is not set to one of
these values then NULL is returned. The format and contents of the vendor
string is implementation dependent, and the format of the extension string
is the same as for glXQueryExtensionsString. The version string is laid
out as follows:




                               Version 1.3 - October 19, 1998
12                            CHAPTER 3. FUNCTIONS AND ERRORS

       major version.minor version       space      vendor-speci c info
Both the major and minor portions of the version number are of arbitrary
length. The vendor-speci c information is optional. However, if it is present,
the format and contents are implementation speci c.
     const char*    glXQueryServerStringDisplay            *dpy, int
        screen, int name;

glXQueryServerString returns a pointer to a static, zero-terminated
string describing some aspect of the server's GLX extension. The possible
values for name and the format of the strings is the same as for glXGet-
ClientString. If name is not set to a recognized value then NULL is returned.
3.3.3 Con guration Management
A GLXFBConfig describes the format, type and size of the color bu ers and
ancillary bu ers for a GLXDrawable. When the GLXDrawable is a GLXWindow
then the GLXFBConfig that describes it has an associated X Visual; for
GLXPixmaps and GLXPbuffers there may or may not be an X Visual asso-
ciated with the GLXFBConfig.
    The attributes for a GLXFBConfig are shown in Table 3.1. The constants
shown here are passed to glXGetFBCon gs and glXChooseFBCon g
to specify which attributes are being queried.
    GLX BUFFER SIZE gives the total depth of the color bu er in bits. For
GLXFBConfigs that correspond to a PseudoColor or StaticColor visual,
this is equal to the depth value reported in the core X11 Visual. For
GLXFBConfigs that correspond to a TrueColor or DirectColor visual,
GLX BUFFER SIZE is the sum of GLX RED SIZE, GLX GREEN SIZE, GLX BLUE SIZE,
and GLX ALPHA SIZE. Note that this value may be larger than the depth
value reported in the core X11 visual since it may include alpha planes
that may not be reported by X11. Also, for GLXFBConfigs that corre-
spond to a TrueColor visual, the sum of GLX RED SIZE, GLX GREEN SIZE, and
GLX BLUE SIZE may be larger than the maximum depth that core X11 can
support.
    The attribute GLX RENDER TYPE has as its value a mask indicating what
type of GLXContext a drawable created with the corresponding GLXFBConfig
can be bound to. The following bit settings are supported: GLX RGBA BIT and
GLX COLOR INDEX BIT. If both of these bits are set in the mask then drawables
created with the GLXFBConfig can be bound to both RGBA and color index
rendering contexts.




                   Version 1.3 - October 19, 1998
3.3. FUNCTIONS                                                             13


         Attribute                Type       Notes
      GLX FBCONFIG ID              XID       XID of GLXFBConfig
      GLX BUFFER SIZE            integer     depth of the color bu er
         GLX LEVEL               integer     frame bu er level
     GLX DOUBLEBUFFER            boolean     True if color bu ers
                                             have front back pairs
        GLX STEREO               boolean     True if color bu ers
                                             have left right pairs
        GLX AUX BUFFERS          integer     no. of auxiliary color bu ers
          GLX RED SIZE           integer     no. of bits of Red in the color bu er
        GLX GREEN SIZE           integer     no. of bits of Green in the color bu er
         GLX BLUE SIZE           integer     no. of bits of Blue in the color bu er
        GLX ALPHA SIZE           integer     no. of bits of Alpha in the color bu er
        GLX DEPTH SIZE           integer     no. of bits in the depth bu er
       GLX STENCIL SIZE          integer     no. of bits in the stencil bu er
      GLX ACCUM RED SIZE         integer     no. Red bits in the accum. bu er
    GLX ACCUM GREEN SIZE         integer     no. Green bits in the accum. bu er
     GLX ACCUM BLUE SIZE         integer     no. Blue bits in the accum. bu er
    GLX ACCUM ALPHA SIZE         integer     no. of Alpha bits in the accum. bu er
        GLX RENDER TYPE          bitmask     which rendering modes are supported.
      GLX DRAWABLE TYPE          bitmask     which GLX drawables are supported.
       GLX X RENDERABLE          boolean     True if X can render to drawable
       GLX X VISUAL TYPE         integer     X visual type of the associated visual
      GLX CONFIG CAVEAT           enum       any caveats for the con guration
    GLX TRANSPARENT TYPE          enum       type of transparency supported
GLX TRANSPARENT INDEX VALUE      integer     transparent index value
 GLX TRANSPARENT RED VALUE       integer     transparent red value
GLX TRANSPARENT GREEN VALUE      integer     transparent green value
 GLX TRANSPARENT BLUE VALUE      integer     transparent blue value
GLX TRANSPARENT ALPHA VALUE      integer     transparent alpha value
    GLX MAX PBUFFER WIDTH        integer     maximum width of GLXPbu er
   GLX MAX PBUFFER HEIGHT        integer     maximum height of GLXPbu er
   GLX MAX PBUFFER PIXELS        integer     maximum size of GLXPbu er
         GLX VISUAL ID           integer     XID of corresponding Visual
                 Table 3.1:    GLXFBConfig     attributes.




                              Version 1.3 - October 19, 1998
14                             CHAPTER 3. FUNCTIONS AND ERRORS

           GLX Token Name                Description
              GLX WINDOW BIT     GLXFBConfig supports windows
              GLX PIXMAP BIT     GLXFBConfig supports pixmaps
             GLX PBUFFER BIT     GLXFBConfig supports pbu ers

         Table 3.2: Types of Drawables Supported by GLXFBConfig

                GLX Token Name                 X Visual Type
                 GLX TRUE COLOR                   TrueColor
                GLX DIRECT COLOR                DirectColor
                GLX PSEUDO COLOR                PseudoColor
                GLX STATIC COLOR                StaticColor
                 GLX GRAY SCALE                   GrayScale
                 GLX STATIC GRAY                 StaticGray
                GLX X VISUAL TYPE         No   associated Visual
            Table 3.3: Mapping of Visual Types to GLX tokens.

    The attribute GLX DRAWABLE TYPE has as its value a mask indicating the
drawable types that can be created with the corresponding GLXFBConfig
the con g is said to support" these drawable types. The valid bit settings
are shown in Table 3.2.
    For example, a GLXFBConfig for which the value of the GLX DRAWABLE TYPE
attribute is
                   j                  j
     GLX WINDOW BIT GLX PIXMAP BIT GLX PBUFFER BIT
can be used to create any type of GLX drawable, while a GLXFBConfig for
which this attribute value is GLX WINDOW BIT can not be used to create a
GLXPixmap or a GLXPbuffer.
    GLX X RENDERABLE is a boolean indicating whether X can be used to render
into a drawable created with the GLXFBConfig. This attribute is True if the
GLXFBConfig supports GLX windows and or pixmaps.
    If a GLXFBConfig supports windows then it has an associated X Visual.
The value of the GLX VISUAL ID attribute speci es the XID of the Visual
and the value of the GLX X VISUAL TYPE attribute speci es the type of Visual.
The possible values are shown in Table 3.3. If a GLXFBConfig does not
support windows, then querying GLX VISUAL ID will return 0 and querying
GLX X VISUAL TYPE will return GLX NONE.
    Note that RGBA rendering may be supported for any of the six Visual




                   Version 1.3 - October 19, 1998
3.3. FUNCTIONS                                                            15

types but color index rendering is supported only for PseudoColor,
StaticColor, GrayScale, and StaticGray visuals i.e., single-channel vi-
suals. If RGBA rendering is supported for a single-channel visual i.e., if
the GLX RENDER TYPE attribute has the GLX RGBA BIT set, then the red com-
ponent maps to the color bu er bits corresponding to the core X11 visual.
The green and blue components map to non-displayed color bu er bits and
the alpha component maps to non-displayed alpha bu er bits if their sizes
are nonzero, otherwise they are discarded.
     The GLX CONFIG CAVEAT attribute may be set to one of the following
values: GLX NONE, GLX SLOW CONFIG or GLX NON CONFORMANT CONFIG. If the at-
tribute is set to GLX NONE then the con guration has no caveats; if it is
set to GLX SLOW CONFIG then rendering to a drawable with this con guration
may run at reduced performance for example, the hardware may not sup-
port the color bu er depths described by the con guration; if it is set to
GLX NON CONFORMANT CONFIG then rendering to a drawable with this con gu-
ration will not pass the required OpenGL conformance tests.
     Servers are required to export at least one GLXFBConfig that sup-
ports RGBA rendering to windows and passes OpenGL conformance
i.e., the GLX RENDER TYPE attribute must have the GLX RGBA BIT set, the
GLX DRAWABLE TYPE attribute must have the GLX WINDOW BIT set and the
GLX CONFIG CAVEAT attribute must not be set to GLX NON CONFORMANT CONFIG.
This GLXFBConfig must have at least one color bu er, a stencil bu er of at
least 1 bit, a depth bu er of at least 12 bits, and an accumulation bu er;
auxillary bu ers are optional, and the alpha bu er may have 0 bits. The
color bu er size for this GLXFBConfig must be as large as that of the deepest
TrueColor, DirectColor, PseudoColor, or StaticColor visual supported
on framebu er level zero the main image planes, and this con guration
must be available on framebu er level zero.
     If the X server exports a PseudoColor or StaticColor visual on frame-
bu er level 0, a GLXFBConfig that supports color index rendering to windows
and passes OpenGL conformance is also required i.e., the GLX RENDER TYPE
attribute must have the GLX COLOR INDEX BIT set, the GLX DRAWABLE TYPE at-
tribute must have the GLX WINDOW BIT set, and the GLX CONFIG CAVEAT at-
tribute must not be set to GLX NON CONFORMANT CONFIG. This GLXFBConfig
must have at least one color bu er, a stencil bu er of at least 1 bit, and a
depth bu er of at least 12 bits. It also must have as many color bitplanes as
the deepest PseudoColor or StaticColor visual supported on framebu er
level zero, and the con guration must be made available on level zero.
     The attribute GLX TRANSPARENT TYPE indicates whether or not the con g-
uration supports transparency, and if it does support transparency, what




                              Version 1.3 - October 19, 1998
16                             CHAPTER 3. FUNCTIONS AND ERRORS

type of transparency is available. If the attribute is set to GLX NONE then
windows created with the GLXFBConfig will not have any transparent
pixels. If the attribute is GLX TRANSPARENT RGB or GLX TRANSPARENT INDEX
then the GLXFBConfig supports transparency. GLX TRANSPARENT RGB is
only applicable if the con guration is associated with a TrueColor
or DirectColor visual: a transparent pixel will be drawn when
the red, green and blue values which are read from the framebu er
are equal to GLX TRANSPARENT RED VALUE, GLX TRANSPARENT GREEN VALUE and
GLX TRANSPARENT BLUE VALUE, respectively. If the con guration is associated
with a PseudoColor, StaticColor, GrayScale or StaticGray visual the
transparency mode GLX TRANSPARENT INDEX is used. In this case, a transpar-
ent pixel will be drawn when the value that is read from the framebu er is
equal to GLX TRANSPARENT INDEX VALUE.
    If GLX TRANSPARENT TYPE is GLX NONE or GLX TRANSPARENT RGB,
then the value for GLX TRANSPARENT INDEX VALUE is unde ned.               If
GLX TRANSPARENT TYPE is GLX NONE or GLX TRANSPARENT INDEX, then the
values for GLX TRANSPARENT RED VALUE, GLX TRANSPARENT GREEN VALUE,
and GLX TRANSPARENT BLUE VALUE are unde ned.                When de ned,
GLX TRANSPARENT RED VALUE,         GLX TRANSPARENT GREEN VALUE,         and
GLX TRANSPARENT BLUE VALUE are integer framebu er values between 0
and the maximum framebu er value for the component. For example,
GLX TRANSPARENT RED VALUE will range between 0 and 2**GLX RED SIZE-1.
GLX TRANSPARENT ALPHA VALUE is for future use.
    GLX MAX PBUFFER WIDTH and GLX MAX PBUFFER HEIGHT indicate the maxi-
mum width and height that can be passed into glXCreatePbu er and
GLX MAX PBUFFER PIXELS indicates the maximum number of pixels width
times height for a GLXPbuffer. Note that an implementation may return a
value for GLX MAX PBUFFER PIXELS that is less than the maximum width times
the maximum height. Also, the value for GLX MAX PBUFFER PIXELS is static
and assumes that no other pbu ers or X resources are contending for the
framebu er memory. Thus it may not be possible to allocate a pbu er of
the size given by GLX MAX PBUFFER PIXELS.
    Use
     GLXFBConfig *    glXGetFBCon gsDisplay          *dpy, int
        screen, int *nelements;

to get the list of all GLXFBConfigs that are available on the speci ed screen.
The call returns an array of GLXFBConfigs; the number of elements in the
array is returned in nelements.




                    Version 1.3 - October 19, 1998
3.3. FUNCTIONS                                                                 17

   Use
      GLXFBConfig *    glXChooseFBCon gDisplay *dpy, int
         screen, const int *attrib list, int *nelements;

to get GLXFBConfigs that match a list of attributes.
    This call returns an array of GLXFBConfigs that match the speci ed
attributes attributes are described in Table 3.1. The number of elements
in the array is returned in nelements.
    If attrib list contains an unde ned GLX attribute, screen is invalid, or
dpy does not support the GLX extension, then NULL is returned.
    All attributes in attrib list, including boolean attributes, are immedi-
ately followed by the corresponding desired value. The list is terminated
with None. If an attribute is not speci ed in attrib list, then the default
value listed in Table 3.4 is used it is said to be speci ed implicitly. For
example, if GLX STEREO is not speci ed then it is assumed to be False. If
GLX DONT CARE is speci ed as an attribute value, then the attribute will not be
checked. GLX DONT CARE may be speci ed for all attributes except GLX LEVEL.
If attrib list is NULL or empty  rst attribute is None, then selection and sort-
ing of GLXFBConfigs is done according to the default criteria in Tables 3.4
and 3.1, as described below under Selection and Sorting.
Selection of GLXFBConfigs
    Attributes are matched in an attribute-speci c manner, as shown in Ta-
ble 3.4. The match criteria listed in the table have the following meanings:
 Smaller GLXFBConfigs with an attribute value that meets or exceeds the
      speci ed value are returned.
 Larger GLXFBConfigs with an attribute value that meets or exceeds the
      speci ed value are returned.
 Exact Only GLXFBConfigs whose attribute value exactly matches the re-
      quested value are considered.
 Mask Only GLXFBConfigs for which the set bits of attribute include all the
      bits that are set in the requested value are considered. Additional
      bits might be set in the attribute.
    Some of the attributes, such as GLX LEVEL, must match the speci ed
value exactly; others, such as GLX RED SIZE must meet or exceed the speci ed
minimum values.




                                Version 1.3 - October 19, 1998
18                               CHAPTER 3. FUNCTIONS AND ERRORS

     To retrieve an GLXFBConfig given its XID, use the GLX FBCONFIG ID at-
tribute. When GLX FBCONFIG ID is speci ed, all other attributes are ignored,
and only the GLXFBConfig with the given XID is returned NULL is returned
if it does not exist.
     If            GLX MAX PBUFFER WIDTH,            GLX MAX PBUFFER HEIGHT,
GLX MAX PBUFFER PIXELS,      or GLX VISUAL ID are speci ed in attrib list,
then they are ignored however, if present, these attributes must still be
followed by an attribute value in attrib list. If GLX DRAWABLE TYPE is spec-
i ed in attrib list and the mask that follows does not have GLX WINDOW BIT
set, then the GLX X VISUAL TYPE attribute is ignored.
     If GLX TRANSPARENT TYPE is set to GLX NONE in attrib list, then in-
clusion of GLX TRANSPARENT INDEX VALUE, GLX TRANSPARENT RED VALUE,
GLX TRANSPARENT GREEN VALUE,          GLX TRANSPARENT BLUE VALUE,          or
GLX TRANSPARENT ALPHA VALUE will be ignored.
     If no GLXFBConfig matching the attribute list exists, then NULL is re-
turned. If exactly one match is found, a pointer to that GLXFBConfig is
returned.
Sorting of GLXFBConfigs
    If more than one matching GLXFBConfig is found, then a list of
GLXFBConfigs,    sorted according to the best match criteria, is returned. The
list is sorted according to the following precedence rules that are applied
in ascending order i.e., con gurations that are considered equal by lower
numbered rule are sorted by the higher numbered rule:
     1. By    GLX CONFIG CAVEAT where the precedence             is     GLX NONE,
        GLX SLOW CONFIG, GLX NON CONFORMANT CONFIG.

     2. Larger total number of RGBA color bits                    GLX RED SIZE,
        GLX GREEN SIZE, GLX BLUE SIZE, plus GLX ALPHA SIZE. If the re-
        quested number of bits in attrib list for a particular color component
        is 0 or GLX DONT CARE, then the number of bits for that component is
        not considered.
     3. Smaller   GLX BUFFER SIZE.

     4. Single bu ered con guration GLX DOUBLE BUFFER being          False   pre-
        cedes a double bu ered one.
     5. Smaller GLX AUX BUFFERS.




                      Version 1.3 - October 19, 1998
3.3. FUNCTIONS                                                         19




          Attribute                 Default          Selection   Sort
                                                    and Sorting Priority
                                                      Criteria
         GLX FBCONFIG ID        GLX DONT CARE          Exact
         GLX BUFFER SIZE               0              Smaller      3
            GLX LEVEL                  0               Exact
       GLX DOUBLEBUFFER         GLX DONT CARE          Exact       4
            GLX STEREO               False             Exact
         GLX AUX BUFFERS               0              Smaller      5
           GLX RED SIZE                0              Larger       2
         GLX GREEN SIZE                0              Larger       2
          GLX BLUE SIZE                0              Larger       2
         GLX ALPHA SIZE                0              Larger       2
         GLX DEPTH SIZE                0              Larger       6
        GLX STENCIL SIZE               0              Larger       7
      GLX ACCUM RED SIZE               0              Larger       8
     GLX ACCUM GREEN SIZE              0              Larger       8
      GLX ACCUM BLUE SIZE              0              Larger       8
     GLX ACCUM ALPHA SIZE              0              Larger       8
         GLX RENDER TYPE         GLX RGBA BIT          Mask
       GLX DRAWABLE TYPE        GLX WINDOW BIT         Mask
        GLX X RENDERABLE        GLX DONT CARE          Exact
       GLX X VISUAL TYPE        GLX DONT CARE          Exact       9
       GLX CONFIG CAVEAT        GLX DONT CARE          Exact       1
     GLX TRANSPARENT TYPE          GLX NONE            Exact
 GLX TRANSPARENT INDEX VALUE    GLX DONT CARE          Exact
  GLX TRANSPARENT RED VALUE     GLX DONT CARE          Exact
 GLX TRANSPARENT GREEN VALUE    GLX DONT CARE          Exact
  GLX TRANSPARENT BLUE VALUE    GLX DONT CARE          Exact
 GLX TRANSPARENT ALPHA VALUE    GLX DONT CARE          Exact
Table 3.4: Default values and match criteria for GLXFBConfig attributes.




                            Version 1.3 - October 19, 1998
20                                  CHAPTER 3. FUNCTIONS AND ERRORS

     6. Larger    GLX DEPTH SIZE.

     7. Smaller   GLX STENCIL BITS.

     8. Larger total number of accumulation bu er color bits
        GLX ACCUM RED SIZE, GLX ACCUM GREEN SIZE, GLX ACCUM BLUE SIZE, plus
        GLX ACCUM ALPHA SIZE. If the requested number of bits in attrib list for
        a particular color component is 0 or GLX DONT CARE, then the number
        of bits for that component is not considered.
     9. By   GLX X VISUAL TYPE where the precedence          is GLX TRUE COLOR,
        GLX DIRECT COLOR,        GLX PSEUDO COLOR,            GLX STATIC COLOR,
        GLX GRAY SCALE, GLX STATIC GRAY.


     Use XFree to free the memory returned by glXChooseFBCon g.
     To get the value of a GLX attribute for a GLXFBConfig use

        int  glXGetFBCon gAttrib  Display *dpy, GLXFBConfig
           config, int attribute, int *value;


If glXGetFBCon gAttrib succeeds then it returns Success and the value
for the speci ed attribute is returned in value; otherwise it returns one of
the following errors:

 GLX BAD ATTRIBUTE attribute      is not a valid GLX attribute.

    Refer to Table 3.1 and Table 3.4 for a list of valid GLX attributes.
    A GLXFBConfig has an associated X Visual only if the
GLX DRAWABLE TYPE attribute has the GLX WINDOW BIT bit set. To retrieve the
associated visual, call:

        XVisualInfo *    glXGetVisualFromFBCon gDisplay
           *dpy, GLXFBConfig config;


If con g is a valid GLXFBConfig and it has an associated X visual then
information describing that visual is returned; otherwise NULL is returned.
Use XFree to free the data returned.




                       Version 1.3 - October 19, 1998
3.3. FUNCTIONS                                                              21

3.3.4 On Screen Rendering
To create an onscreen rendering area, rst create an X Window with a visual
that corresponds to the desired GLXFBConfig, then call
     GLXWindow    glXCreateWindowDisplay *dpy,
        GLXFBConfig config, Window win, const int
        *attrib list;

glXCreateWindow creates a GLXWindow and returns its XID. Any GLX
rendering context created with a compatible GLXFBConfig can be used to
render into this window.
    attrib list speci es a list of attributes for the window. The list has the
same structure as described for glXChooseFBCon g. Currently no
attributes are recognized, so attrib list must be NULL or empty  rst attribute
of None.
    If win was not created with a visual that corresponds to con g, then
a BadMatch error is generated. i.e., glXGetVisualFromFBCon g must
return the visual corresponding to win when the GLXFBConfig parameter
is set to con g. If con g does not support rendering to windows the
GLX DRAWABLE TYPE attribute does not contain GLX WINDOW BIT, a BadMatch
error is generated. If con g is not a valid GLXFBConfig, a GLXBadFBConfig
error is generated. If win is not a valid window XID, then a BadWindow
error is generated. If there is already a GLXFBConfig associated with win
as a result of a previous glXCreateWindow call, then a BadAlloc error
is generated. Finally, if the server cannot allocate the new GLX window, a
BadAlloc error is generated.
    A GLXWindow is destroyed by calling
     glXDestroyWindowDisplay            *dpy, GLXWindow win;

This request deletes the association between the resource ID win and the
GLX window. The storage will be freed when it is not current to any client.
   If win is not a valid GLX window then a GLXBadWindow error is generated.
3.3.5 O Screen Rendering
GLX supports two types of o screen rendering surfaces: GLXPixmaps and
GLXPbuffers. GLXPixmaps and GLXPbuffers di er in the following ways:

  1. GLXPixmaps have an associated X pixmap and can therefore be ren-
     dered to by X. Since a GLXPbuffer is a GLX resource, it may not be
     possible to render to it using X or an X extension other than GLX.




                               Version 1.3 - October 19, 1998
22                              CHAPTER 3. FUNCTIONS AND ERRORS

     2. The format of the color bu ers and the type and size of any associ-
        ated ancillary bu ers for a GLXPbuffer can only be described with
        a GLXFBConfig. The older method of using extended X Visuals to
        describe the con guration of a GLXDrawable cannot be used. See
        section 3.4 for more information on extended visuals.
     3. It is possible to create a GLXPbuffer whose contents may be asyn-
        chronously lost at any time.
     4. If the GLX implementation supports direct rendering, then it must
        support rendering to GLXPbuffers via a direct rendering context. Al-
        though some implementations may support rendering to GLXPixmaps
        via a direct rendering context, GLX does not require this to be sup-
        ported.
     5. The intent of the pbu er semantics is to enable implementations to
        allocate pbu ers in non-visible frame bu er memory. Thus, the allo-
        cation of a GLXPbuffer can fail if there is insu cient framebu er re-
        sources. Implementations are not required to virtualize pbu er mem-
        ory. Also, clients should deallocate GLXPbuffers when they are no
        longer using them for example, when the program is iconi ed.
    To create a GLXPixmap o screen rendering area, rst create an X Pixmap
of the depth speci ed by the desired GLXFBConfig, then call
       GLXPixmap   glXCreatePixmapDisplay *dpy, GLXFBConfig
          config, Pixmap pixmap, const int *attrib list;

glXCreatePixmap creates an o screen rendering area and returns its XID.
Any GLX rendering context created with a GLXFBConfig that is compatible
with con g can be used to render into this o screen area.
    pixmap is used for the RGB planes of the front-left bu er of the resulting
GLX o screen rendering area. GLX pixmaps may be created with a con g
that includes back bu ers and stereoscopic bu ers. However, glXSwap-
Bu ers is ignored for these pixmaps.
    attrib list speci es a list of attributes for the pixmap. The list has the
same structure as described for glXChooseFBCon g. Currently no at-
tributes are recognized, so attrib list must be NULL or empty  rst attribute
of None.
    A direct rendering context might not be able to be made current with a
GLXPixmap.




                     Version 1.3 - October 19, 1998
3.3. FUNCTIONS                                                               23

    If pixmap was not created with respect to the same screen as con g,
then a BadMatch error is generated. If con g is not a valid GLXFBConfig
or if it does not support pixmap rendering then a GLXBadFBConfig error is
generated. If pixmap is not a valid Pixmap XID, then a BadPixmap error
is generated. Finally, if the server cannot allocate the new GLX pixmap, a
BadAlloc error is generated.
    A GLXPixmap is destroyed by calling
      glXDestroyPixmapDisplay          *dpy, GLXPixmap pixmap;

This request deletes the association between the XID pixmap and the GLX
pixmap. The storage for the GLX pixmap will be freed when it is not current
to any client. To free the associated X pixmap, call XFreePixmap.
    If pixmap is not a valid GLX pixmap then a GLXBadPixmap error is
generated.
    To create a GLXPbuffer call
      GLXPbuffer    glXCreatePbu er
                                  Display *dpy,
         GLXFBConfig config, const int *attrib list;

This creates a single GLXPbuffer and returns its XID. Like other drawable
types, GLXPbuffers are shared; any client which knows the associated XID
can use a GLXPbuffer.
    attrib list speci es a list of attributes for the pbu er.          The list
has the same structure as described for glXChooseFBCon g. Cur-
rently only four attributes can be speci ed in attrib list: GLX PBUFFER WIDTH,
GLX PBUFFER HEIGHT, GLX PRESERVED CONTENTS and GLX LARGEST PBUFFER.
    attrib list may be NULL or empty  rst attribute of None, in which case
all the attributes assume their default values as described below.
    GLX PBUFFER WIDTH and GLX PBUFFER HEIGHT specify the pixel width and
height of the rectangular pbu er. The default values for GLX PBUFFER WIDTH
and GLX PBUFFER HEIGHT are zero.
    Use GLX LARGEST PBUFFER to get the largest available pbu er when the
allocation of the pbu er would otherwise fail. The width and height
of the allocated pbu er will never exceed the values of GLX PBUFFER WIDTH
and GLX PBUFFER HEIGHT, respectively. Use glXQueryDrawable to retrieve
the dimensions of the allocated pbu er. By default, GLX LARGEST PBUFFER is
False.
    If the GLX PRESERVED CONTENTS attribute is set to False in attrib list, then
an unpreserved pbu er is created and the contents of the pbu er may be lost




                               Version 1.3 - October 19, 1998
24                             CHAPTER 3. FUNCTIONS AND ERRORS

at any time. If this attribute is not speci ed, or if it is speci ed as True in
attrib list, then when a resource con ict occurs the contents of the pbu er
will be preserved most likely by swapping out portions of the bu er from
the framebu er to main memory. In either case, the client can register to
receive a pbu er clobber event which is generated when the pbu er contents
have been preserved or have been damaged. See glXSelectEvent in
section 3.3.8 for more information.
     The resulting pbu er will contain color bu ers and ancillary bu ers as
speci ed by con g. It is possible to create a pbu er with back bu ers and
to swap the front and back bu ers by calling glXSwapBu ers. Note that
pbu ers use framebu er resources so applications should consider deallocat-
ing them when they are not in use.
     If a pbu er is created with GLX PRESERVED CONTENTS set to False, then
portions of the bu er contents may be lost at any time due to frame bu er
resource con icts. Once the contents of a unpreserved pbu er have been
lost it is considered to be in a damaged state. It is not an error to render to
a pbu er that is in this state but the e ect of rendering to it is the same
as if the pbu er were destroyed: the context state will be updated, but the
frame bu er state becomes unde ned. It is also not an error to query the
pixel contents of such a pbu er, but the values of the returned pixels are
unde ned. Note that while this speci cation allows for unpreserved pbu ers
to be damaged as a result of other pbu er activity, the intent is to have
only the activity of visible windows damage pbu ers.
     Since the contents of a unpreserved pbu er can be lost at anytime with
only asynchronous noti cation via the pbu er clobber event, the only way
a client can guarantee that valid pixels are read back with glReadPixels is
by grabbing the X server. Note that this operation is potentially expensive
and should not be done frequently. Also, since this locks out other X clients,
it should be done only for short periods of time. Clients that don't wish
to do this can check if the data returned by glReadPixels is valid by
calling XSync and then checking the event queue for pbu er clobber events
assuming that these events had been pulled o of the queue prior to the
glReadPixels call.
     When glXCreatePbu er fails to create a GLXPbuffer due to insuf-
  cient resources, a BadAlloc error is generated. If con g is not a valid
GLXFBConfig then a GLXBadFBConfig error is generated; if con g does not
support GLXPbuffers then a BadMatch error is generated.
     A GLXPbuffer is destroyed by calling:




                    Version 1.3 - October 19, 1998
3.3. FUNCTIONS                                                               25

      void  glXDestroyPbu erDisplay             *dpy, GLXPbuffer
         pbuf;

The XID associated with the GLXPbuffer is destroyed. The storage for the
GLXPbuffer    will be destroyed once it is no longer current to any client.
   If pbuf is not a valid GLXPbuffer then a GLXBadPbuffer error is gener-
ated.
3.3.6 Querying Attributes
To query an attribute associated with a GLXDrawable call:
      void  glXQueryDrawable Display *dpy, GLXDrawable
         draw, int attribute, unsigned int *value;

attribute   must     be    set     to      of GLX WIDTH, GLX HEIGHT,
                                          one
GLX PRESERVED CONTENTS, GLX LARGEST PBUFFER, or GLX FBCONFIG ID.
    To get the GLXFBConfig for a GLXDrawable, rst retrieve the XID for
the GLXFBConfig and then call glXChooseFBCon g.
    If draw is not a valid GLXDrawable then a GLXBadDrawable error is
generated. If draw is a GLXWindow or GLXPixmap and attribute is set to
GLX PRESERVED CONTENTS or GLX LARGEST PBUFFER, then the contents of value
are unde ned.
3.3.7 Rendering Contexts
To create an OpenGL rendering context, call
      GLXContext    glXCreateNewContextDisplay *dpy,
         GLXFBConfig config, int render type, GLXContext
         share list, Bool direct;

glXCreateNewContext returns NULL if it fails. If glXCreateNewCon-
text succeeds, it initializes the rendering context to the initial OpenGL
state and returns a handle to it. This handle can be used to render to GLX
windows, GLX pixmaps and GLX pbu ers.
    If render type is set to GLX RGBA TYPE then a context that supports RGBA
rendering is created; if render type is set to GLX COLOR INDEX TYPE then a
context that supports color index rendering is created.
    If share list is not NULL, then all display lists and texture objects except
texture objects named 0 will be shared by share list and the newly created




                                 Version 1.3 - October 19, 1998
26                             CHAPTER 3. FUNCTIONS AND ERRORS

rendering context. An arbitrary number of GLXContexts can share a
single display list and texture object space. The server context state for all
sharing contexts must exist in a single address space or a BadMatch error is
generated.
    If direct is true, then a direct rendering context will be created if the
implementation supports direct rendering and the connection is to an X
server that is local. If direct is False, then a rendering context that renders
through the X server is created.
    Direct rendering contexts may be a scarce resource in some implementa-
tions. If direct is true, and if a direct rendering context cannot be created,
then glXCreateNewContext will attempt to create an indirect context
instead.
    glXCreateNewContext can generate the following errors:
GLXBadContext if share list is neither zero nor a valid GLX rendering
context; GLXBadFBConfig if con g is not a valid GLXFBConfig; BadMatch if
the server context state for share list exists in an address space that cannot
be shared with the newly created context or if share list was created on a
di erent screen than the one referenced by con g; BadAlloc if the server
does not have enough resources to allocate the new context; BadValue if
render type does not refer to a valid rendering type.
    To determine if an OpenGL rendering context is direct, call
      BoolglXIsDirectDisplay *dpy, GLXContext ctx;
glXIsDirect returns True if ctx is a direct rendering context, False other-
wise. If ctx is not a valid GLX rendering context, a GLXBadContext error is
generated.
   An OpenGL rendering context is destroyed by calling
      void   glXDestroyContextDisplay           *dpy, GLXContext
         ctx;

If ctx is still current to any thread, ctx is not destroyed until it is no longer
current. In any event, the associated XID will be destroyed and ctx cannot
subsequently be made current to any thread.
    glXDestroyContext will generate a GLXBadContext error if ctx is not
a valid rendering context.
    To make a context current, call
      Bool   glXMakeContextCurrent Display *dpy,
         GLXDrawable draw, GLXDrawable read, GLXContext
         ctx;




                    Version 1.3 - October 19, 1998
3.3. FUNCTIONS                                                              27

glXMakeContextCurrent binds ctx to the current rendering thread and
to the draw and read drawables. draw is used for all OpenGL operations
except:
     Any pixel data that are read based on the value of GL READ BUFFER.
     Note that accumulation operations use the value of GL READ BUFFER,
     but are not allowed unless draw is identical to read.
     Any depth values that are retrieved by glReadPixels or glCopyP-
     ixels.
     Any stencil values that are retrieved by glReadPixels or glCopyP-
     ixels.
    These frame bu er values are taken from read. Note that the same
GLXDrawable      may be speci ed for both draw and read.
    If the calling thread already has a current rendering context, then that
context is ushed and marked as no longer current. ctx is made the current
context for the calling thread.
     If draw or read are not compatible with ctx a BadMatch error is generated.
If ctx is current to some other thread, then glXMakeContextCurrent will
generate a BadAccess error. GLXBadContextState is generated if there is
a current rendering context and its render mode is either GL FEEDBACK or
GL SELECT. If ctx is not a valid GLX rendering context, GLXBadContext
is generated. If either draw or read are not a valid GLX drawable, a
GLXBadDrawable error is generated.         If the X Window underlying either
draw or read is no longer valid, a GLXBadWindow error is generated. If the
previous context of the calling thread has un ushed commands, and the
previous drawable is no longer valid, GLXBadCurrentDrawable is generated.
Note that the ancillary bu ers for draw and read need not be allocated until
they are needed. A BadAlloc error will be generated if the server does not
have enough resources to allocate the bu ers.
     In addition, implementations may generate a BadMatch error under the
following conditions: if draw and read cannot t into framebu er memory
simultaneously; if draw or read is a GLXPixmap and ctx is a direct rendering
context; if draw or read is a GLXPixmap and ctx was previously bound to a
GLXWindow or GLXPbuffer; if draw or read is a GLXWindow or GLXPbuffer
and ctx was previously bound to a GLXPixmap.
     Other errors may arise when the context state is inconsistent with the
drawable state, as described in the following paragraphs. Color bu ers are




                               Version 1.3 - October 19, 1998
28                             CHAPTER 3. FUNCTIONS AND ERRORS

treated specially because the current GL DRAW BUFFER and GL READ BUFFER con-
text state can be inconsistent with the current draw or read drawable for ex-
ample, when GL DRAW BUFFER is GL BACK and the drawable is single bu ered.
    No error will be generated if the value of GL DRAW BUFFER in ctx indicates
a color bu er that is not supported by draw. In this case, all rendering
will behave as if GL DRAW BUFFER was set to NONE. Also, no error will be
generated if the value of GL READ BUFFER in ctx does not correspond to a valid
color bu er. Instead, when an operation that reads from the color bu er is
executed e.g., glReadPixels or glCopyPixels, the pixel values used will
be unde ned until GL READ BUFFER is set to a color bu er that is valid in read.
Operations that query the value of GL READ BUFFER or GL DRAW BUFFER i.e.,
glGet, glPushAttrib use the value set last in the context, independent
of whether it is a valid bu er in read or draw.
    Note that it is an error to later call glDrawBu er and or glRead-
Bu er even if they are implicitly called via glPopAttrib or glXCopy-
Context and specify a color bu er that is not supported by draw or read.
Also, subsequent calls to glReadPixels or glCopyPixels that specify an
unsupported ancillary bu er will result in an error.
    If draw is destroyed after glXMakeContextCurrent is called, then
subsequent rendering commands will be processed and the context state
will be updated, but the frame bu er state becomes unde ned. If read
is destroyed after glXMakeContextCurrent then pixel values read from
the framebu er e.g., as result of calling glReadPixels, glCopyPixels or
glCopyColorTable are unde ned. If the X Window underlying the
GLXWindow draw or read drawable is destroyed, rendering and readback are
handled as above.
    To release the current context without assigning a new one, set ctx to
NULL and set draw and read to None. If ctx is NULL and draw and read are
not None, or if draw or read are set to None and ctx is not NULL, then a
BadMatch error will be generated.
    The rst time ctx is made current, the viewport and scissor dimensions
are set to the size of the draw drawable as though glViewport0, 0, w,
h and glScissor0, 0, w, h were called, where w and h are the width and
height of the drawable, respectively. However, the viewport and scissor
dimensions are not modi ed when ctx is subsequently made current; it is
the clients responsibility to reset the viewport and scissor in this case.
    Note that when multiple threads are using their current contexts to
render to the same drawable, OpenGL does not guarantee atomicity of frag-
ment update operations. In particular, programmers may not assume that
depth-bu ering will automatically work correctly; there is a race condition




                    Version 1.3 - October 19, 1998
3.3. FUNCTIONS                                                              29

between threads that read and update the depth bu er. Clients are respon-
sible for avoiding this condition. They may use vendor-speci c extensions
or they may arrange for separate threads to draw in disjoint regions of the
framebu er, for example.
    To copy OpenGL rendering state from one context to another, use
     void   glXCopyContextDisplay *dpy, GLXContext
        source, GLXContext dest, unsigned long mask;

glXCopyContext copies selected groups of state variables from source to
dest. mask indicates which groups of state variables are to be copied; it
contains the bitwise OR of the symbolic names for the attribute groups.
The symbolic names are the same as those used by glPushAttrib, described
in the OpenGL Speci cation. Also, the order in which the attributes are
copied to dest as a result of the glXCopyContext operation is the same
as the order in which they are popped o of the stack when glPopAttrib
is called. The single symbolic constant GL ALL ATTRIB BITS can be used to
copy the maximum possible portion of the rendering state. It is not an error
to specify mask bits that are unde ned.
    Not all GL state values can be copied. For example, client side state such
as pixel pack and unpack state, vertex array state and select and feedback
state cannot be copied. Also, some server state such as render mode state,
the contents of the attribute and matrix stacks, display lists and texture
objects, cannot be copied. The state that can be copied is exactly the state
that is manipulated by glPushAttrib.
    If source and dest were not created on the same screen or if the server
context state for source and dest does not exist in the same address space,
a BadMatch error is generated source and dest may be based on di erent
GLXFBConfigs and still share an address space; glXCopyContext will work
correctly in such cases. If the destination context is current for some thread
then a BadAccess error is generated. If the source context is the same
as the current context of the calling thread, and the current drawable of
the calling thread is no longer valid, a GLXBadCurrentDrawable error is
generated. Finally, if either source or dest is not a valid GLX rendering
context, a GLXBadContext error is generated.
    glXCopyContext performs an implicit glFlush if source is the current
context for the calling thread.
    Only one rendering context may be in use, or current, for a particular
thread at a given time. The minimum number of current rendering contexts
that must be supported by a GLX implementation is one. Supporting a




                               Version 1.3 - October 19, 1998
30                             CHAPTER 3. FUNCTIONS AND ERRORS

     Attribute       Type     Description
  GLX FBCONFIG ID    XID      XID of GLXFBConfig associated with context
  GLX RENDER TYPE     int     type of rendering supported
    GLX SCREEN        int     screen number
                       Table 3.5: Context attributes.

larger number of current rendering contexts is essential for general-purpose
systems, but may not be necessary for turnkey applications.
    To get the current context, call
     GLXContext     glXGetCurrentContextvoid;
If there is no current context, NULL is returned.
    To get the XID of the current drawable used for rendering, call
     GLXDrawable    glXGetCurrentDrawablevoid;
If there is no current draw drawable, None is returned.
    To get the XID of the current drawable used for reading, call
     GLXDrawable    glXGetCurrentReadDrawablevoid;
If there is no current read drawable, None is returned.
    To get the display associated with the current context and drawable, call
     Display *   glXGetCurrentDisplayvoid;
If there is no current context, NULL is returned.
    To obtain the value of a context's attribute, use
     int  glXQueryContext Display *dpy, GLXContext ctx,
        int attribute, int *value;

glXQueryContext returns through value the value of attribute for ctx. It
may cause a round trip to the server.
    The values and types corresponding to each GLX context attribute are
listed in Table 3.5.
    glXQueryContext returns GLX BAD ATTRIBUTE if attribute is not a valid
GLX context attribute and Success otherwise. If ctx is invalid and a round
trip to the server is involved, a GLXBadContext error is generated.
    glXGet* calls retrieve client-side state and do not force a round trip
to the X server. Unlike most X calls including the glXQuery* calls that
return a value, these calls do not ush any pending requests.




                    Version 1.3 - October 19, 1998
3.3. FUNCTIONS                                                         31

3.3.8 Events
GLX events are returned in the X11 event stream. GLX and X11 events
are selected independently; if a client selects for both, then both may be
delivered to the client. The relative order of X11 and GLX events is not
speci ed.
    A client can ask to receive GLX events on a GLXWindow or a GLXPbuffer
by calling
     void  glXSelectEventDisplay *dpy, GLXDrawable draw,
        unsigned long event mask;

Calling glXSelectEvent overrides any previous event mask that was set
by the client for draw. Note that the GLX event mask is private to GLX
separate from the core X11 event mask, and that a separate GLX event
mask is maintained in the server state for each client for each drawable.
    If draw is not a valid GLXPbuffer or a valid GLXWindow, a
GLXBadDrawable error is generated.
    To nd out which GLX events are selected for a GLXWindow or
GLXPbuffer call

     void  glXGetSelectedEventDisplay *dpy, GLXDrawable
        draw, unsigned long *event mask;

If draw is not a GLX window or pbu er then a GLXBadDrawable error is
generated.
   Currently only one GLX event can be selected, by setting event mask to
GLX PBUFFER CLOBBER MASK. The data structure describing a pbu er clobber
event is:
     typedef struct    f
          int event type; * GLX DAMAGED or GLX SAVED *
          int draw type; * GLX WINDOW or GLX PBUFFER *
          unsigned long serial; * number of last request processed by server *
          Bool send event; * event was generated by a SendEvent request *
          Display *display; * display the event was read from *
          GLXDrawable drawable; * XID of Drawable *
          unsigned int buffer mask; * mask indicating which bu ers are a ected   *
          unsigned int aux buffer; * which aux bu er was a ected *
          int x, y;
          int width, height;




                             Version 1.3 - October 19, 1998
32                            CHAPTER 3. FUNCTIONS AND ERRORS

                    Bitmask                Corresponding bu er
           GLX FRONT LEFT BUFFER BIT       Front left color bu er
           GLX FRONT RIGHT BUFFER BIT      Front right color bu er
            GLX BACK LEFT BUFFER BIT       Back left color bu er
           GLX BACK RIGHT BUFFER BIT       Back right color bu er
              GLX AUX BUFFERS BIT          Auxillary bu er
              GLX DEPTH BUFFER BIT         Depth bu er
             GLX STENCIL BUFFER BIT        Stencil bu er
              GLX ACCUM BUFFER BIT         Accumulation bu er
              Table 3.6: Masks identifying clobbered bu ers.

            int count;     * if nonzero, at least this many more *
      g GLXPbufferClobberEvent;
    If an implementation doesn't support the allocation of pbu ers, then it
doesn't need to support the generation of GLXPbufferClobberEvents.
    A single X server operation can cause several pbu er clobber events to
be sent e.g., a single pbu er may be damaged and cause multiple pbu er
clobber events to be generated. Each event speci es one region of the
GLXDrawable that was a ected by the X Server operation. bu er mask
indicates which color or ancillary bu ers were a ected; the bits that may be
present in the mask are listed in Table 3.6. All the pbu er clobber events
generated by a single X server action are guaranteed to be contiguous in the
event queue. The conditions under which this event is generated and the
value of event type varies, depending on the type of the GLXDrawable.
    When the GLX AUX BUFFERS BIT is set in bu er mask, then aux bu er is
set to indicate which bu er was a ected. If more than one aux bu er was
a ected, then additional events are generated as part of the same contiguous
event group. Each additional event will have only the GLX AUX BUFFERS BIT
set in bu er mask, and the aux bu er eld will be set appropriately. For non-
stereo drawables, GLX FRONT LEFT BUFFER BIT and GLX BACK LEFT BUFFER BIT
are used to specify the front and back color bu ers.
    For preserved pbu ers, a pbu er clobber event, with event type
GLX SAVED, is generated whenever the contents of a pbu er has to be moved to
avoid being damaged. The events describes which portions of the pbu er
were a ected. Clients who receive many pbu er clobber events, referring to
di erent save actions, should consider freeing the pbu er resource in order




                   Version 1.3 - October 19, 1998
3.3. FUNCTIONS                                                            33

to prevent the system from thrashing due to insu cient resources.
    For an unpreserved pbu er a pbu er clobber event, with event type
GLX DAMAGED, is generated whenever a portion of the pbu er becomes invalid.
    For GLX windows, pbu er clobber events with event type GLX SAVED oc-
cur whenever an ancillary bu er, associated with the window, gets moved
out of o screen memory. The event contains information indicating which
color or ancillary bu ers, and which portions of those bu ers, were a ected.
GLX windows don't generate pbu er clobber events when clobbering each
others' ancillary bu ers, only standard X11 damage events
3.3.9 Synchronization Primitives
To prevent X requests from executing until any outstanding OpenGL ren-
dering is done, call
     void   glXWaitGLvoid;
OpenGL calls made prior to glXWaitGL are guaranteed to be executed
before X rendering calls made after glXWaitGL. While the same result
can be achieved using glFinish, glXWaitGL does not require a round trip
to the server, and is therefore more e cient in cases where the client and
server are on separate machines.
    glXWaitGL is ignored if there is no current rendering context. If the
drawable associated with the calling thread's current context is no longer
valid, a GLXBadCurrentDrawable error is generated.
    To prevent the OpenGL command sequence from executing until any
outstanding X requests are completed, call
     void   glXWaitXvoid;
X rendering calls made prior to glXWaitX are guaranteed to be executed
before OpenGL rendering calls made after glXWaitX. While the same re-
sult can be achieved using XSync, glXWaitX does not require a round
trip to the server, and may therefore be more e cient.
    glXWaitX is ignored if there is no current rendering context. If the
drawable associated with the calling thread's current context is no longer
valid, a GLXBadCurrentDrawable error is generated.
3.3.10 Double Bu ering
For drawables that are double bu ered, the contents of the back bu er can
be made potentially visible i.e., become the contents of the front bu er by
calling




                              Version 1.3 - October 19, 1998
34                             CHAPTER 3. FUNCTIONS AND ERRORS

     void   glXSwapBu ersDisplay           *dpy, GLXDrawable
        draw;

The contents of the back bu er then become unde ned. This operation is
a no-op if draw was created with a non-double-bu ered GLXFBConfig, or if
draw is a GLXPixmap.
    All GLX rendering contexts share the same notion of which are front
bu ers and which are back bu ers for a given drawable. This notion is also
shared with the X double bu er extension DBE.
    When multiple threads are rendering to the same drawable, only one of
them need call glXSwapBu ers and all of them will see the e ect of the
swap. The client must synchronize the threads that perform the swap and
the rendering, using some means outside the scope of GLX, to insure that
each new frame is completely rendered before it is made visible.
    If dpy and draw are the display and drawable for the calling thread's cur-
rent context, glXSwapBu ers performs an implicit glFlush. Subsequent
OpenGL commands can be issued immediately, but will not be executed
until the bu er swapping has completed, typically during vertical retrace of
the display monitor.
    If draw is not a valid GLX drawable, glXSwapBu ers generates a
GLXBadDrawable error. If dpy and draw are the display and drawable as-
sociated with the calling thread's current context, and if draw is a window
that is no longer valid, a GLXBadCurrentDrawable error is generated. If
the X Window underlying draw is no longer valid, a GLXBadWindow error is
generated.

3.3.11 Access to X Fonts
A shortcut for using X fonts is provided by the command
     void   glXUseXFont Font font, int first, int count,
        int list base;

count display lists are de ned starting at list base, each list consisting of a
single call on glBitmap. The de nition of bitmap list base + i is taken from
the glyph rst + i of font. If a glyph is not de ned, then an empty display
list is constructed for it. The width, height, xorig, and yorig of the con-
structed bitmap are computed from the font metrics as rbearing-lbearing,
ascent+descent, -lbearing, and descent respectively. xmove is taken
from the width metric and ymove is set to zero.




                    Version 1.3 - October 19, 1998
3.4. BACKWARDS COMPATIBILITY                                               35

   Note that in the direct rendering case, this requires that the bitmaps be
copied to the client's address space.
   glXUseXFont performs an implicit glFlush.
   glXUseXFont is ignored if there is no current GLX rendering context.
BadFont is generated if font is not a valid X font id. GLXBadContextState is
generated if the current GLX rendering context is in display list construction
mode. GLXBadCurrentDrawable is generated if the drawable associated with
the calling thread's current context is no longer valid.

3.4 Backwards Compatibility
GLXFBConfigs   were introduced in GLX 1.3. Also, new functions for man-
aging drawable con gurations, creating pixmaps, destroying pixmaps, cre-
ating contexts and making a context current were introduced. The 1.2
versions of these functions are still available and are described in this sec-
tion. Even though these older function calls are supported their use is not
recommended.

3.4.1 Using Visuals for Con guration Management
In order to maintain backwards compatibility, visuals continue to be over-
loaded with information describing the ancillary bu ers and color bu ers
for GLXPixmaps and Windows. Note that Visuals cannot be used to create
GLXPbuffers. Also, not all con guration attributes are exported through
visuals e.g., there is no visual attribute to describe which drawables are
supported by the visual.
    The set of extended Visuals is xed at server start up time. Thus
a server can export multiple Visuals that di er only in the extended at-
tributes. Implementors may choose to export fewer GLXDrawable con gu-
rations through visuals than through GLXFBConfigs.
    The X protocol allows a single VisualID to be instantiated at multi-
ple depths. Since GLX allows only one depth for any given VisualID, an
XVisualInfo is used by GLX functions. An XVisualInfo is a fVisual,
Screen, Depthg triple and can therefore be interpreted unambiguously.
    The constants shown in Table 3.7 are passed to glXGetCon g and
glXChooseVisual to specify which attributes are being queried.
    To obtain a description of an OpenGL attribute exported by a Visual
use




                               Version 1.3 - October 19, 1998
36                            CHAPTER 3. FUNCTIONS AND ERRORS




      Attribute           Type       Notes
        GLX USE GL       boolean     True if OpenGL rendering supported
     GLX BUFFER SIZE     integer     depth of the color bu er
         GLX LEVEL       integer     frame bu er level
         GLX RGBA        boolean     True if RGBA rendering supported
    GLX DOUBLEBUFFER     boolean     True if color bu ers have front back pairs
        GLX STEREO       boolean     True if color bu ers have left right pairs
     GLX AUX BUFFERS     integer     number of auxiliary color bu ers
       GLX RED SIZE      integer     number of bits of Red in the color bu er
     GLX GREEN SIZE      integer     number of bits of Green in the color bu er
      GLX BLUE SIZE      integer     number of bits of Blue in the color bu er
     GLX ALPHA SIZE      integer     number of bits of Alpha in the color bu er
     GLX DEPTH SIZE      integer     number of bits in the depth bu er
    GLX STENCIL SIZE     integer     number of bits in the stencil bu er
   GLX ACCUM RED SIZE    integer     number Red bits in the accumulation bu er
 GLX ACCUM GREEN SIZE    integer     number Green bits in the accumulation bu er
  GLX ACCUM BLUE SIZE    integer     number Blue bits in the accumulation bu er
 GLX ACCUM ALPHA SIZE    integer     number Alpha bits in the accumulation bu er
     GLX FBCONFIG ID     integer     XID of most closely associated GLXFBConfig
                  Table 3.7: GLX attributes for Visuals.




                   Version 1.3 - October 19, 1998
3.4. BACKWARDS COMPATIBILITY                                              37

     int   glXGetCon gDisplay *dpy, XVisualInfo *visual,
        int attribute, int *value;

glXGetCon g returns through value the value of the attribute of visual.
   glXGetCon g returns one of the following error codes if it fails, and
Success   otherwise:
 GLX NO EXTENSION dpy     does not support the GLX extension.
 GLX BAD SCREEN   screen of visual does not correspond to a screen.
 GLX BAD ATTRIBUTE     attribute is not a valid GLX attribute.
 GLX BAD VISUAL visual does not     support GLX and an attribute other than
     GLX USE GL was speci ed.

 GLX BAD VALUE   parameter invalid
    A GLX implementation may export many visuals that support OpenGL.
These visuals support either color index or RGBA rendering. RGBA render-
ing can be supported only by Visuals of type TrueColor or DirectColor
unless GLXFBConfigs are used, and color index rendering can be supported
only by Visuals of type PseudoColor or StaticColor.
    glXChooseVisual is used to nd a visual that matches the client's
speci ed attributes.
     XVisualInfo *      glXChooseVisual
                                   Display *dpy, int
        screen, int *attrib list;

glXChooseVisual returns a pointer to an XVisualInfo structure describ-
ing the visual that best matches the speci ed attributes. If no matching
visual exists, NULL is returned.
    The attributes are matched in an attribute-speci c manner, as shown in
Table 3.8. The de nitions for the selection criteria Smaller, Larger, and
Exact are given in section 3.3.3.
    If GLX RGBA is in attrib list then the resulting visual will be TrueColor
or DirectColor. If all other attributes are equivalent, then a TrueColor
visual will be chosen in preference to a DirectColor visual.
    If GLX RGBA is not in attrib list then the returned visual will be
PseudoColor or StaticColor. If all other attributes are equivalent then
a PseudoColor visual will be chosen in preference to a StaticColor visual.




                                 Version 1.3 - October 19, 1998
38                             CHAPTER 3. FUNCTIONS AND ERRORS




                   Attribute          Default Selection Criteria
                    GLX USE GL        True    Exact
                 GLX BUFFER SIZE         0    Smaller
                     GLX LEVEL           0    Exact
                      GLX RGBA        False   Exact
                GLX DOUBLEBUFFER      False   Exact
                    GLX STEREO        False   Exact
                 GLX AUX BUFFERS         0    Smaller
                   GLX RED SIZE          0    Larger
                 GLX GREEN SIZE          0    Larger
                  GLX BLUE SIZE          0    Larger
                 GLX ALPHA SIZE          0    Larger
                 GLX DEPTH SIZE          0    Larger
                GLX STENCIL SIZE         0    Smaller
               GLX ACCUM RED SIZE        0    Larger
              GLX ACCUM GREEN SIZE       0    Larger
              GLX ACCUM BLUE SIZE        0    Larger
              GLX ACCUM ALPHA SIZE       0    Larger
     Table 3.8: Defaults and selection criteria used by glXChooseVisual.




                    Version 1.3 - October 19, 1998
3.4. BACKWARDS COMPATIBILITY                                                39

    If GLX FBCONFIG ID is speci ed in attrib list, then it is ignored however,
if present, it must still be followed by an attribute value.
    If an attribute is not speci ed in attrib list, then the default value is
used. See Table 3.8 for a list of defaults.
    Default speci cations are superseded by the attributes included in at-
trib list. Integer attributes are immediately followed by the corresponding
desired value. Boolean attributes appearing in attrib list have an implicit
True value; such attributes are never followed by an explicit True or False
value. The list is terminated with None.
    To free the data returned, use XFree.
    NULL is returned if an unde ned GLX attribute is encountered.

3.4.2 O Screen Rendering
A GLXPixmap can be created using by calling
     GLXPixmap    glXCreateGLXPixmap Display *dpy,
        XVisualInfo *visual, Pixmap pixmap;

Calling glXCreateGLXPixmapdpy, visual, pixmap is equivalent to call-
ing glXCreatePixmapdpy, con g, pixmap, NULL where con g is the
GLXFBConfig identi ed by the GLX FBCONFIG ID attribute of visual. Before
calling glXCreateGLXPixmap, clients must rst create an X Pixmap
of the depth speci ed by visual. The GLXFBConfig identi ed by the
GLX FBCONFIG ID attribute of visual is associated with the resulting pixmap.
Any compatible GLX rendering context can be used to render into this
o screen area.
    If the depth of pixmap does not match the depth value reported by core
X11 for visual, or if pixmap was not created with respect to the same screen
as visual, then a BadMatch error is generated. If visual is not valid e.g., if
GLX does not support it, then a BadValue error is generated. If pixmap is
not a valid pixmap id, then a BadPixmap error is generated. Finally, if the
server cannot allocate the new GLX pixmap, a BadAlloc error is generated.
    A GLXPixmap created by glXCreateGLXPixmap can be destroyed by
calling
     void   glXDestroyGLXPixmapDisplay               *dpy, GLXPixmap
        pixmap;

This function is equivalent to glXDestroyPixmap; however, GLXPixmaps
created by calls other than glXCreateGLXPixmap should not be passed
to glXDestroyGLXPixmap.




                               Version 1.3 - October 19, 1998
40                            CHAPTER 3. FUNCTIONS AND ERRORS

3.5 Rendering Contexts
An OpenGL rendering context may be created by calling
     GLXContext    glXCreateContext
                                  Display *dpy,
        XVisualInfo *visual, GLXContext share list, Bool
        direct;

Calling glXCreateContextdpy, visual, share list, direct is equivalent to
calling glXCreateNewContextdpy, con g, render type, share list, direct
where con g is the GLXFBConfig identi ed by the GLX FBCONFIG ID attribute
of visual. If visual's GLX RGBA attribute is True then render type is taken as
GLX RGBA TYPE, otherwise GLX COLOR INDEX TYPE. The GLXFBConfig identi ed
by the GLX FBCONFIG ID attribute of visual is associated with the resulting
context.
    glXCreateContext can generate the following errors: GLXBadContext
if share list is neither zero nor a valid GLX rendering context; BadValue
if visual is not a valid X Visual or if GLX does not support it; BadMatch
if share list de nes an address space that cannot be shared with the newly
created context or if share list was created on a di erent screen than the one
referenced by visual; BadAlloc if the server does not have enough resources
to allocate the new context.
    To make a context current, call
     Bool   glXMakeCurrentDisplay *dpy, GLXDrawable
        draw, GLXContext ctx;

Calling glXMakeCurrentdpy, draw, ctx is equivalent to calling glX-
MakeContextCurrentdpy, draw, draw, ctx. Note that draw will be used
for both the draw and read drawable.
    If ctx and draw are not compatible then a BadMatch error will be gen-
erated. Some implementations may enforce a stricter rule and generate a
BadMatch error if ctx and draw were not created with the same XVisualInfo.
    If ctx is current to some other thread, then glXMakeCurrent will
generate a BadAccess error. GLXBadContextState is generated if there
is a current rendering context and its render mode is either GL FEEDBACK
or GL SELECT. If ctx is not a valid GLX rendering context, GLXBadContext
is generated. If draw is not a valid GLXPixmap or a valid Window, a
GLXBadDrawable error is generated. If the previous context of the calling
thread has un ushed commands, and the previous drawable is a window that
is no longer valid, GLXBadCurrentWindow is generated. Finally, note that




                   Version 1.3 - October 19, 1998
3.5. RENDERING CONTEXTS                                                    41

the ancillary bu ers for draw need not be allocated until they are needed. A
BadAlloc error will be generated if the server does not have enough resources
to allocate the bu ers.
    To release the current context without assigning a new one, use NULL for
ctx and None for draw. If ctx is NULL and draw is not None, or if draw is None
and ctx is not NULL, then a BadMatch error will be generated.




                               Version 1.3 - October 19, 1998
Chapter 4

Encoding on the X Byte
Stream
In the remote rendering case, the overhead associated with interpreting the
GLX extension requests must be minimized. For this reason, all commands
have been broken up into two categories: OpenGL and GLX commands that
are each implemented as a single X extension request and OpenGL rendering
requests that are batched within a GLXRender request.

4.1 Requests that hold a single extension request
Each of the commands from glx.h that is, the glX* commands is en-
coded by a separate X extension request. In addition, there is a separate
X extension request for each of the OpenGL commands that cannot be put
into a display list. That list consists of all the glGet* commands plus
     glAreTexturesResident
     glDeleteLists
     glDeleteTextures
     glEndList
     glFeedbackBu er
     glFinish
     glFlush
     glGenLists
     glGenTextures
     glIsEnabled
     glIsList
                                      42



                   Version 1.3 - October 19, 1998
4.2. REQUEST THAT HOLDS MULTIPLE OPENGL COMMANDS 43


                 GLX                  GLX
     Core
          data            data               cmd     data         cmd   data
      X          single             Render



   Figure 4.1. GLX byte stream.


     glIsTexture
     glNewList
     glPixelStoref
     glPixelStorei
     glReadPixels
     glRenderMode
     glSelectBu er

The two PixelStore commands glPixelStorei and glPixelStoref are
exceptions. These commands are issued to the server only to allow it to set
its error state appropriately. Pixel storage state is maintained entirely on the
client side. When pixel data is transmitted to the server by glDrawPixels,
for example, the pixel storage information that describes it is transmitted
as part of the same protocol request. Implementations may not change
this behavior, because such changes would cause shared contexts to behave
incorrectly.

4.2 Request that holds multiple OpenGL com-
    mands
The remaining OpenGL commands are those that may be put into display
lists. Multiple occurrences of these commands are grouped together into
a single X extension request GLXRender. This is diagrammed in Fig-
ure 4.1.
     The grouping minimizes dispatching within the X server. The library
packs as many OpenGL commands as possible into a single X request with-
out exceeding the maximum size limit. No OpenGL command may be split
across multiple GLXRender requests.
     For OpenGL commands whose encoding is longer than the maximum




                                 Version 1.3 - October 19, 1998
44              CHAPTER 4. ENCODING ON THE X BYTE STREAM

X request size, a series of GLXRenderLarge commands are issued. The
structure of the OpenGL command within GLXRenderLarge is the same
as for GLXRender.
    Note that it is legal to have a glBegin in one request, followed by glVer-
tex commands, and eventually the matching glEnd in a subsequent request.
A command is not the same as an OpenGL primitive.

4.3 Wire representations and byte swapping
Unsigned and signed integers are represented as they are represented in
the core X protocol. Single and double precision oating point numbers
are sent and received in IEEE oating point format. The X byte stream
and network speci cations make it impossible for the client to assure that
double precision oating point numbers will be naturally aligned within the
transport bu ers of the server. For those architectures that require it, the
server or client must copy those oating point numbers to a properly aligned
bu er before using them.
    Byte swapping on the encapsulated OpenGL byte stream is performed
by the server using the same rule as the core X protocol. Single precision
 oating point values are swapped in the same way that 32-bit integers are
swapped. Double precision oating point values are swapped across all 8
bytes.

4.4 Sequentiality
There are two sequences of commands: the X stream, and the OpenGL
stream. In general these two streams are independent: Although the com-
mands in each stream will be processed in sequence, there is no guarantee
that commands in the separate streams will be processed in the order in
which they were issued by the calling thread.
    An exception to this rule arises when a single command appears in both
streams. This forces the two streams to rendezvous.
    Because the processing of the two streams may take place at di erent
rates, and some operations may depend on the results of commands in a
di erent stream, we distinguish between commands assigned to each of the
X and OpenGL streams.
    The following commands are processed on the client side and therefore
do not exist in either the X or the OpenGL stream:




                    Version 1.3 - October 19, 1998
4.4. SEQUENTIALITY                                                   45

     glXGetClientString
     glXGetCurrentContext
     glXGetCurrentDisplay
     glXGetCurrentDrawable
     glXGetCurrentReadDrawable
     glXGetCon g
     glXGetFBCon gAttrib
     glXGetFBCon gs
     glXGetSelectedEvent
     glXGetVisualFromFBCon g

   The following commands are in the X stream and obey the sequentiality
guarantees for X requests:
     glXChooseFBCon g
     glXChooseVisual
     glXCreateContext
     glXCreateGLXPixmap
     glXCreateNewContext
     glXCreatePbu er
     glXCreatePixmap
     glXCreateWindow
     glXDestroyContext
     glXDestroyGLXPixmap
     glXDestroyPbu er
     glXDestroyPixmap
     glXDestroyWindow
     glXMakeContextCurrent
     glXMakeCurrent
     glXIsDirect
     glXQueryContext
     glXQueryDrawable
     glXQueryExtension
     glXQueryExtensionsString
     glXQueryServerString
     glXQueryVersion
     glXSelectEvent
     glXWaitGL
     glXSwapBu ers  see below




                            Version 1.3 - October 19, 1998
46               CHAPTER 4. ENCODING ON THE X BYTE STREAM

      glXCopyContext  see below

     glXSwapBu ers is in the X stream if and only if the display and draw-
able are not those belonging to the calling thread's current context; other-
wise it is in the OpenGL stream. glXCopyContext is in the X stream
alone if and only if its source context di ers from the calling thread's cur-
rent context; otherwise it is in both streams.
   Commands in the OpenGL stream, which obey the sequentiality guar-
antees for OpenGL requests are:
      glXWaitX
      glXSwapBu ers see below
      All OpenGL Commands

   glXSwapBu ers is in the OpenGL stream if and only if the display
and drawable are those belonging to the calling thread's current context;
otherwise it is in the X stream.
   Commands in both streams, which force a rendezvous, are:
      glXCopyContext see below
      glXUseXFont

     glXCopyContext is in both streams if and only if the source context
is the same as the current context of the calling thread; otherwise it is in
the X stream only.




                    Version 1.3 - October 19, 1998
Chapter 5

Extending OpenGL
OpenGL implementors may extend OpenGL by adding new OpenGL com-
mands or additional enumerated values for existing OpenGL commands.
When a new vendor-speci c command is added, GLX protocol must also be
de ned. If the new command is one that cannot be added to a display list,
then protocol for a new glXVendorPrivate or glXVendorPrivateWith-
Reply request is required; otherwise protocol for a new rendering command
that can be sent to the X Server as part of a glXRender or glXRender-
Large request is required.
   The OpenGL Architectural Review Board maintains a registry of vendor-
speci c enumerated values; opcodes for vendor private requests, vendor pri-
vate with reply requests, and OpenGL rendering commands; and vendor-
speci c error codes and event codes.
    New names for OpenGL functions and enumerated types must clearly
indicate whether some particular feature is in the core OpenGL or is vendor
speci c. To make a vendor-speci c name, append a company identi er in
upper case and any additional vendor-speci c tags e.g. machine names.
For instance, SGI might add new commands and manifest constants of the
form glNewCommandSGI and GL NEW DEFINITION SGI. If two or more li-
censees agree in good faith to implement the same extension, and to make
the speci cation of that extension publicly available, the procedures and
tokens that are de ned by the extension can be su xed by EXT.
   Implementors may also extend GLX. As with OpenGL, the new names
must indicate whether or not the feature is vendor-speci c. e.g., SGI
might add new GLX commands and constants of the form glXNewCom-
mandSGI and GLX NEW DEFINITION SGI. When a new GLX command is
added, protocol for a new glXVendorPrivate or glXVendorPrivate-
                                    47



                             Version 1.3 - October 19, 1998
48                                CHAPTER 5. EXTENDING OPENGL

WithReply request is required.




                 Version 1.3 - October 19, 1998
Chapter 6

GLX Versions
Each version of GLX supports all versions of OpenGL up to the version
shown in Table 6.1 corresponding to the given GLX version.

6.1 New Commands in GLX Version 1.1
The following GLX commands were added in GLX Version 1.1:
    glXQueryExtensionsString
    glXGetClientString
    glXQueryServerString

6.2 New Commands in GLX Version 1.2
The following GLX commands were added in GLX Version 1.2:

                  GLX Version      Highest OpenGL
                                  Version Supported
                    GLX 1.0          OpenGL 1.0
                    GLX 1.1          OpenGL 1.0
                    GLX 1.2          OpenGL 1.1
                    GLX 1.3          OpenGL 1.2
         Table 6.1: Relationship of OpenGL and GLX versions.

                                  49



                           Version 1.3 - October 19, 1998
50                                        CHAPTER 6. GLX VERSIONS

     glXGetCurrentDisplay

6.3 New Commands in GLX Version 1.3
The following GLX commands were added in GLX Version 1.3:
     glXChooseFBCon g
     glXGetFBCon gAttrib
     glXGetVisualFromFBCon g
     glXCreateWindow
     glXDestroyWindow
     glXCreatePixmap
     glXDestroyPixmap
     glXCreatePbu er
     glXDestroyPbu er
     glXQueryDrawable
     glXCreateNewContext
     glXMakeContextCurrent
     glXGetCurrentReadDrawable
     glXQueryContext
     glXSelectEvent
     glXGetSelectedEvent




                 Version 1.3 - October 19, 1998
Chapter 7

Glossary
Address Space the set of objects or memory locations accessible through
     a single name space. In other words, it is a data region that one or
     more processes may share through pointers.
Client an X client. An application communicates to a server by some path.
     The application program is referred to as a client of the window system
     server. To the server, the client is the communication path itself. A
     program with multiple connections is viewed as multiple clients to
     the server. The resource lifetimes are controlled by the connection
     lifetimes, not the application program lifetimes.
Compatible an OpenGL rendering context is compatible with may be
     used to render into a GLXDrawable if they meet the constraints spec-
     i ed in section 2.1.
Connection a bidirectional byte stream that carries the X and GLX pro-
     tocol between the client and the server. A client typically has only one
     connection to a server.
Rendering Context a OpenGL rendering context. This is a virtual
     OpenGL machine. All OpenGL rendering is done with respect to a
     context. The state maintained by one rendering context is not a ected
     by another except in case of shared display lists and textures.
GLXContext a handle to a rendering context. Rendering contexts consist
     of client side state and server side state.
Similar a potential correspondence among GLXDrawables and rendering
     contexts. Windows and GLXPixmaps are similar to a rendering context
                                     51



                              Version 1.3 - October 19, 1998
52                                                  CHAPTER 7. GLOSSARY

    are similar if, and only if, they have been created with respect to the
    same VisualID and root window.
Thread one of a group of processes all sharing the same address space.
    Typically, each thread will have its own program counter and stack
    pointer, but the text and data spaces are visible to each of the threads.
    A thread that is the only member of its group is equivalent to a process.




                   Version 1.3 - October 19, 1998
Index of GLX Commands
BadAccess, 27, 29, 40                       glGet*, 5, 42
BadAlloc, 21, 23, 24, 26, 27, 39 41         glIsEnabled, 42
BadFont, 35                                 glIsList, 42
BadMatch, 21, 23, 24, 26 29, 39 41          glIsTexture, 43
BadPixmap, 23, 39                           glListBase, 6
BadValue, 26, 39, 40                        glNewCommandSGI, 47
BadWindow, 21                               glNewList, 6, 43
                                            glPixelStoref, 43
GL ALL ATTRIB BITS, 29                      glPixelStorei, 43
GL BACK, 28                                 glPopAttrib, 28, 29
GL DRAW BUFFER, 28                          glPushAttrib, 28, 29
GL FEEDBACK,9,27, 40                        glReadBu er, 28
GL NEW DEFINITION SGI, 47                   glReadPixels, 24, 27, 28, 43
GL READ BUFFER,27, 28                       glRenderMode, 9, 43
GL SELECT,9,27, 40                          glScissor, 28
GL TEXTURE 1D, 6
GL TEXTURE 2D, 6                            glSelectBu er, 43
GL TEXTURE 3D, 6                            glVertex, 44
glAreTexturesResident, 42                   glViewport, 28
glBegin, 9, 10, 44                          glX*, 42
glBindTexture, 6                            GLX ACCUM ALPHA SIZE,13,19,
glBitmap, 34                                          20,36, 38
glCopyColorTable, 28                        GLX ACCUM BLUE SIZE,13,19,
glCopyPixels, 27, 28                                  20,36, 38
glDeleteLists, 6, 42                        GLX ACCUM BUFFER BIT, 32
glDeleteTextures, 42                        GLX ACCUM GREEN SIZE,13,19,
glDrawBu er, 28                                       20,36, 38
glDrawPixels, 43                            GLX ACCUM RED SIZE,13,19,20,
glEnd, 9, 10, 44                                      36, 38
glEndList, 6, 42                            GLX ALPHA SIZE,12,13,18,19,36,
glFeedbackBu er, 42                                   38
glFinish, 8, 33, 42                         GLX AUX BUFFERS,13,18,19,36,
glFlush, 3, 29, 34, 35, 42                            38
glGenLists, 42                              GLX AUX BUFFERS BIT, 32
glGenTextures, 42                           GLX BACK LEFT BUFFER BIT,
glGet, 28                                             32

                                       53



                                Version 1.3 - October 19, 1998
54                                                                  INDEX

GLX BACK RIGHT BUFFER BIT,                 GLX NON CONFORMANT
      32                                          CONFIG,15, 18
GLX BAD ATTRIBUTE,20,30, 37                GLX NONE,14--16,18, 19
GLX BAD SCREEN, 37                         GLX PBUFFER, 31
GLX BAD VALUE, 37                          GLX PBUFFER BIT, 14
GLX BAD VISUAL, 37                         GLX PBUFFER CLOBBER
GLX BLUE SIZE,12,13,18,19,36, 38                  MASK, 31
GLX BUFFER SIZE,12,13,18,19,36,            GLX PBUFFER HEIGHT, 23
      38                                   GLX PBUFFER WIDTH, 23
GLX COLOR INDEX BIT,12, 15                 GLX Pbu erClobber, 10
GLX COLOR INDEX TYPE,25, 40                GLX PIXMAP BIT, 14
GLX CONFIG CAVEAT,13,15,18,                GLX PRESERVED CONTENTS,
      19                                          23 25
GLX DAMAGED,31, 33                         GLX PSEUDO COLOR,14, 20
GLX DEPTH BUFFER BIT, 32                   GLX RED SIZE,12,13,16--19,36, 38
GLX DEPTH SIZE,13,19,20,36, 38             GLX RENDER TYPE,12,13,15,19,
GLX DIRECT COLOR,14, 20                           30
GLX DONT CARE, 17 20                       GLX RGBA,36--38, 40
GLX DOUBLE BUFFER, 18                      GLX RGBA BIT,12,15, 19
GLX DOUBLEBUFFER,13,19,36,                 GLX RGBA TYPE,25, 40
      38                                   GLX SAVED, 31 33
GLX DRAWABLE TYPE,13--15,                  GLX SCREEN, 30
      18 21                                GLX SLOW CONFIG,15, 18
                                           GLX STATIC COLOR,14, 20
GLX EXTENSIONS, 11                         GLX STATIC GRAY,14, 20
GLX FBCONFIG ID,13,18,19,25,               GLX STENCIL BITS, 20
      30,36,39, 40                         GLX STENCIL BUFFER BIT, 32
GLX FRONT LEFT BUFFER BIT,                 GLX STENCIL SIZE,13,19,36, 38
      32                                   GLX STEREO,13,17,19,36, 38
GLX FRONT RIGHT BUFFER                     GLX TRANSPARENT ALPHA
      BIT, 32                                     VALUE,13,16,18, 19
GLX GRAY SCALE,14, 20                      GLX TRANSPARENT BLUE
GLX GREEN SIZE,12,13,18,19,36,                    VALUE,13,16,18, 19
      38                                   GLX TRANSPARENT GREEN
GLX HEIGHT, 25                                    VALUE,13,16,18, 19
GLX LARGEST PBUFFER,23, 25                 GLX TRANSPARENT INDEX, 16
GLX LEVEL,13,17,19,36, 38                  GLX TRANSPARENT INDEX
GLX MAX PBUFFER HEIGHT,13,                        VALUE,13,16,18, 19
      16, 18                               GLX TRANSPARENT RED
GLX MAX PBUFFER PIXELS,13,                        VALUE,13,16,18, 19
      16, 18                               GLX TRANSPARENT RGB, 16
GLX MAX PBUFFER WIDTH,13,                  GLX TRANSPARENT TYPE,13,
      16, 18                                      15,16,18, 19
GLX NEW DEFINITION SGI, 47                 GLX TRUE COLOR,14, 20
GLX NO EXTENSION, 37                       GLX USE GL, 36 38




                  Version 1.3 - October 19, 1998
INDEX                                                                        55

GLX VENDOR, 11                             glXGet*, 30
GLX VERSION, 11                            glXGetClientString, 11, 12, 45, 49
GLX VISUAL ID,13,14, 18                    glXGetCon g, 35, 37, 45
GLX WIDTH, 25                              glXGetCurrentContext, 30, 45
GLX WINDOW, 31                             glXGetCurrentDisplay, 30, 45, 50
GLX WINDOW BIT,14,15, 18 21                glXGetCurrentDrawable, 30, 45
GLX X RENDERABLE,13,14, 19                 glXGetCurrentReadDrawable, 30, 45,
GLX X VISUAL TYPE,13,14, 18                         50
        20                                 glXGetFBCon gAttrib, 20, 45, 50
GLXBadContext, 9, 26, 27, 29, 30, 40       glXGetFBCon gs, 12, 16, 45
GLXBadContextState, 9, 27, 35, 40          glXGetSelectedEvent, 31, 45, 50
GLXBadContextTag, 10                       glXGetVisualFromFBCon g, 20, 21,
GLXBadCurrentDrawable, 9, 27, 29,                   45, 50
        33 35                              glXIsDirect, 26, 45
GLXBadCurrentWindow, 9, 40                 glXMakeContextCurrent, 26 28, 40,
GLXBadDrawable, 9, 25, 27, 31, 34,                  45, 50
        40                                 glXMakeCurrent, 9, 40, 45
GLXBadFBCon g, 9, 23, 24, 26               glXNewCommandSGI, 47
GLXBadLargeRequest, 10                     GLXPbu er, 2, 3, 9, 12, 14, 16, 21
GLXBadPbu er, 9, 25                                 25, 27, 31, 35
GLXBadPixmap, 10, 23                       GLXPbu erClobberEvent, 32
GLXBadRenderRequest, 10                    GLXPixmap, 2, 3, 12, 14, 21 23, 25,
GLXBadWindow, 10, 21, 27, 34                        27, 34, 35, 39, 40, 51
glXChooseFBCon g, 12, 17, 20 23,           glXQuery*, 30
        25, 45, 50                         glXQueryContext, 30, 45, 50
glXChooseVisual, 35, 37, 38, 45            glXQueryDrawable, 23, 25, 45, 50
GLXContext, 12                             glXQueryExtension, 10, 45
glXCopyContext, 28, 29, 46                 glXQueryExtensionsString, 11, 45, 49
glXCreateContext, 40, 45                   glXQueryServerString, 12, 45, 49
glXCreateGLXPixmap, 39, 45                 glXQueryVersion, 11, 45
glXCreateNewContext, 25, 26, 40, 45,       GLXRender, 42
        50                                 glXSelectEvent, 24, 31, 45, 50
glXCreatePbu er, 16, 23, 24, 45, 50        glXSwapBu ers, 22, 24, 34, 45, 46
glXCreatePixmap, 3, 22, 39, 45, 50         GLXUnsupportedPrivateRequest, 10
glXCreateWindow, 21, 45, 50                glXUseXFont, 34, 35, 46
glXDestroyContext, 26, 45                  glXWaitGL, 8, 33, 45
glXDestroyGLXPixmap, 39, 45                glXWaitX, 8, 33, 46
glXDestroyPbu er, 25, 45, 50               GLXWindow, 2, 3, 10, 12, 21, 25, 27,
glXDestroyPixmap, 23, 39, 45, 50                    28, 31
glXDestroyWindow, 21, 45, 50
GLXDrawable, 2, 3, 12, 22, 25, 27,         None, 17, 21 23, 28, 30, 39, 41
        31, 32, 35, 51
GLXFBCon g, 2, 3, 9, 12 26, 29, 30,        PixelStore, 43
        34 37, 39, 40
GLXFBCon gs, 17, 18                        Screen, 35




                               Version 1.3 - October 19, 1998
56                                                     INDEX

Success, 20, 30, 37
Visual, 3, 12, 14, 20, 22, 35 37, 40
VisualID, 35
Window, 2, 3, 9, 21, 27, 28, 34, 40
Windows, 35
XFree, 20, 39
XFreePixmap, 23
XSync, 8, 24, 33
XVisualInfo, 35




                      Version 1.3 - October 19, 1998
