# RaBe CloudEvents Specification

The RaBe [CloudEvents](https://cloudevents.io/) specification defines the required, `URI`
and `URI-reference` based, `type` and `source` attributes of the CloudEvents specification.

## Table of Contents

- [Overview](#overview)
- [Notations and Terminology](#notations-and-terminology)
- [Versioning](#versioning)
- [Type System](#type-system)
- [REQUIRED Attributes](#required-attributes)
- [Example](#example)

## Overview

Events occur all over the place and all the time, having a common understanding
of how to communicate events allows us to capture them in a meaningful way ensuring
they can be leveraged in protocol and implementation agnostic scenarios by a range
of consumers and producers across the diverse landscape of the RaBe IT stack.

This specification is heavily inspired by the work done by the maintainers of
the [CloudEvents v1.0.1 Spec](https://github.com/cloudevents/spec/blob/v1.0.1/spec.md).

## Notations and Terminology

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119](https://tools.ietf.org/html/rfc2119).

This document SHALL adhere to the [Notational Conventions](https://github.com/cloudevents/spec/blob/v1.0.1/spec.md#notational-conventions)
and [Terminology](https://github.com/cloudevents/spec/blob/v1.0.1/spec.md#terminology)
described in the the [CloudEvents v1.0.1 Spec](https://github.com/cloudevents/spec/blob/v1.0.1/spec.md).

## Versioning

This specification is versioned using git tag. It uses [go-semantic-release](https://go-semantic-release.xyz/)
for tagging new versions following the [Conventional Commits v1.0.0 specification](https://www.conventionalcommits.org/en/v1.0.0/).

## Type System

This specification defines types from the CloudEvents [Type System](https://github.com/cloudevents/spec/blob/v1.0.1/spec.md#terminology).

- `URI` - Absolute uniform resource identifier.
  - String encoding: `Absolute URI` as defined in
    [RFC 3986 Section 4.3](https://tools.ietf.org/html/rfc3986#section-4.3).
- `URI-reference` - Uniform resource identifier reference.
  - String encoding: `URI-reference` as defined in
    [RFC 3986 Section 4.1](https://tools.ietf.org/html/rfc3986#section-4.1).

## REQUIRED Attributes

The following attributes MUST follow these constaints in addition to the CloudEvents [REQUIRED Attributes](https://github.com/cloudevents/spec/blob/v1.0.1/spec.md#terminology).

### source

- Type: `URI-reference`
- Description: Identifies the context in which an event happened. Often this
  will include information such as the type of the event source, the
  organization publishing the event or the process that produced the event. The
  exact syntax and semantics behind the data encoded in the URI is defined by
  the event producer.

  An application SHOULD use the RECOMMENDED unique, internet-wide, absolute URI
  format.

  It is RECOMMENDED to use the GitHub page of the project as `source`.

  A source MAY assign a unique `source` to each distinct by appending a fragment
  to the URI. It is RECOMMENDED that the unique part is based on a UUID to aid
  with tracing efforts or similar requirements.

  An application MAY use UUID, URN or application-specific schemes to create
  unique `source` identifiers but this is NOT RECOMMENDED.

- Constraints:
  - SHOULD be a based on the event producers project page.
- Examples
  - `https://github.com/radiorabe/rabemimimi`
  - `https://github.com/LibreTime/libretime#<event-id-for-tracing>`
  - `https://github.com/radiorabe/raar_show_descriptor`

### type

- Type: `String`
- Description: This attribute contains a value describing the type of event
  related to the originating occurrence. Often this attribute is used for
  routing, observability, policy enforcement, etc. The format of this is
  producer defined and might include information such as the version of the
  `type` - see
  [Versioning of CloudEvents in the Primer](primer.md#versioning-of-cloudevents)
  for more information.

  The RaBe DNS authority `events.api.rabe.ch` SHALL be used for reverse-DNS
  naming purposes.
 
  An event producer MAY use a subdomain indicate which component an event
  originated from. Types SHOULD contain versioning information.

- Constraints:
  - SHOULD be prefixed with a reverse-DNS name.
  - if used, the reverse-DNS name SHALL be `ch.rabe.api.events`
- Examples
  - Such event, much type, very version:
    - ch.rabe.api.events.rabemimimi.v1alpha.mimimi.created
    - ch.rabe.api.events.rabemimimi.v1alpha.mimimi.updated
  - Simple unversioned events:
    - ch.rabe.api.libretime.onair

## Example

The following example shows a paired down RaBe CloudEvent serialized as JSON:

```json
{
    "type" : "ch.rabe.api.events.events-spec.v1.such.event",
    "source" : "https://github.com/radiorabe/events-spec"
}
```

## License

This specification is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).

## Copyright

Copyright (c) 2021 [Radio Bern RaBe](http://www.rabe.ch)
