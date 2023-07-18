Use case of CALCULATE

```
CALCULATE(
    [Measure],
    ALL()
)
```

Conditional statements can also be used to manage calculate.

```
IF(
    //condition is true
    ISBLANK([Measure]),
    //then
    BLANK(),
    //else
    CALCULATE(
        [Measure]
    )

)
```
