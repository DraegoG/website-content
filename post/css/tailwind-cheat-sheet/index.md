---
title: "The Tailwind Cheat Sheet"
description: "Reference list of common CSS properties you'll want to use in Tailwind, and their relative classes"
date: 2018-07-09T07:06:29+02:00
tags: css
---

I wrote this cheat sheet because I find myself constantly referencing the Tailwind docs to remind a particular class (I'm starting out and I don't have muscle memory yet for it)

Here are the things I use the most.

<!-- TOC -->

- [Margin and Padding](#margin-and-padding)
- [Width](#width)
- [Max Width](#max-width)
- [Min width](#min-width)
- [Font Family](#font-family)
- [Font Size](#font-size)
- [Font weight](#font-weight)
- [Colors](#colors)
- [Text color](#text-color)
- [Background color](#background-color)
- [Line Height](#line-height)
- [Flexbox](#flexbox)
  - [Container](#container)
  - [Items](#items)
    - [Direction](#direction)
    - [Wrapping](#wrapping)
    - [Align items](#align-items)
    - [Align content](#align-content)
    - [Align self](#align-self)
    - [Justify content](#justify-content)
    - [Flex, grow, shrink](#flex-grow-shrink)
- [Modifiers](#modifiers)
  - [Hover](#hover)

<!-- /TOC -->



## Margin and Padding

Compose those 3 tables. Add a dash before the value (e.g. `pt-2`, `m-auto`)

Symbol | Description
---------|----------
 `p` | Padding
 `m` | Margin
 `-m` | Negative margin

Symbol | Description
---------|----------
t | Top
r | Right
b | Bottom
l | Left
x | Horizontal
y | Vertical

Value | Description
---------|----------
0 | `0`
1 | `0.25rem`
2 | `0.5rem`
3 | `0.75rem`
4 | `1rem`
5 | `1.25rem`
6 | `1.5rem`
8 | `2rem`
10 | `2.5rem`
12 | `3rem`
16 | `4rem`
20 | `5rem`
24 | `6rem`
32 | `8rem`
px | `1px`
auto | `auto`

## Width

Class | CSS
---------|----------
w-1 | `width: 0.25rem`
w-2 | `width: 0.5rem`
w-3 | `width: 0.75rem`
w-4 | `width: 1rem`
w-6 | `width: 1.5rem`
w-8 | `width: 2rem`
w-10 | `width: 2.5rem`
w-12 | `width: 3rem`
w-16 | `width: 4rem`
w-24 | `width: 6rem`
w-32 | `width: 8rem`
w-48 | `width: 12rem`
w-64 | `width: 16rem`
w-auto | `width: auto`
w-px | `width: 1px`
w-1/2 | `width: 50%`
w-1/3 | `width: 33.33333%`
w-2/3 | `width: 66.66667%`
w-1/4 | `width: 25%`
w-3/4 | `width: 75%`
w-1/5 | `width: 20%`
w-2/5 | `width: 40%`
w-3/5 | `width: 60%`
w-4/5 | `width: 80%`
w-1/6 | `width: 16.66667%`
w-5/6 | `width: 83.33333%`
w-full | `width: 100%`
w-screen | `width: 100vw`

## Max Width

Class | CSS
---------|----------
max-w-xs | `max-width: 20rem`
max-w-sm | `max-width: 30rem`
max-w-md | `max-width: 40rem`
max-w-lg | `max-width: 50rem`
max-w-xl | `max-width: 60rem`
max-w-2xl | `max-width: 70rem`
max-w-3xl | `max-width: 80rem`
max-w-4xl | `max-width: 90rem`
max-w-5xl | `max-width: 100rem`
max-w-full | `max-width: 100%`

## Min width

Class | CSS
---------|----------
min-w-0 | `min-width: 0`
min-w-full | `min-width: 100%`

## Font Family

Class | CSS
---------|----------
font-sans |	`font-family: system-ui, BlinkMacSystemFont, -apple-system, Segoe UI, Roboto, Oxygen, Ubuntu, Cantarell, Fira Sans, Droid Sans, Helvetica Neue, sans-serif;`
font-serif | 	`font-family: Constantia, Lucida Bright, Lucidabright, Lucida Serif, Lucida, DejaVu Serif, Bitstream Vera Serif, Liberation Serif, Georgia, serif;`
font-mono |	`font-family: Menlo, Monaco, Consolas, Liberation Mono, Courier New, monospace;`

## Font Size

Class | CSS
---------|----------
text-xs | `font-size: .75rem`
text-sm | `font-size: .875rem`
text-base | `font-size: 1rem`
text-lg | `font-size: 1.125rem`
text-xl | `font-size: 1.25rem`
text-2xl | `font-size: 1.5rem`
text-3xl | `font-size: 1.875rem`
text-4xl | `font-size: 2.25rem`
text-5xl | `font-size: 3rem`

## Font weight

Class | CSS
---------|----------
font-hairline |  `font-weight: 100`
font-thin |  `font-weight: 200`
font-light |  `font-weight: 300`
font-normal |  `font-weight: 400`
font-medium |  `font-weight: 500`
font-semibold |  `font-weight: 600`
font-bold |  `font-weight: 700`
font-extrabold |  `font-weight: 800`
font-black |  `font-weight: 900`

## Colors

Class | CSS
---------|----------
transparent |	`color: transparent`
black	| `color: #22292f`
grey-darkest	| `color: #3d4852`
grey-darker	| `color: #606f7b`
grey-dark	| `color: #8795a1`
grey	| `color: #b8c2cc`
grey-light	| `color: #dae1e7`
grey-lighter	| `color: #f1f5f8`
grey-lightest	| `color: #f8fafc`
white	| `color: #ffffff`
red-darkest	| `color: #3b0d0c`
red-darker	| `color: #621b18`
red-dark	| `color: #cc1f1a`
red	| `color: #e3342f`
red-light	| `color: #ef5753`
red-lighter	| `color: #f9acaa`
red-lightest	| `color: #fcebea`
orange-darkest	| `color: #462a16`
orange-darker	| `color: #613b1f`
orange-dark	| `color: #de751f`
orange	| `color: #f6993f`
orange-light	| `color: #faad63`
orange-lighter	| `color: #fcd9b6`
orange-lightest	| `color: #fff5eb`
yellow-darkest	| `color: #453411`
yellow-darker	| `color: #684f1d`
yellow-dark	| `color: #f2d024`
yellow	| `color: #ffed4a`
yellow-light	| `color: #fff382`
yellow-lighter	| `color: #fff9c2`
yellow-lightest	| `color: #fcfbeb`
green-darkest	| `color: #0f2f21`
green-darker	| `color: #1a4731`
green-dark	| `color: #1f9d55`
green	| `color: #38c172`
green-light	| `color: #51d88a`
green-lighter	| `color: #a2f5bf`
green-lightest	| `color: #e3fcec`
teal-darkest	| `color: #0d3331`
teal-darker	| `color: #20504f`
teal-dark	| `color: #38a89d`
teal	| `color: #4dc0b5`
teal-light	| `color: #64d5ca`
teal-lighter	| `color: #a0f0ed`
teal-lightest	| `color: #e8fffe`
blue-darkest	| `color: #12283a`
blue-darker	| `color: #1c3d5a`
blue-dark	| `color: #2779bd`
blue	| `color: #3490dc`
blue-light	| `color: #6cb2eb`
blue-lighter	| `color: #bcdefa`
blue-lightest	| `color: #eff8ff`
indigo-darkest	| `color: #191e38`
indigo-darker	| `color: #2f365f`
indigo-dark	| `color: #5661b3`
indigo	| `color: #6574cd`
indigo-light	| `color: #7886d7`
indigo-lighter	| `color: #b2b7ff`
indigo-lightest	| `color: #e6e8ff`
purple-darkest	| `color: #21183c`
purple-darker	| `color: #382b5f`
purple-dark	| `color: #794acf`
purple	| `color: #9561e2`
purple-light	| `color: #a779e9`
purple-lighter	| `color: #d6bbfc`
purple-lightest	| `color: #f3ebff`
pink-darkest	| `color: #451225`
pink-darker	| `color: #6f213f`
pink-dark	| `color: #eb5286`
pink	| `color: #f66d9b`
pink-light	| `color: #fa7ea8`
pink-lighter	| `color: #ffbbca`
pink-lightest	| `color: #ffebef`

## Text color

Prepend `text-` to any color

## Background color

Prepend `bg-` to any color

## Center text

Use `text-center`

## Line Height

Class | CSS
---------|----------
.leading-none | `line-height: 1`
.leading-tight | `line-height: 1.25`
.leading-normal | `line-height: 1.5`
.leading-loose | `line-height: 2`

## Flexbox

### Container

Class | CSS
---------|----------
flex | `display: flex`
inline-flex | `display: inline-flex`

### Items

#### Direction

Class | CSS
---------|----------
flex-row | `flex-direction: row`
flex-row-reverse | `flex-direction: row-reverse`
flex-col | `flex-direction: column`
flex-col-reverse | `flex-direction: column-reverse`

#### Wrapping

Class | CSS
---------|----------
flex-no-wrap | `flex-wrap: nowrap`
flex-wrap | `flex-wrap: wrap`
flex-wrap-reverse | `flex-wrap: wrap-reverse`

#### Align items

Class | CSS
---------|----------
items-stretch | `align-items: stretch`
items-start | `align-items: flex-start`
items-center | `align-items: center`
items-end | `align-items: flex-end`
items-baseline | `align-items: baseline`

#### Align content

Class | CSS
---------|----------
content-start | `align-content: flex-start`
content-center | `align-content: center`
content-end | `align-content: flex-end`
content-between | `align-content: space-between`
content-around | `align-content: space-around`

#### Align self

Class | CSS
---------|----------
self-auto | `align-self: auto`
self-start | `align-self: flex-start`
self-center | `align-self: center`
self-end | `align-self: flex-end`
self-stretch | `align-self: stretch`

#### Justify content

Class | CSS
---------|----------
justify-start | `justify-content: flex-start`
justify-center | `justify-content: center`
justify-end | `justify-content: flex-end`
justify-between | `justify-content: space-between`
justify-around | `justify-content: space-around`

#### Flex, grow, shrink

Class | CSS
---------|----------
flex-initial | `flex: initial`
flex-1 | `flex: 1`
flex-auto | `flex: auto`
flex-none | `flex: none`
flex-grow | `flex-grow: 1`
flex-shrink | `flex-shrink: 1`
flex-no-grow | `flex-grow: 0`
flex-no-shrink | `flex-shrink: 0`

## Modifiers

### Hover

`hover:`
