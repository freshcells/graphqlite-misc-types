[![Latest Stable Version](https://poser.pugx.org/thecodingmachine/graphqlite-misc-types/v/stable)](https://packagist.org/packages/thecodingmachine/graphqlite-misc-types)
[![Total Downloads](https://poser.pugx.org/thecodingmachine/graphqlite-misc-types/downloads)](https://packagist.org/packages/thecodingmachine/graphqlite-misc-types)
[![Latest Unstable Version](https://poser.pugx.org/thecodingmachine/graphqlite-misc-types/v/unstable)](https://packagist.org/packages/thecodingmachine/graphqlite-misc-types)
[![License](https://poser.pugx.org/thecodingmachine/graphqlite-misc-types/license)](https://packagist.org/packages/thecodingmachine/graphqlite-misc-types)
[![Build Status](https://travis-ci.org/thecodingmachine/graphqlite-misc-types.svg?branch=master)](https://travis-ci.org/thecodingmachine/graphqlite-misc-types)
[![Coverage Status](https://coveralls.io/repos/thecodingmachine/graphqlite-misc-types/badge.svg?branch=master&service=github)](https://coveralls.io/github/thecodingmachine/graphqlite-misc-types?branch=master)

# GraphQLite miscellaneous types

This package is an add-on to the [GraphQLite](http://graphqlite.thecodingmachine.io/) PHP library.
It contains a set of GraphQL scalar types that can be added to GraphQLite.

This is a takeover drop-in fork of https://github.com/thecodingmachine/graphqlite-misc-types which seems to be abandoned.  
We left the namespace as `TheCodingMachine` to assure drop-in replacement.


## Install

```console
$ composer require freshcells/graphqlite-misc-types
```

## "Any" scalar type

This types adds support for a "AnyScalar" type that can be any of "string", "int", "float" or "bool".

### Usage

```php
/**
 * @Query()
 * @param scalar $scalar
 * @return scalar
 */
public function echoScalar($scalar)
{
    return $scalar;
}
```

Use the "scalar" type-hint in the DocBlock to cast a value to "AnyScalar".

### Registering AnyScalar

#### Using the SchemaFactory

If you are using the `SchemaFactory` to initialize GraphQLite, use this code to add support for `AnyScalar`:

```php
$schemaFactory->addRootTypeMapper(new \TheCodingMachine\GraphQLite\Types\AnyScalar\AnyScalarTypeMapper());
```

#### Using the Symfony bundle

If you are using the Symfony bundle to initialize GraphQLite, register the `AnyScalarTypeMapper` as a service:

```yaml
# config/services.yaml
services:
    TheCodingMachine\GraphQLite\Types\AnyScalar\AnyScalarTypeMapper:
        tags: ['graphql.root_type_mapper']
```

## "JSON" type

This type adds support for a "JSON" type that can be used to represent JSON data.

#### Using the Symfony bundle

If you are using the Symfony bundle to initialize GraphQLite, register the `JSONScalarTypeMapperFactory` as a service:

```yaml
# config/services.yaml
TheCodingMachine\GraphQLite\Types\JSONScalar\JSONScalarTypeMapperFactory:
tags:
  - { name: "graphql.root_type_mapper_factory" }
```
