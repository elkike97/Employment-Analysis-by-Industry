Description:  Used the data set from the U.S. Bureau of Labor Statistics site, which collects demographic information from American households and provides a snapshot of the employment situation in 2011, 2021, and 2031. With our code you can specify which table you want to view; any other person can go to the start text variable and specify the table desired. With our code, you can also pick a specific field (industry) to analyze; if the table has the selected industry that you want to view, it will pick all of the items and store it in the found rows,  which are then converted into a dictionary as its more straightforward to pick the data for the future and make it easier to read for a layperson. In terms of the output, it will show all the values for each column name and show the user all the information for the specified industry.
 

Selected Data Set and General Information: 
Used the data set from the U.S. Bureau of Labor Statistics (BLS) site. This website serves to collect demographic information from American households. The data that the team is looking at is Employment Projections: Employment by Major Industry Sector. This data can be found on the BLS URL: https://www.bls.gov/emp/tables/employment-by-major-industry-sector.htm. This data set collects a randomized sample of American employment and groups the count by industry. 


Method of Data Extraction: 
The BLS website does have CSV/xls formats of the data set available for download. However, the team would like to use this project opportunity and conduct various exploratory analyses of different Python libraries. Among the steps to extract the HTML elements, the group will inspect and decide on the library and then write some code for our desired data output. The team will then choose one of the following libraries for data extraction: Beautiful Soup, Selenium, or Scrappy. As the group is relatively new in Python and general data processing, it will take considerable time to learn and load the data into Jupyter for correct analysis. One of the significant aspects of BLS is the fact that they have a dedicated page for accessing public access API for Python (https://www.bls.gov/developers/api_python.htm) The team will be exploring the API and discussing various ways in which this data can be used for a private company. 

 Installation: The user will have to import the CSV and, from the itertools module, import zip_longest


Usage:   The data can be helpful for any economist trying to predict economic trends or students/employees curious about changing their careers.  Economists can reference this data with the certainty of accuracy as this survey presided over the larger population of the United States. Using government-sponsored data is less biased than a survey carried out by a private entity. Students and current employees can also review this data to determine their career aspirations.  The team would like to use this data and create a better visualization to make it more legible for a novice researcher and suggest various trends regarding employment in a particular industry.  With this data, the team would also like to propose the best industries to look out for in the next decade.

 Potential Uses for Selected Data Set: 

The data can be helpful for any economist trying to predict economic trends or students/employees curious about changing careers. Economists can reference this data with the certainty of accuracy as this survey presided over the larger population of the United States. It is a lesser bias to use government-sponsored data as opposed to a survey carried out by a private 

 Challenges:
Some challenges we faced while running the code are BeautifulSoup Package was restricted for
this particular project With parsing, the developer will need to go into the CSV to find
specifics of the data. Using alternative packages, such as Tabulate, is possible but
challenging to implement without altering the composition of the CV file. It was necessary to
convert the list into a dictionary to provide extractable data. For data analysis, dictionary
values must be expressed as integers or floating point values. Since the data is categorized
by decade, we can use data from 2011 through 2021 for our project. Additionally, we
encountered a limitation related to the problem of overlapping workers when individuals are
assigned to or categorized under multiple functions or departments within an organization.
Identifying clear roles and responsibilities can be challenging, as ensuring appropriate
workload distribution and maintaining accountability in such a situation.


Parsing Code:  
 
import csv 
from itertools import zip_longest 
start_text = "Table 2.1 Employment by major industry sector"  # Specific text to determine the starting row 
end_text = "Table 2.2: Table 1"  # Specific text to determine the ending row 
remove_extra_table_names_start = 'Table 2.2 Output by major industry sector' 
remove_extra_table_names_end = 'Table 2.11 Employment and output by industry' 
  
rows = []  # List to store the extracted rows 
remove_rows = False  # Flag to indicate whether to remove rows or not 
  
with open("/Users/ramshaperwez/Desktop/Drexel/DSCI 511/industry.csv", "r") as file: 
csv_reader = csv.reader(file) 
 
#This for loop removes unwanted lines from our csv so we can extract the specific table we want (2.1) 
for row in csv_reader: 
    	if start_text in row: 
        	remove_rows = True 
    	if remove_extra_table_names_start in row: 
        	remove_rows = False 
    	if remove_extra_table_names_end in row: 
        	remove_rows = True 
    	if remove_rows: 
        	rows.append(row) 
    	if end_text in row: 
        	rows.pop() 
        	break 
        	 
#removing empty lines 
for row in rows[:]: 
    	if not any(cell.strip() for cell in row): 
        	rows.remove(row) 
  
# Selecting a specific field to analyze  
  
selected_text = 'Mining' 
found_rows = [] 
  
for row in rows: 
if selected_text in row: 
    	found_rows = row[:]  # Assuming the row values start from index 1 (excluding the first column) 
  
# Print the found rows 
if found_rows: 
column_names = ['Industry Sector Selected', 'Employment 2011', 'Employment 2021', 'Employment 2031', 'Employment Change, 2011-21', 'Employment Change, 2021-31', 'Percent Distribution, 2011', 'Percent Distribution, 2021', 'Percent Distribution, 2031', 'Compound Annual Rate of Change, 2011-21', 'Compound Annual Rate of Change, 2021-31', '', '', '', '', '', ''] 
  
# Zip the column names and row values together, filling missing values with a default value 
row_dict = { 
column: value 
for column, value in zip_longest(column_names, found_rows, fillvalue='') 
} 
for key, value in list(row_dict.items()): 
if value == '': 
    	row_dict.pop(key) 
 
for key, value in row_dict.items(): 
print(f"{key}: {value}") 
