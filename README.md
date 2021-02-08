#1.Read the three csv files which contains the score of same students in term1 for
each Subject
2. Remove the name and ethnicity column (to ensure confidentiality)


import pandas as pd
df1=pd.read_csv('MathScoreTerm1.csv')
df2=pd.read_csv('PhysicsScoreTerm1.csv')
df3=pd.read_csv('DSScoreTerm1.csv')

del df1['Name']
del df1['Ethinicity']
df1.head()
del df2['Name']
del df2['Ethinicity']

del df3['Name']
del df3['Ethinicity']

df1.fillna(0)
df1.fillna(0)
df1.fillna(0)

#frames = [df1,df2,df3]
#df = pd.concat(frames)

merged_df = df1.merge(df3, on="ID", suffixes=(
    '_math', '_ds')).merge(df2, on="ID", suffixes=('_ds', '_physics'))
df = merged_df.filter(["ID", "Score_math", "Score_ds", "Score", "Age_math","Sex_ds"]).rename(
            columns={"Score": "Score_physics", "Age_math": "Age","Sex_ds": "Sex"})

#print(df_col)



df["Sex"] = [1 if i=="M" else 2 for i in df["Sex"]]

df.head()

df.to_csv('ScoreFinal.csv')
