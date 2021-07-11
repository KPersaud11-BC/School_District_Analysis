# School_District_Analysis by Kieran Persaud

## Overview of the School District Analysis
In the initial analyis, I utilized Anaconda's Jupyter notebook feature, along with the Pandas library, to analyze school funding and student test scores in a particular district. The data was aggregated and summarized in various Dataframes that showed trends in test performance and budget spent per student, across different factors like school size and grade. This was reported to the school board to assist in their decision making.

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


Challenge Code:



- How is the school summary affected?
- How does replacing the ninth graders’ math and reading scores affect Thomas High School’s performance relative to the other schools?
- How does replacing the ninth-grade scores affect the following:
  - Math and reading scores by grade
  - Scores by school spending
  - Scores by school size
  - Scores by school type

## Summary 
Summarize four changes in the updated school district analysis after reading and math scores for the ninth grade at Thomas High School have been replaced with NaNs.
