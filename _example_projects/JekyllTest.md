```python
import pandas as pd
import geopandas as gpd
from vega_datasets import data
import altair as alt
from ipywidgets import widgets, VBox, interactive_output

```


```python
df = pd.read_csv('https://raw.githubusercontent.com/UIUC-iSchool-DataViz/is445_data/main/bfro_reports_fall2022.csv')
```


```python
df
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
      <th>observed</th>
      <th>location_details</th>
      <th>county</th>
      <th>state</th>
      <th>season</th>
      <th>title</th>
      <th>latitude</th>
      <th>longitude</th>
      <th>date</th>
      <th>number</th>
      <th>...</th>
      <th>precip_intensity</th>
      <th>precip_probability</th>
      <th>precip_type</th>
      <th>pressure</th>
      <th>summary</th>
      <th>uv_index</th>
      <th>visibility</th>
      <th>wind_bearing</th>
      <th>wind_speed</th>
      <th>location</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Ed L. was salmon fishing with a companion in P...</td>
      <td>East side of Prince William Sound</td>
      <td>Valdez-Chitina-Whittier County</td>
      <td>Alaska</td>
      <td>Fall</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1261.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>heh i kinda feel a little dumb that im reporti...</td>
      <td>the road is off us rt 80, i dont know the exit...</td>
      <td>Warren County</td>
      <td>New Jersey</td>
      <td>Fall</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>438.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>I was on my way to Claremont from Lebanon on R...</td>
      <td>Close to Claremont down 120 not far from Kings...</td>
      <td>Sullivan County</td>
      <td>New Hampshire</td>
      <td>Summer</td>
      <td>Report 55269: Dawn sighting at Stevens Brook o...</td>
      <td>43.41549</td>
      <td>-72.33093</td>
      <td>2016-06-07</td>
      <td>55269.0</td>
      <td>...</td>
      <td>0.001</td>
      <td>0.7</td>
      <td>rain</td>
      <td>998.87</td>
      <td>Mostly cloudy throughout the day.</td>
      <td>6.0</td>
      <td>9.70</td>
      <td>262.0</td>
      <td>0.49</td>
      <td>POINT(-72.33093000000001 43.415490000000005)</td>
    </tr>
    <tr>
      <th>3</th>
      <td>I was northeast of Macy Nebraska along the Mis...</td>
      <td>Latitude &amp; Longitude :  42.158230  -96.344197</td>
      <td>Thurston County</td>
      <td>Nebraska</td>
      <td>Spring</td>
      <td>Report 59757: Possible daylight sighting of a ...</td>
      <td>42.15685</td>
      <td>-96.34203</td>
      <td>2018-05-25</td>
      <td>59757.0</td>
      <td>...</td>
      <td>0.000</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>1008.07</td>
      <td>Partly cloudy in the morning.</td>
      <td>10.0</td>
      <td>8.25</td>
      <td>193.0</td>
      <td>3.33</td>
      <td>POINT(-96.34203000000001 42.15685)</td>
    </tr>
    <tr>
      <th>4</th>
      <td>While this incident occurred a long time ago, ...</td>
      <td>Ward County, Just outside of a the Minuteman T...</td>
      <td>Ward County</td>
      <td>North Dakota</td>
      <td>Spring</td>
      <td>Report 751: Hunter describes described being s...</td>
      <td>48.25422</td>
      <td>-101.31660</td>
      <td>2000-04-21</td>
      <td>751.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>rain</td>
      <td>1011.47</td>
      <td>Partly cloudy until evening.</td>
      <td>6.0</td>
      <td>10.00</td>
      <td>237.0</td>
      <td>11.14</td>
      <td>POINT(-101.3166 48.254220000000004)</td>
    </tr>
    <tr>
      <th>...</th>
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
      <th>4742</th>
      <td>My cousin and I were camping way out in the wo...</td>
      <td>Indiana, Brown County, Elkinsville, Lake Monro...</td>
      <td>Brown County</td>
      <td>Indiana</td>
      <td>Spring</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2460.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4743</th>
      <td>While backpacking near the horse trails and ac...</td>
      <td>Near Bedford south of Brown County in the Hoos...</td>
      <td>Brown County</td>
      <td>Indiana</td>
      <td>Winter</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2461.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4744</th>
      <td>My wife and I were camping At Yellowood State ...</td>
      <td>Yellowood State Park. Off of highway 46 in bet...</td>
      <td>Brown County</td>
      <td>Indiana</td>
      <td>Summer</td>
      <td>Report 49480: Campers hear possible vocalizati...</td>
      <td>39.17909</td>
      <td>-86.33560</td>
      <td>2015-08-08</td>
      <td>49480.0</td>
      <td>...</td>
      <td>0.000</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>1014.02</td>
      <td>Mostly cloudy in the evening.</td>
      <td>9.0</td>
      <td>9.22</td>
      <td>256.0</td>
      <td>0.34</td>
      <td>POINT(-86.3356 39.17909)</td>
    </tr>
    <tr>
      <th>4745</th>
      <td>My wife and I were driving to Indianapolis to ...</td>
      <td>On Interstate 65 in Indiana somewhere around t...</td>
      <td>Boone County</td>
      <td>Indiana</td>
      <td>Winter</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2459.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4746</th>
      <td>It was about 7:00 PM in September. It was stil...</td>
      <td>Blackford County, Indiana located in the south...</td>
      <td>Blackford County</td>
      <td>Indiana</td>
      <td>Summer</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2458.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>4747 rows × 29 columns</p>
</div>




```python
df.columns
```




    Index(['observed', 'location_details', 'county', 'state', 'season', 'title',
           'latitude', 'longitude', 'date', 'number', 'classification', 'geohash',
           'temperature_high', 'temperature_mid', 'temperature_low', 'dew_point',
           'humidity', 'cloud_cover', 'moon_phase', 'precip_intensity',
           'precip_probability', 'precip_type', 'pressure', 'summary', 'uv_index',
           'visibility', 'wind_bearing', 'wind_speed', 'location'],
          dtype='object')




```python
df.state.unique()
```




    array(['Alaska', 'New Jersey', 'New Hampshire', 'Nebraska',
           'North Dakota', 'North Carolina', 'Montana', 'Missouri',
           'Minnesota', 'Michigan', 'Maine', 'Maryland', 'Massachusetts',
           'Louisiana', 'New Mexico', 'Mississippi', 'Wyoming',
           'West Virginia', 'Vermont', 'Virginia', 'Texas', 'South Dakota',
           'South Carolina', 'Rhode Island', 'Pennsylvania', 'Oregon',
           'Oklahoma', 'Ohio', 'New York', 'Tennessee', 'Utah', 'Washington',
           'Wisconsin', 'Nevada', 'Kentucky', 'Kansas', 'Indiana', 'Illinois',
           'Idaho', 'Georgia', 'Florida', 'Delaware', 'Connecticut',
           'Colorado', 'California', 'Arizona', 'Arkansas', 'Alabama', 'Iowa'],
          dtype=object)




```python
df_louisiana = df[df.state == 'Louisiana']
```


```python
df_arizona = df[df.state == 'Arizona']
```


```python
humid_concat = pd.concat([df_louisiana, df_arizona])
```


```python
humid_concat.isna().sum()
```




    observed               0
    location_details      18
    county                 0
    state                  0
    season                 0
    title                 30
    latitude              30
    longitude             30
    date                  30
    number                 0
    classification         0
    geohash               30
    temperature_high      55
    temperature_mid       58
    temperature_low       58
    dew_point             55
    humidity              55
    cloud_cover           69
    moon_phase            55
    precip_intensity      64
    precip_probability    64
    precip_type           99
    pressure              82
    summary               55
    uv_index              55
    visibility            67
    wind_bearing          55
    wind_speed            55
    location              30
    dtype: int64




```python
humid_clean = humid_concat[humid_concat['temperature_mid'].isna() == False]
```


```python
humid_long = humid_clean.melt(
    id_vars=['humidity', 'state'],
    value_vars=['temperature_high', 'temperature_mid', 'temperature_low'],
    var_name='temperature_type',
    value_name='temperature'
)

labels = {
    'temperature_high': 'High',
    'temperature_mid': 'Mid',
    'temperature_low': 'Low'
}

checkboxes = {
    key: widgets.Checkbox(value=True, description=label)
    for key, label in labels.items()
}

def update_plot(**kwargs):
    selected_types = [key for key, show in kwargs.items() if show]
    filtered_data = humid_long[humid_long['temperature_type'].isin(selected_types)]
    
    chart = alt.Chart(filtered_data).mark_circle().encode(
        x=alt.X('humidity:Q', title='Humidity', scale=alt.Scale(domain=[0, 1])),
        y=alt.Y('temperature:Q', title='Temperature', scale=alt.Scale(domain=[0, 120])),
        color=alt.Color('state:N', legend=alt.Legend(title="State")),
        shape=alt.Shape('temperature_type:N', legend=alt.Legend(title="Temperature Type"))
    ).properties(
        width=600,
        height=400,
        title="Interactive Temperature Chart"
    )
    
    display(chart)

widgets.interactive(update_plot, **checkboxes)
```




    interactive(children=(Checkbox(value=True, description='High'), Checkbox(value=True, description='Mid'), Check…




```python
chart = alt.Chart(humid_long).mark_circle().encode(
        x=alt.X('humidity:Q', title='Humidity', scale=alt.Scale(domain=[0, 1])),
        y=alt.Y('temperature:Q', title='Temperature', scale=alt.Scale(domain=[0, 120])),
        color=alt.Color('state:N', legend=alt.Legend(title="State")),
        shape=alt.Shape('temperature_type:N', legend=alt.Legend(title="Temperature Type"))
    ).properties(
        width=600,
        height=400,
        title="Interactive Temperature Chart"
    )
chart
```





<style>
  #altair-viz-389e760537af42028e5c35ceff1bfe02.vega-embed {
    width: 100%;
    display: flex;
  }

  #altair-viz-389e760537af42028e5c35ceff1bfe02.vega-embed details,
  #altair-viz-389e760537af42028e5c35ceff1bfe02.vega-embed details summary {
    position: relative;
  }
</style>
<div id="altair-viz-389e760537af42028e5c35ceff1bfe02"></div>
<script type="text/javascript">
  var VEGA_DEBUG = (typeof VEGA_DEBUG == "undefined") ? {} : VEGA_DEBUG;
  (function(spec, embedOpt){
    let outputDiv = document.currentScript.previousElementSibling;
    if (outputDiv.id !== "altair-viz-389e760537af42028e5c35ceff1bfe02") {
      outputDiv = document.getElementById("altair-viz-389e760537af42028e5c35ceff1bfe02");
    }
    const paths = {
      "vega": "https://cdn.jsdelivr.net/npm/vega@5?noext",
      "vega-lib": "https://cdn.jsdelivr.net/npm/vega-lib?noext",
      "vega-lite": "https://cdn.jsdelivr.net/npm/vega-lite@5.17.0?noext",
      "vega-embed": "https://cdn.jsdelivr.net/npm/vega-embed@6?noext",
    };

    function maybeLoadScript(lib, version) {
      var key = `${lib.replace("-", "")}_version`;
      return (VEGA_DEBUG[key] == version) ?
        Promise.resolve(paths[lib]) :
        new Promise(function(resolve, reject) {
          var s = document.createElement('script');
          document.getElementsByTagName("head")[0].appendChild(s);
          s.async = true;
          s.onload = () => {
            VEGA_DEBUG[key] = version;
            return resolve(paths[lib]);
          };
          s.onerror = () => reject(`Error loading script: ${paths[lib]}`);
          s.src = paths[lib];
        });
    }

    function showError(err) {
      outputDiv.innerHTML = `<div class="error" style="color:red;">${err}</div>`;
      throw err;
    }

    function displayChart(vegaEmbed) {
      vegaEmbed(outputDiv, spec, embedOpt)
        .catch(err => showError(`Javascript Error: ${err.message}<br>This usually means there's a typo in your chart specification. See the javascript console for the full traceback.`));
    }

    if(typeof define === "function" && define.amd) {
      requirejs.config({paths});
      require(["vega-embed"], displayChart, err => showError(`Error loading script: ${err.message}`));
    } else {
      maybeLoadScript("vega", "5")
        .then(() => maybeLoadScript("vega-lite", "5.17.0"))
        .then(() => maybeLoadScript("vega-embed", "6"))
        .catch(showError)
        .then(() => displayChart(vegaEmbed));
    }
  })({"config": {"view": {"continuousWidth": 300, "continuousHeight": 300}}, "data": {"name": "data-07d54132d3817e2a20e99f5061848946"}, "mark": {"type": "circle"}, "encoding": {"color": {"field": "state", "legend": {"title": "State"}, "type": "nominal"}, "shape": {"field": "temperature_type", "legend": {"title": "Temperature Type"}, "type": "nominal"}, "x": {"field": "humidity", "scale": {"domain": [0, 1]}, "title": "Humidity", "type": "quantitative"}, "y": {"field": "temperature", "scale": {"domain": [0, 120]}, "title": "Temperature", "type": "quantitative"}}, "height": 400, "title": "Interactive Temperature Chart", "width": 600, "$schema": "https://vega.github.io/schema/vega-lite/v5.17.0.json", "datasets": {"data-07d54132d3817e2a20e99f5061848946": [{"humidity": 0.77, "state": "Louisiana", "temperature_type": "temperature_high", "temperature": 88.09}, {"humidity": 0.67, "state": "Louisiana", "temperature_type": "temperature_high", "temperature": 86.43}, {"humidity": 0.73, "state": "Louisiana", "temperature_type": "temperature_high", "temperature": 73.63}, {"humidity": 0.95, "state": "Louisiana", "temperature_type": "temperature_high", "temperature": 79.9}, {"humidity": 0.8, "state": "Louisiana", "temperature_type": "temperature_high", "temperature": 85.67}, {"humidity": 0.83, "state": "Louisiana", "temperature_type": "temperature_high", "temperature": 76.05}, {"humidity": 0.63, "state": "Louisiana", "temperature_type": "temperature_high", "temperature": 73.08}, {"humidity": 0.88, "state": "Louisiana", "temperature_type": "temperature_high", "temperature": 69.22}, {"humidity": 0.66, "state": "Louisiana", "temperature_type": "temperature_high", "temperature": 94.08}, {"humidity": 0.85, "state": "Louisiana", "temperature_type": "temperature_high", "temperature": 76.98}, {"humidity": 0.55, "state": "Louisiana", "temperature_type": "temperature_high", "temperature": 48.45}, {"humidity": 0.91, "state": "Louisiana", "temperature_type": "temperature_high", "temperature": 71.05}, {"humidity": 0.95, "state": "Louisiana", "temperature_type": "temperature_high", "temperature": 39.67}, {"humidity": 0.74, "state": "Louisiana", "temperature_type": "temperature_high", "temperature": 53.29}, {"humidity": 0.66, "state": "Louisiana", "temperature_type": "temperature_high", "temperature": 94.38}, {"humidity": 0.62, "state": "Louisiana", "temperature_type": "temperature_high", "temperature": 95.62}, {"humidity": 0.69, "state": "Louisiana", "temperature_type": "temperature_high", "temperature": 84.78}, {"humidity": 0.75, "state": "Louisiana", "temperature_type": "temperature_high", "temperature": 87.59}, {"humidity": 0.63, "state": "Louisiana", "temperature_type": "temperature_high", "temperature": 93.89}, {"humidity": 0.78, "state": "Louisiana", "temperature_type": "temperature_high", "temperature": 97.99}, {"humidity": 0.86, "state": "Louisiana", "temperature_type": "temperature_high", "temperature": 71.16}, {"humidity": 0.75, "state": "Louisiana", "temperature_type": "temperature_high", "temperature": 83.21}, {"humidity": 0.72, "state": "Arizona", "temperature_type": "temperature_high", "temperature": 79.57}, {"humidity": 0.13, "state": "Arizona", "temperature_type": "temperature_high", "temperature": 97.62}, {"humidity": 0.42, "state": "Arizona", "temperature_type": "temperature_high", "temperature": 52.01}, {"humidity": 0.32, "state": "Arizona", "temperature_type": "temperature_high", "temperature": 84.61}, {"humidity": 0.25, "state": "Arizona", "temperature_type": "temperature_high", "temperature": 97.65}, {"humidity": 0.72, "state": "Arizona", "temperature_type": "temperature_high", "temperature": 53.72}, {"humidity": 0.54, "state": "Arizona", "temperature_type": "temperature_high", "temperature": 45.34}, {"humidity": 0.32, "state": "Arizona", "temperature_type": "temperature_high", "temperature": 81.24}, {"humidity": 0.64, "state": "Arizona", "temperature_type": "temperature_high", "temperature": 45.21}, {"humidity": 0.75, "state": "Arizona", "temperature_type": "temperature_high", "temperature": 34.33}, {"humidity": 0.44, "state": "Arizona", "temperature_type": "temperature_high", "temperature": 77.88}, {"humidity": 0.32, "state": "Arizona", "temperature_type": "temperature_high", "temperature": 79.43}, {"humidity": 0.64, "state": "Arizona", "temperature_type": "temperature_high", "temperature": 73.59}, {"humidity": 0.46, "state": "Arizona", "temperature_type": "temperature_high", "temperature": 56.54}, {"humidity": 0.34, "state": "Arizona", "temperature_type": "temperature_high", "temperature": 69.17}, {"humidity": 0.38, "state": "Arizona", "temperature_type": "temperature_high", "temperature": 68.59}, {"humidity": 0.28, "state": "Arizona", "temperature_type": "temperature_high", "temperature": 72.85}, {"humidity": 0.25, "state": "Arizona", "temperature_type": "temperature_high", "temperature": 74.03}, {"humidity": 0.31, "state": "Arizona", "temperature_type": "temperature_high", "temperature": 56.49}, {"humidity": 0.48, "state": "Arizona", "temperature_type": "temperature_high", "temperature": 81.98}, {"humidity": 0.48, "state": "Arizona", "temperature_type": "temperature_high", "temperature": 84.63}, {"humidity": 0.95, "state": "Arizona", "temperature_type": "temperature_high", "temperature": 64.8}, {"humidity": 0.38, "state": "Arizona", "temperature_type": "temperature_high", "temperature": 62.74}, {"humidity": 0.95, "state": "Arizona", "temperature_type": "temperature_high", "temperature": 69.14}, {"humidity": 0.49, "state": "Arizona", "temperature_type": "temperature_high", "temperature": 87.56}, {"humidity": 0.67, "state": "Arizona", "temperature_type": "temperature_high", "temperature": 73.98}, {"humidity": 0.35, "state": "Arizona", "temperature_type": "temperature_high", "temperature": 73.96}, {"humidity": 0.6, "state": "Arizona", "temperature_type": "temperature_high", "temperature": 49.53}, {"humidity": 0.31, "state": "Arizona", "temperature_type": "temperature_high", "temperature": 78.78}, {"humidity": 0.28, "state": "Arizona", "temperature_type": "temperature_high", "temperature": 67.06}, {"humidity": 0.77, "state": "Arizona", "temperature_type": "temperature_high", "temperature": 77.45}, {"humidity": 0.53, "state": "Arizona", "temperature_type": "temperature_high", "temperature": 76.67}, {"humidity": 0.41, "state": "Arizona", "temperature_type": "temperature_high", "temperature": 84.33}, {"humidity": 0.15, "state": "Arizona", "temperature_type": "temperature_high", "temperature": 70.22}, {"humidity": 0.84, "state": "Arizona", "temperature_type": "temperature_high", "temperature": 44.12}, {"humidity": 0.68, "state": "Arizona", "temperature_type": "temperature_high", "temperature": 72.08}, {"humidity": 0.16, "state": "Arizona", "temperature_type": "temperature_high", "temperature": 76.22}, {"humidity": 0.47, "state": "Arizona", "temperature_type": "temperature_high", "temperature": 82.66}, {"humidity": 0.16, "state": "Arizona", "temperature_type": "temperature_high", "temperature": 106.51}, {"humidity": 0.59, "state": "Arizona", "temperature_type": "temperature_high", "temperature": 61.66}, {"humidity": 0.31, "state": "Arizona", "temperature_type": "temperature_high", "temperature": 63.28}, {"humidity": 0.42, "state": "Arizona", "temperature_type": "temperature_high", "temperature": 51.65}, {"humidity": 0.22, "state": "Arizona", "temperature_type": "temperature_high", "temperature": 79.31}, {"humidity": 0.32, "state": "Arizona", "temperature_type": "temperature_high", "temperature": 73.68}, {"humidity": 0.77, "state": "Louisiana", "temperature_type": "temperature_mid", "temperature": 80.685}, {"humidity": 0.67, "state": "Louisiana", "temperature_type": "temperature_mid", "temperature": 76.09}, {"humidity": 0.73, "state": "Louisiana", "temperature_type": "temperature_mid", "temperature": 66.705}, {"humidity": 0.95, "state": "Louisiana", "temperature_type": "temperature_mid", "temperature": 74.32}, {"humidity": 0.8, "state": "Louisiana", "temperature_type": "temperature_mid", "temperature": 71.595}, {"humidity": 0.83, "state": "Louisiana", "temperature_type": "temperature_mid", "temperature": 69.13}, {"humidity": 0.63, "state": "Louisiana", "temperature_type": "temperature_mid", "temperature": 61.51}, {"humidity": 0.88, "state": "Louisiana", "temperature_type": "temperature_mid", "temperature": 65.265}, {"humidity": 0.66, "state": "Louisiana", "temperature_type": "temperature_mid", "temperature": 83.08}, {"humidity": 0.85, "state": "Louisiana", "temperature_type": "temperature_mid", "temperature": 66.8}, {"humidity": 0.55, "state": "Louisiana", "temperature_type": "temperature_mid", "temperature": 37.285}, {"humidity": 0.91, "state": "Louisiana", "temperature_type": "temperature_mid", "temperature": 62.44}, {"humidity": 0.95, "state": "Louisiana", "temperature_type": "temperature_mid", "temperature": 38.370000000000005}, {"humidity": 0.74, "state": "Louisiana", "temperature_type": "temperature_mid", "temperature": 42.545}, {"humidity": 0.66, "state": "Louisiana", "temperature_type": "temperature_mid", "temperature": 84.015}, {"humidity": 0.62, "state": "Louisiana", "temperature_type": "temperature_mid", "temperature": 84.74000000000001}, {"humidity": 0.69, "state": "Louisiana", "temperature_type": "temperature_mid", "temperature": 75.875}, {"humidity": 0.75, "state": "Louisiana", "temperature_type": "temperature_mid", "temperature": 78.795}, {"humidity": 0.63, "state": "Louisiana", "temperature_type": "temperature_mid", "temperature": 83.39}, {"humidity": 0.78, "state": "Louisiana", "temperature_type": "temperature_mid", "temperature": 83.755}, {"humidity": 0.86, "state": "Louisiana", "temperature_type": "temperature_mid", "temperature": 66.655}, {"humidity": 0.75, "state": "Louisiana", "temperature_type": "temperature_mid", "temperature": 70.245}, {"humidity": 0.72, "state": "Arizona", "temperature_type": "temperature_mid", "temperature": 65.53999999999999}, {"humidity": 0.13, "state": "Arizona", "temperature_type": "temperature_mid", "temperature": 79.285}, {"humidity": 0.42, "state": "Arizona", "temperature_type": "temperature_mid", "temperature": 38.865}, {"humidity": 0.32, "state": "Arizona", "temperature_type": "temperature_mid", "temperature": 72.15}, {"humidity": 0.25, "state": "Arizona", "temperature_type": "temperature_mid", "temperature": 81.71000000000001}, {"humidity": 0.72, "state": "Arizona", "temperature_type": "temperature_mid", "temperature": 46.505}, {"humidity": 0.54, "state": "Arizona", "temperature_type": "temperature_mid", "temperature": 28.425000000000004}, {"humidity": 0.32, "state": "Arizona", "temperature_type": "temperature_mid", "temperature": 58.635}, {"humidity": 0.64, "state": "Arizona", "temperature_type": "temperature_mid", "temperature": 37.175}, {"humidity": 0.75, "state": "Arizona", "temperature_type": "temperature_mid", "temperature": 23.535}, {"humidity": 0.44, "state": "Arizona", "temperature_type": "temperature_mid", "temperature": 69.875}, {"humidity": 0.32, "state": "Arizona", "temperature_type": "temperature_mid", "temperature": 65.275}, {"humidity": 0.64, "state": "Arizona", "temperature_type": "temperature_mid", "temperature": 57.57}, {"humidity": 0.46, "state": "Arizona", "temperature_type": "temperature_mid", "temperature": 43.59}, {"humidity": 0.34, "state": "Arizona", "temperature_type": "temperature_mid", "temperature": 57.965}, {"humidity": 0.38, "state": "Arizona", "temperature_type": "temperature_mid", "temperature": 52.735}, {"humidity": 0.28, "state": "Arizona", "temperature_type": "temperature_mid", "temperature": 62.65}, {"humidity": 0.25, "state": "Arizona", "temperature_type": "temperature_mid", "temperature": 62.635000000000005}, {"humidity": 0.31, "state": "Arizona", "temperature_type": "temperature_mid", "temperature": 44.655}, {"humidity": 0.48, "state": "Arizona", "temperature_type": "temperature_mid", "temperature": 69.035}, {"humidity": 0.48, "state": "Arizona", "temperature_type": "temperature_mid", "temperature": 73.675}, {"humidity": 0.95, "state": "Arizona", "temperature_type": "temperature_mid", "temperature": 57.07}, {"humidity": 0.38, "state": "Arizona", "temperature_type": "temperature_mid", "temperature": 52.025000000000006}, {"humidity": 0.95, "state": "Arizona", "temperature_type": "temperature_mid", "temperature": 63.760000000000005}, {"humidity": 0.49, "state": "Arizona", "temperature_type": "temperature_mid", "temperature": 75.325}, {"humidity": 0.67, "state": "Arizona", "temperature_type": "temperature_mid", "temperature": 60.650000000000006}, {"humidity": 0.35, "state": "Arizona", "temperature_type": "temperature_mid", "temperature": 57.46}, {"humidity": 0.6, "state": "Arizona", "temperature_type": "temperature_mid", "temperature": 36.870000000000005}, {"humidity": 0.31, "state": "Arizona", "temperature_type": "temperature_mid", "temperature": 63.135000000000005}, {"humidity": 0.28, "state": "Arizona", "temperature_type": "temperature_mid", "temperature": 52.64}, {"humidity": 0.77, "state": "Arizona", "temperature_type": "temperature_mid", "temperature": 63.795}, {"humidity": 0.53, "state": "Arizona", "temperature_type": "temperature_mid", "temperature": 64.06}, {"humidity": 0.41, "state": "Arizona", "temperature_type": "temperature_mid", "temperature": 72.13}, {"humidity": 0.15, "state": "Arizona", "temperature_type": "temperature_mid", "temperature": 59.27}, {"humidity": 0.84, "state": "Arizona", "temperature_type": "temperature_mid", "temperature": 35.855}, {"humidity": 0.68, "state": "Arizona", "temperature_type": "temperature_mid", "temperature": 56.845}, {"humidity": 0.16, "state": "Arizona", "temperature_type": "temperature_mid", "temperature": 59.36}, {"humidity": 0.47, "state": "Arizona", "temperature_type": "temperature_mid", "temperature": 71.57}, {"humidity": 0.16, "state": "Arizona", "temperature_type": "temperature_mid", "temperature": 93.7}, {"humidity": 0.59, "state": "Arizona", "temperature_type": "temperature_mid", "temperature": 55.305}, {"humidity": 0.31, "state": "Arizona", "temperature_type": "temperature_mid", "temperature": 47.09}, {"humidity": 0.42, "state": "Arizona", "temperature_type": "temperature_mid", "temperature": 40.18}, {"humidity": 0.22, "state": "Arizona", "temperature_type": "temperature_mid", "temperature": 66.72}, {"humidity": 0.32, "state": "Arizona", "temperature_type": "temperature_mid", "temperature": 60.38}, {"humidity": 0.77, "state": "Louisiana", "temperature_type": "temperature_low", "temperature": 73.28}, {"humidity": 0.67, "state": "Louisiana", "temperature_type": "temperature_low", "temperature": 65.75}, {"humidity": 0.73, "state": "Louisiana", "temperature_type": "temperature_low", "temperature": 59.78}, {"humidity": 0.95, "state": "Louisiana", "temperature_type": "temperature_low", "temperature": 68.74}, {"humidity": 0.8, "state": "Louisiana", "temperature_type": "temperature_low", "temperature": 57.52}, {"humidity": 0.83, "state": "Louisiana", "temperature_type": "temperature_low", "temperature": 62.21}, {"humidity": 0.63, "state": "Louisiana", "temperature_type": "temperature_low", "temperature": 49.94}, {"humidity": 0.88, "state": "Louisiana", "temperature_type": "temperature_low", "temperature": 61.31}, {"humidity": 0.66, "state": "Louisiana", "temperature_type": "temperature_low", "temperature": 72.08}, {"humidity": 0.85, "state": "Louisiana", "temperature_type": "temperature_low", "temperature": 56.62}, {"humidity": 0.55, "state": "Louisiana", "temperature_type": "temperature_low", "temperature": 26.12}, {"humidity": 0.91, "state": "Louisiana", "temperature_type": "temperature_low", "temperature": 53.83}, {"humidity": 0.95, "state": "Louisiana", "temperature_type": "temperature_low", "temperature": 37.07}, {"humidity": 0.74, "state": "Louisiana", "temperature_type": "temperature_low", "temperature": 31.8}, {"humidity": 0.66, "state": "Louisiana", "temperature_type": "temperature_low", "temperature": 73.65}, {"humidity": 0.62, "state": "Louisiana", "temperature_type": "temperature_low", "temperature": 73.86}, {"humidity": 0.69, "state": "Louisiana", "temperature_type": "temperature_low", "temperature": 66.97}, {"humidity": 0.75, "state": "Louisiana", "temperature_type": "temperature_low", "temperature": 70.0}, {"humidity": 0.63, "state": "Louisiana", "temperature_type": "temperature_low", "temperature": 72.89}, {"humidity": 0.78, "state": "Louisiana", "temperature_type": "temperature_low", "temperature": 69.52}, {"humidity": 0.86, "state": "Louisiana", "temperature_type": "temperature_low", "temperature": 62.15}, {"humidity": 0.75, "state": "Louisiana", "temperature_type": "temperature_low", "temperature": 57.28}, {"humidity": 0.72, "state": "Arizona", "temperature_type": "temperature_low", "temperature": 51.51}, {"humidity": 0.13, "state": "Arizona", "temperature_type": "temperature_low", "temperature": 60.95}, {"humidity": 0.42, "state": "Arizona", "temperature_type": "temperature_low", "temperature": 25.72}, {"humidity": 0.32, "state": "Arizona", "temperature_type": "temperature_low", "temperature": 59.69}, {"humidity": 0.25, "state": "Arizona", "temperature_type": "temperature_low", "temperature": 65.77}, {"humidity": 0.72, "state": "Arizona", "temperature_type": "temperature_low", "temperature": 39.29}, {"humidity": 0.54, "state": "Arizona", "temperature_type": "temperature_low", "temperature": 11.51}, {"humidity": 0.32, "state": "Arizona", "temperature_type": "temperature_low", "temperature": 36.03}, {"humidity": 0.64, "state": "Arizona", "temperature_type": "temperature_low", "temperature": 29.14}, {"humidity": 0.75, "state": "Arizona", "temperature_type": "temperature_low", "temperature": 12.74}, {"humidity": 0.44, "state": "Arizona", "temperature_type": "temperature_low", "temperature": 61.87}, {"humidity": 0.32, "state": "Arizona", "temperature_type": "temperature_low", "temperature": 51.12}, {"humidity": 0.64, "state": "Arizona", "temperature_type": "temperature_low", "temperature": 41.55}, {"humidity": 0.46, "state": "Arizona", "temperature_type": "temperature_low", "temperature": 30.64}, {"humidity": 0.34, "state": "Arizona", "temperature_type": "temperature_low", "temperature": 46.76}, {"humidity": 0.38, "state": "Arizona", "temperature_type": "temperature_low", "temperature": 36.88}, {"humidity": 0.28, "state": "Arizona", "temperature_type": "temperature_low", "temperature": 52.45}, {"humidity": 0.25, "state": "Arizona", "temperature_type": "temperature_low", "temperature": 51.24}, {"humidity": 0.31, "state": "Arizona", "temperature_type": "temperature_low", "temperature": 32.82}, {"humidity": 0.48, "state": "Arizona", "temperature_type": "temperature_low", "temperature": 56.09}, {"humidity": 0.48, "state": "Arizona", "temperature_type": "temperature_low", "temperature": 62.72}, {"humidity": 0.95, "state": "Arizona", "temperature_type": "temperature_low", "temperature": 49.34}, {"humidity": 0.38, "state": "Arizona", "temperature_type": "temperature_low", "temperature": 41.31}, {"humidity": 0.95, "state": "Arizona", "temperature_type": "temperature_low", "temperature": 58.38}, {"humidity": 0.49, "state": "Arizona", "temperature_type": "temperature_low", "temperature": 63.09}, {"humidity": 0.67, "state": "Arizona", "temperature_type": "temperature_low", "temperature": 47.32}, {"humidity": 0.35, "state": "Arizona", "temperature_type": "temperature_low", "temperature": 40.96}, {"humidity": 0.6, "state": "Arizona", "temperature_type": "temperature_low", "temperature": 24.21}, {"humidity": 0.31, "state": "Arizona", "temperature_type": "temperature_low", "temperature": 47.49}, {"humidity": 0.28, "state": "Arizona", "temperature_type": "temperature_low", "temperature": 38.22}, {"humidity": 0.77, "state": "Arizona", "temperature_type": "temperature_low", "temperature": 50.14}, {"humidity": 0.53, "state": "Arizona", "temperature_type": "temperature_low", "temperature": 51.45}, {"humidity": 0.41, "state": "Arizona", "temperature_type": "temperature_low", "temperature": 59.93}, {"humidity": 0.15, "state": "Arizona", "temperature_type": "temperature_low", "temperature": 48.32}, {"humidity": 0.84, "state": "Arizona", "temperature_type": "temperature_low", "temperature": 27.59}, {"humidity": 0.68, "state": "Arizona", "temperature_type": "temperature_low", "temperature": 41.61}, {"humidity": 0.16, "state": "Arizona", "temperature_type": "temperature_low", "temperature": 42.5}, {"humidity": 0.47, "state": "Arizona", "temperature_type": "temperature_low", "temperature": 60.48}, {"humidity": 0.16, "state": "Arizona", "temperature_type": "temperature_low", "temperature": 80.89}, {"humidity": 0.59, "state": "Arizona", "temperature_type": "temperature_low", "temperature": 48.95}, {"humidity": 0.31, "state": "Arizona", "temperature_type": "temperature_low", "temperature": 30.9}, {"humidity": 0.42, "state": "Arizona", "temperature_type": "temperature_low", "temperature": 28.71}, {"humidity": 0.22, "state": "Arizona", "temperature_type": "temperature_low", "temperature": 54.13}, {"humidity": 0.32, "state": "Arizona", "temperature_type": "temperature_low", "temperature": 47.08}]}}, {"mode": "vega-lite"});
</script>




```python
chart.properties(width = 'container').save('humidity.json')
```

In this visualization, we are being shown the temperature differences between the most and least humid states. Arizona is the least humid state while Louisiana is a close second to the most humid state (I thought Alaska would skew the data a lot). I wanted to record if there were big temperature differences between humid and not humid states. I used the default colors because they are easy to tell apart and since there are only two points, I thought a color map would not be necessary. This is completely different from my HW 5 visualizations since it is a different data set. I thought the interactivity with the different min, max, and mids would show more trends better and you can choose which one you want to see, because there can be meaningful trends by finding max or min temps. Finally, I used a little ChatGPT to help me with this code since I was unsure about how to do check boxes, here were my prompts and responses, I fact checked it with my data to see if it would work:

how to do ipywidgets checkboxes interactively witha  graph

what if i want to do 3 or more

Here is the code I was given as an example


```python
# Sample data
functions = {
    "Sin(x)": np.sin(x),
    "Cos(x)": np.cos(x),
    "Tan(x)": np.tan(x),
    "Sin(x)^2": np.sin(x)**2,
    "Cos(x)^2": np.cos(x)**2
}

# Generate checkboxes dynamically
checkboxes = {name: widgets.Checkbox(value=True, description=name) for name in functions}

# Function to update the plot dynamically
def update_plot(**kwargs):
    plt.figure(figsize=(8, 5))
    for name, show in kwargs.items():
        if show:
            plt.plot(x, functions[name], label=name)
    plt.legend()
    plt.xlabel("x")
    plt.ylabel("y")
    plt.title("Interactive Trigonometric Functions")
    plt.grid(True)
    plt.show()

# Create interactive widget with dynamic checkboxes
interactive_plot = widgets.interactive(update_plot, **checkboxes)

# Display checkboxes and plot
display(widgets.VBox(list(checkboxes.values())))
interactive_plot

```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    Cell In[13], line 3
          1 # Sample data
          2 functions = {
    ----> 3     "Sin(x)": np.sin(x),
          4     "Cos(x)": np.cos(x),
          5     "Tan(x)": np.tan(x),
          6     "Sin(x)^2": np.sin(x)**2,
          7     "Cos(x)^2": np.cos(x)**2
          8 }
         10 # Generate checkboxes dynamically
         11 checkboxes = {name: widgets.Checkbox(value=True, description=name) for name in functions}
    

    NameError: name 'np' is not defined



```python
df.columns
```




    Index(['observed', 'location_details', 'county', 'state', 'season', 'title',
           'latitude', 'longitude', 'date', 'number', 'classification', 'geohash',
           'temperature_high', 'temperature_mid', 'temperature_low', 'dew_point',
           'humidity', 'cloud_cover', 'moon_phase', 'precip_intensity',
           'precip_probability', 'precip_type', 'pressure', 'summary', 'uv_index',
           'visibility', 'wind_bearing', 'wind_speed', 'location'],
          dtype='object')




```python
df_nebraska = df[df.state == 'Nebraska']
```


```python
df_mississippi = df[df.state == 'Mississippi']
```


```python
wind_concat = pd.concat([df_mississippi, df_nebraska])
```


```python
wind_concat.isna().sum()
```




    observed               1
    location_details       8
    county                 0
    state                  0
    season                 0
    title                  2
    latitude               2
    longitude              2
    date                   2
    number                 0
    classification         0
    geohash                2
    temperature_high       9
    temperature_mid       11
    temperature_low       11
    dew_point              9
    humidity               9
    cloud_cover           11
    moon_phase             8
    precip_intensity      14
    precip_probability    14
    precip_type           25
    pressure              14
    summary                8
    uv_index               8
    visibility            12
    wind_bearing           8
    wind_speed             8
    location               2
    dtype: int64




```python
wind_clean = wind_concat[wind_concat['temperature_mid'].isna() == False]
```


```python
wind_long = wind_clean.melt(
    id_vars=['wind_speed', 'state'],
    value_vars=['temperature_high', 'temperature_mid', 'temperature_low'],
    var_name='temperature_type',
    value_name='temperature'
)

labels = {
    'temperature_high': 'High',
    'temperature_mid': 'Mid',
    'temperature_low': 'Low'
}

checkboxes = {
    key: widgets.Checkbox(value=True, description=label)
    for key, label in labels.items()
}

def update_plot(**kwargs):
    selected_types = [key for key, show in kwargs.items() if show]
    filtered_data = wind_long[wind_long['temperature_type'].isin(selected_types)]
    
    chart = alt.Chart(filtered_data).mark_circle().encode(
        x=alt.X('wind_speed:Q', title='Wind Speed', scale=alt.Scale(domain=[0, 15])),
        y=alt.Y('temperature:Q', title='Temperature', scale=alt.Scale(domain=[0, 120])),
        color=alt.Color('state:N', legend=alt.Legend(title="State")),
        shape=alt.Shape('temperature_type:N', legend=alt.Legend(title="Temperature Type"))
    ).properties(
        width=600,
        height=400,
        title="Interactive Temperature Chart"
    )
    
    display(chart)

widgets.interactive(update_plot, **checkboxes)
```




    interactive(children=(Checkbox(value=True, description='High'), Checkbox(value=True, description='Mid'), Check…




```python
chart2 = alt.Chart(wind_long).mark_circle().encode(
        x=alt.X('wind_speed:Q', title='Wind Speed', scale=alt.Scale(domain=[0, 15])),
        y=alt.Y('temperature:Q', title='Temperature', scale=alt.Scale(domain=[0, 120])),
        color=alt.Color('state:N', legend=alt.Legend(title="State")),
        shape=alt.Shape('temperature_type:N', legend=alt.Legend(title="Temperature Type"))
    ).properties(
        width=600,
        height=400,
        title="Interactive Temperature Chart"
    )
chart2
```





<style>
  #altair-viz-be7ce7cccb974f80925751485c8d42f2.vega-embed {
    width: 100%;
    display: flex;
  }

  #altair-viz-be7ce7cccb974f80925751485c8d42f2.vega-embed details,
  #altair-viz-be7ce7cccb974f80925751485c8d42f2.vega-embed details summary {
    position: relative;
  }
</style>
<div id="altair-viz-be7ce7cccb974f80925751485c8d42f2"></div>
<script type="text/javascript">
  var VEGA_DEBUG = (typeof VEGA_DEBUG == "undefined") ? {} : VEGA_DEBUG;
  (function(spec, embedOpt){
    let outputDiv = document.currentScript.previousElementSibling;
    if (outputDiv.id !== "altair-viz-be7ce7cccb974f80925751485c8d42f2") {
      outputDiv = document.getElementById("altair-viz-be7ce7cccb974f80925751485c8d42f2");
    }
    const paths = {
      "vega": "https://cdn.jsdelivr.net/npm/vega@5?noext",
      "vega-lib": "https://cdn.jsdelivr.net/npm/vega-lib?noext",
      "vega-lite": "https://cdn.jsdelivr.net/npm/vega-lite@5.17.0?noext",
      "vega-embed": "https://cdn.jsdelivr.net/npm/vega-embed@6?noext",
    };

    function maybeLoadScript(lib, version) {
      var key = `${lib.replace("-", "")}_version`;
      return (VEGA_DEBUG[key] == version) ?
        Promise.resolve(paths[lib]) :
        new Promise(function(resolve, reject) {
          var s = document.createElement('script');
          document.getElementsByTagName("head")[0].appendChild(s);
          s.async = true;
          s.onload = () => {
            VEGA_DEBUG[key] = version;
            return resolve(paths[lib]);
          };
          s.onerror = () => reject(`Error loading script: ${paths[lib]}`);
          s.src = paths[lib];
        });
    }

    function showError(err) {
      outputDiv.innerHTML = `<div class="error" style="color:red;">${err}</div>`;
      throw err;
    }

    function displayChart(vegaEmbed) {
      vegaEmbed(outputDiv, spec, embedOpt)
        .catch(err => showError(`Javascript Error: ${err.message}<br>This usually means there's a typo in your chart specification. See the javascript console for the full traceback.`));
    }

    if(typeof define === "function" && define.amd) {
      requirejs.config({paths});
      require(["vega-embed"], displayChart, err => showError(`Error loading script: ${err.message}`));
    } else {
      maybeLoadScript("vega", "5")
        .then(() => maybeLoadScript("vega-lite", "5.17.0"))
        .then(() => maybeLoadScript("vega-embed", "6"))
        .catch(showError)
        .then(() => displayChart(vegaEmbed));
    }
  })({"config": {"view": {"continuousWidth": 300, "continuousHeight": 300}}, "data": {"name": "data-e7ac6e233169fd1537663e0f7a8d63fb"}, "mark": {"type": "circle"}, "encoding": {"color": {"field": "state", "legend": {"title": "State"}, "type": "nominal"}, "shape": {"field": "temperature_type", "legend": {"title": "Temperature Type"}, "type": "nominal"}, "x": {"field": "wind_speed", "scale": {"domain": [0, 15]}, "title": "Wind Speed", "type": "quantitative"}, "y": {"field": "temperature", "scale": {"domain": [0, 120]}, "title": "Temperature", "type": "quantitative"}}, "height": 400, "title": "Interactive Temperature Chart", "width": 600, "$schema": "https://vega.github.io/schema/vega-lite/v5.17.0.json", "datasets": {"data-e7ac6e233169fd1537663e0f7a8d63fb": [{"wind_speed": 5.26, "state": "Mississippi", "temperature_type": "temperature_high", "temperature": 50.99}, {"wind_speed": 1.79, "state": "Mississippi", "temperature_type": "temperature_high", "temperature": 40.51}, {"wind_speed": 1.52, "state": "Mississippi", "temperature_type": "temperature_high", "temperature": 86.17}, {"wind_speed": 0.85, "state": "Mississippi", "temperature_type": "temperature_high", "temperature": 91.23}, {"wind_speed": 0.76, "state": "Mississippi", "temperature_type": "temperature_high", "temperature": 84.31}, {"wind_speed": 7.59, "state": "Mississippi", "temperature_type": "temperature_high", "temperature": 61.99}, {"wind_speed": 3.09, "state": "Mississippi", "temperature_type": "temperature_high", "temperature": 71.59}, {"wind_speed": 2.24, "state": "Mississippi", "temperature_type": "temperature_high", "temperature": 81.23}, {"wind_speed": 6.96, "state": "Mississippi", "temperature_type": "temperature_high", "temperature": 45.23}, {"wind_speed": 10.87, "state": "Mississippi", "temperature_type": "temperature_high", "temperature": 48.36}, {"wind_speed": 2.24, "state": "Mississippi", "temperature_type": "temperature_high", "temperature": 81.23}, {"wind_speed": 6.44, "state": "Mississippi", "temperature_type": "temperature_high", "temperature": 87.96}, {"wind_speed": 1.21, "state": "Mississippi", "temperature_type": "temperature_high", "temperature": 82.36}, {"wind_speed": 2.43, "state": "Mississippi", "temperature_type": "temperature_high", "temperature": 81.27}, {"wind_speed": 1.05, "state": "Mississippi", "temperature_type": "temperature_high", "temperature": 100.1}, {"wind_speed": 3.33, "state": "Nebraska", "temperature_type": "temperature_high", "temperature": 93.4}, {"wind_speed": 7.44, "state": "Nebraska", "temperature_type": "temperature_high", "temperature": 72.69}, {"wind_speed": 1.49, "state": "Nebraska", "temperature_type": "temperature_high", "temperature": 9.8}, {"wind_speed": 3.99, "state": "Nebraska", "temperature_type": "temperature_high", "temperature": 68.0}, {"wind_speed": 9.66, "state": "Nebraska", "temperature_type": "temperature_high", "temperature": 98.22}, {"wind_speed": 3.49, "state": "Nebraska", "temperature_type": "temperature_high", "temperature": 80.99}, {"wind_speed": 3.86, "state": "Nebraska", "temperature_type": "temperature_high", "temperature": 73.19}, {"wind_speed": 3.9, "state": "Nebraska", "temperature_type": "temperature_high", "temperature": 84.46}, {"wind_speed": 2.77, "state": "Nebraska", "temperature_type": "temperature_high", "temperature": 81.52}, {"wind_speed": 5.85, "state": "Nebraska", "temperature_type": "temperature_high", "temperature": 70.87}, {"wind_speed": 5.26, "state": "Mississippi", "temperature_type": "temperature_mid", "temperature": 42.36}, {"wind_speed": 1.79, "state": "Mississippi", "temperature_type": "temperature_mid", "temperature": 30.32}, {"wind_speed": 1.52, "state": "Mississippi", "temperature_type": "temperature_mid", "temperature": 77.715}, {"wind_speed": 0.85, "state": "Mississippi", "temperature_type": "temperature_mid", "temperature": 83.105}, {"wind_speed": 0.76, "state": "Mississippi", "temperature_type": "temperature_mid", "temperature": 78.345}, {"wind_speed": 7.59, "state": "Mississippi", "temperature_type": "temperature_mid", "temperature": 51.46}, {"wind_speed": 3.09, "state": "Mississippi", "temperature_type": "temperature_mid", "temperature": 57.58}, {"wind_speed": 2.24, "state": "Mississippi", "temperature_type": "temperature_mid", "temperature": 62.78}, {"wind_speed": 6.96, "state": "Mississippi", "temperature_type": "temperature_mid", "temperature": 42.06999999999999}, {"wind_speed": 10.87, "state": "Mississippi", "temperature_type": "temperature_mid", "temperature": 43.870000000000005}, {"wind_speed": 2.24, "state": "Mississippi", "temperature_type": "temperature_mid", "temperature": 62.78}, {"wind_speed": 6.44, "state": "Mississippi", "temperature_type": "temperature_mid", "temperature": 81.555}, {"wind_speed": 1.21, "state": "Mississippi", "temperature_type": "temperature_mid", "temperature": 62.06}, {"wind_speed": 2.43, "state": "Mississippi", "temperature_type": "temperature_mid", "temperature": 67.31}, {"wind_speed": 1.05, "state": "Mississippi", "temperature_type": "temperature_mid", "temperature": 88.08}, {"wind_speed": 3.33, "state": "Nebraska", "temperature_type": "temperature_mid", "temperature": 77.7}, {"wind_speed": 7.44, "state": "Nebraska", "temperature_type": "temperature_mid", "temperature": 68.19}, {"wind_speed": 1.49, "state": "Nebraska", "temperature_type": "temperature_mid", "temperature": 8.595}, {"wind_speed": 3.99, "state": "Nebraska", "temperature_type": "temperature_mid", "temperature": 52.025}, {"wind_speed": 9.66, "state": "Nebraska", "temperature_type": "temperature_mid", "temperature": 85.15}, {"wind_speed": 3.49, "state": "Nebraska", "temperature_type": "temperature_mid", "temperature": 68.735}, {"wind_speed": 3.86, "state": "Nebraska", "temperature_type": "temperature_mid", "temperature": 64.935}, {"wind_speed": 3.9, "state": "Nebraska", "temperature_type": "temperature_mid", "temperature": 68.75}, {"wind_speed": 2.77, "state": "Nebraska", "temperature_type": "temperature_mid", "temperature": 64.095}, {"wind_speed": 5.85, "state": "Nebraska", "temperature_type": "temperature_mid", "temperature": 50.635000000000005}, {"wind_speed": 5.26, "state": "Mississippi", "temperature_type": "temperature_low", "temperature": 33.73}, {"wind_speed": 1.79, "state": "Mississippi", "temperature_type": "temperature_low", "temperature": 20.13}, {"wind_speed": 1.52, "state": "Mississippi", "temperature_type": "temperature_low", "temperature": 69.26}, {"wind_speed": 0.85, "state": "Mississippi", "temperature_type": "temperature_low", "temperature": 74.98}, {"wind_speed": 0.76, "state": "Mississippi", "temperature_type": "temperature_low", "temperature": 72.38}, {"wind_speed": 7.59, "state": "Mississippi", "temperature_type": "temperature_low", "temperature": 40.93}, {"wind_speed": 3.09, "state": "Mississippi", "temperature_type": "temperature_low", "temperature": 43.57}, {"wind_speed": 2.24, "state": "Mississippi", "temperature_type": "temperature_low", "temperature": 44.33}, {"wind_speed": 6.96, "state": "Mississippi", "temperature_type": "temperature_low", "temperature": 38.91}, {"wind_speed": 10.87, "state": "Mississippi", "temperature_type": "temperature_low", "temperature": 39.38}, {"wind_speed": 2.24, "state": "Mississippi", "temperature_type": "temperature_low", "temperature": 44.33}, {"wind_speed": 6.44, "state": "Mississippi", "temperature_type": "temperature_low", "temperature": 75.15}, {"wind_speed": 1.21, "state": "Mississippi", "temperature_type": "temperature_low", "temperature": 41.76}, {"wind_speed": 2.43, "state": "Mississippi", "temperature_type": "temperature_low", "temperature": 53.35}, {"wind_speed": 1.05, "state": "Mississippi", "temperature_type": "temperature_low", "temperature": 76.06}, {"wind_speed": 3.33, "state": "Nebraska", "temperature_type": "temperature_low", "temperature": 62.0}, {"wind_speed": 7.44, "state": "Nebraska", "temperature_type": "temperature_low", "temperature": 63.69}, {"wind_speed": 1.49, "state": "Nebraska", "temperature_type": "temperature_low", "temperature": 7.39}, {"wind_speed": 3.99, "state": "Nebraska", "temperature_type": "temperature_low", "temperature": 36.05}, {"wind_speed": 9.66, "state": "Nebraska", "temperature_type": "temperature_low", "temperature": 72.08}, {"wind_speed": 3.49, "state": "Nebraska", "temperature_type": "temperature_low", "temperature": 56.48}, {"wind_speed": 3.86, "state": "Nebraska", "temperature_type": "temperature_low", "temperature": 56.68}, {"wind_speed": 3.9, "state": "Nebraska", "temperature_type": "temperature_low", "temperature": 53.04}, {"wind_speed": 2.77, "state": "Nebraska", "temperature_type": "temperature_low", "temperature": 46.67}, {"wind_speed": 5.85, "state": "Nebraska", "temperature_type": "temperature_low", "temperature": 30.4}]}}, {"mode": "vega-lite"});
</script>




```python
chart2.properties(width = 'container').save('wind.json')
```

I decided to go for a similar type of graph but this time I was comapring wind speeds. Surprisingly, Nebraska is supposed to have a higher average wind speen than Mississippi, but it seems to be even if not Mississippi having higher wind speeds than Nebraska. I think the data is jjust not representative of the actual states and next time I should just compare the variables within the dataset by grouping them and finding the average. I also tried looking for temperature differences on this one. Similar idea with the color map aas well since you can tell which colors are which on this one pretty easily. I did not do any data transformations but I did do some data cleaning for NA values. There is no overlap from this to Homework 5. 


```python

```
