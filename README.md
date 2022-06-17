# NYC-Taxi-Anomaly-Detection
*Final Project for the 'Machine Learning and Deep Learning' Course at AGH Doctoral School*

## Dataset
```nyc_taxi.csv``` - Number of NYC taxi passengers, where the five anomalies occur during 
* [NYC Marathon](https://en.wikipedia.org/wiki/2014_New_York_City_Marathon) (02.11.2014)
* Thanksgiving (27.11.2014)
* Christmas (25-28.12.2014)
* New Years Day (01.01.2015)
* [January 2015 North American blizzard](https://en.wikipedia.org/wiki/January_2015_North_American_blizzard) (26-27.01.2015)

The raw data is from the [NYC Taxi and Limousine Commission](https://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml). The data file consists of aggregating the total number of taxi passengers into 30 minute buckets.

**Data with highlighted anomalies**:
![info](https://raw.githubusercontent.com/bartk97/NYC-Taxi-Anomaly-Detection/main/Images/Data%20with%20highlighted%20anomalies.png)





## Goal
The goal of the project is to detect an anomaly in the dataset containing the number of taxi passengers in New York.


## Antoencoder

An **autoencoder** is is a neural network that has two parts: an **encoder** and a **decoder**.
* an encoder maps the input into the code,
* a decoder maps the code to a reconstruction of the input.

An autocoder tires to reconstruct the input, so anomalies can be detected by analysis of the reconstruction loss.

![info](https://raw.githubusercontent.com/bartk97/NYC-Taxi-Anomaly-Detection/main/Images/Autoencoder%20architecture.png)


## LSTM Antoencoder
text

![info](https://raw.githubusercontent.com/bartk97/NYC-Taxi-Anomaly-Detection/main/Images/LSTM.png)


## 1st Approach
```NYC Taxi- anomaly detection with Autoencoder.ipynb```

## 2nd Approach
text


## References

1.	**YouTube**:
	* DigitalSreeni, “88 - Applications of Autoencoders - Anomaly Detection”, https://www.youtube.com/watch?v=u1vLJBwOFC8
	* DigitalSreeni, “165 - An introduction to RNN and LSTM”, https://www.youtube.com/watch?v=Mdp5pAKNNW4&t=881s
	* DigitalSreeni, “180 - LSTM Autoencoder for anomaly detection”, https://www.youtube.com/watch?v=6S2v7G-OupA&t=4s
	* Venelin Valkov, “Time Series Anomaly Detection Tutorial with PyTorch in Python | LSTM Autoencoder for ECG Data”, https://www.youtube.com/watch?v=qN3n0TM4Jno
2. **Blogs**:
	* Chris Kuo/Dr. Dataman, “Anomaly Detection with Autoencoders Made Easy”, https://towardsdatascience.com/anomaly-detection-with-autoencoder-b4cdce4866a6
	* Raghav Agrawal, “Complete Guide to Anomaly Detection with AutoEncoders using Tensorflow”, https://www.analyticsvidhya.com/blog/2022/01/complete-guide-to-anomaly-detection-with-autoencoders-using-tensorflow/
3.	**Papers**:
	* T. Kieu, B. Yang and C. S. Jensen, “Outlier Detection for Multidimensional Time Series Using Deep Neural Networks”, 2018, doi: 10.1109/MDM.2018.00029
	* T. Kieu, B. Yang, C. Guoand and C. S. Jensen, “Outlier Detection for Time Series with Recurrent Autoencoder Ensembles”, 2019, doi: 10.24963/ijcai.2019/378
4.	**Wikipedia**:
	* Autoencoder, https://en.wikipedia.org/wiki/Autoencoder
	* Long short-term memory, https://en.wikipedia.org/wiki/Long_short-term_memory	
