
# Basic
**To import pandas:**

	import pandas as pd
	
**To read/load a csv file as data frame:**

	df = pd.read_csv('data/survey_results_public.csv')
  * we can put any csv link too.
	
**If we run this df jupyter will automaticly show us only 20 rows**

**to get rows and columns number(how many rows and columns our csv file has):**

	df.shape
	
**To get rows and colums number also with all of the rows and columns data types:**

	df.info()
	
**To see all 85 columns we can set max_column 85:**

	pd.set_option('display.max_columns',85) 
	
**To see all 85 rows we can set max_rows 85:**

	pd.set_option('display.max_rows',85)
	
**To see first 5 rows**

	df.head()
	
**To see first 10 rows:**

	df.head(10)
  * can see maximum 50 value with head and tail
 
**To see last 5 rows:**

	df.tail()

**To see last 10 rows(have to put as argumant):**

	df.tail(10)

# To retrive data 

**To turn a dictionary to data frame:**

	people={
    		'first':['Chandler','Joey','Ross'],
    		'last':['Bing','Trivianni','Geller'],
    		'email':['chandler@gmail.com','joey@gmail.com','ross@gmail.com']
	}
	
	df = pd.DataFrame(people)
	
	
**To retrive individual column from data frame:**

	df['email'] or df.get('email') or df.email
	
   * it will return all email as a series object
   * series is like a list of data..
   * but it's a little bit different
   * it's basically a single column of rows
   
**To retrive or get multiple column at same time:**

	df[['first','last']]
 * remember have to passed those key as a list
 * multiple column can't be a series object it's only a filtered data frame
 * because series object must have to be a single column

**To see only column's index:**

	df.columns
	
**TO get rows:**

	df.iloc[0]
	
 * it will return a series which contains the value of first row of data.
 * iloc = integer location
 
**To get a range of rows:**

	df.iloc[[0,1]]
	
 * it will return a data frame with two(0,1) rows
 
**To get specific value from a data frame:**

	df.iloc[[0,1],2]
	
* [0,1] = first and second rows
* 2 = third number column

**To search with level(can retrive rows wise too):**

	df.loc[0,'email']
	df.loc[[0,1],['email','first']]
 * from 0 and 1 rows
 * we will retrive email and first columns
 * we can't passed columns key's name in iloc.	
 * To retrive multiple rows or multiple columns we have to pass those argument as list.

**To use slice in loc:**

	df.loc[0:3,'Hobbyist']
  * 0 to 3 rows will be captured. 3 is inclusive 
        
	     df.loc[0:3,'Hobbyist':'Employment']
	
   * also slice can be used in key's.
   * 'Employment' is inclusive

# index
21. In data frame they gives us an extra column which is contained some range of number
    we called it index.basically that's an integer unique identifier of the rows.

22.We can create index or unique identifier explicitly:
	df.set_index('email',inplace=True)
	->now email is the unique identifier or index.
	->now we can use these index in example: pd.loc['joey@gmail.com']
	->but if we use iloc[] instead of loc[]
	->loc[] will still gives us the rows.
	->Now we no longer have those integer as default index.

23. To see those index:
	df.index
	-->>This indexes are the level of these rows.
	
24. To reset our index:
	df.reset_index(inplace=True)

25. We can set index by passing a argument in read_csv():
	df = pd.read_csv('data/survey_results_public.csv',index_col='Respondent')
	->now Respondent column is our index.

26. Sometimes when we retrive a data it is truncated .To see the full text we can pass columns name with rows name.

27. To sort our index list:
	schema_df.sort_index()
	schema_df.sort_index(ascending=False)
	-> descending order
28. To sort our index list permanently:
	schema_df.sort_index(inplace=True)

29. To filter data:
	df['last'] == 'Bing'
	it will return true and false(if match true otherwise false).
30. To filter out some rows with true:
	filt = df['last'] == 'Bing'
	df[filt] or df.loc[filt] //.loc[] is prefered
	->these can be filter out data with boolean.
	it will return a data frame where it return all rows that have the last name Bing.
31. To filter out more specific data:
	df.loc[filt,'email']
32. To filter out with multiple condition:
	&=and
	|=or
	~=not
	filt = (df['first']=='Chandler') | (df['last']=='Geller')
	df.loc[filt,'email']
	df.loc[~filt,'email'] //opposite data will be returned

33. To filter out with a list:
	countries = ['Bangladesh','United States','Germany']
	filt = df['Country'].isin(countries)	
	df.loc[filt,'Country']
	->if any country is available in df['Country'] otherwise return False.
	->it will return True
34. Check with str method conatins:
	filt = df['LanguageWorkedWith'].str.contains('Python',na=False)
	df.loc[filt,'LanguageWorkedWith']

	->In languageWorkedWith column is contains 'Python word' .
	->If any NaN value contains it will return error
	->na = False means it won't do anything with NaN value

#Modify index columns
35. To change any columns names:
	df.columns = ['first_name','last_name','email']
36. To uppercase all of the columns name:
	df.columns = [x.upper() for x in df.columns]
37. To replace any word or something from the columns:
	df.columns = df.columns.str.replace(' ','_')
38. Another way to rename columns:
	df.rename(columns={'first_name':'first','last_name':'last'},inplace=True) 

#Modify:
39. To modify a certain row:
	df.loc[0] = ['Phoebe','Buffay','phoebe@gmail.com']
40. To modify a certain value from data frame:
	df.loc[2,['first','email']]=['Monica','monica@gmail.com']
41. To modify a single value from data frame:
	df.loc[2,'first']='Monica'
	->another way:
	df.at[2,'email'] = 'ross@gmail.com'
42. To change data with filter:
	filt = (df['email'] == 'ross@gmail.com')
	df.loc[filt,'email'] = 'geller@gmail.cpm'

43. To set uppercase to a specific columns data:
	df['email'] = df['email'].str.upper()

# apply-we will passed a function in apply() it will do that function wise worked on every rows/columns.
44. To get length of a column/series:
	df['email'].apply(len)
45.To change columns with apply() permanently:
	df['email'] = df['email'].apply(lambda x:x.upper())

46. To get (how many value inside a columns) length:
	df.apply(len)
47. To get (how many value inside a rows) length:
	df.apply(len,axis='columns')
48. To get the minimum value from a data frame:
	df.apply(lambda x: x.min()) or df.apply(pd.Series.min)

#applymap() - only workes on data frame.
49. To apply a function to every individual element in a data frame:
	df.applymap(len)
50. To make all value uppercase from a data frame:
	df=df.applymap(lambda x : x.lower())
	or df=df.applymap(str.lower)

#Repace
51. To replace value:
	df['first'] = df['first'].replace({'chandler':'Chandler','joey':'Joye'})

52. To add new columns:
	df['full_name'] = df['first'] +' '+df['last']
53. To delete a column:
	df.drop(columns='first',inplace=True)
54. To delete multiple column:
	df.drop(columns=['first','last'],inplace=True)
55. To split a value:
	df['full_name'].str.split(' ')
56. To split a value with two columns:
	df['full_name'].str.split(' ',expand=True)
57. To create two new column with those seperated value:
	df[['first_name','last_name']] = df['full_name'].str.split(' ',expand=True)
58. To append a single row:
	df=df.append({'first':'Tom'}, ignore_index=True)
	->other values are stored as NaN
59. To append another data frame:
	df=df.append(df2, ignore_index=True)
60. To drop a row:
	df.drop(index=6,inplace=True)

61. Delete a row with filtering:
	filt=(df['last'] == 'Hanks')
	df=df.drop(index=df[filt].index)

#Sorting:

62. To sort data by a index column name:
	df.sort_values(by='last',inplace=True)
	->last is a column.
63. To sort by descending order:
	df.sort_values(by='last',ascending=False,inplace=True)	
64. To sort data by multiple index column name:
	df.sort_values(by=['last','first'],ascending=False,inplace=True)
	->after sorting by 'last' if there are multiple value with same name
	->then it will go for 'first'
65. To sort multiple column with multiple type(Ascending/Descending):
	df.sort_values(by=['last','first'],ascending=[False,True],inplace=True)
66. After sorting the row index will remain same To change them in ascending order:
	df=df.sort_index()
67. To see sorted value of any column:
	df['last'].sort_values()

68.To see first 10 largest value:
	df['ConvertedComp'].nlargest(10)
	-> only 'ConvertedComp' value will be printed.
69. To see whole data frame with sorting first largest 10 value:
	df.nlargest(10,'ConvertedComp')
	->10 could be change as any number.	
70.To see first 10 smallestvalue:
	df['ConvertedComp'].nsmallest(10)
	-> only 'ConvertedComp' value will be printed.
71. To see whole data frame with sorting in 'ConvertedComp' first smallest 10 value:
	df.nsmallest(10,'ConvertedComp')
	->10 could be change in any number.	

#Aggregate function:
72. To get mediam value from 'ConvertedComp' column:
	df['ConvertedComp'].median()
73. To get medium value from whole data frame's numaric type:
	df.median()
74. To get overview of different state from a data frame:
	df.describe()
	-> we will get a row a of 50% that means the medium value
75. To get overview of a single column:
	df['ConvertedComp'].describe()
76. To count how many value is exist whom it will count:
	df['ConvertedComp'].count()
77. To count how many is unique:
	df['Hobbyist'].value_counts()
78.To get counted value from unique data in percentage:
	df['SocialMedia'].value_counts(normalize=True)
	->it will return 0.170...something like that.
	->that means 17%

#GROUP BY - split our object->applying a function -> combining those results:

79. To get all country by group:
	country_grp = df.groupby('Country')
80. To get most used social media by country group:
	country_grp['SocialMedia'].value_counts()
	->instead of value_counts() we can use any type of aggregate function
81. To get an individual country from a country group:
	country_grp['SocialMedia'].value_counts().loc['Bangladesh']
82. To get a group:
	country_grp.get_group('United States')
83. To use multiple aggregate function:
	country_grp['ConvertedComp'].agg(['median','mean'])
84. We can use sum() in boolean type too:
	filt=df['Country'] == 'India'
	df.loc[filt]['LanguageWorkedWith'].str.contains('Python').sum()
85. In group By we can't use str method directly(bcz groupby return a series object) to use str method we have to use apply():
	country_grp['LanguageWorkedWith'].apply(lambda x : x.str.contains('Python'))
86. To concat multiple data frame :
	python_df=pd.concat([country_respondents,country_know_python],axis='columns',sort=False)
	->defaultly axis='rows'

#Handling Missing values:

87. to drop rows based on missing value:
	df.dropna(axis='index',how='any',inplace=True) OR df.dropna(inplace=True)
	->how='any' means if any of the value from data frame in None or NaN 
	->(axis='index') that row will be deleted.
	->if we set axis='columns' then column will be deleted instead of row
  	->if we use how='all' instead of 'any' columns or rows all value have to be None or NaNs 
88. To drop more specific:
	example I don't need first_name or last_name but i need the email,,
	So, if first_name or last_name = None or NaN i don't want to delete that row/column untill i have 
	his/her email.if email is None or NaN then we can delete that row or column,,,
	
	df.dropna(axis='index', how='any', subset=['email'],inplace=True)
	->it will delete based on 'email'.
	-> so, we can say that our how='' won't do anything

	If we want to do something like we want email or last_name.
	then we can use
	df.dropna(axis='index', how='all', subset=['email','last'],inplace=True)
	-> in here all is required 
	-> because all will checked email and first 
	-> but any will check either email or first 
89. In data frame some NA or Missing value are exist to drop them:
	df.replace('NA',np.nan,inplace=True)
	df.replace('Missing', np.nan, inplace=True)
	df.dropna()
	->can do replace in any specific column

90. To get True false based on None or NaN:
	df.isna()
	->it will give us True if that value is None or NaN

91. To replace those NaN or None value to numarical or string type:
	df.fillna(0)
	-> instead of zero we can writhe down any string value too.
92. To see data type:
	df.dtypes
	-> in our people data frame there is an age column ,
	-> but age column is not in numaric ,it was in string type
	-> to use this age we have to cast those string to float.

93. To cast String to float:
	df['age'] = df['age'].astype(float)
	-> now we can use aggregate function too,,,
94. To cast whole data frame into float(if possible):
	df = df.astype(float)
	-> can do with specific column
95.To see all unique value from a column:
	df['YearsCode'].unique()

96. To replace multiple value into NaN in csv file:
	na_vals = ['NA','Missing']
	df = pd.read_csv('data/survey_results_public.csv',index_col='Respondent',na_values=na_vals)


#Date Time:

97. To convert a string datetime to pandas datetime format:
	df['Date'] = pd.to_datetime(df['Date'],format='%Y-%m-%d %I-%p')
	->format have to be as same as like data frame's date.
	->format='' is may different for every data frame  
	-> we convert to date format bcz now we can behave with them like date not like string
	-> If pandas can read our date format we don't need to add fromat.


98. To see day of the week from an individual datetime:
	df.loc[0,'Date'].day_name()

99. To convert a string datetime to pandas datetime format when loading the csv file:
	d_parser = lambda x: datetime.strptime(x, '%Y-%m-%d %I-%p')
	df = pd.read_csv('data/ETH_1h.csv',parse_dates = ['Date'], date_parser = d_parser)
	-> if pandas can read that datetime format we don't need to use 'date_parser'.

100. To see whole column's day of the week at once:
	df['Date'].dt.day_name()
101. To create a day of the week column:
	df['DayOfWeek'] = df['Date'].dt.day_name()

102. To see the most earliest date:
	df['Date'].min()
103. To see the most newest date:
	df['Date'].max()
104. We can subtract date:
	df['Date'].max()-df['Date'].min()

105. To filter out a range of date with string format date:
	filt = (df['Date'] >= '2019') & (df['Date'] < '2020')
	df.loc[filt]

106. To filter out a range of date with panda's datetime format:
	filt = (df['Date'] >= pd.to_datetime('2019-01-01')) & (df['Date'] < pd.to_datetime('2020-01-01'))
	df.loc[filt]
107. Slicing range of date:
	df['2020-01':'2020-02']
	-> our date time is our index
108. To get an individiual column's value:
	df['High'].resample('D').max()
	-> from 'High' column we got maximum value of each Day.
	-> to get each day we write down 'D' as a Day format.
	-> can do resample for whole data frame (df.resample('W') W=Week)
109. To show this High as graph with the help of matplotlib:
	highs=df['High'].resample('D').max()
	%matplotlib inline
	highs.plot()
110. To use so many aggregate function at once with different columns:
	df.resample('W').agg({'Close':'mean','High':'max','Low':'min','Volume':'sum'})
	-> Key = column name
	-> value = aggregate function

#Read and write data

111. To write data frame as csv:
	filt = (df['Country'] == 'Bangladesh')
	bd_df = df.loc[filt]
	bd_df.to_csv('data/bd_survey.csv')
112. To write data as tsv:
	bd_df.to_csv('data/bd_survey.tsv' , sep='\t')
	->tab seperated value
#Excel :
113. To install required module:
	pip install xlwt openpyxl xlrd

114. To write data as Excel:
	bd_df.to_excel('data/bd_survey.xlsx')

115. To read an excel file:
	test = pd.read_excel('data/bd_survey.xlsx',index_col='Respondent')
116. To write data as json file like dictionary:
	bd_df.to_json('data/bd_survey.json')
117. To write data as json like list type:
	bd_df.to_json('data/bd_survey2.json' , orient='records' , lines=True)
	-> other='records' means it will create that json as list type.
	-> lines=True means it will create new line after every line
118. To read json (dictionary type) file:
	test = pd.read_json('data/bd_survey.json')
119. To read json (list type) file:
	test = pd.read_json('data/bd_survey2.json', orient='records', lines=True)
120. To write data as sql:
     =>First import:
	from sqlalchemy import create_engine
	import psycopg2
	
	engine = create_engine('postgresql://postgres:788881137@localhost:5432/test')
	-> username:postgres, pass:788881137, post:5432, tablename: test
	bd_df.to_sql('test_table',engine)

121. To replace existing table:
	bd_df.to_sql('test_table',engine, if_exists='replace')
122. To reas sql :
	sql_df = pd.read_sql('test_table', engine, index_col='Respondent')
123. To read sql with query:
	sql_df = pd.read_sql('SELECT * FROM test_table', engine)








#df['name'] = this is working with columns
#df.loc[0] = this is working with rows and boolean too











