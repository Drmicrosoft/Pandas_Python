# Pandas_Python

# series is  a column
# data frames is multiple columns "Series" with name for each row 

# to call a columm in dataframe : 
df['email']
df.email
# to access multipe columms 
df[['email','last']]

# to print all columns name 
df.columns

# to access a row 
df.iloc[0]  << with integer not row name
df.iloc[[0,1,2]] << multiple rows


# to access rows and columns 
df.iloc[- list of rows - , - list of columns - ]
df.iloc[[1,2],1]
df.iloc[1.['email','last']]
df.loc[0:100,'email']
df.loc[0:100,'email':'last']

# to get the size of dataframe 
df.shape


# if you have a yes or no question in a column and need to count the
YESs and NOs then we can use 
df.email.value_counts()


# if we want to change our index to anontehr coloum 
df.set_index('email')  >>>  but this change wont happen to df
df.set_index('email',inplace=True) >> changes will be applied at df


# if we changed the index and we want to get it back to default 
df.reset_index(inplace=True)

# if the data was too long in sepecific column then you should 
df.loc['omar','qeustion']

# to sort df alphapeticily 
df.sort_index()
# reverse order 
df.sort_index(asending = False )



================================================

# to filter output values of a column 
df.email == 'omar'

>>>> this will return a Series of False and Trues for achieving condition
or not
1 False
2 True

# to turn it to the real values 
df(df.email== 'omar')
------
filt = df,email == 'omar'
df(filt)
or
df.loc(filt)


>>> IMPORTANT
# For Mulitple Filtering & | 
filt = (df.email == 'omar' ) & (df.name == 'beeb')


# to get all data except this filter >> ~ 
df.loc(~filt , 'email') 

# if we have punch of values and we want to filter a coloum with it 
Names = ['omar','soso']
filt = df.names.isin(Names)


# if we want to check if word inside a column 
filt = df.names.str.contains("c++") 
if there is NaN values >>
filt = df.names.str.contains("c++".na=False) 

????? need to search to for pandas.str and learn more about the methods 
over there 

# to update values 
df.loc[2] = [' ' , ' ' , ' ' ] >> to change all values in row
df.loc[2,['email' , 'last'] = ['omar','soso']
df.loc[2,'email'] = 'omar' 
df.at[2.'last'] = 'omar'

# update value with filter  
filt = (df['email'] == 'omar')
df[filt]['last'] = 'omar' >> this is fault error for warning and
value will not be changed

df.loc[filt,'last'] = 'omar' >> this is the right way to do this 

# to update columns names 

df.rename(columns = {'old_value' : 'new_value' , 'old_v : 'new_v'},inplace = True )
df.columns = [x.lower() for x in df.columns ] 
df.columns = ['value_1' , 'value_2' , 'value_3']



>>>>>>>>

In next Operations when we apply function to a Series will apply 
this function to all Values 
..........

# to do operations from standard python ON A SERIES

df['emails'] = df['emails'].apply(len)


# to do function and use it inside ON A SERIES

def update_email(email) :
	return email.upper()
df['email'].apply(update_email)

# Lambda function ON A SERIES
df['emails'] = df['emails'].apply(lambda x : x.lower())

>>>>>>>>>>

When you do operations on Dataframe level the operation
will be implemennted on the series

...........

# to do Operaitons on DataFrame 

df.apply(len)
output >> 
column_1 numnber of items in series 1
column_2 numnber of items in series 2

>>> Series has a function for min 
>>> this will get all the min values for all series
df.apply(pd.Series.min)
df.apply(lambda x : x.min())


# to apply function to all values in the dataframes not SERIES

df.applymap(len)
df.applymap(str.lower)

for changing values of column :
df['emails'].map ({'omar' : 'soso' , 'soso' : 'omar'}) 
will remove all other values and convert them to NaN

to avoid this 
df['emails'].replace ({'omar' : 'soso' , 'soso' : 'omar'}) 







