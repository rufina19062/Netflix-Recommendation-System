# **Implementation of Cosine Similarity Method for Netflix Recommendation**

![image](https://user-images.githubusercontent.com/90761863/213609378-aaabd38f-ed8e-4dfd-ac89-fb98796d177c.png)


This project was created by:
- [Rufina Indriani](https://www.linkedin.com/in/rufina-indriani-/)
- [Rizki Tetania](https://www.linkedin.com/in/rizki-tetania-mahalang/)

you can view our presentation [here](https://docs.google.com/presentation/d/1m542BlPlI5GM8OF-yqRQ6lnil4fX6ZykFHTgUBv94SI/edit#slide=id.g1d6e0c26920_0_360)

Movie/Tv show is visual entertain created in 19th century that can also use as education and represent social issues. There is a lot type of movies and Tv shows in now days. We can also watch it in many platform, spacially in online platform. There is many streaming platform for us to watch movies and Tv shows, one of the famous streaming platform is Netflix. [Netflix](https://about.netflix.com/en) was created in 1998 as a DVD rental and sales site and in 2007 you can use Netflix as streaming platform allowing members to instantly watch movies and TV shows. Netflix have recommendation system to predict future choice for membership to watch. This method can increase membership loyalty because Netflix can give them something they like to watch. 

Recommendation system is a [[1]](https://dl.ucsc.cmb.ac.lk/jspui/bitstream/123456789/4596/1/2018%20BA%20033.pdf) Sudasinghe, P.G. (2019). Enhancing Book Recommendation with the use of Reviews. Sri Lanka: University of Colombo School of Computing.

Content-based Filtering 
[[2]](https://iopscience.iop.org/article/10.1088/1742-6596/1000/1/012101/pdf) Geetha, G., Safa, M., Fancy, C., & Saranya, D. (2018, April).A hybrid approach using collaborative filtering and content based filtering for recommender system. In Journal of Physics: Conference Series (Vol. 1000, No. 1, p. 012101). IOP Publishing. DOI:10.1088/1742-6596/1000/1/012101.
[[3]](http://singhal.info/ieee2001.pdf) Singhal A 2001 Modern Information Retrieval: A Brief Overview Bulletin of the Technical Committee on Data Engineering pp 35–43.


## **Business Statement**
Based on its website on [netflix.com](https://help.netflix.com/en/node/412), Netflix is a subscription-based streaming service that allows members to watch TV shows and movies on an internet-connected device. Users can also download TV shows and movies to their devices and watch it without internet connection. Netflix have content varies by region and may change over time. You can watch a variety of award-winning Netflix originals, TV shows, movies, documentaries, and more. Netflix also have recommendation on TV shows and movies for their users to watch. The more you watch, the better Netflix gets at recommending TV shows and movies. So, this project is an implementation of recommendation system on Netflix dataset to predict similar TV shows and Movies based on its title and description.

**Problem Statement**

Based on the statement, the problems in this project are explained as follows:
- Based on certain title, how to identify any titles that has similar content?

**Goals**

the following goals:

- Predict 10 titles based on similarity of certain title with .

**Solution Statement**
So to achieve the desired goals, a recommendation system will be formed with the following flow.

1. Data Understanding
> Data Understanding is the initial stage of the project to understand data. In this case, we have 12 variables with missing values on 6 variables.

2. Univariate Exploratory Data Analysis
> Analyze and explore several variables in the data. 

3. Data Preparation
> This is the preparation of data before analyzing dataset with recommendation system.

4. Recommendation System with Cosine Similarity
> This step give several titles which have similarity based on certain titles. The title recommendation is obtained from the text similarity on titles and description. This method calculate the similarity of two vector, but in this case we have to vactorize the text first to calculate the similarity. The result of this methode is number of persentage similarity between two text. In order to get the title recommendation, we have to choose the largest similar number and get the title of TV Series or Movies and the description.



## **Data Understanding**
The data in this project comes from [Netflix Movies and TV Shows dataset](https://www.kaggle.com/datasets/shivamb/netflix-shows). 

**About this Dataset**: Netflix is one of the most popular media and video streaming platforms. They have over 8000 movies or tv shows available on their platform, as of mid-2021, they have over 200M Subscribers globally. This tabular dataset consists of listings of all the movies and tv shows available on Netflix, along with details such as - cast, directors, ratings, release year, duration, etc.
Netflix dataset has 12 variables and description of these variables are as follows.


Table 1. Variable of Netflix Dataset
|Variable | Description|
|---|---|
|show_id	|	Unique ID for every Movie / Tv Show
|type	|	Identifier - A Movie or TV Show
|title	|	Title of the Movie / Tv Show
|director	|	Director of the Movie
|cast	|	Actors involved in the movie / show
|country	|	Country where the movie / show was produced
|date_added	|	Date it was added on Netflix
|release_year	|	Actual Release year of the movie / tv show
|rating	|	TV Rating of the movie / show
|duration	|	Total Duration - in minutes or number of seasons
|listed_in	|	Genre
|description	|	The summary description


## **Preprocessing Data**
Before we get our hand dirty with netflix dataset, we have to preprocess the data in order to create better result.
In this step we process the missing value of dataset.

Netflix dataset have missing values in:
- "director": Very little information (even though we have searched the internet, the information on the name of the director of the Movie/TV Show is still very minimal, and the truth cannot be confirmed) so we will be dropping this variable.
- "cast": there are too many different values, so we also dropping this variable.
- "country": Important variable so we need to fix it
- "duration": there are only a few cases (where an error occurs during data entry) so let's fix it
- "rating": there are only a few cases, so let's fix it.
- "date_added": there are only a few cases (and I can't find out in the Internet) so I will drop these as they are only 10 rows


## **Univariate Exploratory Data Analysis**
There are more movies titles than TV show titles in Netflix. This is proofen by the persentage rates of types of titles which has 69.7% movies titiles and the rest is TV show titles.
Exploratory netflix data divided into 2 dataset, which is netflix titles for TV show and netflix titles for movies
- Top Rating
![Top 5 ratings movies](https://user-images.githubusercontent.com/90761863/213623100-fb2c9609-f4c4-40b7-bc4b-6b39be14c684.png)

![image](https://user-images.githubusercontent.com/90761863/213612440-4c80e27d-f555-4355-a35f-a6b8c97191ea.png)

Figure 1. Barplot of rating

Figure 1 The graph explains the most rating categories in the two programs. Where in the first and second order have the same category, namely TV-MA and TV-14.
TV-MA: designed specifically for viewing by adults and thus not suitable for children under 17 years of age.
TV-14: This program contains some material that many parents find unsuitable for children under the age of 14

So it can be concluded that the majority of streaming services provided by Netflix have TV-MA and TV-14 rating categories.





- Top Release Year

![image](https://user-images.githubusercontent.com/90761863/213612462-fff8b3ad-fbdc-485b-a137-e35836648a64.png)

![image](https://user-images.githubusercontent.com/90761863/213612474-4137cd7c-600b-452f-9ea1-125df69cd4da.png)

The actual release year of the film is mostly in 2017 and the actual release year of the TV Show is mostly in 2020.
So when compared to Movie streaming, the majority of TV Show streaming services use the latest content.



- Top Genre

![image](https://user-images.githubusercontent.com/90761863/213612510-365c15e0-da04-47f1-8e8d-a7f61302435e.png)

The film genres most often released by Netflix are drama, comedy, action and international movies. Based on 8797 data in the list of Netflix streaming program titles, 362 data are streaming programs with Drama and International Movie genres.

![image](https://user-images.githubusercontent.com/90761863/213612526-d0b04572-1d05-4efc-8307-b2c15f41c689.png)

The TV Show genres most often released by Netflix are International TV, romantic, comedies, Kid's TV, and drama. The Wordcloud provides information that one of the reasons Netflix is more attractive to users is because the genre of the program being broadcast is an international genre.


- Top Country

![image](https://user-images.githubusercontent.com/90761863/213612548-6b4dd41c-81b3-4cd5-ba8c-05032bfb703b.png)

![image](https://user-images.githubusercontent.com/90761863/213612558-2a956619-9740-4975-8645-6813526bbcfa.png)

![image](https://user-images.githubusercontent.com/90761863/213612570-8afdbeda-d271-4e5e-9cb1-b48193ba0895.png)

Based on the 782 countries that have contributed to their work on the Netflix streaming service, there are 3 countries that have contributed the most, namely the United States with 2,818 Movie/TV Shows, followed by the United Kingdom and India.
The three countries have a sizable contribution to Netflix, this data can represent that Netflix users are more interested in streaming movies and TV shows from these three countries. So that based on the information obtained, it can be used as a reference for future decision making.


## **Build Model with Cosine Similarity**


## **Conclusion**


## **Reference**
[[1]](https://dl.ucsc.cmb.ac.lk/jspui/bitstream/123456789/4596/1/2018%20BA%20033.pdf) Sudasinghe, P.G. (2019). Enhancing Book Recommendation with the use of Reviews. Sri Lanka: University of Colombo School of Computing.
[[2]](https://iopscience.iop.org/article/10.1088/1742-6596/1000/1/012101/pdf) Geetha, G., Safa, M., Fancy, C., & Saranya, D. (2018, April).mA hybrid approach using collaborative filtering and content based filtering for recommender system. In Journal of Physics: Conference Series (Vol. 1000, No. 1, p. 012101). IOP Publishing. DOI:10.1088/1742-6596/1000/1/012101. 
[[3]](http://singhal.info/ieee2001.pdf) Singhal A 2001 Modern Information Retrieval: A Brief Overview Bulletin of the Technical Committee on Data Engineering pp 35–43.
