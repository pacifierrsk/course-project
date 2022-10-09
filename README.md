# course-project
1: address the question of which types of events are most harmful to population health
Calculate the fatalities and injuries seperately

The fatalities:
totFatalities <- aggregate(noaaDF$FATALITIES, by = list(noaaDF$EVTYPE), "sum")
names(totFatalities) <- c("Event", "Fatalities")
totFatalitiesSorted <- totFatalities[order(-totFatalities$Fatalities), ][1:20, ]
totFatalitiesSorted
##                       Event Fatalities
## 834                 TORNADO       5633
## 130          EXCESSIVE HEAT       1903
## 153             FLASH FLOOD        978
## 275                    HEAT        937
## 464               LIGHTNING        816
## 856               TSTM WIND        504
## 170                   FLOOD        470
## 585             RIP CURRENT        368
## 359               HIGH WIND        248
## 19                AVALANCHE        224
## 972            WINTER STORM        206
## 586            RIP CURRENTS        204
## 278               HEAT WAVE        172
## 140            EXTREME COLD        160
## 760       THUNDERSTORM WIND        133
## 310              HEAVY SNOW        127
## 141 EXTREME COLD/WIND CHILL        125
## 676             STRONG WIND        103
## 30                 BLIZZARD        101
## 350               HIGH SURF        101
The injuries:
totInjuries <- aggregate(noaaDF$INJURIES, by = list(noaaDF$EVTYPE), "sum")
names(totInjuries) <- c("Event", "Injuries")
totInjuriesSorted <- totInjuries[order(-totInjuries$Injuries), ][1:20, ]
totInjuriesSorted
##                  Event Injuries
## 834            TORNADO    91346
## 856          TSTM WIND     6957
## 170              FLOOD     6789
## 130     EXCESSIVE HEAT     6525
## 464          LIGHTNING     5230
## 275               HEAT     2100
## 427          ICE STORM     1975
## 153        FLASH FLOOD     1777
## 760  THUNDERSTORM WIND     1488
## 244               HAIL     1361
## 972       WINTER STORM     1321
## 411  HURRICANE/TYPHOON     1275
## 359          HIGH WIND     1137
## 310         HEAVY SNOW     1021
## 957           WILDFIRE      911
## 786 THUNDERSTORM WINDS      908
## 30            BLIZZARD      805
## 188                FOG      734
## 955   WILD/FOREST FIRE      545
## 117         DUST STORM      440
Finally plot both the fatalities and injuries in a single plot:

par(mfrow = c(1, 2), mar = c(10, 4, 2, 2), las = 3, cex = 0.7, cex.main = 1.4, cex.lab = 1.2)
barplot(totFatalitiesSorted$Fatalities, names.arg = totFatalitiesSorted$Event, col = 'red',
        main = 'Top 20 Weather Events for Fatalities', ylab = 'Number of Fatalities')
barplot(totInjuriesSorted$Injuries, names.arg = totInjuriesSorted$Event, col = 'orange',
        main = 'Top 20 Weather Events for Injuries', ylab = 'Number of Injuries')


Thus we see that Tornados cause most deaths and injuries in the U.S. National Oceanic and Atmospheric Administration’s (NOAA) storm database. But Excessive heat causes second most deaths, whereas as far as injuries are conserned second to fourth causes have very similar values.
address the question of which types of events have the greatest economic consequences
Calculate the cost of property and crop damages seperately
The property:
totProperty <- aggregate(noaaDF$PROPDMG, by = list(noaaDF$EVTYPE), "sum")
names(totProperty) <- c("Event", "Property")
totPropertySorted <- totProperty[order(-totProperty$Property), ][1:20, ]
totPropertySorted
##                    Event   Property
## 834              TORNADO 3212258.16
## 153          FLASH FLOOD 1420124.59
## 856            TSTM WIND 1335965.61
## 170                FLOOD  899938.48
## 760    THUNDERSTORM WIND  876844.17
## 244                 HAIL  688693.38
## 464            LIGHTNING  603351.78
## 786   THUNDERSTORM WINDS  446293.18
## 359            HIGH WIND  324731.56
## 972         WINTER STORM  132720.59
## 310           HEAVY SNOW  122251.99
## 957             WILDFIRE   84459.34
## 427            ICE STORM   66000.67
## 676          STRONG WIND   62993.81
## 376           HIGH WINDS   55625.00
## 290           HEAVY RAIN   50842.14
## 848       TROPICAL STORM   48423.68
## 955     WILD/FOREST FIRE   39344.95
## 164       FLASH FLOODING   28497.15
## 919 URBAN/SML STREAM FLD   26051.94
The crop:
totCrop <- aggregate(noaaDF$CROPDMG, by = list(noaaDF$EVTYPE), "sum")
names(totCrop) <- c("Event", "Crop")
totCropSorted <- totCrop[order(-totCrop$Crop), ][1:20, ]
totCropSorted
##                  Event      Crop
## 244               HAIL 579596.28
## 153        FLASH FLOOD 179200.46
## 170              FLOOD 168037.88
## 856          TSTM WIND 109202.60
## 834            TORNADO 100018.52
## 760  THUNDERSTORM WIND  66791.45
## 95             DROUGHT  33898.62
## 786 THUNDERSTORM WINDS  18684.93
## 359          HIGH WIND  17283.21
## 290         HEAVY RAIN  11122.80
## 212       FROST/FREEZE   7034.14
## 140       EXTREME COLD   6121.14
## 848     TROPICAL STORM   5899.12
## 402          HURRICANE   5339.31
## 164     FLASH FLOODING   5126.05
## 411  HURRICANE/TYPHOON   4798.48
## 957           WILDFIRE   4364.20
## 873     TSTM WIND/HAIL   4356.65
## 955   WILD/FOREST FIRE   4189.54
## 464          LIGHTNING   3580.61
Next plot both the cost of property and crop damages in a single plot:

par(mfrow = c(1, 2), mar = c(10, 4, 2, 2), las = 3, cex = 0.7, cex.main = 1.4, cex.lab = 1.2)
barplot(totPropertySorted$Property, names.arg = totPropertySorted$Event, col = 'Brown',
        main = 'Top 20 Weather Events for Property Damage ', ylab = 'Amount of Property Damage', ylim = c(0, 3500000))
barplot(totCropSorted$Crop, names.arg = totCropSorted$Event, col = 'Green',
        main = 'Top 20 Weather Events for Crop Damage', ylab = 'Amount of  Crop Damage', ylim = c(0, 3500000))


Finally the totl damage by adding both costs (property and crop damage)
totTotalCost <- aggregate(noaaDF$CROPDMG+noaaDF$PROPDMG, by = list(noaaDF$EVTYPE), "sum")
names(totTotalCost) <- c("Event", "TotalCost")
totTotalCostSorted <- totTotalCost[order(-totTotalCost$TotalCost), ][1:20, ]
totTotalCostSorted
##                  Event  TotalCost
## 834            TORNADO 3312276.68
## 153        FLASH FLOOD 1599325.05
## 856          TSTM WIND 1445168.21
## 244               HAIL 1268289.66
## 170              FLOOD 1067976.36
## 760  THUNDERSTORM WIND  943635.62
## 464          LIGHTNING  606932.39
## 786 THUNDERSTORM WINDS  464978.11
## 359          HIGH WIND  342014.77
## 972       WINTER STORM  134699.58
## 310         HEAVY SNOW  124417.71
## 957           WILDFIRE   88823.54
## 427          ICE STORM   67689.62
## 676        STRONG WIND   64610.71
## 290         HEAVY RAIN   61964.94
## 376         HIGH WINDS   57384.60
## 848     TROPICAL STORM   54322.80
## 955   WILD/FOREST FIRE   43534.49
## 95             DROUGHT   37997.67
## 164     FLASH FLOODING   33623.20
And a single plot
par(mfrow = c(1,1), mar = c(10, 4, 2, 2), las = 3, cex = 0.7, cex.main = 1.4, cex.lab = 1.2)
barplot(totTotalCostSorted$TotalCost, names.arg = totTotalCostSorted$Event, col = 'Black',
        main = 'Top 20 Weather Events for total Damage ', ylab = 'Amount of total Damage', ylim = c(0, 3500000))


Thus we notice that tornadoes cause most total damage.
the Problem
Instructions Introduction

Storms and other severe weather events can cause both public health and economic problems for communities and municipalities. Many severe events can result in fatalities, injuries, and property damage, and preventing such outcomes to the extent possible is a key concern.

This project involves exploring the U.S. National Oceanic and Atmospheric Administration’s (NOAA) storm database. This database tracks characteristics of major storms and weather events in the United States, including when and where they occur, as well as estimates of any fatalities, injuries, and property damage. Data

The data for this assignment come in the form of a comma-separated-value file compressed via the bzip2 algorithm to reduce its size. You can download the file from the course web site:

Storm Data [47Mb]
There is also some documentation of the database available. Here you will find how some of the variables are constructed/defined.

National Weather Service Storm Data Documentation
National Climatic Data Center Storm Events FAQ
The events in the database start in the year 1950 and end in November 2011. In the earlier years of the database there are generally fewer events recorded, most likely due to a lack of good records. More recent years should be considered more complete. Review criterialess

Has either a (1) valid RPubs URL pointing to a data analysis document for this assignment been submitted; or (2) a complete PDF file presenting the data analysis been uploaded?
Is the document written in English?
Does the analysis include description and justification for any data transformations?
Does the document have a title that briefly summarizes the data analysis?
Does the document have a synopsis that describes and summarizes the data analysis in less than 10 sentences?
Is there a section titled "Data Processing" that describes how the data were loaded into R and processed for analysis?
Is there a section titled "Results" where the main results are presented?
Is there at least one figure in the document that contains a plot?
Are there at most 3 figures in this document?
Does the analysis start from the raw data file (i.e. the original .csv.bz2 file)?
Does the analysis address the question of which types of events are most harmful to population health?
Does the analysis address the question of which types of events have the greatest economic consequences?
Do all the results of the analysis (i.e. figures, tables, numerical summaries) appear to be reproducible?
Do the figure(s) have descriptive captions (i.e. there is a description near the figure of what is happening in the figure)?
As far as you can determine, does it appear that the work submitted for this project is the work of the student who submitted it?
Assignmentless Assignment

The basic goal of this assignment is to explore the NOAA Storm Database and answer some basic questions about severe weather events. You must use the database to answer the questions below and show the code for your entire analysis. Your analysis can consist of tables, figures, or other summaries. You may use any R package you want to support your analysis. Questions

Your data analysis must address the following questions:

Across the United States, which types of events (as indicated in the EVTYPE variable) are most harmful with respect to population health?
Across the United States, which types of events have the greatest economic consequences?
Consider writing your report as if it were to be read by a government or municipal manager who might be responsible for preparing for severe weather events and will need to prioritize resources for different types of events. However, there is no need to make any specific recommendations in your report. Requirements

For this assignment you will need some specific tools

RStudio: You will need RStudio to publish your completed analysis document to RPubs. You can also use RStudio to edit/write your analysis.
knitr: You will need the knitr package in order to compile your R Markdown document and convert it to HTML
Document Layout

Language: Your document should be written in English.
Title: Your document should have a title that briefly summarizes your data analysis
Synopsis: Immediately after the title, there should be a synopsis which describes and summarizes your analysis in at most 10 complete sentences.
There should be a section titled Data Processing which describes (in words and code) how the data were loaded into R and processed for analysis. In particular, your analysis must start from the raw CSV file containing the data. You cannot do any preprocessing outside the document. If preprocessing is time-consuming you may consider using the cache = TRUE option for certain code chunks.
There should be a section titled Results in which your results are presented.
You may have other sections in your analysis, but Data Processing and Results are required.
The analysis document must have at least one figure containing a plot.
Your analysis must have no more than three figures. Figures may have multiple plots in them (i.e. panel plots), but there cannot be more than three figures total.
You must show all your code for the work in your analysis document. This may make the document a bit verbose, but that is okay. In general, you should ensure that echo = TRUE for every code chunk (this is the default setting in knitr.
