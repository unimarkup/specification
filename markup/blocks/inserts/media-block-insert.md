# Media block insert

The general syntax for the media block insert is described in the general [block insert](/markup/blocks/inserts/README.md) section.

The keyword for media inserts is `!!`.

Compared to [inline media inserts](/markup/inlines/boxes/inserts/inline-media-insert.md), a media block insert allows [block decorations](/markup/decorators/block-decoration.md). This may be used to create captions.

**Usage:**

```
!![some image](<image-path> myImageTitle).
+++
Image caption.
+++
```

**Type:** `media-block-insert`

## Media kind identification

The syntax is the same for image, video, audio, etc., so the implementation must identify the media kind according to the file extension of the resource.

The rendered output may then depend on the media kind.

**Example:**

```
!![some image](/assets/myImage.png)

!![some video](/assets/myVideo.mp4)

!![some audio](/assets/myAudio.mp3)
```

## Set multiple resources

**WIP**

The syntax is the same as defined for the inline [media insert](/markup/inlines/boxes/inserts/inline-media-insert.md#set-multiple-resources).

```
!![some resource](<default link>)(<other source link>, <other source link> { type: <media type>; media: <media query> })(<other source link> { type: <media type> })
```
