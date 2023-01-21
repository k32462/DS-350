---
title: "Reducing Gun Deaths"
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





## Reducing Gun Deaths

Fifty Thirty-Eight wrote an article about the gun deaths in The United States of America. Surprisingly, the majority of gun deaths in the states are lost to suicides instead of the common thought of outgoing sources of violence. Furthermore, the vast majority of the suicide victims are also male being at 85%. Within this population, more than half are men older than 45. Continually, back to the proportion of homicides, the majority of the victims are also men. Are there any relationships between the qualities of these attackers? Let's look at the data to find out!

## Visualizing a relationship

Below is a graph of the intent of the attacker in comparison to the education.


::: {.cell}

```{.r .cell-code}
ggplot(guns, aes(x=education, fill=intent)) + 
  geom_bar(position="dodge") +
  labs(x='Race',title='Race & Intent of Gun Violence') +
  theme_bw()
```

::: {.cell-output-display}
![](Reducing_gun_deaths_files/figure-html/unnamed-chunk-2-1.png){width=1200}
:::
:::

## Addressing Groups in Seasons
Below is an info graphic separating the data into groups of seasons, as we look into the race of the attackers concerning homicide & suicide. The patterns of suicide far surpass the rates of homicide as mentioned in the article by fifty thirty eight. However, there is a clear common trend of white men being victims to suicide due to gun violence. Continually, the pattern seems to be slightly lower during winter. Let's look into this further in another graphic.


::: {.cell}

```{.r .cell-code}
ggplot(guns3, aes( x=intent ,
                fill = race,
                by = season)) +
   geom_bar(position='dodge') +
   labs(title='Season in comparison to intent') +
  facet_grid(~ season)
```

::: {.cell-output-display}
![](Reducing_gun_deaths_files/figure-html/unnamed-chunk-3-1.png){width=1200}
:::
:::


Below is a further interpretation of this data, only being white men being victims to suicide. There appears to be a slight trend within the seasons, with winter having the lowest rates and summer having the highest rates. The vast majority of these incidences also occur in the home. Ultimately, we know that the majority of gun incidences are suicide from white men in their home, typically over the summer. 


::: {.cell}

```{.r .cell-code}
ggplot(guns4, aes(x= sex,
                  fill = place,
                  by = season
                    )) +
  geom_bar(position = 'dodge') +
  labs(x='Sex', title='Where and When do these Incidents Occur?') +
  facet_grid(~ season) +
  theme_bw()
```

::: {.cell-output-display}
![](Reducing_gun_deaths_files/figure-html/unnamed-chunk-4-1.png){width=1200}
:::
:::