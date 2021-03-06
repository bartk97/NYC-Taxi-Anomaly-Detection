# Anomaly Detection in Time Series with Autoencoder
*Final Project for the 'Machine Learning and Deep Learning' Course at AGH Doctoral School*

My scientific field is mathematical statistics, and more precisely the analysis of non-stationary series and resampling methods for them. My research problem is not related to ML and DL, and I chose this subject to learn DL methods for time series.


## Dataset
```nyc_taxi.csv``` - Number of NYC taxi passengers, where the five anomalies occur during 
* [NYC Marathon](https://en.wikipedia.org/wiki/2014_New_York_City_Marathon) (02.11.2014)
* Thanksgiving (27.11.2014)
* Christmas (24-26.12.2014)
* New Years Day (01.01.2015)
* [January 2015 North American blizzard](https://en.wikipedia.org/wiki/January_2015_North_American_blizzard) (26-27.01.2015)

The raw data is from the [NYC Taxi and Limousine Commission](https://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml). The data file consists of aggregating the total number of taxi passengers into 30 minute buckets.

**Data with highlighted anomalies**:
![info](https://raw.githubusercontent.com/bartk97/NYC-Taxi-Anomaly-Detection/main/Images/Data%20with%20highlighted%20anomalies.png)





## Goal
The goal of the project is to detect anomalies in the dataset containing the number of taxi passengers in New York.


## Anomaly Detection with Antoencoder

An **autoencoder** is a neural network used to learn efficient codings of unlabeled data (unsupervised learning). It has two main parts: an **encoder** and a **decoder**.
* an encoder maps the input into the code,
* a decoder maps the code to a reconstruction of the input.

An autocoder tires to reconstruct the input, so anomalies can be detected by analysis of the reconstruction loss.

![info](https://raw.githubusercontent.com/bartk97/NYC-Taxi-Anomaly-Detection/main/Images/Autoencoder%20architecture.png)


## Anomaly Detection with LSTM Antoencoder

**Recurrent neural network (RNN)** - a neural network that is typically used to time series. The RNN keeps a memory of what it has already processed so that it can learn from previous iterations during training.

![info](https://raw.githubusercontent.com/bartk97/NYC-Taxi-Anomaly-Detection/main/Images/rnn.png)

**Long short-term memory (LSTM)** - when training a RNN using back-propagation, the long-term gradients which are back-propagated "vanish" or "explode", because of the computations involved in the process, which use finite-precision numbers. RNNs using LSTM units partially solve the vanishing gradient problem, because LSTM units allow gradients to also flow unchanged. 

![info](https://raw.githubusercontent.com/bartk97/NYC-Taxi-Anomaly-Detection/main/Images/LSTM.png)


**LSTM Antoencoder** - an implementation of an autoencoder for sequence data using an Encoder-Decoder LSTM architecture. For a given dataset of sequences, an encoder-decoder LSTM is configured to read the input sequence, encode it, decode it, and recreate it. The performance of the model is evaluated based on the model???s ability to recreate the input.




## 1st Approach
```NYC Taxi- anomaly detection with Autoencoder.ipynb``` [[Notebook]](https://github.com/bartk97/NYC-Taxi-Anomaly-Detection/blob/main/NYC%20Taxi-%20anomaly%20detection%20with%20Autoencoder.ipynb)

The first approach was to use a vanilla autocoder to detect days on which the number of passengers per hour was significantly different than on other days. The idea was to split the time series into days and create a new data frame as follows: one row corresponds to one day and one column corresponds to a 30-minute interval:

![link](https://raw.githubusercontent.com/bartk97/NYC-Taxi-Anomaly-Detection/main/Images/data%20frame.png)

The next step was to train the autoencoder to reconstruct the number of taxi passengers on a given day as 48-dimensional observations (each dimension corresponded to a 30-minute interval). 

![link](https://raw.githubusercontent.com/bartk97/NYC-Taxi-Anomaly-Detection/main/Images/reconstruction.png)

Then I was able to detect days with a different pattern of of NYC taxi passengers by looking at reconstruction loss:

![link](https://github.com/bartk97/NYC-Taxi-Anomaly-Detection/blob/main/Images/loss%20per%20day.png)

Threshold = mean loss + 2*std loss 

**Deceted anomalies:** The darker the fill, the greater the reconstruction error

![link](https://raw.githubusercontent.com/bartk97/NYC-Taxi-Anomaly-Detection/main/Images/detected%20anomalies.jpg)

Dates where anomalies have been detected:
* '2014-11-01' - one day before the NYC Marathon
* '2014-11-27' - Thanksgiving
* '2014-12-24' - Christmas time
* '2014-12-25' - Christmas time
* '2014-12-26' - Christmas time
* '2014-12-27' - Christmas time
* '2014-12-28' - Christmas time
* '2015-01-01' - New Year Day
* '2015-01-04' - ?
* '2015-01-18' - ?
* '2015-01-26' - blizzard
* '2015-01-27' - blizzard 


## 2nd Approach

```NYC TAXI- anomaly detection - LSTM Autoencoder.ipynb``` [[Notebook]](https://github.com/bartk97/NYC-Taxi-Anomaly-Detection/blob/main/NYC%20TAXI-%20anomaly%20detection%20with%20LSTM%20Autoencoder.ipynb)

This approach differed from the previous one. I didn't look at days separately, but at data points. I tried to detect anomalies by looking at single observations (30 minutes). This method used LSTM Autoecnder and I were using the previous 24 hours to recreate each data. At first I split into 24h moving winodws $\{X_{i}. X_{i+1}, \ldots, X_{i+48}\}$. I trained the LSTM Autoencoder to reconstruct a time series:

![link](https://raw.githubusercontent.com/bartk97/NYC-Taxi-Anomaly-Detection/main/Images/reconstruction%20lstm.png)

and analyzed the reconstruction error of the data from the test set:

![link](https://raw.githubusercontent.com/bartk97/NYC-Taxi-Anomaly-Detection/main/Images/loss%20lstm.png)

The threshold was selected by analyzing the above plot, threshold = 0.2. Perhaps, if I decreased the threshold, thanksgiving might be detected as anomalies, but also other additional dates that may not necessarily be anomalies.

**Deceted anomalies:**

![link](https://raw.githubusercontent.com/bartk97/NYC-Taxi-Anomaly-Detection/main/Images/detected%20anomalies%20lstm.jpg)

Dates where anomalies have been detected:
* 2014-11-01 08:00:00 - 2014-11-02 01:00:00 - NYC Marathon
* 2014-12-24 13:00:00 - 2014-12-26 03:00:00 - Christmas time
* 2015-01-25 21:00:00 - 2015-01-27 16:00:00 - blizzard

It did not detect anomalies in the period: Thanksgiving, New Year Day and parts of the Christmas time.


## Appendix
When I was preparing this project and learning about anomaly detection with DL, I created two projects:
* [Set of ECG signals - anomaly detection - Autoencoder](https://github.com/bartk97/NYC-Taxi-Anomaly-Detection/blob/main/Other/Set%20of%20ECG%20-%20anomaly%20detection%20-%20Autoencoder.ipynb)
* [Stock Price - anomaly detection - LSTM Autoencoder](https://github.com/bartk97/NYC-Taxi-Anomaly-Detection/blob/main/Other/Stock%20price%20-%20anomaly%20detection%20-%20LSTM%20Autoencoder.ipynb) (needs to be improved)
 
 which are based on projects from *References*.

## References

1.	**YouTube**:
	* DigitalSreeni, ???88 - Applications of Autoencoders - Anomaly Detection???, https://www.youtube.com/watch?v=u1vLJBwOFC8
	* DigitalSreeni, ???165 - An introduction to RNN and LSTM???, https://www.youtube.com/watch?v=Mdp5pAKNNW4&t=881s
	* DigitalSreeni, ???180 - LSTM Autoencoder for anomaly detection???, https://www.youtube.com/watch?v=6S2v7G-OupA&t=4s
	* Venelin Valkov, ???Time Series Anomaly Detection Tutorial with PyTorch in Python | LSTM Autoencoder for ECG Data???, https://www.youtube.com/watch?v=qN3n0TM4Jno
2. **Blogs**:
	* Chris Kuo/Dr. Dataman, ???Anomaly Detection with Autoencoders Made Easy???, https://towardsdatascience.com/anomaly-detection-with-autoencoder-b4cdce4866a6
	* Raghav Agrawal, ???Complete Guide to Anomaly Detection with AutoEncoders using Tensorflow???, https://www.analyticsvidhya.com/blog/2022/01/complete-guide-to-anomaly-detection-with-autoencoders-using-tensorflow/
3.	**Papers**:
	* T. Kieu, B. Yang and C. S. Jensen, ???Outlier Detection for Multidimensional Time Series Using Deep Neural Networks???, 2018, doi: 10.1109/MDM.2018.00029
	* T. Kieu, B. Yang, C. Guoand and C. S. Jensen, ???Outlier Detection for Time Series with Recurrent Autoencoder Ensembles???, 2019, doi: 10.24963/ijcai.2019/378
4.	**Wikipedia**:
	* Autoencoder, https://en.wikipedia.org/wiki/Autoencoder
	* Long short-term memory, https://en.wikipedia.org/wiki/Long_short-term_memory	


## 
Author: Bartosz Majewski, 
	PhD Student at AGH Doctoral School, 
	Faculty of Applied Mathematics
