go-version [![Build Status](https://travis-ci.org/mcuadros/go-version.png?branch=master)](https://travis-ci.org/mcuadros/go-version)
==============================

Version normalizer and comparison library for go, heavy based on PHP version_compare function and Version comparsion libs from [Composer](https://github.com/composer/composer) PHP project

Installation
------------

The recommended way to install go-version

```
go get github.com/mcuadros/go-version
```

Examples
--------

How import the package

```go
import (
    "github.com/mcuadros/go-version"
)
```

`version.Normalize()`: Normalizes a version string to be able to perform comparisons on it

```go
version.Normalize("10.4.13-b")
//Returns: 10.4.13.0-beta
```


`version.CompareSimple()`: Compares two normalizated version number strings

```go
version.CompareSimple("1.2", "1.0.1")
//Returns: 1

version.CompareSimple("1.0rc1", "1.0")
//Returns: -1
```


`version.Compare()`: Compares two normalizated version number strings, for a particular relationship

```go
version.Compare("1.0-dev", "1.0", "<")
//Returns: true

version.Compare("1.0rc1", "1.0", ">=")
//Returns: false

version.Compare("1.0", "1.0b1", "ge")
//Returns: true
```

`version.ConstrainGroup.Match()`: Match a given version againts a group of constrains, read about constraint string format at [Composer documentation](http://getcomposer.org/doc/01-basic-usage.md#package-versions)  

```go
c := version.NewConstrainGroupFromString(">2.0,<=3.0")
c.Match("2.5.0beta")
//Returns: true

c := version.NewConstrainGroupFromString("~1.2.3")
c.Match("1.2.3.5")
//Returns: true
```

License
-------

MIT, see [LICENSE](LICENSE)