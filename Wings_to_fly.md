---
title: "Wings to Fly"
editor: visual
format:
  html:
    code-fold: true
    code-line-numbers: true
execute:
  keep-md: true
---






## For each origin airport (JFK, EWR, LGA), which airline has the lowest 75th percentile of delay time for flights scheduled to leave earlier than noon?


::: {.cell}

```{.r .cell-code}
flights2 <- flights %>%
  filter(sched_dep_time < 1200) %>%
  drop_na(dep_delay)

flights3 <- flights2%>%
  filter(origin == 'EWR')
flights4 <- flights2 %>%
  filter(origin == 'JFK')
flights5 <- flights2%>%
  filter(origin == 'LGA')
```
:::

::: {.cell}

```{.r .cell-code}
ggplot(flights2, aes(x=carrier, 
                     y=dep_delay, 
                     by=origin,
                     )) +
  geom_boxplot(outlier.shape = NA) +
  facet_wrap(vars(origin)) +
  labs(x='Carrier', y='Departure Delay Time', title='Departure Delay Time by Carrier') +
  ylim(c(-15,15))
```

::: {.cell-output-display}
![](Wings_to_fly_files/figure-html/unnamed-chunk-3-1.png){width=672}
:::
:::


Above shows a five number summary for each carrier within each airport. Outliers were also excluded, however this will not change the data since we are looking for the smallest departure delay time. For EWR, the lowest 75% percentile for flights scheduled to leave before noon are 9E & US with a 75% of -2. For JFK, the the lowest 75% percentile for flights scheduled to leave before noon are DL & HA with a 75% of -1. Lastly for LGA, the lowest 75% percentile for flights scheduled to leave before noon is US with a 75% of -3.

## Which origin airport is best to minimize my chances of a late arrival when I am using Delta Airlines?


::: {.cell}

```{.r .cell-code}
delta.flights <- flights %>%
  filter(carrier == 'DL')

ggplot(data = delta.flights, 
       mapping = aes(x=carrier, 
                     y = arr_delay,
                     color = origin)) +
  geom_point() + 
  labs(x= "Delta Airlines", # changes the name of the x-axis
       y = "Delay in Arrival Times") +  # changes the name of the y-axis
  theme_bw() +
  facet_wrap(vars(as.factor(origin))) # These lines splits the chart into several bars
```

::: {.cell-output-display}
![](Wings_to_fly_files/figure-html/unnamed-chunk-4-1.png){width=672}
:::
:::


The visualization above shows the delay in departure times. It appears that the mean delay in arrival times is highest for the LGA airport based on the density of the graph. However to further understand the values, below is a summary table of the arrival delay times.


::: {.cell}

```{.r .cell-code}
delta.flights %>%
  drop_na(arr_delay) %>%
  group_by(origin) %>%
  summarise(mean=mean(arr_delay)) %>%
  pander()
```

::: {.cell-output-display}
-----------------
 origin    mean  
-------- --------
  EWR      8.78  

  JFK     -2.379 

  LGA     3.928  
-----------------
:::
:::


Clearly shown above, the JFK airport has the lowest average delay time for Delta Airlines. This means that the JFK airport is (on average) 2 minutes earlier than the anticipated arrival time when it comes to Delta Airlines. Therefore, the **JFK** airport is best at minimizing late arrival times.