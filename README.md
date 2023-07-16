# Project Title

Rise and-Fall of Programming Languages

## Project Description

This project analyzes the trends of Stack Overflow tags over time using data from the "by_tag_year.csv" dataset. It provides insights into the popularity and usage of different tags in the Stack Overflow community. The project utilizes various libraries such as `readr`, `dplyr`, and `ggplot2` for data manipulation and visualization.

## Table of Contents

- [Installation](#installation)
- [Usage](#usage)
- [Contributing](#contributing)
- [License](#license)

## Installation

To run this project, follow these steps:

1. Install the required libraries by executing the following code:
```R
# Load libraries
library(readr)
library(dplyr)
library(ggplot2)
```

2. Download the dataset "by_tag_year.csv" and place it in the "datasets" folder.

3. Run the code provided in the project to load the dataset and perform the analysis.

## Usage

1. Load the dataset by executing the following code:
```R
# Load dataset
by_tag_year <- read_csv("datasets/by_tag_year.csv")
```

2. View the dataset by executing:
```R
print(by_tag_year)
```

3. Add the fraction column to the dataset by executing:
```R
by_tag_year_fraction <- mutate(by_tag_year, fraction = number / year_total)
```

4. Print the updated dataset:
```R
print(by_tag_year_fraction)
```

5. Filter the dataset for the "R" tag and assign it to `r_over_time`:
```R
r_over_time <- by_tag_year_fraction %>%
    filter(tag == "r")
```

6. Print the filtered dataset:
```R
print(r_over_time)
```

7. Create a line plot showing the fraction of the "R" tag over time:
```R
ggplot(r_over_time, aes(x = year, y = fraction)) +
  geom_line() +
  labs(x = "Year", y = "Fraction") +
  ggtitle("Fraction over Time")
```

8. Further analysis can be performed by selecting specific tags and visualizing their trends over time. For example, to plot the tags "R", "dplyr", and "ggplot2" together, execute:
```R
selected_tags <- c("r", "dplyr", "ggplot2")

selected_tags_over_time <- by_tag_year_fraction %>%
    filter(tag %in% selected_tags)

ggplot(selected_tags_over_time, aes(x = year, y = fraction, color = tag)) +
  geom_line()
```

9. Additional analysis can be done by exploring the total number of questions for each tag and plotting the largest tags over time. Execute the following code:
```R
sorted_tags <- by_tag_year %>%
    group_by(tag) %>%
    summarize(tag_total = sum(number)) %>%
    arrange(desc(tag_total))

print(sorted_tags)

highest_tags <- head(sorted_tags$tag)

by_tag_subset <- by_tag_year_fraction %>%
    filter(tag %in% highest_tags)

ggplot(by_tag_subset, aes(x = year, y = fraction, color = tag)) +
  geom_line()
```

10. Finally, to explore specific tags of interest (e.g., "android", "ios", "windows-phone"), execute:
```R
my_tags <- c("android", "ios", "windows-phone")

by_tag_subset <- by_tag_year_fraction %>%
    filter(tag %in% my_tags)

ggplot(by_tag_subset, aes(x = year, y = fraction, color = tag)) +
  geom_line()
```

