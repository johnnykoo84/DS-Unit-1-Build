# DS Unit 01 Build
## DSPT5 Ilmo Koo


Dataset: Stack Overflow Developer Survey Results 2019


```python
# imports
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```


```python
# Plotly imports
import plotly
import plotly.graph_objs as go
import plotly.express as px
```


```python
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




```python
df.iloc[0]
```




    Respondent                                                      1
    MainBranch                 I am a student who is learning to code
    Hobbyist                                                      Yes
    OpenSourcer                                                 Never
    OpenSource      The quality of OSS and closed source software ...
                                          ...                        
    Sexuality                                 Straight / Heterosexual
    Ethnicity                                                     NaN
    Dependents                                                     No
    SurveyLength                                Appropriate in length
    SurveyEase                             Neither easy nor difficult
    Name: 0, Length: 85, dtype: object




```python
# let's see what each column means
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


# choice and concentration
There are 85 columns and it is necessary to focus a few of them
I might add and analyze more data, but for now let's pick maybe a couple
Let's keep it simple (LEAN)

## Prior to EDA
There are a few assumptions/stoires that I want to validate from the data. 
I am not sure which to pick and analyze but let's brainstrom them first.

1. Are bootcamp graduates doing well in the field?
2. B.S or higher of C.S. degree really matter in terms of salary?
3. 

# 


```python
df.shape
```




    (88883, 85)




```python
df_sch.shape
```




    (85, 2)




```python
df.describe()
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
      <th>CompTotal</th>
      <th>ConvertedComp</th>
      <th>WorkWeekHrs</th>
      <th>CodeRevHrs</th>
      <th>Age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>count</td>
      <td>88883.000000</td>
      <td>5.594500e+04</td>
      <td>5.582300e+04</td>
      <td>64503.000000</td>
      <td>49790.000000</td>
      <td>79210.000000</td>
    </tr>
    <tr>
      <td>mean</td>
      <td>44442.000000</td>
      <td>5.519014e+11</td>
      <td>1.271107e+05</td>
      <td>42.127197</td>
      <td>5.084308</td>
      <td>30.336699</td>
    </tr>
    <tr>
      <td>std</td>
      <td>25658.456325</td>
      <td>7.331926e+13</td>
      <td>2.841523e+05</td>
      <td>37.287610</td>
      <td>5.513931</td>
      <td>9.178390</td>
    </tr>
    <tr>
      <td>min</td>
      <td>1.000000</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <td>25%</td>
      <td>22221.500000</td>
      <td>2.000000e+04</td>
      <td>2.577750e+04</td>
      <td>40.000000</td>
      <td>2.000000</td>
      <td>24.000000</td>
    </tr>
    <tr>
      <td>50%</td>
      <td>44442.000000</td>
      <td>6.200000e+04</td>
      <td>5.728700e+04</td>
      <td>40.000000</td>
      <td>4.000000</td>
      <td>29.000000</td>
    </tr>
    <tr>
      <td>75%</td>
      <td>66662.500000</td>
      <td>1.200000e+05</td>
      <td>1.000000e+05</td>
      <td>44.750000</td>
      <td>6.000000</td>
      <td>35.000000</td>
    </tr>
    <tr>
      <td>max</td>
      <td>88883.000000</td>
      <td>1.000000e+16</td>
      <td>2.000000e+06</td>
      <td>4850.000000</td>
      <td>99.000000</td>
      <td>99.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
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
df.select_dtypes(include=np.number).columns.tolist()

```




    ['Respondent',
     'CompTotal',
     'ConvertedComp',
     'WorkWeekHrs',
     'CodeRevHrs',
     'Age']




```python
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
print(df_obj.shape)
print(df_obj.dtypes)
```

    (88883, 79)
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



```python
df_num_corr = df_num.corr()
df_num_corr
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
      <th>CompTotal</th>
      <th>ConvertedComp</th>
      <th>WorkWeekHrs</th>
      <th>CodeRevHrs</th>
      <th>Age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Respondent</td>
      <td>1.000000</td>
      <td>-0.003357</td>
      <td>0.002930</td>
      <td>-0.004589</td>
      <td>-0.005240</td>
      <td>-0.001829</td>
    </tr>
    <tr>
      <td>CompTotal</td>
      <td>-0.003357</td>
      <td>1.000000</td>
      <td>0.039725</td>
      <td>0.003074</td>
      <td>0.061090</td>
      <td>0.016500</td>
    </tr>
    <tr>
      <td>ConvertedComp</td>
      <td>0.002930</td>
      <td>0.039725</td>
      <td>1.000000</td>
      <td>0.013908</td>
      <td>-0.021261</td>
      <td>0.108268</td>
    </tr>
    <tr>
      <td>WorkWeekHrs</td>
      <td>-0.004589</td>
      <td>0.003074</td>
      <td>0.013908</td>
      <td>1.000000</td>
      <td>0.021092</td>
      <td>0.019976</td>
    </tr>
    <tr>
      <td>CodeRevHrs</td>
      <td>-0.005240</td>
      <td>0.061090</td>
      <td>-0.021261</td>
      <td>0.021092</td>
      <td>1.000000</td>
      <td>-0.022486</td>
    </tr>
    <tr>
      <td>Age</td>
      <td>-0.001829</td>
      <td>0.016500</td>
      <td>0.108268</td>
      <td>0.019976</td>
      <td>-0.022486</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
sns.heatmap(df_num_corr,
cmap='RdBu_r',
annot=True,
linewidth=0.5)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a212ccb10>




![svg](ds_unit_1_build_files/ds_unit_1_build_19_1.svg)



```python
pd.crosstab(df['EdLevel'], df['EduOther'])
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
      <th>EduOther</th>
      <th>Completed an industry certification program (e.g. MCPD)</th>
      <th>Completed an industry certification program (e.g. MCPD);Contributed to open source software</th>
      <th>Completed an industry certification program (e.g. MCPD);Participated in a hackathon</th>
      <th>Completed an industry certification program (e.g. MCPD);Participated in a hackathon;Contributed to open source software</th>
      <th>Completed an industry certification program (e.g. MCPD);Participated in online coding competitions (e.g. HackerRank, CodeChef, TopCoder)</th>
      <th>Completed an industry certification program (e.g. MCPD);Participated in online coding competitions (e.g. HackerRank, CodeChef, TopCoder);Contributed to open source software</th>
      <th>Completed an industry certification program (e.g. MCPD);Participated in online coding competitions (e.g. HackerRank, CodeChef, TopCoder);Participated in a hackathon</th>
      <th>Completed an industry certification program (e.g. MCPD);Participated in online coding competitions (e.g. HackerRank, CodeChef, TopCoder);Participated in a hackathon;Contributed to open source software</th>
      <th>Completed an industry certification program (e.g. MCPD);Received on-the-job training in software development</th>
      <th>Completed an industry certification program (e.g. MCPD);Received on-the-job training in software development;Contributed to open source software</th>
      <th>...</th>
      <th>Taken an online course in programming or software development (e.g. a MOOC);Taught yourself a new language, framework, or tool without taking a formal course;Participated in online coding competitions (e.g. HackerRank, CodeChef, TopCoder);Participated in a hackathon</th>
      <th>Taken an online course in programming or software development (e.g. a MOOC);Taught yourself a new language, framework, or tool without taking a formal course;Participated in online coding competitions (e.g. HackerRank, CodeChef, TopCoder);Participated in a hackathon;Contributed to open source software</th>
      <th>Taught yourself a new language, framework, or tool without taking a formal course</th>
      <th>Taught yourself a new language, framework, or tool without taking a formal course;Contributed to open source software</th>
      <th>Taught yourself a new language, framework, or tool without taking a formal course;Participated in a hackathon</th>
      <th>Taught yourself a new language, framework, or tool without taking a formal course;Participated in a hackathon;Contributed to open source software</th>
      <th>Taught yourself a new language, framework, or tool without taking a formal course;Participated in online coding competitions (e.g. HackerRank, CodeChef, TopCoder)</th>
      <th>Taught yourself a new language, framework, or tool without taking a formal course;Participated in online coding competitions (e.g. HackerRank, CodeChef, TopCoder);Contributed to open source software</th>
      <th>Taught yourself a new language, framework, or tool without taking a formal course;Participated in online coding competitions (e.g. HackerRank, CodeChef, TopCoder);Participated in a hackathon</th>
      <th>Taught yourself a new language, framework, or tool without taking a formal course;Participated in online coding competitions (e.g. HackerRank, CodeChef, TopCoder);Participated in a hackathon;Contributed to open source software</th>
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
      <td>Associate degree</td>
      <td>11</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>1</td>
      <td>...</td>
      <td>11</td>
      <td>17</td>
      <td>212</td>
      <td>123</td>
      <td>16</td>
      <td>22</td>
      <td>21</td>
      <td>21</td>
      <td>10</td>
      <td>9</td>
    </tr>
    <tr>
      <td>Bachelor’s degree (BA, BS, B.Eng., etc.)</td>
      <td>107</td>
      <td>7</td>
      <td>9</td>
      <td>6</td>
      <td>7</td>
      <td>2</td>
      <td>4</td>
      <td>0</td>
      <td>24</td>
      <td>5</td>
      <td>...</td>
      <td>332</td>
      <td>521</td>
      <td>2607</td>
      <td>1313</td>
      <td>358</td>
      <td>497</td>
      <td>373</td>
      <td>304</td>
      <td>234</td>
      <td>353</td>
    </tr>
    <tr>
      <td>I never completed any formal education</td>
      <td>6</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>...</td>
      <td>1</td>
      <td>3</td>
      <td>44</td>
      <td>34</td>
      <td>0</td>
      <td>10</td>
      <td>4</td>
      <td>5</td>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <td>Master’s degree (MA, MS, M.Eng., MBA, etc.)</td>
      <td>66</td>
      <td>9</td>
      <td>3</td>
      <td>1</td>
      <td>5</td>
      <td>4</td>
      <td>0</td>
      <td>1</td>
      <td>17</td>
      <td>4</td>
      <td>...</td>
      <td>143</td>
      <td>246</td>
      <td>1337</td>
      <td>846</td>
      <td>134</td>
      <td>246</td>
      <td>156</td>
      <td>197</td>
      <td>56</td>
      <td>181</td>
    </tr>
    <tr>
      <td>Other doctoral degree (Ph.D, Ed.D., etc.)</td>
      <td>5</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>6</td>
      <td>31</td>
      <td>219</td>
      <td>221</td>
      <td>11</td>
      <td>59</td>
      <td>15</td>
      <td>41</td>
      <td>4</td>
      <td>25</td>
    </tr>
    <tr>
      <td>Primary/elementary school</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>8</td>
      <td>15</td>
      <td>198</td>
      <td>96</td>
      <td>6</td>
      <td>17</td>
      <td>26</td>
      <td>18</td>
      <td>3</td>
      <td>11</td>
    </tr>
    <tr>
      <td>Professional degree (JD, MD, etc.)</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>...</td>
      <td>4</td>
      <td>4</td>
      <td>75</td>
      <td>38</td>
      <td>8</td>
      <td>7</td>
      <td>10</td>
      <td>6</td>
      <td>1</td>
      <td>6</td>
    </tr>
    <tr>
      <td>Secondary school (e.g. American high school, German Realschule or Gymnasium, etc.)</td>
      <td>19</td>
      <td>1</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>5</td>
      <td>1</td>
      <td>...</td>
      <td>88</td>
      <td>140</td>
      <td>990</td>
      <td>527</td>
      <td>75</td>
      <td>141</td>
      <td>147</td>
      <td>161</td>
      <td>50</td>
      <td>102</td>
    </tr>
    <tr>
      <td>Some college/university study without earning a degree</td>
      <td>23</td>
      <td>6</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>4</td>
      <td>0</td>
      <td>...</td>
      <td>47</td>
      <td>119</td>
      <td>816</td>
      <td>534</td>
      <td>78</td>
      <td>141</td>
      <td>81</td>
      <td>113</td>
      <td>33</td>
      <td>107</td>
    </tr>
  </tbody>
</table>
<p>9 rows × 490 columns</p>
</div>




```python
df['EdLevel'].isna().sum()
```




    2493




```python
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
# let's see education level
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
fig = px.box(df, x="EdLevel", y='ConvertedComp', range_y=[0, 2*10**5])
fig.show()
```




```python
# let's define df for only United States Country respondent
df_us = df[df['Country'] == 'United States']
df_us['Country'].head()
```




    3     United States
    12    United States
    21    United States
    22    United States
    25    United States
    Name: Country, dtype: object




```python
# I need to show exact median values for B.S. degree vs I never completed formal education
df_us.groupby(['EdLevel'])['ConvertedComp'].median()
```




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




```python
df_us['YearsCodePro'] = df_us['YearsCodePro'].apply(lambda x: 0.5 if x == 'Less than 1 year' else (50 if x == 'More than 50 years' else x))
```


```python
df_us.head()
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
      <td>12</td>
      <td>13</td>
      <td>I am a developer by profession</td>
      <td>Yes</td>
      <td>Less than once a month but more than once per ...</td>
      <td>OSS is, on average, of HIGHER quality than pro...</td>
      <td>Employed full-time</td>
      <td>United States</td>
      <td>No</td>
      <td>Master’s degree (MA, MS, M.Eng., MBA, etc.)</td>
      <td>Computer science, computer engineering, or sof...</td>
      <td>...</td>
      <td>Somewhat more welcome now than last year</td>
      <td>Tech articles written by other developers;Cour...</td>
      <td>28.0</td>
      <td>Man</td>
      <td>No</td>
      <td>Straight / Heterosexual</td>
      <td>White or of European descent</td>
      <td>Yes</td>
      <td>Appropriate in length</td>
      <td>Easy</td>
    </tr>
    <tr>
      <td>21</td>
      <td>22</td>
      <td>I am a developer by profession</td>
      <td>Yes</td>
      <td>Less than once per year</td>
      <td>OSS is, on average, of HIGHER quality than pro...</td>
      <td>Employed full-time</td>
      <td>United States</td>
      <td>No</td>
      <td>Some college/university study without earning ...</td>
      <td>NaN</td>
      <td>...</td>
      <td>Just as welcome now as I felt last year</td>
      <td>Tech articles written by other developers;Indu...</td>
      <td>47.0</td>
      <td>Man</td>
      <td>No</td>
      <td>Straight / Heterosexual</td>
      <td>White or of European descent</td>
      <td>Yes</td>
      <td>Appropriate in length</td>
      <td>Easy</td>
    </tr>
    <tr>
      <td>22</td>
      <td>23</td>
      <td>I am a developer by profession</td>
      <td>Yes</td>
      <td>Less than once per year</td>
      <td>The quality of OSS and closed source software ...</td>
      <td>Employed full-time</td>
      <td>United States</td>
      <td>No</td>
      <td>Bachelor’s degree (BA, BS, B.Eng., etc.)</td>
      <td>Information systems, information technology, o...</td>
      <td>...</td>
      <td>Just as welcome now as I felt last year</td>
      <td>Tech articles written by other developers;Tech...</td>
      <td>22.0</td>
      <td>Man</td>
      <td>No</td>
      <td>Straight / Heterosexual</td>
      <td>Black or of African descent</td>
      <td>No</td>
      <td>Appropriate in length</td>
      <td>Easy</td>
    </tr>
    <tr>
      <td>25</td>
      <td>26</td>
      <td>I am a developer by profession</td>
      <td>Yes</td>
      <td>Less than once per year</td>
      <td>The quality of OSS and closed source software ...</td>
      <td>Employed full-time</td>
      <td>United States</td>
      <td>No</td>
      <td>Some college/university study without earning ...</td>
      <td>Computer science, computer engineering, or sof...</td>
      <td>...</td>
      <td>Just as welcome now as I felt last year</td>
      <td>NaN</td>
      <td>34.0</td>
      <td>Man</td>
      <td>No</td>
      <td>Gay or Lesbian</td>
      <td>NaN</td>
      <td>No</td>
      <td>Appropriate in length</td>
      <td>Easy</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 85 columns</p>
</div>




```python
df_us[df_us['YearsCodePro'] == 0.5]
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
      <td>306</td>
      <td>308</td>
      <td>I am a developer by profession</td>
      <td>Yes</td>
      <td>Never</td>
      <td>OSS is, on average, of HIGHER quality than pro...</td>
      <td>Employed full-time</td>
      <td>United States</td>
      <td>No</td>
      <td>Master’s degree (MA, MS, M.Eng., MBA, etc.)</td>
      <td>Computer science, computer engineering, or sof...</td>
      <td>...</td>
      <td>Just as welcome now as I felt last year</td>
      <td>NaN</td>
      <td>36.0</td>
      <td>Woman</td>
      <td>No</td>
      <td>Straight / Heterosexual</td>
      <td>White or of European descent</td>
      <td>No</td>
      <td>Appropriate in length</td>
      <td>Easy</td>
    </tr>
    <tr>
      <td>316</td>
      <td>318</td>
      <td>I am a developer by profession</td>
      <td>Yes</td>
      <td>Less than once per year</td>
      <td>The quality of OSS and closed source software ...</td>
      <td>Employed full-time</td>
      <td>United States</td>
      <td>Yes, full-time</td>
      <td>Bachelor’s degree (BA, BS, B.Eng., etc.)</td>
      <td>Computer science, computer engineering, or sof...</td>
      <td>...</td>
      <td>Just as welcome now as I felt last year</td>
      <td>NaN</td>
      <td>21.0</td>
      <td>Man</td>
      <td>No</td>
      <td>Bisexual;Straight / Heterosexual</td>
      <td>South Asian</td>
      <td>No</td>
      <td>Too long</td>
      <td>Easy</td>
    </tr>
    <tr>
      <td>378</td>
      <td>380</td>
      <td>I am a developer by profession</td>
      <td>No</td>
      <td>Never</td>
      <td>OSS is, on average, of HIGHER quality than pro...</td>
      <td>Employed part-time</td>
      <td>United States</td>
      <td>No</td>
      <td>Secondary school (e.g. American high school, G...</td>
      <td>NaN</td>
      <td>...</td>
      <td>Just as welcome now as I felt last year</td>
      <td>NaN</td>
      <td>34.0</td>
      <td>Woman</td>
      <td>No</td>
      <td>Bisexual</td>
      <td>White or of European descent</td>
      <td>No</td>
      <td>Appropriate in length</td>
      <td>Easy</td>
    </tr>
    <tr>
      <td>381</td>
      <td>383</td>
      <td>I am not primarily a developer, but I write co...</td>
      <td>Yes</td>
      <td>Never</td>
      <td>OSS is, on average, of HIGHER quality than pro...</td>
      <td>Employed full-time</td>
      <td>United States</td>
      <td>No</td>
      <td>Master’s degree (MA, MS, M.Eng., MBA, etc.)</td>
      <td>Information systems, information technology, o...</td>
      <td>...</td>
      <td>Just as welcome now as I felt last year</td>
      <td>Tech articles written by other developers;Tech...</td>
      <td>38.0</td>
      <td>Man</td>
      <td>No</td>
      <td>Straight / Heterosexual</td>
      <td>White or of European descent</td>
      <td>Yes</td>
      <td>Appropriate in length</td>
      <td>Easy</td>
    </tr>
    <tr>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <td>88773</td>
      <td>70197</td>
      <td>NaN</td>
      <td>No</td>
      <td>Once a month or more often</td>
      <td>OSS is, on average, of HIGHER quality than pro...</td>
      <td>Independent contractor, freelancer, or self-em...</td>
      <td>United States</td>
      <td>No</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>Not applicable - I did not use Stack Overflow ...</td>
      <td>Courses on technologies you're interested in</td>
      <td>NaN</td>
      <td>Woman</td>
      <td>No</td>
      <td>NaN</td>
      <td>Black or of African descent</td>
      <td>Yes</td>
      <td>Too long</td>
      <td>Easy</td>
    </tr>
    <tr>
      <td>88777</td>
      <td>70955</td>
      <td>NaN</td>
      <td>No</td>
      <td>Once a month or more often</td>
      <td>The quality of OSS and closed source software ...</td>
      <td>Not employed, but looking for work</td>
      <td>United States</td>
      <td>NaN</td>
      <td>I never completed any formal education</td>
      <td>NaN</td>
      <td>...</td>
      <td>Not applicable - I did not use Stack Overflow ...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Non-binary, genderqueer, or gender non-conforming</td>
      <td>No</td>
      <td>NaN</td>
      <td>Native American, Pacific Islander, or Indigeno...</td>
      <td>Yes</td>
      <td>Appropriate in length</td>
      <td>Neither easy nor difficult</td>
    </tr>
    <tr>
      <td>88840</td>
      <td>82717</td>
      <td>NaN</td>
      <td>No</td>
      <td>Less than once per year</td>
      <td>The quality of OSS and closed source software ...</td>
      <td>Not employed, but looking for work</td>
      <td>United States</td>
      <td>No</td>
      <td>Secondary school (e.g. American high school, G...</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>Industry news about technologies you're intere...</td>
      <td>44.0</td>
      <td>Man</td>
      <td>No</td>
      <td>Straight / Heterosexual</td>
      <td>White or of European descent</td>
      <td>Yes</td>
      <td>Appropriate in length</td>
      <td>Neither easy nor difficult</td>
    </tr>
    <tr>
      <td>88844</td>
      <td>83397</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Less than once per year</td>
      <td>NaN</td>
      <td>Not employed, but looking for work</td>
      <td>United States</td>
      <td>No</td>
      <td>Bachelor’s degree (BA, BS, B.Eng., etc.)</td>
      <td>Computer science, computer engineering, or sof...</td>
      <td>...</td>
      <td>Just as welcome now as I felt last year</td>
      <td>NaN</td>
      <td>27.0</td>
      <td>Woman</td>
      <td>No</td>
      <td>Bisexual</td>
      <td>White or of European descent</td>
      <td>No</td>
      <td>Appropriate in length</td>
      <td>Easy</td>
    </tr>
    <tr>
      <td>88859</td>
      <td>85642</td>
      <td>NaN</td>
      <td>No</td>
      <td>Less than once per year</td>
      <td>OSS is, on average, of LOWER quality than prop...</td>
      <td>Independent contractor, freelancer, or self-em...</td>
      <td>United States</td>
      <td>No</td>
      <td>Associate degree</td>
      <td>Information systems, information technology, o...</td>
      <td>...</td>
      <td>Just as welcome now as I felt last year</td>
      <td>Tech articles written by other developers;Indu...</td>
      <td>34.0</td>
      <td>Non-binary, genderqueer, or gender non-conforming</td>
      <td>NaN</td>
      <td>Bisexual;Gay or Lesbian</td>
      <td>White or of European descent</td>
      <td>No</td>
      <td>Appropriate in length</td>
      <td>Easy</td>
    </tr>
  </tbody>
</table>
<p>833 rows × 85 columns</p>
</div>




```python
# df_us['YearsCodePro'] = df_us['YearsCodePro'].astype(int) // this cannot take care of NaN
df_us['YearsCodePro'] = pd.to_numeric(df_us['YearsCodePro'])
```


```python
df_us.dtypes
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
    YearsCodePro              float64
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
df_us.groupby(['Code'])
```


```python
# condition for B.S. in computer science or similar degree in U.S
condition_1 = (df_us['UndergradMajor'] == 'Computer science, computer engineering, or software engineering')
result = df_us[condition].groupby(['EdLevel'])['ConvertedComp'].median()
print('Compensation with EdLevel with less than 3 years of professional coding expereince\n', result)
```

    Compensation with EdLevel with less than 3 years of professional coding expereince
     EdLevel
    Associate degree                                           60000.0
    Bachelor’s degree (BA, BS, B.Eng., etc.)                   82000.0
    Master’s degree (MA, MS, M.Eng., MBA, etc.)               100000.0
    Other doctoral degree (Ph.D, Ed.D., etc.)                 125000.0
    Professional degree (JD, MD, etc.)                         64200.0
    Some college/university study without earning a degree     60000.0
    Name: ConvertedComp, dtype: float64



```python
# condition for B.S. in computer science or similar degree in U.S, less than 5 years of professional coding experience
condition_2 = (df_us['UndergradMajor'] == 'Computer science, computer engineering, or software engineering')
result = df_us[condition_2].groupby(['EdLevel'])['ConvertedComp'].median()
print('Compensation with EdLevel with less than 3 years of professional coding expereince\n', result)
```

    Compensation with EdLevel with less than 3 years of professional coding expereince
     EdLevel
    Associate degree                                           95000.0
    Bachelor’s degree (BA, BS, B.Eng., etc.)                  110250.0
    Master’s degree (MA, MS, M.Eng., MBA, etc.)               132000.0
    Other doctoral degree (Ph.D, Ed.D., etc.)                 169000.0
    Professional degree (JD, MD, etc.)                        120000.0
    Some college/university study without earning a degree    105000.0
    Name: ConvertedComp, dtype: float64



```python
# I need to show exact median values for B.S. degree vs I never completed formal education
condition_1 = df['EduOther'] == 'Participated in a full-time developer training program or bootcamp'
bootcamp_grad_comp = df_us[condition_1].groupby(['EduOther'])['ConvertedComp'].median()
condition_2 = (df['EduOther'] == 'Participated in a full-time developer training program or bootcamp') & (df_us['YearsCodePro'] >= 3)
bootcamp_grad_three_years_exp_comp = df_us[condition_2].groupby(['EduOther'])['ConvertedComp'].median()

print('boot camp grad compensation\n', bootcamp_grad_comp)
print('boot camp grad with less than 3 years of professional coding expereince compensation\n', bootcamp_grad_three_years_exp_comp)
```

    boot camp grad compensation
     EduOther
    Participated in a full-time developer training program or bootcamp    84375.0
    Name: ConvertedComp, dtype: float64
    boot camp grad with less than 3 years of professional coding expereince compensation
     EduOther
    Participated in a full-time developer training program or bootcamp    91500.0
    Name: ConvertedComp, dtype: float64



```python
df['EduOther'].value_counts()
```


```python
fig = px.scatter(df, x="EduOther", y='ConvertedComp')
fig.show()
```


```python
fig = px.scatter(df, x="DevType", y='ConvertedComp')
fig.show()
```


```python
# age vs salary with education level

import plotly.io as pio

```

# future work
So initially, I thought comparing compensation between CS B.S. degree vs bootcamp graduates would work and the result was against my hypothesis. 

CS degree is more attractive in terms of making money. 

However I realized I cannot have simple comparison because I did not take time into the calcuation

CS degree people would normally take 4 years to get started as a professional programmer. On the other hands, bootcamp graduate tend to get a job within a year, so I completely changed a condition. I gave a factor with 3 years of professional experience for bootcamp graudate. (<3 years, but I will have to do = 3 years)

so Here are my steps

1. CS degree vs bootcamp with no time factor
2. CS degree vs bootcamp with 3 years or more
3. CS degree with 2 years of exp vs bootcamp with 5 yeras of exp

