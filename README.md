# Predictions-and-Forecasting
Time Series in R


# Introduction

Statistics is a common practice to the application of predictions and forecasting. That said, there are numerous
methods and techniques within statistics that can be applied in order to output results deemed sufficiently
viable. When considering data points that occur over a specified time period or interval an appropriate
statistical technique is time series analysis. Through the use of historical data, time series analysis is a popular
method in determining trends, seasonality, cyclicity and irregularity. Through the use of two different R
datasets, time series techniques such as decomposing and ARIMA will be explored to understand trends in the
data along with forecast production.

# Time Series: Decomposing

Time series analysis is a unique statistical method in that it takes into account the fact that data points
that are taken over a period of time may be dispositioned to autocorrelation, trend or seasonal variation (Nist
Sematech, n.d.). Different from other techniques, time series use observations as both outcome and predictor
variables. Due to the practicality of this type of statistical method, there are various time series techniques that
can be applied to time-based data.
Decomposing is a time series technique used to separate data into trend, irregular and seasonal
components. Time series analysis and decomposing lend themselves well to visual representations to
showcase their outputs. Many business applications can use time series analysis to help enable decision
making. An example of such is the use of Australian beer production over time. The ausbeer dataset
represents an Australian beer company’s total quarterly beer production in megaliters from the first quarter of
1956 to the third quarter of 2008. R is a constructive tool to utilize to apply time series techniques, but as with
many statistical methods, proper set up of the dataset is critical.
It is not intuitive to R when a dataset is a time series, this makes it important when working with R to
specify that a dataset be interpreted as such. The ts function is utilized for this particular reason. By specifying
the dataset be read this way, indicating where to start and stop and assigning the frequency level, such as “4”
for quarterly, a dataset can easily be converted to a time series. The R code provided in Figure 1, applies the
conversion to a time series to the ausbeer dataset and then plots the data.


By reviewing the plot in Figure 2 certain inferences can be made such as the appearance of a
seasonality factor. Logically this makes sense, as beer is likely to be produced and consumed more often during warmer weather and downtime which in Australia would be December through February which falls into
Q1 and Q4 in terms of quarters. Another inference that can be made is the appearance of a constant seasonal
variation, in other words as time increases the seasonality stays relatively the same. This is indicative of an
additive model. At this stage decomposing has not occurred. In order to estimate the trend, irregular and
seasonal components the use of the decompose function in R must be utilized.



The decompose function is used to store the estimated values of trend, irregular and seasonal
components as variables (Coghlan, 2010). When plotted a decomposed time series provides much more
insight into how the data is functioning over time. Figure 3 provides the R code for decomposing the data while
Figure 4 reflects the plotted estimates of each of the three different components along with the original time
series.




From Figure 4, there are substantially more inferences that can be made about the pattern and
behavior of the dataset. Using the trend output it can be deduced that from roughly 1960 to 1975 beer
production saw a steady increase which then remained relatively stable until 1990 when a small decrease
occurred prior to stabilizing in the mid ‘90s through the 2000’s. As expressed previously and further confirmed by the seasonal output, there’s a strong seasonality factor to the dataset, which favors the top and bottom of
each year. The random or irregular component displays the random noise found in the time series.
Seasonal data can pose an issue when attempting to understand trends in time series. Economists and
businesses need to be able to understand whether spikes and falls in data are attributed solely to seasonal
variations or not (Federal Reserve Bank of Dallas, n.d.)). This is where seasonally adjusting time series comes
into play. Seasonally adjusting a dataset simply means estimating the seasonal component and then
subtracting it from the original time series. The R code provided in Figure 5, showcases the extraction of the
seasonal component from the ausbeer time series.




