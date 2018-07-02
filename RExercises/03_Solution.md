# Recreating Figure 1 From Heim *et al.* 2015

````r
> # Read in dataset directly from the web
> sizeData <- read.delim(file='https://stacks.stanford.edu/file/druid:rf761bx8302/supplementary_data_file.txt')

> # checkout the dataset
> dim(sizeData) # there are 17208 rows and 14 columns
> head(sizeData)

> # Read the timescale file in directly from the web
> timescale <- read.delim(file='https://raw.githubusercontent.com/naheim/paleosizePaper/master/rawDataFiles/timescale.txt')

> # Open a plot window, make and empty plot and set the x and y limits of the plot as well as the x and y axis labels.
> plot(1:10,1:10, type="n", xlim=c(550,0), ylim=c(-2,12), xlab="Geological time (Ma)", ylab=expression(paste("Biovolume (log"[10]," cm"^3)))

> # add the genus ranges using segments()
> segments(sizeData$fad_age, sizeData$log10_volume, sizeData$lad_age, sizeData$log10_volume)

# calculate the mean size & percentiles of all animals in each of the geologic time interval

> # set up vectors
> myMean <- vector(mode="numeric", length=nrow(timescale))
> my05 <- myMean
> my95 <- myMean
> for(i in 1:nrow(timescale)) {
	temp <- sizeData[sizeData $fad_age > timescale$age_top[i] & sizeData $lad_age < timescale$age_bottom[i], ]
	myMean[i] <- mean(temp$log10_volume)
	my05[i] <- quantile(temp$log10_volume, 0.05)
	my95[i] <- quantile(temp$log10_volume, 0.95)
}

> # add the lines
> lines(timescale$age_mid, myMean, col='red', lwd=2.5)
> lines(timescale$age_mid, my05, col='red')
> lines(timescale$age_mid, my95, col='red')
````