The Chelsea Premier League Predictor Project
========================================================
author: Shailee Shrestha
date: May 23, 2016

========================================================
* Chelsea have been dominant in the Premier League this season. They are 3 points clear and have a game in hand, with just 10 games left.
* However, they still have some tricky games coming up including Man Utd and Arsenal.
* Football fans would be able to see easily how many points Chelsea will end up on by predicting the results of their remaining games.
* They can then see how many points their team would still require to win the league.
* Something like this could be expanded to include all remaining Premier League fixtures.

========================================================
## The ui.R file

* It uses the fluidPage layout.
* Then, to ensure all the information is not crammed onto one page, the tabsetPanel has been used to effectively put multiple pages all on one page.
* Radio buttons have been used instead of a select menu. It will be easy for users to select the choice.


```r
library(shiny)
radioButtons("southampton", "16/03 - Chelsea vs Southampton",
                                              c("Chelsea Win" = "win",
                                                "Draw" = "draw",
                                                "Chelsea Loss" = "loss"), inline=TRUE)
```

* The results are just shown as lines of text. The presentation here is very basic but the information is still clearly conveyed.


========================================================

## The server.R file

* Makes use of the renderDataTable function. This means that the results can be stored in server.R as a data frame for easy R calculation.


```r
output$lTable <- renderDataTable(leagueTable, options=list(paging = FALSE, 
                                                           searching = FALSE))
```

* Turning a radio buttin input from text into a number is not trivial and the switch function must be used.


```r
southampton <- reactive({
                        switch(input$southampton, "win" = 3, 
                                                  "draw" = 1, 
                                                  "loss" = 0)
                })
```

========================================================

## The Calculations

* The points are assigned to each fixture similarly to this. Then Chelsea's total points are calculated:

```r
southampton <- 3; hull <- 1; stoke <- 3; qpr <- 3; manutd <- 0; arsenal <- 1; 
leicester <- 3; crystalpalace <- 3; liverpool <- 1; westbrom <- 3; sunderland <- 3
```


```r
totPoints <- 63 + southampton + hull + stoke + qpr + manutd + arsenal + leicester + 
        crystalpalace + liverpool + westbrom + sunderland; totPoints
```

```
[1] 87
```
* And then the points another team (eg Southampton) requires to win can be calculated

```r
southamptonNeed <- 64 + totPoints - 28; southamptonNeed
```

```
[1] 123
```

