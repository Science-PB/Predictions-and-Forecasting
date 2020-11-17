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

<img width="680" alt="Screen Shot 2020-11-16 at 10 55 58 PM" src="https://user-images.githubusercontent.com/66921930/99345019-5354c280-285f-11eb-9b65-284e809e5d42.png">


By reviewing the plot in Figure 2 certain inferences can be made such as the appearance of a
seasonality factor. Logically this makes sense, as beer is likely to be produced and consumed more often during warmer weather and downtime which in Australia would be December through February which falls into
Q1 and Q4 in terms of quarters. Another inference that can be made is the appearance of a constant seasonal
variation, in other words as time increases the seasonality stays relatively the same. This is indicative of an
additive model. At this stage decomposing has not occurred. In order to estimate the trend, irregular and
seasonal components the use of the decompose function in R must be utilized.

<img width="714" alt="Screen Shot 2020-11-16 at 10 56 27 PM" src="https://user-images.githubusercontent.com/66921930/99345020-53ed5900-285f-11eb-888d-1c412702c35c.png">

The decompose function is used to store the estimated values of trend, irregular and seasonal
components as variables (Coghlan, 2010). When plotted a decomposed time series provides much more
insight into how the data is functioning over time. Figure 3 provides the R code for decomposing the data while
Figure 4 reflects the plotted estimates of each of the three different components along with the original time
series.

<img width="745" alt="Screen Shot 2020-11-16 at 10 57 42 PM" src="https://user-images.githubusercontent.com/66921930/99345022-5485ef80-285f-11eb-8b7d-a441eb452583.png">


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

<img width="650" alt="Screen Shot 2020-11-16 at 10 58 13 PM" src="https://user-images.githubusercontent.com/66921930/99345026-551e8600-285f-11eb-9052-c871be701ff6.png">

After removing the seasonal component, the data can then be plotted to understand the trend. Figure 6
provides the insight to make conclusions about the actual trend of productivity. Productivity stayed relatively
flat from 1956 until the early 1960s, where it then exponentially rose until the early 1970s. Featuring relative
stability, production then made a onetime peak at almost 550 megaliters in the early 1980s. Since that peak in
productivity, the Australian beer company has seen a gradual downturn, barring some spikes in the late 1980s
and early 1990s.



Forecasting and predictions are a main component for the application of statistics to time series data.
Exponential smoothing techniques are one way of making forecasts, however when dealing with stationary
time series, ARIMA is seen as a better predictive model (Coghlan, 2010). ARIMA, an acronym for
autoregressive integrated moving average, is a form of regression analysis that explores and describes the
strength of a dependent variable in relation to other changing variables. The objective behind the use of
ARIMA is to output future predictions through the examination of differences between time series values as
opposed to through the actual values themselves (Chen, 2019).
In order to showcase the functionality of addressing issues of correlation between successive values in
a times series another R dataset, LakeHuron is applied. The time series dataset provides the annual water
level for Lake Huron from 1875 to 1972. By plotting the dataset as seen in Figure 7, an understanding of how
the data behaves can begin to be formed.



The techniques and concepts of ARIMA models are utilized mainly for stationary time series as
previously mentioned. Time series data that is riddled with trend and seasonality fluctuations may not be
properly suited to an ARIMA model, however, methods exist to eliminate these components. Differencing is an alternative method to decomposition. By calculating the difference between consecutive observations, the
differencing method can help smooth out the mean of a time series by removing the trend and seasonality
components, thereby outputting a stationary time series (Hyndman & Athanasopoulos, 2018).
In order to apply differencing the diff function is utilized in R. From Figure 7 a downward trend is noted
along with a seeming lack of seasonality. Based on these conclusions, the choice is made to apply first-
differencing, or the removal of a linear trend, to remove the trend component. Differencing is coded and plotted
in Figure 8. With first-differencing applied the series appears to be stationary in both mean and variance.
Calculating the mean at a result near 0 reflects the now constant behavior over time.




# Time Series: ARIMA Model

With the result of a stationary time series, an ARIMA model can be selected in order to predict future
water levels for Lake Huron. In order to apply the best ARIMA model, appropriate values have to be found for
p, d and q which make up the ARIMA(p,d,q) model. At this stage, d, the order of differencing used, has already
been discovered to be 1, since first-differencing provided a stationary series. In order to find p and q a
correlogram and partial correlogram analysis is used.
Correlograms are a visual representation of the serial correlation among data in a time series (Glen,
2016). Serial correlation, or autocorrelation, can be defined as the error component in a time series that
transfers from one point in time to another. The utilization of correlograms indicates whether autocorrelation
exists in a dataset, which can result in exaggerated overfitting (Glen, 2016). By applying an estimate and
partial estimate of autocorrelation as seen in Figure 9, it can be understood if autocorrelation exists in a
significant enough form to merit consideration.




