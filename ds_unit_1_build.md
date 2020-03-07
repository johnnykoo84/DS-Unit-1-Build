# How are Coding Bootcamp graduates valued in the field?
There are many arguments whether or not coding boocamps are worth it.
People debate a lot in the communities <a href="https://www.reddit.com/r/webdev/comments/6tcnt9/are_coding_bootcamps_worth_the_time_and_money/" target="_blank">reddit discussion link</a>  and it is hot issue among those who want to start their new professional software engineering career. 

I can talk about pros and cons of going to bootcamp here, but I won't do it because there are already <a href="https://careerkarma.com/blog/are-coding-bootcamps-worth-it/" target="_blank">many discussion out there</a>. 

In this article, I would instead talk about how much coding boocamp are valued in the field based on <a href="https://www.kaggle.com/mchirico/stack-overflow-developer-survey-results-2019" target="_blank">stackoverflow survey 2019</a> data.

There are some assumptions that I have to tell you. 

1. Not all coding bootcamp graduates probably got their job 100%, so this analysis would be fully based on those survey results by whom I belive that they got their job. Therefore, my argument is not focused on "Can you get a job through coding bootcamp?'.

2. There are no specific educational backgroudn group with labed as 'coding bootcamp' but there is one like 'Participated in a full-time developer training program or bootcamp'. Therefore I would like to consider the group as 'coding bootcamp' group since 9 years ago because wikipedia says the very first bootcamp was in 2001 in U.S.
3. I restricted the region to U.S. becasue the compensation is relative all over the world and did not want to go into market and exchange rate issue. 

## My Hypothesis
The bootcamp graduates are valued as equal as B.S. degree in Computer Science in the field

## Steps to validate my Hypothesis
1. EDA: let's explore the data
2. visualize data
3. analyze and see if my hypothesis is correct

## Step 1: EDA


```python
# imports
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```


```python
# Plotly imports
import plotly as py
import plotly.graph_objs as go
import plotly.express as px
```


```python
# original survey_data_2019.csv file size was 150Mb
# had to compress the size down to 50Mb with pickle format
df = pd.read_pickle('./survey_data_2019.pkl')
df_sch = pd.read_csv('./survey_results_schema.csv')
```


```python
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Respondent</th>
      <th>MainBranch</th>
      <th>Hobbyist</th>
      <th>OpenSourcer</th>
      <th>OpenSource</th>
      <th>Employment</th>
      <th>Country</th>
      <th>Student</th>
      <th>EdLevel</th>
      <th>UndergradMajor</th>
      <th>...</th>
      <th>WelcomeChange</th>
      <th>SONewContent</th>
      <th>Age</th>
      <th>Gender</th>
      <th>Trans</th>
      <th>Sexuality</th>
      <th>Ethnicity</th>
      <th>Dependents</th>
      <th>SurveyLength</th>
      <th>SurveyEase</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>1</td>
      <td>I am a student who is learning to code</td>
      <td>Yes</td>
      <td>Never</td>
      <td>The quality of OSS and closed source software ...</td>
      <td>Not employed, and not looking for work</td>
      <td>United Kingdom</td>
      <td>No</td>
      <td>Primary/elementary school</td>
      <td>NaN</td>
      <td>...</td>
      <td>Just as welcome now as I felt last year</td>
      <td>Tech articles written by other developers;Indu...</td>
      <td>14.0</td>
      <td>Man</td>
      <td>No</td>
      <td>Straight / Heterosexual</td>
      <td>NaN</td>
      <td>No</td>
      <td>Appropriate in length</td>
      <td>Neither easy nor difficult</td>
    </tr>
    <tr>
      <td>1</td>
      <td>2</td>
      <td>I am a student who is learning to code</td>
      <td>No</td>
      <td>Less than once per year</td>
      <td>The quality of OSS and closed source software ...</td>
      <td>Not employed, but looking for work</td>
      <td>Bosnia and Herzegovina</td>
      <td>Yes, full-time</td>
      <td>Secondary school (e.g. American high school, G...</td>
      <td>NaN</td>
      <td>...</td>
      <td>Just as welcome now as I felt last year</td>
      <td>Tech articles written by other developers;Indu...</td>
      <td>19.0</td>
      <td>Man</td>
      <td>No</td>
      <td>Straight / Heterosexual</td>
      <td>NaN</td>
      <td>No</td>
      <td>Appropriate in length</td>
      <td>Neither easy nor difficult</td>
    </tr>
    <tr>
      <td>2</td>
      <td>3</td>
      <td>I am not primarily a developer, but I write co...</td>
      <td>Yes</td>
      <td>Never</td>
      <td>The quality of OSS and closed source software ...</td>
      <td>Employed full-time</td>
      <td>Thailand</td>
      <td>No</td>
      <td>Bachelor’s degree (BA, BS, B.Eng., etc.)</td>
      <td>Web development or web design</td>
      <td>...</td>
      <td>Just as welcome now as I felt last year</td>
      <td>Tech meetups or events in your area;Courses on...</td>
      <td>28.0</td>
      <td>Man</td>
      <td>No</td>
      <td>Straight / Heterosexual</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Appropriate in length</td>
      <td>Neither easy nor difficult</td>
    </tr>
    <tr>
      <td>3</td>
      <td>4</td>
      <td>I am a developer by profession</td>
      <td>No</td>
      <td>Never</td>
      <td>The quality of OSS and closed source software ...</td>
      <td>Employed full-time</td>
      <td>United States</td>
      <td>No</td>
      <td>Bachelor’s degree (BA, BS, B.Eng., etc.)</td>
      <td>Computer science, computer engineering, or sof...</td>
      <td>...</td>
      <td>Just as welcome now as I felt last year</td>
      <td>Tech articles written by other developers;Indu...</td>
      <td>22.0</td>
      <td>Man</td>
      <td>No</td>
      <td>Straight / Heterosexual</td>
      <td>White or of European descent</td>
      <td>No</td>
      <td>Appropriate in length</td>
      <td>Easy</td>
    </tr>
    <tr>
      <td>4</td>
      <td>5</td>
      <td>I am a developer by profession</td>
      <td>Yes</td>
      <td>Once a month or more often</td>
      <td>OSS is, on average, of HIGHER quality than pro...</td>
      <td>Employed full-time</td>
      <td>Ukraine</td>
      <td>No</td>
      <td>Bachelor’s degree (BA, BS, B.Eng., etc.)</td>
      <td>Computer science, computer engineering, or sof...</td>
      <td>...</td>
      <td>Just as welcome now as I felt last year</td>
      <td>Tech meetups or events in your area;Courses on...</td>
      <td>30.0</td>
      <td>Man</td>
      <td>No</td>
      <td>Straight / Heterosexual</td>
      <td>White or of European descent;Multiracial</td>
      <td>No</td>
      <td>Appropriate in length</td>
      <td>Easy</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 85 columns</p>
</div>



The shape of the data is 88883 x 85


```python
df.shape
```




    (88883, 85)




```python
# let's see what each column survey question asks
pd.set_option('display.max_rows', df_sch.shape[0]+1)
print(df_sch)
```

    Column                                       QuestionText
    0               Respondent  Randomized respondent ID number (not in order ...
    1               MainBranch  Which of the following options best describes ...
    2                 Hobbyist                            Do you code as a hobby?
    3              OpenSourcer        How often do you contribute to open source?
    4               OpenSource  How do you feel about the quality of open sour...
    5               Employment  Which of the following best describes your cur...
    6                  Country          In which country do you currently reside?
    7                  Student  Are you currently enrolled in a formal, degree...
    8                  EdLevel  Which of the following best describes the high...
    9           UndergradMajor  What was your main or most important field of ...
    10                EduOther  Which of the following types of non-degree edu...
    11                 OrgSize  Approximately how many people are employed by ...
    12                 DevType  Which of the following describe you? Please se...
    13               YearsCode  Including any education, how many years have y...
    14              Age1stCode  At what age did you write your first line of c...
    15            YearsCodePro  How many years have you coded professionally (...
    16               CareerSat  Overall, how satisfied are you with your caree...
    17                  JobSat  How satisfied are you with your current job? (...
    18                MgrIdiot  How confident are you that your manager knows ...
    19                MgrMoney  Do you believe that you need to be a manager t...
    20                 MgrWant  Do you want to become a manager yourself in th...
    21                 JobSeek  Which of the following best describes your cur...
    22            LastHireDate  When was the last time that you took a job wit...
    23                 LastInt  In your most recent successful job interview (...
    24                FizzBuzz  Have you ever been asked to solve FizzBuzz in ...
    25              JobFactors  Imagine that you are deciding between two job ...
    26            ResumeUpdate  Think back to the last time you updated your r...
    27          CurrencySymbol  Which currency do you use day-to-day? If your ...
    28            CurrencyDesc  Which currency do you use day-to-day? If your ...
    29               CompTotal  What is your current total compensation (salar...
    30                CompFreq   Is that compensation weekly, monthly, or yearly?
    31           ConvertedComp  Salary converted to annual USD salaries using ...
    32             WorkWeekHrs   On average, how many hours per week do you work?
    33                WorkPlan            How structured or planned is your work?
    34           WorkChallenge  Of these options, what are your greatest chall...
    35              WorkRemote                    How often do you work remotely?
    36                 WorkLoc                    Where would you prefer to work?
    37                  ImpSyn  For the specific work you do, and the years of...
    38                 CodeRev           Do you review code as part of your work?
    39              CodeRevHrs  On average, how many hours per week do you spe...
    40               UnitTests  Does your company regularly employ unit tests ...
    41             PurchaseHow  How does your company make decisions about pur...
    42            PurchaseWhat  What level of influence do you, personally, ha...
    43      LanguageWorkedWith  Which of the following programming, scripting,...
    44  LanguageDesireNextYear  Which of the following programming, scripting,...
    45      DatabaseWorkedWith  Which of the following database environments h...
    46  DatabaseDesireNextYear  Which of the following database environments h...
    47      PlatformWorkedWith  Which of the following platforms have you done...
    48  PlatformDesireNextYear  Which of the following platforms have you done...
    49      WebFrameWorkedWith  Which of the following web frameworks have you...
    50  WebFrameDesireNextYear  Which of the following web frameworks have you...
    51      MiscTechWorkedWith  Which of the following other frameworks, libra...
    52  MiscTechDesireNextYear  Which of the following other frameworks, libra...
    53              DevEnviron  Which development environment(s) do you use re...
    54                   OpSys  What is the primary operating system in which ...
    55              Containers  How do you use containers (Docker, Open Contai...
    56           BlockchainOrg  How is your organization thinking about or imp...
    57            BlockchainIs  Blockchain / cryptocurrency technology is prim...
    58              BetterLife  Do you think people born today will have a bet...
    59                ITperson   Are you the "IT support person" for your family?
    60                   OffOn        Have you tried turning it off and on again?
    61             SocialMedia        What social media site do you use the most?
    62            Extraversion    Do you prefer online chat or IRL conversations?
    63              ScreenName                               What do you call it?
    64              SOVisit1st  To the best of your memory, when did you first...
    65             SOVisitFreq  How frequently would you say you visit Stack O...
    66               SOVisitTo  I visit Stack Overflow to... (check all that a...
    67            SOFindAnswer  On average, how many times a week do you find ...
    68             SOTimeSaved  Think back to the last time you solved a codin...
    69           SOHowMuchTime  About how much time did you save? If you're no...
    70               SOAccount              Do you have a Stack Overflow account?
    71              SOPartFreq  How frequently would you say you participate i...
    72                  SOJobs  Have you ever used or visited Stack Overflow J...
    73                EntTeams  Have you ever used Stack Overflow for Enterpri...
    74                  SOComm  Do you consider yourself a member of the Stack...
    75           WelcomeChange  Compared to last year, how welcome do you feel...
    76            SONewContent  Would you like to see any of the following on ...
    77                     Age  What is your age (in years)? If you prefer not...
    78                  Gender  Which of the following do you currently identi...
    79                   Trans                    Do you identify as transgender?
    80               Sexuality  Which of the following do you currently identi...
    81               Ethnicity  Which of the following do you identify as? Ple...
    82              Dependents  Do you have any dependents (e.g., children, el...
    83            SurveyLength  How do you feel about the length of the survey...
    84              SurveyEase  How easy or difficult was this survey to compl...


# 


```python
# types of each column
df.dtypes
```




    Respondent                  int64
    MainBranch                 object
    Hobbyist                   object
    OpenSourcer                object
    OpenSource                 object
    Employment                 object
    Country                    object
    Student                    object
    EdLevel                    object
    UndergradMajor             object
    EduOther                   object
    OrgSize                    object
    DevType                    object
    YearsCode                  object
    Age1stCode                 object
    YearsCodePro               object
    CareerSat                  object
    JobSat                     object
    MgrIdiot                   object
    MgrMoney                   object
    MgrWant                    object
    JobSeek                    object
    LastHireDate               object
    LastInt                    object
    FizzBuzz                   object
    JobFactors                 object
    ResumeUpdate               object
    CurrencySymbol             object
    CurrencyDesc               object
    CompTotal                 float64
    CompFreq                   object
    ConvertedComp             float64
    WorkWeekHrs               float64
    WorkPlan                   object
    WorkChallenge              object
    WorkRemote                 object
    WorkLoc                    object
    ImpSyn                     object
    CodeRev                    object
    CodeRevHrs                float64
    UnitTests                  object
    PurchaseHow                object
    PurchaseWhat               object
    LanguageWorkedWith         object
    LanguageDesireNextYear     object
    DatabaseWorkedWith         object
    DatabaseDesireNextYear     object
    PlatformWorkedWith         object
    PlatformDesireNextYear     object
    WebFrameWorkedWith         object
    WebFrameDesireNextYear     object
    MiscTechWorkedWith         object
    MiscTechDesireNextYear     object
    DevEnviron                 object
    OpSys                      object
    Containers                 object
    BlockchainOrg              object
    BlockchainIs               object
    BetterLife                 object
    ITperson                   object
    OffOn                      object
    SocialMedia                object
    Extraversion               object
    ScreenName                 object
    SOVisit1st                 object
    SOVisitFreq                object
    SOVisitTo                  object
    SOFindAnswer               object
    SOTimeSaved                object
    SOHowMuchTime              object
    SOAccount                  object
    SOPartFreq                 object
    SOJobs                     object
    EntTeams                   object
    SOComm                     object
    WelcomeChange              object
    SONewContent               object
    Age                       float64
    Gender                     object
    Trans                      object
    Sexuality                  object
    Ethnicity                  object
    Dependents                 object
    SurveyLength               object
    SurveyEase                 object
    dtype: object




```python
# what are the numeric answers?
df.select_dtypes(include=np.number).columns.tolist()
```




    ['Respondent',
     'CompTotal',
     'ConvertedComp',
     'WorkWeekHrs',
     'CodeRevHrs',
     'Age']




```python
# Are there null values?
df.isna().sum()
```




    Respondent                    0
    MainBranch                  552
    Hobbyist                      0
    OpenSourcer                   0
    OpenSource                 2041
    Employment                 1702
    Country                     132
    Student                    1869
    EdLevel                    2493
    UndergradMajor            13269
    EduOther                   4623
    OrgSize                   17092
    DevType                    7548
    YearsCode                   945
    Age1stCode                 1249
    YearsCodePro              14552
    CareerSat                 16036
    JobSat                    17895
    MgrIdiot                  27724
    MgrMoney                  27726
    MgrWant                   27651
    JobSeek                    8328
    LastHireDate               9029
    LastInt                   21728
    FizzBuzz                  17539
    JobFactors                 9512
    ResumeUpdate              11006
    CurrencySymbol            17491
    CurrencyDesc              17491
    CompTotal                 32938
    CompFreq                  25615
    ConvertedComp             33060
    WorkWeekHrs               24380
    WorkPlan                  19969
    WorkChallenge             20742
    WorkRemote                18599
    WorkLoc                   18828
    ImpSyn                    17104
    CodeRev                   18493
    CodeRevHrs                39093
    UnitTests                 26215
    PurchaseHow               27775
    PurchaseWhat              26854
    LanguageWorkedWith         1314
    LanguageDesireNextYear     4795
    DatabaseWorkedWith        12857
    DatabaseDesireNextYear    19736
    PlatformWorkedWith         8169
    PlatformDesireNextYear    11440
    WebFrameWorkedWith        23861
    WebFrameDesireNextYear    25939
    MiscTechWorkedWith        29297
    MiscTechDesireNextYear    24372
    DevEnviron                 1566
    OpSys                      1032
    Containers                 3517
    BlockchainOrg             40708
    BlockchainIs              28718
    BetterLife                 2614
    ITperson                   1742
    OffOn                      2220
    SocialMedia                4446
    Extraversion               1578
    ScreenName                 8397
    SOVisit1st                 5006
    SOVisitFreq                 620
    SOVisitTo                   797
    SOFindAnswer               1067
    SOTimeSaved                2539
    SOHowMuchTime             20505
    SOAccount                  1055
    SOPartFreq                14191
    SOJobs                      817
    EntTeams                   1042
    SOComm                      752
    WelcomeChange              3028
    SONewContent              19323
    Age                        9673
    Gender                     3477
    Trans                      5276
    Sexuality                 12736
    Ethnicity                 12215
    Dependents                 5824
    SurveyLength               1899
    SurveyEase                 1802
    dtype: int64




```python
# let's see if I can filter out non-numeric columns from df
df_obj = df.select_dtypes(['object'])
print(df_obj.dtypes)
```

    MainBranch                object
    Hobbyist                  object
    OpenSourcer               object
    OpenSource                object
    Employment                object
    Country                   object
    Student                   object
    EdLevel                   object
    UndergradMajor            object
    EduOther                  object
    OrgSize                   object
    DevType                   object
    YearsCode                 object
    Age1stCode                object
    YearsCodePro              object
    CareerSat                 object
    JobSat                    object
    MgrIdiot                  object
    MgrMoney                  object
    MgrWant                   object
    JobSeek                   object
    LastHireDate              object
    LastInt                   object
    FizzBuzz                  object
    JobFactors                object
    ResumeUpdate              object
    CurrencySymbol            object
    CurrencyDesc              object
    CompFreq                  object
    WorkPlan                  object
    WorkChallenge             object
    WorkRemote                object
    WorkLoc                   object
    ImpSyn                    object
    CodeRev                   object
    UnitTests                 object
    PurchaseHow               object
    PurchaseWhat              object
    LanguageWorkedWith        object
    LanguageDesireNextYear    object
    DatabaseWorkedWith        object
    DatabaseDesireNextYear    object
    PlatformWorkedWith        object
    PlatformDesireNextYear    object
    WebFrameWorkedWith        object
    WebFrameDesireNextYear    object
    MiscTechWorkedWith        object
    MiscTechDesireNextYear    object
    DevEnviron                object
    OpSys                     object
    Containers                object
    BlockchainOrg             object
    BlockchainIs              object
    BetterLife                object
    ITperson                  object
    OffOn                     object
    SocialMedia               object
    Extraversion              object
    ScreenName                object
    SOVisit1st                object
    SOVisitFreq               object
    SOVisitTo                 object
    SOFindAnswer              object
    SOTimeSaved               object
    SOHowMuchTime             object
    SOAccount                 object
    SOPartFreq                object
    SOJobs                    object
    EntTeams                  object
    SOComm                    object
    WelcomeChange             object
    SONewContent              object
    Gender                    object
    Trans                     object
    Sexuality                 object
    Ethnicity                 object
    Dependents                object
    SurveyLength              object
    SurveyEase                object
    dtype: object



```python
# let's filter out numeric columns
df_num = df.select_dtypes(np.number)
print(df_num.shape)
print(df_num.dtypes)
```

    (88883, 6)
    Respondent         int64
    CompTotal        float64
    ConvertedComp    float64
    WorkWeekHrs      float64
    CodeRevHrs       float64
    Age              float64
    dtype: object


## Startegy
In order to validate my hypothesis, I would like to compare Salaries for two different gropus. 
1. B.S. degree in Computer Science or similar computer related study
2. Coding Bootcamp graduates

Stackoverflow gives two columns, one with 'EdLevel' where I can figure who got B.S. degree in computer science or similar. 


```python
# see if EdLevel has null values
df['EdLevel'].isna().sum()
```




    2493




```python
# see how the value counts for each categorical value
df['EdLevel'].value_counts()
```




    Bachelor’s degree (BA, BS, B.Eng., etc.)                                              39134
    Master’s degree (MA, MS, M.Eng., MBA, etc.)                                           19569
    Some college/university study without earning a degree                                10502
    Secondary school (e.g. American high school, German Realschule or Gymnasium, etc.)     8642
    Associate degree                                                                       2938
    Other doctoral degree (Ph.D, Ed.D., etc.)                                              2432
    Primary/elementary school                                                              1422
    Professional degree (JD, MD, etc.)                                                     1198
    I never completed any formal education                                                  553
    Name: EdLevel, dtype: int64




```python
# let's visualize education level
data = go.Histogram(
    y=df['EdLevel'],
    histnorm='percent'
    )
fig = go.Figure(data=[data])
fig.update_layout(
    title_text='Education Level', # title of plot
    xaxis_title_text='Counts', # xaxis label
    yaxis_title_text='Ed Level', # yaxis label
    bargap=0.2, # gap between bars of adjacent location coordinates
    bargroupgap=0.1 # gap between bars of the same location coordinates
)
fig.update_yaxes(automargin=True)
fig.show()
```




```python
# let's define df for only United States Country respondent
df_us = df[df['Country'] == 'United States']
```


```python
df_us['EdLevel'].value_counts()
```




    Bachelor’s degree (BA, BS, B.Eng., etc.)                                              10953
    Master’s degree (MA, MS, M.Eng., MBA, etc.)                                            3585
    Some college/university study without earning a degree                                 2779
    Secondary school (e.g. American high school, German Realschule or Gymnasium, etc.)     1113
    Associate degree                                                                        977
    Other doctoral degree (Ph.D, Ed.D., etc.)                                               673
    Primary/elementary school                                                               310
    Professional degree (JD, MD, etc.)                                                      119
    I never completed any formal education                                                   96
    Name: EdLevel, dtype: int64




```python
# Salary with education levels
print('salary median for B.S. degree in all majors\n', df_us.groupby(['EdLevel'])['ConvertedComp'].median())
str_bs_ed_level = 'Bachelor’s degree (BA, BS, B.Eng., etc.)'
```

    salary median for B.S. degree in all majors
     EdLevel
    Associate degree                                                                       90000.0
    Bachelor’s degree (BA, BS, B.Eng., etc.)                                              110000.0
    I never completed any formal education                                                123500.0
    Master’s degree (MA, MS, M.Eng., MBA, etc.)                                           125000.0
    Other doctoral degree (Ph.D, Ed.D., etc.)                                             140000.0
    Primary/elementary school                                                             120000.0
    Professional degree (JD, MD, etc.)                                                    106500.0
    Secondary school (e.g. American high school, German Realschule or Gymnasium, etc.)     95000.0
    Some college/university study without earning a degree                                107000.0
    Name: ConvertedComp, dtype: float64


## result
B.S. undergraduate degree salary median is 110,000 USD.
However, I think I need to filter only C.S. or similar degree here. That way, I expect to get higher median value. Another way to say is that I assum non-CS major in SW engieering field will have lower salary. 


```python
# what majors do i have
df_us['UndergradMajor'].value_counts()
```




    Computer science, computer engineering, or software engineering          10747
    Another engineering discipline (ex. civil, electrical, mechanical)        1344
    Information systems, information technology, or system administration     1186
    A natural science (ex. biology, chemistry, physics)                        961
    Mathematics or statistics                                                  895
    A humanities discipline (ex. literature, history, philosophy)              718
    A social science (ex. anthropology, psychology, political science)         695
    Fine arts or performing arts (ex. graphic design, music, studio art)       667
    A business discipline (ex. accounting, finance, marketing)                 615
    Web development or web design                                              493
    I never declared a major                                                   345
    A health science (ex. nursing, pharmacy, radiology)                         87
    Name: UndergradMajor, dtype: int64




```python
# get the string for C.S or similar major
str_cs_degree = df_us['UndergradMajor'].iloc[3733]
str_cs_degree
```




    'Computer science, computer engineering, or software engineering'




```python
# Salary with education levels specifically CS major
condition_bs_degree = df_us['EdLevel'] == str_bs_ed_level
condition_cs_bs_major = condition_bs_degree & (df_us['UndergradMajor'] == str_cs_degree)

# there is something wrong with 10953 because number of bs degree cannot be number of cs undergrad major
# I need to show that b.s. degree filter has all majors
print('number of people who has B.S. degree in all majors\n', df_us[condition_bs_degree]['EdLevel'].value_counts())
print('number of people who has B.S. degree in computer science or similar\n', df_us[condition_cs_bs_major]['EdLevel'].value_counts())
print('salary median for people with B.S. degree in C.S and their education level is B.S.\n', df_us[condition_cs_bs_major].groupby(['EdLevel'])['ConvertedComp'].median())
```

    number of people who has B.S. degree in all majors
     Bachelor’s degree (BA, BS, B.Eng., etc.)    10953
    Name: EdLevel, dtype: int64
    number of people who has B.S. degree in computer science or similar
     Bachelor’s degree (BA, BS, B.Eng., etc.)    6449
    Name: EdLevel, dtype: int64
    salary median for people with B.S. degree in C.S and their education level is B.S.
     EdLevel
    Bachelor’s degree (BA, BS, B.Eng., etc.)    110250.0
    Name: ConvertedComp, dtype: float64


## result
The median value for C.S. or similar undergraduate B.S. degree is more or less the same than overal B.S. degree people. Therefore, my assumption that 'C.S. degree median salary will be higher' is wrong.


```python
# here we have to update years of coding as pforessional column string values to integere values
df_us['YearsCodePro'] = df_us['YearsCodePro'].apply(lambda x: 0.5 if x == 'Less than 1 year' else (50 if x == 'More than 50 years' else x))
```


```python
df_us['YearsCodePro'].sample(20)
```




    81473      1
    56714      7
    71342    NaN
    19982      1
    10991      1
    86387     23
    75534      2
    17647     17
    66701     10
    42384    0.5
    77301    NaN
    30337    NaN
    62335     20
    18719      1
    48194      5
    46498     18
    26382      3
    74167    0.5
    32180    NaN
    77322      4
    Name: YearsCodePro, dtype: object




```python
# I'm not sure why but below astype cannot take care of NaN
# df_us['YearsCodePro'] = df_us['YearsCodePro'].astype(int) 
df_us['YearsCodePro'] = pd.to_numeric(df_us['YearsCodePro'])
```


```python
# see if the type updated
df_us['YearsCodePro'].dtypes
```




    dtype('float64')




```python
edu_level = df_us.pivot_table(
    index = 'EdLevel',
    columns='YearsCodePro',
    values='ConvertedComp',
    aggfunc={
        'ConvertedComp': np.median
        }
    )
bs_degree = edu_level[edu_level.index == str_bs_ed_level]
bs_degree
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>YearsCodePro</th>
      <th>0.5</th>
      <th>1.0</th>
      <th>2.0</th>
      <th>3.0</th>
      <th>4.0</th>
      <th>5.0</th>
      <th>6.0</th>
      <th>7.0</th>
      <th>8.0</th>
      <th>9.0</th>
      <th>...</th>
      <th>40.0</th>
      <th>41.0</th>
      <th>42.0</th>
      <th>43.0</th>
      <th>44.0</th>
      <th>45.0</th>
      <th>47.0</th>
      <th>48.0</th>
      <th>49.0</th>
      <th>50.0</th>
    </tr>
    <tr>
      <th>EdLevel</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Bachelor’s degree (BA, BS, B.Eng., etc.)</td>
      <td>70700.0</td>
      <td>75000.0</td>
      <td>81000.0</td>
      <td>90000.0</td>
      <td>95000.0</td>
      <td>101000.0</td>
      <td>106000.0</td>
      <td>111000.0</td>
      <td>120000.0</td>
      <td>130000.0</td>
      <td>...</td>
      <td>132500.0</td>
      <td>133400.0</td>
      <td>125000.0</td>
      <td>92000.0</td>
      <td>115000.0</td>
      <td>180000.0</td>
      <td>145000.0</td>
      <td>157500.0</td>
      <td>176000.0</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>1 rows × 50 columns</p>
</div>




```python
edu_level = df_us[condition_cs_bs_major].pivot_table(
    index = 'EdLevel',
    columns='YearsCodePro',
    values='ConvertedComp',
    aggfunc={
        'ConvertedComp': np.median
        }
    )
bs_cs_degree = edu_level[edu_level.index == str_bs_ed_level]
bs_cs_degree
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>YearsCodePro</th>
      <th>0.5</th>
      <th>1.0</th>
      <th>2.0</th>
      <th>3.0</th>
      <th>4.0</th>
      <th>5.0</th>
      <th>6.0</th>
      <th>7.0</th>
      <th>8.0</th>
      <th>9.0</th>
      <th>...</th>
      <th>37.0</th>
      <th>38.0</th>
      <th>39.0</th>
      <th>40.0</th>
      <th>41.0</th>
      <th>42.0</th>
      <th>43.0</th>
      <th>44.0</th>
      <th>45.0</th>
      <th>47.0</th>
    </tr>
    <tr>
      <th>EdLevel</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Bachelor’s degree (BA, BS, B.Eng., etc.)</td>
      <td>72900.0</td>
      <td>75000.0</td>
      <td>82000.0</td>
      <td>90000.0</td>
      <td>95000.0</td>
      <td>105000.0</td>
      <td>105000.0</td>
      <td>114500.0</td>
      <td>130000.0</td>
      <td>130000.0</td>
      <td>...</td>
      <td>123500.0</td>
      <td>145000.0</td>
      <td>150000.0</td>
      <td>155000.0</td>
      <td>133400.0</td>
      <td>90000.0</td>
      <td>91000.0</td>
      <td>115000.0</td>
      <td>180000.0</td>
      <td>220000.0</td>
    </tr>
  </tbody>
</table>
<p>1 rows × 47 columns</p>
</div>




```python
edu_other = df_us.pivot_table(
    index = 'EduOther',
    columns='YearsCodePro',
    values='ConvertedComp',
    aggfunc={
        'ConvertedComp': np.median
        }
    )
# bootcamp.shape
bootcamp_graduate = edu_other[bootcamp.index == 'Participated in a full-time developer training program or bootcamp']
bootcamp_graduate
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>YearsCodePro</th>
      <th>0.5</th>
      <th>1.0</th>
      <th>2.0</th>
      <th>3.0</th>
      <th>4.0</th>
      <th>5.0</th>
      <th>6.0</th>
      <th>7.0</th>
      <th>8.0</th>
      <th>9.0</th>
      <th>...</th>
      <th>40.0</th>
      <th>41.0</th>
      <th>42.0</th>
      <th>43.0</th>
      <th>44.0</th>
      <th>45.0</th>
      <th>47.0</th>
      <th>48.0</th>
      <th>49.0</th>
      <th>50.0</th>
    </tr>
    <tr>
      <th>EduOther</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Participated in a full-time developer training program or bootcamp</td>
      <td>68000.0</td>
      <td>71000.0</td>
      <td>83750.0</td>
      <td>88500.0</td>
      <td>87000.0</td>
      <td>112000.0</td>
      <td>567500.0</td>
      <td>NaN</td>
      <td>65000.0</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>1 rows × 50 columns</p>
</div>




```python
years_code_pro = bootcamp.columns.tolist()

fig = go.Figure(
    data=[
        go.Bar(name='B.S in Computer Science', x=years_code_pro, y=bs_degree_cs.values.tolist()[0]),
        go.Bar(name='Bootcamp Graduates', x=years_code_pro, y=bootcamp_graduate.values.tolist()[0])
    ]
)
# Change the bar mode
fig.update_layout(
    title='Salary Comparison between CS degree and Bootcamp',
    xaxis_title='number of years of professional coding',
    yaxis_title='Salaray(median) in dollars',
    barmode='group'
    )
fig.show()
```



# Plot Result
I have an insane salary median peak for bootcamp graduate at 6 years of professional coding expereience. I am very skeptical about it. This can't be right unless someone went to coding bootcamp years ago and he or she quickly went IPO and somehow he or she submitted stackoverflow survey. Also, there should not many people in that condition unless otherwise the insane peak cannot be shown. Therefore, let's investigate what's going on here.   


```python
# we will find if the 6 years of pro coding exp people really have insane median peak here
condition_4 = (df['EduOther'] == str_bootcamp_graduate)
bootcamp_grad_salary = df_us[condition_4]['ConvertedComp']
bootcamp_grad_years = df_us[condition_4]['YearsCodePro']
bootcamp_grad_comp_per_years_med = df_us[condition_4].groupby(['YearsCodePro'])['ConvertedComp'].median()
condition_5 = condition_4 & (df_us['YearsCodePro'] == 6)
bootcamp_grad_with_6_yrs = df_us[condition_5]['ConvertedComp']
print(bootcamp_grad_with_6_yrs)
```

    67663    1000000.0
    73526     135000.0
    Name: ConvertedComp, dtype: float64


## Investigation Result
we found that index 67663 gave 1,000,000 for his convertedComp, salary
which is either a additional digit mistake or on purpose
1. fix digit
2. drop the row

Let's fix the digit assuming the respondent had a typo.


```python
# let's fix the digit typo
df_us.set_value(67663, 'ConvertedComp', 100000)
print('is it fixed?', df_us[df_us.index == 67663]['ConvertedComp'])
```

    is it fixed? 67663    100000.0
    Name: ConvertedComp, dtype: float64



```python
# let's plot it again with fixed typo
edu_level = df_us[condition_cs_bs_major].pivot_table(
    index = 'EdLevel',
    columns='YearsCodePro',
    values='ConvertedComp',
    aggfunc={
        'ConvertedComp': np.median
        }
    )
edu_other = df_us.pivot_table(
    index = 'EduOther',
    columns='YearsCodePro',
    values='ConvertedComp',
    aggfunc={
        'ConvertedComp': np.median
        }
    )
bs_cs_degree = edu_level[edu_level.index == str_bs_ed_level]
bootcamp_graduate = edu_other[bootcamp.index == 'Participated in a full-time developer training program or bootcamp']

years_code_pro = bootcamp.columns.tolist()

fig = go.Figure(
    data=[
        go.Bar(name='B.S in Computer Science', x=years_code_pro, y=bs_degree_cs.values.tolist()[0]),
        go.Bar(name='Bootcamp Graduates', x=years_code_pro, y=bootcamp_graduate.values.tolist()[0])
    ]
)
# Change the bar mode
fig.update_layout(
    xaxis=dict(range=[0, 10], dtick=1),
    title='Salary Comparison between CS degree and Bootcamp',
    xaxis_title='number of years of professional coding',
    yaxis_title='Salaray(median) in dollars',
    barmode='group'
    )
fig.show()
```



## Plot
plot is now updatedd with fixed data.
I trimmed years of coding prefossional down to 10 years max because according to wiki it says the coding bootcamp has been for 9 years. 


# Final Analysis
My hypothesis was
The bootcamp graduates are valued as equal as B.S. degree in Computer Science in the field

I think i came up with reasonable data which supports my hypothesis because the first 6 years of professional career years, the salary medians are pretty close each other. For range from 5 to 6 years, coding bootcamp graduates were even more valued in the field.

Of course, I think we need more years to validate this idea because coding bootcamp graduates gorup is a lot less in terms of number of people in the group. 




```python
# condition for B.S. in computer science or similar major in U.S
cond_cs_mjr = df_us['UndergradMajor'] == str_cs_degree
cond_bs_dgr = df_us['EdLevel'] == str_bs_ed_level
cond_less_3_yrs = df_us['YearsCodePro'] < 3
cond_more_3_yrs = (df_us['YearsCodePro'] >= 3) & df_us['YearsCodePro'] <= 9

result_bs_cs_less_3 = df_us[cond_cs_mjr & cond_bs_dgr & cond_less_3_yrs].groupby(['EdLevel'])['ConvertedComp'].median()
result_bs_cs_more_3 = df_us[cond_cs_mjr & cond_bs_dgr & cond_more_3_yrs].groupby(['EdLevel'])['ConvertedComp'].median()
print('Compensation with B.S. in CS with less than 3 years of professional coding expereince\n', result_less_3)
print('Compensation with B.S. in CS with more than 3 years of professional coding expereince\n', result_more_3)
```

    Compensation with B.S. in CS with less than 3 years of professional coding expereince
     EdLevel
    Bachelor’s degree (BA, BS, B.Eng., etc.)    77250.0
    Name: ConvertedComp, dtype: float64
    Compensation with B.S. in CS with more than 3 years of professional coding expereince
     EdLevel
    Bachelor’s degree (BA, BS, B.Eng., etc.)    115500.0
    Name: ConvertedComp, dtype: float64



```python
# I need to show exact median values for B.S. degree vs I never completed formal education
str_bootcamp_graduate = 'Participated in a full-time developer training program or bootcamp'

condition_1 = df['EduOther'] == str_bootcamp_graduate
bootcamp_grad_comp = df_us[condition_1].groupby(['EduOther'])['ConvertedComp'].median()

condition_2 = condition_1 & (df_us['YearsCodePro'] <= 3)
result_bootcamp_grad_three_years_less_exp_comp = df_us[condition_2].groupby(['EduOther'])['ConvertedComp'].median()

condition_3 = condition_1 & (df_us['YearsCodePro'] >= 3)
result_bootcamp_grad_three_years_more_exp_comp = df_us[condition_3].groupby(['EduOther'])['ConvertedComp'].median()

print('boot camp grad compensation\n', bootcamp_grad_comp)
print('\n')
print('boot camp grad with less than 3 years of professional coding expereince compensation\n', result_bootcamp_grad_three_years_less_exp_comp)
print('\n')
print('boot camp grad with more than 3 years of professional coding expereince compensation\n', result_bootcamp_grad_three_years_more_exp_comp)
```

    boot camp grad compensation
     EduOther
    Participated in a full-time developer training program or bootcamp    84375.0
    Name: ConvertedComp, dtype: float64
    
    
    boot camp grad with less than 3 years of professional coding expereince compensation
     EduOther
    Participated in a full-time developer training program or bootcamp    80000.0
    Name: ConvertedComp, dtype: float64
    
    
    boot camp grad with more than 3 years of professional coding expereince compensation
     EduOther
    Participated in a full-time developer training program or bootcamp    91500.0
    Name: ConvertedComp, dtype: float64

