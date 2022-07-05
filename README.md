# vuenos-upload-image

> description

## Prerequisites

This project using NodeJS (version 16.10.0 or later) and NPM.
[Node](http://nodejs.org/) and [NPM](https://npmjs.org/) are really easy to install.
To make sure you have them available on your machine,
try running the following command.

```sh
$ npm -v && node -v
7.24.0
v16.10.0
```

## Table of contents

- [vuenos-upload-image](#vuenos-upload-image)
  - [Prerequisites](#prerequisites)
  - [Table of contents](#table-of-contents)
  - [Getting Started](#getting-started)
  - [Installation](#installation)
  - [Usage](#usage)
    - [Import component](#import-component)
    - [Upload image](#upload-image)
    - [Preview image](#preview-image)
  - [Variables binding](#variables-binding)
  - [Versioning](#versioning)
  - [Author](#author)

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

## Installation
To install and set up the library, run:
```sh
npm install vuenos-upload-image
```

## Usage

### Import component
```typescript
import VuenosUploadImage from "vuenos-upload-image";
```

```html
<vuenos-upload-image :imgListPreview="imgListPreview"
           :type="'upload'"
           :disabled="true"
           @getImgFileList="getImgFileList">
</vuenos-upload-image>
```

### Upload image

> * Set ```type = 'upload'```
> * Get list of file image through function ```getImgFileList()```

```typescript
const getImgFileList = (val) => {
    console.log(val)
}
```

* Example
```html
<vuenos-upload-image :type="'upload'"
           @getImgFileList="getImgFileList">
</vuenos-upload-image>
```

### Preview image

> * Set ```type = 'preview'```
>* Pass array of img path to ```:imgListPreview```

```typescript
const imgListPreview = ref([]);
```

* Example

```html
<vuenos-upload-image :type="'preview'"
           :imgListPreview="imgListPreview">
</vuenos-upload-image>
```

### Variables binding

| ATTRIBUTE      | DESCRIPTION                   |    REQUIRED     |   TYPE   |  ACCEPTED VALUE |   DEFAULT |
|:---------------|:------------------------------|:---------------:|:--------:|----------------:|----------:|
| imgListPreview | List of image want to show    | *(Only preview) |  Array   |                 |     empty | 
| type           | Type of use                   |        *        |  String  |  upload/preview |     empty |
| getImgFileList | Function get image list       | *(Only upload)  | Function |                 |           |
| disabled       | disable select img            |                 | Boolean  |      true/false |     false |
| width          | width of component frame      |                 |  Number  |              90 |      75px |
| maxImages      | max image can upload          |                 |  Number  |               3 |      9999 |
| imageTypes     | image type can upload         |                 |  String  | '.jpg,.jpeg,..' | 'image/*' |
| maxSize        | max size of each image upload |                 |  Number  |         8000000 |   8000000 |

## Versioning

v0.0.1

## Author

* **Sơn Nguyễn** - *Initial work* - [Sơn Nguyễn](https://github.com/biennui1998mu)
