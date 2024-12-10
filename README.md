# Exploring the Connections: How the 'Healthy' Tag Relates to Other Tags and Nutritional Features
Author: Grace Trainor

# Preview 

Following is a data science project that dives into the relationship between the recipe tag 'healthy', other tags, and other nutrional features, such as sodium. 

# Introduction

This project focuses on understanding patterns in two datasets: recipes and ratings posted on Food.com since 2008. Recipes play a crucial role in shaping our meals, our days, and sometimes even our well-being. Beyond taste and satisfaction, having access to healthy recipes that properly fuel and fulfill one’s nutritional needs is vital for daily life. In this project, we aim to answer the central question: "What are the key factors that determine whether a recipe is 'healthy'?"
This question matters because understanding the attributes of healthy recipes can empower individuals to make informed choices, leading to better health outcomes. Additionally, it can help food enthusiasts, nutritionists, and recipe creators craft meals that align with diverse dietary needs and preferences. 

Recipe: the first dataset, which has 83782 rows and 12 columns. Every row pertains to a unique recipe. 

insert chart here

Interactions: the second dataset, which has 731927 rows and 5 columns. Each row represents a review for a recipe. 

insert chart here

Provided these datasets, I am investigating whether a recipe with a 'healthy' tag will exhibit specific patterns in terms of the other tags and nutritional features that it is described by. As a result, I separated the values in the 'nutrition' column into individual columns, such as 'calories (#)', 'sugar (PDV)', and others. I additioinally created a 'healthy' column that consisted of True and Falses, true if one the recipes describing tags was 'healthy' and false if not. The most relevant columns for this question are 'tags', 'calories', 'sodium, 'minutes', 'n_steps', 'protein', 'rating', and 'healthy. 

This question is important because understanding these associations can help individuals better identify recipes that align with their dietary goals. It can also support recipe creators and platforms in improving categorization and recommendations for health-conscious users.

# Data Cleaning and Exploratory Data Analysis

In order to properly use the datasets and discover accurate results, I performed data cleaning on these two datasets. 

1. Left merge the recipes and interactions datasets on id and recipe_id.
    This allows for the recipes to be connected with their reviews and ratings.
2. Fill all ratings 0 with np.nan
    Ratings are typically from 1-5, with 1 being the lowest and 5 being the highest. 0 as a rating doesn't make sense and rather is meant to represent missing ratings. So to fix this, I represent all 0 ratings as np.nan
3. Add column 'avg_rating' containing average rating per recipe.
    This allows for a deeper understand of the overall consensus for a recipe, across different users. 
4. Split values in the nutrition column to individual columns. 
    The values are objects and in order to use them properly it was essentially to turn them into individual, usable columns. 
5. Convert submitted and date to datetime.
    Converted these two columns to datetime objects in order to easily do analysis over time
6. Turned tags into a list
    Tags looks to be made up of lists, but it is actually made up of objects. So I transformed them into actual lists that I could access.
7. Added a healthy column 
    This is a boolean column in which a true represents the tag 'healthy' being in the recipes' tags and false if not.
8. Added a healthy-2 column
    There were two different columns that contained the word'healthy', they were 'healthy' and 'healthy-2', so I did the same process for 'healthy-2'. This is a boolean column in which a true represents the tag 'healthy-2' being in the recipes' tags and false if not.

Our cleaned dataframe ended up with 234429 rows and 26 columns. Here are the first 5 rows of the cleaned dataset from a visual. This is just displaying the most essential columns for this project, as there are so many columns. 

insert df here

Univariate Analysis (delete this once i fix font)

The bar chart below illustrates the average ratings for different tag combinations, with a focus on those receiving ratings of 4 and above. Looking specifically at the tags, 'vegetarian', 'low-fat', 'holiday', 'healthy-2', 'dessert','healthy'. The highest-ranked combinations were 'vegetarian' and 'low-fat', as well as 'vegetarian,' 'low-fat,' and 'healthy-2'. These combinations suggest that recipes which are both vegetarian and low in fat are highly rated, and adding the "healthy-2" tag further enhances the appeal. This is an interesting discovery and makes one wonder if there is a correlation, or at least connection, between 'vegetarian' and 'low-fat', as well as 'vegetarian,' 'low-fat,' and 'healthy-2'.

<iframe
  src="assets/frequency_of_top_tags.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Bivariate Analysis (delete this once i fix font)
The scatter plot visualizes the relationship between Sodium and Protein content in recipes, categorized by the 'healthy' and 'healthy-2' tags. In the plot, recipes labeled as "healthy" (green) tend to cluster in regions with lower sodium levels and varying protein amounts, indicating that healthier recipes often prioritize low sodium content while maintaining a range of protein levels. The pattern suggests that lower sodium content is a consistent trait in recipes labeled as healthy, while protein varies more widely. Additionally there seems to be a greater amount of 'unhealthy' recipes in comparison to the 'healthy' recipes, as the red colors seems to outweight the green ones substantially so. 

insert scatter plot here

Interesting Aggregates (delete this once i fix font)

The pivot table provides a comparison of the average nutritional values, such as sodium, saturated fat, total fat, carbohydrates, sugar, calories, and protein, for recipes categorized as 'healthy' and 'unhealthy.' By summarizing this data, we can observe key nutritional differences between the two groups. Generally, healthy recipes are characterized by lower amounts of unhealthy nutrients, such as sodium, saturated fat, and total fat, while offering a more balanced nutritional profile. This table is an effective tool for identifying common nutritional traits in healthy versus unhealthy recipes, helping to uncover the overall qualities of healthier meal choices.

include pivot table here


# Assessment of Missingness
