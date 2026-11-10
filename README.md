# project1-sequence-analysis
Project 1: Identifying Mutatiobs in NGS Data

This Project simulates NGS data analysis workflow to investigate mutation patterns between fission yeast samples treated with a genotoxic agent versus untreated controls

How to run the program:
1. Open the notebook in Google Colab
2. Run the setup and download cells to get 'reference.txt' and 'readd.csv'
3. Execute the code blocks for step 1 through 5

Inputs and Outputs:

The input expects a 200-nt reference sequence string and a dataset of sequencing read dictionaries containing sample metadata and sequences. It returns structured dictionaries containing validation statuses, error codes, and annotated missmatch lists. Additionally, it displays formatted summary tables grouped by treatment status, substitution mutation frequencies, and statistical comparision results for identified mutation hotspots.

Code Design:

First, i modularised the pipeline into distinct, single reponsibility functions to improve testability and code readability. Isolating validation prevents cascading errors when processing malformed reads. Alternatively, a monolithic function was considered but rejected due to poor maintainability. Second, i utilised nested dictionaries and robust sorting keys (sorting by count descending, then position ascending) in summarise_samples to handle tie breaking cleanly for mutation hotspots. Finally, i ensured invalid reads gracefully bypass mutation scanning rather than the script, storing error codes cleanly in a list.

Testing:

1. Invalid character and length test: Passed strings containning non A/C/G/T characters and incorrect lengths to verify proper error logging (wrong_length, invalid_characters)
2. Case-insensitivity test: Inputted lower-case sequences to confirm automatic normalisation to upper case without triggering false mismatch flags.
3. Edge case sample test: Tested datasets with zero valid reads to ensure percentage calculations gracefully evaluate to None without division by zero errors.
