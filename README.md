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
5. Projections for the Future
6. Where to Next

## Questions
* Is there any relation to education and solar usage?
* Is household income related to the usage of solar energy?
* What states are using solar the most?
* Is there a connection between population density and solar usage? 

## Overview of Data
In this project we used two main datasets:
* Deep Solar (last updated 2016)
* Cenus API (last updated 2020)

The Deep Solar data is a csv we found on Kaggle with 72,538 rows organized by zip codes of different areas in the states and 143 columns of different metrics related to solar and other useful information like education. Due to the size of the csv we extracted the columns we wanted to analyze and merged all the data for the same state together to form a new dataframe of all the states in the United States. Then we extracted data from the Census API and merged it with the Deep Solar data to create a new dataframe to use for our analysis. Three states/territories were dropped in they process due to lack of information which was Hawaii, Alaska, and Puerto Rico.

*** Note: The Deep Solar dataset is a csv file that is larger than the 100 MB limit that is set for Github. So here is a link to my google drive to download the csv to your desktop so the mainscript.ipynb will run correctly when cycling through. Once downloaded you may need to adjust the path in the mainscript when reading the csv to your precise location. Link: "https://drive.google.com/file/d/1LzgMzcCLY813-dPi2gsYcrA2fw_52L63/view?usp=share_link" 

## Data Retrieval and Cleansing
The first step in the project was to gather data from both sources, clean it, and merge it together in the mainscript.ipynb.

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

## Edscript.ipynb
The first part of the analysis is using edscript.ipynb. We used the number or residential solar systems as a base comparison where we ran statistical analysis on all the different columns in our dataframe along with some other columns that were added later which you can find in the combined.csv file in the main repository. Here are our findings.


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

<img width="1197" alt="Screenshot 2022-11-14 at 3 08 05 PM" src="https://user-images.githubusercontent.com/112406455/201765900-48f931bf-d708-465d-ae87-18993d0159bc.png">

<img width="1213" alt="Screenshot 2022-11-14 at 3 08 13 PM" src="https://user-images.githubusercontent.com/112406455/201766006-c1d03752-5e08-4d51-a942-4cfadd2d901e.png">

### Results 
After thorough testing, we found only one variable that held any significant correlation, with a R-value of 0.9989 but that variable was total solar panel area. Ultimately, predicting how many residential solar installations a given state will have probably depends on some complex combination of variables of different weights, but at this point and with the data readily available from the government and industry, we just haven’t been able to work out exactly what that equation is.

## Allyson's part.ipynb
For the next part of the analysis we will be using allyson's part.ipynb where we looked at who is using solar energy more, the northernmost states or the southernmost states. In this analysis, the combined.csv was used to make two new dataframes one for the northern states and one for the southern states and then plotted in a bar chart to see who uses the most solar by state for each region. 

<img width="1209" alt="Screenshot 2022-11-14 at 3 51 07 PM" src="https://user-images.githubusercontent.com/112406455/201775531-9192cc5c-883e-4b9f-9dcd-fbbc9f4a46fb.png">

<img width="1128" alt="Screenshot 2022-11-14 at 3 52 03 PM" src="https://user-images.githubusercontent.com/112406455/201775824-6c1262a1-9ec2-4e33-940f-67b585c2fe6d.png">

<img width="1110" alt="Screenshot 2022-11-14 at 3 52 13 PM" src="https://user-images.githubusercontent.com/112406455/201775939-af7afb1a-6a30-4f72-89a4-fc89bfd401da.png">

### Results 
We found that the southernmost states have a higher count of residential solar systems in place at 905,267. The northernmost states only came out with 82,213 systems. 

## Project_One_LH.ipynb
In the next part of the analysis we will be using Project_One_LH.ipynb to look to see if there is any correlation between residential electricity price and per capita income, home ownership and solar companies in the state. In this script we also analyzed to see if the availability to solar businesses was a major factor in solar usage.

<img width="1246" alt="Screenshot 2022-11-14 at 6 13 00 PM" src="https://user-images.githubusercontent.com/112406455/201794660-b70da4da-4239-43b6-a419-714e1b685e75.png">

<img width="1109" alt="Screenshot 2022-11-14 at 7 12 55 PM" src="https://user-images.githubusercontent.com/112406455/201802207-79380def-b1cc-4d5d-b84b-a40c7cc3e5a6.png">

<img width="1109" alt="Screenshot 2022-11-14 at 7 18 32 PM" src="https://user-images.githubusercontent.com/112406455/201802924-5e3ba6e0-eddc-42fc-8417-d1529b2f3364.png">

<img width="1109" alt="Screenshot 2022-11-14 at 7 18 38 PM" src="https://user-images.githubusercontent.com/112406455/201802946-fd904320-f2e2-48cf-94af-4148fe5e110a.png">

### Results
Although availability may play a role, the data does not show a correlation.  Determining how a household makes their decision in this case is not confirmed to be home ownership, per capita income or the availability of solar.  So, once again a negative result is still a result.  Our data shows there are a multitude of factors that play key roles in solar across the US, a continent that is vast and varied in its population density, income, education, technology and land use.

## Ericscript.ipynb
For the final analysis we used ericscript.ipynb to look for any trends in our data on a heat map made in Google Maps.

Heat map showing electricity costs by state:

<img width="970" alt="Screenshot 2022-11-14 at 8 02 50 PM" src="https://user-images.githubusercontent.com/112406455/201808484-5b680f72-c484-4324-906c-be0300504a19.png">


This one is displaying daily solar radiation by state:

<img width="994" alt="Screenshot 2022-11-14 at 3 40 31 PM" src="https://user-images.githubusercontent.com/112406455/201771503-62441af9-9b2f-455b-8ae4-f4c3e6b1cfa0.png">

## Projections for the Future

As of today:
<img width="981" alt="Screenshot 2022-11-14 at 7 39 21 PM" src="https://user-images.githubusercontent.com/112406455/201805615-96eb561c-5583-4242-b2d7-bc6d7e08ab08.png">

Projected in five years:
<img width="980" alt="Screenshot 2022-11-14 at 7 39 27 PM" src="https://user-images.githubusercontent.com/112406455/201805717-724ae685-3186-4ff4-a6fb-b9d52f4deed6.png">

As of today, solar installations generate 130.9 GW of energy in the country, and account for about 2.8% of the U.S.’s energy production.  However, by mapping out the energy generation, we can get a good visual of how individual states are doing.
Now, the heat map is focused on the coordinates of the state capitals, so there is some overlapping artifact that make their individual effects look a bit out-sized, particularly in the smaller northern states, but it’s a good map to show us the overall trend.
This map reveals that Texas is actually number two in the nation in energy produced by solar panels, behind only CA with 15 GW compared to their 37 GW.
However, as we can see from this next map, over the next 5 years, the focus of solar panel growth is expected to be heavily in Texas, followed by the north and midwest.  Nationally, this will represent a 249.4% projected increase in solar power generation.
Closer to home, Texas is expected to outpace CA in solar panel growth.  However, CA is growing its solar generation at approximately 5 GW per year, while Texas is outpacing it at 8 GW.  At those rates of growth, Texas will surpass CA in solar power generation before the end of 2029.
(Data from: https://www.seia.org/states-map and https://www.eia.gov/energyexplained/electricity/electricity-in-the-us-generation-capacity-and-sales.php)

## Where to Next
Coming into this we had some questions that we were unable to find answers to with the data we had available. 
Such as data on the age of homes/efficiency of construction? Or the attainability of solar for the average homeowner? We also couldn’t find a reason why the states with the highest solar radiation didn’t also have the highest adoption? The effects of weather and the issues regarding power transmission that would allow remote solar to work because professional estimates say the US would only need .5 to 1 % of all land to generate 100% of the needs we have. We just need more data. 

## Instructions on how to run the code properly:
* Download the repository onto your computer
* Then download the Deep Solar csv from the link that we provided in the Overview of Data section
* Open the repository in Jupiter Notebook
* Add your api keys to the apikeys.py file
* Then select solar.ipynb 
* Make sure to create the correct pathway when reading the Deep Solar csv in line 4 of the code
* Select the "Kernel" tab and click "Restart Kernel and Clear all Outputs"
* Then proceed to hit shift+enter to cycle through the script cell by cell
* The code is accompanied by an outline to walk you through the process step by step
* Once finished, you will notice an output_data file with all images of the plots that were generated in the code.

## References 
© 2022 edX Boot Camps LLC
