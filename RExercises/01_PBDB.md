# Lab Exercise 01: Introduction to the PBDB

## Finding the Paleobiology Database Website

The URL for the Paleobiology Database is [www.paleobiodb.org](https://paleobiodb.org).  Go there now in your web browser. The first thing that you should see is the **SPLASH** page. 

<a href="url"><img src="01_Figures/Figure1.png" align="center" height="450" width="500" ></a>

The Paleobiology Database (**PBDB** for short) splash page has a lot of information packed into it. At the bottom of the screen you will see some basic stats on the types and quantity of data located in the database.

Data Type | Definition
--------- | ----------
**References** | Scientific articles, books, monographs, or other sources of data.
**Taxa** | A taxon (plural taxa) is a group of one or more populations of an organism or organisms seen by taxonomists to form a unit. 
**Opinions** | Different opinions on the correct taxonomic name/identification of different fossil taxa.
**Collections** | A group (collection) of fossil taxa at a specific location.
**Occurrences** | An individual observation of a taxon at a specific location.
**Scientists** | The number of scientists that are *officially* involved in the Paleobiology Database initiative.

## References

All data in the PBDB can ultimatley be traced back to one or more references. The interface for searching and viewing references is currently being overhauled this semester, which is why there is no search button on the splash page. You can still access the old references search feature by clicking [here](https://paleobiodb.org/cgi-bin/bridge.pl?a=displaySearchRefs&type=view).

The references search page should look something like this.
<a href="url"><img src="01_Figures/Figure2.png" align="center" height="450" width="500" ></a>

#### Exercise Questions 1

Let's take a look at a great scientific paper by Steven M. Holland and Mark E. Patzkowsky. 

<a href="url"><img src="01_Figures/Figure3.png" align="center" height="450" width="500" ></a>

Use the reference search tool to look up collections associated with this paper and answer the following questions.

1. How many collections are associated with this references?

2. What is the reference id number for the article? 

Once you have answered the above questions, click the **view collections** hyperlink to see a print out of the collections associated with the study.

<a href="url"><img src="01_Figures/Figure4.png" align="center" height="450" width="500" ></a>

Click on collection no. **72438**. Answer the following questions about this collection.

<a href="url"><img src="01_Figures/Figure5.png" align="center" height="450" width="500" ></a>

1. The first taxon in the taxonomic list is *Rafinesquina alternata*. Next to the taxonomic name is the citation (Conrad 1830), what is the significance of this citation?

2. What is the *class*, *order*, *family*, *genus*, and *species* name of the second taxon in the taxonomic list?

3. In what County was the data collected?

4. What age (Period) is the data from?

5. What is the geologic formation where the data was found?

## Collections

Collections are useful for getting additional information about the age, location, and geologic context of collected fossils. They are, however, generally a poor tool for data analysis. This is because there is no standard operational definition of a collection in the Paleobiology Database.

For example, collection **72438** from the above example represents a single sample from the study by Holland and Patzkowsky. In that study, a sample represents a single *bedding plane* (i.e., the top of a single rock layer) between 100 cm<sup>2</sup> and 1600 cm<sup>2</sup> in size.

In contrast, collection **91240** represents a single sample in a study by Ivany et al. 2009, Ref# 30540. In that study, a sample was defined as an entire rock outcrop (multiple beds), generally several square meters in extent. 

If you blindly compared these two collections, you would be making an apples and oranges comparison.

## Occurrences

Occurrences are the number of collections that contain a taxon. Since the size and definition of collections is variable, the meaning of occurrences is also somewhat imprecise. 

Therefore, as we progress in this class, you will see that often times the first step of any data analysis project using the PBDB is to reorganize occurrences into a more sensible and standardized format. We will discuss occurrences more when discussing how to download data.

#### Exercise Questions 2

Return to the **SPLASH** page, and enter the PBDB [navigator](https://paleobiodb.org/navigator/) tool. This tool is the best way to visualize the age and location of collections in the PBDB.

<a href="url"><img src="01_Figures/Figure6.png" align="center" height="450" width="500" ></a>

Look at the search bar prompt in the top right corner. Navigator will allow you to enter a geologic time period, a taxon, an authorizer, or a geologic unit. Let's look for the genus *Abra*.

<a href="url"><img src="01_Figures/Figure7.png" align="center" height="450" width="500" ></a>

1. Zoom in so that you can see from Texas to Florida and from Florida to New York. You can zoom using the mouse wheel, by double-clicking, or clicking the **+** and **-** signs. Some of the occurrences are orange and others are yellow, what is the significance of the different colors?

2. Zoom back out. Add an additional filter into the searchbar, the Ypresian stage. The Ypresian is a time interval ranging from 47.8–56.0 million years ago. In what countries are there Ypresian occurrences of *Abra*?

3. Clear the *Abra* and Ypresian filters from the search. Look for the genus *Ambonychia*. Within the United States find the city with the most occurrences of *Ambonychia*. What is the name of this city? 

4. What age (Period) are most *Ambonychia* occurrences?

Add in your answer to question 4 as an additional filter. Click on the little icon of South America breaking away from Africa on the left side of the screen. This icon rotates the continents back to their position in the specified time-period. **Note that it requires you to have set a specific time-period as a filter**. 

5. During this time-period, were most occurrences of *Ambonychia* arrayed parallel or perpendicular to the equator?

6. Click on the little insect icon on the left side of the screen. This brings up taxonomic information on the target taxon. What order does *Ambonychia* belong to?

## Downloading Data

You can download the data displayed in your Navigator window using the little arrow icon on the left side of the screen, but its options are limited. 

To customize the data you want, use the new and more detailed download form. To find the form, return to the **SPLASH** page and click on [Download Data](https://paleobiodb.org/cgi-bin/bridge.pl?a=displayDownloadGenerator). This download form uses the new Paleobiology Database **API**. Once you are more advanced, you will be able to download data directly into R using the **API**, and will no longer need to use Navigator or the download form.

<a href="url"><img src="01_Figures/Figure8.png" align="center" height="450" width="500" ></a>

Let's try downloading all collections of both *Ambonychia* and *Abra* as a tab-separated file. 

1. Select Collections
2. Select Tab-separated values (tsv)
3. Enter Abra, Ambonychia into the Taxon textbar.

<a href="url"><img src="01_Figures/Figure9.png" align="center" height="450" width="500" ></a>

If you were successful you should have gotten a blue URL, describing your data request.

https://paleobiodb.org/data1.2/colls/list.tsv?datainfo&rowcount&base_name=Abra,Ambonychia

#### Exercise Questions 3

For the following questions generate the appropriate URL for the following data queries.

1. What is the appropriate URL for downloading all occurrences of Ambonychia in the Lexington Limestone as a JSON?

2. What is the appropriate URL for downloading all occurrences of mammals present in the Paleocene through Oligocene epochs as a csv?

3. What is the appropriate URL for downloading all opinions on the order Testudines in the Mesozoic?

4. What is the appropriate URL for downloading all collections of Aves, Marsupialia, and Sirenia in the United States as a csv?

5. What is the approopriate URL for downloading all occurrences of the gastropod genus *Ficus* as a csv?

#### Exercise Questions 4

The next set of questions is free form, in that you can find the answer to the following questions using any of the PBDB tools discussed so far.

1. What family does the genus *Gastrocopta* belong to?

2. There is only once occurrence of *Isoetes* in Portugal. What age is it?

3. What is the age of the oldest occurrence of *Gastrocopta*?

4. There is only one occurrence of *Tiktaalik* in the Paleobiology Database? Was that occurrence located in the tropics or the extratropics when it was alive?

5. There are two occurrences of *Namacalathus* in Sibera. What geologic formations are they found in?

## Paleobiology Database API

The acronym API stands for Application Programming Interface. Technical definitions aside, it is a way for users to access data stored in an online database through web addresses (URLs). Companies that store a lot of data (e.g., Google, Twitter, Facebook) make API's available so that 3rd party developers can use their data to make applications. For example, if you've ever played a Facebook game (e.g., Candy Crush, Farmville), those programs were accessing information about you and your friends through the API.

The best way to think about using an API is to imagine it as a map to all the data stored online. You need to use this map to give the computer directions on how to find the particular data you want and access it. When we give directions to a location in the real world, we generally do so in two ways. We either give geographic coordinates (i.e., latitude, longitude, elevation) that specify the destination, or a set of routes to get somewhere (e.g., Take I-90 E to Chicago, then I-80 W to Joliet).

When we access data in R via **subscripting** (````Object[ ]````), we are using a coordinate system to point out the data in our object. In contrast, when we access data through an API we are defining a **route**. In fact, route is the formal terminology. Depending on the size of an API there may be dozens of routes, which may feel overwhelming at first. However, remember that a car map has thousands or hundreds of thousands of roads, most of which you will never travel upon, but you still know how to use a map. It is the same way with an API.

Let's deconstruct a specific API **query** (i.e., URL).

````
https://paleobiodb.org/data1.2/occs/list.csv?base_name=Smilodon&interval=Pleistocene
````

The following figure deconstructs each element of this query.

<a href="url"><img src="01_Figures/API.png" align="center" height="600" width="750" ></a>

The first half of the query, before the **?** is fairly straightforward because there are only a few possible variations. However, the **parameters** that come afterwards can become quite cumbersome because there are many varieties of them, and many of them will change depending on what type of data you are using (i.e., collections vs. occurrences). You will need to use the documentation to see a full list of the possible paramters.

+ [Occurrences Parameters](https://paleobiodb.org/data1.2/occs/list_doc.html)
+ [Collections Parameters](https://paleobiodb.org/data1.2/colls/list_doc.html)
+ [References Parameters](https://paleobiodb.org/data1.2/refs/list_doc.html)
+ [Opinions Parameters](https://paleobiodb.org/data1.2/opinions/list_doc.html)
+ [Specimens Parameters](https://paleobiodb.org/data1.2/specs/list_doc.html)

You can also access the API documentation from the main SPLASH page.

<a href="url"><img src="01_Figures/Figure10.png" align="center" height="450" width="500" ></a>

This will take you to a page that lists the different data routes. If you click on those routes, it will take you to pages that describe different parameters associated with the chosen route. Let's take a breather though and answer some questions.

The API is most useful for using in programs like R (or for making web or smart phone apps). As indicated in the API documentation, you can request files in several different formats. Importantly, you can directly dowload files into R. Two of the most use ful are CSV and TSV. CSV stands for **comma separated file**, it is one of the most common file formats used in R for storing two-dimensional arrays - i.e., matrices or data frames. You can also view, create, and edit them using a spreadsheet program like Microsoft Excel.

#### Exercise Questions 5

````
https://paleobiodb.org/data1.2/colls/list.csv?base_name=Mammut&interval=Pliocene
````

1. What code would you use to download the above PBDB data directly into R? Hint: ````?read.csv````

2. Download the above data into R. What are its dimensions?

3. Did the above call use the occurrences, collections, references, opinions, or specimens route?

4. What genus is being called for? What is its colloquial name? What age did I limit the data query too?

5. Look through the service documentation for the appropriate route (based on your answer to Question 2). Find out how to extend the age search to range from the Miocene Epoch through to the Pleistocene Epoch. Give the new data query URL.

6. I want the data query to show me the paleocoordinates (i.e., paleolatitude and paleolongitude) of each data point. Give the updated data query URL.

## Writing your own API function in R

Wouldn't it be really convenient if instead of typing out the URL every time, you could write an R function that takes a specific **taxon name** and **interval** and downloads the data into R automatically? 

Specifically, your final question for this lab is to write a function in R that will take as its arguments a **taxon name** and an **interval**, and download all fossil occurrences from the PBDB as a CSV.

Your final product should look like this:

````
# Download all instances of the genus Abra from the Pleistocene interval
AbraData<-downloadPBDB(taxon="Abra",interval="Pleistocene")

# Your output should look like this
AbraData[1:6,1:6]
  occurrence_no record_type reid_no flags collection_no identified_name
1         94761         occ      NA    NA          7108   Abra aequalis
2        256368         occ      NA    NA         20604   Abra aequalis
3        256386         occ      NA    NA         20606   Abra aequalis
4        425385         occ      NA    NA         41501   Abra aequalis
5        427341         occ      NA    NA         41705   Abra aequalis
6        427901         occ      NA    NA         41740   Abra aequalis

# Download all instances of the genus Tyrannosaurus from the Mesozoic
TRexData<-downloadPBDB(taxon="Tyrannosaurus",interval="Mesozoic")

# Your output shoud look like this
TRexData[1:6,1:6]
  occurrence_no record_type reid_no flags collection_no       identified_name
1        139292         occ   22878    NA         11917     Tyrannosaurus rex
2        139293         occ      NA    NA         11918 Tyrannosaurus cf. rex
3        219998         occ      NA    NA         22654     Tyrannosaurus rex
4        220009         occ      NA    NA         22657     Tyrannosaurus rex
5        280101         occ      NA    NA         26760     Tyrannosaurus rex
6        291021         occ      NA    NA         14640 Tyrannosaurus cf. rex
````

In order to achieve this you will need to use the ````paste( )```` function. Here are some examples of the paste function in use. See if you can figure out how it fits into the problem.

````
# Example 1
paste("We","Love","R",sep=" ")
[1] "We Love R"

# Example 2
paste("We","Love","R",sep="")
[1] "WeLoveR"

# Example 3
paste("We","Love","R",sep="!")
[1] "We!Love!R"

# Example 4
LoveR<-c("We Love R")
HateR<-c("We Hate R")
paste(LoveR,HateR,sep=" >> ")
[1] "We Love R >> We Hate R"
````

#### Question 6

1. Write an R function that will take a taxonomic name (as a character string) and an interval (as a character string) as its argument, and will download all fossil occurrences into R. See above.

## Morphologic Measurements

Some species have morphologic data attached to them in the Paleobiology Database. Let's consider the following three species of Ammonite: *Glyptophiceras sinuatum*, *Xenoceltites variocostatus*, and *Submeekoceras mushbachanum*. 

Each of these species have morphologic data (e.g., shell width measurements) attached to them in the paleobiology database. You can search for this information by searching taxonomic names [here](https://paleobiodb.org/cgi-bin/bridge.pl?a=beginTaxonInfo).

1. Look up *Glyptophiceras sinuatum*, *Xenoceltites variocostatus*, and *Submeekoceras mushbachanum* in the Paleobiology Database. Find the first person (journal paper/reference) to name this species. (Hint: For *X. variocostatus *, both the first and second author's last names start with "B"). What is the name of the article for each?

2. Do a [google scholar](https://scholar.google.com/) search for the article that first names *Xenoceltites variocostatus*. Open it and scroll down to the "Plates" subsection. You should see various pictures of different ammonites towards the very end of the article. Find the pictures of *Xenoceltites variocostatus*. Which plates illustrate this species, and how what is the maximum diameter of the illustrated specimens (in units of mm)?