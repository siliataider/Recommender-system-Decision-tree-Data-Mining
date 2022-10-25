# 📳 Recommender system - Decision tree

This project was developped whithin a Data Mining course.

## Goals

- Implementation of a [Recommender system](https://en.wikipedia.org/wiki/Recommender_system) in Python


The goal of this project is to recommend images based on the preferences
of the user, while ensuring that all the tasks related to data acquisition, annotation,
analysis, and visualization are automated.

The main tasks of the project are:

1.  💻 Data Collection
2.  🖱 Data filtering
3.  📔 Labeling and Annotation
4.  💽 Data Analyses
5.  🖥 Data Visualization
6.  🖱 Recommendation System
7.  ✅ Tests
8.  📓 Report

## Data Collection

<p align="center">
<img src="https://user-images.githubusercontent.com/69010419/197755060-a22dffd2-5ae9-4c0c-8612-7d8539827d74.png" width="400">
</p>

We worked with kaggle, an open-licensed images plateform where we chose our dataset from, it containes pictures of cats, dogs and monkeys as well as some information in a separate csv file.

The dataset contains 2 folders:
➔ Train ⇒ Contains 1309 éléments.
➔ Test.

We then worked on collecting the basic metadata of every image ans stored it.

## Data filtering

In this task, you may need to label, annotate and save additional
information about every image. You may analyze the images using
clustering algorithms for finding the predominant colours.

You already have some metadata from the EXIF of images from the previous
task. In this task, your goal is to obtain additional information, like
the predominant colors, tags. How about asking users to tag the images?
E.g., color names, \#cat, \#flower, \#sunflower, rose etc. How are you
planning to process the user tags? Is it possible to automate this
process?

Before starting our program, we first filtered the relevant information for us, mainly:

➔ The dataset contained “.xml” files that we didn't have any use for.
➔ The dataset contained duplicates: nwe used the
.drop_duplicates() method on the .csv file before converting it to the json and creating the
dataframe.
➔ After the cleanup, we had 469 images to treat.

## Labeling and Annotation

We went through 2 main steps: transformationm and lebeling & annotation.

We at first had 8 key information on every image:

    ➔ filename.
    ➔ width.
    ➔ height.
    ➔ class (“cats”, “dogs”, “monkeys”).
    ➔ xmin, ymin, xmax, ymax (bounding box coordinates).
    
We decided to keep these elements:

    ➔ width
    ➔ height
    ➔ class

And we decided to treat the rest of the elements to get new information out of them: 

    ● Transformation: The animal's size inside the image.
    
In order to do that, we made use of the bounding box coordinates :

    ■ tailleX = xmax - xmin.
    ■ tailleY = ymax - ymin.
    
We then used a label encoder to define 3 categories :

    ■ Object size < 30% image size: small ⇒ 0.
    ■ 70% image size > Object size > 30% image size: médium ⇒ 1.
    ■ Object size > 70% image size: large ⇒2.
    
    LabelEncoder imported from sklearn.preprocessing

The second main information we tried to extract is: 

    ● Traitement: Dominating color.
    
In order to do that, we used a clustering algorithm:

    ■ Mini Batch K-means, with 3 clusters.

○ we imported conversion functions
from webcolors, mainly css3_hex_to_names and
hex_to_rgb to make the colors understadable.

The final dataframe contained:

| width | height | class | tailleX | tailleY | couleur1 |



## Data Analyses

In order to simulate a user liking or not a picture we generated a "likes" column that either contains the value "favorite" (1) or "nor favorite" (0) that we inserted in our resultframe. The data was randomly generated.

We then built our user-preference profile.


## Data Visualization

We tried to visualize the most relevent information, so we implemented:

    ➔ Un plot.bar to visualize the “width” and “height” (image size):
    ➔ Un plot.bar to visualize “tailleX” et “tailleY” (object size):
    ➔ Un plot.bar to visualize the dominant color.
    
![image](https://user-images.githubusercontent.com/69010419/197754960-ef60c61c-9ffe-4c63-8de9-8a779f31e150.png)
    
    ➔ In this example the user seems to have a preference towards pictures with a medium width and a medium height.
    ➔ He seems to like objects with a medium width (tailleX) and objects with a medium to large height (tailleY).
    ➔ The user seems to like objects with the color code 12.
    
    

## Recommendation System

In order to satisfy the original goal of the project, we decided to work with decision trees.

It's a supervised learning method, non paramétrique used for classification and régression. The goal is to create a model that can predict the value or a target variable taking into consideration the rules of simple decisions deducted fron the iven characteristics.
The deeper the tree is, the more complex decision making rules are, and the fitter the model.

We imported DecisionTreeClassifier avec ces deux lignes :

     ➔ from sklearn import tree
     ➔ Xxx = tree.DecisionTreeClassifier()
     
We then applied this classifier on out data

    ➔ xxxx = xxxx.fit()



