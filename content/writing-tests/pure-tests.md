---
title: "Pure Unit Tests"
date: 2019-11-21T17:42:10-05:00
draft: false
weight: 1
---

Pure unit tests are simple unit test cases in which "pure" functions are
tested.

Pure functions are those that:

- Do not contain any ["side effects"](https://en.wikipedia.org/wiki/Side_effect_(computer_science))
- Map the same input to the same output no matter how many times they are
invoked.

Here's an example of a simple test of a tax calculator function:

{{<highlight csharp>}}
using FluentAssertions;
using Xunit;
using static NeverendingTeaShop.Application.TeaPriceCalculator;

namespace NeverendingTeaShop.Application.Tests
{
    public class TeaPriceCalculatorTest
    {
        [Fact]
        public void CalculateTaxedPrice_GivenARetailPrice_ReturnsFullPriceWithTaxApplied()
        {
            CalculateTaxedPrice(19.99).Should().Be(21.74);
        }
    }
}
{{</highlight>}}

Frameworks in use to run this test are:

- [Xunit (Test framework)](https://xunit.net/)
- [FluentAssertions (Assertion framework)](https://fluentassertions.com/)
