# Welcome to your Geno Book
This is a small step taken by Genotechies to allow knowleage generation based on data in Sri Lankan context
<html>
<head>
<title>An active web page</title>
</head>
<body>
 part 1:
<pre data-executable>
!pip install pandas
!pip install matplotlib
#!pip install seaborn
!pip install ipywidgets
#from __future__ import print_function
from ipywidgets import interact, interactive, fixed, interact_manual
import ipywidgets as widgets
import requests  # Import the requests library
import pandas as pd
import matplotlib.pyplot as plt
import matplotlib as mpl
#import seaborn as sns
</pre>
<pre data-executable>
url = ('https://covid19-healthylk.herokuapp.com/api/districtstotal?startdate=2021-08-31&enddate=2021-09-31')
#print(url)
response = requests.get(url)  # Make a GET request to the URL
# Print status code (and associated text)
print(f"Data Request returned {response.status_code} : '{response.reason}'")
# Print data returned (parsing as JSON)
payload = response.json()  # Parse `response.text` into JSON
</pre>
<pre data-executable>
data=pd.json_normalize(payload['data'])
selected=data[["datetext", "counttext","location.formattedAddress"]]
print('Dataset feactched as selected dataframe')
#print(selected)
#list(selected.columns.values)
filtedVals= selected[selected['location.formattedAddress'].str.contains('Nuwara Eliya, Sri Lanka')]
print('By defult Nuwara Eliya District selected')
print('For other district select it form the dropdown below >>>')
def f(x):
    print("District changed to %s" % x)
    filtedVals=selected[selected['location.formattedAddress'].str.contains(x)]
    print(filtedVals)
    pivoted = pd.DataFrame(filtedVals.pivot_table(values='counttext', index='datetext', columns='location.formattedAddress', aggfunc='sum'))
    return pivoted
interact(f, x=['Nuwara Eliya, Sri Lanka', 'Badulla, Sri Lanka', 'Kurunegala, Sri Lanka']);
</pre>
<pre data-executable>
import numpy as np
x = np.random.uniform(0, 5, size=100)
ep = np.random.normal(size=100)
y = 2*x + ep
x_values = np.linspace(0, 5, 1000)
def slope_viz(m=1):
    plt.scatter(x, y)
    plt.plot(x_values, m*x_values, lw=3, color='black')
    plt.ylim(-1.2, 12.2);
widgets.interact(slope_viz, m=[0, 1, 2, 3, 4]);
</pre>
 <script src="_static/juniper.min.js"></script>
 <script>new Juniper({ repo: 'GenoTechies/spacy-io-binder',isolateCells:false })</script>
  </body>
</html>
<!-- 
https://github.com/executablebooks/thebe/blob/65800aa141f708476e953c080f12ebbadcf8dd2d/docs/_static/html_examples/demo-status-widget.html -->