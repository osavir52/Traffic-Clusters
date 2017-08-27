# Traffic-Clusters
Spatial analysis of 311 traffic complaints and lower Manhattan construction sites.

This project analyzes whether 311 traffic complaints made in May 2017 were clustered, with statistical significance, around the locations of ongoing construction projecs. 

All work was completed using R. Data was obtained from NYC Open Data portal and the only modification made was to geocode the construction sites (the 311 data already has X-Y coordinates projected in EPSG:2263 - New York/Long Island).

First, let's take a look at the locations of both datasets:

![Plot of 311 traffic complaints and construction sites in New York City](/initial_plot.jpeg)

We can see from this that the 311 traffic complaints pretty spread out throughout the city, so to get a more focused scope let's zoom in on only Lower Manhattan:

![Plot of 311 traffic complaints and construction sites in lower Manhattan](/initial_lowman.jpeg)

Now we have some clusters to work with. Using standard deviation ellipses, we can identify the centerpoint of each cluster and delineate an area of 311 traffic complaints that is within one standard deviation of that center. By eyeballing, it looks like there are roughly 4 clusters, so let's make the ellipses:

![Plot of 4 clusters](/clusters.jpeg)

Now let's take away the traffic complaint data and just look at the ellipses with the construction sites:

![Plot of ellipses and construction sites](/ellipses-consites.jpeg)

Based on this, we can see that only one construction site is anywhere near the center of one of the ellipses. So maybe that construction site actually is responsible for traffic complaints - but more likely it happens to be near the Holland Tunnel, so big surprise that traffic is clustered around that area. It would appear based on this visualization that there is no statistical link between construction sites and traffic complaints.

We can still take this analysis a step further. By using a randomized simulation, we can determine whether there is any statistical spatial link between the datasets. First, let's make a standard deviation ellipse for each dataset and compare:

![S-D Ellipses of traffic complaint and construction data respectively](/traf-const-centers.jpeg)

So the two ellipse's centerpoints _are_ pretty close together. But we can check this for sure using a randomized simulation. First, we calculate the distance between all sets of points for both data sets together and find the mean miminum distance. Then we randomize the data and once again calculate the mean minimum distance, and compare this to our original number. If the two are similar within statistical significance, then there is evidence these two datasets represent the same population. If the two are not similar, then any such linkage that is apparent from visualizing the data is likely a coincidence.

First off, calculating the mean minimum distance of all points, we get 1234.008. My result for simulated mean minimum distance after 100 simulations is 374.4693. Seen visually:

![Graphic results of randomized simulation.](/calc-results.jpeg)

Our randomized mean minimum distance is represented by the red line. If you're wondering where the actual, pre-randomized one is - it's so far out it doesn't even make the graph's parameters. In other words, it is way out of statistical significance!

So we can safely say, based on this data, there is no statistically significant link between the locations of construction sites and 311 traffic complaints in May 2017 in lower Manhattan.

It's worth noting that the complaint data only represents people who bothered to call 311 - so it may not accurately reflected traffic patterns. But hey, it's free data.
