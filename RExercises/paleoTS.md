# Learning to use the *paleoTS* package for modeling evolutionary trends


## goals
* learn how to install and run an R package
* practice making plots in R
* become more familiar with the concepts of *random walk*, *directional trend*, and *stasis*.
* use the *paleoTS* package to choose the best-fit model for our size data

## Installing packages.
Packages are bundled sets of R functions written by users who want R to perform specific tasks. There are hundereds of packages and you can even write your own. Today we will learn to use the *paleoTS* package, which was written by Gene Hunt, who wrote the [Hunt 2007](https://github.com/naheim/seyibExercises/raw/master/ReadingExercises/papers/Hunt2007.pdf) paper we read.

1.	Choose an R mirror site to download and install packages from -- once you do this you won't have to do it again -- choosing a nearby mirror will increase the download speeds through distributing the server traffic and reduced distance the data has to travel

	* you want to select the mirror that is geographically close to you.  At Stanford this is the mirror housed at UC Berkeley.
	
	* from the application menu go to: R -> Preferences... -> Startup
	
	* Hit the "Select" button under the section titled Default CRAN mirror and scroll down and choose "USA (CA 1)" and close the preferences menu.

2. install the paleoTS package by launching the Package Installer: R -> Packages & Data -> Package Installer
	* Make sure the top right dropdown menu has "CRAN (binaries)" selected
	* Hit the "Get List" button, which will generate a list of all the available packages (from the Mirror you selected in step 1)
	* Type "paleoTS" into the package search box and you'll see it listed on the screen below
	* Highlight the paleoTS package, make sure the "Install Dependencies" box is checked (this will download all the packages that paleoTS requires), hit "Install Selected"



````r
# load the paleoTS library
# packages installed through the Package Installer are not automatically loaded, so you need to tell R to load the packages you want with the library() command
# it is always a good idea to load all the needed libraries at the top of your script
library(paleoTS) 

# read in size and timescale data files
sizeData <- read.delim('bodySizes.txt') 
timescale <- read.delim('timescale.txt') 

# USING the paleoTS package.
n.bins <- nrow(timescale) # this is just a variable for the number of time intervals.  This will be useful in writing loops, an is a bit easier and faster than writing nrow(timescale) every time you need to know how many time intervals there are
````

### paleoTS Usage
*paleoTS* requires four vectors of data: mean, variance, sample size, and age of time interval. The simplest way to get these vectors is to write a loop:

#### Refresher on Writing Loops
* Writing loops is very useful for all sorts of analyses -- sometimes R is slow at loops but for a relatively small data set like the one used here, it's not too bad. The idea behind a loop is that you want to do the same thing to some set of data over and over again. For example, we want to caclulate the mean, variance and sample size of maximum length for each time interval in the geological timescale.

* The most basic, common and easiest loop to use is called a *for* loop. Conceptually, there are three parts to a for loop: an iterator, a start value, an end value.  By convention, the iterator vairialbe is usually called "i", although you can call it anything you want. The basic process of a for loop is to set the iterator vairable equal to the start value, do whatever it is you want to do (in this case calculate mean, variance and sample size), then add 1 to your iterator variable and repeat the calculation.  This continues until the iterator variable equals the stop value.

Let's first set up some vectors to hold our raw data that we will pass to paleoTS.

````r
my.mean <- vector(mode="numeric", length=n.bins)  # this is a vector that will hold number and has the same length as our timescale
my.var <- vector(mode="numeric", length=n.bins)
my.n <- vector(mode="numeric", length=n.bins)
my.time <- timescale$age_bottom  # we don't really need to make a separate variable for this, but just for clarity I have.  Also not that I've used age_bottom (rather than interval midpoint or age_top) so that the duration of each stage are calculated by paleoTS

# just to make thigs easier to read, we are optionally naming each value in our vectors after the time interval they correspond to
my.mean # look at the nameless empty vector
names(my.mean) <- timescale$interval_name
my.mean # now look at the empty vector with each value named
names(my.var) <- timescale$interval_name
names(my.n) <- timescale$interval_name
names(my.time) <- timescale$interval_name

for(i in 1:n.bins) {  #all three parts of the for loop are called inside for function.  i = iterator variable, 1 = start value, n.bins = end value.  In english this means For each value of i between 1 and n.bins (97 in this case), including the endpoints, do whatever is inside the curly braces
	temp.data <- log10(sizeData$max_vol[sizeData$fad_age > timescale$age_top[i] & sizeData$lad_age < timescale$age_bottom[i]])
	# Here we're getting the subset of max_length from my.data where
	#	a. the base of the stratigraphic range  (fad_age) is older than the top of the i-th interval
	#	b. AND the top of the stratigraphic range  (lad_age) is younger than the base of the i-th interval
	#	this will give us all genera whos stratigraphic range intersects the i-th interval
	# NOTE that we've taken the log10 of the max lengths
	
	my.mean[i] <- mean(temp.data)  # we are setting the i-th value of my.mean to the mean of our subset of data
	my.var[i] <- var(temp.data)  # variance
	my.n[i] <- length(temp.data)  # sample size
}
````

Now that we have all the vectors we need, we can make an obect that is of type 'paleoTS' and fit the evolutionary models to our mean size trend.

To fit the evolutionary models, we first need to take our 4 data vectors and make them into a paleoTS object using the ``as.paleoTS()`` function. Below is the code for creating the object. If it makes total sense, great! If not, run ``?as.paleoTS`` to read the help file with a full descriptions. In short though we are giving the function our four vectors and telling it with ``oldest="last"`` that our vectors are ordered with the youngest time interval first and the oldest interval last.

````r
my.ts <- as.paleoTS(mm=my.mean, vv=my.var, nn=my.n, tt=my.time, oldest="last")  

# fit three evolutionary models and print the output
fit3models(my.ts, method="Joint", pool=FALSE)
````

The rows in this output are: GRW = driven trend, URW = unbiased random walk, stasis = Stasis

The most important column in the output is the Akaike.wt, which ranks the models by how well the fit the data.  The model with the highest value has the most support. In this example, the trend is mean animal body size is best fit by an unbiased random walk. ***Make sure you understand what an unbiased random walk is***

### Make a plot of our mean size trend

````r
plot(timescale$age_bottom, my.mean, xlim=c(541,0), type="o", pch=16, xlab="Geologic time (Ma)", ylab=expression(paste("Mean body size (log"[10],"mm)")))
````
The above code makes our basic plot. However, it is the best practice to add confidence intervals to our plots. Because we have calculated the mean value from a sample of fossils (we have not measured every single marine fossil genus that ever lived), we would expect that if we were to sample a different set of genera we might get a slightly different mean value for each time interval. We can use the mean and variance to tell us how confident we should be in our estimates. 95% confidence intervals tell us that if we were able to resample the fossil record 100 times, the mean value would fall within in the range of the confidence interval 95 of those time. In other words, we are 95% confident that the true mean is within the range.


The formula for 95% CI on the mean is: **mean +/- 1.96*standard deviation/sqrt(n)**. Note that the standard deviation is simply the square root of the variance. 

Let's write a loop to plot our confidence intervals

````r
for(i in 1:n.bins) {
	ci <- 1.96 * sqrt(my.var[i]) / sqrt(my.n[i])
	# 2 points will define our confidence interval lines so let's just make x and y vectors to make the lines() command look neater
	my.x <- rep(timescale$age_bottom[i], 2)  # rep() repeats a value.  Since we want a vertical line, both points will have the same x-value
	my.y <- c(my.mean[i] + ci, my.mean[i] - ci)
	lines(my.x, my.y, lwd=0.75) # ldw is line width and here we're plotting CI lines that are 0.75 times as thick as the default line (i.e., 25% thinner)
}
````

# Now you have a publishable figure!!!