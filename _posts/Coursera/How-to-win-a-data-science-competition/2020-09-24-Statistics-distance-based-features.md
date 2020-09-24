---
layout: post
title:  "Coursera - Advanced Features II - Statistics and Distance Based Features"
categories: coursera data_science
author: "Manuel"
---

# Some data for CTR Task
![Example data]({{ site.baseurl }}/assets/Data_CTR_Task.png)

The most straightforward way to solve this problem is to label and call the Ad_position and feed some classifier. It would be a very good classifier that could take into account all the hidden relations between variables.
But no matter how good it is, it still treats all the data points independently. And this is where we can apply feature engineering. 

# Useful Features 
For example:
- We can assume that an ad with the lowest price on the page will catch most of the attention. 
    - We can add lowest and highest prices for every user and page per ad.
    - Position of an ad with the lowest price could also be of use in such case. 

![Useful Features]({{ site.baseurl }}/assets/Useful_Features.png)

# Useful Features: Implementation

{% highlight python %}
gb = df.groupby(['user_id','page_id'], as_index=False).agg({'ad_price':{'max_price':np.max, 'min_price':np.min}})
gb.columns = ['user_id', 'page_id', 'min_price','max_price']
gb
{% endhighlight %}

{% highlight python %}
df = pd.merge(df, gb, how='left', on=['user_id', 'page_id'])
{% endhighlight %}

# More features
- How many pages user visited
- Standard deviation of prices
- Most visited page
- Many, many more

# Neighbors
But what if there is no features to use groupby on? In such case, we can replace grouping operations with finding the nearest neighbors.
- On the one hand, it's much harder to implement and collect useful information.
- On the other hand, the method is more flexible.
- We can fine tune things like the size of relevant neighborhood or metric.
- The most common and natural example of neighborhood analysis arises from property pricing. 

### Predict Rental Prices
e.g.
- Number of houses in 500m, 1000m
- Average price per square meter in 500m, 1000m
- Number of schools/supermarkets/parking lots in 500m, 1000m
- Distance to closest subway station

# KNN features in Springleaf
- Mean encode all the variables
- For every point, find the 2000 nearest neigbors using Bray-Curtis metric

$$
\frac{\sum |u_i-v_i|}{\sum |u_i+v_i|}
$$

- Calculate various features from those 2000 neighbors
- Mean target of nearest 5, 10, 15, 500, 2000 neighbors
- Mean distance to 10 closest neighbors
- Mean distance to 10 closest neighbors with target 1
- Mean distance to 10 closest neighbors with target 0
- etc.