- 👋 Hi, I’m @BillChao23
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
BillChao23/BillChao23 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
### week 4 assignment

# this week we install

install.packages("dplyr")

 #download libary("dplyr")  need to everytime using

library("dplyr")

  # example 2 download data  and save

  ### download, the data, 
## file name then use <- read.csv("data/file name.csv")to import it into R

shrub_dimensions_labeled <- read.csv("data/shrub-dimensions-labeled.csv")  

#name(file name) str= structure(file name) head(file name) run

names(shrub_dimensions_labeled)  
str(shrub_dimensions_labeled)
head(shrub_dimensions_labeled)

#select(file name, length,height,width)

select(shrub_dimensions_labeled, length) 
  
select(shrub_dimensions_labeled)  

#ex2 
#name it what ever shrub_vol_exp then <- read.csv("data/tab key file name")
## file name then use <- read.csv("data/file name.csv")to import it into R

shrub_vol_exp <- read.csv("data/shrub-volume-experiment.csv")
names(shrub_vol_exp) 
str(shrub_vol_exp)
head(shrub_vol_exp)
select(shrub_vol_exp, length)
select(shrub_vol_exp, site,experiment)

#Filter the data for all of the plants with heights greater than 5 and print out the result.
filter(shrub_vol_exp, height < 5)

#ex2 question 7
#mutate Create a new data frame (shrub_vol_exp)
shrub_data_w_vols <- mutate(shrub_vol_exp, volume = length*width*height)
# next step includes all of the original data and a new column containing the volumes
head(shrub_data_w_vols)

#playing around line 38-43
shrub_data_w_vols$volume

names(shrub_data_w_vols)
str(shrub_data_w_vols)
head(shrub_data_w_vols)

#ex3 aggregation by group

shrub_vol_exp <- read.csv("data/shrub-volume-experiment.csv")

library("dplyr")

#by_site <- group_by(shrub_data_w_vols, site)

#avg_height <- summarize(by_site, avg_height = mean(height))

#aggregate()
#summarize(shrub_data_w_vols, avg_height = mean(height))

#max(summarize(by_site, (height))
    
    
### excersice 5
#make sure variable name are assigned correctly
## missing pipe %>% height

shrub_data <-read.csv("data/shrub-volume-experiment.csv")
shrub_data %>%
  mutate(volume = length * width * height) %>%
  group_by(site) %>%
  summarize(mean_volume = max(volume))
shrub_data %>%
  mutate(volume = length * width * height)%>% 
  group_by(experiment) %>%
  summarize(mean_volume = mean(volume))
  
  
  #### Week 5 
  
  size_mr_data <- data.frame(
  body_mass = c(32000, 37800, 347000, 4200, 196500, 100000, 4290, 
                32000, 65000, 69125, 9600, 133300, 150000, 407000, 115000, 
                67000,325000, 21500, 58588, 65320, 85000, 135000, 20500, 1613,
                1618),
  metabolic_rate = c(49.984, 51.981, 306.770, 10.075, 230.073, 
                     148.949, 11.966, 46.414, 123.287, 106.663, 20.619, 180.150, 
                     200.830, 224.779, 148.940, 112.430, 286.847, 46.347, 142.863, 
                     106.670, 119.660, 104.150, 33.165, 4.900, 4.865))

Mammal_life <-read.csv("https://esapubs.org/archive/ecol/E084/093/Mammal_lifehistories_v2.txt",sep = "\t", nrows = 1440, na.strings = c("-999", "-999.00"))

 ### install packages ggplot

install.packages("ggplot")
library("ggplot2")

## exercise 1 two plots with appropriate axis labels

ggplot(data = size_mr_data, mapping = aes(x = body_mass, y = metabolic_rate)) +
  geom_point()

ggplot(size_mr_data, aes(x = body_mass, y = metabolic_rate)) +
  geom_point()

##  two plots with appropriate axis labels
## keeps the numbers on the original scale
## and the point size set to 5.

ggplot(size_mr_data, aes(x = body_mass, y = metabolic_rate)) +
  geom_point(size = 5, color = "blue", alpha = .5)

## wrong argument Mammal <- read.csv(data/"mammal_lifehistories_V2.csv")
### exercise 2

Mammal_life <-read.csv("https://esapubs.org/archive/ecol/E084/093/Mammal_lifehistories_v2.txt",sep = "\t", nrows = 1440, na.strings = c("-999", "-999.00"))

ggplot(data = Mammal_lifehistories_v2, mapping = aes(x = mass.g., y = newborn.g.)) +
  geom_point()

#### saving plot as adult_mass rename We can create a new variable by assigning a value to it using <-

adult_mass <- ggplot(data = Mammal_lifehistories_v2, mapping = aes(x = mass.g., y = newborn.g.)) +
  geom_point()

## print axes with clearer labels than the column names

print(adult_mass + labs(x = "adult_mass"))
print(adult_mass + labs(x = "adult_mass", y = "newborn_mass"))

## log transformation to be more linear

ggplot(Mammal_lifehistories_v2, aes(x = mass.g., y = newborn.g.)) +
  geom_point(size = 3, color = "blue", alpha = 0.5) +
  scale_y_log10() +
  scale_x_log10()


ggplot(Mammal_lifehistories_v2, aes(x = mass.g., y = newborn.g.)) +
  geom_point(size = 3, color = "red", alpha = 0.5) +
  labs(x = "mass.g. [g]", y = "newborn.g. [g]",
       title = "mammal_lifehistories_V2")

## facet

ggplot(Mammal_lifehistories_v2, aes(x = mass.g., y = newborn.g.)) +
  geom_point(size = 5, alpha = 0.3) + scale_x_log10()+scale_y_log10()+
  facet_wrap(~order)

#exercise 3

ggplot(Mammal_lifehistories_v2, aes(x = mass.g., y = newborn.g.)) +
  geom_point() +
  geom_smooth(method = "lm")
 


ggplot(data = avian_ssd_jan07, mapping = aes(x = F_mass, y = M_mass)) +
  geom_point()

ggplot(avian_ssd_jan07, aes(x = F_mass, y = M_mass)) +
  geom_point(size = 3, color = "blue", alpha = 0.5) +
  scale_y_log10() +
  scale_x_log10()

ggplot(avian_ssd_jan07, aes(x = F_mass)) +
  geom_histogram()

ggplot(avian_ssd_jan07, aes(x = F_mass, y = M_mass)) +
  geom_point(size = 3, color = "blue", alpha = 0.5)

## saving plot as F_histogram rename 

F_histogram <- ggplot(avian_ssd_jan07, aes(x = F_mass, y = M_mass)) +
  geom_point(size = 3, color = "blue", alpha = 0.5)

print(F_histogram + labs(x = "Female Mass(g)"))

F_histogram <- ggplot(avian_ssd_jan07, aes(x = F_mass, y = M_mass)) +
  geom_point(size = 3, color = "blue", alpha = 0.5)

print(F_histogram + labs(y = "Male Mass(g)", x = "Female Mass (g)"))
  
library(dplyr)


## data to get the subset of your data with more than 25 species 

large_n_families <- avian_ssd_jan07 %>%
  filter(!is.na(M_mass), !is.na(F_mass)) %>%
  group_by(Family) %>%
  summarize(num_species = n()) %>%
  filter(num_species >=25)

combine_data = inner_join(large_n_families, avian_ssd_jan07, by="Family")

ggplot(data = combine_data, mapping = aes(x = F_mass, y = M_mass)) +
  geom_point()

ggplot(data = combine_data, mapping = aes(x = F_mass, y = M_mass)) +
  geom_point()

ggplot(combine_data, aes(x = F_mass, y = M_mass)) +
  geom_point(size = 3, color = "blue", alpha = 0.5) +
  scale_y_log10() +
  scale_x_log10()

ggplot(combine_data, aes(x = F_mass)) +
  geom_histogram()

ggplot(combine_data, aes(x = F_mass, y = M_mass)) +
  geom_point(size = 3, color = "blue", alpha = 0.5)

## saving plot as F_histogram rename We can create a new variable by assigning a value to it using <- 

F_histogram <- ggplot(combine_data, aes(x = F_mass, y = M_mass)) +
  geom_point(size = 3, color = "blue", alpha = 0.5)

print(F_histogram + labs(x = "Female Mass(g)"))

F_histogram <- ggplot(combine_data, aes(x = F_mass, y = M_mass)) +
  geom_point(size = 3, color = "blue", alpha = 0.5)

print(F_histogram + labs(y = "Male Mass(g)", x = "Female Mass (g)"))

