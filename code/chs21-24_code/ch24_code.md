[toc]
# Exploring data


```python
# coding: utf-8

# In[3]:


get_ipython().system('pip install pandas matplotlib numpy')


# In[2]:


get_ipython().magic('matplotlib inline')
import pandas as pd
import numpy as np


# In[3]:


grid = [[1,2,3], [4,5,6], [7,8,9]]
print(grid)

[[1, 2, 3], [4, 5, 6], [7, 8, 9]]


# In[4]:


import pandas as pd
df = pd.DataFrame(grid)
print(df)


# In[5]:


df = pd.DataFrame(grid, columns=["one", "two", "three"] )
print(df)


# In[6]:


print(df["two"])


# In[7]:


print([x[1] for x in grid])
[2, 5, 8]


# In[8]:


for x in df["two"]:
    print(x)


# In[9]:


edges = df[["one", "three"]]
print(edges)


# In[10]:


print(edges.add(2))


# In[11]:


df['two'].value_counts()


# In[18]:


mars = pd.read_json("mars_data_01.json")
print(mars)


# In[27]:


temp = pd.read_csv("temp_data_01.csv", header=0, names=range(18), usecols=range(4,18))


# In[28]:


print(temp)


# In[26]:


temp = pd.read_csv("temp_data_01.csv", na_values=['Missing'], header=0, names=range(18), usecols=range(4,18))
print(temp)


# In[29]:


temp[17][0]


# In[31]:


temp[17]=temp[17].str.strip("%")
temp[17][0]


# In[34]:


temp[17][0]


# In[32]:


temp[17] = pd.to_numeric(temp[17])
temp[17][0]


# In[33]:


temp[17] = temp[17].div(100)
temp[17]


# In[34]:


calls = pd.read_csv("sales_calls.csv")
print(calls)


# In[35]:


revenue = pd.read_csv("sales_revenue.csv")
print(revenue)


# In[37]:


calls_revenue = pd.merge(calls, revenue, on=['Territory', 'Month'])
print(calls_revenue)


# In[38]:


print(calls_revenue[calls_revenue.Territory==3])


# In[39]:


print(calls_revenue[calls_revenue.Amount/calls_revenue.Calls>500])


# In[40]:


calls_revenue['Call_Amount'] = calls_revenue.Amount/calls_revenue.Calls
print(calls_revenue)


# In[42]:


print(calls_revenue.Calls.sum())
print(calls_revenue.Calls.mean())
print(calls_revenue.Calls.median())
print(calls_revenue.Calls.max())
print(calls_revenue.Calls.min())


# In[43]:


print(calls_revenue[calls_revenue.Call_Amount >= calls_revenue.Call_Amount.median()])
print(calls_revenue.Call_Amount.median())


# In[45]:


print(calls_revenue[['Month', 'Calls', 'Amount']].groupby(['Month']).sum())


# In[46]:


print(calls_revenue[['Territory', 'Calls', 'Amount']].groupby(['Territory']).sum())


# In[47]:


calls_revenue[['Territory', 'Calls']].groupby(['Territory']).sum().plot.bar()


# In[152]:


calls_revenue[['Month', 'Call_Amount']].groupby(['Month']).mean().plot()


# In[ ]:

```


