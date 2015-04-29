# XPath Basics

XPath is used to select nodes or values from an XML document, very similar to how SQL is used to select data form a database. However, with SQL you're always selecting "from the top", so to speak, whereas in XPath, you have a *context node* that your expression is evaluated from.

Let's see a simple example:

We'll work with a simple XML document that looks like this:

```xml
<movies>
	<movie id="4815162342">
		<title>The Numbers Are Bad</title>
	</movie>
	<movie id="314" in3D="yes">
		<title>Life of Pi</title>
	</movie>
	<movie id="42">
		<title>The Hitchhiker's Guide to the Galaxy</title>
	</movie>
</movies>
```



## Simple steps

Let's start by selecting the `<movies>` element:

### XPath

	movies

### Result

```xml
<movies>
```

If there's no current context, the *root node* (often referred to as "/") of the document is used - the `<movies>` node is a child of the root node, so all we had to do was to use the element name in the expression.

Next up, we'll try to select a `<movie>`:

### XPath

	movies/movie

### Result

```xml
<movie id="4815162342">...</movie>
<movie id="314" in3D="yes">...</movie>
<movie id="42">...</movie>
```

*The ellipsis (...) denotes that the complete subtree of a node is included in the result - we just don't need to see it all*

It may be a little unexpected, but the result is a nodeset with **three nodes**; every node that matches the expression will be included in the result. If we only want to select a single movie, we need to specify which one we're after — we do that with a *predicate:*

## Filtering with predicates

To select only the first movie we can use a *positional* predicate:

	movies/movie[1]

which is actually shorthand for this:

	movies/movie[position() = 1]

*(So the first element in a nodeset is referred to as being in "position one", not at "offset zero" - just to get that out of the way :-)*

### Result

```xml
<movie id="4815162342">...</movie>
```

As you can see, a *predicate* is a filter that affects the selection preceding it. So in this case, the initial selection is all `<movie>` nodes that are children of the `<movies>` node - but then by applying the predicate we're narrowing down the number of matching nodes; In this case to a single one.

A predicate is essentially an expression returning either `true()` or `false()`, which means you can do stuff like asking for movies with a specific feature:

	movies/movie[@in3D = 'yes']

### Result

```xml
<movie id="314" in3D="yes">...</movie>
```

Or maybe something like this, using a function call:

	movies/movie[starts-with(title, 'The')]
	
### Result

```xml
<movie id="4815162342">
	<title>The Numbers Are Bad</title>
</movie>
<movie id="42">
	<title>The Hitchhiker's Guide to the Galaxy</title>
</movie>
```

Note that **title** used inside the function is, in itself, an XPath - evaluated relative to the *current context,* which is a movie element, since that's what the predicate is "attached" to.



