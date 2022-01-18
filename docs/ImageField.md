---
layout: default
title: "The ImageField Component"
---

# `<ImageField>`

If you need to display an image based on a path contained in a record field, you can use the `<ImageField />` component:

```jsx
import { ImageField } from 'react-admin';

<ImageField source="url" title="title" />

// renders the record { id: 123, url: 'cat.png', title: 'meow' } as 
<div>
    <img src="cat.png" title="meow" />
</div>
```

This field is also often used within the [`<ImageInput />`](./ImageInput.md) component to display a preview.

## Properties

| Prop    | Required | Type   | Default      | Description                                                                              |
| ------- | -------- | ------ | ------------ | ---------------------------------------------------------------------------------------- |
| `src`   | Optional | string | -            | A function returning a string (or an element) to display based on a record               |
| `title` | Optional | string | record.title | The name of the property containing the image source if the value is an array of objects |

`<ImageField>` also accepts the [common field props](./Fields.md#common-field-props).

## `sx`: CSS API

The `<ImageField>` component accepts the usual `className` prop. You can also override many styles of the inner components thanks to the `sx` property (as most Material UI components, see their [documentation about it](https://mui.com/customization/how-to-customize/#overriding-nested-component-styles)). This property accepts the following subclasses:

| Rule name               | Description                                                                    |
|-------------------------|--------------------------------------------------------------------------------|
| `& .RaImageField-list`  | Applied to the underlying `<ul>` component when `sourceValue` prop is an array |
| `& .RaImageField-image` | Applied to each underlying `<img>` component                                   |

To override the style of all instances of `<ImageField>` using the [material-ui style overrides](https://mui.com/customization/globals/#css), use the `RaImageField` key.

## Usage

The optional `title` prop points to the picture title property, used for both `alt` and `title` attributes. It can either be a hard-written string, or a path within your JSON object:

```jsx
// { picture: { url: 'cover.jpg', title: 'Larry Cover (French pun intended)' } }

<ImageField source="picture.url" title="picture.title" />
// renders img title as "Larry Cover (French pun intended)"

<ImageField source="picture.url" title="Picture" />
// renders img title as "Picture", since "Picture" is not a path in previous given object
```

If the record actually contains an array of images in the property defined by the `source` prop, the `src` prop will be needed to determine the `src` value of the images, for example:

```js
// This is the record
{
    pictures: [
        { url: 'image1.jpg', desc: 'First image' },
        { url: 'image2.jpg', desc: 'Second image' },
    ],
}

<ImageField source="pictures" src="url" title="desc" />
```