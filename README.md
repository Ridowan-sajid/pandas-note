# pandas-note

1. to import pandas:
	import pandas as pd
2.to read/load a csv file as data frame:
	df = pd.read_csv('data/survey_results_public.csv')
3. if we run this df jupyter will automaticly show us only 20 rows

4.to get rows and columns number(how many rows and columns our csv file has):
	df.shape
5. to get rows and colums number also with all of the rows and columns data types:
	df.info()
6. To see all 85 columns we can set max_column 85:
	pd.set_option('display.max_columns',85) 
7. To see all 85 rows we can set max_rows 85:
	pd.set_option('display.max_rows',85)
8. to see first 5 rows:
	df.head()
9. to see first 10 rows:
	df.head(10)
10. to see last 5 rows:
	df.tail()
11. to see last 10 rows(have to put as argumant):
	df.tail(10)

12. To turn a dictionary to data frame:
	df = pd.DataFrame(people)
	->people is a dictionary
	people={
    		'first':['Chandler','Joey','Ross'],
    		'last':['Bing','Trivianni','Geller'],
    		'email':['chandler@gmail.com','joey@gmail.com','ross@gmail.com']
	}
13. To retrive individual column from data frame:
	df['email'] or df.get('email') or df.email
	->it will return all email as a series object
	->series is like a list of data..
	->but it's a little bit different
	->it's basically a single column of rows
14.To retrive or get multiple column at same time:
	df[['first','last']]
	-> remember have to passed those key as a list
	-> multiple column can't be a series object it's only a filtered data frame
	-> because series object must have to be a single column

15. To see only column's key:
	df.columns
16. TO get rows:
	df.iloc[0]
	->it will return a series which contains the value of first row of data.
	->iloc = integer location:
17. To get a range of rows:
	df.iloc[[0,1]]
	->it will return a data frame with two(0,1) rows
18. To get specific value from a data frame:
	df.iloc[[0,1],2]
	[0,1] = first and second rows
	2 = third number column
19. To search with level(can retrive rows wise too):
	df.loc[0,'email']

	df.loc[[0,1],['email','first']]
	->from 0 and 1 rows
	->we will retrive email and first columns
	->we can't passed columns key's name in iloc.	
 -->>To retrive multiple rows or multiple columns we have to pass those argument as list.

20. To use slice in loc:
	df.loc[0:3,'Hobbyist']
	->0 to 3 rows will be captured. 3 is inclusive 
        
	df.loc[0:3,'Hobbyist':'Employment']
	
	->also slice can be used in key's.
	->'Employment' is inclusive

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
	filt=df['last'] == 'Hanks'
	df=df.drop(index=df[filt].index)







#df['Hobbyist'].value_counts()
#df['name'] = this is working with columns
#df.loc[0] = this is working with rows











