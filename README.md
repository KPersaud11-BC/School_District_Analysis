# School_District_Analysis by Kieran Persaud

## Overview of the School District Analysis
In the initial analysis, I utilized Anaconda's Jupyter notebook feature, along with the Pandas library, to analyze school funding and student test scores in a particular district. The data was aggregated and summarized in various Dataframes that showed trends in test performance and budget spent per student, across different factors like school size and grade. This was reported to the school board to assist in their decision making.

The school board determined that the initial analysis showed evidence of academic dishonesty; specifically, reading and math grades for Thomas High School ninth graders appear to have been altered. In the Challenge, I was asked to replace the math and reading scores for Thomas High School with NaNs while keeping the rest of the data intact. I re-ran the school district analysis, and was tasked with determining differences between the initial analysis and the Challenge

## Resources
- Data Source: schools_complete.csv, students_complete.csv
- Software: Anaconda 4.10.1, Pandas Library, kernels PythonData and numpy; Jupyter Notebook
- Reference:
  - Initial Analysis Code: PyCitySchools.ipynb
  - Challenge Code: PYCitySchools_Challenge.ipynb

## Results
The Challenge required me to replace all 9th grade reading and math scores with NaN. This was accomplished using the ```loc``` function. The code used for this is as follows;
To replace math scores:
```
student_data_df.loc[(student_data_df["school_name"]=="Thomas High School") & 
                    (student_data_df["grade"]=="9th"),["math_score"]]=np.nan
```
To replace reading scores:
```
student_data_df.loc[(student_data_df["school_name"]=="Thomas High School") & 
                    (student_data_df["grade"]=="9th"),["reading_score"]]=np.nan
```
- **How is the district summary affected?**

With the values changed to NaN, the above code was used to determine the count of 9th grade students, and subtract that number from the total student count to create a new     total student count. Below is that code.
```
# Step 1. Get the number of students that are in ninth grade at Thomas High School.
# These students have no grades. 
Thomas_df = student_data_df.loc[(student_data_df["school_name"]=="Thomas High School") & 
                    (student_data_df["grade"]=="9th")]
Thomas_ninth_count= Thomas_df["Student ID"].count()

# Get the total student count 
student_count = school_data_complete_df["Student ID"].count()
student_count
# Step 2. Subtract the number of students that are in ninth grade at 
# Thomas High School from the total student count to get the new total student count.
new_student_count = student_count - Thomas_ninth_count
new_student_count
```
This ```new_student_count``` was used to recalculate the percentages of students who passed math, reading, and overall, and created new variables. Below is the example for just math. The code was refactored for the other instances.
```
new_passing_math_percentage = (passing_math_count / float(new_student_count)) * 100
```
The Challenge District Summary values for Average Math Score, % Passing Math, % Passing Reading, and % Overall Passing all decreased by between 0.1 and 0.3 percentage points. This was a minor change, as we only changed approximately 461 entries out of 39,170 (1.2% change). The outputs of the Dataframes show the difference.

Initial Analysis Code:
![Initial District Summary](https://user-images.githubusercontent.com/84286467/125217730-605f6f80-e28f-11eb-8809-ccced975a522.PNG)

Challenge Code:
![Challenge District Summary](https://user-images.githubusercontent.com/84286467/125217747-6b1a0480-e28f-11eb-863e-aa5a97e107b5.PNG)



- **How is the school summary affected?**
There is a slight decrease in the average scores and the % passing for each subject area and overall, except for average reading which saw a slight increase. The most notable difference is the decrease in % Overall Passing by 0.3 percentage points

**Initial Analysis Code:**
![Header](https://user-images.githubusercontent.com/84286467/125217848-a9afbf00-e28f-11eb-8f96-0cff1978b481.PNG)
![Initial Code School Summary](https://user-images.githubusercontent.com/84286467/125217793-89800000-e28f-11eb-818c-c9a7e53d3ff9.PNG)

**Challenge Code:**
![Challenge Code School Summary](https://user-images.githubusercontent.com/84286467/125217800-8f75e100-e28f-11eb-9537-f8cfe326dc4d.PNG)

- **How does replacing the ninth graders’ math and reading scores affect Thomas High School’s performance relative to the other schools?**
There is no change in Thomas High School's performance relative to the other schools. It remains in the high performing schools dataframe in both analyses.

![High Performer](https://user-images.githubusercontent.com/84286467/125218075-1fb42600-e290-11eb-8b7b-de2241181de4.PNG)

- **How does replacing the ninth-grade scores affect the following:**
  - Math and reading scores by grade
  
  By removing 9th grade math and reading scores from Thomas HS, the dataframes show nan for that intersection.
  
  ![By_Grade](https://user-images.githubusercontent.com/84286467/125218082-26db3400-e290-11eb-838e-0f5e42d80b9b.PNG)

  - Scores by school spending
  
  There is a very slight decrease across all column categories in the $630-644 bin, in which Thomas High School is categorized. However, since the difference in the hundredths and thousandths, it is unnoticeable when rounded using our formatting.
  
  **Initial Analysis Code:**
  
  <img src="https://user-images.githubusercontent.com/84286467/125218134-4a05e380-e290-11eb-84e1-62ab583757b6.PNG" width="810" height="186">

  **Challenge Code:**
  
  ![Challenge_spending](https://user-images.githubusercontent.com/84286467/125218787-9e5d9300-e291-11eb-93b2-56655a660563.PNG)
  
  - Scores by school size
  
  There is a very slight decrease across all column categories in the Medium size bin, in which Thomas High School is categorized. However, since the difference in the     hundredths and thousandths, it is unnoticeable when rounded using our formatting.
  
  **Initial Analysis Code:**
  
  <img src="https://user-images.githubusercontent.com/84286467/125218884-d1a02200-e291-11eb-8050-59751887f56f.PNG" width="810" height="186">

  **Challenge Code:**
  
  ![Challenge_size](https://user-images.githubusercontent.com/84286467/125218935-f6949500-e291-11eb-8794-01c6cf26954d.PNG)

  - Scores by school type
  
  There is a very slight decrease across all column categories in the Charter type, in which Thomas High School is categorized. However, since the difference in the     hundredths and thousandths, it is unnoticeable when rounded using our formatting.
  
  **Initial Analysis Code:**
  
  <img src="https://user-images.githubusercontent.com/84286467/125219056-26dc3380-e292-11eb-8b96-f0dbec0dee62.PNG" width="810" height="186">
  
  **Challenge Code:**
  
  ![Challenge_type](https://user-images.githubusercontent.com/84286467/125219134-4f642d80-e292-11eb-8fd5-9cd5ea73799e.PNG)

  
## Summary 
Summarize four changes in the updated school district analysis after reading and math scores 
for the ninth grade at Thomas High School have been replaced with NaNs.
