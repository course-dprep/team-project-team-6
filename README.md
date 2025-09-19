---
editor_options: 
  markdown: 
    wrap: 72
---

# Does Run Time Matter? How Genre Moderates the Impact of Run Time on Audience Ratings

*This project investigates the relationship between a film's run time
and its average audience rating. The main purpose is to determine if an
optimal run time for viewer rating exist and, to examine how genre
moderates this relationship. This research uses a large dataset from the
IMDb database to empirically test common industry assumptions, such as
the belief that audiences award higher ratings to shorter comedies and
longer dramas.*

## Motivation

In the highly competitive field of film making, every decision is
important, especially when significant financial investments are at
stake. Key creative decisions, such as a film's run time, can influence
on how it is received by audiences. This is further complicated by
genre, as audience expectations for a quirky comedy differ for a biopic.
Audience ratings serve as a direct measure of viewer satisfaction. By
analyzing the relationship between run time, genre, and these ratings,
we can move from industry intuition to data-backed insights. This
knowledge provides filmmakers and producers with a strategic tool for
better aligning their creative ideas with audience preferences,
potentially lowering financial risk and increasing a film's success.

Based on this, this study will focus on the following research question:

**To what extent does movie run time influence average audience ratings,
and how does this relationship differ across various film genres?**

## Data

-   What dataset(s) did you use? How was it obtained?
-   How many observations are there in the final dataset?
-   Include a table of variable description/operstionalisation.

## Method

-   What methods do you use to answer your research question?
-   Provide justification for why it is the most suitable.

## Preview of Findings

-   Describe the gist of your findings (save the details for the final
    paper!)
-   How are the findings/end product of the project deployed?
-   Explain the relevance of these findings/product.

## Repository Overview

\*\*Include a tree diagram that illustrates the repository structure\*

## Dependencies

*Explain any tools or packages that need to be installed to run this
workflow.*

## Running Instructions

library(dplyr)

library(tidyverse)

library(readr)

**Loading and exploring original datasets**

basics \<- read_tsv("title.basics.tsv")

ratings \<- read_tsv("title.ratings.tsv")

tail(basics)

tail(ratings)

head(basics)

head(ratings)

summary(basics)

summary(ratings)

**Merging datasets**

merged_unfiltered \<- left_join(ratings, basics, by = "tconst")

**Identifying NA's**

merged_unfiltered \<- merged_unfiltered %\>% mutate(across(everything(),
\~ ifelse(.x == "\\N", NA, .x)))

**Save merged file**

write_csv(merged_unfiltered, "Merged_IMDB_unfiltered.csv")

merged_unfiltered \<- read_csv("Merged_IMDB_unfiltered.csv")

**Filter dataset using intermediate dataframe 'filtered_df'**

filtered_df \<- merged_unfiltered %\>% filter(titleType == "movie")

filtered_df \<- filtered_df %\>% filter(numVotes \>= 250)

str(filtered_df$runtimeMinutes)
filtered_df$runtimeMinutes \<- as.numeric(filtered_df\$runtimeMinutes)

**This keeps the year it was published, could remove later**

filtered_df \<- filtered_df %\>% select(-originalTitle, -isAdult,
-endYear, -titleType)

**Make clean dataset**

movies_clean \<- subset(filtered_df, !is.na(runtimeMinutes) &
runtimeMinutes \> 30 & runtimeMinutes \< 250 & !is.na(genres))

write_csv(movies_clean, "movies_clean.csv")

## About

This project is set up as part of the Master's course [Data Preparation
& Workflow Management](https://dprep.hannesdatta.com/) at the
[Department of
Marketing](https://www.tilburguniversity.edu/about/schools/economics-and-management/organization/departments/marketing),
[Tilburg University](https://www.tilburguniversity.edu/), the
Netherlands.

The project is implemented by team \< x \> members: \< insert member
details\>
