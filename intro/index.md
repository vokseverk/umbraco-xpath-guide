# How XPath works

XPath is used to select nodes or values from an XML document, very similar to how SQL is used to select data form a database. However, with SQL you're always selecting "from the top", so to speak, whereas in XPath, you have a *context node* that your expression is evaluated from.

Let's see a simple example:

We'll work with a simple XML document that looks like this:

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

Let's start by selecting the `<movies>` element:

### XPath

	movies

### Result

	<movies>


If there's no current context, the *root node* (often referred to as "/") of the document is used - the movies node is a child of the root node so all we had to do was to use the element name in the expression.
