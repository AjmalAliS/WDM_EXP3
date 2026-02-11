### EX3 Implementation of GSP Algorithm In Python
### DATE: 11/02/26
### AIM: To implement GSP Algorithm In Python.
### Description:
The Generalized Sequential Pattern (GSP) algorithm is a data mining technique used for discovering frequent patterns within a sequence database. It operates by identifying sequences that frequently occur together. GSP works by employing a depth-first search strategy to explore and extract frequent patterns efficiently.
### Steps:
1. <strong>Database Scanning:</strong> GSP scans the sequence database to determine the support of each item in the dataset.
2. <strong>Candidate Generation:</strong> It generates a set of candidate sequences using frequent items found in the previous step.
3. <strong>Pattern Growth:</strong> It extends the candidate sequences by merging them to form longer patterns, checking their support against a user-defined minimum support threshold.
4. <strong>Repeat:</strong> The process continues until no new sequences meet the minimum support threshold.
<p align="justify">
GSP finds application in various domains such as market basket analysis, web usage mining, bioinformatics, and more. For instance, in retail, GSP can identify common purchasing patterns, helping businesses understand customer behavior for targeted marketing or inventory management.
</p>

### Procedure:
<p align="justify">
1. From collections import defaultdict, from itertools import combinations: Imports necessary libraries/modules. defaultdict is
used to create a dictionary with default values and combinations generates all possible combinations of a sequence.</p>
<p align="justify">
2. generate_candidates(dataset, k): Function to generate candidate k-item sequences from a dataset. It loops through each sequence in the
dataset and finds combinations of length k for each sequence, updating their counts in a dictionary.</p>
<p align="justify">
3. gsp(dataset, min_support): Function that implements the Generalized Sequential Pattern (GSP) algorithm. It iterates through increasing
sequence lengths (k) until no new frequent patterns are found. It calls generate_candidates() to find patterns of varying lengths.</p>
<p align="justify">
4. Example dataset for each category: Defines example sequences for top wear, bottom wear, and party wear categories.</p>
<p align="justify">
5. Minimum support threshold: Sets the minimum support count required for a pattern to be considered frequent.</p>
<p align="justify">
6. Perform GSP algorithm for each category: Applies the GSP algorithm for each category using the defined example datasets and the
minimum support threshold.</p>
<p align="justify">
7. Output the frequent sequential patterns for each category: Prints the frequent sequential patterns 
    along with their support counts
for each wear category.</p>
<p align="justify">
8. Visulaize the sequence patterns using matplotlib.
</p>
### Program:

```
from collections import defaultdict
from itertools import combinations
import pandas as pd

# Function to generate candidate k-item sequences
def generate_candidates(dataset, k):
    candidates = defaultdict(int)
    for sequence in dataset:
        for combination in combinations(sequence, k):
            candidates[combination] += 1
    return candidates

# Function to perform GSP algorithm
def gsp(dataset, min_support):
    k = 1
    frequent_patterns = defaultdict(int)

    # Initially, find all frequent items (1-item sequences)
    candidates = generate_candidates(dataset, k)
    while candidates:
        # Filter out candidates that don't meet the minimum support
        for candidate, support in candidates.items():
            if support >= min_support:
                frequent_patterns[candidate] = support

        # Generate new candidates of length k+1
        k += 1
        candidates = generate_candidates(dataset, k)

    return frequent_patterns

    # Function to display patterns length-wise as separate tables
def display_results_by_length(category, result):
    print(f"\nFrequent Sequential Patterns - {category}")

    if not result:
        print("No frequent patterns found.")
        return

    max_length = max(len(pattern) for pattern in result.keys())

    for length in range(1, max_length + 1):

        # Filter patterns of current length
        filtered_patterns = {
            pattern: support
            for pattern, support in result.items()
            if len(pattern) == length
        }

        print(f"\n{length} Length Pattern")
        print("-" * 40)

        if filtered_patterns:
            data = {
                "Sequence": [str(pattern) for pattern in filtered_patterns.keys()],
                "Support": list(filtered_patterns.values())
            }
            df = pd.DataFrame(data)
            print(df.to_string(index=False))
        else:
            print("No frequent patterns")

top_wear_data = [['a','b','c','b','e','c','f','g','a','b','e'],['a','d','b','c','c','f','g','c','h'],['b','c','a','d','e','b','f','c','d','f','g','h'],['c','e','c','e','h']]

# Minimum support threshold
min_support = 5

# Perform GSP algorithm for each category
top_wear_result = gsp(top_wear_data, min_support)



# Display the frequent sequential patterns as a table
display_results_by_length('Top Wear', top_wear_result)

```
### Output:

<img width="582" height="728" alt="image" src="https://github.com/user-attachments/assets/80941674-346f-477e-87b6-0946573bfb4d" />












<img width="395" height="618" alt="image" src="https://github.com/user-attachments/assets/31b0262b-14bd-4e56-8050-1cd222b6a4a8" />

### Visualization:
```python
import matplotlib.pyplot as plt

# Function to visualize frequent sequential patterns with a line plot
def visualize_patterns_line(result, category):
    if result:
        patterns = list(result.keys())
        support = list(result.values())

        plt.figure(figsize=(10, 6))
        plt.plot([str(pattern) for pattern in patterns], support, marker='o', linestyle='-', color='blue')
        plt.xlabel('Patterns')
        plt.ylabel('Support Count')
        plt.title(f'Frequent Sequential Patterns - {category}')
        plt.xticks(rotation=90)
        plt.tight_layout()
        plt.show()
    else:
        print(f"No frequent sequential patterns found in {category}.")

# Visualize frequent sequential patterns for each category using a line plot
visualize_patterns_line(top_wear_result, 'Top Wear')

```
### Output:
<img width="1161" height="571" alt="image" src="https://github.com/user-attachments/assets/5f96cf06-b412-4fd6-8e3f-51cbc8835494" />



### Result:
Thus the implementation of the GSP algorithm in python has been successfully executed.
