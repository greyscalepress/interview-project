# Dave Crossland - Future Type Tools

Interview with Dave Crossland about the floss type design ecosystem, recorded April 30 2014. Conducted for Libre Graphics Magazine, the Type Issue.

on FontForge   
Metapolator   
font bakery  
type testing tool

## FontForge 

So, George Williams started FontForge[^fontforge]. 
From his perspective, it was technically complete. This is similar to the way Inkscape emerged from Sodipodi. The Sodipodi developer, as I understand the story, was very much involved in the technical development of the SVG editor. 
Things which were mathematically interesting for him to develop, but it wasn't really focussed on making a tool for end users.

[^fontforge]: http://fontforge.github.io/
    https://github.com/fontforge/fontforge  
    License: GPLv3+  

**M:** That was the person who developed **Spiro**?

**D:** No, no. Raph Levien, who wrote **Spiro**, initiated the project, the code base that is now most widely recognized as **Inkscape**. 

He made a program called **Gill**, as in Eric Gill, which was the "Gnome Illustration program". Raph also developed a very simple font editor, which I don't think he ever published. This is about fifteen years ago.

So, when Raph moved on, and got into his PhD, I think he was working around this time on his first PhD, which was on *"Attack-Resistant Trust Metrics"*. And he dropped these projects, stopped developing them.

He had a little web browser, called "Delo". 

**Gill**, the SVG editor which he developed, was taken up by Lauris Kaplinski, I believe in Russia, and it was called **Sodipodi**. And then, there was some Americans, who wanted to make the program more user-friendly: key bindings, actually they removed some functionality ... this kind of thing.

A couple of years ago, I was looking on **FontForge** in a similiar light. I was going to start using FontForge to teach type design to beginners. 
It's technically very complete, but for new users, it has a lot of rough edges.

And so, it's not much effort to polish that up. So, similar to Inkscape, we did the key bindings system, so that all of the hotkeys are defined in one simple text file.
The most recent workshop I ran was at a design school in Sweden called (((Hypo))) Island, and obviously most of the students there had swedish keyboards, and so the US keyboard of the FontForge native package wasn't working for them. And so, it was very easy to take minutes, and step the class through shutting down FontForge, opening the MacOSX application bundle, navigating to the text file where the hotkeys are defined, and editing the hotkeys.

## realtime collaboration mode

**M:** At LGM Madrid (2013), you presented that "Fonts of Doom" mode in FontForge.

**D:** There has been a lot of tiny little changes made. We redid the icons on the toolbar. We redid the hotkeys. We fixed a lot of crashes. We added that you could interact with the metrics in a more easy way. I have been fairly shy of actually adding any major features to fontforge.  

This is the irony, everyone's like "Wow, Fontforge is so much better than two years ago." But actually we didn't change anything in the functionality. We just made a lot of little changes to the user interface. 

One of the bigger things is that we packaged it for Mac OSX, and we also packaged it for Windows, although I haven't really been promoting the Windows version yet. So the packaging was kind of a big deal. 

### Realtime collaboration mode

And then, about a year and a half ago, I proposed to add a major feature to Fontforge, to see how that would go. So we added this realtime collaboration feature, which hijacks the undo system, and uses the ZeroMQ library to basically broadcast the undo stack across a network, so that people can have a realtime collaboration experience. If you set it up right, then it works very well. We polished it up a little bit after the LGM 2013, but we didn’t really make it rock solid.

This threw up all kinds of problems, it crashed a lot, it was pretty difficult for Dr Ben Martin to develop. He has a PhD in computer science, and he could do it. But there's very few other people in the world, comparatively, wo can contribute to that codebase. So it's been a bit of a dead end, because if I can raise money, through running workshops or other means, to fund development, then it's ok. But that's relatively difficult to do. Whereas, if it was a web application, then there's millions times more people who have web development skills, and who will also be users of a font editor. Not every user has development skills, but enough users would have those skills, and would be able to contribute directly to the improvement of the editor. 

So I considered, after Madrid, (())
We had a working basic prototype level, so I could the demo on stage, and it basically works. We polished it up a little bit after the LGM last year, but we didn't really make it rock solid. 

After LGM last year, I met Simon Egli. Simon and I had been discussing about that previous **Metaflop** project, which had been developed by some other people in Zurich. I had also done quite a lot of research into Metafont, when I was a student at University of Reading, and I had abandonned my experiment with Metafont, when I was a student, because it was taking too long. I didn't end up with anything practical. 

So, Simon did follow a very similar path. When we met in New York, a year and a half ago, a couple of months before the LGM 2013, we discussed how Metafont could be used in a way which would be more accessible to designers. And from that conversation, Simon came up with the basis for **Metapolator**. And so, I shifted away from Fontforge, in a way, because my attention has been on Metapolator.

**FontForge** is a very capable font outline editor. But it’s focussed at the _letter_ level, or the _word_ level. It doesn’t really provide any functionality for dealing with families. And actually this is very common.

The **Glyphs** font editor, which is a proprietary Mac OSX editor, has some support in it’s user interface, for working on families. But other editors don’t. Fontlab and Robofont. I mean, Robofont obviously copies Emacs' design to be very extensible, so it's difficult to make categorical statements about Robofont. But still. 

So, with FontForge, we had that realtime collaboration feature. If you set it up right, then it works very well. It can crash, but then it has time crash protection. But it's just not pleasant to use. The user inteface of FontForge is difficult to work on. And working on the Fontforge user interface toolkit doesn't just make any sense whatsoever. Because *the web* is the default dominant user interface toolkit for software these days.

> That leads me to the conclusion that we should be writing web based font editors. 

One of the things that we did, at the LGM, and at the *Interactivos* workshop, the week after the LGM in Madrid, was to work on a kind of web interface to FontForge. And the way that this worked in the collaboration mode was that, everytime someone in the collaboration session does something, if the font is in a buildable state, then the font is built, and pushed, using web sockets, to a web page. So that you have a live *web-document preview* of your typeface, as you're developing it.

A problem that a lot of software (both libre and proprietary) has, is that when developers decide to make a rewrite, they often stop development of the old thing and start development of the new thing. And this often frustrates users, because they aren't getting improvements to the version that they're using, and although the new version may have a lot of potential, and maybe some advanced features that wouldn't be possible in the old version, its lacking a lot of the refinements and little features that the users depend on.

Font editors have often been plagued by this, and Fontographer and Fontlab have reached a very dominant market position, where all professionals are depending on them. And then there isn't really any growth in licensing, because all the professionals have licensed it. And so they run out of money for further development. And so the codebase languishes. In Fontographer's case, it was abandoned completely. In Fontlab's case, they have been working for 5 or 6, maybe 8 years, on a total rewrite, and they haven't released anything so far. 

I'm very keen to not see that happen to FontForge. So, the way I see the development proceeding, over this year and next year, is that we are developing *plugins* for FontForge, for additional functionality.

### FontForge Plugins

Making a completely new font editor from scratch has this dilemma that you need all this functionality that is in FontForge, but at the same time, you want the new interface, to do what the new interface can do. To run these things concurrently is ideal.

We started with Lasse Fister’s **iPython**, as a plugin for FontForge, so that you can to interactive scripting development, while running fontforge. 

Then Juraj Sukop has developed **Even**, which is a very simple little Qt IDE, very similar to the classic *NodeBox* or *DrawBot*, where you have a three-paned window, with input, output and display. You can write a Python program in the input area, you can run the program, you can see it's standard output in the tray underneath, and on the left you get a canvas where the program output is drawn. It can be used to produce test document PDFs from within FontForge.

We also added this to the FontForge codebase, as a plugin. So we now have GTK and Qt plugins bundled with FontForge. Therefore, it's possible to develop functionality for FontForge, using either GTK, or Qt, or the web, as your toolkit.

What I would like to see, over the next year or two, is to replace the FontForge user interface by web or Qt or GTK plugins. 

My preference is the web as a toolkit. 

Currently, various web based font editors are being developed. There's *Glyphr Studio*[^glyphr], which is developed by Matt LaGrandeur, a UX designer and developer who works at Microsoft. *Glyphr Studio* is a classic font editor, based very much on the TrueType spec. Even if it has some nice features. 

[^glyphr]: https://github.com/mattlag/Glyphr-Studio/  
    http://glyphrstudio.com/  
    License: GPLv3

Then there is *Prototypo*[^prototypo], which has been running a successful kickstarter in May 2014. The basic idea of Protoypo, as I see it, is to apply Mustache style templating to SVG fonts. 

[^prototypo]: https://github.com/byte-foundry/prototypo/  
    http://www.prototypo.io/  
    License: GPLv3

**MS:** Which means?

**DC:** In web developement, there's been hundreds of templating syntaxes developed over the last years. The one which has really come to dominate is called Mustache. There's lot of derivatives of the Mustache syntax. Liquid Templates is also quite popular.

Prototypo is putting that kind of templating together with SVG. So you can have a SVG path syntax, and the point positions, the X and Y positions on an SVG path, rather than being defined literally as integer values, are defined through a templating syntax. That gives you an algebra-equation power of specifying point positions, parametrically.

This being web based, it's a self contained *node.js* application. What I am interested in doing, is making that kind of thing possible to turn into a FontForge plugin. So that you would be able to click "export" in the web app, and then have that immediately appear in FontForge.

**Metapolator** is in a very similar position to this. Simon Egli has done quite a lot of research into Metafont, how Metafont could be used in a way which would be more accessible to designers. Metapolator imports and exports UFO fonts, so it can fit into any UFO-based workflow. It has a parser, which parses UFO into Metafont, and allows you to store Metafont parameters and values in the UFO format. This means that you can "round trip" fonts in and out of Metapolator, into any UFO tool.

Metapolator is a font family design tool. It's not about drawing the masters - that would be done in FontForge, or any other UFO editor. Metapolator is about multiplying those masters into families. It's very much a type designer's tool, same as Prototypo and Glyphr Studio. 

Another big thing we have been working on since LGM 2013: the UFO support in FontForge. 

**MS:** Is this working now in FontForge?

**DC:** It's working a lot better than it used to. And we started to implement UFO version 3, which at the moment still isn't supported by any other font editors. We will see how that goes. 

((question about the funding)) 

In the work that I have been doing with Google Fonts, we have a lot of single style families, that it needs to expand into full families. I have been able to suggest to Google to give Simon and the other Metapolator developers financial support, in order to solve that problem for Google. 

And I believe that the best way to fund free software is to align institution needs with user's needs. 

**MS:** when at LGM 2014, you pointed out the similarities..

**DC:** The basic idea of a font directory is that you have specimen cards for each card. And similarly, in **Metaflop**, which is kind of a Metapolator version one, you also have these three cards, where a glyph palette is showing all letters, then there's another card with one letter scaled up very big, and there's a third card where you can have a couple of lines of text.

This is conceptually very similar: you have this main staging area, showing type, to the left you have the sidebar with sliders. The Prototypo user interface is also very much like this: there's a sidebar with sliders, then you have the main stage area, with different views of type at various scales. 

And these tools are all very much focused on the type designer. There's a couple of other tools that I have been interested in, which are for different kinds of users. For myself, as a kind of curator of the Google Fonts library, I am hopeful for a couple of tools to validate the technical quality of the fonts, and manage the process of making updates - this is the **Font Bakery[^bakery]**  tool. And then I'm also interested in validating the *design quality* of the  typefaces, not just the technical quality. 

[^bakery]: License: Apache 2.0 License  
    https://github.com/googlefonts/fontbakery

Pablo Impallari has been developing a testing tool, that he uses doing his type design developement. I would love to ramp that up. So I have been discussing the possiblity, working with various foundries, taking the knowledge of how they test type, and bring this together in a kind of Master Type Testing page, or rather testing application. 

And again, you are having little cards, there is typography on each card, where instead of sliders to change the type rendered in the card, you have a sidebar with questions. When you have a typeface, and want to put it through it's paces, then you have dozens or hundreds of test cases, that allow to evaluate various aspects of the typeface. 

**MS:** this is the thing a designer will do, before he submits the font?

**DC:** They can be used as a part of the type design process. There are different kinds of users. Someone who manages a collection of hundreds of fonts, is different of someone who is trying to originate a new design.

**MS:** **TTFautohint** - this has now reached a stable version number?

**DC:** Yes, that's right. Werner Lemberg has been doing a great job during the last few years. He is probably the leading example of somebody working on libre font tools who has been able to sustain it financially. I made a little video for him when we started the project, for the initial fundraising, a campaign that was run on Pledgie. We managed to find funding from Fontlab, Extensis, Webink, the Android project, the Google Fonts project, and also hundreds of individuals. 

That has been working very well, it's now the point when you can design with ((TTFautohint)) to be able to hint as part of your development process from day one. So that you can draw a glyph, and TTFautohint it, and preview how that's rendering in browsers. And by integrating TTFautohint in your design process, you can produce designs which render extremely well on legacy windows platforms, without needing to do any hinting. 

**MS:** is this integrated into existing design software?

**DC:** There is a very simple graphical user interface to TTFAutohint. You can load a font file, and check the boxes with the options, rather than reading a manual. I would expect all these programs to integrate TTFauthint , build process, options.

And one of the things I am very excited about in technology is Enscripten, and (())dot js. So, Enscripten is transpiler, that allows you to take a C or C++, or even Python, or another scripting language program, and it allows you to compile it into Javascript. And specifically, (()) Javascript, which has been highly optimized in Firefox and in a few other browsers. This allows is to take a lot of existing free software, and run it in the browser. It should be possible to take TTFAutohint, and have that hinting process done as part of a web application.

**MS:** as part of Metapolator, or whatever?

Obviously with FontForge, since FontForge is a binary application, this isn't totally necessary. But what I would like to see, over the next year or two, is to replace the FontForge user interface by web or Qt or TTK plugins. I'm kind of agnostic to whatever wins out, personally I'd be betting on the web stack. But if people jump in, develop Qt or TTK functionality, then that sounds great to me.

**MS:** There was one last thing: **Kernagic**. What's happening with that?

**DC:** So, **Kernagic** (pronouced ‘Kemagic’) is a project by Pippin (Øyvind Kolås). He has pretty much come to the point where he's happy with it. It is very much an intellectual exercise to him, as a kind of hacker nomad, who was trying at the LGM 2013 in Madrid to crack at the spacing. Here we are a year later, and he has done an amazing job. 

Kernagic has two modes. It has the *table of cadences*, from Frank E. Blokland’s letter model. And then it got Pippin's own independent thinking, which was informed by Frank's model, but is an independent perspective on the whole problem. 

Pippin's gone forward with fonts now, he has also done **Fontile**, which is his "puzzle style interface" for creating pixel fonts. It's pretty amazing stuff really, you see a lot of functionality, in Fontile, which you only see in major web applications, and it's something that he was able to put together in a couple of months. 

**Kernagic** is a C application, it's TTK2, so it's not that easy to package for Windows or Mac OSX. So the best way to use Kernagic is to run it on a GNU system. And obviously, most type designers are using Mac OSX, so it's got a somewhat limited audience. But the results that designers, like Vernon Adams, achieved with Kernagic are very compelling.

**MS:** so, Kernagic is an independent application? 

**DC:** Yes, it's a standalone TTK application. It uses UFO for input and output, and it follows the UFO live-file-system-watcher model, so that you have one UFO file, and you can open that in several UFO applications at the same time. And when you click the "save" button in one of the applications, the other applications are watching the file system, and allow you to select how you want to take the update. So it doesn't really make sense to have Kernagic as a FontForge plugin, because it is cooperating with FontForge by the file system.  

Something that underpins all of this is: all of these project are developed on Git version control, and almost all of them are developed on GitHub. So, becoming familiar with Git and GitHub is essential for designers, especially type designers -  because that's really the dominant collaboration channel of today.

((Payment model of FontForge))

As I said, we packaged a Windows native build of FontForge, which runs pretty good. And the Ardour audio editor has been quite successfully working to provide a "pay libre software" model, where users are asked to pay for a copy, or to buy a subscription, so that they get updates on an annual subscription basis. I'm very keen on this idea, because I think that freedom is valuable, and we live in a capitalist system where people pay for valuable things. So I think that free software should be more expensive than proprietary software - because it's more valuable.

I definitely think that not enough free software developers are funded to work on it full time, and that's a major stumbling block for the free software movement.

((Q: how is the decision taking done in FontForge)) 

Only a couple of people had commit access on Sourceforge. Somebody brough FontForge over to Github. Then we set up FontForge as a GitHub organization. And there's 35 members in the organization right now. But only a few of them are really active contributors. 



**************