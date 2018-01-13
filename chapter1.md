---
title       : Introduction
description : Modelling and Break-Even point
attachments :
  slides_link : https://s3.amazonaws.com/assets.datacamp.com/course/teach/slides_example.pdf

---
## Supply Chain Process

```yaml
type: MultipleChoiceExercise
lang: r
xp: 50
skills: 1
key: 94bd77445e
```

Have a look at the image that showed up in the viewer to the right. Which ones are associate with the core Management Science techniques?

`@instructions`
- Observation
- Problem Defintion
- Model construction
- Solution
- Implementation

`@hint`
All steps are necessary for solving a Supply Chain Analytics challenges, but two of them are more related to techniques.

`@pre_exercise_code`
```{r}
# The pre exercise code runs code to initialize the user's workspace.
# You can use it to load packages, initialize datasets and draw a plot in the viewer

movies <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/course/introduction_to_r/movies.csv")

library(ggplot2)

ggplot(movies, aes(x = runtime, y = rating, col = genre)) + geom_point()
```

`@sct`
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

msg_bad <- "That is not correct!"
msg_success <- "Exactly! There seems to be a very bad action movie in the dataset."
test_mc(correct = 2, feedback_msgs = c(msg_bad, msg_success, msg_bad, msg_bad))
```

---
## Simple Business Problem (warmup)

```yaml
type: NormalExercise
lang: r
xp: 100
skills: 1
key: 8bcbbfbaad
```

### Information
- Business produces Basmati rice bags
- Product costs £5 to produce
- Product sells for £20
- One bag requires 22 pounds of grain to make
- Company has 1100 pounds of rice grain per day

### Business problem
- Determine the number of units to produce to make the most profit, given the limited amount of rice grain available.

`@instructions`
- Define variables x= # units to produce (decision variable)
- Create a model 
  - z= £20x -£5x (objective function)
  - 22x= 1100 lb of rice grain (resource constraint)
- Formal Specification of Model
 $$ \max_x {20x-5x:22x=1100} $$
`@hint`
- Find $x$ by solving the resource constraint. This will give you the number of units to produce (known as solution)
- Use the solution to compute the profit $z$ (known as solution value)

`@pre_exercise_code`
```{r}
# You can also prepare your dataset in a specific way in the pre exercise code
load(url("https://s3.amazonaws.com/assets.datacamp.com/course/teach/movies.RData"))
movie_selection <- Movies[Movies$Genre %in% c("action", "animated", "comedy"), c("Genre", "Rating", "Run")]

# Clean up the environment
rm(Movies)
```

`@sample_code`
```{r}
# movie_selection is available in your workspace

# Check out the structure of movie_selection


# Select movies that have a rating of 5 or higher: good_movies


# Plot Run (i.e. run time) on the x axis, Rating on the y axis, and set the color using Genre

```

`@solution`
```{r}
# movie_selection is available in your workspace

# Check out the structure of movie_selection
str(movie_selection)

# Select movies that have a rating of 5 or higher: good_movies
good_movies <- movie_selection[movie_selection$Rating >= 5, ]

# Plot Run (i.e. run time) on the x axis, Rating on the y axis, and set the color using Genre
plot(good_movies$Run, good_movies$Rating, col = good_movies$Genre)
```

`@sct`
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

test_function("str", args = "object",
              not_called_msg = "You didn't call `str()`!",
              incorrect_msg = "You didn't call `str(object = ...)` with the correct argument, `object`.")

test_object("good_movies")

test_function("plot", args = "x")
test_function("plot", args = "y")
test_function("plot", args = "col")

test_error()

success_msg("Good work!")
```
