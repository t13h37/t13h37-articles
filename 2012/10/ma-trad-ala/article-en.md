# Learning to Love the Boring Bits of CSS

The future of CSS gives us much to be excited about: On the one hand, there’s a whole range of new methods that are going to revolutionize the way we lay out pages on the web; on the other, there’s a new set of graphical effects that will allow on-the-fly filters and shaders. People love this stuff. Magazines and blogs are full of articles about them.

But if these tools are the show ponies of CSS, then I think it’s time we gave some love to the carthorses: the nuts-and-bolts components of the language, like selectors, units, and functions. I often call these the boring bits, although I say that only with great affection—an affection I think you should share.

To see why, let’s take a quick walk through some of the best of the new boring bits in CSS—the bits being worked on in half-lit laboratories away from the brilliance of the shiny new things in the shop windows. Some of these boring bits have been around for a while but deserve more recognition, while others are just starting to appear in browsers. But they’ll all be revolutionary to the way we work—albeit in humble, unassuming ways.

Relative size units
It’s likely that, as the smart and forward-thinking developer you are, you’ve worked with relative sizing—that is, em units or percentages—so you’ll know this problem: having to use a calculator to work out sizes because of inheritance. For example, it’s pretty common nowadays to set a base font size for your document and then use relative sizing to set your fonts across the rest of the page. In CSS, that probably looks something like this:

html { font-size: 10px; }
p { font-size: 1.4em; }
This is fine, and not a problem at all, until you have a child element you want to set at a different font size. For example, in markup like this:

The cat sat on the <span>mat</span>.
If you want that span to be at a smaller font size, say 1.2em, what do you have to do? Get your calculator out and work out 1.2 divided by 1.4, resulting in this:

p span { font-size: 0.85714em; }
And the problem’s not limited to using em either. If you’re building a fluid site using percentages, you’ll know that the percentage is relative to its container; so if you have an element that you want to be 40 percent of its parent, the length of which is 75 percent, then the width of the element must be set to 53.33333 percent.

Not ideal.

Root-relative lengths
To combat this font-sizing problem, we now have access to the rem (root em) unit. This is still a relative unit, but it’s always relative to a fixed base value, which is the font size of the root element of the document (in HTML, that’s always the html element). Presuming the same root font size of 10px that we used in the preceding example, the CSS rules required for the case at hand are:

p { font-size: 1.4rem; }
p span { font-size: 1.2rem; }
Now both rules are relative to the root font size, which is much more elegant and easy to work with, especially if you have a simple base like 10px or 12px. It’s sort of like going back to using px values again, only scalable.

This is one of the better-supported features in this article; it’s in all modern browsers including IE9, and only absent in Opera Mobile.

Viewport-relative lengths
If you think the rem unit is cool (I do), you’ll be delighted to know there’s also a new set of length units to combat the percentages problem. These work in a similar way to rem, except that they’re relative not to a user-defined value on the document root, but to the dimensions of the device viewport itself.

The two main units are vh and vw, which are relative to the height and width (respectively) of the viewport. Each takes a number as a value, and that number is equal to the same percentage of the specified length. As I still remember the lessons of screenwriting school, let me show that rather than trying to tell it:

div { height: 50vh; }
In this example, the height of the div would be exactly half of the height of the viewport; 1vh = 1 percent of the viewport height, so it stands to reason that 50vh = 50 percent of the viewport height.

As the viewport size changes, so does the value of the unit—but the advantage of this over percentages is that you don’t have to worry about containing elements: an item with a value of 10vw will always be that wide regardless of the width of its parent.

There’s also a vmin unit, which is equal to the smallest of either vh or vw, and it was recently announced that a corresponding vmax unit would be added to the spec (although it hasn’t been at the time of writing).

As of right now these are in IE9+, Chrome, and Safari 6.

Calculated values
When you’re working fluidly and/or responsively, you’ll doubtless come across the problem of mixing units—wanting to have a grid that’s sized in percentages but with fixed margins. For example:

div {
  margin: 0 20px;
  width: 33%; 
}
If your layout only uses padding and border, then you can use box-sizing to help you get around that, but it won’t help you with margins. A better, more flexible approach is to use the calc() value function, which lets you perform mathematical operations with different units, such as:

div {
  margin: 0 20px;
  width: calc(33% - 40px);
}
You’re not limited to using it only on width; you can use it anywhere length values are permitted—and if you want to go really deep down the rabbit hole, you can also use calc() inside calc().

IE9+ has this unprefixed (!), Firefox has it with the -moz- prefix (which should be unprefixed in release 16 or 17), and Chrome and Safari have implemented it with the -webkit- prefix. It doesn't seem to be in mobile WebKit yet, however.

Load a subset of characters
Snappy performance has always been important, but the broad range of mobile devices on the market now—each bringing great variability and uncertainty in connection speed—makes it perhaps even more so. One way to speed up page loading is to keep external file sizes down, which makes a new property for @font-face that aids in doing just that a very welcome addition.

The property in question is unicode-range, and it takes as a value a range of unicode character references. When pulling in external assets, only those specified characters are loaded from the font file, instead of the complete set. This code demonstrates how to load only three characters from the file foo.ttf:

@font-face {
  font-family: foo;
  src: url('foo.ttf');
  unicode-range: U+31-33;
}
This is especially useful if you’re using font icons and only want to show a subset on a given page. In one test I ran, using unicode-range shaved an average 0.85 seconds from the loading time of a font file, which is not insubstantial. Of course, your own mileage may vary.

This property is currently implemented in IE9+ and WebKit browsers like Chrome and Safari.

New pseudo-classes
Units and values are all well and good, but it’s selectors and pseudo-classes that I get particularly excited about. Coming up with a clever selector pattern, even though it’s hidden away where only a hardy few may ever see it, makes me feel like a craftsman. To paraphrase Steve Jobs’ father: you should make the back of the fence look as good as the front even if no one else knows you’ve done it—because you’ll know.

When I first used :nth-of-type() it was a revelation, like I had kicked down the doors of perception. OK, I’m exaggerating a little. But there are a couple of new CSS pseudo-classes that are really worth getting enthused about.

The negation pseudo-class
You probably won’t realize quite how useful the :not() pseudo-class is until you try it. The argument provided to :not() is a simple selector—no compounds. When a list of subjects is being made by a selector that includes :not(), any elements matching the argument will be excluded from that list. I know, that sounds complicated to me, too. But it’s actually quite simple.

Imagine this: you have an item list and you want to apply a rule to all its odd-numbered items, but never the last one in the list. At the moment you’d have to do something like this:

li { color: #00F; }
li:nth-child(odd) { color: #F00; }
li:last-child { color: #00F; } 
With the negation pseudo-class you can exclude the last item from the rule using :last-child as the argument, thus reducing the number of rules by one and making the code a little easier to manage:

li { color: #00F; }
li:nth-child(odd):not(:last-child) { color: #F00; }
It’s nothing groundbreaking, and as I’ve shown already you can work without it—but it’s quite useful. I had the opportunity to use it on a project built with embedded WebKit, and it proved its worth consistently. It’s honestly one of my favorite pseudo-classes.

That’s right, I have favorite pseudo-classes.

This is the most widely implemented of all the features in this article; it’s in IE9+ and all modern browsers, unprefixed. And if you’re familiar with jQuery, you may already be used to using this—it’s been in there since version 1.0, along with the similar not() method.

The matches-any pseudo-class
The :matches() pseudo-class accepts as an argument a simple selector, a compound selector, a comma separated list, or any combination of those items. Great! But what does it do?

It’s most useful for cutting the cruft of multiple selectors. As a use case, imagine you have a bunch of p elements in different containers but you only want to select a few of them; perhaps the style rule you write would look something like this:

.home header p,
.home footer p,
.home aside p {
  color: #F00;
}
With :matches(), you can shorten that considerably by finding the commonalities in the selectors; in our example here all have .home at the start and end in p, so we can use :matches() to aggregate all of the elements in between those. Confusing? Here’s what it looks like:

.home :matches(header,footer,aside) p { color: #F00; }
This is actually part of CSS4 (CSS Selectors Level 4, to be precise), and in the same spec it mentions that you’ll also be able to use the same syntax—comma-separated compound selectors—in future versions of :not(). Exciting!

Today, :matches() is in Chrome and Safari with the -webkit- prefix, and in Firefox under its old name, :any(), with the -moz- prefix.

Do you love the carthorse yet?
The best thing about all the new features in this article is that they solve real-world problems, from the small but annoying repetition of selectors to the new and ongoing challenges of building high-performance responsive sites. In fact, I can imagine using every single one of these features on a regular basis.

New features like filters may have higher visibility, but you’re far more likely to find the ones presented here useful on every one of your builds.

Each of them will make your professional life a little easier while expanding the possibility space of what you can achieve—and there’s nothing boring about that. 