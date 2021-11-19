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
 <script src="_static/juniper.min.js"></script>
 <script>new Juniper({ repo: 'GenoTechies/spacy-io-binder',isolateCells:false })</script>
  </body>
</html>
<!-- 
https://github.com/executablebooks/thebe/blob/65800aa141f708476e953c080f12ebbadcf8dd2d/docs/_static/html_examples/demo-status-widget.html -->