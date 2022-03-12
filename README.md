# Election_Analysis
## Overview of Election Audit
### Background
Election commision was provided with Audit Results of the most recent Elections of Colorado. Upon this available data Election Commision requested more insite on the data and a detailed report.
	
### Purpose
The purpose of this project is to provide more information related to the Audit Results which was submitted to The Election Commission. We work over the data, analyzed and created a report to answers the following requested details
	- The Voter turnout for each county
	- The percentage of Votes from each county out of the total count
	- The county with the highest turnout

## Election-Audit Results
### Overview
Inorder to analyze the data we read the data from [Election Result data file](https://github.com/DeepaGheewala/Election_Analysis/blob/694fc9f2d651ffb8712654427bf5171775bf11bf/Resources/election_results.csv)

This file was analyzed using the Python Code and the results generated were stored into [Election Analysis text file](https://github.com/DeepaGheewala/Election_Analysis/blob/694fc9f2d651ffb8712654427bf5171775bf11bf/analysis/election_analysis.txt)
The below image shows the analysis results

<img src="https://github.com/DeepaGheewala/Election_Analysis/blob/735e962a245065f7dd740f0209eaf7ee15dd1c1c/Resources/election_analysis.png" width="350" height="450"/>


### Detailed Report
Let us understand in detail regarding the Analysis Report. The snapshots used below are taken from the [Election Analysis file](/analysis/election_analysis.txt)
   
  The below code snippet was used for reading the CSV file [Election Result data file](https://github.com/DeepaGheewala/Election_Analysis/blob/694fc9f2d651ffb8712654427bf5171775bf11bf/Resources/election_results.csv)
```phython
# Add our dependencies.
import csv

# Add a variable to load a file from a path.
file_to_load = os.path.join("Resources", "election_results.csv")

# Add a variable to save the file to a path.
file_to_save = os.path.join("analysis", "election_analysis.txt")

# Read the csv and convert it into a list of dictionaries
	with open(file_to_load) as election_data:
		reader = csv.reader(election_data)

```
  
  Code to write into the [Election Analysis file](/analysis/election_analysis.txt)
  
```phython
# Add our dependencies.
import os

# Add a variable to save the file to a path.
file_to_save = os.path.join("analysis", "election_analysis.txt")

# Save the results to our text file.
with open(file_to_save, "w") as txt_file:

	# Print the final vote count (to terminal)
	election_results = (
		f"\nElection Results\n"
		f"-------------------------\n"
		f"Total Votes: {total_votes:,}\n"
		f"-------------------------\n\n"
		f"County Votes:\n")
	print(election_results, end="")

txt_file.write(election_results)
```
    
#### Total votes casted in this congressional election 
  Total of ***369,711** votes were casted during this Congressional Election.
 <img src="https://github.com/DeepaGheewala/Election_Analysis/blob/735e962a245065f7dd740f0209eaf7ee15dd1c1c/Resources/TotalVotes.png" width="300" height="150"/>
 
 code snippets to count Total Votes
 ```python
   # For each row in the CSV file.
    for row in reader:

        # Add to the total vote count
        total_votes = total_votes + 1

...

 # Print the final vote count (to terminal)
    election_results = (
        f"\nElection Results\n"
        f"-------------------------\n"
        f"Total Votes: {total_votes:,}\n"
        f"-------------------------\n\n"
 ```
 
#### County wise breakdown and percentage of total votes and determined the largest number of votes of winning County
<img src="https://github.com/DeepaGheewala/Election_Analysis/blob/735e962a245065f7dd740f0209eaf7ee15dd1c1c/Resources/LargestCountyVotes.png" width="300" height="200"/>

***To get distinct list of counties and count votes for each county***
 1. Read each county value from the extracted row and check if the previous county name is same as the current. 
 2. Once we have all the list of counties and corresponding vote countes
	- Iterate through each county to find the percentage of Votes
 	- compare and find the winning county
 3 Lastly write into the file
 
 Refer to [Code Snippet](#Python_Code_for_Candidates_Votes)

#### Candidate wise breakdown and percentage of total votes and determined the winning Candidate
	
<img src="https://github.com/DeepaGheewala/Election_Analysis/blob/e23022b8df9a28cccc7f8bdb59923d0aeee94ffc/Resources/winner.png" width="300" height="200"/>

***To get distinct list of candidates and count votes for each Candidate***
 1. Read each Candidates from the extracted row and check if the previous county name is same as the current. 
 2. Once we have all the list of counties and corresponding vote countes
	- Iterate through each county to find the percentage of Votes
 	- compare and find the winning Candidate
 3 Lastly write into the file

Refer to [Code Snippet](#Python_Code_for_County_Votes)

## Code Snippets
### Python Code for County Votes
```python
# 4a: Write an if statement that checks that the
        # county does not match any existing county in the county list.
        if county_name not in county:
            
            # 4b: Add the existing county to the list of counties.
            county.append(county_name)

            # 4c: Begin tracking the county's vote count.
            county_votes[county_name] = 0

        # 5: Add a vote to that county's vote count.
        county_votes[county_name] += 1
	
	...
	
	# 6a: Write a for loop to get the county from the county dictionary.
    for county_nam in county:
        # 6b: Retrieve the county vote count.
       
        votes_counting = county_votes[county_nam]
        # 6c: Calculate the percentage of votes for the county.
        vote_percent = float(votes_counting) / float(total_votes) * 100

        county_results = (
            f"{county_nam}: {vote_percent:.1f}% ({votes_counting:,})\n"
        )
         # 6d: Print the county results to the terminal.
        print(county_results)
         # 6e: Save the county votes to a text file.
        txt_file.write(county_results)
         # 6f: Write an if statement to determine the winning county and get its vote count.
        if (votes_counting > winning_count) and (vote_percent > winning_percentage):
            winning_count = votes_counting
            winning_county = county_nam
            winning_percentage = vote_percent

    # 7: Print the county with the largest turnout to the terminal.
    turnout_results = (
        f"\n-------------------------\n"
        f"Largest County Turnout: {winning_county}\n"
        f"-------------------------\n\n"
    )
    print(turnout_results)

```
### Python Code for Candidates Votes
```python
  # If the candidate does not match any existing candidate add it to
  # the candidate list
       
  if candidate_name not in candidate_options:

    # Add the candidate name to the candidate list.
     candidate_options.append(candidate_name)

    # And begin tracking that candidate's voter count.
     candidate_votes[candidate_name] = 0

    # Add a vote to that candidate's count
     candidate_votes[candidate_name] += 1
	
...
	
# Save the final candidate vote count to the text file.
    
for candidate_name in candidate_votes:
	# Retrieve vote count and percentage
        votes = candidate_votes.get(candidate_name)
        vote_percentage = float(votes) / float(total_votes) * 100
        candidate_results = (
            f"{candidate_name}: {vote_percentage:.1f}% ({votes:,})\n\n")

    	# Print each candidate's voter count and percentage to the
        # terminal.
        print(candidate_results)
        #  Save the candidate results to our text file.
        txt_file.write(candidate_results)

        # Determine winning vote count, winning percentage, and candidate.
        if (votes > winning_count) and (vote_percentage > winning_percentage):
            winning_count = votes
            winning_candidate = candidate_name
            winning_percentage = vote_percentage

# Print the winning candidate (to terminal)
winning_candidate_summary = (
    f"-------------------------\n"
    f"Winner: {winning_candidate}\n"
    f"Winning Vote Count: {winning_count:,}\n"
    f"Winning Percentage: {winning_percentage:.1f}%\n"
    f"-------------------------\n")
print(winning_candidate_summary)

# Save the winning candidate's name to the text file
txt_file.write(winning_candidate_summary)

```

## Resources
CSV Files
Phython 3.9.10
VS Code 1.65.2
