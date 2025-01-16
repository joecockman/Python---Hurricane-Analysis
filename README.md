# Python---Hurricane-Analysis

Project Goals
The following project work is part of the Codecademy 'Business Intelligence Data Analyst' Career Path. For this project, open-ended questions were set around provided hurricane data. The goal was to use everything I had learned so far about Python to create functions that would answer the given question.

# Question 1.
Hurricanes, also known as cyclones or typhoons, are one of the most powerful forces of nature on Earth. Due to climate change caused by human activity, the number and intensity of hurricanes has risen, calling for better preparation by the many communities that are devastated by them. As a concerned environmentalist, you want to look at data about the most powerful hurricanes that have occured.

Begin by looking at the damages list. The list contains strings representing the total cost in USD($) caused by 34 category 5 hurricanes (wind speeds  157 mph (252 km/h)) in the Atlantic region. For some of the hurricanes, damage data was not recorded ("Damages not recorded"), while the rest are written in the format "Prefix-B/M", where B stands for billions (1000000000) and M stands for millions (1000000).

Write a function that returns a new list of updated damages where the recorded data is converted to float values and the missing data is retained as "Damages not recorded".

```
damages = ['Damages not recorded', '100M', 'Damages not recorded', '40M',
          '27.9M', '5M', 'Damages not recorded', '306M', '2M', '65.8M',
          '326M', '60.3M', '208M', '1.42B', '25.4M', 'Damages not recorded',
          '1.54B', '1.24B', '7.1B', '10B', '26.5B', '6.2B', '5.37B', '23.3B',
          '1.01B', '125B', '12B', '29.4B', '1.76B', '720M', '15.1B', '64.8B',
          '91.6B', '25.1B']

# 1
# Update Recorded Damages
conversion = {"M": 1000000,
             "B": 1000000000}

# test function by updating damages
```

Above is the list,'damages', and the conversions, showing that M = million (1000000) and B = billion (1000000000). To achieve the desired result I need to remove the "B's" and the "M's" from the numbers, and convert them from strings to floats. Cases of 'Damages not recorded' should also be added to the new list.


```
def hurricanomatic():
    updated_damages = []
    for value in damages:
        if value == 'Damages not recorded':
            updated_damages.append('Damages not recorded')
        elif 'M' in value:
            value = value.strip('M')
            updated_damages.append(float(value) * 1000000)
        elif 'B' in value:
            value = value.strip('B')
            updated_damages.append(float(value) * 1000000000)
    return updated_damages

print(hurricanomatic())
```

Above is the function I created, hurricanomatic. It initialises an empty list called 'updated_damages' which I will append all of my updated data into.

I then created a for loop to loop through each 'value' in the 'damages' list. 
 - If the value is 'Damages not recorded' then this will be appended to the new list.
 - If the value contains 'M', I use strip to remove it before converting the string to a float and then multiplying it by 1000000. I then append it to the new list.
 - If the value contains 'B', I  use strip to remove it before converting the string to a float and then multiplying it by 1000000000. I then append to the new list.

Finally, I return the newly populated 'updated_damages' list and then print the function. The output is a list of float values with the missing values retained as  'Damages not recorded'.

```
['Damages not recorded', 100000000.0, 'Damages not recorded', 40000000.0, 27900000.0,
5000000.0, 'Damages not recorded', 306000000.0, 2000000.0, 65800000.0, 326000000.0,
60300000.0, 208000000.0, 1420000000.0, 25400000.0, 'Damages not recorded', 1540000000.0,
1240000000.0, 7100000000.0, 10000000000.0, 26500000000.0, 6200000000.0, 5370000000.0,
23300000000.0, 1010000000.0, 125000000000.0, 12000000000.0, 29400000000.0, 1760000000.0,
 720000000.0, 15100000000.0, 64800000000.0, 91600000000.0, 25100000000.0]
```

#  Question 2.

Additional data collected on the 34 strongest Atlantic hurricanes are provided in a series of lists. The data includes:

names: names of the hurricanes
months: months in which the hurricanes occurred
years: years in which the hurricanes occurred
max_sustained_winds: maximum sustained winds (miles per hour) of the hurricanes
areas_affected: list of different areas affected by each of the hurricanes
deaths: total number of deaths caused by each of the hurricanes
The data is organized such that the data at each index, from 0 to 33, corresponds to the same hurricane.

For example, names[0] yields the "Cuba I" hurricane, which occurred in months[0] (October) years[0] (1924).

Write a function that constructs a dictionary made out of the lists, where the keys of the dictionary are the names of the hurricanes, and the values are dictionaries themselves containing a key for each piece of data (Name, Month, Year, Max Sustained Wind, Areas Affected, Damage, Death) about the hurricane.

```
# names of hurricanes
names = ['Cuba I', 'San Felipe II Okeechobee', 'Bahamas', 'Cuba II', 'CubaBrownsville', 'Tampico', 'Labor Day', 'New England', 'Carol', 'Janet', 'Carla', 'Hattie', 'Beulah', 'Camille', 'Edith', 'Anita', 'David', 'Allen', 'Gilbert', 'Hugo', 'Andrew', 'Mitch', 'Isabel', 'Ivan', 'Emily', 'Katrina', 'Rita', 'Wilma', 'Dean', 'Felix', 'Matthew', 'Irma', 'Maria', 'Michael']

# months of hurricanes
months = ['October', 'September', 'September', 'November', 'August', 'September', 'September', 'September', 'September', 'September', 'September', 'October', 'September', 'August', 'September', 'September', 'August', 'August', 'September', 'September', 'August', 'October', 'September', 'September', 'July', 'August', 'September', 'October', 'August', 'September', 'October', 'September', 'September', 'October']

# years of hurricanes
years = [1924, 1928, 1932, 1932, 1933, 1933, 1935, 1938, 1953, 1955, 1961, 1961, 1967, 1969, 1971, 1977, 1979, 1980, 1988, 1989, 1992, 1998, 2003, 2004, 2005, 2005, 2005, 2005, 2007, 2007, 2016, 2017, 2017, 2018]

# maximum sustained winds (mph) of hurricanes
max_sustained_winds = [165, 160, 160, 175, 160, 160, 185, 160, 160, 175, 175, 160, 160, 175, 160, 175, 175, 190, 185, 160, 175, 180, 165, 165, 160, 175, 180, 185, 175, 175, 165, 180, 175, 160]

# areas affected by each hurricane
areas_affected = [['Central America', 'Mexico', 'Cuba', 'Florida', 'The Bahamas'], ['Lesser Antilles', 'The Bahamas', 'United States East Coast', 'Atlantic Canada'], ['The Bahamas', 'Northeastern United States'], ['Lesser Antilles', 'Jamaica', 'Cayman Islands', 'Cuba', 'The Bahamas', 'Bermuda'], ['The Bahamas', 'Cuba', 'Florida', 'Texas', 'Tamaulipas'], ['Jamaica', 'Yucatn Peninsula'], ['The Bahamas', 'Florida', 'Georgia', 'The Carolinas', 'Virginia'], ['Southeastern United States', 'Northeastern United States', 'Southwestern Quebec'], ['Bermuda', 'New England', 'Atlantic Canada'], ['Lesser Antilles', 'Central America'], ['Texas', 'Louisiana', 'Midwestern United States'], ['Central America'], ['The Caribbean', 'Mexico', 'Texas'], ['Cuba', 'United States Gulf Coast'], ['The Caribbean', 'Central America', 'Mexico', 'United States Gulf Coast'], ['Mexico'], ['The Caribbean', 'United States East coast'], ['The Caribbean', 'Yucatn Peninsula', 'Mexico', 'South Texas'], ['Jamaica', 'Venezuela', 'Central America', 'Hispaniola', 'Mexico'], ['The Caribbean', 'United States East Coast'], ['The Bahamas', 'Florida', 'United States Gulf Coast'], ['Central America', 'Yucatn Peninsula', 'South Florida'], ['Greater Antilles', 'Bahamas', 'Eastern United States', 'Ontario'], ['The Caribbean', 'Venezuela', 'United States Gulf Coast'], ['Windward Islands', 'Jamaica', 'Mexico', 'Texas'], ['Bahamas', 'United States Gulf Coast'], ['Cuba', 'United States Gulf Coast'], ['Greater Antilles', 'Central America', 'Florida'], ['The Caribbean', 'Central America'], ['Nicaragua', 'Honduras'], ['Antilles', 'Venezuela', 'Colombia', 'United States East Coast', 'Atlantic Canada'], ['Cape Verde', 'The Caribbean', 'British Virgin Islands', 'U.S. Virgin Islands', 'Cuba', 'Florida'], ['Lesser Antilles', 'Virgin Islands', 'Puerto Rico', 'Dominican Republic', 'Turks and Caicos Islands'], ['Central America', 'United States Gulf Coast (especially Florida Panhandle)']]

# damages (USD($)) of hurricanes
damages = ['Damages not recorded', '100M', 'Damages not recorded', '40M', '27.9M', '5M', 'Damages not recorded', '306M', '2M', '65.8M', '326M', '60.3M', '208M', '1.42B', '25.4M', 'Damages not recorded', '1.54B', '1.24B', '7.1B', '10B', '26.5B', '6.2B', '5.37B', '23.3B', '1.01B', '125B', '12B', '29.4B', '1.76B', '720M', '15.1B', '64.8B', '91.6B', '25.1B']

# deaths for each hurricane
deaths = [90,4000,16,3103,179,184,408,682,5,1023,43,319,688,259,37,11,2068,269,318,107,65,19325,51,124,17,1836,125,87,45,133,603,138,3057,74]
```

```
def hurricane_dictionary_creator():
    hurricanes = {}
    number_of_hurricanes = len(names)
    for i in range(number_of_hurricanes):
        hurricanes[names[i]] = {"name": names[i],
                                "month": months[i],
                                "year": years[i],
                                "max sustained wind": max_sustained_winds[i],
                                "areas affected": areas_affected[i],
                                "damages": damages[i],
                                "deaths": deaths[i]}
    return hurricanes

dumba = (hurricane_dictionary_creator())
print(dumba)
```
