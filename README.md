# DSI-Capstone
The problem statement I entered this project looking for an answer to was, is there racial bias in the words used by newspapers, in this case, the New York Times, when covering mass shootings in relation to the ethnicity of the shooter. If so, does the content predict racial bias.

#### The Data
The data was initially gathered from two main sources the Stanford University Mass Shooting Database and the New York Times. I chose the Stanford database because they are among the leading data collectors when it comes to mass shootings in the US. In fact, they are the ones who created the current definition of what constitutes a mass shooting. That is if four or more people are wounded or killed. Their database consists of every incident between 1966 and March 2016. However, due to the format of the New York Times files, I was unable to get articles from the 1960s and thus only used articles from 1970 to March 2016. The New York Times was selected because it is one of a few papers who cover national news that has readily available archived articles. The data chosen from the New York Times was every article and article title related to each incident from the day of the incident and the six days following. This period was selected because it is the typical length of one news cycle.

The final data features that would be used for the model would be the Incident Name and Shooter Race features from the Stanford Database and each articles content and its title. After reviewing the ethnicities in the database, I discovered that Latin Americans were largely classified as "other" and as such I researched each individual to confirm their ethnicity and changed it in the data frame. The races included were (in order of Number of Shooters) White, Asian, African American, Latin American, and Native American or Alaska Native.


#### Preparing the Data
To prepare the data for Natural Language processing, certain steps had to occur to assure smooth processing and least amount of unnecessary words. This was done by using a function that removed non-letters, made every letter lower case, and removed the standard English dictionary words as well as my custom list of stopwords which included the location of the shooting, the shooters name, month, and the name of the incident. In addition, in using, Tokenizer, Lemmatizer, and Stemming I was able to cut down on the repeating of words that are basically the same as run, runs, running, and ran.

The other major challenge here with the data was to manage the unbalanced classes before doing a train-test split or countvectorizing. The numbers of occurrences were massively imbalanced because as expected their ethnicities were not evenly spread. The spread, in percent, is as follows:

    White = 68.66%
    Asian = 14.43%
    African American = 14.43%
    Latin American = 2.09%
    Native American or Alaska Native = 1.33%

These numbers are actually quite interesting when you compare them to the demographic make up of the entire US populationm, which is as follows:

    White = 72.4%
    Asian = 4.8%
    African American = 12.6%
    Latin American = 16.3%
    Naive American or Alaska Native = 0.9%

In addition, using the SKLearn Logistic Regression model I found that a large portion of words had no impact(positive or negative) on my variables and as such decided to remove them from my model and expediting the processing of the rest of my data.

### Model Selection
To adjust for the unbalanced classes I chose to use Random Forest Classifier as it creates multiple decision trees with Bootstrapped Aggregation to better handle the unbalanced nature of the information. In the future I hope to gather more information from more news sources to help balance the data, but as this data is sadly dependent on more mass shootings happening I do hope that the only data I can get more of is articles of past events and not of those that hopefully will be as sparse as possible in the future..

Multiple RandomForest Models were created. The first is to see what the most important features are in relation to the Shooter Race Column in general. Then the following models were generated comparing the same words from the first model to see how they interacted with each race and see if there was a clear indication of different words being used and if they are particularly geared towards a specific race.

### Statistical Analysis, Recommendations, and Next Steps
The General Random Forest generated a cross-validation score of .71. The modelling was much more precise with Latin Americans(98.1%), Native American or Alaska Native(98.8%), and Asian(98.8%).As well as 89.1% for African Americans and a surprisingly low number of 72.6% for White.

While the model appears to be precise in predicting certain races it is lacking in other areas and needs to be adjusted to counteract oversampling. Once the feature importance’s are printed out it is clear that there are no certain words that appear in an article by the New York Times that would specifically indicate the individual race of the shooter despite some that are quite compelling. While this does allow me to reject my hypothesis (good news for the New York Times) moving forward I would like to look at more national newspapers and see how they differ by location, region, political leaning. I would also like to see how the local papers covered events to see if their focuses are primarily on the crime, the shooter, and event that occurred or upon helping the families affected by the horrible events.
