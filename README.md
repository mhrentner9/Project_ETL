# README for ETL Project 2: External Benefits derived from higher Rent costs in MSAs in NFL cities

**Version 1.0.0

Python file for merging two datasets from 1) the American Housing Survey (AHS) and 2) Bureau of Labor Statistics (BLS) population and employment metrics

The goal is to setup a dataframe in order to run a regression analysis with an AHS survey respondent's monthly rent as the dependent variable. 
Housing and neighborhood characteristics from the AHS survey and population and employment metrics from the BLS Metroplolitan Statistical Areas (MSA) data
on population and employment. Additionally, a dummy variable for presence of an NFL team in an MSA must be accounted for.

# AHS Dataset
The AHS dataset is setup by merging 6 .sas7bdat files containing two datasets from 2015, 2017 and 2019. 
These are merged through a pandas sas7bdat conversion.

The AHS dataset is then transformed by 1) reducing the file to the necessary columns and observations and 
2) transforming the remaining independent variable columns into dummy variables.

The column needed for a dependent variable is RENT. Any observation non-observed value from RENT must be removed from the dataframe.

The independent variables needed are:
1) YRBUILT for year the building was built
2) GARAGE for if the unit has a garage
3) BATHROOM for # of bathrooms the unit has
4) UNITSIZE for squarefeet of the unit
5) HUDSUB for if the unit gets subsidized by Housing and Urban Development
6) SEWTYPE for if it has access to a public sewer
7) BLD to help control for number of units in the building. Buildings with 10 or more units are considered "high-rise" while <10 are considered "low-rise"
8) ACPRIMARY for if the unit has air conditioning
9) FLOORHOLE for if the unit has holes in the floor
10) HEATTYPE for if the unit has electric heating
11) NHQSCRIME for if the respondent said the neighborhood has serious crime
12) NHQPCRIME for if the respondent said the neighborhood has petty crime
13) NEARABAND for if the there is one or more abandoned buildings in the neighborhood

None of the independent AHS variables are ready to use. Some are YES/NO responses that need to be transformed into 1 for YES and 2 for NO. 
Some are marked numercially or alphabetically standing for various responses that can be found in the AHS 2019 Value Labels excel. 
All these variables were inspected from labels excel and views in Jupiter notebook. Number of Bathrooms, Year Built, and Unit Size are treated as linear
inputs. The remaining are then transformed into YES/NO dummy variables.

OMB13CBSA is the key for join with the BLS Metro file. This is the MSA numerical code for each MSA.

#BLS Metro Data
This data was pulled off the BLS data site and pasted into excel. A dummy variable for NFL team presence in the MSA was included in this .csv file too.
NFL team presence was 1 if the MSA included a team, while 0 did not. Only the top 50 MSA's are captured in the dataset. So, smaller markets like Green Bay
are not included in MSAs like Milwaukee.

#Merging
The dataframes are merged using pandas merge function with the AHS being the left anchor dataframe. Both anchor keys have the same column name (MSA_NO) 
and column format (int.).


