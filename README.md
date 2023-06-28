# CryptoClustering

![Matt Damon Stars in Crypto.com ad](https://i.ytimg.com/vi/0SLPQHQOAgY/maxresdefault.jpg)

## Project Description

Remember the halcyon days of October 2021, where you just _had_ to get into crypto? Your brother-in-law and other, more distant, relations telling you that this was the time to get in; that you had to buy now, because this thing was going "to the moon 🚀"?

I haven't checked in since then, but I assume they're all millionaires almost two years on.

As we all know, if everyone around you is getting into a get-rich-quick scheme and it sounds too-good-to-be-true, then you'd better get in right now, because they're going to be rich and on the moon 🚀 (?) and you're going to be left behind 🌎 like a dummy. But since you didn't get in then, let's analyze some coins right now - it's never too late to become a ~~rube~~ wealthy investor.

The goal of this project was to use machine learning algorithms to organize a list of 41 cryptocurrencies into clusters to see what insights we can glean. The list contains cryptocurrencies as well-known as Bitcoin and as well-respected as ftx-token.

-----

## Data Preparation

The data contained in the [csv file](https://github.com/jonnybrammah/CryptoClustering/blob/main/Resources/crypto_market_data.csv) contained the information on the percentage price change over several timescales:
- 24 hours
- 7 days
- 14 days
- 30 days
- 60 days
- 200 days
- 1 year

Despite the well-known stability of the cryptocurrencies markets, the coins are liable to have more variability in their values over some of these timescales than in others. To avoid our KMeans model weighting these timescales more highly than others due to this increased variability, we used the StandardScaler function to standardize the data values. 

Once this has been done, let's cluster! ✨

-----

## Clustering the data using KMeans

Our first step here is to find what is an appropriate number of clusters to fit to. For this, an elbow curve plot was created with the number of possible clusters on the x axis and the inertia on the y axis. The inertia represents how easily a datapoint can be added to an existing cluster, with a high inertia meaning it is more 'difficult' to reasonably add the datapoint to a cluster. With this in mind, we want the inertia to be relatively low so the clusters do identify the differences between datapoints. However, there is a point at which too many clusters will also not adequately represent the data since it will be visually hard to parse, and only a handful of datapoints that may be otherwise similar may be clustered into different groups. To find the balance between these two factors, we plot the elbow-curve at select the cluster number at which the inertia is low but stops decreasing as much between clusters thereafter.

The elbow curve for our data looked like this:

![Elbow curve](https://github.com/jonnybrammah/CryptoClustering/blob/main/Output/elbow_curve.png?raw=true)

and so visually, it appears the optimal number of clusters seems to be around 4. 

We can then use the KMeans method to cluster the data into four clusters, and plot two of the dimensions against each other to visualize this. The resulting graph looks like this:

![Scatter Plot](https://github.com/jonnybrammah/CryptoClustering/blob/main/Output/market_scaled_data.png?raw=true)

Two very distinct clusters stand out from this graph, blue and yellow. Looking at this in broad strokes, you can see that both clusters hover around zero percent price change in the previous 24 hours with roughly equal amounts either positive and negative, with the yellow cluster having had a positive price change in the previous week and the blue cluster having had a negative price change.

Two other clusters exist, red and green, but each cluster only contains one data point.



-----

## Analysis
