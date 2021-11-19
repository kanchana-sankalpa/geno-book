# Welcome to your Geno Book

This is a small step taken by Genotechies to allow knowleage generation based on data in Sri Lankan context
<html>
  <head>
    <title>An active web page</title>
<!--     <script type="text/x-thebe-config">
      {
        bootstrap: true,
        selector: "pre",
        requestKernel: true,
    binderOptions: {
        repo: "binder-examples/requirements",
        ref: "master",
    },
      }
    </script>
  <script src="https://unpkg.com/thebe@latest/lib/index.js"></script>
     <script >$.getScript("https://unpkg.com/thebe@latest")
    .done(function (script, textStatus) {
           thebelab.events.on("request-kernel")((kernel) => {
    // Find any cells with an initialization tag and ask Thebe to run them when ready
    kernel.requestExecute({code: "import numpy as np"})
    kernel.requestExecute({code: "import matplotlib.pyplot as plt"})
      });
    })
</script> -->
  </head>
  <body>
 part 1:
  <!--   <pre>
    %matplotlib inline
import ipywidgets as widgets
import requests  # Import the requests library
import pandas as pd
import matplotlib.pyplot as plt
import matplotlib as mpl
import seaborn as sns
    </pre>
    Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua:
    <pre data-executable="true">
x = np.linspace(0,10)
plt.plot(x, np.sin(x))
plt.plot(x, np.cos(x))
    </pre> -->
  <pre data-executable>
  !pip install pandas
  !pip install matplotlib
  !pip install seaborn
  !pip install ipywidgets
  from ipywidgets import interact, interactive, fixed, interact_manual
  import ipywidgets as widgets
  import requests  # Import the requests library
  import pandas as pd
  import matplotlib.pyplot as plt
  import matplotlib as mpl
  import seaborn as sns
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
    </pre>
    <pre data-executable>
    filtedVals= selected[selected['location.formattedAddress'].str.contains('Nuwara Eliya, Sri Lanka')]
    print('By defult Nuwara Eliya District selected')
    print('For other district select it form the dropdown below >>>')
    def f(x):
      print("District changed to %s" % x)
      filtedVals=selected[selected['location.formattedAddress'].str.contains(x)]
      print(filtedVals)
      pivoted = pd.DataFrame(filtedVals.pivot_table(values='counttext', index='datetext', columns='location.formattedAddress', aggfunc='sum'))
      return pivoted
    
    params = widgets.Dropdown(options= ['Nuwara Eliya, Sri Lanka', 'Badulla, Sri Lanka', 'Kurunegala, Sri Lanka'])
    c = widgets.IntSlider()
    ui = widgets.HBox([params])
    def f2(params):
      return params;
    
    out = widgets.interactive_output(f2, {'params': params})
    display(ui, out)
 </pre>
 <script src="_static/juniper.min.js"></script>
 
 <script>new Juniper({ repo: 'GenoTechies/spacy-io-binder',isolateCells:false })</script>
  </body>
</html>
<!-- 
https://github.com/executablebooks/thebe/blob/65800aa141f708476e953c080f12ebbadcf8dd2d/docs/_static/html_examples/demo-status-widget.html -->