# Yandex.Music

The comparison of Moscow and St. Petersburg is surrounded by myths. For example:
 * Moscow is a metropolis subject to the rigid rhythm of the working week;
 * St. Petersburg is a cultural capital, with its own tastes.

Using Yandex Music data, we will compare the behavior of users in the two capitals.

## Research Purpose - Test three hypotheses:
1. User activity depends on the day of the week. Moreover, in Moscow and St. Petersburg this manifests itself in different ways.
2. On Monday morning, certain genres prevail in Moscow, while others prevail in St. Petersburg. Similarly, Friday evenings are dominated by different genres, depending on the city. 
3. Moscow and St. Petersburg prefer different genres of music. In Moscow, they listen to pop music more often, in St. Petersburg - Russian rap.

## Research Process

We will use data on user behavior from the `yandex_music_project.csv` file. Nothing is known about the quality of the data. Therefore, before testing hypotheses, a review of the data is required. 

We will check the data for errors and assess their impact on the study. Then, during the pre-processing phase, we will look for opportunities to correct the most critical data errors.
 
Thus, the study will take place in three stages:
  1. Data review.
  2. Data preprocessing.
  3. Hypothesis testing.

## Results of the study

We tested three hypotheses and found:

1. The day of the week has a different effect on the activity of users in Moscow and St. Petersburg.

The first hypothesis was fully confirmed.

2. Musical preferences do not change much during the week - be it Moscow or St. Petersburg. Small differences are noticeable at the beginning of the week, on Mondays:
* in Moscow users listen to the music of the “world” genre,
* in St. Petersburg - jazz and classical music.

Thus, the second hypothesis was only partly confirmed. This result could have been different were it not for gaps in the data.

3. The tastes of users of Moscow and St. Petersburg have more in common than differences. Contrary to expectations, genre preferences in St. Petersburg resemble those in Moscow.

The third hypothesis was not confirmed. If there are differences in preferences, they are invisible to the bulk of users.

**In practice, studies contain tests of statistical hypotheses.**
From the data of one service, it is not always possible to draw a conclusion about all the inhabitants of the city.
Tests of statistical hypotheses will show how reliable they are, based on the available data.
