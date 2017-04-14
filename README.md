# Data Visualization: Major U.S. Airline Performance in 2016

## Summary

This data visualization describes data on flight delays for 4 major U.S. airlines for the year 2016. The data set can be accessed from [RITA](https://www.transtats.bts.gov/OT_Delay/OT_DelayCause1.asp).

## Design 

I only focus on the 4 biggest airlines with combined market share of about [70%](https://www.statista.com/statistics/250577/domestic-market-share-of-leading-us-airlines/). Those are:

* Southwest
* Delta
* American
* United

Exploratory data analysis was performed in **Rstudio**. The code and details can be seen in the file `eda.Rmd`.

In this phase I decided to see whether there are peak times when more flights across carriers are delayed. I supposed that more delays would occur during busier times of the year, that is holiday periods in the summer and Christmas. I also wanted to look at how much of delayed time is caused by different carriers.

Therefore, two hypothesis can be stated:

* *more flights are delayed in summer and in December*
* *different carriers may be causing the delays more than others*

With this in mind, I make two plots: 

* share of flights delayed by each carrier, monthly
* share of delayed minutes caused by each carrier, monthly

![R Plot](https://raw.githubusercontent.com/kanfibl/flights/master/rplot.png)

From the plots we see that **July** and **December** have a lot of delays, but its mostly not carriers’ fault - months correspond to peak holiday seasons. **Delta Airlines** is pretty bad, being responsible for half of delayed time usually. But somehow this carrier is lucky with weather and other factors, because proportion of delayed flights is lower than for other carriers. In July and August Delta improved, but was still the most "guilty" carrier.

The plots provided support for my hypothesis, so I proceeded with making a visualization.

### Data Visualization with dimple.js

To implement visualization I solely used **dimple.js**, as **d3.js** seemed excessively verbose to me, especially for this case.

My decision was to keep the line chart, as I thought it best represented the trend across various carriers.
I impoved my initial R plots in the following ways:

* overlayed the line charts with scatter plots and decided to drop the second plot altogether. Instead I reflected the shares of delays due to the carriers by changing radius sizes of pointmarks: the more guilty the carrier - the bigger are the circles.
* fixed the y-axis by properly expressing percentages
* added an annotation to the graph about the circle sizes
* edited graph and axis titles for better understanding 
* kept the visual encoding of different airlines by color, so the reader can distiguish between them
* put the legend in the top right corner
* put limits on the y-axis in order to make a better comparison between airlines. Having a 100% axis would have flatted out the lines and made the interpretation difficult.

The initial visualization can be seen in `index_initial.html` or below:
![initial](https://raw.githubusercontent.com/kanfibl/flights/master/initial.png)
Howewer, to interact with the graph and see the data values in detail for each circle, the html version should be accessed.

## Feedback

I made a post on [Udacity Forum](https://discussions.udacity.com/t/project-feedback-flights-data/238986/9) and received 2 feedbacks from course participants. Another feedback was given to me by a friend. The feedbacks were:

#### Feedback #1 by [arundathi.ga](https://discussions.udacity.com/users/arundathi.ga/summary)

> Hello Alex,

> The visualization explains the delays in the major airlines very well. The visualization is aesthetically very appealing and neat.
The only scope for improvement I see is to include the number representing each size of bubble , which I believe maybe already achieved and visible when you dynamically see the plot vs the screenshot.

> I observe that American airlines has had the highest delay in most months and delta airlines has the least delay consistently across months. 
Though, among all the delays, delta seems to be having higher share of delays caused by their carrier itself which is represented well with the size of the green dot.
Overall all the airlines seem to be having high delays in summer and in December.

>Great job in making this wonderful visualization.

>Thanks,
Aru

#### Feedback #2 by [vishy730](https://discussions.udacity.com/users/vishy730/summary)

> Hi @kanfibl,

> Let me tell you first that your visualization looks awesome. Coming to your doubts, I suggest to you use bubble chart itself than a heatmap. Here is the reference for that which has both heatmap and bubblechart for the same example.
[https://bl.ocks.org/gordonwoodhull/14c623b95993808d69620563508edba6](https://bl.ocks.org/gordonwoodhull/14c623b95993808d69620563508edba6)

> Hope you know to narrate a story in animation form (month wise) with some description. I would also suggest you to add another chart, probably the above one that highlights the top 5 delays.

> Hope that helps.

#### Feedback #3 by [Karolus Sariola](https://github.com/karosaurus)

> Dear Alexander,
The visualization is clear and the interactive nature of it works well. Good job!

>Perhaps the way the variable 'the percentage of delays caused by the airlines' is presented still leaves some room for improvement. I would suggest varying the fill colour of the ball instead of its size by introducing a gradient of colours - a heatmap with a scale from 0 to 100. Keep up the good work!

### Redesign

Overall, reviewer suggested I should highlight the fact that Delta Airlines causes more delays: either with heatmap or adding numbers in the circles. Vishy730 also suggested adding another graph to highlight top delays.

Considering feedback I tried different options and decided not to overload one graphs with more colors by implementing the heatmap, as each carrier was already differentiated by color. 

Instead, I decided to add another graph (coincidentally  moving back to the initial R layout), which focuses just on the share of delayed minutes caused by carriers. This way, I also incorporate Vishy730 suggestion. The best way was to put graphs below each other, so each month is on the same x-coordinate. *I removed the varying circle sizes from the first graph* not to overload the visualisation, but left opaque circle marks to make it easier for the reader to hover over any particular datapoint and examine the actual values.

The final version can be viewed at `index_final.html` or below:

To interact with the graph and see the data values in detail for each circle, the html version should be accessed.

## Resources

- [dimple.js Documentation](http://dimplejs.org/)
- [Data Visualization and D3.js (Udacity)](https://www.udacity.com/course/viewer#!/c-ud507-nd)
- [Stack Overflow](http://stackoverflow.com/search?q=dimple.js) posts

## Data

- `655176550_12017_3428_airline_delay_causes.csv`: original dataset
- `data.csv`: cleaned and reshaped dataset used to implement visualization
