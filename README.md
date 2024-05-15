# Final-332

## Contributors
Summer Chalmers & Hannah Maurer

## Introduction
In this project we chose people who have asthma and air pollution in the State of California. Asthma is split by lifetime and current, meaning people who were born with it and people who contracted it over time. The pollution was measure by the totals of each element in the air at a given location. All the data was recorde in between the years 2000 and 2020. 

## Cleaning Data

Removing any empty rows

```
asthma2012_present <- asthma2012_present[, !(names(asthma2012_present) == "X")]
asthma2012_present <- asthma2012_present[, !(names(asthma2012_present) == "X.1")]
asthma2012_present <- asthma2012_present[, !(names(asthma2012_present) == "X.2")]
asthma2012_present <- na.omit(asthma2012_present)
airquality <- airquality[, !(names(airquality) == "Date.Time")]
```

Merging all the data

```
df1 <- merge(airquality, asthma1995_2011, by = "Year")
df2 <- merge(airquality, asthma2012_present, by = "Year")
df <- bind_rows(df1,df2)
```

Clear non-used columns

```
df <- subset(df, select = -Ca.Dry)
df <- subset(df, select = -Ca.Wet)
df <- subset(df, select = -Cl.Dry)
df <- subset(df, select = -Cl.Wet)
df <- subset(df, select = -K.Dry)
df <- subset(df, select = -K.Wet)
df <- subset(df, select = -Mg.Dry)
df <- subset(df, select = -Mg.Wet)
df <- subset(df, select = -N.Dry)
df <- subset(df, select = -N.Dry.HNO3)
df <- subset(df, select = -N.Dry.NH3)
df <- subset(df, select = -N.Dry.NH4)
df <- subset(df, select = -N.Dry.NO3)  
df <- subset(df, select = -N.Dry.NOM)
df <- subset(df, select = -N.Dry.NOXI)
df <- subset(df, select = -N.Dry.NRED)
df <- subset(df, select = -N.Dry.TNO3)
df <- subset(df, select = -N.Wet)
df <- subset(df, select = -N.Wet.NH4)
df <- subset(df, select = -N.Wet.NO3)
df <- subset(df, select = -NA.Dry)
df <- subset(df, select = -NA.Wet)
df <- subset(df, select = -S.Dry)
df <- subset(df, select = -S.Dry.SO2)
df <- subset(df, select = -S.Dry.SO4)
df <- subset(df, select = -S.Wet)
df <- subset(df, select = -S.Wet.SO4)
```

Change Elements to Numeric Class

```
df$Ca.Total <- as.numeric(df$Ca.Total)
df$Cl.Total <- as.numeric(df$Cl.Total)
df$K.Total <- as.numeric(df$K.Total)
df$Mg.Total <- as.numeric(df$Mg.Total)
df$N.Total <- as.numeric(df$N.Total)
df$NA.Total <- as.numeric(df$NA.Total)
df$S.Total <- as.numeric(df$S.Total)
df$N.Total.NOXI <- as.numeric(df$N.Total.NOXI)
df$N.Total.NRED <- as.numeric(df$N.Total.NRED)
df$Precip <- as.numeric(df$Precip)
```

Creating a location column based off of Site ID

```
location_key <- data.frame(
  SITE_ID = c('LAV410', 'JOT403', 'YOS404', 'PIN414', 'SEK430', 'DEV412'),
              location = c('Shasta', 'San Bernardino', 'Mariposa', 'San Benito', 'Tulare','Inyo'))
df <- df %>%
  left_join(location_key, by = 'SITE_ID')
```
