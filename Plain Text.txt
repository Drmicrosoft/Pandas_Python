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



# ================================================

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



# >>>>>>>>

In next Operations when we apply function to a Series will apply 
this function to all Values 
# ..........

# to do operations from standard python ON A SERIES

df['emails'] = df['emails'].apply(len)


# to do function and use it inside ON A SERIES

def update_email(email) :
	return email.upper()
df['email'].apply(update_email)

# Lambda function ON A SERIES
df['emails'] = df['emails'].apply(lambda x : x.lower())

# >>>>>>>>>>

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

# for changing values of column :
df['emails'].map ({'omar' : 'soso' , 'soso' : 'omar'}) 
will remove all other values and convert them to NaN

to avoid this 
df['emails'].replace ({'omar' : 'soso' , 'soso' : 'omar'}) 




# =================================================
>> this is for Columns 

# to add 2 series togethers  

df['full_name'] = df['first'] + ' ' + df['last'] 
omar okasha

# to remove columns 

df.drop(columns=['first','last'], inplace=True)


# to split column to multiple columns 
df[['first','last']] = df['full_names'].str.split(' ', expand=True)

# ===============================================
# to add rows 
df.append({'column.name' : 'omar'},ignore_index = True)
df.append(df2,ignore_index = True)



# to drop rows 

df.drop(index=4)

###### IMPORTANT

# to remove with INDEX from FIlter 

filt = df['last'] == 'omar'
df.drop(index = df[filt].index)


#=================================

# to sort daraframe with values in a column 

df.sort_values(by='last', ascending = False )


# to make multiple sorting as second one will sort 
# the duplicate elements in the first sorting 

df.sort_values(by = ['last','first'] )


# to make multiple sorting with different ascending and descending 

df.sort_values ( by = ['last','first'] , ascending = [False, True] , inplace = True )
df.sort_index()

# to sort a series of the dataframe alone 

df['last'].sort_values()


===========================

# to get a number of largest values in a series 

df['salary'].nlargest(100)

# to get a number if largest values in a dataframe from pov of a
specific series

df.nlargest(100,'salary')

there is also nsmallest


# to get the midian value of a series 

df['salary'].midian()

# to get all series midian 

df.midian()

# to get overview over all the series in details 
df.descripe()

#to get the number of the lines that not NaN

df['omar'].count()

# to get how many different values and how many they appeared 

df['omar'].values_count()

# to get it in percentage 

df['omar'].values_count(normalize=True)

#========================================================
#========================================================
#========================================================
#========================================================
#========================================================

# Group # Important #

OK ... 

# to catergorize and split the whole df based on values in a series 

country_grp = df.groupby(['country'])

>> this is the object of dataframegroupobject

country_grp.get_group('United States')

>> will out all the df that only have value at the country equal to
>> united states
>> and this is equal to the filter what we have done

filt = df['country'] == 'United States'
df.loc[filt]

if we want to count things in another column based on the filter

filt = df['country'] == 'United States'
df.loc[filt]['social_media'].value_counts() 


another way >> # Important

country_grp['social_media'].value_counts()
>> this will give us for all values in country and the number of 
>> users in social media for each country 
 
>> to select specific country 
country_grp['social_media'].value_counts().loc['india']

country_grp['salary'].midian().loc['germany']

>> if i want to make some operations pf tje column like midian 

country_grp['salary'].agg(['midian','mean']).loc['germany']

#important 
#important 
#important 

# groupby take the values in the columns we groupby it and make them
# as the rows for all other columns . and that is why in the last 
# code we select the row of india after all the process we have made
# on the coloum 


+++++





