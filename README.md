# Linkify <small>a jQuery Plugin</small>

Download 1.0.0:
- [Minified](https://github.com/HitSend/jQuery-linkify/blob/master/dist/jquery.linkify.min.js)
- [Source](https://github.com/HitSend/jQuery-linkify/blob/master/dist/jquery.linkify.js)

===

Linkify is a jQuery plugin for finding URLs in plain-text and converting them to HTML links. It works with all valid URLs and email addresses.

## Demo
[Launch demo](https://github.com/HitSend/jQuery-linkify/tree/master/demo)

## Examples

### Basic Usage

To detect links within any set of elements, just call $(selector).linkify() on document load.

#### Code

```html
<p id="paragraph1">Check out this link to http://google.com</p>
<p id="paragraph2">You can also email support@example.com to view more.</p>
```

```javascript
$(window).on('load', function () {
  $('p').linkify();
});
```

#### Output

``` html
<p id="paragraph1">
  Check out this link to
  <a href="http://google.com" class="linkified" target="_blank">
    http://google.com
  </a>
</p>
<p id="paragraph2">
  You can also email
  <a href="mailto:support@example.com" class="linkified">
    support@example.com
  </a>
  to view more.
</p>
```

#### Notice

Linkify currently cannot process elements that contain HTML. It will strip out any tags it encounters before discovering URLs.

### Usage via HTML attributes

Linkify also provides a DOM data- API. The following code will find links in the #linkify-example paragraph element:

```html
<p id="linkify-example" data-linkify="this">
  Lorem ipsum dolor sit amet, consectetur adipisicing
  elit, sed do eiusmod tempor incididunt ut labore et
  dolore magna aliqua.
</p>
```

Pass in a selector instead of this to linkify every element with that selector. The example below linkifies every paragraph and .plain-text element in the bodytag:

```html
<body data-linkify="p, .plain-text">
  ...
</body>
```

## Options

Linkify is applied with the following default options. Below is a description of each.

```javascript
$('selector').linkify({
  tagName: 'a',
  target: '_blank',
  newLine: '\n',
  linkClass: 'linkified',
  linkAttributes: null
});
```

<table>
	<thead>
		<tr>
			<th>Option</th>
			<th>Type</th>
			<th>Default</th>
			<th>Description</th>
			<th>
				Data Attribute (used on the same element as
				<code>data-linkify</code>)
			</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>tagName</td>
			<td>String</td>
			<td><code>"a"</code></td>
			<td>
				The tag that should be used to wrap each URL. This is
				useful for cases where <code>a</code> tags might be
				innapropriate, or might syntax problems (e.g., finding
				URLs inside an <code>a</code> tag).
			</td>
			<td>
				<code class="small">data-linkify-tagname</code>
			</td>
		</tr>
		<tr>
			<td>target</td>
			<td>String</td>
			<td><code>"_blank"</code></td>
			<td><code>target</code> attribute for each linkified tag.</td>
			<td><code class="small">data-linkify-target</code></td>
		</tr>
		<tr>
			<td>newLine</td>
			<td>String</td>
			<td><code>"\n"</code></td>
			<td>
				The character to replace new lines with. Replace with
				<code>"&lt;br&gt;"</code> to space out multi-line user
				content.
			</td>
			<td><code class="small">data-linkify-newline</code></td>
		</tr>

		<tr>
			<td>linkClass</td>
			<td>String</td>
			<td><code>"linkified"</code></td>
			<td>
				The class to be added to each linkified tag. The default
				<code>.linkified</code> ensures that each link will be
				clickable, regardless of the value of <code>tagName</code>.
			</td>
			<td><code class="small">data-linkify-linkclass</code></td>
		</tr>

		<tr>
			<td>linkAttributes</td>
			<td>Object</td>
			<td><code>null</code></td>
			<td>
				HTML attributes to add to each linkified tag. In the
				following example, the <code>tabindex</code> and
				<code>rel</code> attributes will be added to each link.

<pre>
$('p').linkify({
	linkAttributes: {
		tabindex: 0,
		rel: 'nofollow'
	}
});
</pre>

			</td>
			<td>N/A</td>
		</tr>
	</tbody>
</table>