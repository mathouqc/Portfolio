---
title: Testing Post
author: Mathias Boudreau
pubDatetime: 2025-02-20T00:00:00Z
featured: false
draft: false
tags:
  - Demo
  - Astro
description: "A post to test different features of markdown in Astro."
---

This document is made to test different features of markdown in Astro.

## Table of contents

# h1 Heading

## h2 Heading

### h3 Heading

#### h4 Heading

##### h5 Heading

###### h6 Heading

## Horizontal Rules

---

---

---

## Emphasis

**This is bold text**

_This is italic text_

~~Strikethrough~~

## Blockquotes

> Blockquotes can also be nested...
>
> > ...by using additional greater-than signs right next to each other...
> >
> > > ...or with spaces between arrows.

## Lists

Unordered

- Create a list by starting a line with `+`, `-`, or `*`
- Sub-lists are made by indenting 2 spaces:
  - Marker character change forces new list start:
    - Ac tristique libero volutpat at
    * Facilisis in pretium nisl aliquet
    - Nulla volutpat aliquam velit
- Very easy!

Ordered

1. Lorem ipsum dolor sit amet
2. Consectetur adipiscing elit
3. Integer molestie lorem at massa

4. You can use sequential numbers...
5. ...or keep all the numbers as `1.`

Start numbering with offset:

57. foo
1. bar

## Code

Inline `code`

Indented code

    // Some comments
    line 1 of code
    line 2 of code
    line 3 of code

Block code "fences"

```
Sample text here...
```

### Syntax highlighting

Javascript :

```js
var foo = function (bar) {
  return bar++;
};

console.log(foo(5));

new Promise((resolve, reject) => {
  // asynchronous operation

  // then in case of success
  resolve();
  // or
  reject("failure reason");
});

const defer = (fn, ...args) => setTimeout(fn, 1, ...args);

defer(console.log, "a"), console.log("b"); // logs 'b' then 'a'
```

```js
/*
 * RLE (Run Length Encoding) is a simple form of data compression.
 * The basic idea is to represent repeated successive characters as a single count and character.
 * For example, the string "AAAABBBCCDAA" would be encoded as "4A3B2C1D2A".
 *
 * @author - [ddaniel27](https://github.com/ddaniel27)
 */

function Compress(str) {
  let compressed = "";
  let count = 1;

  for (let i = 0; i < str.length; i++) {
    if (str[i] !== str[i + 1]) {
      compressed += count + str[i];
      count = 1;
      continue;
    }

    count++;
  }

  return compressed;
}

function Decompress(str) {
  let decompressed = "";
  let match = [...str.matchAll(/(\d+)(\D)/g)]; // match all groups of digits followed by a non-digit character

  match.forEach(item => {
    let [count, char] = [item[1], item[2]];
    decompressed += char.repeat(count);
  });

  return decompressed;
}

export { Compress, Decompress };
```

```js
/*
 * RLE (Run Length Encoding) is a simple form of data compression.
 * The basic idea is to represent repeated successive characters as a single count and character.
 * For example, the string "AAAABBBCCDAA" would be encoded as "4A3B2C1D2A".
 *
 * @author - [ddaniel27](https://github.com/ddaniel27)
 */

function Compress(str) {
  let compressed = "";
  let count = 1;

  for (let i = 0; i < str.length; i++) {
    if (str[i] !== str[i + 1]) {
      compressed += count + str[i];
      count = 1;
      continue;
    }

    count++;
  }

  return compressed;
}

function Decompress(str) {
  let decompressed = "";
  let match = [...str.matchAll(/(\d+)(\D)/g)]; // match all groups of digits followed by a non-digit character

  match.forEach(item => {
    let [count, char] = [item[1], item[2]];
    decompressed += char.repeat(count);
  });

  return decompressed;
}

export { Compress, Decompress };
```

```js
class Car {
  constructor(make, model, color) {
    this.make = make;
    this.model = model;
    this.color = color;
  }

  setMake(make) {
    this.make = make;
    // NOTE: Returning this for chaining
    return this;
  }

  setModel(model) {
    this.model = model;
    // NOTE: Returning this for chaining
    return this;
  }

  setColor(color) {
    this.color = color;
    // NOTE: Returning this for chaining
    return this;
  }

  save() {
    console.log(this.make, this.model, this.color);
    // NOTE: Returning this for chaining
    return this;
  }
}

const car = new Car("Ford", "F-150", "red").setColor("pink").save();
```

```ts
import { PriorityQueue } from "../data_structures/heap/heap";
/**
 * @function dijkstra
 * @description Compute the shortest path from a source node to all other nodes. The input graph is in adjacency list form. It is a multidimensional array of edges. graph[i] holds the edges for the i'th node. Each edge is a 2-tuple where the 0'th item is the destination node, and the 1'th item is the edge weight.
 * @Complexity_Analysis
 * Time complexity: O((V+E)*log(V)). For fully connected graphs, it is O(E*log(V)).
 * Space Complexity: O(V)
 * @param {[number, number][][]} graph - The graph in adjacency list form
 * @param {number} start - The source node
 * @return {number[]} - The shortest path to each node
 * @see https://en.wikipedia.org/wiki/Dijkstra%27s_algorithm
 */
export const dijkstra = (
  graph: [number, number][][],
  start: number
): number[] => {
  // We use a priority queue to make sure we always visit the closest node. The
  // queue makes comparisons based on path weights.
  const priorityQueue = new PriorityQueue(
    (a: [number, number]) => {
      return a[0];
    },
    graph.length,
    (a: [number, number], b: [number, number]) => {
      return a[1] < b[1];
    }
  );
  priorityQueue.insert([start, 0]);
  // We save the shortest distance to each node in `distances`. If a node is
  // unreachable from the start node, its distance is Infinity.
  const distances = Array(graph.length).fill(Infinity);
  distances[start] = 0;

  while (priorityQueue.size() > 0) {
    const node = priorityQueue.extract()[0];
    graph[node].forEach(([child, weight]) => {
      const new_distance = distances[node] + weight;
      if (new_distance < distances[child]) {
        // Found a new shortest path to child node. Record its distance and add child to the queue.
        // If the child already exists in the queue, the priority will be updated. This will make sure the queue will be at most size V (number of vertices).
        priorityQueue.increasePriority(child, [child, weight]);
        distances[child] = new_distance;
      }
    });
  }

  return distances;
};
```

C# code

```cs
#region Studio Style
class Program : IThemeable
{
    static int _I = 1;
    delegate void DoSomething();

    /// <summary>
    /// The quick brown fox jumps over the lazy dog
    /// THE QUICK BROWN FOX JUMPS OVER THE LAZY DOG
    /// </summary>
    static void Main(string[] args)
    {
        string normalStr = "The time now is approximately " + DateTime.Now;
        Uri Illegal1Uri = new Uri("http://packmyboxwith/jugs.html?q=five-dozen&t=liquor");
        Regex OperatorRegex = new Regex(@"S#$", RegexOptions.IgnorePatternWhitespace);

        for (int O = 0; O < 123456789; O++)
        {
            _I += (O % 3) * ((O / 1) ^ 2) - 5;
            if (!OperatorRegex.IsMatch(Illegal1Uri.ToString()))
            {
                // no idea what this does!?
                Console.WriteLine(Illegal1Uri + normalStr);

            }
        }
    }
}
#endregion
```

C++ code

```cpp
#pragma once
#include "Header.h" // Contains ISomeClass and includes <vector>, <list>
#define PREPROCESSOR_DEFINITION

namespace MyNamespace
{
void GlobalFunction() {}
bool GlobalVariable = true;
/// <summary>
/// The quick brown fox jumps over the lazy dog
/// THE QUICK BROWN FOX JUMPS OVER THE LAZY DOG
/// </summary>
class SomeClass    : public ISomeClass
{
public:
    enum SomeEnum
    {
        ENUM_0 = 0,
        ENUM_1 = 1
    };
    struct SomeData
    {
        int m_Integer;
        float m_Float;
    };

    SomeClass() { m_Data = new SomeData(); }
    ~SomeClass() { delete m_Data; m_Data = 0; }

    static int DoSomethingStatic( int _Arg0, float _Arg1 )
    {
        std::vector<float> Vec = std::vector<float>();

        float f = 0.0f;
        for (int i = 0; i < _Arg0; ++i)
        {
            if (i % 3 != 0)
            {
                f += _Arg1;
                Vec.push_back(f);
            }
        }
        return Vec.size();
    }

    template<class _T>
    int DoSomethingNonStatic() const;
private:
    SomeData* m_Data;
    static SomeData* m_StaticData;
};

}    // MyNamespace
```

```xml
<?xml version="1.0" encoding="utf-8" ?>
<!-- this is an example XML file -->
<people xmlns:x="http://studiostyles.info">
  <person name="Jim Jones" ID="27">
    <email html="yes">jim@example.invalid</email>
    <address>
      <post>123 Example St, &#160;South Brisbane</post>
      <city>Brisbane</city>
    </address>
    <x:comments>
    <![CDATA[ See? Data. Don't worry about this <tag>. ]]>
    </x:comments>
  </person>
</people>
```

## Tables

| Option | Description                                                               |
| ------ | ------------------------------------------------------------------------- |
| data   | path to data files to supply the data that will be passed into templates. |
| engine | engine to be used for processing templates. Handlebars is the default.    |
| ext    | extension to be used for dest files.                                      |

## Links

[link text](http://dev.nodeca.com)

[link with title](http://nodeca.github.io/pica/demo/ "title text!")

Autoconverted link https://github.com/nodeca/pica

## Images

![Minion](https://octodex.github.com/images/minion.png)

With title

![Stormtroopocat](https://octodex.github.com/images/stormtroopocat.jpg "The Stormtroopocat")

Sized image

<img src="https://octodex.github.com/images/dojocat.jpg" alt="Dojocat" width=200>

## Equations

### Inline Equations

Inline equations are written between single dollar signs `$...$`. Here are some examples:

1. The famous mass-energy equivalence formula: $E = mc^2$
2. The quadratic formula: $x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}$
3. Euler's identity: $e^{i\pi} + 1 = 0$

### Block Equations

For more complex equations or when you want the equation to be displayed on its own line, use double dollar signs `$$...$$`:

The Gaussian integral:

$$
\int_{-\infty}^{\infty} e^{-x^2} dx = \sqrt{\pi}
$$

The definition of the Riemann zeta function:

$$
\zeta(s) = \sum_{n=1}^{\infty} \frac{1}{n^s}
$$

Maxwell's equations in differential form:

$$
\begin{aligned}
\nabla \cdot \mathbf{E} &= \frac{\rho}{\varepsilon_0} \\
\nabla \cdot \mathbf{B} &= 0 \\
\nabla \times \mathbf{E} &= -\frac{\partial \mathbf{B}}{\partial t} \\
\nabla \times \mathbf{B} &= \mu_0\left(\mathbf{J} + \varepsilon_0 \frac{\partial \mathbf{E}}{\partial t}\right)
\end{aligned}
$$

### Using Mathematical Symbols

LaTeX provides a wide range of mathematical symbols:

- Greek letters: $\alpha$, $\beta$, $\gamma$, $\delta$, $\epsilon$, $\pi$
- Operators: $\sum$, $\prod$, $\int$, $\partial$, $\nabla$
- Relations: $\leq$, $\geq$, $\approx$, $\sim$, $\propto$
- Logical symbols: $\forall$, $\exists$, $\neg$, $\wedge$, $\vee$
