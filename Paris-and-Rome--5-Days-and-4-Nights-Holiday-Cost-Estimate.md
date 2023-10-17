Paris and Rome: 5 Days and 4 Nights Holiday Cost Estimate
================
A.M. Simon

#### *Overview:*

*This R document is a budgeting visual guide and comparison for a
five-day tour and four-night stay in Paris, France and in Rome, Italy.
The figures indicated here are based on the costs indicated in the 2023
pages directly (and officially) related to the respective cities’
transportation, travel, and popular tourist attractions. Due to various
economic factors (inflation, tourist popularity, etc.) that may change
the accuracy of the data with time, fellow travelers are encouraged to
always check and compare current costs for an efficient
travel-budgeting. For those who aren't concerned about the R codes behind the graphs and computations, feel free to scroll past the code sections and refer to the tables or graphs displayed under it :)*

HTML view: <https://rpubs.com/A_M_S/ParisvsRome_Rproject23>

> ## Contents:
>
> 1.  **Average Lodging Cost for 4 Nights: Paris and Rome**
>
> 2.  **Top 10 Tourist Sites and their Entrance Fees as of the year
>     2023: Paris and Rome**
>
> 3.  **Average Travel Expenses for 5 days: Paris and Rome**
>
> 4.  **OVERALL Holiday Tour Cost: Paris or Rome? Paris AND Rome?**
>
> 5.  **Data Sources and References**
>
> 6.  **GitHub Link for this Project**

### 1. Average Lodging Cost for 4 Nights: Paris and Rome

For a **quick visual comparison of the average costs to stay at each
city**, here’s a column graph:

``` r
ALL_Paris_Lodging <- (129 * 4)

ALL_Rome_Lodging <- (103 * 4)


Lodging_Summary2 <- data.frame(
  City_Hotel = c("Paris", "Rome"),
  Cost.4.Nights= c(ALL_Paris_Lodging, ALL_Rome_Lodging)
)

ggplot(data = Lodging_Summary2) +
  geom_col(mapping = aes(x = City_Hotel, y = Cost.4.Nights, fill = City_Hotel)) +
  labs(
    x = "Cities",
    y = "Cost for 4 nights stay",
    title = "Comparison of Total Average Lodging Expenses",
    subtitle = "4 Nights in Paris vs. 4 Nights in Rome",
    caption = "The average price per night is based on the average 
    of the midrange hotel rates for the respective cities; where
    Paris= 129 Euros/night and Rome= 103 Euros/night."
  )
```

![](Paris-and-Rome--5-Days-and-4-Nights-Holiday-Cost-Estimate_files/figure-gfm/Graph:%204%20Nights_Paris%20vs%20Rome-1.png)<!-- -->

The average price per night for a **mid-priced hotel** in Paris is at
**129 USD** while in Rome it is at **103 USD**. Here’s a quick break
down for the average cost of a **four-night** stay in each city, and if
your budget allows it, the average total for staying at both is:

``` r
ALL_LodgingCosts <- sum(Holiday$Average.Lodging.Cost.Per.Night) - (129 + 103)  #I made a spreadsheet composed of 5 nights stay, but     in order to even out the 5-day Holiday in Paris vs. 5-day Holiday in Rome comparison, I decided to deduct one night from each city  (thus the  129-103 subtraction from the sum of the Average lodging cost per night column)

ALL_Paris_Lodging <- (129 * 4)

ALL_Rome_Lodging <- (103 * 4)

Lodging_Summary1 <- data.frame(
  City_ = c("Paris", "Rome", "Paris AND Rome"),
  Cost_4_Nights= c(ALL_Paris_Lodging, ALL_Rome_Lodging, ALL_LodgingCosts))
print (Lodging_Summary1)
```

    ##            City_ Cost_4_Nights
    ## 1          Paris           516
    ## 2           Rome           412
    ## 3 Paris AND Rome           928

### 2. Top 10 Tourist Sites and their Entrance Fees as of the year 2023: Paris and Rome

Below is a list of the **Top 10 Tourist Sites for Paris and Rome.** *If
you’re viewing this in a narrow screen, don’t forget to click the arrow
“\>” to the right of the column header to view the rest of the
table/list;*

``` r
selected_columns <- Holiday[, c("X10.Most.Popular.Tourist.Sites_Paris", "X10.Most.Popular.Tourist.Sites_Rome")]
print(selected_columns)
```

    ##    X10.Most.Popular.Tourist.Sites_Paris  X10.Most.Popular.Tourist.Sites_Rome
    ## 1                                Louvre                            Colosseum
    ## 2             Eiffel Tower (To the top)                          Roman Forum
    ## 3                  Notre Dame Cathedral                       Trevi Fountain
    ## 4    The Latin Quarter (Quartier Latin)                             Pantheon
    ## 5                            Montmartre                        Piazza Navona
    ## 6                         Les Invalides Piazza di Spagna & the Spanish Steps
    ## 7                       Arc de Triomphe                 St. Peter's Basilica
    ## 8                        Champs-Élysées                       Sistine Chapel
    ## 9                         The Panthéon                    St. Peter's Square
    ## 10                 Palace of Versailles                            Catacombs

If you’re curious **which city is more affordable to tour**, here’s a
column graph for your reference:

``` r
ALL_Paris_Admission <- sum(Holiday$X10.Most.Popular.Tourist.Sites_Paris..Cost.of.General.Admission.Ticket)
ALL_Rome_Admission <- sum(Holiday$X10.Most.Popular.Tourist.Sites_Rome..General.Admission.Ticket.Cost..Euros.)

Paris_vs_Rome<- data.frame(
  City = c("Paris", "Rome"),
  Total_Admission_Fees = c(ALL_Paris_Admission, ALL_Rome_Admission)
)

ggplot(data = Paris_vs_Rome) +
  geom_col(mapping= aes(x = City, y = Total_Admission_Fees, fill = City) ) +
  labs(
    title = "Total Admission Tickets Expenses",
    subtitle = "Top 10 sites in Paris vs. Top 10 sites in Rome",
    caption = "A reference for which city may be more costly to tour",
    x = "City",
    y = "Total Admission Fees"
  )
```

![](Paris-and-Rome--5-Days-and-4-Nights-Holiday-Cost-Estimate_files/figure-gfm/Graph:%20Total%20Admission%20Tickets_Paris%20vs%20Rome-1.png)<!-- -->

There’s quite a disparity, eh? That’s because the Admission fees for the
following sites are as follows:

``` r
#first graph for Paris
plot_paris <- ggplot(data = Holiday) +
  geom_col(
    mapping = aes(
      y = X10.Most.Popular.Tourist.Sites_Paris,
      x = X10.Most.Popular.Tourist.Sites_Paris..Cost.of.General.Admission.Ticket,
      fill = X10.Most.Popular.Tourist.Sites_Paris..Cost.of.General.Admission.Ticket
    ),
    color = "yellow",
    position = "dodge"
  ) +
  labs(
    fill = "Entrance Fee",
    x = "Entrance/Admission Cost in Euros",
    y = "Top Tourist Sites",
    title = "Tourist Sites Admission Costs",
    subtitle = "Top 10 Sites in Paris",
    caption = "See references for the source of Top 10 sites."
  )

# second graph for Rome
plot_rome <- ggplot(data = Holiday) + 
  geom_col(
    mapping = aes(
      y = X10.Most.Popular.Tourist.Sites_Rome,
      x = X10.Most.Popular.Tourist.Sites_Rome..General.Admission.Ticket.Cost..Euros.,
      fill = X10.Most.Popular.Tourist.Sites_Rome..General.Admission.Ticket.Cost..Euros.
    ),
    color = "green",
    position = "dodge"
  ) +
  labs(
    fill = "Entrance Fee",
    x = "Entrance/Admission Cost in Euros",
    y = "Top Tourist Sites",
    title = "Tourist Sites Admission Costs",
    subtitle = "Top 10 Sights in Rome",
    caption = "See references for the source of Top 10 sites."
  )

# Stuffing em side by side
grid.arrange(plot_paris, plot_rome, ncol = 2)
```

![](Paris-and-Rome--5-Days-and-4-Nights-Holiday-Cost-Estimate_files/figure-gfm/Graph:%20Admission%20Cost%20SIDE%20BY%20SIDE_Paris%20vs%20Rome-1.png)<!-- -->

While both cities have popular tourist sites that don’t charge an
entrance fee for visitors, **Rome has significantly less sites that
charges a fee**. To view the specific figures for the costs separately
for each city (as of the time of this documentation), simply run the
code chunk below…

Here’s the **cost of Admission Tickets to Paris’ Top 10 Tourist Sites**:

``` r
selected_columns <- Holiday[, c("X10.Most.Popular.Tourist.Sites_Paris",     "X10.Most.Popular.Tourist.Sites_Paris..Cost.of.General.Admission.Ticket")]
names(selected_columns) <- c("Paris_Sites", "Paris_Admission_Cost")
print(selected_columns)
```

    ##                           Paris_Sites Paris_Admission_Cost
    ## 1                              Louvre                 18.3
    ## 2           Eiffel Tower (To the top)                 28.8
    ## 3                Notre Dame Cathedral                  0.0
    ## 4  The Latin Quarter (Quartier Latin)                  0.0
    ## 5                          Montmartre                  0.0
    ## 6                       Les Invalides                 14.9
    ## 7                     Arc de Triomphe                  0.0
    ## 8                      Champs-Élysées                  0.0
    ## 9                       The Panthéon                  12.4
    ## 10               Palace of Versailles                 21.3

… And here’s the **cost of Admission Tickets to Rome’s Top 10 Tourist
Sites**:

``` r
selected_columns <- Holiday[, c("X10.Most.Popular.Tourist.Sites_Rome",  "X10.Most.Popular.Tourist.Sites_Rome..General.Admission.Ticket.Cost..Euros.")]
names(selected_columns) <- c("Rome_Sites", "Rome_Admission_Cost")
print(selected_columns)
```

    ##                              Rome_Sites Rome_Admission_Cost
    ## 1                             Colosseum                17.2
    ## 2                           Roman Forum                 0.0
    ## 3                        Trevi Fountain                 0.0
    ## 4                              Pantheon                 0.0
    ## 5                         Piazza Navona                 0.0
    ## 6  Piazza di Spagna & the Spanish Steps                 0.0
    ## 7                  St. Peter's Basilica                 0.0
    ## 8                        Sistine Chapel                17.2
    ## 9                    St. Peter's Square                 0.0
    ## 10                            Catacombs                 8.6

Now that we’re familiar with the costs of touring each of the Top 10
sites in Rome and Italy costs, here’s a **breakdown on the Total Cost**
should you decide to visit all of them:

``` r
ALL_AdmissionCosts <- sum(Holiday$X10.Most.Popular.Tourist.Sites_Rome..General.Admission.Ticket.Cost..Euros.,Holiday$X10.Most.Popular.Tourist.Sites_Paris..Cost.of.General.Admission.Ticket)

ALL_Paris_Admission <- sum(Holiday$X10.Most.Popular.Tourist.Sites_Paris..Cost.of.General.Admission.Ticket)

ALL_Rome_Admission <- sum(Holiday$X10.Most.Popular.Tourist.Sites_Rome..General.Admission.Ticket.Cost..Euros.)

Admission_Summary <- data.frame(
  Top_10_Sites = c("Paris", "Rome", "Paris AND Rome"),
  Total_AdmissionCosts= c(ALL_Paris_Admission, ALL_Rome_Admission, ALL_AdmissionCosts)
)
print (Admission_Summary)
```

    ##     Top_10_Sites Total_AdmissionCosts
    ## 1          Paris                 95.7
    ## 2           Rome                 43.0
    ## 3 Paris AND Rome                138.7

### 3. Average Travel Expenses for 5 days: Paris and Rome

``` r
Gen.Transpo <- na.omit(Holiday[, c("Average.Transportation.Expenses", "Transportation_ReturnTrip_Costs..Euros.")])

ggplot(data = Gen.Transpo) +
  geom_col(mapping = aes(x=Average.Transportation.Expenses, y = Transportation_ReturnTrip_Costs..Euros.,    fill=Average.Transportation.Expenses )) +
  labs(x=NULL, title= "General Transportation Expenses",
       subtitle= ( "5 days in Paris and 5 Days in Rome;
         Flight cost is composed of the back and forth plane 
          trip from Paris to Rome.
          "), caption= " While this basic itinerary budgeting is only meant for 10 days 
        (--5 days in Paris, France and 5 days in Rome, Italy), the Rome 
          Metro/Public Transportation doesn't offer an exact 5-day promo 
          pass, so I opted for the most affordable transportation promo 
          to cover for the 5-day duration; the 7-day Pass.")
```

![](Paris-and-Rome--5-Days-and-4-Nights-Holiday-Cost-Estimate_files/figure-gfm/Graph:%20Travel%20Expenses%20for%205%20days_Paris%20vs%20Rome%20+%20flight-1.png)<!-- -->

Overall, the sum of the **average travel expenses** for Paris and Rome
would cost is… *(Also, if you’re viewing this in a narrow screen, don’t
forget to click the arrow “\>” to the right of the column header to view
the rest of the list)*

``` r
Ave_Trip_Exp<- Gen.Transpo[, c("Average.Transportation.Expenses", "Transportation_ReturnTrip_Costs..Euros.")]
print(Ave_Trip_Exp)
```

    ##   Average.Transportation.Expenses Transportation_ReturnTrip_Costs..Euros.
    ## 1                 Flight (Return)                                   200.0
    ## 2        Paris (5-day) Metro Pass                                    43.3
    ## 3        Rome (1-week) Metro Pass                                    24.0

### 4. OVERALL Holiday Tour Cost: Paris or Rome? Paris AND Rome?

So have you decided yet if your travel budget can take you to either
Paris, Rome, or both (–or perhaps it’s time to save some more so we can
have a budget to splurge on the local gourmet)? Whatever your decision
is, here’s a point graph to give you a quick visual idea on the gap
between the price points of the costs to visit either cities or both:

``` r
Transpo_Col <- Holiday$Transportation_ReturnTrip_Costs..Euros.[c(1,2,3)]

Flight <- Holiday$Transportation_ReturnTrip_Costs..Euros.[c(1)]
Paris_Metro <- Holiday$Transportation_ReturnTrip_Costs..Euros.[c(2)]
Rome_Metro <- Holiday$Transportation_ReturnTrip_Costs..Euros.[c(3)]

ALL_Transportation<- sum(Transpo_Col)

Paris_OVERALL <- sum(ALL_Paris_Lodging,ALL_Paris_Admission,Paris_Metro)
Rome_OVERALL <- sum(ALL_Rome_Lodging,ALL_Rome_Admission,Rome_Metro)
BOTH_OVERALL <- sum(ALL_LodgingCosts,ALL_AdmissionCosts,ALL_Transportation)

OVERALL_Summary <- data.frame(
  FourNights_FiveDays = c("Paris", "Rome", "Paris AND Rome"),
  Average_Costs= c(Paris_OVERALL, Rome_OVERALL, BOTH_OVERALL)
)

ggplot(data = OVERALL_Summary) +
  geom_point(mapping = aes(x = FourNights_FiveDays, y = Average_Costs, color= FourNights_FiveDays)) +
  labs( color="City",
        title = "Price Points for a 5-day Holiday to Paris, Rome, and Both"
  )
```

![](Paris-and-Rome--5-Days-and-4-Nights-Holiday-Cost-Estimate_files/figure-gfm/Graph:%20OVERALL%20Price%20Point%20Reference_%20Paris,%20Rome,%20BOTH-1.png)<!-- -->

Here’s a **summary of the total of the average cost to travel, stay, and
tour** in Paris, Rome, and both for 5 days and 4 nights:

``` r
Transpo_Col <- Holiday$Transportation_ReturnTrip_Costs..Euros.[c(1,2,3)]

Flight <- Holiday$Transportation_ReturnTrip_Costs..Euros.[c(1)]
Paris_Metro <- Holiday$Transportation_ReturnTrip_Costs..Euros.[c(2)]
Rome_Metro <- Holiday$Transportation_ReturnTrip_Costs..Euros.[c(3)]

ALL_Transportation<- sum(Transpo_Col)

Paris_OVERALL <- sum(ALL_Paris_Lodging,ALL_Paris_Admission,Paris_Metro)
Rome_OVERALL <- sum(ALL_Rome_Lodging,ALL_Rome_Admission,Rome_Metro)
BOTH_OVERALL <- sum(ALL_LodgingCosts,ALL_AdmissionCosts,ALL_Transportation)

OVERALL_Summary <- data.frame(
  FourNights_FiveDays = c("Paris", "Rome", "Paris AND Rome"),
  Average_Costs= c(Paris_OVERALL, Rome_OVERALL, BOTH_OVERALL)
)
print (OVERALL_Summary)
```

    ##   FourNights_FiveDays Average_Costs
    ## 1               Paris           655
    ## 2                Rome           479
    ## 3      Paris AND Rome          1334

This is where my little Travel budgeting project ends (for now). Thanks
for reading through this output with me and I hope it helps both my
fellow R-learning newbies and travelers alike.

#### Bon voyage!~

### 5. Data Sources/ References:

> - ‘Paris Average Hotel Costs: Nightly Room Prices by Accommodation
>   Type’,
>   <https://www.budgetyourtrip.com/hotels/france/paris-2988507#mid-range-hotels>
>
> - ‘Paris Visite travel pass’,
>   <https://www.ratp.fr/en/titres-et-tarifs/paris-visite-travel-pass>
>
> - ‘Rome Average Hotel Costs: Nightly Room Prices by Accommodation
>   Type’, <https://www.budgetyourtrip.com/hotels/italy/rome-3169070>
>
> - ‘Rome Transport Tickets’,
>   <https://www.rome.net/rome-transport-tickets>
>
> - ‘Top 10 Sights in Paris’, <https://www.introducingparis.com/top-10>
>
> - ‘Top 10 Sights in Rome’, <https://www.rome.net/top-10#>

##### \>\>\> RPubs HTML View:

<https://rpubs.com/A_M_S/ParisvsRome_Rproject23>

##### \>\>\> github Repository for this project:

Repository name: R_Paris_vs_Rome_Holiday-Tour

<http://github.com/writethings-whirlpool/R_Paris_vs_Rome_Holiday-Tour.git>

