---
title       : Pitch for shiny application
subtitle    : Injuries and fatalities in USA by location
author      : Alberto Hevia
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
url: 
   assests: ../assets
hittheme: zenburn           #
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Synopsis

Harmful events have caused many injuries and fatalities in USA in the last years.

This shiny app tries to show the number of injuries and fatalities in a specific location during the last 10 years. 

To do this, information from The National Oceanic
and Atmospheric Administration (NOAA) dataset has been used and filtered to obtain a summary of events in the years between 2000 and 2010. You can obtain more information in:

http://www.nws.noaa.gov

The purpose of this app is to show in a graphic the number of fatalities and injuries in that location and the evolution of them during those years. 



--- .class #id 

## Criteria / Results

There are several options to show the fatalities / injuries evolution. You can choose between the following criteria:

  * Latitude and Longitude. The values by defect are related to Los Angeles.
  * Two dates within you want to restrict the evaluation. By defect the years from 2000 to 2010.
  * The radius in kilometers around the location where you want to evaluate injuries and fatalities. You can find more details on how this calculation was implemented in the following slide.

The results for the above criteria can be displayed as:
  * A graph where it can be seen the total of injures / fatalities in those years and a prediction line model for them.
  * A summary with the total of injuries / fatalities grouped by year.


--- .class #id

## Distance between two locations

The earth is not a plane, so calculation of distance must consider that earh is a circunference, the following function was used:


```r
distance <- function (p1, p2) {
  pr1 <- c(p1[1]*pi/180, p1[2]*pi/180)
  pr2 <- c(p2[1]*pi/180, p2[2]*pi/180)
  dx <- abs(pr1[1]-pr2[1])
  dy <- abs(pr1[2]-pr2[2])
    
  a <- (sin(dx/2)^2 + cos(pr1[1]))*cos(pr2[1])*sin(dy/2)^2
  c <- 2 * atan(sqrt(a)/sqrt(1-a))
  return = (6371 * c)
}
```

--- .class #id

## Final

Therefore the distance between New York (40.70, 74) and Los Angeles (34.05, 118.24) can be calculated as:

```r
p1 <- c(34.05,118.24)
p2 <- c(40.70,74)
print(paste("Kilometers between Los Angeles and New York",round(distance(p1,p2),2)))
```

```
## [1] "Kilometers between Los Angeles and New York 3869.6"
```


And finally, you can evaluate this shiny app in:

http://alberto-hevia-developing-project.shinyapps.io/Developing

    
  
Thanks

