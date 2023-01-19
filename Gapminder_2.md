---
title: "Gapminder  2"
editor: visual
format:
  html:
    code-fold: true
    code-line-numbers: true
    fig-width: 12.5
    fig-height: 7.5

execute:
  keep-md: true
---



## Gapminder




::: {.cell}

```{.r .cell-code}
thegap2 <- gapminder %>%
  filter(country != 'Kuwait') %>%
  mutate(pop1 = pop/100000) %>%
    group_by(year, continent) %>% 
  summarise(gdp_mean = weighted.mean(gdpPercap, pop), country, gdpPercap, pop)
```

::: {.cell-output .cell-output-stderr}
```
`summarise()` has grouped output by 'year', 'continent'. You can override using
the `.groups` argument.
```
:::
:::

::: {.cell}

```{.r .cell-code}
ggplot(thegap2, aes(
  x = year,
  y = gdpPercap,
  group = country),
  size = (pop/100000)) +
geom_line(aes(color = continent)) +
 geom_point(aes(color = continent, size = (pop / 100000))) +
geom_line(aes(x = year, y = gdp_mean)) +
geom_point(aes(x = year, y = gdp_mean, size = (pop / 100000))) +
theme_bw() +
labs(x = "Year" , y ="GDP per Capita", size = "Population (100K)") +
 facet_grid(~ continent) 
```

::: {.cell-output-display}
![](Gapminder_2_files/figure-html/unnamed-chunk-3-1.png){width=1200}
:::
:::