---
title: "Comparing Go Values"
date: 2017-08-13T11:04:59+02:00
tags: go
---

## Comparability by type

Basic data types are always comparable using the `==` and `!=` operators: **integer** values, **floating-point** numbers, **complex** numbers, **boolean** values, **string** values, **constant** values.

**Array** values are comparable, if they contain a comparable element type

**Pointer** values are comparable.

**Channel** values are comparable.

**Interface** values are comparable.

Comparing **interface** values works only if the dynamic type is comparable.

**Function** values, **Slice** values and **Map** values are **not** comparable, they can only be compared with `nil`, as a special case.

## The rules of comparison

From the Go spec:

- **Boolean** values are comparable. Two boolean values are equal if they are either both `true` or both `false`.

- **Integer** values are comparable and ordered, in the usual way.

- **Floating point** values are comparable and ordered, as defined by the _IEEE-754_ standard.

- **Complex** values are comparable. Two complex values u and v are equal if both `real(u) == real(v)`` and `imag(u) == imag(v)`.

- **String** values are comparable and ordered, lexically byte-wise.

- **Pointer** values are comparable. Two pointer values are equal if they point to the same variable or if both have value `nil`. Pointers to distinct zero-size variables may or may not be equal.

- **Channel** values are comparable. Two channel values are equal if they were created by the same call to make or if both have value `nil`.

- **Interface** values are comparable. Two interface values are equal if they have identical dynamic types and equal dynamic values or if both have value `nil`.

- A value x of **non-interface** type `X` and a value `t` of **interface** type `T` are comparable when values of type `X` are comparable and `X` implements `T`. They are equal if `t`'s dynamic type is identical to `X` and t's dynamic value is equal to `x`.

- **Struct** values are comparable if all their fields are comparable. Two struct values are equal if their corresponding non-blank fields are equal.

- **Array** values are comparable if values of the array element type are comparable. Two array values are equal if their corresponding elements are equal.

## Failing comparing

If the struct contains a field whose type is not comparable, you'll get a compile time error when comparing.

## Comparing uncomparable types: enter `refect.DeepEqual()`

The `reflect` stdlib package provides the `reflect.DeepEqual()` function which takes 2 types, and returns a boolean:

> `func DeepEqual(x, y interface{}) bool`

Values of distinct types are never deeply equal, so if you pass 2 different types you'll always get `false`.

**Array** values are deeply equal when their corresponding elements are deeply equal.

**Struct** values are deeply equal if their corresponding fields, are deeply equal.

**Func** values are deeply equal if both are `nil`; otherwise they are not deeply equal.

**Interface** values are deeply equal if they hold deeply equal concrete values.

**Map** values are deeply equal when all of the following are true:
- they are both `nil` or both non-`nil`
- they have the same length
- they are the same map object or their corresponding keys (matched using Go equality) map to deeply equal values.

**Pointer** values are deeply equal if they are equal using Go's `==` operator or if they point to deeply equal values.

**Slice** values are deeply equal when all of the following are true:
- they are both `nil` or both non-`nil`
- they have the same length,
- they point to the same initial entry of the same underlying array (that is, `&x[0] == &y[0]`) or their corresponding elements (up to length) are deeply equal.

A non-nil empty slice and a `nil` slice (for example, `[]byte{}` and `[]byte(nil)`) are not deeply equal.

Other values - **numbers**, **bools**, **strings**, and **channels** - are deeply equal if they are equal using Go's == operator.

Some inevitable "special" cases worth listing: **it is possible for a value to be unequal to itself**:
- because it is of `func` type
- because it is a floating-point `NaN` value
- because it is an **array**, **struct**, or **interface** containing such a value

Pointer values are always equal to themselves, even if they point at or contain such problematic values, because they compare equal using Go's `==` operator, and that is a sufficient condition to be deeply equal, regardless of content.

The same applies to **slices** and **maps**: if `x` and `y` are the same slice or the same map, they are deeply equal regardless of content.
