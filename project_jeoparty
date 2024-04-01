import pandas as pd
import re

# Adjust the display settings for columns
pd.set_option('display.max_colwidth', 500) 
# Load the data
jeopardy_data = pd.read_csv('jeopardy.csv')

# Inspect the first few rows and the column names
print(jeopardy_data.head())
print(jeopardy_data.columns)
# Rename the columns to remove spaces and make them consistent
jeopardy_data.columns = jeopardy_data.columns.str.strip().str.replace(' ', '_').str.lower()
print(jeopardy_data.columns)  # Confirm the column names are as expected
def filter_data(data, words):
    filter = lambda x: all(word.lower() in x.lower() for word in words)
    return data.loc[data['question'].apply(filter)]

# Test the function
filtered_questions = filter_data(jeopardy_data, ["King", "England"])
print(filtered_questions['question'])
def filter_data_improved(data, words):
    word_filter = lambda x: all(re.fullmatch(r'.*\b' + word.lower() + r'\b.*', x.lower()) for word in words)
    return data.loc[data['question'].apply(word_filter)]

# Test the improved function
filtered_questions_improved = filter_data_improved(jeopardy_data, ["King", "England"])
print(filtered_questions_improved['question'])
def convert_value_float(value):
    try:
        return float(value.strip('$').replace(',', ''))
    except:
        return 0

jeopardy_data['value_float'] = jeopardy_data['value'].apply(convert_value_float)

# Now you can calculate the average value of questions containing "King"
filtered_king = filter_data_improved(jeopardy_data, ["King"])
average_value_king = filtered_king['value_float'].mean()
print(average_value_king)
def count_unique_answers(data):
    return data['answer'].value_counts()

# Test the function
unique_answers_king = count_unique_answers(filtered_king)
print(unique_answers_king)

# Filter data for the 90s and count "Computer" mentions
computer_90s = filter_data_improved(jeopardy_data, ["Computer"])
computer_90s = computer_90s[computer_90s['air_date'].str.contains('199')]
print(len(computer_90s))

# Do the same for the 2000s
computer_2000s = filter_data_improved(jeopardy_data, ["Computer"])
computer_2000s = computer_2000s[computer_2000s['air_date'].str.contains('200')]
print(len(computer_2000s))
