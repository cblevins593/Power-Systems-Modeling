# Assignment 1
'Assignment_1.ipynb' requires the following input files to be loaded into the directory:<br>
'Market PJMISO constraint list.csv'<br>
'Pano PJMISO constraint list.csv'<br>
'Dayzer PJMISO constraint list.csv'

This script will output the following into the directory:<br>
'Assignment 1 Output.csv'

# Assignment 2
## Creating Features - Runtime ~ 20 minutes
'A2_create_features.ipynb' shall be run first with the following input files loaded into the directory:<br>
'bus_load_2022.parquet'<br>
'bus_load_2023.parquet'<br>
'bus_load_2024.parquet'<br>
'bus_load_2025.parquet'<br>
'zone_load_2022.parquet'<br>
'zone_load_2023.parquet'<br>
'zone_load_2024.parquet'<br>
'zone_load_2025.parquet'<br>

This script will output the following into the directory:<br>
'features.parquet'<br>
'zone_features.parquet'<br>
'lagged_bus_share.parquet'<br>

## Direct Bus Forcast - Runtime ~ 20 minutes
'A2_direct_bus.ipynb' shall be run second with the following file in the directory:<br>
'features.parquet'<br>

This script will output the following into the directory:<br>
'direct_bus_predictions.parquet' - The file is not uploaded to Github however, a sample is shown at the bottom of the jupyter notebook

## Zone Share Bus Forcast - Runtime ~ 3 minutes
'A2_zone_bus_share.ipynb' shall be run third with the following files in the directory:<br>
'features.parquet'<br>
'zone_features.parquet'<br>
'lagged_bus_share.parquet'<br>

This script will output the following into the directory:<br>
'zone_bus_share_predictions.parquet' - The file is not uploaded to Github however, a sample is shown at the bottom of the jupyter notebook

# Assignment 3 - Strategy
A possible strategy for matching Dayzer buses to the Panorama buses is outlined as follows:<br>
1. Normalize all data as performed in assignment 1. Create a string that will be used for matching for each entry in the branch data by combining key columns including branch type, name, from_bus, and to_bus. 
2. Find the inverse document frequency of words as done in assignment 1.
3. Build a token index as done in assignment 1.
4. For each PANO branch, find the best quality match from the Dayzer branch dataset
5. While calculating the quality of the matches, filter out any potential matches that do not share the same to_kv and from_kv since they are likely not matches
6. Once the best match is found, the to_bus and from_bus from each dataset will be used as pointers towards matching buses
7. take the to_bus from the matching Dayzer and PANO branches and find the best match in the Dayzer bus and PANO bus datasets respectively
8. Repeat step 7 with the from_bus for each branch
9. Store the bus matches

This strategy would only find matches to the buses attached to the branches in the PANO dataset. Duplicate matches, disagreeing matches, and buses not appearing in any matches would all be possible issues that need to be properly addressed.
# AI Usage Log
AI was used throughout this project for pipeline design, coding, debugging, and solution suggestions. All code was thoroughly reviewed and modified before being implemented in the forecast pipeline. ChatGPT was the AI that was used for this project. See below links to the chat history.

https://chatgpt.com/share/6a14bfbf-fdb4-83ea-b827-657c5508a069

https://chatgpt.com/share/6a14c047-b4f4-83ea-842d-0fa1cf39a925
