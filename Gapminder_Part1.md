---
title: "Gapminder"
editor: visual
format:
  html:
    code-fold: true
    code-line-numbers: true

execute:
  keep-md: true
---



## Gapminder Code




::: {.cell}

```{.r .cell-code}
thegap <- gapminder |>
  filter(country != 'Kuwait') |>
 mutate(lifeExp = as.numeric(lifeExp)) |>
 mutate(gdpPercap = as.numeric(gdpPercap)) |>
  mutate(`Population (100k)` = pop/100000 )

# This was to filter the data to better fit the visualization
```
:::

::: {.cell}

```{.r .cell-code}
ggplot(data = thegap, 
       mapping = aes(x=lifeExp, 
                     y = gdpPercap,
                     color = continent,
                     size = `Population (100k)`)) +
  geom_point() + 
  labs(x= "Life Expectancy (Years)", # changes the name of the x-axis
       y = "GDP per Capita") +  # changes the name of the y-axis
  theme_bw() +
  facet_wrap(vars(as.factor(year))) + # These lines splits the chart into several bars
  facet_grid(. ~ year) + # this changes the charts to be horizontal
  scale_y_continuous(trans = "sqrt") # this adjusts the scale of the y-axis
```

::: {.cell-output-display}
![](Gapminder_Part1_files/figure-html/unnamed-chunk-3-1.png){width=672}
:::
:::
