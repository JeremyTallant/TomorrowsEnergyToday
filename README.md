# Tomorrow's Energy Today

![1663640](https://user-images.githubusercontent.com/112406455/201741488-1522622e-4e36-40f4-b23e-db2096061e7e.jpg)


## Description
The aim of our project is to uncover patterns in solar usage in the United States. We'll examine relationships between the number of residential solar sytems in each state and different economic and socioeconmic variables. In addition, we will examine other relationships that can be derived from the data.

## API Keys
To run the python scripts in this project, first you will need to obtain two API keys. The first API key is for the US Census API which is used in the mainscript.ipynb. Here is the link: "https://api.census.gov/data/key_signup.html". The second API key is for the Google Maps API which is used in both edscript.ipynb and ericsript.ipynb. Here is the link: "https://developers.google.com/maps/documentation/geocoding/start". Once you have obtained both keys you will need to place them in the apikeys.py file where it says, "YOUR KEY HERE" in the main repository.


## Table of Contents
1. Questions
2. Overview of Data
3. Data Retrieval and Cleansing
4. Analysis
5. Where to Next

## Questions
* Is there any relation to education and solar usage?
* Is household income related to the usage of solar energy?
* What states are using solar the most?
* Is there a connection between population density and solar usage? 

## Overview of Data
In this project we used two main datasets:
* Deep Solar (last updated 2016)
* Cenus API (last updated 2020)

The Deep Solar data is a csv we found on Kaggle with 72,538 rows organized by zip codes of different areas in the states and 143 columns of different metrics related to solar and other useful information like education. Due to the size of the csv we extracted the columns we wanted to analyze and merged all the data for the same state together to form a new dataframe of all the states in the United States. Three states/territories were dropped in they process due to lack of information which was Hawaii, Alaska, and Puerto Rico.
Then we extracted data from the Census API and merged it with the Deep Solar data to create a new dataframe to use for our analysis.

*** Note: The Deep Solar dataset is a csv file that is larger than the 100 MB limit that is set for Github. So here is a link to my google drive to download the csv to your desktop so the mainscript.ipynb will run correctly when cycling through. Once downloaded you may need to adjust the path in the mainscript when reading the csv to your precise location. Link: "https://drive.google.com/file/d/1LzgMzcCLY813-dPi2gsYcrA2fw_52L63/view?usp=share_link" 

## Data Retrieval and Cleansing
The first step in the project was to gather data from both sources, clean it, and merge it together.

We started with the Census API where we created a dataframe of all the states and different economic and socioeconomic factors.

<img width="1216" alt="Screenshot 2022-11-14 at 1 50 45 PM" src="https://user-images.githubusercontent.com/112406455/201752675-af2ee07f-18a8-43fc-a1a5-603d8728d49c.png">

Then we read in the deepsolar csv and created another dataframe with certain columns that we felt were the most important to our task and dropped any nulls in the process. 

<img width="1213" alt="Screenshot 2022-11-14 at 1 57 10 PM" src="https://user-images.githubusercontent.com/112406455/201753923-31c63b03-ef7a-48e9-b626-2d496c7fdb62.png">

Once we had both dataframes from each dataset established we found that both of them had the fips numbers which could be used for merging but first we had to do some number altering in the deepsolar dataframe to just get the two digit state code. So we took the fips column in the deepsolar dataframe and divided by a billion to move the decimal place over. Then we coverted the column to an integer to drop all numbers after the decimal place. 

<img width="1216" alt="Screenshot 2022-11-14 at 2 08 26 PM" src="https://user-images.githubusercontent.com/112406455/201755756-75d0b434-49af-4fb6-ba48-c6c19613178a.png">

The next step in the process was to merge all the data for each state together in the deepsolar dataframe using an aggregate function and a grouby. This resulted in a new dataframe with just the states that is almost ready to be merged with the census dataframe. 

<img width="1214" alt="Screenshot 2022-11-14 at 2 15 04 PM" src="https://user-images.githubusercontent.com/112406455/201756936-a6354657-ab5f-47cd-884c-aa78901179c5.png">

Then we changed the name of the fips column in the deepsolar dataframe to "State" to match the column in the census dataframe for merging. 

<img width="1214" alt="Screenshot 2022-11-14 at 2 19 57 PM" src="https://user-images.githubusercontent.com/112406455/201757895-68e15244-c0de-4993-a7c7-0cab473adeaf.png">

After this we merged both dataframes together on the "State" column to create a single dataframe to use for our analysis. We also dropped any nulls which resulted in losing Alaska, Hawaii, and Puerto Rico in our set. 

<img width="1216" alt="Screenshot 2022-11-14 at 2 24 32 PM" src="https://user-images.githubusercontent.com/112406455/201758780-22842e99-ebbe-4b04-aab5-6c28f2b42674.png">

<img width="1192" alt="Screenshot 2022-11-14 at 2 26 46 PM" src="https://user-images.githubusercontent.com/112406455/201759112-2f6df8b4-7a20-4336-bb89-82c3889997e7.png">

## Analysis
Using the number or residential solar systems as a base comparison we ran statiscal analyis on all the different columns in our dataframe along with some other columns that were added later which you can find in the combined.csv file in the main repository and here are our findings.


<img width="1169" alt="Screenshot 2022-11-14 at 2 44 10 PM" src="https://user-images.githubusercontent.com/112406455/201762738-a37d8a0c-ff41-4972-803d-055acb4ee191.png">

<img width="1106" alt="Screenshot 2022-11-14 at 2 44 22 PM" src="https://user-images.githubusercontent.com/112406455/201762862-321aa710-2a67-4015-b17f-fa94a6223b0a.png">

<img width="1109" alt="Screenshot 2022-11-14 at 2 44 30 PM" src="https://user-images.githubusercontent.com/112406455/201763667-9d478045-8664-45ed-bca3-5161401eacd9.png">

<img width="1212" alt="Screenshot 2022-11-14 at 2 44 37 PM" src="https://user-images.githubusercontent.com/112406455/201763785-69080947-73cc-4ab8-8acd-10389279bbc5.png">

<img width="1183" alt="Screenshot 2022-11-14 at 2 44 45 PM" src="https://user-images.githubusercontent.com/112406455/201763913-49abb41c-f239-4084-9b36-28a00dba0c75.png">

<img width="1184" alt="Screenshot 2022-11-14 at 2 44 51 PM" src="https://user-images.githubusercontent.com/112406455/201764022-7b1a9c2f-5f28-4ad0-876f-1988f6bcb9bb.png">

<img width="1116" alt="Screenshot 2022-11-14 at 2 44 57 PM" src="https://user-images.githubusercontent.com/112406455/201764150-1d265f77-29bd-46d4-b694-07a19fa9f8b9.png">

<img width="1107" alt="Screenshot 2022-11-14 at 2 45 04 PM" src="https://user-images.githubusercontent.com/112406455/201764305-5bb061d1-5f01-494b-a9de-25a2d4b9f464.png">

<img width="1106" alt="Screenshot 2022-11-14 at 2 45 11 PM" src="https://user-images.githubusercontent.com/112406455/201764375-bfc7a938-7e98-4de8-8d47-8881088c8f30.png">

<img width="1214" alt="Screenshot 2022-11-14 at 2 45 19 PM" src="https://user-images.githubusercontent.com/112406455/201764473-0f8e8605-b202-41ad-9da6-c215b52fd4d2.png">

<img width="1104" alt="Screenshot 2022-11-14 at 2 45 26 PM" src="https://user-images.githubusercontent.com/112406455/201764574-98c26e98-5f8b-47a6-bc2f-b16ee619f8a5.png">

<img width="1106" alt="Screenshot 2022-11-14 at 2 45 34 PM" src="https://user-images.githubusercontent.com/112406455/201764739-a24d40f0-2eb1-4716-9b98-bc6c16ca9def.png">

<img width="1106" alt="Screenshot 2022-11-14 at 2 45 41 PM" src="https://user-images.githubusercontent.com/112406455/201764841-5d7b8996-c572-4550-af82-4b8e05e5979b.png">

<img width="1106" alt="Screenshot 2022-11-14 at 2 45 48 PM" src="https://user-images.githubusercontent.com/112406455/201764940-fc70a06a-d957-414e-8ad4-f5c34f677c4e.png">

