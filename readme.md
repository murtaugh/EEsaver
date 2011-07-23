<<<<<<< HEAD
## EEsaver: The Basic Idea

EEsaver is a starting point for building ExpressionEngine-powered Treesaver sites. [We love EE](http://monkeydo.biz/), and we think that its highly-customizable nature (not to mention its low price) makes it an ideal system for delivering the long-form, magazine-style content Treesaver was designed to publish.

What we've put together is a free set of ExpressionEngine templates, plus instructions for configuring EE to make them work. Drop in some content and you've got the beginnings of your own cross-platform magazine.

### Treesaver?

In a nutshell, [Treesaver](http://treesaver.net/) is a JavaScript framework for creating magazine-style layouts using standards-compliant HTML and CSS. You should go read about it; it has a ton of features.

## The Demo

Starting with the open-source [Treesaver.js](http://treesaverjs.com/) files (and adding a few bits and pieces of markup from our own [HTML5 Reset](http://html5reset.org/)) we've developed a simple set of requirements for integrating Treesaver and EE.

We then had a little fun (thanks to [Google Books](http://books.google.com/books?id=EfEvAAAAMAAJ&pg=PP1#v=onepage&q&f=false)) and dug out some public-domain content from some of the very earliest issues of Harper's Magazine.

### Harper's Magazine, Volume 9 (published 1854)

(Do some window resizing to see Treesaver's responsiveness in action.)

* [Cover](http://eesaver.monkeydo.biz/harpers/volume-9/)
* [Table of Contents](http://eesaver.monkeydo.biz/harpers/toc/volume-9)
* [Behind the Louvre](http://eesaver.monkeydo.biz/harpers/article/volume-9/behind-the-louvre)
* [The Holy Week at Rome](http://eesaver.monkeydo.biz/harpers/article/volume-9/the-holy-week-at-rome)
* [A Few Words About Birds](http://eesaver.monkeydo.biz/harpers/article/volume-9/a-few-words-about-birds)
* [The Last Moments of Beethoven](http://eesaver.monkeydo.biz/harpers/article/volume-9/the-last-moments-of-beethoven) This is actually a really neat little story. (Completely apocryphal we assume…)

## The Set Up

<i>Note: These instructions assume a decent level of familiarity with ExpressionEngine and how it works. If you'd like to learn more about EE, pay a visit to the official documentation.</i>

<i>Also note: We have deliberately not made use of any Expression Engine add-ons, even free ones. We wanted a setup that would work with EE right out of the box.</i>

Since what Treesaver creates is sort of a metaphorical magazine, let's extend that metaphor to explain how we're using ExpressionEngine for EEsaver:

* The installation of Expression Engine is the <b>magazine</b>.
* Channels within Expression Engine are the <b>issues</b>.
* Individual entries within channels are the <b>articles</b>.

There are other ways to do it (using categories as issues for example), but this works for us.

### Before Starting: Install ExpressionEngine and the Treesaver Assets

Once you have Expression Engine installed (no special changes to the normal set up procedures are required), you can move on to...

### Step One: Set up a channel.

This is easy, which is good considering we will be creating a new channel each time we release a new issue of our magazine.

First, set the General Preferences:

<img src="http://eesaver.monkeydo.biz/-/img/screenshots/channel-prefs-1.gif" alt="" />

* <b>Full Channel Name</b>: Harper's Magazine, Volume 9 (the name of the issue)
* <b>Channel Name</b>: harpers-9 (EE will use this as the URL trigger for the issue)
* <b>Channel Description</b>: This is optional, but we're using it to populate meta tags.

Next, set the Channel Posting Preferences:

<img src="http://eesaver.monkeydo.biz/-/img/screenshots/channel-prefs-2.gif" alt="" />

* We need to be able to put whatever HTML tags we want into our articles
* We also don't want EE to turn any URL into a link. (It baffles us that EE still does this by default.)

Feel free to do other things, but these settings are all we need right now.

### Step Two: Custom Fields

This can get as complicated as you want it to once you've gotten the hang of Treesaver, but we've kept it very simple:

<img src="http://eesaver.monkeydo.biz/-/img/screenshots/custom-fields.gif" alt="" />

* <b>Excerpt</b>: Again, this is optional, and we're using it for meta tags.
* <b>Content</b>: The full text of your article. No pagination is required; Treesaver handles that.
* <b>Spillover Content</b>: This is very optional. Even though ExpressionEngine does not set a character limit for textareas, MySQL does. That limit is about 65,000 characters, which is slightly less than some of our sample Sherlock Holmes stories, so we added this field to hold any text that spills over.
* <b>Figures</b>: This is where you will put any images, videos, etc. Technically, there's no reason you can't just put these in the Content field with the text of your article, but since Treesaver places images how it likes based on the layout it renders (more on this later), it makes more editorial sense to split them out.

A note on markup: You don't want to let ExpressionEngine do your text formatting for you. EE's formatting options (either "Auto <br />" or "XHTML" don't play well with some of the HTML5 tags you'll probably need to use (like `figure`). Until a better parser comes along, set all your fields' Default Text Formatting to None (the default is "XHTML"), and add `p` tags to your content fields by hand.

### Step Three: Templates

<img src="http://eesaver.monkeydo.biz/-/img/screenshots/templates.gif" alt="" />

* <b>article</b>: A single article page.
* <b>index</b>: This is our cover page. It pulls its content from a Global Variable (more on this in a moment).
* <b>resources</b>: This is the heart of the operation; Treesaver looks at this file to determine how we want our pages to be assembled. (For more on this, visit the [TreesaverJS wiki](https://github.com/Treesaver/treesaver/wiki).)
* <b>toc</b>: The Table of Contents.

All our templates are set to be of the type "Web Page," since they all have ExpressionEngine tags in them.

The name of the template group is essentially whatever we want to show up in our URLs; here it's the name of our magazine. If our domain name were already the name of our magazine, we'd probably name the group issues or something.

### Step Four: Snippets

We have two Snippets (accessed through the Template Manager); one is un-important, the other is quite important.

<img src="http://eesaver.monkeydo.biz/-/img/screenshots/snippets.gif" alt="" />

* <b>analytics-id</b>: (optional) If this exists and contains your site's Google Analytics UID, the templates will automatically include the javascript that calls Google Analytics, as well as some extra scripting provided by Treesaver that passes article change events, allowing us to track them as page views.
* <b>cover-volume-9</b>: This holds the contents of our cover page. Since each issue of our magazine will need its own cover, we will need to create a new Snippet for each new issue. As I'm sure you've sussed out, the Snippet's name needs to match the "Channel Name" of that issue's channel, preceded by "cover-".

Please note: Currently the templates *require* that a cover Snippet exists for each issue.

### Notes on Images/Figures

Putting images into articles is one of the more counter-intuitive aspects of working with Treesaver. In order to achieve a fully flexible and responsive layout engine, it's often not possible to ensure that an image is adjacent to a related piece of text.

Let's look at a sample figure from our Harper's demo and break down the important bits:

	<figure>
		<img data-sizes="single" src="/-/img/rome/rome-1-280.jpg" width="280" height="244" alt="">
		<img data-sizes="double" data-src="/-/img/rome/rome-1-600.jpg" width="600" height="429" alt="">
	</figure>

* <b>Multiple images</b>: There are two image tags here, one for large layouts and one for small ones. The small one is called first, but if the layout engine determines that the viewport is large enough to accommodate the larger version, it will swap it in.
* <b>data-sizes</b>: This data attribute tells Treesaver how many columns this image is allowed to take up.
* <b>src / data-src</b>: These attributes are where the system looks for the URI of an image. We use the data-src attribute for the images we don't want the system to load unless it determines it can accommodate them, e.g. large ones.

In the EEsaver templates, we've set it up so that images are only shown on every other page of an article. This is our way of preventing images from clumping up at the beginning of an article, leaving later pages image-free. You can edit the resources template to re-configure this scheme as you see fit.

## And there you have it.

Treesaver is a really interesting beast with a lot of potential. There's a lot that can be done with it once you learn how to manipulate it.

One of the most important things to understand is that Treesaver doesn't allow for traditional approaches to page layout. Based on viewport size and other considerations, the framework lays out each article as it understands the constraints set up in the stylesheet and the resources template.

As a framework it's still brand new and not fully documented. We encourage you to [give the wiki](https://github.com/Treesaver/treesaver/wiki) a good read, as well as taking a close look at the [examples on the TreesaverJS site](http://treesaverjs.com/) before getting started. (Look and learn, but the designs aren't open source...)

The CSS and images that we've released via GitHub are free. We hope we've made getting started a little easier (actually we hope we've made it *very* easy), and we hope to see some new Treesaver sites very soon!
=======
# EEsaver: The Basic Idea

EEsaver is a starting point for building ExpressionEngine-powered Treesaver sites. [We love EE](http://monkeydo.biz/), and we think that its highly-customizable nature (not to mention its low price) makes it an ideal system for delivering the long-form, magazine-style content Treesaver was designed to publish.

What we've put together is a free set of ExpressionEngine templates, plus instructions for configuring EE to make them work. Drop in some content and you've got the beginnings of your own cross-platform magazine.

## Treesaver?

In a nutshell, [Treesaver](http://treesaver.net/) is a JavaScript framework for creating magazine-style layouts using standards-compliant HTML and CSS. You should go read about it; it has a ton of features.

# The Demo

Starting with the open-source [Treesaver.js](http://treesaverjs.com/) files (and adding a few bits and pieces of markup from our own [HTML5 Reset](http://html5reset.org/)) we've developed a simple set of requirements for integrating Treesaver and EE.

We then had a little fun (thanks to [Google Books](http://books.google.com/books?id=EfEvAAAAMAAJ&pg=PP1#v=onepage&q&f=false)) and dug out some public-domain content from some of the very earliest issues of Harper's Magazine.

## Harper's Magazine, Volume 9 (published 1854)

(Do some window resizing to see Treesaver's responsiveness in action.)

* [Cover](http://eesaver.monkeydo.biz/harpers/volume-9/)
* [Table of Contents](http://eesaver.monkeydo.biz/harpers/toc/volume-9)
* [Behind the Louvre](http://eesaver.monkeydo.biz/harpers/article/volume-9/behind-the-louvre)
* [The Holy Week at Rome](http://eesaver.monkeydo.biz/harpers/article/volume-9/the-holy-week-at-rome)
* [A Few Words About Birds](http://eesaver.monkeydo.biz/harpers/article/volume-9/a-few-words-about-birds)
* [The Last Moments of Beethoven](http://eesaver.monkeydo.biz/harpers/article/volume-9/the-last-moments-of-beethoven) This is actually a really neat little story. (Completely apocryphal we assume…)

# The Set Up

<i>Note: These instructions assume a decent level of familiarity with ExpressionEngine and how it works. If you'd like to learn more about EE, pay a visit to the official documentation.</i>

<i>Also note: We have deliberately not made use of any Expression Engine add-ons, even free ones. We wanted a setup that would work with EE right out of the box.</i>

Since what Treesaver creates is sort of a metaphorical magazine, let's extend that metaphor to explain how we're using ExpressionEngine for EEsaver:

* The installation of Expression Engine is the <b>magazine</b>.
* Channels within Expression Engine are the <b>issues</b>.
* Individual entries within channels are the <b>articles</b>.

There are other ways to do it (using categories as issues for example), but this works for us.

## Before Starting: Install ExpressionEngine and the Treesaver Assets

Once you have Expression Engine installed (no special changes to the normal set up procedures are required), you can move on to...

## Step One: Set up a channel.

This is easy, which is good considering we will be creating a new channel each time we release a new issue of our magazine.

First, set the General Preferences:

<img src="http://eesaver.monkeydo.biz/-/img/screenshots/channel-prefs-1.gif" alt="" />

* <b>Full Channel Name</b>: Harper's Magazine, Volume 9 (the name of the issue)
* <b>Channel Name</b>: harpers-9 (EE will use this as the URL trigger for the issue)
* <b>Channel Description</b>: This is optional, but we're using it to populate meta tags.

Next, set the Channel Posting Preferences:

<img src="http://eesaver.monkeydo.biz/-/img/screenshots/channel-prefs-2.gif" alt="" />

* We need to be able to put whatever HTML tags we want into our articles
* We also don't want EE to turn any URL into a link. (It baffles us that EE still does this by default.)

Feel free to do other things, but these settings are all we need right now.

## Step Two: Custom Fields

This can get as complicated as you want it to once you've gotten the hang of Treesaver, but we've kept it very simple:

<img src="http://eesaver.monkeydo.biz/-/img/screenshots/custom-fields.gif" alt="" />

* <b>Excerpt</b>: Again, this is optional, and we're using it for meta tags.
* <b>Content</b>: The full text of your article. No pagination is required; Treesaver handles that.
* <b>Spillover Content</b>: This is very optional. Even though ExpressionEngine does not set a character limit for textareas, MySQL does. That limit is about 65,000 characters, which is slightly less than some of our sample Sherlock Holmes stories, so we added this field to hold any text that spills over.
* <b>Figures</b>: This is where you will put any images, videos, etc. Technically, there's no reason you can't just put these in the Content field with the text of your article, but since Treesaver places images how it likes based on the layout it renders (more on this later), it makes more editorial sense to split them out.

A note on markup: You don't want to let ExpressionEngine do your text formatting for you. EE's formatting options (either "Auto <br />" or "XHTML" don't play well with some of the HTML5 tags you'll probably need to use (like `figure`). Until a better parser comes along, set all your fields' Default Text Formatting to None (the default is "XHTML"), and add `p` tags to your content fields by hand.

## Step Three: Templates

<img src="http://eesaver.monkeydo.biz/-/img/screenshots/templates.gif" alt="" />

* <b>article</b>: A single article page.
* <b>index</b>: This is our cover page. It pulls its content from a Global Variable (more on this in a moment).
* <b>resources</b>: This is the heart of the operation; Treesaver looks at this file to determine how we want our pages to be assembled. (For more on this, visit the [TreesaverJS wiki](https://github.com/Treesaver/treesaver/wiki).)
* <b>toc</b>: The Table of Contents.

All our templates are set to be of the type "Web Page," since they all have ExpressionEngine tags in them.

The name of the template group is essentially whatever we want to show up in our URLs; here it's the name of our magazine. If our domain name were already the name of our magazine, we'd probably name the group issues or something.

## Step Four: Snippets

We have two Snippets (accessed through the Template Manager); one is un-important, the other is quite important.

<img src="http://eesaver.monkeydo.biz/-/img/screenshots/snippets.gif" alt="" />

* <b>analytics-id</b>: (optional) If this exists and contains your site's Google Analytics UID, the templates will automatically include the javascript that calls Google Analytics, as well as some extra scripting provided by Treesaver that passes article change events, allowing us to track them as page views.
* <b>cover-volume-9</b>: This holds the contents of our cover page. Since each issue of our magazine will need its own cover, we will need to create a new Snippet for each new issue. As I'm sure you've sussed out, the Snippet's name needs to match the "Channel Name" of that issue's channel, preceded by "cover-".

Please note: Currently the templates *require* that a cover Snippet exists for each issue.

## Notes on Images/Figures

Putting images into articles is one of the more counter-intuitive aspects of working with Treesaver. In order to achieve a fully flexible and responsive layout engine, it's often not possible to ensure that an image is adjacent to a related piece of text.

Let's look at a sample figure from our Harper's demo and break down the important bits:

<pre><code><figure>
	<img data-sizes="single" src="/-/img/rome/rome-1-280.jpg" width="280" height="244" alt="">
	<img data-sizes="double" data-src="/-/img/rome/rome-1-600.jpg" width="600" height="429" alt="">
</figure></code></pre>

* <b>Multiple images</b>: There are two image tags here, one for large layouts and one for small ones. The small one is called first, but if the layout engine determines that the viewport is large enough to accommodate the larger version, it will swap it in.
* <b>data-sizes</b>: This data attribute tells Treesaver how many columns this image is allowed to take up.
* <b>src / data-src</b>: These attributes are where the system looks for the URI of an image. We use the data-src attribute for the images we don't want the system to load unless it determines it can accommodate them, e.g. large ones.

In the EEsaver templates, we've set it up so that images are only shown on every other page of an article. This is our way of preventing images from clumping up at the beginning of an article, leaving later pages image-free. You can edit the resources template to re-configure this scheme as you see fit.

## And there you have it.

Treesaver is a really interesting beast with a lot of potential. There's a lot that can be done with it once you learn how to manipulate it.

One of the most important things to understand is that Treesaver doesn't allow for traditional approaches to page layout. Based on viewport size and other considerations, the framework lays out each article as it understands the constraints set up in the stylesheet and the resources template.

As a framework it's still brand new and not fully documented. We encourage you to [give the wiki](https://github.com/Treesaver/treesaver/wiki) a good read, as well as taking a close look at the [examples on the TreesaverJS site](http://treesaverjs.com/) before getting started. (Look and learn, but the designs aren't open source...)

The CSS and images that we've released via GitHub are free. We hope we've made getting started a little easier (actually we hope we've made it *very* easy), and we hope to see some new Treesaver sites very soon!

>>>>>>> Approaching release.

