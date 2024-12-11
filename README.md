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
  src="assets/average_ratings_by_tag_combinations.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>



Below is an interesting pie chart visualizing the top 10 used tags and their frequencies in comparison to one another.

<iframe
  src="assets/frequency_of_top_tags.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Bivariate Analysis (delete this once i fix font)
The scatter plot visualizes the relationship between Sodium and Protein content in recipes, categorized by the 'healthy' and 'healthy-2' tags. In the plot, recipes labeled as "healthy" (green) tend to cluster in regions with lower sodium levels and varying protein amounts, indicating that healthier recipes often prioritize low sodium content while maintaining a range of protein levels. The pattern suggests that lower sodium content is a consistent trait in recipes labeled as healthy, while protein varies more widely. Additionally there seems to be a greater amount of 'unhealthy' recipes in comparison to the 'healthy' recipes, as the red colors seems to outweight the green ones substantially so. 


<iframe
  src="assets/sodium_vs_protein_healthy.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Interesting Aggregates (delete this once i fix font)

The pivot table provides a comparison of the average nutritional values, such as sodium, saturated fat, total fat, carbohydrates, sugar, calories, and protein, for recipes categorized as 'healthy' and 'unhealthy.' By summarizing this data, we can observe key nutritional differences between the two groups. Generally, healthy recipes are characterized by lower amounts of unhealthy nutrients, such as sodium, saturated fat, and total fat, while offering a more balanced nutritional profile. This table is an effective tool for identifying common nutritional traits in healthy versus unhealthy recipes, helping to uncover the overall qualities of healthier meal choices.

| name                                 |   id   | minutes | contributor_id | submitted           | tags                           | nutrition            | n_steps | steps                           | description                    | ingredients                     | n_ingredients |
|:-------------------------------------|:-------|:--------|:---------------|:--------------------|:-------------------------------|:---------------------|:--------|:--------------------------------|:-------------------------------|:-------------------------------|:--------------|
| 1 brownies in the world...           | 333281 |      40 |          985201 | 2008-10-27 00:00:00 | ['60-minutes-or-less...']      | [138.4, 10.0, ...]   |      10 | ['heat the oven to 350f...']    | these are the most...          | ['bittersweet chocolate...']    |              9 |
| 1 in canada chocolate...             | 453467 |      45 |         1848091 | 2011-04-11 00:00:00 | ['60-minutes-or-less...']      | [595.1, 46.0, ...]   |      12 | ['pre-heat oven the 350...']    | this is the recipe...          | ['white sugar', 'brown...']     |             11 |
| 412 broccoli casserole               | 306168 |      40 |           50969 | 2008-05-30 00:00:00 | ['60-minutes-or-less...']      | [194.8, 20.0, ...]   |       6 | ['preheat oven to 350...']      | since there are already...     | ['frozen broccoli cuts...']     |              9 |
|                                      |        |         |                |                     |                                |                      |         |                                 |                                |                                |                |
|                                      |        |         |                |                     |                                |                      |         |                                 |                                |                                |                |
| 412 broccoli casserole               | 306168 |      40 |           50969 | 2008-05-30 00:00:00 | ['60-minutes-or-less...']      | [194.8, 20.0, ...]   |       6 | ['preheat oven to 350...']      | since there are already...     | ['frozen broccoli cuts...']     |              9 |
| 412 broccoli casserole               | 306168 |      40 |           50969 | 2008-05-30 00:00:00 | ['60-minutes-or-less...']      | [194.8, 20.0, ...]   |       6 | ['preheat oven to 350...']      | since there are already...     | ['frozen broccoli cuts...']     |              9 |



# Assessment of Missingness

When looking at missingness, the columns with the main missing are 'rating', 'description,' and 'review.'

NMAR Analysis (delete after fixing font)

I think the column 'review' in the dataset appears to be Not Missing At Random (NMAR), as its absence is likely tied to the behavior of individuals choosing not to leave a review. This pattern makes sense because people might not leave reviews for various reasons, such as lack of interest, forgetting, or having neutral feelings about the recipe. The missingness is therefore dependent on an underlying, unobserved factor related to the individual's decision-making process, making it NMAR rather than completely random.

Missing Dependency (delete after ifxing font)

After going through rating', 'description,' and 'review,' I thought about what was missing and why. I didn't believe that the descriptions being missing seemed to have a pattern and wondered if missing ratings did. So I investigated whether the missiness in the 'rating' column was dependent on the 'calories' columns because I could see how the negative connotation that society has with calories could relate to a lack of a review. 

Null Hypothesis: The missigness of ratings are MCAR

Alternative Hypothesis: The missingless of ratings is dependent on 'Calories'. 

Test Statistic: The difference in means of missing and non-missing ratings, with the column that is being shuffled changing. 

Significance Level: 0.05

The observed statistic was 0.0 (and in a second test, 0.00014), which is less than the significance level and so I rejected the null. 

The results strongly indicate that the missingness of rating is systematically related to the calories column. Specifically, recipes with missing ratings tend to have significantly higher calorie counts compared to recipes with ratings. This implies that the likelihood of a rating being missing depends on the calorie content of the recipe. One plausible explanation is that individuals might consciously avoid rating high-calorie recipes, possibly due to feelings of guilt, dissatisfaction, or a perception that these recipes do not align with their dietary preferences or goals. 


<iframe
  src="assets/permutation_test_distribution.htm"
  width="800"
  height="600"
  frameborder="0"
></iframe>

In summary, the empirical distribution visualizes the range of differences in means generated by shuffling the data under the assumption that missingness is random. The observed difference being far from the center of the distribution suggests that the missingness is dependent on calorie content and is likely not random (NMAR).

# Hypothesis Testing

I was curious to see if recipes with tags 'healthy' or 'healthy-2' were rated differently than tags without them to help me further understand what could help me predict 'healthy.' To understand this query, I ran a hypothesis test. 

Null Hypothesis: There is no difference in the ratings of recipes with the tags 'healthy' or 'healthy-2' compared to those without these tags.

Alternative Hypothesis: Recipes with the tags 'healthy' or 'healthy-2' receive different ratings compared to those without these tags.

Test Statistic: he difference in the average ratings (means) between the two groups—recipes with the 'healthy' or 'healthy-2' tags and those without these tags

Significance Level: 0.05

The p-values for the "healthy" and "healthy-2" tags provide interesting insights into how these labels influence recipe ratings. The p-value for the "healthy" tag is 0.0, which is highly significant and leads us to reject the null hypothesis, indicating that recipes labeled as "healthy" are rated differently from those without the tag. This suggests that the "healthy" label does influence ratings, possibly due to consumer biases or associations with health-conscious behaviors. In contrast, the p-value for the "healthy-2" tag is 0.6281, which is not significant, meaning we fail to reject the null hypothesis for this tag. This suggests that the "healthy-2" label does not have a statistically significant effect on recipe ratings. The difference between the two results suggests that not all health-related tags are perceived equally, with the "healthy" label having a stronger impact on ratings than "healthy-2". This could reflect differing consumer perceptions of these tags, with the "healthy" label possibly carrying more weight in terms of expectations around nutrition and quality. Further research could explore why the "healthy" tag has a significant impact while the "healthy-2" tag does not, potentially investigating the characteristics of recipes with these labels or surveying users to understand their perceptions.

# Framing a Prediction Problem

The task at hand is a binary classification problem where the goal is to predict whether a recipe is "healthy" (1) or "unhealthy" (0). The response variable is the healthy variable, which indicates whether a recipe is considered healthy based on various features such as ingredients, preparation steps, and nutritional information. This variable was chosen because the problem is focused on classifying recipes into two categories: healthy vs. unhealthy, which is a straightforward binary decision. To evaluate the model, precision is chosen as the evaluation metric because it is particularly important in this context to minimize false positives—i.e., incorrectly classifying an unhealthy recipe as healthy. This is a more suitable metric than accuracy because the dataset may be imbalanced (more unhealthy recipes than healthy ones), and precision provides a better understanding of how well the model performs for the positive class (healthy recipes).

The model will only use information available at the time of prediction. This includes features like ingredients, preparation steps, cooking times, and nutritional content, but does not use information such as the recipe's rating or any future data points (e.g., user reviews or ratings). This ensures that the model’s predictions are realistic and based on what is available at the time of predicting whether a recipe is healthy.

Additionally, fairness is assessed by comparing precision between low-rated and high-rated recipes. A permutation test is conducted to test whether there is a significant difference in precision for these two groups. The null hypothesis assumes that the model is fair and has similar precision for both groups, while the alternative hypothesis suggests that there is a significant difference in precision. A p-value less than 0.05 would indicate that the model's performance is unfair and that the precision varies significantly between these groups.

# Baseline Model

For my baseline model, I developed a Random Forest Classifier to predict whether a recipe is healthy based on its attributes. I split the data into training and test and the model used the features tags and healthy. I manually looked through all the unique tags and then picked out the ones I thought correlate the most to what most perceive as "healthy". I created a temporary dataframe that had these specific tags, such as 'low-calorie', as columns and each row consisted of a True if the recipe contained that tag and a False if not. 

I one hot encoded the boolean values in these "healthy" tags and then trained my model. These features are all nominal.

The model achieved an impressive accuracy of 93.7%, indicating that it correctly classified most recipes in the dataset. However, a closer inspection of the confusion matrix reveals a significant issue: the model predicted no healthy recipes (class 1) correctly. Specifically, the confusion matrix shows that for the 4,939 healthy recipes, the model classified all of them as non-healthy (class 0), leading to zero true positives for the healthy class. As a result, the classification report highlights this problem, with the precision and recall for the healthy class (1) both being 0.0, meaning the model failed to identify any healthy recipes. On the other hand, the precision for the non-healthy class (0) is 94%, and the recall is 100%, which suggests that the model is highly biased towards predicting non-healthy recipes. The F1-score for the non-healthy class is 0.97, which is quite strong, but the F1-score for the healthy class is 0.0, highlighting the model's poor performance on that class.

The macro average metrics (precision, recall, and F1-score) are all low (around 0.5), reflecting the imbalance in the model's ability to classify both classes. While the overall accuracy appears high, the model suffers from severe class imbalance, as it predominantly predicts the majority class (non-healthy) and ignores the minority class (healthy). I think the model is okay, but could definitely be way better as even though it has great accuracy, it is lacking in the precision, recall, and F1-score. 

# Final Model

For my final model, I used those same "healthy" tags and one hot encoded them as before.

Yet I also used 'carbohydrates', 'protein', 'saturated_fat', 'sugar', 'total_fat'.

For these features, 'carbohydrates', 'protein', 'saturated_fat', 'sugar', 'total_fat', I used STD Scalar to incorporate these numerical feautures in my dataset. I chose to use these values of nutrition because I knew that they have a relationship with health. Health is majorly about nutrition and incorportating these numerical nutrition values was essential. These features are critical in determining the healthiness of a recipe because they directly correlate with factors like energy content, metabolic impact, and disease prevention. I chose to use these nutritional features because they are directly tied to how health-conscious individuals might evaluate a recipe. These variables are commonly used in nutrition science and public health guidelines to categorize food as either healthy or unhealthy. By incorporating them into my model, I aim to predict whether a recipe is healthy based on its nutritional profile, which is essential for anyone seeking to improve their diet. 

In addition to using the numerical features like 'sugar', 'sodium', and 'carbohydrates', I applied Binarizers to these features to help convert them into binary values, which can simplify the model’s interpretation and potentially enhance its performance. To determine the appropriate thresholds for binarization, I used the pivot table that I created earlier to analyze the mean values of sugar, sodium, and carbohydrates for both healthy and non-healthy recipes. This allowed me to see distinct patterns between the two groups, which helped me set the thresholds. For example, I found that the average carbohydrate content for healthy recipes was greater than 15 grams. Therefore, I set the threshold for the carbohydrate Binarizer at 15 grams. Recipes with carbohydrates greater than 15 grams would be classified as 1 (healthy), while recipes with carbohydrates less than or equal to 15 grams would be classified as 0 (non-healthy).

Similarly, I applied this technique to sugar and sodium levels, selecting thresholds based on the average values I observed in the pivot table. The purpose of binarizing these nutritional features was to transform continuous variables into categorical ones, making them easier for the model to process. This also helped highlight the relationship between certain levels of these nutrients and whether a recipe would be classified as healthy or not.

I chose this method because binarizing features based on meaningful thresholds allows the model to focus on whether a specific nutrient level is above or below a critical point, which can provide a clearer understanding of what makes a recipe healthy or unhealthy. Additionally, this approach can help improve the model’s predictive power by making certain patterns more explicit, especially when dealing with highly variable nutritional data. By setting these thresholds based on observed data, I ensured that the model had clear, data-driven criteria for classifying recipes based on their nutritional content.

For my final model, I chose a Random Forest Classifier. The model was optimized through Grid Search with 5-fold cross-validation to identify the best hyperparameters: n_estimators (100), min_samples_split (2), min_samples_leaf (1), max_depth (30), and class_weight ('balanced'). These hyperparameters helped improve accuracy and address class imbalance. The final model achieved an accuracy of 0.95, with a recall of 0.88 for healthy recipes, indicating a strong ability to correctly identify healthy items. The precision for healthy recipes was 0.82, and the F1-score was 0.85. Compared to the baseline model, which would likely have relied on predicting the majority class (unhealthy recipes) and thus performed poorly in detecting healthy recipes, the final model shows significant improvements in both precision and recall. The use of a balanced class weight further addressed the class imbalance, allowing the model to treat both classes fairly and resulting in a more reliable prediction of healthy and non-healthy recipes. Overall, this model outperformed the baseline by offering a better balance between precision and recall, particularly for the healthy recipe classification, and provides more accurate predictions across both classes.

# Fairness Analysis





