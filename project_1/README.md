# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Project 1: Standardized Test Analysis

## Project 1: Standardized Test Analysis

### Details
Name: Wenna Loo Yan Ying

Class: DSIF-SG-1


### Problem Statement

As part of the team working in the college board, we have been tasked by the board to look at increasing SAT participation rates across the various states.

The problem of lower SAT test participation in comparison to our competitor the ACTs, has impacted our revenue.

Hence, a good starting point would be to look at the current SAT participation rate in comparison to ACTs. As well as, the current demographics and what pain points they are facing.

---

### Background

The SAT and ACT are standardized tests that many colleges and universities in the United States require for their admissions process. This score is used along with other materials such as grade point average (GPA) and essay responses to determine whether or not a potential student will be accepted to the university.

The SAT has two sections of the test: Evidence-Based Reading and Writing and Math ([*source*](https://www.princetonreview.com/college/sat-sections)). The ACT has 4 sections: English, Mathematics, Reading, and Science, with an additional optional writing section ([*source*](https://www.act.org/content/act/en/products-and-services/the-act/scores/understanding-your-scores.html)). They have different score ranges, which you can read more about on their websites or additional outside sources (a quick Google search will help you understand the scores for each test):
* [SAT](https://collegereadiness.collegeboard.org/sat)
* [ACT](https://www.act.org/content/act/en.html)

Standardized tests have long been a controversial topic for students, administrators, and legislators. Since the 1940's, an increasing number of colleges have been using scores from sudents' performances on tests like the SAT and the ACT as a measure for college readiness and aptitude ([*source*](https://www.minotdailynews.com/news/local-news/2017/04/a-brief-history-of-the-sat-and-act/)). Supporters of these tests argue that these scores can be used as an objective measure to determine college admittance. Opponents of these tests claim that these tests are not accurate measures of students potential or ability and serve as an inequitable barrier to entry. Lately, more and more schools are opting to drop the SAT/ACT requirement for their Fall 2021 applications ([*read more about this here*](https://www.cnn.com/2020/04/14/us/coronavirus-colleges-sat-act-test-trnd/index.html)).

---

### Datasets

#### Provided Data

The datasets used for analysis in project are:
* [`act_2017.csv`](./data/act_2017.csv): 2017 ACT Scores by State
* [`act_2018.csv`](./data/act_2018.csv): 2018 ACT Scores by State
* [`act_2019.csv`](./data/act_2019.csv): 2019 ACT Scores by State
* [`sat_2017.csv`](./data/sat_2017.csv): 2017 SAT Scores by State
* [`sat_2018.csv`](./data/sat_2018.csv): 2018 SAT Scores by State
* [`sat_2019.csv`](./data/sat_2019.csv): 2019 SAT Scores by State


The 2017-2019 ACT scores by state dataset contains 156 rows, and 8 columns. The data show the breakdown of average ACT scores by year, state, as well as the average in each subject area. The 2017-2019 SAT scores by state dataset contains 155 rows, and 8 columns. The data shows the breakdown of average SAT scores by year, state, as well as the average in each subject area.


#### Additional Data

Additional dataset used - to determine the profile of test takers:
* [`unemployment_income_by_states.xlsx`](./data/unemployment_income_by_states.xlsx): 2017 to 2019 Unemployment and Median Household Income by State [(source](https://www.ers.usda.gov/data-products/county-level-data-sets/download-data/), [source)](https://data.census.gov/cedsci/table?q=median%20income&g=0100000US.04000.001&tid=ACSST1Y2019.S1901&tp=true&hidePreview=true)

---

### Data Dictionary
|Feature|Type|Dataset|Description|
|---|---|---|---|
|**state**|*object*|2017-2019 ACT/SAT Scores by State|State name from which ACT/SAT data was collected| 
|**year**|*integer*|2017-2019 ACT/SAT Scores by State |Year of ACT/SAT taken| 
|**act_participation_rate**|*float*|2017-2019 ACT Scores by State |Participation rate for the ACT in each state| 
|**act_english_score**|*float*|2017-2019 ACT Scores by State |Average english score (Min: 1, Max: 36)|
|**act_math_score**|*float*|2017-2019 ACT Scores by State |Average math score (Min: 1, Max: 36)|
|**act_reading_score**|*float*|2017-2019 ACT Scores by State |Average reading score (Min: 1, Max:36)|
|**act_science_score**|*float*|2017-2019 ACT Scores by State |Average science score (Min: 1, Max:36)|
|**act_composite_score**|*float*|2017-2019 ACT Scores by State|Average total score derived as a composite of Math, Reading, English and Science scores (Min: 1, Max:36).| 
|**sat_participation_rate**|*float*|2017-2019 SAT Scores by State |Participation rate for the SAT in each state| 
|**sat_ebrw_score**|*integer*|2017-2019 SAT Scores by State |Average evidence-based reading and writing score (Min: 200, Max: 800)| 
|**sat_math_score**|*integer*|2017-2019 SAT Scores by State |Average math score (Min: 200, Max: 800)| 
|**sat_total_score**|*integer*|2017-2019 SAT Scores by State |Average total score (Min: 400, Max: 1600)| 
|**unemployment_rate**|*float*|2017-2019 Unemployment and Median Household Income by State|Unemployment rate in each state| 
|**median_household_income**|*integer*|2017-2019 Unemployment and Median Household Income by State|Estimate of median household income in each state| 


---

### Conclusions and Recommendations

#### Key Takeaways
* Nationwide, the ACT is preferred over the SAT.
* SAT participation rate and ACT participation rate has an inverse relationship.
* State education policies drastically affects participation rates among high school students in taking the ACT and SAT college entrance exams.
* SAT participation rate has a moderately positive relationship with the median household income.

#### Recommendations to improve the College Board's revenue
* Provide free test preparation materials and review lessons by partnering up with study platforms (eg. Khan academy).
* Lower the entry barrier for low-income students by offering testing fee waivers.
* Improve testing convenience by allowing remote arrangements to be made (eg. remote proctoring).
* Allow exam candidates to reschedule their examination date.
* Target states which have not made the SAT a mandatory high school graduation requirement.
* Collaborate with school districts on offering more SAT School Days.
* Team up with the states' education leaders to roll out college‐ and career‐readiness initiatives so that the students are more encouraged to think about their future.
* Provide college entry assistance to students who take the SAT exam.
