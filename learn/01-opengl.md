---
layout: default
---
# OpenGL

Before starting our journey we should first define what OpenGL actually is. OpenGL is mainly considered an API (an <span><mark>Application Programming Interface</mark></span>) that provides us with a large set of functions that we can use to manipulate graphics and images. However, OpenGL by itself is not an API, but merely a specification, developed and maintained by the [Khronos Group](http://www.khronos.org/).

![Image of OpenGL's logo](/images/01-opengl.jpg){:.img-rounded .pull-xs-right}{:width="275px" height="142px"}

The OpenGL specification specifies exactly what the result/output of each function should be and how it should perform. It is then up to the developers implementing this specification to come up with a solution of how this function should operate. Since the OpenGL specification does not give us implementation details, the actual developed versions of OpenGL are allowed to have different implementations, as long as their results comply with the specification (and are thus the same to the user).

The people developing the actual OpenGL libraries are usually the graphics card manufacturers. Each graphics card that you buy supports specific versions of OpenGL which are the versions of OpenGL developed specifically for that card (series). When using an Apple system the OpenGL library is maintained by Apple themselves and under Linux there exists a combination of graphic suppliers' versions and hobbyists' adaptations of these libraries. This also means that whenever OpenGL is showing weird behavior that it shouldn't, this is most likely the fault of the graphics cards manufacturers (or whoever developed/maintained the library).

Since most implementations are built by graphics card manufacturers. Whenever there is a bug in the implementation this is usually solved by updating your video card drivers; those drivers include the newest versions of OpenGL that your card supports. This is one of the reasons why it's always advised to occasionally update your graphic drivers.
{: .alert .alert-info}

Khronos publicly hosts all specification documents for all the OpenGL versions. The interested reader can find the OpenGL specification of version 3.3 (which is what we'll be using) [here](https://www.opengl.org/registry/doc/glspec33.core.20100311.withchanges.pdf) which is a good read if you want to delve into the details of OpenGL (note how they mostly just describe results and not implementations). The specifications also provide a great reference for finding the **exact** workings of its functions.

## Core-profile vs Immediate mode

In the old days, using OpenGL meant developing in <span><mark>immediate mode</mark></span> (also known as the <span><mark>fixed function pipeline</mark></span>) which was an easy-to-use method for drawing graphics. Most of the functionality of OpenGL was hidden in the library and developers did not have much freedom at how OpenGL does its calculations. Developers eventually got hungry for more flexibility and over time the specifications became more flexible; developers gained more control over their graphics. The immediate mode is really easy to use and understand, but it is also extremely inefficient. For that reason the specification started to deprecate immediate mode functionality from version 3.2 and started motivating developers to develop in OpenGL's <span><mark>core-profile</mark></span> mode which is a division of OpenGL's specification that removed all old deprecated functionality.

When using OpenGL's core-profile, OpenGL forces us to use modern practices. Whenever we try to use one of OpenGL's deprecated functions, OpenGL raises an error and stops drawing. The advantage of learning the modern approach is that it is very flexible and efficient, but unfortunately is also more difficult to learn. The immediate mode abstracted quite a lot from the **actual** operations OpenGL performed and while it was easy to learn, it was hard to grasp how OpenGL actually operates. The modern approach requires the developer to truly understand OpenGL and graphics programming and while it is a bit difficult, it allows for much more flexibility, more efficiency and most importantly a much better understanding of graphics programming.

This is also the reason why our tutorials are geared at Core-Profile OpenGL version 3.3. Although it is more difficult, it is greatly worth the effort.

As of today, much higher versions of OpenGL are published (at the time of writing 4.5) at which you might ask: why do I want to learn OpenGL 3.3 when OpenGL 4.5 is out? The answer to that question is relatively simple. All future versions of OpenGL starting from 3.3 basically add extra useful features to OpenGL without changing OpenGL's core mechanics; the newer versions just introduce slightly more efficient or more useful ways to accomplish the same tasks. The result is that all concepts and techniques remain the same over the modern OpenGL versions so it is perfectly valid to learn OpenGL 3.3. Whenever you're ready and/or more experienced you can easily use specific functionality from more recent OpenGL versions.

When using functionality from the most recent version of OpenGL, only the most modern graphics cards will be able to run your application. This is often why most developers generally target lower versions of OpenGL and optionally enable higher version functionality.
{: .alert .alert-warning}

In some tutorials you'll sometimes find more modern features which are noted down as such.

## Extensions

A great feature of OpenGL is its support of extensions. Whenever a graphics company comes up with a new technique or a new large optimization for rendering this is often found in an extension implemented in the drivers. If the hardware an application runs on supports such an extension the developer can use the functionality provided by the extension for more advanced or efficient graphics. This way, a graphics developer can still use these new rendering techniques without having to wait for OpenGL to include the functionality in its future versions, simply by checking if the extension is supported by the graphics card. Often, when an extension is popular or very useful it eventually becomes part of future OpenGL versions.

The developer then has to query whether any of these extensions are available (or use an OpenGL extension library). This allows the developer to do things better or more efficient, based on whether an extension is available:

{% highlight swift %}
if GL_ARB_extension_name != nil
{
    // Do cool new and modern stuff supported by hardware
}
else
{
    // Extension not supported: do it the old way
}
{% endhighlight %}


With OpenGL version 3.3 we rarely need an extension for most techniques, but wherever it is necessary proper instructions are provided.

## State machine

OpenGL is by itself a large state machine: a collection of variables that define how OpenGL should currently operate. The state of OpenGL is commonly referred to as the OpenGL <span><mark>context</mark></span>. When using OpenGL, we often change its state by setting some options, manipulating some buffers and then render using the current context.

Whenever we tell OpenGL that we now want to draw lines instead of triangles for example, we change the state of OpenGL by changing some context variable that sets how OpenGL should draw. As soon as we changed the state by telling OpenGL it should draw lines, the next drawing commands will now draw lines instead of triangles.

When working in OpenGL we will come across several <span><mark>state-changing</mark></span> functions that change the context and several <span><mark>state-using functions</mark></span> that perform some operations based on the current state of OpenGL. As long as you keep in mind that OpenGL is basically one large state machine, most of its functionality will make more sense.

Objects

The OpenGL libraries are written in C and allows for many derivations in other languages, but in its core it remains a C-library. Since many of C's language-constructs do not translate that well to other higher-level languages, OpenGL was developed with several abstractions in mind. One of those abstractions are objects in OpenGL.

An <span><mark>object</mark></span> in OpenGL is a collection of options that represents a subset of OpenGL's state. For example, we could have an object that represents the settings of the drawing window; we could then set its size, how many colors it supports and so on. One could visualize an object as a C-like struct:

{% highlight swift %}
struct ObjectType {
    option1: GLfloat
    option2: GLuint
    name: [GLchar]
}
{% endhighlight %}

**Primitive types**<br/>
Note that when working in OpenGL it is advised to use the primitive types defined by OpenGL. Instead of writing `Float` we use `GLfloat`; the same holds for `Int32`, `UInt32`, `Int8`, `Bool`, etc. OpenGL defines the memory-layout of their GL primitives in a cross-platform manner since some operating systems may have different memory-layouts for their primitive types. Using OpenGL's primitive types helps to ensure that your application works on multiple platforms.
{: .alert .alert-info}

Whenever we want to use OpenGL objects it generally looks something like this:

{% highlight swift %}
// Create object
var objectId: GLuint = 0
glGenObject(1, &objectId)
// Bind object to context
glBindObject(GL_WINDOW_TARGET, objectId)
// Set options of object currently bound to GL_WINDOW_TARGET
glSetObjectOption(GL_WINDOW_TARGET, GL_OPTION_WINDOW_WIDTH, 800)
glSetObjectOption(GL_WINDOW_TARGET, GL_OPTION_WINDOW_HEIGHT, 600)
// Set context target back to default
glBindObject(GL_WINDOW_TARGET, 0)
{% endhighlight %}


This little piece of code is a workflow you'll frequently see when working in OpenGL. We first create an object and store a reference to it as an id (the real object data is stored behind the scenes). Then we bind the object to the target location of the context (the location of the example window object target is defined as `GL_WINDOW_TARGET`{:.kt}). Next we set the window options and finally we un-bind the object by setting the current object id of the window target to 0. The options we set are stored in the object referenced by `objectId`{:.n} and restored as soon as we bind the object back to `GL_WINDOW_TARGET`{:.kt}.

The code samples provided so far are only approximations of how OpenGL operates; throughout the tutorial you will come across enough actual examples.
{: .alert .alert-danger}

The great thing about using these objects is that we can define more than one object in our application, set their options and whenever we start an operation that uses OpenGL's state, we bind the object with our preferred settings. There are objects for example that act as container objects for 3D model data (a house or a character) and whenever we want to draw one of them, we bind the object containing the model data that we want to draw (we first created and set options for these objects). Having several objects allows us to specify many models and whenever we want to draw a specific model, we simply bind the corresponding object before drawing without setting all their options again.

## Let's get started

You now learned a bit about OpenGL as a specification and a library, how OpenGL approximately operates under the hood and a few custom tricks that OpenGL uses. Don't worry if you didn't get all of it; throughout the tutorial we'll walk through each step and you'll see enough examples to really get a grasp of OpenGL.

## Additional resources

 * [opengl.org](https://www.opengl.org/): official website of OpenGL.
 * [OpenGL registry](https://www.opengl.org/registry/): hosts the OpenGL specifications and extensions for all OpenGL versions.
 