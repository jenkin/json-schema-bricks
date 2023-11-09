# JSON Schema Bricks

A bunch of JSON Schema specifications of general interest you can freely `$ref`.

## Getting started

[JSON Schema](https://json-schema.org/) specification allows [schemas composition](https://json-schema.org/understanding-json-schema/reference/combining) and [cross-reference](https://json-schema.org/understanding-json-schema/structuring#dollarref) using `$ref` attribute.

This project lists some useful reusable schemas ready to be referenced by yours. The `dev` variants are human-readable and can contain external references (resolved at runtime), in the `prod` ones all external schemas are *dereferenced* (so resolved at build time) and included in a standalone minified bundle. You can also refer to a sub-schema using [JSON pointers](https://json-schema.org/understanding-json-schema/structuring#json-pointer) (see the second example).

> Tip! Take also a look to [JSON Schema Store](https://www.schemastore.org/json/), it freely lists and serves hundreds of open source schemas!

### Example

A (partial) validation of the Node Package Manager `package.json` (see the [official docs](https://docs.npmjs.com/cli/v10/configuring-npm/package-json)).

```json
{
  "title": "A node project",
  "type": "object",
  "properties": {
    "name": {
      "type": "string"
    },
    "version": {
      "$ref": "https://jenkin.dev/json-schema-bricks/semver.schema.min.json"
    }
    "description": {
      "type": "string"
    },
    "keywords": {
      "type": "array",
      "items": {
        "type": "string"
      }
    },
    "homepage": {
      "type": "string",
      "format": "uri"
    }
  }
}
```

Validation of an object that represents an image.

```json
{
  "title": "An image",
  "type": "object",
  "properties": {
    "name": {
      "type": "string"
    },
    "size": {
      "description": "File size in bytes",
      "type": "integer",
      "minimum": 0
    },
    "width": {
      "description": "Image width in pixels",
      "type": "integer",
      "minimum": 0
    },
    "height": {
      "description": "Image height in pixels",
      "type": "integer",
      "minimum": 0
    },
    "type": {
      "description": "An official mime-type",
      "$ref": "https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.min.json#/$defs/ImageRegistry"
    }
  }
}
```

## Table of Contents

- [IANA Protocol Registries](#iana-protocol-registries)
  - [Language Subtag Registry](#iana-language-subtag-registry) [[prod](https://jenkin.dev/json-schema-bricks/IANALanguageSubtags.schema.min.json), [dev](https://jenkin.dev/json-schema-bricks/IANALanguageSubtags.schema.json)]
  - [Link Relation Types Registry](#iana-link-relation-types-registry) [[prod](https://jenkin.dev/json-schema-bricks/IANALinkRelationTypes.schema.min.json), [dev](https://jenkin.dev/json-schema-bricks/IANALinkRelationTypes.schema.json)]
  - [Media Types Registry](#iana-media-types-registries) [[prod](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.min.json), [dev](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.json)]
- [Geographic Information System (GIS)](#geographic-information-system-gis)
  - [GeocodeJSON](#geocodejson) [[prod](https://github.com/geocoders/geocodejson-spec/blob/master/draft/geocodejson.schema.json), [dev](https://github.com/geocoders/geocodejson-spec/blob/master/src/geocodejson.schema.json)] :partying_face: OFFICIALLY ADOPTED! :partying_face:
  - [GeoHash](#geohash) [[prod](https://jenkin.dev/json-schema-bricks/geohash.schema.min.json), [dev](https://jenkin.dev/json-schema-bricks/geohash.schema.json)]
- [Miscellaneous](#miscellaneous)
  - [HAL+JSON](#json-hypertext-application-language) [[prod](https://jenkin.dev/json-schema-bricks/hal.schema.min.json), [dev](https://jenkin.dev/json-schema-bricks/hal.schema.json)]
  - [SemVer](#semantic-versioning) [[prod](https://jenkin.dev/json-schema-bricks/semver.schema.min.json), [dev](https://jenkin.dev/json-schema-bricks/semver.schema.json)]

### IANA Protocol Registries

[IANA](https://www.iana.org/about) (Internet Assigned Numbers Authority) allocates and maintains unique codes and numbering systems that are used in the technical standards (protocols) that drive the Internet.

[Protocol parameter registries](https://www.iana.org/protocols) represent the authoritative record of many of the codes and numbers contained in a variety of Internet protocols. IANA maintains these records in compliance with the associated technical standards and allocation policies, and provides this service in coordination with the Internet Engineering Task Force (IETF).

#### IANA Language Subtag Registry

IANA Language Subtag schema [[prod](https://jenkin.dev/json-schema-bricks/IANALanguageSubtags.schema.min.json), [dev](https://jenkin.dev/json-schema-bricks/IANALanguageSubtags.schema.json)].

> This document describes the structure, content, construction, and semantics of language tags for use in cases where it is desirable to indicate the language used in an information object. It also describes how to register values for use in language tags and the creation of user-defined extensions for private interchange.

Source: https://www.iana.org/assignments/language-subtag-registry/language-subtag-registry (see [RFC5646](https://www.rfc-editor.org/rfc/rfc5646.html)).

> Notes: only Subtags with `Type: language` are listed.

#### IANA Link Relation Types Registry

IANA Link Relation Types schema [[prod](https://jenkin.dev/json-schema-bricks/IANALinkRelationTypes.schema.min.json), [dev](https://jenkin.dev/json-schema-bricks/IANALinkRelationTypes.schema.json)].

> This specification defines a model for the relationships between resources on the Web (links) and the type of those relationships (link relation types).

Source: https://www.iana.org/assignments/link-relations/link-relations.xhtml (see [RFC8288](https://www.rfc-editor.org/rfc/rfc8288.html)).

#### IANA Media Types Registries

IANA Media Types schema [[prod](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.min.json), [dev](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.json)].

> This specification defines a model for the relationships between resources on the Web (links) and the type of those relationships (link relation types).

Source: https://www.iana.org/assignments/media-types/media-types.xhtml (see [RFC6838](https://www.rfc-editor.org/rfc/rfc6838.html) and [RFC4855](https://www.rfc-editor.org/rfc/rfc4855.html)).

Registries:

- [application](https://www.iana.org/assignments/media-types/media-types.xhtml#application) [[prod](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.min.json#/$defs/ApplicationRegistry), [dev](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.json#/$defs/ApplicationRegistry)]
- [audio](https://www.iana.org/assignments/media-types/media-types.xhtml#audio) [[prod](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.min.json#/$defs/AudioRegistry), [dev](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.json#/$defs/AudioRegistry)]
- [font](https://www.iana.org/assignments/media-types/media-types.xhtml#font) [[prod](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.min.json#/$defs/FontRegistry), [dev](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.json#/$defs/FontRegistry)]
- [example](https://www.iana.org/assignments/media-types/media-types.xhtml#example) (empty set)
- [image](https://www.iana.org/assignments/media-types/media-types.xhtml#image) [[prod](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.min.json#/$defs/ImageRegistry), [dev](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.json#/$defs/ImageRegistry)]
- [message](https://www.iana.org/assignments/media-types/media-types.xhtml#message) [[prod](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.min.json#/$defs/MessageRegistry), [dev](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.json#/$defs/MessageRegistry)]
- [model](https://www.iana.org/assignments/media-types/media-types.xhtml#model) [[prod](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.min.json#/$defs/ModelRegistry), [dev](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.json#/$defs/ModelRegistry)]
- [multipart](https://www.iana.org/assignments/media-types/media-types.xhtml#multipart) [[prod](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.min.json#/$defs/MultipartRegistry), [dev](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.json#/$defs/MultipartRegistry)]
- [text](https://www.iana.org/assignments/media-types/media-types.xhtml#text) [[prod](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.min.json#/$defs/TextRegistry), [dev](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.json#/$defs/TextRegistry)]
- [video](https://www.iana.org/assignments/media-types/media-types.xhtml#video) [[prod](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.min.json#/$defs/VideoRegistry), [dev](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.json#/$defs/VideoRegistry)]

Templates (custom regex):

- application [[prod](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.min.json#/$defs/ApplicationTemplate), [dev](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.json#/$defs/ApplicationTemplate)]
- audio [[prod](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.min.json#/$defs/AudioTemplate), [dev](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.json#/$defs/AudioTemplate)]
- font [[prod](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.min.json#/$defs/FontTemplate), [dev](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.json#/$defs/FontTemplate)]
- example [[prod](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.min.json#/$defs/ExampleTemplate), [dev](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.json#/$defs/ExampleTemplate)]
- image [[prod](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.min.json#/$defs/ImageTemplate), [dev](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.json#/$defs/ImageTemplate)]
- message [[prod](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.min.json#/$defs/MessageTemplate), [dev](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.json#/$defs/MessageTemplate)]
- model [[prod](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.min.json#/$defs/ModelTemplate), [dev](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.json#/$defs/ModelTemplate)]
- multipart [[prod](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.min.json#/$defs/MultipartTemplate), [dev](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.json#/$defs/MultipartTemplate)]
- text [[prod](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.min.json#/$defs/TextTemplate), [dev](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.json#/$defs/TextTemplate)]
- video [[prod](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.min.json#/$defs/VideoTemplate), [dev](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.json#/$defs/VideoTemplate)]

Combinations:

- all registries [[prod](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.min.json#/$defs/AllRegistries), [dev](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.json#/$defs/AllRegistries)]
- all templates [[prod](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.min.json#/$defs/AllTemplates), [dev](https://jenkin.dev/json-schema-bricks/IANAMediaTypes.schema.json#/$defs/AllTemplates)]

> Notes: empty, obsolete or deprecated media types are excluded, `text/plain` is included. Root schema references `AllRegistries`.

### Geographic Information System (GIS)

A [geographic information system](https://en.wikipedia.org/wiki/Geographic_information_system) (GIS) consists of integrated computer hardware and software that store, manage, analyze, edit, output, and visualize geographic data.

#### GeocodeJSON

> OFFICIALLY ADOPTED!!!

Official GeocodeJSON schema [[prod](https://github.com/geocoders/geocodejson-spec/blob/master/draft/geocodejson.schema.json), [dev](https://github.com/geocoders/geocodejson-spec/blob/master/src/geocodejson.schema.json)].

> An attempt to have standard geojson responses from geocoders.

Source: https://github.com/geocoders/geocodejson-spec (see [geocodejson-spec/pull/25](https://github.com/geocoders/geocodejson-spec/pull/25)).

#### GeoHash

GeoHash [[prod](https://jenkin.dev/json-schema-bricks/geohash.schema.min.json), [dev](https://jenkin.dev/json-schema-bricks/geohash.schema.json)].

> Geohash is a public domain geocode system which encodes a geographic location into a short string of letters and digits.

Source: http://geohash.org

### Miscellaneous

#### JSON Hypertext Application Language

HAL+JSON [[prod](https://jenkin.dev/json-schema-bricks/hal.schema.min.json), [dev](https://jenkin.dev/json-schema-bricks/hal.schema.json)].

> This document proposes a media type for representing resources and their relations with hyperlinks.

Source: https://github.com/mikekelly/hal-rfc (see [hal-rfc/issues/28](https://github.com/mikekelly/hal-rfc/issues/28)).

#### Semantic Versioning

SemVer [[prod](https://jenkin.dev/json-schema-bricks/semver.schema.min.json), [dev](https://jenkin.dev/json-schema-bricks/semver.schema.json)].

> Under this scheme, version numbers and the way they change convey meaning about the underlying code and what has been modified from one version to the next.

Source: https://semver.org (see [semver.org/issues/431](https://github.com/semver/semver.org/issues/431)).

## Contributing

Any contribution is welcome! Please read and accept our [Code of Conduct](https://github.com/jenkin/json-schema-bricks/blob/main/CODE_OF_CONDUCT.md), then refer to [Contributing Guidelines](https://github.com/jenkin/json-schema-bricks/blob/main/CONTRIBUTING.md) before [opening issues](https://github.com/jenkin/json-schema-bricks/issues) or [pull requests](https://github.com/jenkin/json-schema-bricks/pulls).

## License

CC0 1.0 Universal
