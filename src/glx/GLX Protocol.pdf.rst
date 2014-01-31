   GLX, the protocol
for networked OpenGL
                       Mark J. Kilgard
                        mjk@sgi.com
                   Silicon Graphics, Inc.

                    Connetathon ’96
                   February 28, 1996
SiliconGraphics
Computer Systems
                     Jist of this talk...
                        Overview of
                   OpenGL’s GLX protocol
                           for the
                     network engineer,
                          not the
                     graphics engineer:
                   What does GLX do?
                     When is it used?
                   How does it operate?
                   What’s novel about it?
SiliconGraphics
Computer Systems
                        What does GLX do?
o GLX is an X11 extension protocol.
o GLX integrates the OpenGL 3D graphics
  standard with the X Window System.
o GLX provides two things:

  1)                   Network protocol for network
                       extensibility.
  2)                   Integration and programming
                       interface for using OpenGL with X.
    SiliconGraphics
    Computer Systems
                       OpenGL (in two slides)
o Industry standard programming interface
  for interactive 2D and 3D graphics.
o Developed by Silicon Graphics.
o Overseen by Architectural Review Board.

o Low−level, procedural interface.
o High−performance, well−suited to
  hardware implementation.

    SiliconGraphics
    Computer Systems
                   OpenGL (almost done!)
o Mandated functionality; no subsetting
  of rendering capabilities.
o Advanced functionality: lighting,
  texture mapping, antialiasing, blah, blah.
o Conformance suite & well−defined
  specification provides compatibility.
o Window system independent rendering
  interface. X, NT, OS/2, Mac, etc.

    SiliconGraphics
    Computer Systems
    Obligatory OpenGL State Machine

          Display
          list


                                      Per−Vertex
                                      Operations               Per−
                         Evaluator                 Rasteriz−
                                      Primitive                Fragment
                                                   ation
                                      Assembly                 Operations


commands
                                                   Texture
                                                   Memory

                                Pixel                            Frame−
                                Operations                       buffer




      SiliconGraphics
      Computer Systems
Integrating OpenGL with win−systems
o OpenGL’s win−system independence
  requires integration to win−systems.
o Each window system defines its own
  interface model/API to use OpenGL.
o Functionality provided: creating
  rendering contexts, binding to windows,
  buffer swaps, etc.
o GLX is OpenGL’s interface for X11.

    SiliconGraphics
    Computer Systems
              How does GLX do its job?
o GLX is implemented as X extension.
o Therefore, GLX protocol embedded in
    the X protocol stream.
o GLX also has API.
  Example: glXCreateContext
o Both GLX and OpenGL calls translated
  into GLX protocol requests.
o GLX protocol is standard & interoperable.
    SiliconGraphics
    Computer Systems
                      Example GLX calls
o glXChooseVisual
o glXCreateContext
o glXCreateGLXPixmap
o glXSwapBuffers
o glXCopyContext
o glXDestroyContext

   SiliconGraphics
   Computer Systems
 GLX makes X server 3D render proxy

Client code                                       Rest of the X server
      GLwMDrawingArea
      widget

                                          Motif
  OpenGL GLX                    X
  API    API                    Toolkit                             GLX/
                                                          Core X
                                                          rendering OpenGL
                                                                    extension
                         Xlib



                             X Protocol Connection
                           (TCP/IP, local socket, etc.)        Graphics hardware


      SiliconGraphics
      Computer Systems
     Distinction: GLX and OpenGL
o Logically, two distinct APIs (gl− vs. glX−).
o OpenGL = 3D rendering.

o GLX = managing OpenGL for X.

o Two APIs packed into the single
  GLX protocol.




    SiliconGraphics
    Computer Systems
   A little about OpenGL rendering
o OpenGL routines take no context or
  destination: Example:
         glRectf(1.0,2.0,1.0,3.0);

o GLX ‘‘binds’’ an OpenGL context and
  drawable to thread with glXMakeCurrent.
o OpenGL calls done with respect to
  current bound context and drawable.
o Lower overhead; win−sys independent API.
    SiliconGraphics
    Computer Systems
              Generating GLX Requests
o Most GLX calls have corresponding
  GLX protocol request.
o OpenGL rendering calls (no replies)
  are packed into glXRender requests.
o OpenGL rendering calls (no replies)
  with >256KB data use glXRenderLarge.
o Non−rendering OpenGL calls each
  have corresponding GLX requests.

    SiliconGraphics
    Computer Systems
  Displays Lists Minimize Bandwidth
o To reduce protocol overhead, OpenGL
  display lists are useful, ie. glCallList
o Display lists are uneditable sequences
  of OpenGL commands.
o Once created, they are in the X server.
o Display lists can call other display lists.
o Effective use minimizes protocol use.

    SiliconGraphics
    Computer Systems
                       GLX Context Tags
o Multiple client threads using shared
  X server connection?
o ‘‘Make current’’ managed per−thread,
  not X connection.
o Each OpenGL request sends a GLX
  Context Tag identifying thread.
o Context tag to use is returned by
  glXMakeCurrent request.

    SiliconGraphics
    Computer Systems
            Value of GLX Context Tags
o Context tags distinguish distinct
  threads’ current OpenGL binding.
o GLX API hides this ‘‘protocol detail’’
  from the program calling GLX &
  OpenGL routines.

o In practice, value of this is dubious.




    SiliconGraphics
    Computer Systems
  OpenGL & X Streams Independent
o OpenGL & X command streams
  independent.
o glXWaitX and glXWaitGL provide
  explicit ordering of the streams.
o Logically, these exist in both streams.
o More about why this might be later. . .



    SiliconGraphics
    Computer Systems
 GLX & OpenGL Extensions Possible
o Yes, extensions of an X extension!
o glXVendorPrivate &
  glXVendorPrivateWithReply
o Op−code space assigned by OpenGL
  ARB for shared extensions; vendor
  ranges for vendor−specific extensions.
o Distinct GLX and OpenGL extensions
  possible.

    SiliconGraphics
    Computer Systems
Overhead of GLX Protocol Hurts OpenGL
             Performance
o 3D graphics & imaging = hi−bandwidth.
o Network extensibility is nice, but . . .
o For fast graphics hardware, GLX
  protocol ‘‘relay’’ starves graphics
  hardware.
o GLX permits bypassing of protocol
  for (local) direct access.

    SiliconGraphics
    Computer Systems
Architecture of Direct Rendering OpenGL
           (locals only, dude!)
 Client code                                                Rest of the X server
       GLwMDrawingArea
       widget

                                           Motif
   OpenGL GLX                    X
   API    API                    Toolkit                                  GLX/
                                                                Core X
                                                                rendering OpenGL
                                                                          extension
                          Xlib

                                    X Protocol Connection



                                      Graphics hardware
       SiliconGraphics
       Computer Systems
 Direct Rendering Bypasses X Server
o Optional for GLX implementations.
o glXCreateContext has option to try
  direct rendering.
o Need some support for virtualizing
  access to graphics.
  See ‘‘System Support for OpenGL Direct Rendering,’’ GI ’95.

o OpenGL calls = direct hardware access;
  no protocol (independent streams!).

o Connection to X server still exists.
    SiliconGraphics
    Computer Systems
 Example of Local RPC Optimization
o Access to OpenGL’s state machine
  can be considered client/server.
o Logically, OpenGL rendering commands
  are Remote Procedure Calls.
o GLX’s direct rendering is an example
  of local RPC optimization.
o Direct rendering lets OpenGL render
  at hardware performance limits!

    SiliconGraphics
    Computer Systems
                       GLX Summary
o GLX supports OpenGL for X11.
o Makes OpenGL inter−operable &
  network extensible.
o GLX itself can be extended for GLX
  and OpenGL extensions.
o Direct rendering is very important
  optimization of GLX (by eliminating
  the rendering protocol!).

    SiliconGraphics
    Computer Systems
