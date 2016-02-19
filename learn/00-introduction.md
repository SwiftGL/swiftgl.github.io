---
layout: default
---
# Introduction

Since you came here you probably want to learn the inner workings of computer graphics and do all the stuff the cool kids do by yourself. Doing things by yourself is extremely fun and resourceful and gives you a great understanding of graphics programming. However, there are a few items that need to be taken into consideration before starting your journey.

## Prerequisites

Since OpenGL is a graphics API and not a platform of its own, it requires a language to operate in and the language of choice is Swift, therefore some knowledge of the Swift programming language is required for these tutorials. However, I will try to explain most of the concepts used, including advanced Swift topics where required so it is not required to be an expert in Swift, but you should be able to write more than just a 'Hello World' program.

Also, we will be using some math (linear algebra, geometry and trigonometry) along the way and I will try to explain all the required concepts of the math required. However, I'm not a mathematician by heart so even though my explanations might be easy to understand, they will most likely be incomplete. So where necessary I will provide pointers to good resources that explain the material in a more complete fashion. Do not be scared about the mathematical knowledge required before starting your journey into OpenGL; almost all the concepts can be understood with a basic mathematical background and I will try to keep the mathematics to a minimum where possible. Most of the functionality does not even require you to understand all the math as long as you know how to use it.

## Structure

Learn SwiftGL is broken down into a number of general subjects. Each subject contains several sections that each explain different concepts in large detail. Each of the subjects can be found at the menu to your left. The subjects are taught in a linear fashion (so it is advised to start from the top to the bottom, unless otherwise instructed) where each page explains the background theory and the practical aspects.

To make the tutorials easier to follow and give them some added structure the site contains boxes, code blocks, and color hints.

## Boxes

**Blue** boxes encompasses some notes or useful features/hints about the subject at hand.
{: .alert .alert-info}

**Red** boxes will contain warnings or other features you have to be extra careful with.
{: .alert .alert-danger}

## Code

You will find plenty of small pieces of code in the website that are located in boxes with syntax-highlighted code as you can see below:

{% highlight swift linenos %}
// This box contains code
print("Hello World")
{% endhighlight %}

Since these provide only snippets of code, wherever necessary I will provide a link to the entire source code required for a given subject.

## Color hints

Some words are displayed with a different color to make it extra clear these words portray a special meaning:

 * <span><mark>Definition</mark></span>: highlighted words specify a definition i.e. an important aspect/name of something you're likely to hear more often.
 * `Program logic`{:.red}: red words specify function names or class names.
 * `Variables`{:.blue}: blue words specify variables including all OpenGL constants.

Now that you got a bit of a feel of the structure of the site, hop over to the Getting Started section to start your journey in SwiftGL.
