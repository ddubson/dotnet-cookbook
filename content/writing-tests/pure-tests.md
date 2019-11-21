---
title: "Pure Unit Tests"
date: 2019-11-21T17:42:10-05:00
draft: true
weight: 1
---

Pure unit tests are simple unit test cases in which "pure" functions are
tested.

Pure functions are those that do not trigger "side effects", map the same
input to the same output no matter how many times they are invoked.

Here's an example of a simple test of a tax calculator function:

```csharp
using FluentAssertions;
using Xunit;
using static GoodProduct.Application.ProductPriceCalculator;

namespace GoodProduct.Application.Tests
{
    public class ProductPriceCalculatorTest
    {
        [Fact]
        public void CalculateTax_GivenARetailPrice_ReturnsFullPriceWithTaxApplied()
        {
            CalculateTax(19.99).Should().Be(21.74);
        }
    }
}
```
