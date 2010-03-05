http://css-tricks.com/eliminate-jumps-in-horizontal-centering-by-forcing-a-scroll-bar/



You are likely aware of the page-centering technique of adding auto left and right margins to an outer div:

#page-wrap {
    margin: 0 auto;
}

One of the shortcomings of this technique is that when used on websites with multiple pages, the layout can appear to “jump” a little bit when going back and forth between pages that require scroll bars and pages that do not. This is because the ~16px width of the scroll bar in the browser window causes the content area to become that much narrower and the wrap div re-centers itself in the narrower content area causing the jump.

One way to eliminate this jump is to force scroll bars onto every page regardless if they need them or not. This may annoy some purists out there, but I think it’s a decent solution.

This is one way to do it, which forces the page to always be just a little bit taller than the browser window forcing a right scroll bar:

html {
    height: 100%;
    margin-bottom: 0.01em;
}

It’s a good idea, but it doesn’t seem to get the job done in Firefox.

Here is a way you can force only the right sidebar with a nasty and unsemantic hack:

#scroll {
    position: absolute;
    top: 0;
    bottom: -0.1px;
    width: 1em;
    z-index: -1;
}

Then just include an empty div in your HTML with an id of “scroll”. Like I said, this is kind of a nasty way to do it, here is a much cleaner way:

html {
    height: 102%;
}

Here is another solution, which effectively forces both horizontal and vertical scrollbars:

html {
    overflow: scroll;
} 

You can see an example of this working in this example. It would be nice if we could get just the vertical scroll bar by assigning overflow-y to scroll, but again it doesn’t work in Firefox. UPDATE: Actually, I’ve been shown the light. Assigning overflow-y to scroll does work, and it works in Firefox, Safari, and IE 6, and that makes it the best solution:

html {
	overflow-y: scroll;
}