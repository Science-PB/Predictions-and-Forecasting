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

<img width="762" alt="Screen Shot 2020-11-16 at 11 00 45 PM" src="https://user-images.githubusercontent.com/66921930/99345265-e4c43480-285f-11eb-8777-57021c015f5f.png">

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

<img width="689" alt="Screen Shot 2020-11-16 at 11 01 29 PM" src="https://user-images.githubusercontent.com/66921930/99345268-e55ccb00-285f-11eb-9516-6f4506fed224.png">

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

<img width="746" alt="Screen Shot 2020-11-16 at 11 02 01 PM" src="https://user-images.githubusercontent.com/66921930/99345270-e5f56180-285f-11eb-8ddb-daad413f3dae.png">


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

<img width="741" alt="Screen Shot 2020-11-16 at 11 02 40 PM" src="https://user-images.githubusercontent.com/66921930/99345273-e68df800-285f-11eb-9d6b-89e67c113c86.png">


The first correlogram in Figure 10, describes the relationship between how autocorrelated the
observations are in comparison to observations of prior time steps. Something worth noting, is the ACF at lag 0
equals 1 by default and is purely a reference point (Holmes, Scheuerell & Ward, 2020). A default confidence interval of 95% is represented by the horizontal blue lines and the data showcases that the autocorrelation
coefficients do not exceed the significance bounds. This leads to the conclusion that there is little evidence for
autocorrelation. The second correlogram in Figure 10 represents a partial correlogram which takes into
account the removal of the relationship of intervening observations. For the Lake Huron data, the partial
correlogram shows that the partial correlations at time lags 2 and 20 exceed the significance bounds resulting
in two lagged values, tailing off to zero between each.

<img width="744" alt="Screen Shot 2020-11-16 at 11 05 31 PM" src="https://user-images.githubusercontent.com/66921930/99345537-8c416700-2860-11eb-8f66-4a1214c5dfd5.png">

In order to conclude the ARIMA(p,d,q) model, the principle of parsimony needs to be considered. The
principle of parsimony assumes that the best model is the model with the fewest parameters. Due to the
correlograms showcased in Figure 10 resulting in the autocorrelation coefficients generally tailing to zero, the p
and q values are determined to be 0 themselves. This can be further validated by applying the R code in
Figure 11, the result of which confirms the optimal ARIMA model at ARIMA(0,1,0).

<img width="668" alt="Screen Shot 2020-11-16 at 11 05 54 PM" src="https://user-images.githubusercontent.com/66921930/99345539-8cd9fd80-2860-11eb-8d9f-4a90b14d4e34.png">


# Time Series: ARIMA Forecasting
Once the ARIMA(p,d,q) model has been identified and the parameters estimated, the model is ready for
use as a predictive model for making forecasts (Coghlan, 2010). By applying the forecast function in R as
shown in Figure 12, the observed water levels over 97 years at Lake Huron as well as the predicted water
levels for the next five years is represented in Figure 13’s plot. The data forecasts the water level at Lake
Huron to be 579.96 feet for the next five years with prediction intervals at 80% and 95%.

<img width="742" alt="Screen Shot 2020-11-16 at 11 06 46 PM" src="https://user-images.githubusercontent.com/66921930/99345540-8cd9fd80-2860-11eb-8349-b9b55b6d7230.png">
<img width="738" alt="Screen Shot 2020-11-16 at 11 06 54 PM" src="https://user-images.githubusercontent.com/66921930/99345544-8e0b2a80-2860-11eb-9f5f-37ca3972d800.png">


An important step in ARIMA models is evaluating the output to understand whether the forecast errors
of the model are normally distributed and whether there are correlations between the errors. Taking necessary
steps, ARIMA models can be evaluated to ensure their viability as a predictive model. By creating a
correlogram of the forecast errors, as seen in Figure 14, it is observed that the coefficients stay within the
significance bounds. In addition to a correlogram a Ljung-Box test can be utilized to demonstrate if the model
demonstrates lack of fit.

<img width="724" alt="Screen Shot 2020-11-16 at 11 07 22 PM" src="https://user-images.githubusercontent.com/66921930/99345546-8e0b2a80-2860-11eb-9277-4b02675b84f6.png">

A Ljung-Box test is a hypothesis test used to determine whether or not a model’s autocorrelations for
the errors are non-zero (Glen, 2018). Being a hypothesis test, the model has a null and alternative hypothesis
placed on it. The null hypothesis represents the model not showing a lack of fit while the alternative is that a
lack of fit does exist. Demonstrated by the code in Figure 14, the p-value is determined to be 0.1457. At a
value higher than the significance value of 0.05, the claim can be made that there is not enough evidence to
reject the null hypothesis and therefore the model is appropriate to be used as a predictive model.
As mentioned previously, it is important to understand if the forecast errors are normally distributed,
with a mean of zero and a constant variance. By plotting the model’s residuals in Figure 15, the mean is determined to be 0.0016 and roughly constant over time. To test for normality a histogram of the residuals and
an overlaid density plot of a randomly generated normal distribution is produced using R code in Figure 16.

<img width="700" alt="Screen Shot 2020-11-16 at 11 09 54 PM" src="https://user-images.githubusercontent.com/66921930/99345916-6c5e7300-2861-11eb-8f60-96a7423e4c59.png">
<img width="718" alt="Screen Shot 2020-11-16 at 11 10 00 PM" src="https://user-images.githubusercontent.com/66921930/99345919-6cf70980-2861-11eb-97a7-a1d988edd820.png">


Conclusions can be made by the outputted histogram in Figure 17 that the model is normally distributed
with a mean of 0. Taking into consideration the multiple tests run on the ARIMA model for Lake Huron it can be
concluded that the ARIMA(0,1,0) model is an acceptable predictive model for forecasting water levels.

<img width="752" alt="Screen Shot 2020-11-16 at 11 10 20 PM" src="https://user-images.githubusercontent.com/66921930/99345920-6d8fa000-2861-11eb-8f2a-4150202dda4b.png">

# Conclusion
A significant portion of time series analysis revolves around smoothing the model and eliminating
seasonality and even trend components. The purpose behind which is to be able to make more reliable
predictions. Time series data can provide significant seasonal variation, as with the Australian beer production
example but can also be undetectable such as in the water levels of Lake Huron example. The removal of
seasonality, via decomposing or differencing, allows the signal used for forecasting to not be obscured by the
repetitious cycle that seasonality embeds creating a more effective model (Brownlee, 2016).
Much of the science behind time series data takes into account visualizations. As an example, a plot
was used early on to determine the existence of seasonality in Australian beer production, while with Lake
Huron it was used in the decision to apply first-differencing and remove the linear trend. A common practice is
to evaluate the model via a plot during different stages to understand component estimates as well as
understand what the elimination of components does to the data and help determine next steps. Going back to
basics, visual representations can quickly tell a person a lot about a dataset, particularly with time series.
With the pursuit of predictive modeling and forecasting in mind, potential drawbacks do exist with time
series methods. For starters the methods can rely heavily on old data which can skew forecasts if no longer
relevant. In addition, time series analysis cannot fully adjust various factors that affect fluctuations in a series
(Das, 2019). What is important to remember is that statistics is a method to make educational decisions, it
does not claim to be absolute truth in its applications. Time series is not an exception in this case. Instead it is
a tool utilized by many businesses and economists to make plausible interpretations from data that can then be
utilized to drive real world actions.

# References
Nist Sematech. (n.d.). Introduction to Time Series Analysis. Nist Sematech. Retrieved from:
https://www.itl.nist.gov/div898/handbook/pmc/section4/pmc4.htm

Coghlan, A. (2010). Using R for Time Series Analysis. Read the Docs. Retrieved from: https://a-little-book-of-r-
for-time-series.readthedocs.io/en/latest/src/timeseries.html#decomposing-time-series

Federal Reserve Bank of Dallas. (n.d.). Seasonally Adjusting Data. Federal Reserve Bank of Dallas. Retrieved
from: https://www.dallasfed.org/research/basics/seasonally.aspx

Chen, J. (2019, Apr 13). Autoregressive Integrated Moving Average (ARIMA). Investopedia. Retrieved from:
https://www.investopedia.com/terms/a/autoregressive-integrated-moving-average-arima.asp

Hyndman, R. and Athanasopoulos, G. (2018). Forecasting: principles and practice (2nd ed.). Melbourne,
Australia: OTexts. Retrieved from: https://otexts.com/fpp2/stationarity.html

Holmes, E., Scheuerell, M. and Ward, E. (2020, Feb 3). Applied Time Series Analysis for Fisheries and

Environmental Sciences. Bookdown. Retrieved from: https://nwfsc-timeseries.github.io/atsa-labs/sec-tslab-
differencing-to-remove-a-trend-or-seasonal-effects.html

Glen, S. (2018, Sep 7). Ljung Box Test: Definition. Statistics How To. Retrieved from:
https://www.statisticshowto.com/ljung-box-test/

Glen. S. (2016, Aug 23). Correlogram / Auto Correlation Function ACF Plot: Definition in Plain English.
Statistics How To. Retrieved from: https://www.statisticshowto.com/correlogram/

Das, R. (2019, Feb 13). Advantages and Disadvantages of time series. Physics Pie. Retrieved from:
https://thephysicspi.blogspot.com/2019/02/advantages-and-disadvantages-of-time.html
