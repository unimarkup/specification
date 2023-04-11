# Inline media insert

The general syntax for the inline media insert is described in the general [inline insert](/markup/inlines/boxes/inserts/README) section.

The keyword for media inserts is `!!`.

**Usage:**

```
Some paragraph text with [!!some image](/assets/myImage.png).

[!!<alternate text for this media resource>](<url to some media resource> <link title>)
```

**Type:** `inline-media-insert`

## Media kind identification

The syntax is the same for image, video, audio, etc., so the implementation must identify the media kind according to the file extension of the resource.

The rendered output may then depend on the media kind.

**Example:**

```
[!!some image](/assets/myImage.png)

[!!some video](/assets/myVideo.mp4)

[!!some audio](/assets/myAudio.mp3)
```

## Set multiple resources

**WIP**

Multiple resources may be set for one media insert, by adding one or more `()` at the end of the media insert.
This is useful for e.g. the HTML output, where a browser may choose the best fitting resource.

In addition, a media type and media query may be set per `()` at the end using the attribute syntax. The `type` attribute sets the media type for all resources in the same `()`. The `media` attribute allows to set a media query like `@media` in CSS.

```
[!!some resource](<default link>)(<other source link>, <other source link> { type: <media type>; media: <media query> })(<other source link> { type: <media type> })
```
