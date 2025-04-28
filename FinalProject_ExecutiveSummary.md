# Final Project Executive Summary: Food Access in the United States

## Introduction

This project investigates disparities in food access across demographic and geographic lines using the USDA Food Access Research Atlas dataset. With a focus on equity, the analysis explores how access to SNAP benefits, household vehicles, and elderly populations affect health and community wellbeing, particularly in underserved areas.

---

## A Legacy of Food Insecurity and Structural Inequality

Many low-income and racially marginalized communities face persistent barriers to accessing healthy food. The data reflects systemic disparities, with indicators such as high SNAP use, low vehicle ownership, and high senior populations correlating with poor food access across specific states and tracts.

---

## Methodology

The dataset was cleaned, analyzed, and stored in a SQLite database. Queries using `SELECT`, `JOIN`, `WHERE`, and `BETWEEN` logic were used to extract insights. Two Jupyter notebooks (Assignments 1 and 2) include detailed Python and SQL workflows. Visualizations were generated using Matplotlib.

---

## Analysis

### Assignment 1

<a href="https://colab.research.google.com/github/omyahro/Data_200_Royals/blob/main/Assignment1_Food_Access.ipynb" target="_parent"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>

# **Do low-income, predominantly Black communities experience greater food access barriers than other racial groups?**

Supermarket access, economic conditions, and food assistance affect food availability across racial groups, highlighting inequalities in food security. Studying these factors can help address disparities and improve food access in underserved communities. The findings will highlight the disproportionate impact of food insecurity on Black communities and emphasize the need for policy interventions to address racial disparities in food access.




# **Problem Statement:**

Low-income, predominantly Black communities often experience significant barriers to accessing affordable and nutritious food. Many of these neighborhoods are classified as food deserts, where grocery stores are scarce, and fresh food options are limited. As a result, residents frequently rely on convenience stores and fast food, leading to higher rates of food insecurity and diet-related health issues.


# **Data Definition:**

The Food Access Research Atlas provides a geographic analysis of food accessibility in low-income and other census tracts using various measures of supermarket proximity. It includes data on food access for populations within these tracts and offers census-tract-level information that can be used for research or community planning.


https://catalog.data.gov/dataset/food-access-research-atlas



```python
# Import the libraries
import numpy as np                  # Scientific Computing
import pandas as pd                 # Data Analysis
import matplotlib.pyplot as plt     # Plotting
import seaborn as sns               # Statistical Data Visualization

# Let's make sure pandas returns all the rows and columns for the dataframe
pd.set_option('display.max_rows', None)
pd.set_option('display.max_columns', None)

# Force pandas to display full numbers instead of scientific notation
# pd.options.display.float_format = '{:.0f}'.format

# Library to suppress warnings
import warnings
warnings.filterwarnings('ignore')
```


```python
from google.colab import drive

# Mount Google Drive
drive.mount('/content/drive')

# Define the file path (adjust to your folder location)
file_path = "/content/drive/My Drive/Food_Access_Research_Atlas.csv"

# Read the Excel file
food_access = pd.read_csv(file_path)


```

    Mounted at /content/drive



```python
# Display the first seven rows of the dataframe
food_access.head(7)
```





  <div id="df-291a9f55-3750-46ce-be70-cdd9d0a92938" class="colab-df-container">
    <div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CensusTract</th>
      <th>State</th>
      <th>County</th>
      <th>Urban</th>
      <th>Pop2010</th>
      <th>OHU2010</th>
      <th>GroupQuartersFlag</th>
      <th>NUMGQTRS</th>
      <th>PCTGQTRS</th>
      <th>LILATracts_1And10</th>
      <th>LILATracts_halfAnd10</th>
      <th>LILATracts_1And20</th>
      <th>LILATracts_Vehicle</th>
      <th>HUNVFlag</th>
      <th>LowIncomeTracts</th>
      <th>PovertyRate</th>
      <th>MedianFamilyIncome</th>
      <th>LA1and10</th>
      <th>LAhalfand10</th>
      <th>LA1and20</th>
      <th>LATracts_half</th>
      <th>LATracts1</th>
      <th>LATracts10</th>
      <th>LATracts20</th>
      <th>LATractsVehicle_20</th>
      <th>LAPOP1_10</th>
      <th>LAPOP05_10</th>
      <th>LAPOP1_20</th>
      <th>LALOWI1_10</th>
      <th>LALOWI05_10</th>
      <th>LALOWI1_20</th>
      <th>lapophalf</th>
      <th>lapophalfshare</th>
      <th>lalowihalf</th>
      <th>lalowihalfshare</th>
      <th>lakidshalf</th>
      <th>lakidshalfshare</th>
      <th>laseniorshalf</th>
      <th>laseniorshalfshare</th>
      <th>lawhitehalf</th>
      <th>lawhitehalfshare</th>
      <th>lablackhalf</th>
      <th>lablackhalfshare</th>
      <th>laasianhalf</th>
      <th>laasianhalfshare</th>
      <th>lanhopihalf</th>
      <th>lanhopihalfshare</th>
      <th>laaianhalf</th>
      <th>laaianhalfshare</th>
      <th>laomultirhalf</th>
      <th>laomultirhalfshare</th>
      <th>lahisphalf</th>
      <th>lahisphalfshare</th>
      <th>lahunvhalf</th>
      <th>lahunvhalfshare</th>
      <th>lasnaphalf</th>
      <th>lasnaphalfshare</th>
      <th>lapop1</th>
      <th>lapop1share</th>
      <th>lalowi1</th>
      <th>lalowi1share</th>
      <th>lakids1</th>
      <th>lakids1share</th>
      <th>laseniors1</th>
      <th>laseniors1share</th>
      <th>lawhite1</th>
      <th>lawhite1share</th>
      <th>lablack1</th>
      <th>lablack1share</th>
      <th>laasian1</th>
      <th>laasian1share</th>
      <th>lanhopi1</th>
      <th>lanhopi1share</th>
      <th>laaian1</th>
      <th>laaian1share</th>
      <th>laomultir1</th>
      <th>laomultir1share</th>
      <th>lahisp1</th>
      <th>lahisp1share</th>
      <th>lahunv1</th>
      <th>lahunv1share</th>
      <th>lasnap1</th>
      <th>lasnap1share</th>
      <th>lapop10</th>
      <th>lapop10share</th>
      <th>lalowi10</th>
      <th>lalowi10share</th>
      <th>lakids10</th>
      <th>lakids10share</th>
      <th>laseniors10</th>
      <th>laseniors10share</th>
      <th>lawhite10</th>
      <th>lawhite10share</th>
      <th>lablack10</th>
      <th>lablack10share</th>
      <th>laasian10</th>
      <th>laasian10share</th>
      <th>lanhopi10</th>
      <th>lanhopi10share</th>
      <th>laaian10</th>
      <th>laaian10share</th>
      <th>laomultir10</th>
      <th>laomultir10share</th>
      <th>lahisp10</th>
      <th>lahisp10share</th>
      <th>lahunv10</th>
      <th>lahunv10share</th>
      <th>lasnap10</th>
      <th>lasnap10share</th>
      <th>lapop20</th>
      <th>lapop20share</th>
      <th>lalowi20</th>
      <th>lalowi20share</th>
      <th>lakids20</th>
      <th>lakids20share</th>
      <th>laseniors20</th>
      <th>laseniors20share</th>
      <th>lawhite20</th>
      <th>lawhite20share</th>
      <th>lablack20</th>
      <th>lablack20share</th>
      <th>laasian20</th>
      <th>laasian20share</th>
      <th>lanhopi20</th>
      <th>lanhopi20share</th>
      <th>laaian20</th>
      <th>laaian20share</th>
      <th>laomultir20</th>
      <th>laomultir20share</th>
      <th>lahisp20</th>
      <th>lahisp20share</th>
      <th>lahunv20</th>
      <th>lahunv20share</th>
      <th>lasnap20</th>
      <th>lasnap20share</th>
      <th>TractLOWI</th>
      <th>TractKids</th>
      <th>TractSeniors</th>
      <th>TractWhite</th>
      <th>TractBlack</th>
      <th>TractAsian</th>
      <th>TractNHOPI</th>
      <th>TractAIAN</th>
      <th>TractOMultir</th>
      <th>TractHispanic</th>
      <th>TractHUNV</th>
      <th>TractSNAP</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1001020100</td>
      <td>Alabama</td>
      <td>Autauga County</td>
      <td>1</td>
      <td>1912</td>
      <td>693</td>
      <td>0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>11.3</td>
      <td>81250.0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1896.0</td>
      <td>1912.0</td>
      <td>1896.0</td>
      <td>461.0</td>
      <td>467.0</td>
      <td>461.0</td>
      <td>1912.0</td>
      <td>100.00</td>
      <td>467.0</td>
      <td>24.42</td>
      <td>507.0</td>
      <td>26.52</td>
      <td>221.0</td>
      <td>11.56</td>
      <td>1622.0</td>
      <td>84.83</td>
      <td>217.0</td>
      <td>11.35</td>
      <td>14.0</td>
      <td>0.73</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>14.0</td>
      <td>0.73</td>
      <td>45.0</td>
      <td>2.35</td>
      <td>44.0</td>
      <td>2.30</td>
      <td>5.0</td>
      <td>0.79</td>
      <td>92.0</td>
      <td>13.33</td>
      <td>1896.0</td>
      <td>99.19</td>
      <td>461.0</td>
      <td>24.11</td>
      <td>504.0</td>
      <td>26.33</td>
      <td>219.0</td>
      <td>11.44</td>
      <td>1611.0</td>
      <td>84.26</td>
      <td>214.0</td>
      <td>11.17</td>
      <td>14.0</td>
      <td>0.72</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>14.0</td>
      <td>0.73</td>
      <td>44.0</td>
      <td>2.31</td>
      <td>43.0</td>
      <td>2.27</td>
      <td>5.0</td>
      <td>0.79</td>
      <td>92.0</td>
      <td>13.22</td>
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
      <td>NaN</td>
      <td>NaN</td>
      <td>455.0</td>
      <td>507.0</td>
      <td>221.0</td>
      <td>1622.0</td>
      <td>217.0</td>
      <td>14.0</td>
      <td>0.0</td>
      <td>14.0</td>
      <td>45.0</td>
      <td>44.0</td>
      <td>6.0</td>
      <td>102.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1001020200</td>
      <td>Alabama</td>
      <td>Autauga County</td>
      <td>1</td>
      <td>2170</td>
      <td>743</td>
      <td>0</td>
      <td>181.0</td>
      <td>8.34</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>17.9</td>
      <td>49000.0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1261.0</td>
      <td>2170.0</td>
      <td>1261.0</td>
      <td>604.0</td>
      <td>962.0</td>
      <td>604.0</td>
      <td>2170.0</td>
      <td>100.00</td>
      <td>962.0</td>
      <td>44.34</td>
      <td>606.0</td>
      <td>27.93</td>
      <td>214.0</td>
      <td>9.86</td>
      <td>888.0</td>
      <td>40.92</td>
      <td>1217.0</td>
      <td>56.08</td>
      <td>5.0</td>
      <td>0.23</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>5.0</td>
      <td>0.23</td>
      <td>55.0</td>
      <td>2.53</td>
      <td>75.0</td>
      <td>3.46</td>
      <td>93.0</td>
      <td>12.47</td>
      <td>161.0</td>
      <td>21.70</td>
      <td>1261.0</td>
      <td>58.11</td>
      <td>604.0</td>
      <td>27.83</td>
      <td>406.0</td>
      <td>18.69</td>
      <td>127.0</td>
      <td>5.83</td>
      <td>357.0</td>
      <td>16.43</td>
      <td>854.0</td>
      <td>39.36</td>
      <td>4.0</td>
      <td>0.18</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>4.0</td>
      <td>0.20</td>
      <td>42.0</td>
      <td>1.93</td>
      <td>33.0</td>
      <td>1.52</td>
      <td>67.0</td>
      <td>9.00</td>
      <td>96.0</td>
      <td>12.95</td>
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
      <td>NaN</td>
      <td>NaN</td>
      <td>802.0</td>
      <td>606.0</td>
      <td>214.0</td>
      <td>888.0</td>
      <td>1217.0</td>
      <td>5.0</td>
      <td>0.0</td>
      <td>5.0</td>
      <td>55.0</td>
      <td>75.0</td>
      <td>89.0</td>
      <td>156.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1001020300</td>
      <td>Alabama</td>
      <td>Autauga County</td>
      <td>1</td>
      <td>3373</td>
      <td>1256</td>
      <td>0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>15.0</td>
      <td>62609.0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1552.0</td>
      <td>2857.0</td>
      <td>1552.0</td>
      <td>478.0</td>
      <td>971.0</td>
      <td>478.0</td>
      <td>2857.0</td>
      <td>84.70</td>
      <td>971.0</td>
      <td>28.79</td>
      <td>771.0</td>
      <td>22.86</td>
      <td>358.0</td>
      <td>10.60</td>
      <td>2177.0</td>
      <td>64.53</td>
      <td>554.0</td>
      <td>16.43</td>
      <td>10.0</td>
      <td>0.30</td>
      <td>1.0</td>
      <td>0.03</td>
      <td>10.0</td>
      <td>0.30</td>
      <td>105.0</td>
      <td>3.10</td>
      <td>78.0</td>
      <td>2.30</td>
      <td>39.0</td>
      <td>3.09</td>
      <td>139.0</td>
      <td>11.05</td>
      <td>1552.0</td>
      <td>46.00</td>
      <td>478.0</td>
      <td>14.18</td>
      <td>416.0</td>
      <td>12.34</td>
      <td>201.0</td>
      <td>5.96</td>
      <td>1242.0</td>
      <td>36.81</td>
      <td>255.0</td>
      <td>7.56</td>
      <td>8.0</td>
      <td>0.24</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>2.0</td>
      <td>0.06</td>
      <td>45.0</td>
      <td>1.33</td>
      <td>36.0</td>
      <td>1.08</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>74.0</td>
      <td>5.87</td>
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
      <td>NaN</td>
      <td>NaN</td>
      <td>1306.0</td>
      <td>894.0</td>
      <td>439.0</td>
      <td>2576.0</td>
      <td>647.0</td>
      <td>17.0</td>
      <td>5.0</td>
      <td>11.0</td>
      <td>117.0</td>
      <td>87.0</td>
      <td>99.0</td>
      <td>172.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1001020400</td>
      <td>Alabama</td>
      <td>Autauga County</td>
      <td>1</td>
      <td>4386</td>
      <td>1722</td>
      <td>0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>2.8</td>
      <td>70607.0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1363.0</td>
      <td>3651.0</td>
      <td>1363.0</td>
      <td>343.0</td>
      <td>893.0</td>
      <td>343.0</td>
      <td>3651.0</td>
      <td>83.24</td>
      <td>893.0</td>
      <td>20.36</td>
      <td>847.0</td>
      <td>19.30</td>
      <td>767.0</td>
      <td>17.48</td>
      <td>3395.0</td>
      <td>77.41</td>
      <td>170.0</td>
      <td>3.88</td>
      <td>15.0</td>
      <td>0.34</td>
      <td>3.0</td>
      <td>0.06</td>
      <td>8.0</td>
      <td>0.18</td>
      <td>60.0</td>
      <td>1.38</td>
      <td>61.0</td>
      <td>1.40</td>
      <td>19.0</td>
      <td>1.13</td>
      <td>84.0</td>
      <td>4.88</td>
      <td>1363.0</td>
      <td>31.09</td>
      <td>343.0</td>
      <td>7.83</td>
      <td>346.0</td>
      <td>7.89</td>
      <td>237.0</td>
      <td>5.39</td>
      <td>1233.0</td>
      <td>28.12</td>
      <td>81.0</td>
      <td>1.85</td>
      <td>7.0</td>
      <td>0.16</td>
      <td>2.0</td>
      <td>0.05</td>
      <td>4.0</td>
      <td>0.08</td>
      <td>37.0</td>
      <td>0.84</td>
      <td>30.0</td>
      <td>0.68</td>
      <td>8.0</td>
      <td>0.46</td>
      <td>30.0</td>
      <td>1.76</td>
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
      <td>NaN</td>
      <td>NaN</td>
      <td>922.0</td>
      <td>1015.0</td>
      <td>904.0</td>
      <td>4086.0</td>
      <td>193.0</td>
      <td>18.0</td>
      <td>4.0</td>
      <td>11.0</td>
      <td>74.0</td>
      <td>85.0</td>
      <td>21.0</td>
      <td>98.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1001020500</td>
      <td>Alabama</td>
      <td>Autauga County</td>
      <td>1</td>
      <td>10766</td>
      <td>4082</td>
      <td>0</td>
      <td>181.0</td>
      <td>1.68</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>15.2</td>
      <td>96334.0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>2643.0</td>
      <td>7778.0</td>
      <td>2643.0</td>
      <td>586.0</td>
      <td>1719.0</td>
      <td>586.0</td>
      <td>7778.0</td>
      <td>72.25</td>
      <td>1719.0</td>
      <td>15.97</td>
      <td>2309.0</td>
      <td>21.45</td>
      <td>840.0</td>
      <td>7.80</td>
      <td>6299.0</td>
      <td>58.51</td>
      <td>1001.0</td>
      <td>9.29</td>
      <td>209.0</td>
      <td>1.94</td>
      <td>5.0</td>
      <td>0.05</td>
      <td>38.0</td>
      <td>0.35</td>
      <td>227.0</td>
      <td>2.11</td>
      <td>277.0</td>
      <td>2.57</td>
      <td>164.0</td>
      <td>4.01</td>
      <td>235.0</td>
      <td>5.76</td>
      <td>2643.0</td>
      <td>24.55</td>
      <td>586.0</td>
      <td>5.45</td>
      <td>715.0</td>
      <td>6.64</td>
      <td>362.0</td>
      <td>3.36</td>
      <td>2168.0</td>
      <td>20.14</td>
      <td>343.0</td>
      <td>3.19</td>
      <td>47.0</td>
      <td>0.44</td>
      <td>1.0</td>
      <td>0.01</td>
      <td>14.0</td>
      <td>0.13</td>
      <td>70.0</td>
      <td>0.65</td>
      <td>86.0</td>
      <td>0.80</td>
      <td>55.0</td>
      <td>1.35</td>
      <td>83.0</td>
      <td>2.04</td>
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
      <td>NaN</td>
      <td>NaN</td>
      <td>2242.0</td>
      <td>3162.0</td>
      <td>1126.0</td>
      <td>8666.0</td>
      <td>1437.0</td>
      <td>296.0</td>
      <td>9.0</td>
      <td>48.0</td>
      <td>310.0</td>
      <td>355.0</td>
      <td>230.0</td>
      <td>339.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1001020600</td>
      <td>Alabama</td>
      <td>Autauga County</td>
      <td>1</td>
      <td>3668</td>
      <td>1311</td>
      <td>0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>21.6</td>
      <td>69521.0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>3438.0</td>
      <td>3668.0</td>
      <td>3438.0</td>
      <td>1585.0</td>
      <td>1674.0</td>
      <td>1585.0</td>
      <td>3668.0</td>
      <td>100.00</td>
      <td>1674.0</td>
      <td>45.63</td>
      <td>1008.0</td>
      <td>27.48</td>
      <td>411.0</td>
      <td>11.21</td>
      <td>2751.0</td>
      <td>75.00</td>
      <td>740.0</td>
      <td>20.17</td>
      <td>9.0</td>
      <td>0.25</td>
      <td>1.0</td>
      <td>0.03</td>
      <td>10.0</td>
      <td>0.27</td>
      <td>157.0</td>
      <td>4.28</td>
      <td>176.0</td>
      <td>4.80</td>
      <td>73.0</td>
      <td>5.54</td>
      <td>220.0</td>
      <td>16.82</td>
      <td>3438.0</td>
      <td>93.72</td>
      <td>1585.0</td>
      <td>43.21</td>
      <td>955.0</td>
      <td>26.03</td>
      <td>375.0</td>
      <td>10.22</td>
      <td>2539.0</td>
      <td>69.22</td>
      <td>726.0</td>
      <td>19.80</td>
      <td>9.0</td>
      <td>0.25</td>
      <td>1.0</td>
      <td>0.03</td>
      <td>9.0</td>
      <td>0.26</td>
      <td>153.0</td>
      <td>4.16</td>
      <td>168.0</td>
      <td>4.59</td>
      <td>72.0</td>
      <td>5.47</td>
      <td>206.0</td>
      <td>15.70</td>
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
      <td>NaN</td>
      <td>NaN</td>
      <td>1659.0</td>
      <td>1008.0</td>
      <td>411.0</td>
      <td>2751.0</td>
      <td>740.0</td>
      <td>9.0</td>
      <td>1.0</td>
      <td>10.0</td>
      <td>157.0</td>
      <td>176.0</td>
      <td>71.0</td>
      <td>224.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1001020700</td>
      <td>Alabama</td>
      <td>Autauga County</td>
      <td>1</td>
      <td>2891</td>
      <td>1188</td>
      <td>0</td>
      <td>36.0</td>
      <td>1.25</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>30.5</td>
      <td>39875.0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1231.0</td>
      <td>2287.0</td>
      <td>1231.0</td>
      <td>742.0</td>
      <td>1307.0</td>
      <td>742.0</td>
      <td>2287.0</td>
      <td>79.12</td>
      <td>1307.0</td>
      <td>45.19</td>
      <td>557.0</td>
      <td>19.25</td>
      <td>277.0</td>
      <td>9.57</td>
      <td>1849.0</td>
      <td>63.97</td>
      <td>337.0</td>
      <td>11.67</td>
      <td>10.0</td>
      <td>0.35</td>
      <td>3.0</td>
      <td>0.10</td>
      <td>9.0</td>
      <td>0.30</td>
      <td>79.0</td>
      <td>2.73</td>
      <td>82.0</td>
      <td>2.84</td>
      <td>23.0</td>
      <td>1.91</td>
      <td>263.0</td>
      <td>22.12</td>
      <td>1231.0</td>
      <td>42.58</td>
      <td>742.0</td>
      <td>25.67</td>
      <td>298.0</td>
      <td>10.31</td>
      <td>109.0</td>
      <td>3.78</td>
      <td>1005.0</td>
      <td>34.77</td>
      <td>158.0</td>
      <td>5.47</td>
      <td>4.0</td>
      <td>0.13</td>
      <td>2.0</td>
      <td>0.08</td>
      <td>4.0</td>
      <td>0.14</td>
      <td>58.0</td>
      <td>2.00</td>
      <td>56.0</td>
      <td>1.93</td>
      <td>12.0</td>
      <td>1.01</td>
      <td>140.0</td>
      <td>11.82</td>
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
      <td>NaN</td>
      <td>NaN</td>
      <td>2175.0</td>
      <td>686.0</td>
      <td>360.0</td>
      <td>2333.0</td>
      <td>435.0</td>
      <td>13.0</td>
      <td>3.0</td>
      <td>11.0</td>
      <td>96.0</td>
      <td>98.0</td>
      <td>34.0</td>
      <td>390.0</td>
    </tr>
  </tbody>
</table>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-291a9f55-3750-46ce-be70-cdd9d0a92938')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  
    </button>

  

    
  </div>


<div id="df-8f9da8c4-5a0e-4efd-962f-14527f7ae2e7">
  <button class="colab-df-quickchart" onclick="quickchart('df-8f9da8c4-5a0e-4efd-962f-14527f7ae2e7')"
            title="Suggest charts"
            style="display:none;">


  </button>



  
</div>

    </div>
  </div>





```python
# Display the bottom seven rows of the dataframe
food_access.tail(7)

```





  <div id="df-eca142c5-0d70-4bbf-a632-80145daa02a4" class="colab-df-container">
    <div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CensusTract</th>
      <th>State</th>
      <th>County</th>
      <th>Urban</th>
      <th>Pop2010</th>
      <th>OHU2010</th>
      <th>GroupQuartersFlag</th>
      <th>NUMGQTRS</th>
      <th>PCTGQTRS</th>
      <th>LILATracts_1And10</th>
      <th>LILATracts_halfAnd10</th>
      <th>LILATracts_1And20</th>
      <th>LILATracts_Vehicle</th>
      <th>HUNVFlag</th>
      <th>LowIncomeTracts</th>
      <th>PovertyRate</th>
      <th>MedianFamilyIncome</th>
      <th>LA1and10</th>
      <th>LAhalfand10</th>
      <th>LA1and20</th>
      <th>LATracts_half</th>
      <th>LATracts1</th>
      <th>LATracts10</th>
      <th>LATracts20</th>
      <th>LATractsVehicle_20</th>
      <th>LAPOP1_10</th>
      <th>LAPOP05_10</th>
      <th>LAPOP1_20</th>
      <th>LALOWI1_10</th>
      <th>LALOWI05_10</th>
      <th>LALOWI1_20</th>
      <th>lapophalf</th>
      <th>lapophalfshare</th>
      <th>lalowihalf</th>
      <th>lalowihalfshare</th>
      <th>lakidshalf</th>
      <th>lakidshalfshare</th>
      <th>laseniorshalf</th>
      <th>laseniorshalfshare</th>
      <th>lawhitehalf</th>
      <th>lawhitehalfshare</th>
      <th>lablackhalf</th>
      <th>lablackhalfshare</th>
      <th>laasianhalf</th>
      <th>laasianhalfshare</th>
      <th>lanhopihalf</th>
      <th>lanhopihalfshare</th>
      <th>laaianhalf</th>
      <th>laaianhalfshare</th>
      <th>laomultirhalf</th>
      <th>laomultirhalfshare</th>
      <th>lahisphalf</th>
      <th>lahisphalfshare</th>
      <th>lahunvhalf</th>
      <th>lahunvhalfshare</th>
      <th>lasnaphalf</th>
      <th>lasnaphalfshare</th>
      <th>lapop1</th>
      <th>lapop1share</th>
      <th>lalowi1</th>
      <th>lalowi1share</th>
      <th>lakids1</th>
      <th>lakids1share</th>
      <th>laseniors1</th>
      <th>laseniors1share</th>
      <th>lawhite1</th>
      <th>lawhite1share</th>
      <th>lablack1</th>
      <th>lablack1share</th>
      <th>laasian1</th>
      <th>laasian1share</th>
      <th>lanhopi1</th>
      <th>lanhopi1share</th>
      <th>laaian1</th>
      <th>laaian1share</th>
      <th>laomultir1</th>
      <th>laomultir1share</th>
      <th>lahisp1</th>
      <th>lahisp1share</th>
      <th>lahunv1</th>
      <th>lahunv1share</th>
      <th>lasnap1</th>
      <th>lasnap1share</th>
      <th>lapop10</th>
      <th>lapop10share</th>
      <th>lalowi10</th>
      <th>lalowi10share</th>
      <th>lakids10</th>
      <th>lakids10share</th>
      <th>laseniors10</th>
      <th>laseniors10share</th>
      <th>lawhite10</th>
      <th>lawhite10share</th>
      <th>lablack10</th>
      <th>lablack10share</th>
      <th>laasian10</th>
      <th>laasian10share</th>
      <th>lanhopi10</th>
      <th>lanhopi10share</th>
      <th>laaian10</th>
      <th>laaian10share</th>
      <th>laomultir10</th>
      <th>laomultir10share</th>
      <th>lahisp10</th>
      <th>lahisp10share</th>
      <th>lahunv10</th>
      <th>lahunv10share</th>
      <th>lasnap10</th>
      <th>lasnap10share</th>
      <th>lapop20</th>
      <th>lapop20share</th>
      <th>lalowi20</th>
      <th>lalowi20share</th>
      <th>lakids20</th>
      <th>lakids20share</th>
      <th>laseniors20</th>
      <th>laseniors20share</th>
      <th>lawhite20</th>
      <th>lawhite20share</th>
      <th>lablack20</th>
      <th>lablack20share</th>
      <th>laasian20</th>
      <th>laasian20share</th>
      <th>lanhopi20</th>
      <th>lanhopi20share</th>
      <th>laaian20</th>
      <th>laaian20share</th>
      <th>laomultir20</th>
      <th>laomultir20share</th>
      <th>lahisp20</th>
      <th>lahisp20share</th>
      <th>lahunv20</th>
      <th>lahunv20share</th>
      <th>lasnap20</th>
      <th>lasnap20share</th>
      <th>TractLOWI</th>
      <th>TractKids</th>
      <th>TractSeniors</th>
      <th>TractWhite</th>
      <th>TractBlack</th>
      <th>TractAsian</th>
      <th>TractNHOPI</th>
      <th>TractAIAN</th>
      <th>TractOMultir</th>
      <th>TractHispanic</th>
      <th>TractHUNV</th>
      <th>TractSNAP</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>72524</th>
      <td>56041975300</td>
      <td>Wyoming</td>
      <td>Uinta County</td>
      <td>0</td>
      <td>7761</td>
      <td>2696</td>
      <td>0</td>
      <td>205.0</td>
      <td>2.64</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>13.6</td>
      <td>62445.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>479.0</td>
      <td>479.0</td>
      <td>5.0</td>
      <td>264.0</td>
      <td>264.0</td>
      <td>3.0</td>
      <td>6037.0</td>
      <td>77.78</td>
      <td>2302.0</td>
      <td>29.66</td>
      <td>1882.0</td>
      <td>24.25</td>
      <td>455.0</td>
      <td>5.86</td>
      <td>5509.0</td>
      <td>70.99</td>
      <td>13.0</td>
      <td>0.17</td>
      <td>24.0</td>
      <td>0.31</td>
      <td>20.0</td>
      <td>0.26</td>
      <td>34.0</td>
      <td>0.43</td>
      <td>436.0</td>
      <td>5.62</td>
      <td>613.0</td>
      <td>7.90</td>
      <td>96.0</td>
      <td>3.57</td>
      <td>194.0</td>
      <td>7.19</td>
      <td>3934.0</td>
      <td>50.69</td>
      <td>1772.0</td>
      <td>22.84</td>
      <td>1197.0</td>
      <td>15.43</td>
      <td>339.0</td>
      <td>4.36</td>
      <td>3583.0</td>
      <td>46.17</td>
      <td>10.0</td>
      <td>0.13</td>
      <td>14.0</td>
      <td>0.18</td>
      <td>9.0</td>
      <td>0.11</td>
      <td>17.0</td>
      <td>0.22</td>
      <td>301.0</td>
      <td>3.88</td>
      <td>435.0</td>
      <td>5.61</td>
      <td>51.0</td>
      <td>1.90</td>
      <td>127.0</td>
      <td>4.70</td>
      <td>479.0</td>
      <td>6.17</td>
      <td>264.0</td>
      <td>3.40</td>
      <td>118.0</td>
      <td>1.52</td>
      <td>73.0</td>
      <td>0.95</td>
      <td>466.0</td>
      <td>6.00</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>1.0</td>
      <td>0.01</td>
      <td>2.0</td>
      <td>0.03</td>
      <td>1.0</td>
      <td>0.01</td>
      <td>9.0</td>
      <td>0.11</td>
      <td>13.0</td>
      <td>0.17</td>
      <td>5.0</td>
      <td>0.17</td>
      <td>16.0</td>
      <td>0.61</td>
      <td>5.0</td>
      <td>0.06</td>
      <td>3.0</td>
      <td>0.04</td>
      <td>1.0</td>
      <td>0.02</td>
      <td>1.0</td>
      <td>0.02</td>
      <td>5.0</td>
      <td>0.06</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.01</td>
      <td>2965.0</td>
      <td>2387.0</td>
      <td>569.0</td>
      <td>7052.0</td>
      <td>21.0</td>
      <td>29.0</td>
      <td>23.0</td>
      <td>64.0</td>
      <td>572.0</td>
      <td>797.0</td>
      <td>107.0</td>
      <td>255.0</td>
    </tr>
    <tr>
      <th>72525</th>
      <td>56041975400</td>
      <td>Wyoming</td>
      <td>Uinta County</td>
      <td>0</td>
      <td>6852</td>
      <td>2632</td>
      <td>0</td>
      <td>65.0</td>
      <td>0.95</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>17.3</td>
      <td>57248.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>120.0</td>
      <td>120.0</td>
      <td>NaN</td>
      <td>24.0</td>
      <td>24.0</td>
      <td>NaN</td>
      <td>5809.0</td>
      <td>84.78</td>
      <td>2151.0</td>
      <td>31.39</td>
      <td>1632.0</td>
      <td>23.83</td>
      <td>575.0</td>
      <td>8.39</td>
      <td>5221.0</td>
      <td>76.19</td>
      <td>15.0</td>
      <td>0.22</td>
      <td>13.0</td>
      <td>0.19</td>
      <td>1.0</td>
      <td>0.01</td>
      <td>60.0</td>
      <td>0.87</td>
      <td>500.0</td>
      <td>7.29</td>
      <td>751.0</td>
      <td>10.96</td>
      <td>108.0</td>
      <td>4.12</td>
      <td>180.0</td>
      <td>6.83</td>
      <td>3112.0</td>
      <td>45.42</td>
      <td>1107.0</td>
      <td>16.16</td>
      <td>909.0</td>
      <td>13.26</td>
      <td>255.0</td>
      <td>3.72</td>
      <td>2852.0</td>
      <td>41.62</td>
      <td>7.0</td>
      <td>0.10</td>
      <td>9.0</td>
      <td>0.13</td>
      <td>0.0</td>
      <td>0.01</td>
      <td>33.0</td>
      <td>0.48</td>
      <td>211.0</td>
      <td>3.08</td>
      <td>328.0</td>
      <td>4.79</td>
      <td>49.0</td>
      <td>1.87</td>
      <td>89.0</td>
      <td>3.39</td>
      <td>120.0</td>
      <td>1.76</td>
      <td>24.0</td>
      <td>0.35</td>
      <td>46.0</td>
      <td>0.67</td>
      <td>10.0</td>
      <td>0.15</td>
      <td>114.0</td>
      <td>1.66</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>1.0</td>
      <td>0.01</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>3.0</td>
      <td>0.05</td>
      <td>3.0</td>
      <td>0.04</td>
      <td>1.0</td>
      <td>0.01</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>3.0</td>
      <td>0.12</td>
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
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2273.0</td>
      <td>1921.0</td>
      <td>709.0</td>
      <td>6160.0</td>
      <td>20.0</td>
      <td>19.0</td>
      <td>2.0</td>
      <td>67.0</td>
      <td>584.0</td>
      <td>871.0</td>
      <td>124.0</td>
      <td>217.0</td>
    </tr>
    <tr>
      <th>72526</th>
      <td>56043000200</td>
      <td>Wyoming</td>
      <td>Washakie County</td>
      <td>0</td>
      <td>3326</td>
      <td>1317</td>
      <td>0</td>
      <td>57.0</td>
      <td>1.71</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>9.7</td>
      <td>67254.0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>902.0</td>
      <td>902.0</td>
      <td>730.0</td>
      <td>218.0</td>
      <td>218.0</td>
      <td>176.0</td>
      <td>3326.0</td>
      <td>99.99</td>
      <td>843.0</td>
      <td>25.36</td>
      <td>884.0</td>
      <td>26.58</td>
      <td>593.0</td>
      <td>17.83</td>
      <td>3106.0</td>
      <td>93.38</td>
      <td>6.0</td>
      <td>0.18</td>
      <td>15.0</td>
      <td>0.45</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>27.0</td>
      <td>0.81</td>
      <td>172.0</td>
      <td>5.17</td>
      <td>309.0</td>
      <td>9.29</td>
      <td>67.0</td>
      <td>5.06</td>
      <td>64.0</td>
      <td>4.83</td>
      <td>2714.0</td>
      <td>81.60</td>
      <td>675.0</td>
      <td>20.29</td>
      <td>716.0</td>
      <td>21.52</td>
      <td>472.0</td>
      <td>14.18</td>
      <td>2550.0</td>
      <td>76.67</td>
      <td>6.0</td>
      <td>0.18</td>
      <td>14.0</td>
      <td>0.42</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>21.0</td>
      <td>0.62</td>
      <td>123.0</td>
      <td>3.70</td>
      <td>221.0</td>
      <td>6.64</td>
      <td>34.0</td>
      <td>2.56</td>
      <td>50.0</td>
      <td>3.82</td>
      <td>902.0</td>
      <td>27.12</td>
      <td>218.0</td>
      <td>6.56</td>
      <td>177.0</td>
      <td>5.33</td>
      <td>218.0</td>
      <td>6.56</td>
      <td>857.0</td>
      <td>25.75</td>
      <td>2.0</td>
      <td>0.06</td>
      <td>6.0</td>
      <td>0.19</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>5.0</td>
      <td>0.15</td>
      <td>32.0</td>
      <td>0.96</td>
      <td>35.0</td>
      <td>1.05</td>
      <td>7.0</td>
      <td>0.51</td>
      <td>19.0</td>
      <td>1.47</td>
      <td>730.0</td>
      <td>21.95</td>
      <td>176.0</td>
      <td>5.30</td>
      <td>144.0</td>
      <td>4.33</td>
      <td>191.0</td>
      <td>5.74</td>
      <td>695.0</td>
      <td>20.90</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.03</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>4.0</td>
      <td>0.12</td>
      <td>30.0</td>
      <td>0.90</td>
      <td>24.0</td>
      <td>0.72</td>
      <td>6.0</td>
      <td>0.0</td>
      <td>16.0</td>
      <td>1.23</td>
      <td>765.0</td>
      <td>884.0</td>
      <td>593.0</td>
      <td>3106.0</td>
      <td>6.0</td>
      <td>15.0</td>
      <td>0.0</td>
      <td>27.0</td>
      <td>172.0</td>
      <td>309.0</td>
      <td>61.0</td>
      <td>64.0</td>
    </tr>
    <tr>
      <th>72527</th>
      <td>56043000301</td>
      <td>Wyoming</td>
      <td>Washakie County</td>
      <td>1</td>
      <td>2665</td>
      <td>1154</td>
      <td>0</td>
      <td>10.0</td>
      <td>0.38</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>11.6</td>
      <td>64152.0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>743.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>279.0</td>
      <td>NaN</td>
      <td>743.0</td>
      <td>27.89</td>
      <td>279.0</td>
      <td>10.49</td>
      <td>187.0</td>
      <td>7.03</td>
      <td>122.0</td>
      <td>4.57</td>
      <td>638.0</td>
      <td>23.95</td>
      <td>2.0</td>
      <td>0.09</td>
      <td>14.0</td>
      <td>0.54</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>19.0</td>
      <td>0.69</td>
      <td>70.0</td>
      <td>2.62</td>
      <td>135.0</td>
      <td>5.05</td>
      <td>27.0</td>
      <td>2.30</td>
      <td>12.0</td>
      <td>1.02</td>
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
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>774.0</td>
      <td>674.0</td>
      <td>399.0</td>
      <td>2377.0</td>
      <td>5.0</td>
      <td>23.0</td>
      <td>0.0</td>
      <td>40.0</td>
      <td>220.0</td>
      <td>446.0</td>
      <td>88.0</td>
      <td>41.0</td>
    </tr>
    <tr>
      <th>72528</th>
      <td>56043000302</td>
      <td>Wyoming</td>
      <td>Washakie County</td>
      <td>1</td>
      <td>2542</td>
      <td>1021</td>
      <td>0</td>
      <td>73.0</td>
      <td>2.87</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>16.3</td>
      <td>69605.0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>155.0</td>
      <td>892.0</td>
      <td>155.0</td>
      <td>44.0</td>
      <td>261.0</td>
      <td>44.0</td>
      <td>892.0</td>
      <td>35.10</td>
      <td>261.0</td>
      <td>10.25</td>
      <td>215.0</td>
      <td>8.45</td>
      <td>173.0</td>
      <td>6.80</td>
      <td>806.0</td>
      <td>31.71</td>
      <td>7.0</td>
      <td>0.26</td>
      <td>0.0</td>
      <td>0.02</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>4.0</td>
      <td>0.15</td>
      <td>75.0</td>
      <td>2.96</td>
      <td>147.0</td>
      <td>5.78</td>
      <td>12.0</td>
      <td>1.18</td>
      <td>24.0</td>
      <td>2.31</td>
      <td>155.0</td>
      <td>6.11</td>
      <td>44.0</td>
      <td>1.72</td>
      <td>30.0</td>
      <td>1.17</td>
      <td>34.0</td>
      <td>1.32</td>
      <td>145.0</td>
      <td>5.70</td>
      <td>2.0</td>
      <td>0.09</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.01</td>
      <td>8.0</td>
      <td>0.30</td>
      <td>12.0</td>
      <td>0.46</td>
      <td>3.0</td>
      <td>0.26</td>
      <td>5.0</td>
      <td>0.45</td>
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
      <td>NaN</td>
      <td>NaN</td>
      <td>789.0</td>
      <td>614.0</td>
      <td>516.0</td>
      <td>2312.0</td>
      <td>11.0</td>
      <td>10.0</td>
      <td>1.0</td>
      <td>26.0</td>
      <td>182.0</td>
      <td>407.0</td>
      <td>23.0</td>
      <td>64.0</td>
    </tr>
    <tr>
      <th>72529</th>
      <td>56045951100</td>
      <td>Wyoming</td>
      <td>Weston County</td>
      <td>0</td>
      <td>3314</td>
      <td>1322</td>
      <td>0</td>
      <td>252.0</td>
      <td>7.60</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>17.5</td>
      <td>74500.0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>840.0</td>
      <td>840.0</td>
      <td>188.0</td>
      <td>247.0</td>
      <td>247.0</td>
      <td>55.0</td>
      <td>2709.0</td>
      <td>81.74</td>
      <td>837.0</td>
      <td>25.26</td>
      <td>491.0</td>
      <td>14.80</td>
      <td>403.0</td>
      <td>12.15</td>
      <td>2609.0</td>
      <td>78.73</td>
      <td>14.0</td>
      <td>0.42</td>
      <td>7.0</td>
      <td>0.22</td>
      <td>1.0</td>
      <td>0.03</td>
      <td>31.0</td>
      <td>0.93</td>
      <td>47.0</td>
      <td>1.41</td>
      <td>77.0</td>
      <td>2.32</td>
      <td>26.0</td>
      <td>1.98</td>
      <td>26.0</td>
      <td>1.93</td>
      <td>2283.0</td>
      <td>68.87</td>
      <td>687.0</td>
      <td>20.73</td>
      <td>394.0</td>
      <td>11.90</td>
      <td>321.0</td>
      <td>9.69</td>
      <td>2193.0</td>
      <td>66.19</td>
      <td>13.0</td>
      <td>0.39</td>
      <td>5.0</td>
      <td>0.16</td>
      <td>1.0</td>
      <td>0.03</td>
      <td>29.0</td>
      <td>0.88</td>
      <td>41.0</td>
      <td>1.23</td>
      <td>67.0</td>
      <td>2.01</td>
      <td>13.0</td>
      <td>1.00</td>
      <td>21.0</td>
      <td>1.59</td>
      <td>840.0</td>
      <td>25.34</td>
      <td>247.0</td>
      <td>7.45</td>
      <td>143.0</td>
      <td>4.33</td>
      <td>154.0</td>
      <td>4.64</td>
      <td>818.0</td>
      <td>24.68</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>2.0</td>
      <td>0.06</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>6.0</td>
      <td>0.18</td>
      <td>14.0</td>
      <td>0.42</td>
      <td>14.0</td>
      <td>0.42</td>
      <td>2.0</td>
      <td>0.19</td>
      <td>9.0</td>
      <td>0.70</td>
      <td>188.0</td>
      <td>5.68</td>
      <td>55.0</td>
      <td>1.66</td>
      <td>40.0</td>
      <td>1.22</td>
      <td>44.0</td>
      <td>1.32</td>
      <td>182.0</td>
      <td>5.50</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>6.0</td>
      <td>0.18</td>
      <td>10.0</td>
      <td>0.30</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>2.0</td>
      <td>0.14</td>
      <td>955.0</td>
      <td>655.0</td>
      <td>499.0</td>
      <td>3179.0</td>
      <td>15.0</td>
      <td>10.0</td>
      <td>1.0</td>
      <td>47.0</td>
      <td>62.0</td>
      <td>91.0</td>
      <td>47.0</td>
      <td>34.0</td>
    </tr>
    <tr>
      <th>72530</th>
      <td>56045951300</td>
      <td>Wyoming</td>
      <td>Weston County</td>
      <td>1</td>
      <td>3894</td>
      <td>1699</td>
      <td>0</td>
      <td>61.0</td>
      <td>1.57</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>17.3</td>
      <td>76838.0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1376.0</td>
      <td>2528.0</td>
      <td>1376.0</td>
      <td>384.0</td>
      <td>671.0</td>
      <td>384.0</td>
      <td>2528.0</td>
      <td>64.93</td>
      <td>671.0</td>
      <td>17.24</td>
      <td>620.0</td>
      <td>15.93</td>
      <td>421.0</td>
      <td>10.80</td>
      <td>2400.0</td>
      <td>61.63</td>
      <td>3.0</td>
      <td>0.09</td>
      <td>6.0</td>
      <td>0.15</td>
      <td>2.0</td>
      <td>0.05</td>
      <td>24.0</td>
      <td>0.63</td>
      <td>93.0</td>
      <td>2.38</td>
      <td>96.0</td>
      <td>2.47</td>
      <td>17.0</td>
      <td>1.01</td>
      <td>71.0</td>
      <td>4.18</td>
      <td>1376.0</td>
      <td>35.34</td>
      <td>384.0</td>
      <td>9.85</td>
      <td>341.0</td>
      <td>8.76</td>
      <td>197.0</td>
      <td>5.05</td>
      <td>1290.0</td>
      <td>33.12</td>
      <td>2.0</td>
      <td>0.05</td>
      <td>6.0</td>
      <td>0.15</td>
      <td>2.0</td>
      <td>0.05</td>
      <td>16.0</td>
      <td>0.40</td>
      <td>61.0</td>
      <td>1.57</td>
      <td>69.0</td>
      <td>1.78</td>
      <td>9.0</td>
      <td>0.52</td>
      <td>37.0</td>
      <td>2.20</td>
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
      <td>NaN</td>
      <td>NaN</td>
      <td>1095.0</td>
      <td>918.0</td>
      <td>650.0</td>
      <td>3706.0</td>
      <td>6.0</td>
      <td>10.0</td>
      <td>2.0</td>
      <td>44.0</td>
      <td>126.0</td>
      <td>125.0</td>
      <td>34.0</td>
      <td>110.0</td>
    </tr>
  </tbody>
</table>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-eca142c5-0d70-4bbf-a632-80145daa02a4')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  
    </button>

  

    
  </div>


<div id="df-39ffe4e5-7796-40c3-a77b-2159ceac7f09">
  <button class="colab-df-quickchart" onclick="quickchart('df-39ffe4e5-7796-40c3-a77b-2159ceac7f09')"
            title="Suggest charts"
            style="display:none;">


  </button>



  
</div>

    </div>
  </div>





```python
food_access.shape

```




    (72531, 147)




```python
72531 * 147
```




    10662057



State the shape of the dataframe :

How many rows does the dataframe have?

- 72531 rows

How many columns does the dataframe have?

- 147 columns

What is the total number of datapoints expected in the dataset (rows x columns)?

- 10662057 total datapoints


```python
food_access.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 72531 entries, 0 to 72530
    Columns: 147 entries, CensusTract to TractSNAP
    dtypes: float64(126), int64(19), object(2)
    memory usage: 81.3+ MB



```python
food_access.info(show_counts=True, verbose=True)
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 72531 entries, 0 to 72530
    Data columns (total 147 columns):
     #    Column                Non-Null Count  Dtype  
    ---   ------                --------------  -----  
     0    CensusTract           72531 non-null  int64  
     1    State                 72531 non-null  object 
     2    County                72531 non-null  object 
     3    Urban                 72531 non-null  int64  
     4    Pop2010               72531 non-null  int64  
     5    OHU2010               72531 non-null  int64  
     6    GroupQuartersFlag     72531 non-null  int64  
     7    NUMGQTRS              72506 non-null  float64
     8    PCTGQTRS              72506 non-null  float64
     9    LILATracts_1And10     72531 non-null  int64  
     10   LILATracts_halfAnd10  72531 non-null  int64  
     11   LILATracts_1And20     72531 non-null  int64  
     12   LILATracts_Vehicle    72531 non-null  int64  
     13   HUNVFlag              72531 non-null  int64  
     14   LowIncomeTracts       72531 non-null  int64  
     15   PovertyRate           72528 non-null  float64
     16   MedianFamilyIncome    71783 non-null  float64
     17   LA1and10              72531 non-null  int64  
     18   LAhalfand10           72531 non-null  int64  
     19   LA1and20              72531 non-null  int64  
     20   LATracts_half         72531 non-null  int64  
     21   LATracts1             72531 non-null  int64  
     22   LATracts10            72531 non-null  int64  
     23   LATracts20            72531 non-null  int64  
     24   LATractsVehicle_20    72531 non-null  int64  
     25   LAPOP1_10             42574 non-null  float64
     26   LAPOP05_10            57991 non-null  float64
     27   LAPOP1_20             36617 non-null  float64
     28   LALOWI1_10            42574 non-null  float64
     29   LALOWI05_10           57991 non-null  float64
     30   LALOWI1_20            36617 non-null  float64
     31   lapophalf             67963 non-null  float64
     32   lapophalfshare        67963 non-null  float64
     33   lalowihalf            67963 non-null  float64
     34   lalowihalfshare       67963 non-null  float64
     35   lakidshalf            67963 non-null  float64
     36   lakidshalfshare       67963 non-null  float64
     37   laseniorshalf         67963 non-null  float64
     38   laseniorshalfshare    67963 non-null  float64
     39   lawhitehalf           67963 non-null  float64
     40   lawhitehalfshare      67963 non-null  float64
     41   lablackhalf           67963 non-null  float64
     42   lablackhalfshare      67963 non-null  float64
     43   laasianhalf           67963 non-null  float64
     44   laasianhalfshare      67963 non-null  float64
     45   lanhopihalf           67963 non-null  float64
     46   lanhopihalfshare      67963 non-null  float64
     47   laaianhalf            67963 non-null  float64
     48   laaianhalfshare       67963 non-null  float64
     49   laomultirhalf         67963 non-null  float64
     50   laomultirhalfshare    67963 non-null  float64
     51   lahisphalf            67963 non-null  float64
     52   lahisphalfshare       67963 non-null  float64
     53   lahunvhalf            67963 non-null  float64
     54   lahunvhalfshare       67969 non-null  float64
     55   lasnaphalf            67963 non-null  float64
     56   lasnaphalfshare       67969 non-null  float64
     57   lapop1                52542 non-null  float64
     58   lapop1share           52542 non-null  float64
     59   lalowi1               52542 non-null  float64
     60   lalowi1share          52542 non-null  float64
     61   lakids1               52542 non-null  float64
     62   lakids1share          52542 non-null  float64
     63   laseniors1            52542 non-null  float64
     64   laseniors1share       52542 non-null  float64
     65   lawhite1              52542 non-null  float64
     66   lawhite1share         52542 non-null  float64
     67   lablack1              52542 non-null  float64
     68   lablack1share         52542 non-null  float64
     69   laasian1              52542 non-null  float64
     70   laasian1share         52542 non-null  float64
     71   lanhopi1              52542 non-null  float64
     72   lanhopi1share         52542 non-null  float64
     73   laaian1               52542 non-null  float64
     74   laaian1share          52542 non-null  float64
     75   laomultir1            52542 non-null  float64
     76   laomultir1share       52542 non-null  float64
     77   lahisp1               52542 non-null  float64
     78   lahisp1share          52542 non-null  float64
     79   lahunv1               52542 non-null  float64
     80   lahunv1share          52565 non-null  float64
     81   lasnap1               52542 non-null  float64
     82   lasnap1share          52565 non-null  float64
     83   lapop10               7766 non-null   float64
     84   lapop10share          7766 non-null   float64
     85   lalowi10              7766 non-null   float64
     86   lalowi10share         7766 non-null   float64
     87   lakids10              7766 non-null   float64
     88   lakids10share         7766 non-null   float64
     89   laseniors10           7766 non-null   float64
     90   laseniors10share      7766 non-null   float64
     91   lawhite10             7766 non-null   float64
     92   lawhite10share        7766 non-null   float64
     93   lablack10             7766 non-null   float64
     94   lablack10share        7766 non-null   float64
     95   laasian10             7766 non-null   float64
     96   laasian10share        7766 non-null   float64
     97   lanhopi10             7766 non-null   float64
     98   lanhopi10share        7766 non-null   float64
     99   laaian10              7766 non-null   float64
     100  laaian10share         7766 non-null   float64
     101  laomultir10           7766 non-null   float64
     102  laomultir10share      7766 non-null   float64
     103  lahisp10              7766 non-null   float64
     104  lahisp10share         7766 non-null   float64
     105  lahunv10              7766 non-null   float64
     106  lahunv10share         7865 non-null   float64
     107  lasnap10              7766 non-null   float64
     108  lasnap10share         7865 non-null   float64
     109  lapop20               1506 non-null   float64
     110  lapop20share          1506 non-null   float64
     111  lalowi20              1506 non-null   float64
     112  lalowi20share         1506 non-null   float64
     113  lakids20              1506 non-null   float64
     114  lakids20share         1506 non-null   float64
     115  laseniors20           1506 non-null   float64
     116  laseniors20share      1506 non-null   float64
     117  lawhite20             1506 non-null   float64
     118  lawhite20share        1506 non-null   float64
     119  lablack20             1506 non-null   float64
     120  lablack20share        1506 non-null   float64
     121  laasian20             1506 non-null   float64
     122  laasian20share        1506 non-null   float64
     123  lanhopi20             1506 non-null   float64
     124  lanhopi20share        1506 non-null   float64
     125  laaian20              1506 non-null   float64
     126  laaian20share         1506 non-null   float64
     127  laomultir20           1506 non-null   float64
     128  laomultir20share      1506 non-null   float64
     129  lahisp20              1506 non-null   float64
     130  lahisp20share         1506 non-null   float64
     131  lahunv20              1506 non-null   float64
     132  lahunv20share         1611 non-null   float64
     133  lasnap20              1506 non-null   float64
     134  lasnap20share         1611 non-null   float64
     135  TractLOWI             72527 non-null  float64
     136  TractKids             72527 non-null  float64
     137  TractSeniors          72527 non-null  float64
     138  TractWhite            72527 non-null  float64
     139  TractBlack            72527 non-null  float64
     140  TractAsian            72527 non-null  float64
     141  TractNHOPI            72527 non-null  float64
     142  TractAIAN             72527 non-null  float64
     143  TractOMultir          72527 non-null  float64
     144  TractHispanic         72527 non-null  float64
     145  TractHUNV             72527 non-null  float64
     146  TractSNAP             72527 non-null  float64
    dtypes: float64(126), int64(19), object(2)
    memory usage: 81.3+ MB



```python
food_accessColumns = food_access.columns
food_accessColumns
```




    Index(['CensusTract', 'State', 'County', 'Urban', 'Pop2010', 'OHU2010',
           'GroupQuartersFlag', 'NUMGQTRS', 'PCTGQTRS', 'LILATracts_1And10',
           ...
           'TractSeniors', 'TractWhite', 'TractBlack', 'TractAsian', 'TractNHOPI',
           'TractAIAN', 'TractOMultir', 'TractHispanic', 'TractHUNV', 'TractSNAP'],
          dtype='object', length=147)




```python
food_access.isnull().sum()

```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>CensusTract</th>
      <td>0</td>
    </tr>
    <tr>
      <th>State</th>
      <td>0</td>
    </tr>
    <tr>
      <th>County</th>
      <td>0</td>
    </tr>
    <tr>
      <th>Urban</th>
      <td>0</td>
    </tr>
    <tr>
      <th>Pop2010</th>
      <td>0</td>
    </tr>
    <tr>
      <th>OHU2010</th>
      <td>0</td>
    </tr>
    <tr>
      <th>GroupQuartersFlag</th>
      <td>0</td>
    </tr>
    <tr>
      <th>NUMGQTRS</th>
      <td>25</td>
    </tr>
    <tr>
      <th>PCTGQTRS</th>
      <td>25</td>
    </tr>
    <tr>
      <th>LILATracts_1And10</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LILATracts_halfAnd10</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LILATracts_1And20</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LILATracts_Vehicle</th>
      <td>0</td>
    </tr>
    <tr>
      <th>HUNVFlag</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LowIncomeTracts</th>
      <td>0</td>
    </tr>
    <tr>
      <th>PovertyRate</th>
      <td>3</td>
    </tr>
    <tr>
      <th>MedianFamilyIncome</th>
      <td>748</td>
    </tr>
    <tr>
      <th>LA1and10</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LAhalfand10</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LA1and20</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LATracts_half</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LATracts1</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LATracts10</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LATracts20</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LATractsVehicle_20</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LAPOP1_10</th>
      <td>29957</td>
    </tr>
    <tr>
      <th>LAPOP05_10</th>
      <td>14540</td>
    </tr>
    <tr>
      <th>LAPOP1_20</th>
      <td>35914</td>
    </tr>
    <tr>
      <th>LALOWI1_10</th>
      <td>29957</td>
    </tr>
    <tr>
      <th>LALOWI05_10</th>
      <td>14540</td>
    </tr>
    <tr>
      <th>LALOWI1_20</th>
      <td>35914</td>
    </tr>
    <tr>
      <th>lapophalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lapophalfshare</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lalowihalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lalowihalfshare</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lakidshalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lakidshalfshare</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>laseniorshalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>laseniorshalfshare</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lawhitehalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lawhitehalfshare</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lablackhalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lablackhalfshare</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>laasianhalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>laasianhalfshare</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lanhopihalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lanhopihalfshare</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>laaianhalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>laaianhalfshare</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>laomultirhalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>laomultirhalfshare</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lahisphalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lahisphalfshare</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lahunvhalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lahunvhalfshare</th>
      <td>4562</td>
    </tr>
    <tr>
      <th>lasnaphalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lasnaphalfshare</th>
      <td>4562</td>
    </tr>
    <tr>
      <th>lapop1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lapop1share</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lalowi1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lalowi1share</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lakids1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lakids1share</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>laseniors1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>laseniors1share</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lawhite1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lawhite1share</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lablack1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lablack1share</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>laasian1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>laasian1share</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lanhopi1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lanhopi1share</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>laaian1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>laaian1share</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>laomultir1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>laomultir1share</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lahisp1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lahisp1share</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lahunv1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lahunv1share</th>
      <td>19966</td>
    </tr>
    <tr>
      <th>lasnap1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lasnap1share</th>
      <td>19966</td>
    </tr>
    <tr>
      <th>lapop10</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>lapop10share</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>lalowi10</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>lalowi10share</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>lakids10</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>lakids10share</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>laseniors10</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>laseniors10share</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>lawhite10</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>lawhite10share</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>lablack10</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>lablack10share</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>laasian10</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>laasian10share</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>lanhopi10</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>lanhopi10share</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>laaian10</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>laaian10share</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>laomultir10</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>laomultir10share</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>lahisp10</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>lahisp10share</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>lahunv10</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>lahunv10share</th>
      <td>64666</td>
    </tr>
    <tr>
      <th>lasnap10</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>lasnap10share</th>
      <td>64666</td>
    </tr>
    <tr>
      <th>lapop20</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>lapop20share</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>lalowi20</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>lalowi20share</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>lakids20</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>lakids20share</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>laseniors20</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>laseniors20share</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>lawhite20</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>lawhite20share</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>lablack20</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>lablack20share</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>laasian20</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>laasian20share</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>lanhopi20</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>lanhopi20share</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>laaian20</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>laaian20share</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>laomultir20</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>laomultir20share</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>lahisp20</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>lahisp20share</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>lahunv20</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>lahunv20share</th>
      <td>70920</td>
    </tr>
    <tr>
      <th>lasnap20</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>lasnap20share</th>
      <td>70920</td>
    </tr>
    <tr>
      <th>TractLOWI</th>
      <td>4</td>
    </tr>
    <tr>
      <th>TractKids</th>
      <td>4</td>
    </tr>
    <tr>
      <th>TractSeniors</th>
      <td>4</td>
    </tr>
    <tr>
      <th>TractWhite</th>
      <td>4</td>
    </tr>
    <tr>
      <th>TractBlack</th>
      <td>4</td>
    </tr>
    <tr>
      <th>TractAsian</th>
      <td>4</td>
    </tr>
    <tr>
      <th>TractNHOPI</th>
      <td>4</td>
    </tr>
    <tr>
      <th>TractAIAN</th>
      <td>4</td>
    </tr>
    <tr>
      <th>TractOMultir</th>
      <td>4</td>
    </tr>
    <tr>
      <th>TractHispanic</th>
      <td>4</td>
    </tr>
    <tr>
      <th>TractHUNV</th>
      <td>4</td>
    </tr>
    <tr>
      <th>TractSNAP</th>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div><br><label><b>dtype:</b> int64</label>




```python
def missing(DataFrame):
    print ('Percentage of missing values in the dataset:\n',
           round((DataFrame.isnull().sum() * 100/ len(DataFrame)),2).sort_values(ascending=False))


# Call the function and execute
# Syntax: missing(DataFrame)
missing(food_access)
```

    Percentage of missing values in the dataset:
     lanhopi20               97.92
    lalowi20                97.92
    lanhopi20share          97.92
    laaian20                97.92
    laaian20share           97.92
    laomultir20             97.92
    laomultir20share        97.92
    lahisp20                97.92
    lahunv20                97.92
    lasnap20                97.92
    lapop20                 97.92
    lapop20share            97.92
    lahisp20share           97.92
    lalowi20share           97.92
    lawhite20               97.92
    lakids20                97.92
    laasian20               97.92
    lablack20share          97.92
    lablack20               97.92
    lawhite20share          97.92
    laasian20share          97.92
    laseniors20             97.92
    lakids20share           97.92
    laseniors20share        97.92
    lahunv20share           97.78
    lasnap20share           97.78
    laasian10share          89.29
    laseniors10             89.29
    lablack10share          89.29
    lablack10               89.29
    lawhite10share          89.29
    lawhite10               89.29
    laseniors10share        89.29
    lalowi10share           89.29
    lakids10share           89.29
    lakids10                89.29
    lalowi10                89.29
    lapop10share            89.29
    lapop10                 89.29
    laasian10               89.29
    lahisp10                89.29
    lanhopi10               89.29
    lasnap10                89.29
    laaian10                89.29
    laaian10share           89.29
    laomultir10             89.29
    laomultir10share        89.29
    lahisp10share           89.29
    lahunv10                89.29
    lanhopi10share          89.29
    lasnap10share           89.16
    lahunv10share           89.16
    LAPOP1_20               49.52
    LALOWI1_20              49.52
    LALOWI1_10              41.30
    LAPOP1_10               41.30
    lasnap1                 27.56
    lahunv1                 27.56
    lahisp1share            27.56
    lahisp1                 27.56
    laomultir1share         27.56
    laomultir1              27.56
    laaian1share            27.56
    lablack1share           27.56
    lanhopi1share           27.56
    lanhopi1                27.56
    laasian1share           27.56
    laasian1                27.56
    laaian1                 27.56
    lablack1                27.56
    lalowi1share            27.56
    lawhite1share           27.56
    lapop1                  27.56
    lapop1share             27.56
    lalowi1                 27.56
    lakids1share            27.56
    lakids1                 27.56
    laseniors1              27.56
    lawhite1                27.56
    laseniors1share         27.56
    lahunv1share            27.53
    lasnap1share            27.53
    LAPOP05_10              20.05
    LALOWI05_10             20.05
    lapophalf                6.30
    lapophalfshare           6.30
    lablackhalfshare         6.30
    lalowihalfshare          6.30
    lakidshalf               6.30
    lakidshalfshare          6.30
    laseniorshalfshare       6.30
    lawhitehalf              6.30
    lawhitehalfshare         6.30
    lalowihalf               6.30
    laseniorshalf            6.30
    laasianhalf              6.30
    laomultirhalfshare       6.30
    laasianhalfshare         6.30
    lasnaphalf               6.30
    lahunvhalf               6.30
    lahisphalfshare          6.30
    lahisphalf               6.30
    lablackhalf              6.30
    laomultirhalf            6.30
    laaianhalfshare          6.30
    laaianhalf               6.30
    lanhopihalfshare         6.30
    lanhopihalf              6.30
    lahunvhalfshare          6.29
    lasnaphalfshare          6.29
    MedianFamilyIncome       1.03
    PCTGQTRS                 0.03
    NUMGQTRS                 0.03
    TractKids                0.01
    TractSeniors             0.01
    TractLOWI                0.01
    TractBlack               0.01
    TractAsian               0.01
    TractNHOPI               0.01
    TractAIAN                0.01
    TractOMultir             0.01
    TractHispanic            0.01
    TractHUNV                0.01
    TractWhite               0.01
    TractSNAP                0.01
    State                    0.00
    LATractsVehicle_20       0.00
    County                   0.00
    Urban                    0.00
    Pop2010                  0.00
    OHU2010                  0.00
    GroupQuartersFlag        0.00
    LILATracts_1And10        0.00
    LILATracts_halfAnd10     0.00
    LILATracts_1And20        0.00
    LILATracts_Vehicle       0.00
    HUNVFlag                 0.00
    LowIncomeTracts          0.00
    PovertyRate              0.00
    LA1and10                 0.00
    LAhalfand10              0.00
    LA1and20                 0.00
    LATracts_half            0.00
    LATracts1                0.00
    LATracts10               0.00
    LATracts20               0.00
    CensusTract              0.00
    dtype: float64


**Observations**:

How many missing values are there?

- There are missing values in many of the columns; some variables have missing data of over 97%, while others have moderate missingness of between 27% and 49%.  Some of the columns, such as State, County, and CensusTract, have no missing data, while others have minimal missing values, (<1%).


Are these concentrated in specific rows or columns? How does this affect the analysis?

- The majority of missing values are found in specific columns, particularly those pertaining to race and food access.  Comparing various racial groups may become more difficult as a result, and bias may develop if more data is missing from some communities or regions.

Based on the information that is present, how should the missing values be handled?
How will this affect the analysis?
- Columns missing too much data (over 30%) should be removed. Those with moderate missing data (5%-20%) can be filled in using averages or the most common values. Removing extremely incomplete columns guarantees more trustworthy results.  Although it helps preserve more data, filling in missing values could result in minor mistakes.  The analysis may understate disparities in food access in some communities if missing data is dispersed unevenly.






```python
columns_to_drop = [
    'lanhopi20', 'lanhopi20share', 'laaian20', 'laaian20share', 'laomultir20', 'laomultir20share',
    'lahisp20', 'lahisp20share', 'lawhite20', 'lawhite20share', 'laasian20', 'laasian20share',
    'laseniors20', 'laseniors20share', 'lakids20', 'lakids20share', 'lapop20', 'lapop20share',
    'lalowi20', 'lalowi20share', 'lahunv20', 'lahunv20share', 'lasnap20', 'lasnap20share',
    'laasian10', 'laasian10share', 'lahisp10', 'lahisp10share', 'lablack10', 'lablack10share',
    'lawhite10', 'lawhite10share', 'laseniors10', 'laseniors10share', 'lakids10', 'lakids10share',
    'lalowi10', 'lalowi10share', 'lapop10', 'lapop10share', 'lahunv10', 'lahunv10share',
    'lasnap10', 'lasnap10share', 'LAPOP1_20', 'LALOWI1_20', 'LALOWI1_10', 'LAPOP1_10'
]

food_access = food_access.drop(columns=[col for col in columns_to_drop if col in food_access.columns], errors='ignore')

# Check missing values
food_access.isnull().sum()


```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>CensusTract</th>
      <td>0</td>
    </tr>
    <tr>
      <th>State</th>
      <td>0</td>
    </tr>
    <tr>
      <th>County</th>
      <td>0</td>
    </tr>
    <tr>
      <th>Urban</th>
      <td>0</td>
    </tr>
    <tr>
      <th>Pop2010</th>
      <td>0</td>
    </tr>
    <tr>
      <th>OHU2010</th>
      <td>0</td>
    </tr>
    <tr>
      <th>GroupQuartersFlag</th>
      <td>0</td>
    </tr>
    <tr>
      <th>NUMGQTRS</th>
      <td>25</td>
    </tr>
    <tr>
      <th>PCTGQTRS</th>
      <td>25</td>
    </tr>
    <tr>
      <th>LILATracts_1And10</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LILATracts_halfAnd10</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LILATracts_1And20</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LILATracts_Vehicle</th>
      <td>0</td>
    </tr>
    <tr>
      <th>HUNVFlag</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LowIncomeTracts</th>
      <td>0</td>
    </tr>
    <tr>
      <th>PovertyRate</th>
      <td>3</td>
    </tr>
    <tr>
      <th>MedianFamilyIncome</th>
      <td>748</td>
    </tr>
    <tr>
      <th>LA1and10</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LAhalfand10</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LA1and20</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LATracts_half</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LATracts1</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LATracts10</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LATracts20</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LATractsVehicle_20</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LAPOP05_10</th>
      <td>14540</td>
    </tr>
    <tr>
      <th>LALOWI05_10</th>
      <td>14540</td>
    </tr>
    <tr>
      <th>lapophalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lapophalfshare</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lalowihalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lalowihalfshare</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lakidshalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lakidshalfshare</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>laseniorshalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>laseniorshalfshare</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lawhitehalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lawhitehalfshare</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lablackhalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lablackhalfshare</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>laasianhalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>laasianhalfshare</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lanhopihalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lanhopihalfshare</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>laaianhalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>laaianhalfshare</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>laomultirhalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>laomultirhalfshare</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lahisphalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lahisphalfshare</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lahunvhalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lahunvhalfshare</th>
      <td>4562</td>
    </tr>
    <tr>
      <th>lasnaphalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lasnaphalfshare</th>
      <td>4562</td>
    </tr>
    <tr>
      <th>lapop1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lapop1share</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lalowi1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lalowi1share</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lakids1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lakids1share</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>laseniors1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>laseniors1share</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lawhite1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lawhite1share</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lablack1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lablack1share</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>laasian1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>laasian1share</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lanhopi1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lanhopi1share</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>laaian1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>laaian1share</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>laomultir1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>laomultir1share</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lahisp1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lahisp1share</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lahunv1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lahunv1share</th>
      <td>19966</td>
    </tr>
    <tr>
      <th>lasnap1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lasnap1share</th>
      <td>19966</td>
    </tr>
    <tr>
      <th>lanhopi10</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>lanhopi10share</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>laaian10</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>laaian10share</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>laomultir10</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>laomultir10share</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>lablack20</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>lablack20share</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>TractLOWI</th>
      <td>4</td>
    </tr>
    <tr>
      <th>TractKids</th>
      <td>4</td>
    </tr>
    <tr>
      <th>TractSeniors</th>
      <td>4</td>
    </tr>
    <tr>
      <th>TractWhite</th>
      <td>4</td>
    </tr>
    <tr>
      <th>TractBlack</th>
      <td>4</td>
    </tr>
    <tr>
      <th>TractAsian</th>
      <td>4</td>
    </tr>
    <tr>
      <th>TractNHOPI</th>
      <td>4</td>
    </tr>
    <tr>
      <th>TractAIAN</th>
      <td>4</td>
    </tr>
    <tr>
      <th>TractOMultir</th>
      <td>4</td>
    </tr>
    <tr>
      <th>TractHispanic</th>
      <td>4</td>
    </tr>
    <tr>
      <th>TractHUNV</th>
      <td>4</td>
    </tr>
    <tr>
      <th>TractSNAP</th>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div><br><label><b>dtype:</b> int64</label>




```python
food_access.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 72531 entries, 0 to 72530
    Data columns (total 99 columns):
     #   Column                Non-Null Count  Dtype  
    ---  ------                --------------  -----  
     0   CensusTract           72531 non-null  int64  
     1   State                 72531 non-null  object 
     2   County                72531 non-null  object 
     3   Urban                 72531 non-null  int64  
     4   Pop2010               72531 non-null  int64  
     5   OHU2010               72531 non-null  int64  
     6   GroupQuartersFlag     72531 non-null  int64  
     7   NUMGQTRS              72506 non-null  float64
     8   PCTGQTRS              72506 non-null  float64
     9   LILATracts_1And10     72531 non-null  int64  
     10  LILATracts_halfAnd10  72531 non-null  int64  
     11  LILATracts_1And20     72531 non-null  int64  
     12  LILATracts_Vehicle    72531 non-null  int64  
     13  HUNVFlag              72531 non-null  int64  
     14  LowIncomeTracts       72531 non-null  int64  
     15  PovertyRate           72528 non-null  float64
     16  MedianFamilyIncome    71783 non-null  float64
     17  LA1and10              72531 non-null  int64  
     18  LAhalfand10           72531 non-null  int64  
     19  LA1and20              72531 non-null  int64  
     20  LATracts_half         72531 non-null  int64  
     21  LATracts1             72531 non-null  int64  
     22  LATracts10            72531 non-null  int64  
     23  LATracts20            72531 non-null  int64  
     24  LATractsVehicle_20    72531 non-null  int64  
     25  LAPOP05_10            57991 non-null  float64
     26  LALOWI05_10           57991 non-null  float64
     27  lapophalf             67963 non-null  float64
     28  lapophalfshare        67963 non-null  float64
     29  lalowihalf            67963 non-null  float64
     30  lalowihalfshare       67963 non-null  float64
     31  lakidshalf            67963 non-null  float64
     32  lakidshalfshare       67963 non-null  float64
     33  laseniorshalf         67963 non-null  float64
     34  laseniorshalfshare    67963 non-null  float64
     35  lawhitehalf           67963 non-null  float64
     36  lawhitehalfshare      67963 non-null  float64
     37  lablackhalf           67963 non-null  float64
     38  lablackhalfshare      67963 non-null  float64
     39  laasianhalf           67963 non-null  float64
     40  laasianhalfshare      67963 non-null  float64
     41  lanhopihalf           67963 non-null  float64
     42  lanhopihalfshare      67963 non-null  float64
     43  laaianhalf            67963 non-null  float64
     44  laaianhalfshare       67963 non-null  float64
     45  laomultirhalf         67963 non-null  float64
     46  laomultirhalfshare    67963 non-null  float64
     47  lahisphalf            67963 non-null  float64
     48  lahisphalfshare       67963 non-null  float64
     49  lahunvhalf            67963 non-null  float64
     50  lahunvhalfshare       67969 non-null  float64
     51  lasnaphalf            67963 non-null  float64
     52  lasnaphalfshare       67969 non-null  float64
     53  lapop1                52542 non-null  float64
     54  lapop1share           52542 non-null  float64
     55  lalowi1               52542 non-null  float64
     56  lalowi1share          52542 non-null  float64
     57  lakids1               52542 non-null  float64
     58  lakids1share          52542 non-null  float64
     59  laseniors1            52542 non-null  float64
     60  laseniors1share       52542 non-null  float64
     61  lawhite1              52542 non-null  float64
     62  lawhite1share         52542 non-null  float64
     63  lablack1              52542 non-null  float64
     64  lablack1share         52542 non-null  float64
     65  laasian1              52542 non-null  float64
     66  laasian1share         52542 non-null  float64
     67  lanhopi1              52542 non-null  float64
     68  lanhopi1share         52542 non-null  float64
     69  laaian1               52542 non-null  float64
     70  laaian1share          52542 non-null  float64
     71  laomultir1            52542 non-null  float64
     72  laomultir1share       52542 non-null  float64
     73  lahisp1               52542 non-null  float64
     74  lahisp1share          52542 non-null  float64
     75  lahunv1               52542 non-null  float64
     76  lahunv1share          52565 non-null  float64
     77  lasnap1               52542 non-null  float64
     78  lasnap1share          52565 non-null  float64
     79  lanhopi10             7766 non-null   float64
     80  lanhopi10share        7766 non-null   float64
     81  laaian10              7766 non-null   float64
     82  laaian10share         7766 non-null   float64
     83  laomultir10           7766 non-null   float64
     84  laomultir10share      7766 non-null   float64
     85  lablack20             1506 non-null   float64
     86  lablack20share        1506 non-null   float64
     87  TractLOWI             72527 non-null  float64
     88  TractKids             72527 non-null  float64
     89  TractSeniors          72527 non-null  float64
     90  TractWhite            72527 non-null  float64
     91  TractBlack            72527 non-null  float64
     92  TractAsian            72527 non-null  float64
     93  TractNHOPI            72527 non-null  float64
     94  TractAIAN             72527 non-null  float64
     95  TractOMultir          72527 non-null  float64
     96  TractHispanic         72527 non-null  float64
     97  TractHUNV             72527 non-null  float64
     98  TractSNAP             72527 non-null  float64
    dtypes: float64(78), int64(19), object(2)
    memory usage: 54.8+ MB



```python
food_access.describe()
```





  <div id="df-a2e760c5-6a66-47e9-b9e7-9806f97217db" class="colab-df-container">
    <div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CensusTract</th>
      <th>Urban</th>
      <th>Pop2010</th>
      <th>OHU2010</th>
      <th>GroupQuartersFlag</th>
      <th>NUMGQTRS</th>
      <th>PCTGQTRS</th>
      <th>LILATracts_1And10</th>
      <th>LILATracts_halfAnd10</th>
      <th>LILATracts_1And20</th>
      <th>LILATracts_Vehicle</th>
      <th>HUNVFlag</th>
      <th>LowIncomeTracts</th>
      <th>PovertyRate</th>
      <th>MedianFamilyIncome</th>
      <th>LA1and10</th>
      <th>LAhalfand10</th>
      <th>LA1and20</th>
      <th>LATracts_half</th>
      <th>LATracts1</th>
      <th>LATracts10</th>
      <th>LATracts20</th>
      <th>LATractsVehicle_20</th>
      <th>LAPOP05_10</th>
      <th>LALOWI05_10</th>
      <th>lapophalf</th>
      <th>lapophalfshare</th>
      <th>lalowihalf</th>
      <th>lalowihalfshare</th>
      <th>lakidshalf</th>
      <th>lakidshalfshare</th>
      <th>laseniorshalf</th>
      <th>laseniorshalfshare</th>
      <th>lawhitehalf</th>
      <th>lawhitehalfshare</th>
      <th>lablackhalf</th>
      <th>lablackhalfshare</th>
      <th>laasianhalf</th>
      <th>laasianhalfshare</th>
      <th>lanhopihalf</th>
      <th>lanhopihalfshare</th>
      <th>laaianhalf</th>
      <th>laaianhalfshare</th>
      <th>laomultirhalf</th>
      <th>laomultirhalfshare</th>
      <th>lahisphalf</th>
      <th>lahisphalfshare</th>
      <th>lahunvhalf</th>
      <th>lahunvhalfshare</th>
      <th>lasnaphalf</th>
      <th>lasnaphalfshare</th>
      <th>lapop1</th>
      <th>lapop1share</th>
      <th>lalowi1</th>
      <th>lalowi1share</th>
      <th>lakids1</th>
      <th>lakids1share</th>
      <th>laseniors1</th>
      <th>laseniors1share</th>
      <th>lawhite1</th>
      <th>lawhite1share</th>
      <th>lablack1</th>
      <th>lablack1share</th>
      <th>laasian1</th>
      <th>laasian1share</th>
      <th>lanhopi1</th>
      <th>lanhopi1share</th>
      <th>laaian1</th>
      <th>laaian1share</th>
      <th>laomultir1</th>
      <th>laomultir1share</th>
      <th>lahisp1</th>
      <th>lahisp1share</th>
      <th>lahunv1</th>
      <th>lahunv1share</th>
      <th>lasnap1</th>
      <th>lasnap1share</th>
      <th>lanhopi10</th>
      <th>lanhopi10share</th>
      <th>laaian10</th>
      <th>laaian10share</th>
      <th>laomultir10</th>
      <th>laomultir10share</th>
      <th>lablack20</th>
      <th>lablack20share</th>
      <th>TractLOWI</th>
      <th>TractKids</th>
      <th>TractSeniors</th>
      <th>TractWhite</th>
      <th>TractBlack</th>
      <th>TractAsian</th>
      <th>TractNHOPI</th>
      <th>TractAIAN</th>
      <th>TractOMultir</th>
      <th>TractHispanic</th>
      <th>TractHUNV</th>
      <th>TractSNAP</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>7.253100e+04</td>
      <td>72531.000000</td>
      <td>72531.000000</td>
      <td>72531.000000</td>
      <td>72531.000000</td>
      <td>72506.000000</td>
      <td>72506.000000</td>
      <td>72531.000000</td>
      <td>72531.000000</td>
      <td>72531.000000</td>
      <td>72531.000000</td>
      <td>72531.000000</td>
      <td>72531.000000</td>
      <td>72528.000000</td>
      <td>71783.000000</td>
      <td>72531.000000</td>
      <td>72531.000000</td>
      <td>72531.000000</td>
      <td>72531.000000</td>
      <td>72531.000000</td>
      <td>72531.000000</td>
      <td>72531.000000</td>
      <td>72531.000000</td>
      <td>57991.000000</td>
      <td>57991.000000</td>
      <td>67963.000000</td>
      <td>67963.00000</td>
      <td>67963.000000</td>
      <td>67963.000000</td>
      <td>67963.000000</td>
      <td>67963.000000</td>
      <td>67963.000000</td>
      <td>67963.000000</td>
      <td>67963.000000</td>
      <td>67963.000000</td>
      <td>67963.000000</td>
      <td>67963.000000</td>
      <td>67963.000000</td>
      <td>67963.000000</td>
      <td>67963.000000</td>
      <td>67963.000000</td>
      <td>67963.000000</td>
      <td>67963.000000</td>
      <td>67963.000000</td>
      <td>67963.00000</td>
      <td>67963.000000</td>
      <td>67963.000000</td>
      <td>67963.000000</td>
      <td>67969.000000</td>
      <td>67963.000000</td>
      <td>67969.000000</td>
      <td>52542.000000</td>
      <td>52542.000000</td>
      <td>52542.000000</td>
      <td>52542.000000</td>
      <td>52542.000000</td>
      <td>52542.000000</td>
      <td>52542.000000</td>
      <td>52542.000000</td>
      <td>52542.000000</td>
      <td>52542.000000</td>
      <td>52542.000000</td>
      <td>52542.000000</td>
      <td>52542.000000</td>
      <td>52542.000000</td>
      <td>52542.000000</td>
      <td>52542.000000</td>
      <td>52542.000000</td>
      <td>52542.000000</td>
      <td>52542.000000</td>
      <td>52542.000000</td>
      <td>52542.000000</td>
      <td>52542.000000</td>
      <td>52542.000000</td>
      <td>52565.000000</td>
      <td>52542.000000</td>
      <td>52565.000000</td>
      <td>7766.000000</td>
      <td>7766.000000</td>
      <td>7766.000000</td>
      <td>7766.000000</td>
      <td>7766.000000</td>
      <td>7766.000000</td>
      <td>1506.000000</td>
      <td>1506.000000</td>
      <td>72527.000000</td>
      <td>72527.000000</td>
      <td>72527.000000</td>
      <td>72527.000000</td>
      <td>72527.000000</td>
      <td>72527.000000</td>
      <td>72527.000000</td>
      <td>72527.000000</td>
      <td>72527.000000</td>
      <td>72527.000000</td>
      <td>72527.000000</td>
      <td>72527.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>2.782573e+10</td>
      <td>0.760626</td>
      <td>4256.739022</td>
      <td>1609.191821</td>
      <td>0.007114</td>
      <td>110.121549</td>
      <td>2.708677</td>
      <td>0.128125</td>
      <td>0.279150</td>
      <td>0.112228</td>
      <td>0.139609</td>
      <td>0.210820</td>
      <td>0.417573</td>
      <td>15.183864</td>
      <td>77037.792249</td>
      <td>0.379810</td>
      <td>0.682756</td>
      <td>0.340668</td>
      <td>0.638830</td>
      <td>0.335884</td>
      <td>0.043926</td>
      <td>0.004784</td>
      <td>0.214750</td>
      <td>2657.206946</td>
      <td>797.488214</td>
      <td>3166.061901</td>
      <td>73.42577</td>
      <td>955.153495</td>
      <td>23.095219</td>
      <td>770.609493</td>
      <td>17.395343</td>
      <td>422.928564</td>
      <td>10.325693</td>
      <td>2428.490944</td>
      <td>56.060217</td>
      <td>360.950326</td>
      <td>9.064957</td>
      <td>115.071833</td>
      <td>2.398870</td>
      <td>4.783117</td>
      <td>0.104870</td>
      <td>31.484852</td>
      <td>0.806837</td>
      <td>225.295322</td>
      <td>4.98998</td>
      <td>401.074129</td>
      <td>8.631819</td>
      <td>69.491223</td>
      <td>4.684649</td>
      <td>135.491120</td>
      <td>8.934348</td>
      <td>2337.675612</td>
      <td>54.081743</td>
      <td>669.711107</td>
      <td>16.149574</td>
      <td>569.749496</td>
      <td>12.810448</td>
      <td>319.298675</td>
      <td>7.826267</td>
      <td>1904.910319</td>
      <td>44.084766</td>
      <td>218.471946</td>
      <td>5.243149</td>
      <td>57.908587</td>
      <td>1.172348</td>
      <td>2.883312</td>
      <td>0.063707</td>
      <td>27.301131</td>
      <td>0.724699</td>
      <td>126.201591</td>
      <td>2.793007</td>
      <td>215.850101</td>
      <td>4.630486</td>
      <td>39.596875</td>
      <td>2.631525</td>
      <td>92.520003</td>
      <td>5.995943</td>
      <td>0.521762</td>
      <td>0.026813</td>
      <td>38.426346</td>
      <td>1.250255</td>
      <td>30.291398</td>
      <td>0.971561</td>
      <td>3.717131</td>
      <td>0.138612</td>
      <td>1385.054352</td>
      <td>1022.695327</td>
      <td>555.197113</td>
      <td>3082.337157</td>
      <td>536.756160</td>
      <td>202.327685</td>
      <td>7.445655</td>
      <td>40.152316</td>
      <td>387.664649</td>
      <td>695.979277</td>
      <td>143.709736</td>
      <td>201.753182</td>
    </tr>
    <tr>
      <th>std</th>
      <td>1.581647e+10</td>
      <td>0.426704</td>
      <td>1955.987626</td>
      <td>725.676046</td>
      <td>0.084046</td>
      <td>443.931753</td>
      <td>9.570875</td>
      <td>0.334231</td>
      <td>0.448584</td>
      <td>0.315649</td>
      <td>0.346584</td>
      <td>0.407894</td>
      <td>0.493162</td>
      <td>11.919903</td>
      <td>37544.445885</td>
      <td>0.485343</td>
      <td>0.465406</td>
      <td>0.473937</td>
      <td>0.480343</td>
      <td>0.472302</td>
      <td>0.204932</td>
      <td>0.069002</td>
      <td>0.410651</td>
      <td>2044.331313</td>
      <td>771.432588</td>
      <td>2003.570508</td>
      <td>29.06663</td>
      <td>790.299662</td>
      <td>16.502754</td>
      <td>582.563153</td>
      <td>8.473848</td>
      <td>328.272913</td>
      <td>7.330619</td>
      <td>1772.177187</td>
      <td>30.344494</td>
      <td>687.258803</td>
      <td>16.866031</td>
      <td>269.501279</td>
      <td>4.930797</td>
      <td>33.925042</td>
      <td>0.776388</td>
      <td>173.356852</td>
      <td>4.574504</td>
      <td>331.576406</td>
      <td>6.17208</td>
      <td>742.022316</td>
      <td>13.411754</td>
      <td>80.667756</td>
      <td>6.011297</td>
      <td>135.906721</td>
      <td>9.072652</td>
      <td>1980.761103</td>
      <td>36.760908</td>
      <td>706.558756</td>
      <td>15.479861</td>
      <td>541.167867</td>
      <td>9.479667</td>
      <td>304.305296</td>
      <td>7.189503</td>
      <td>1730.446988</td>
      <td>33.825309</td>
      <td>514.874189</td>
      <td>12.092215</td>
      <td>163.044838</td>
      <td>2.947656</td>
      <td>27.618672</td>
      <td>0.687778</td>
      <td>182.466993</td>
      <td>4.889572</td>
      <td>230.437308</td>
      <td>4.390135</td>
      <td>516.519961</td>
      <td>9.393900</td>
      <td>55.315309</td>
      <td>4.072878</td>
      <td>111.490443</td>
      <td>7.311362</td>
      <td>5.977160</td>
      <td>0.987922</td>
      <td>284.216232</td>
      <td>8.045275</td>
      <td>94.638767</td>
      <td>2.712061</td>
      <td>33.886497</td>
      <td>0.897988</td>
      <td>983.709351</td>
      <td>615.445960</td>
      <td>351.805391</td>
      <td>1796.364560</td>
      <td>889.118109</td>
      <td>435.878339</td>
      <td>45.186581</td>
      <td>177.378696</td>
      <td>529.349680</td>
      <td>1119.472739</td>
      <td>232.738869</td>
      <td>185.760089</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1.001020e+09</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>2499.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.00000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.00000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>1.212708e+10</td>
      <td>1.000000</td>
      <td>2899.000000</td>
      <td>1108.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>6.500000</td>
      <td>51484.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1083.000000</td>
      <td>237.000000</td>
      <td>1756.000000</td>
      <td>55.63000</td>
      <td>380.000000</td>
      <td>10.160000</td>
      <td>369.000000</td>
      <td>11.550000</td>
      <td>195.000000</td>
      <td>5.290000</td>
      <td>1071.000000</td>
      <td>31.430000</td>
      <td>22.000000</td>
      <td>0.560000</td>
      <td>10.000000</td>
      <td>0.280000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>4.000000</td>
      <td>0.100000</td>
      <td>51.000000</td>
      <td>1.45000</td>
      <td>52.000000</td>
      <td>1.470000</td>
      <td>18.000000</td>
      <td>1.250000</td>
      <td>35.000000</td>
      <td>2.460000</td>
      <td>665.000000</td>
      <td>17.892500</td>
      <td>132.000000</td>
      <td>3.310000</td>
      <td>137.000000</td>
      <td>3.720000</td>
      <td>74.000000</td>
      <td>1.880000</td>
      <td>405.000000</td>
      <td>10.820000</td>
      <td>7.000000</td>
      <td>0.190000</td>
      <td>4.000000</td>
      <td>0.100000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>0.030000</td>
      <td>19.000000</td>
      <td>0.550000</td>
      <td>20.000000</td>
      <td>0.570000</td>
      <td>5.000000</td>
      <td>0.320000</td>
      <td>12.000000</td>
      <td>0.790000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.010000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>680.000000</td>
      <td>611.000000</td>
      <td>320.000000</td>
      <td>1848.000000</td>
      <td>43.000000</td>
      <td>17.000000</td>
      <td>0.000000</td>
      <td>7.000000</td>
      <td>85.000000</td>
      <td>88.000000</td>
      <td>36.000000</td>
      <td>67.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>2.712979e+10</td>
      <td>1.000000</td>
      <td>4011.000000</td>
      <td>1525.000000</td>
      <td>0.000000</td>
      <td>7.000000</td>
      <td>0.180000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>12.000000</td>
      <td>68821.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>2387.000000</td>
      <td>584.000000</td>
      <td>2926.000000</td>
      <td>83.50000</td>
      <td>769.000000</td>
      <td>19.990000</td>
      <td>673.000000</td>
      <td>18.640000</td>
      <td>373.000000</td>
      <td>9.770000</td>
      <td>2193.000000</td>
      <td>60.550000</td>
      <td>84.000000</td>
      <td>2.040000</td>
      <td>32.000000</td>
      <td>0.810000</td>
      <td>1.000000</td>
      <td>0.020000</td>
      <td>10.000000</td>
      <td>0.250000</td>
      <td>112.000000</td>
      <td>2.78000</td>
      <td>139.000000</td>
      <td>3.460000</td>
      <td>45.000000</td>
      <td>2.910000</td>
      <td>95.000000</td>
      <td>6.260000</td>
      <td>2003.000000</td>
      <td>55.215000</td>
      <td>464.000000</td>
      <td>11.710000</td>
      <td>456.000000</td>
      <td>12.480000</td>
      <td>259.000000</td>
      <td>6.550000</td>
      <td>1545.000000</td>
      <td>40.720000</td>
      <td>31.000000</td>
      <td>0.750000</td>
      <td>14.000000</td>
      <td>0.350000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>6.000000</td>
      <td>0.140000</td>
      <td>56.000000</td>
      <td>1.410000</td>
      <td>63.000000</td>
      <td>1.560000</td>
      <td>22.000000</td>
      <td>1.400000</td>
      <td>53.000000</td>
      <td>3.430000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>0.020000</td>
      <td>6.000000</td>
      <td>0.180000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1164.000000</td>
      <td>924.000000</td>
      <td>497.000000</td>
      <td>2914.000000</td>
      <td>160.000000</td>
      <td>58.000000</td>
      <td>1.000000</td>
      <td>15.000000</td>
      <td>186.000000</td>
      <td>243.000000</td>
      <td>82.000000</td>
      <td>152.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>4.103900e+10</td>
      <td>1.000000</td>
      <td>5330.500000</td>
      <td>2021.000000</td>
      <td>0.000000</td>
      <td>64.000000</td>
      <td>1.570000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>20.600000</td>
      <td>93868.500000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>3827.000000</td>
      <td>1128.500000</td>
      <td>4299.000000</td>
      <td>99.80000</td>
      <td>1329.000000</td>
      <td>32.910000</td>
      <td>1048.000000</td>
      <td>23.410000</td>
      <td>586.000000</td>
      <td>14.080000</td>
      <td>3476.000000</td>
      <td>82.920000</td>
      <td>355.000000</td>
      <td>8.580000</td>
      <td>104.000000</td>
      <td>2.340000</td>
      <td>3.000000</td>
      <td>0.070000</td>
      <td>22.000000</td>
      <td>0.520000</td>
      <td>256.000000</td>
      <td>5.93000</td>
      <td>400.000000</td>
      <td>9.370000</td>
      <td>92.000000</td>
      <td>5.800000</td>
      <td>193.000000</td>
      <td>12.470000</td>
      <td>3540.000000</td>
      <td>94.070000</td>
      <td>987.000000</td>
      <td>25.260000</td>
      <td>846.000000</td>
      <td>20.990000</td>
      <td>484.000000</td>
      <td>12.230000</td>
      <td>2969.000000</td>
      <td>75.867500</td>
      <td>161.000000</td>
      <td>3.780000</td>
      <td>46.000000</td>
      <td>1.030000</td>
      <td>1.000000</td>
      <td>0.030000</td>
      <td>15.000000</td>
      <td>0.350000</td>
      <td>135.000000</td>
      <td>3.080000</td>
      <td>182.000000</td>
      <td>4.170000</td>
      <td>54.000000</td>
      <td>3.400000</td>
      <td>134.000000</td>
      <td>8.660000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>6.000000</td>
      <td>0.180000</td>
      <td>24.000000</td>
      <td>0.760000</td>
      <td>1.000000</td>
      <td>0.020000</td>
      <td>1846.000000</td>
      <td>1312.000000</td>
      <td>718.000000</td>
      <td>4118.000000</td>
      <td>610.000000</td>
      <td>189.000000</td>
      <td>5.000000</td>
      <td>33.000000</td>
      <td>448.000000</td>
      <td>751.000000</td>
      <td>168.500000</td>
      <td>282.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>5.604595e+10</td>
      <td>1.000000</td>
      <td>37452.000000</td>
      <td>16043.000000</td>
      <td>1.000000</td>
      <td>19496.000000</td>
      <td>100.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>100.000000</td>
      <td>250001.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>32582.000000</td>
      <td>9874.000000</td>
      <td>37452.000000</td>
      <td>100.00000</td>
      <td>19602.000000</td>
      <td>100.000000</td>
      <td>9084.000000</td>
      <td>90.800000</td>
      <td>15261.000000</td>
      <td>100.000000</td>
      <td>28477.000000</td>
      <td>100.000000</td>
      <td>13594.000000</td>
      <td>100.000000</td>
      <td>6964.000000</td>
      <td>100.000000</td>
      <td>2786.000000</td>
      <td>85.880000</td>
      <td>8507.000000</td>
      <td>100.000000</td>
      <td>6415.000000</td>
      <td>100.00000</td>
      <td>12805.000000</td>
      <td>100.000000</td>
      <td>1803.000000</td>
      <td>100.000000</td>
      <td>1582.000000</td>
      <td>100.000000</td>
      <td>37061.000000</td>
      <td>100.000000</td>
      <td>19397.000000</td>
      <td>100.000000</td>
      <td>8907.000000</td>
      <td>90.800000</td>
      <td>10349.000000</td>
      <td>100.000000</td>
      <td>28165.000000</td>
      <td>100.000000</td>
      <td>12112.000000</td>
      <td>100.000000</td>
      <td>5809.000000</td>
      <td>100.000000</td>
      <td>2164.000000</td>
      <td>85.880000</td>
      <td>8444.000000</td>
      <td>100.000000</td>
      <td>6146.000000</td>
      <td>100.000000</td>
      <td>11502.000000</td>
      <td>100.000000</td>
      <td>1794.000000</td>
      <td>100.000000</td>
      <td>1582.000000</td>
      <td>100.000000</td>
      <td>266.000000</td>
      <td>85.880000</td>
      <td>6947.000000</td>
      <td>99.340000</td>
      <td>1724.000000</td>
      <td>45.450000</td>
      <td>1086.000000</td>
      <td>20.410000</td>
      <td>12562.000000</td>
      <td>11845.000000</td>
      <td>17271.000000</td>
      <td>28983.000000</td>
      <td>16804.000000</td>
      <td>10485.000000</td>
      <td>3491.000000</td>
      <td>9009.000000</td>
      <td>8839.000000</td>
      <td>15420.000000</td>
      <td>6059.000000</td>
      <td>2175.000000</td>
    </tr>
  </tbody>
</table>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-a2e760c5-6a66-47e9-b9e7-9806f97217db')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  
    </button>

  

    
  </div>


<div id="df-0370ff1c-e3ba-4e36-9483-ec14a55de970">
  <button class="colab-df-quickchart" onclick="quickchart('df-0370ff1c-e3ba-4e36-9483-ec14a55de970')"
            title="Suggest charts"
            style="display:none;">


  </button>



  
</div>

    </div>
  </div>





```python
maxValuesFA = food_access.max()

maxValuesFA

```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>CensusTract</th>
      <td>56045951300</td>
    </tr>
    <tr>
      <th>State</th>
      <td>Wyoming</td>
    </tr>
    <tr>
      <th>County</th>
      <td>Ziebach County</td>
    </tr>
    <tr>
      <th>Urban</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Pop2010</th>
      <td>37452</td>
    </tr>
    <tr>
      <th>OHU2010</th>
      <td>16043</td>
    </tr>
    <tr>
      <th>GroupQuartersFlag</th>
      <td>1</td>
    </tr>
    <tr>
      <th>NUMGQTRS</th>
      <td>19496.0</td>
    </tr>
    <tr>
      <th>PCTGQTRS</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>LILATracts_1And10</th>
      <td>1</td>
    </tr>
    <tr>
      <th>LILATracts_halfAnd10</th>
      <td>1</td>
    </tr>
    <tr>
      <th>LILATracts_1And20</th>
      <td>1</td>
    </tr>
    <tr>
      <th>LILATracts_Vehicle</th>
      <td>1</td>
    </tr>
    <tr>
      <th>HUNVFlag</th>
      <td>1</td>
    </tr>
    <tr>
      <th>LowIncomeTracts</th>
      <td>1</td>
    </tr>
    <tr>
      <th>PovertyRate</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>MedianFamilyIncome</th>
      <td>250001.0</td>
    </tr>
    <tr>
      <th>LA1and10</th>
      <td>1</td>
    </tr>
    <tr>
      <th>LAhalfand10</th>
      <td>1</td>
    </tr>
    <tr>
      <th>LA1and20</th>
      <td>1</td>
    </tr>
    <tr>
      <th>LATracts_half</th>
      <td>1</td>
    </tr>
    <tr>
      <th>LATracts1</th>
      <td>1</td>
    </tr>
    <tr>
      <th>LATracts10</th>
      <td>1</td>
    </tr>
    <tr>
      <th>LATracts20</th>
      <td>1</td>
    </tr>
    <tr>
      <th>LATractsVehicle_20</th>
      <td>1</td>
    </tr>
    <tr>
      <th>LAPOP05_10</th>
      <td>32582.0</td>
    </tr>
    <tr>
      <th>LALOWI05_10</th>
      <td>9874.0</td>
    </tr>
    <tr>
      <th>lapophalf</th>
      <td>37452.0</td>
    </tr>
    <tr>
      <th>lapophalfshare</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>lalowihalf</th>
      <td>19602.0</td>
    </tr>
    <tr>
      <th>lalowihalfshare</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>lakidshalf</th>
      <td>9084.0</td>
    </tr>
    <tr>
      <th>lakidshalfshare</th>
      <td>90.8</td>
    </tr>
    <tr>
      <th>laseniorshalf</th>
      <td>15261.0</td>
    </tr>
    <tr>
      <th>laseniorshalfshare</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>lawhitehalf</th>
      <td>28477.0</td>
    </tr>
    <tr>
      <th>lawhitehalfshare</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>lablackhalf</th>
      <td>13594.0</td>
    </tr>
    <tr>
      <th>lablackhalfshare</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>laasianhalf</th>
      <td>6964.0</td>
    </tr>
    <tr>
      <th>laasianhalfshare</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>lanhopihalf</th>
      <td>2786.0</td>
    </tr>
    <tr>
      <th>lanhopihalfshare</th>
      <td>85.88</td>
    </tr>
    <tr>
      <th>laaianhalf</th>
      <td>8507.0</td>
    </tr>
    <tr>
      <th>laaianhalfshare</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>laomultirhalf</th>
      <td>6415.0</td>
    </tr>
    <tr>
      <th>laomultirhalfshare</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>lahisphalf</th>
      <td>12805.0</td>
    </tr>
    <tr>
      <th>lahisphalfshare</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>lahunvhalf</th>
      <td>1803.0</td>
    </tr>
    <tr>
      <th>lahunvhalfshare</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>lasnaphalf</th>
      <td>1582.0</td>
    </tr>
    <tr>
      <th>lasnaphalfshare</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>lapop1</th>
      <td>37061.0</td>
    </tr>
    <tr>
      <th>lapop1share</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>lalowi1</th>
      <td>19397.0</td>
    </tr>
    <tr>
      <th>lalowi1share</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>lakids1</th>
      <td>8907.0</td>
    </tr>
    <tr>
      <th>lakids1share</th>
      <td>90.8</td>
    </tr>
    <tr>
      <th>laseniors1</th>
      <td>10349.0</td>
    </tr>
    <tr>
      <th>laseniors1share</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>lawhite1</th>
      <td>28165.0</td>
    </tr>
    <tr>
      <th>lawhite1share</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>lablack1</th>
      <td>12112.0</td>
    </tr>
    <tr>
      <th>lablack1share</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>laasian1</th>
      <td>5809.0</td>
    </tr>
    <tr>
      <th>laasian1share</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>lanhopi1</th>
      <td>2164.0</td>
    </tr>
    <tr>
      <th>lanhopi1share</th>
      <td>85.88</td>
    </tr>
    <tr>
      <th>laaian1</th>
      <td>8444.0</td>
    </tr>
    <tr>
      <th>laaian1share</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>laomultir1</th>
      <td>6146.0</td>
    </tr>
    <tr>
      <th>laomultir1share</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>lahisp1</th>
      <td>11502.0</td>
    </tr>
    <tr>
      <th>lahisp1share</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>lahunv1</th>
      <td>1794.0</td>
    </tr>
    <tr>
      <th>lahunv1share</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>lasnap1</th>
      <td>1582.0</td>
    </tr>
    <tr>
      <th>lasnap1share</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>lanhopi10</th>
      <td>266.0</td>
    </tr>
    <tr>
      <th>lanhopi10share</th>
      <td>85.88</td>
    </tr>
    <tr>
      <th>laaian10</th>
      <td>6947.0</td>
    </tr>
    <tr>
      <th>laaian10share</th>
      <td>99.34</td>
    </tr>
    <tr>
      <th>laomultir10</th>
      <td>1724.0</td>
    </tr>
    <tr>
      <th>laomultir10share</th>
      <td>45.45</td>
    </tr>
    <tr>
      <th>lablack20</th>
      <td>1086.0</td>
    </tr>
    <tr>
      <th>lablack20share</th>
      <td>20.41</td>
    </tr>
    <tr>
      <th>TractLOWI</th>
      <td>12562.0</td>
    </tr>
    <tr>
      <th>TractKids</th>
      <td>11845.0</td>
    </tr>
    <tr>
      <th>TractSeniors</th>
      <td>17271.0</td>
    </tr>
    <tr>
      <th>TractWhite</th>
      <td>28983.0</td>
    </tr>
    <tr>
      <th>TractBlack</th>
      <td>16804.0</td>
    </tr>
    <tr>
      <th>TractAsian</th>
      <td>10485.0</td>
    </tr>
    <tr>
      <th>TractNHOPI</th>
      <td>3491.0</td>
    </tr>
    <tr>
      <th>TractAIAN</th>
      <td>9009.0</td>
    </tr>
    <tr>
      <th>TractOMultir</th>
      <td>8839.0</td>
    </tr>
    <tr>
      <th>TractHispanic</th>
      <td>15420.0</td>
    </tr>
    <tr>
      <th>TractHUNV</th>
      <td>6059.0</td>
    </tr>
    <tr>
      <th>TractSNAP</th>
      <td>2175.0</td>
    </tr>
  </tbody>
</table>
</div><br><label><b>dtype:</b> object</label>




```python
minValuesFA = food_access.min()
minValuesFA

```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>CensusTract</th>
      <td>1001020100</td>
    </tr>
    <tr>
      <th>State</th>
      <td>Alabama</td>
    </tr>
    <tr>
      <th>County</th>
      <td>Abbeville County</td>
    </tr>
    <tr>
      <th>Urban</th>
      <td>0</td>
    </tr>
    <tr>
      <th>Pop2010</th>
      <td>1</td>
    </tr>
    <tr>
      <th>OHU2010</th>
      <td>0</td>
    </tr>
    <tr>
      <th>GroupQuartersFlag</th>
      <td>0</td>
    </tr>
    <tr>
      <th>NUMGQTRS</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>PCTGQTRS</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>LILATracts_1And10</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LILATracts_halfAnd10</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LILATracts_1And20</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LILATracts_Vehicle</th>
      <td>0</td>
    </tr>
    <tr>
      <th>HUNVFlag</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LowIncomeTracts</th>
      <td>0</td>
    </tr>
    <tr>
      <th>PovertyRate</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>MedianFamilyIncome</th>
      <td>2499.0</td>
    </tr>
    <tr>
      <th>LA1and10</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LAhalfand10</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LA1and20</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LATracts_half</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LATracts1</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LATracts10</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LATracts20</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LATractsVehicle_20</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LAPOP05_10</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>LALOWI05_10</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lapophalf</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lapophalfshare</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lalowihalf</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lalowihalfshare</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lakidshalf</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lakidshalfshare</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>laseniorshalf</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>laseniorshalfshare</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lawhitehalf</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lawhitehalfshare</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lablackhalf</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lablackhalfshare</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>laasianhalf</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>laasianhalfshare</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lanhopihalf</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lanhopihalfshare</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>laaianhalf</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>laaianhalfshare</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>laomultirhalf</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>laomultirhalfshare</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lahisphalf</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lahisphalfshare</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lahunvhalf</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lahunvhalfshare</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lasnaphalf</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lasnaphalfshare</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lapop1</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lapop1share</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lalowi1</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lalowi1share</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lakids1</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lakids1share</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>laseniors1</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>laseniors1share</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lawhite1</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lawhite1share</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lablack1</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lablack1share</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>laasian1</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>laasian1share</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lanhopi1</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lanhopi1share</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>laaian1</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>laaian1share</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>laomultir1</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>laomultir1share</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lahisp1</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lahisp1share</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lahunv1</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lahunv1share</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lasnap1</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lasnap1share</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lanhopi10</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lanhopi10share</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>laaian10</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>laaian10share</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>laomultir10</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>laomultir10share</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lablack20</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lablack20share</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>TractLOWI</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>TractKids</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>TractSeniors</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>TractWhite</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>TractBlack</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>TractAsian</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>TractNHOPI</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>TractAIAN</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>TractOMultir</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>TractHispanic</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>TractHUNV</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>TractSNAP</th>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div><br><label><b>dtype:</b> object</label>




```python
food_access.describe().T

```





  <div id="df-97995fb2-9bc8-4387-bbf3-82bfd0c984b1" class="colab-df-container">
    <div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>count</th>
      <th>mean</th>
      <th>std</th>
      <th>min</th>
      <th>25%</th>
      <th>50%</th>
      <th>75%</th>
      <th>max</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>CensusTract</th>
      <td>72531.0</td>
      <td>2.782573e+10</td>
      <td>1.581647e+10</td>
      <td>1.001020e+09</td>
      <td>1.212708e+10</td>
      <td>2.712979e+10</td>
      <td>4.103900e+10</td>
      <td>5.604595e+10</td>
    </tr>
    <tr>
      <th>Urban</th>
      <td>72531.0</td>
      <td>7.606265e-01</td>
      <td>4.267040e-01</td>
      <td>0.000000e+00</td>
      <td>1.000000e+00</td>
      <td>1.000000e+00</td>
      <td>1.000000e+00</td>
      <td>1.000000e+00</td>
    </tr>
    <tr>
      <th>Pop2010</th>
      <td>72531.0</td>
      <td>4.256739e+03</td>
      <td>1.955988e+03</td>
      <td>1.000000e+00</td>
      <td>2.899000e+03</td>
      <td>4.011000e+03</td>
      <td>5.330500e+03</td>
      <td>3.745200e+04</td>
    </tr>
    <tr>
      <th>OHU2010</th>
      <td>72531.0</td>
      <td>1.609192e+03</td>
      <td>7.256760e+02</td>
      <td>0.000000e+00</td>
      <td>1.108000e+03</td>
      <td>1.525000e+03</td>
      <td>2.021000e+03</td>
      <td>1.604300e+04</td>
    </tr>
    <tr>
      <th>GroupQuartersFlag</th>
      <td>72531.0</td>
      <td>7.114199e-03</td>
      <td>8.404573e-02</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e+00</td>
    </tr>
    <tr>
      <th>NUMGQTRS</th>
      <td>72506.0</td>
      <td>1.101215e+02</td>
      <td>4.439318e+02</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>7.000000e+00</td>
      <td>6.400000e+01</td>
      <td>1.949600e+04</td>
    </tr>
    <tr>
      <th>PCTGQTRS</th>
      <td>72506.0</td>
      <td>2.708677e+00</td>
      <td>9.570875e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>1.800000e-01</td>
      <td>1.570000e+00</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>LILATracts_1And10</th>
      <td>72531.0</td>
      <td>1.281245e-01</td>
      <td>3.342307e-01</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e+00</td>
    </tr>
    <tr>
      <th>LILATracts_halfAnd10</th>
      <td>72531.0</td>
      <td>2.791496e-01</td>
      <td>4.485843e-01</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e+00</td>
      <td>1.000000e+00</td>
    </tr>
    <tr>
      <th>LILATracts_1And20</th>
      <td>72531.0</td>
      <td>1.122279e-01</td>
      <td>3.156488e-01</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e+00</td>
    </tr>
    <tr>
      <th>LILATracts_Vehicle</th>
      <td>72531.0</td>
      <td>1.396093e-01</td>
      <td>3.465836e-01</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e+00</td>
    </tr>
    <tr>
      <th>HUNVFlag</th>
      <td>72531.0</td>
      <td>2.108202e-01</td>
      <td>4.078938e-01</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e+00</td>
    </tr>
    <tr>
      <th>LowIncomeTracts</th>
      <td>72531.0</td>
      <td>4.175732e-01</td>
      <td>4.931624e-01</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e+00</td>
      <td>1.000000e+00</td>
    </tr>
    <tr>
      <th>PovertyRate</th>
      <td>72528.0</td>
      <td>1.518386e+01</td>
      <td>1.191990e+01</td>
      <td>0.000000e+00</td>
      <td>6.500000e+00</td>
      <td>1.200000e+01</td>
      <td>2.060000e+01</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>MedianFamilyIncome</th>
      <td>71783.0</td>
      <td>7.703779e+04</td>
      <td>3.754445e+04</td>
      <td>2.499000e+03</td>
      <td>5.148400e+04</td>
      <td>6.882100e+04</td>
      <td>9.386850e+04</td>
      <td>2.500010e+05</td>
    </tr>
    <tr>
      <th>LA1and10</th>
      <td>72531.0</td>
      <td>3.798100e-01</td>
      <td>4.853428e-01</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e+00</td>
      <td>1.000000e+00</td>
    </tr>
    <tr>
      <th>LAhalfand10</th>
      <td>72531.0</td>
      <td>6.827563e-01</td>
      <td>4.654064e-01</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e+00</td>
      <td>1.000000e+00</td>
      <td>1.000000e+00</td>
    </tr>
    <tr>
      <th>LA1and20</th>
      <td>72531.0</td>
      <td>3.406681e-01</td>
      <td>4.739372e-01</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e+00</td>
      <td>1.000000e+00</td>
    </tr>
    <tr>
      <th>LATracts_half</th>
      <td>72531.0</td>
      <td>6.388303e-01</td>
      <td>4.803429e-01</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e+00</td>
      <td>1.000000e+00</td>
      <td>1.000000e+00</td>
    </tr>
    <tr>
      <th>LATracts1</th>
      <td>72531.0</td>
      <td>3.358840e-01</td>
      <td>4.723018e-01</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e+00</td>
      <td>1.000000e+00</td>
    </tr>
    <tr>
      <th>LATracts10</th>
      <td>72531.0</td>
      <td>4.392605e-02</td>
      <td>2.049320e-01</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e+00</td>
    </tr>
    <tr>
      <th>LATracts20</th>
      <td>72531.0</td>
      <td>4.784161e-03</td>
      <td>6.900245e-02</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e+00</td>
    </tr>
    <tr>
      <th>LATractsVehicle_20</th>
      <td>72531.0</td>
      <td>2.147496e-01</td>
      <td>4.106513e-01</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e+00</td>
    </tr>
    <tr>
      <th>LAPOP05_10</th>
      <td>57991.0</td>
      <td>2.657207e+03</td>
      <td>2.044331e+03</td>
      <td>0.000000e+00</td>
      <td>1.083000e+03</td>
      <td>2.387000e+03</td>
      <td>3.827000e+03</td>
      <td>3.258200e+04</td>
    </tr>
    <tr>
      <th>LALOWI05_10</th>
      <td>57991.0</td>
      <td>7.974882e+02</td>
      <td>7.714326e+02</td>
      <td>0.000000e+00</td>
      <td>2.370000e+02</td>
      <td>5.840000e+02</td>
      <td>1.128500e+03</td>
      <td>9.874000e+03</td>
    </tr>
    <tr>
      <th>lapophalf</th>
      <td>67963.0</td>
      <td>3.166062e+03</td>
      <td>2.003571e+03</td>
      <td>0.000000e+00</td>
      <td>1.756000e+03</td>
      <td>2.926000e+03</td>
      <td>4.299000e+03</td>
      <td>3.745200e+04</td>
    </tr>
    <tr>
      <th>lapophalfshare</th>
      <td>67963.0</td>
      <td>7.342577e+01</td>
      <td>2.906663e+01</td>
      <td>0.000000e+00</td>
      <td>5.563000e+01</td>
      <td>8.350000e+01</td>
      <td>9.980000e+01</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>lalowihalf</th>
      <td>67963.0</td>
      <td>9.551535e+02</td>
      <td>7.902997e+02</td>
      <td>0.000000e+00</td>
      <td>3.800000e+02</td>
      <td>7.690000e+02</td>
      <td>1.329000e+03</td>
      <td>1.960200e+04</td>
    </tr>
    <tr>
      <th>lalowihalfshare</th>
      <td>67963.0</td>
      <td>2.309522e+01</td>
      <td>1.650275e+01</td>
      <td>0.000000e+00</td>
      <td>1.016000e+01</td>
      <td>1.999000e+01</td>
      <td>3.291000e+01</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>lakidshalf</th>
      <td>67963.0</td>
      <td>7.706095e+02</td>
      <td>5.825632e+02</td>
      <td>0.000000e+00</td>
      <td>3.690000e+02</td>
      <td>6.730000e+02</td>
      <td>1.048000e+03</td>
      <td>9.084000e+03</td>
    </tr>
    <tr>
      <th>lakidshalfshare</th>
      <td>67963.0</td>
      <td>1.739534e+01</td>
      <td>8.473848e+00</td>
      <td>0.000000e+00</td>
      <td>1.155000e+01</td>
      <td>1.864000e+01</td>
      <td>2.341000e+01</td>
      <td>9.080000e+01</td>
    </tr>
    <tr>
      <th>laseniorshalf</th>
      <td>67963.0</td>
      <td>4.229286e+02</td>
      <td>3.282729e+02</td>
      <td>0.000000e+00</td>
      <td>1.950000e+02</td>
      <td>3.730000e+02</td>
      <td>5.860000e+02</td>
      <td>1.526100e+04</td>
    </tr>
    <tr>
      <th>laseniorshalfshare</th>
      <td>67963.0</td>
      <td>1.032569e+01</td>
      <td>7.330619e+00</td>
      <td>0.000000e+00</td>
      <td>5.290000e+00</td>
      <td>9.770000e+00</td>
      <td>1.408000e+01</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>lawhitehalf</th>
      <td>67963.0</td>
      <td>2.428491e+03</td>
      <td>1.772177e+03</td>
      <td>0.000000e+00</td>
      <td>1.071000e+03</td>
      <td>2.193000e+03</td>
      <td>3.476000e+03</td>
      <td>2.847700e+04</td>
    </tr>
    <tr>
      <th>lawhitehalfshare</th>
      <td>67963.0</td>
      <td>5.606022e+01</td>
      <td>3.034449e+01</td>
      <td>0.000000e+00</td>
      <td>3.143000e+01</td>
      <td>6.055000e+01</td>
      <td>8.292000e+01</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>lablackhalf</th>
      <td>67963.0</td>
      <td>3.609503e+02</td>
      <td>6.872588e+02</td>
      <td>0.000000e+00</td>
      <td>2.200000e+01</td>
      <td>8.400000e+01</td>
      <td>3.550000e+02</td>
      <td>1.359400e+04</td>
    </tr>
    <tr>
      <th>lablackhalfshare</th>
      <td>67963.0</td>
      <td>9.064957e+00</td>
      <td>1.686603e+01</td>
      <td>0.000000e+00</td>
      <td>5.600000e-01</td>
      <td>2.040000e+00</td>
      <td>8.580000e+00</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>laasianhalf</th>
      <td>67963.0</td>
      <td>1.150718e+02</td>
      <td>2.695013e+02</td>
      <td>0.000000e+00</td>
      <td>1.000000e+01</td>
      <td>3.200000e+01</td>
      <td>1.040000e+02</td>
      <td>6.964000e+03</td>
    </tr>
    <tr>
      <th>laasianhalfshare</th>
      <td>67963.0</td>
      <td>2.398870e+00</td>
      <td>4.930797e+00</td>
      <td>0.000000e+00</td>
      <td>2.800000e-01</td>
      <td>8.100000e-01</td>
      <td>2.340000e+00</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>lanhopihalf</th>
      <td>67963.0</td>
      <td>4.783117e+00</td>
      <td>3.392504e+01</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e+00</td>
      <td>3.000000e+00</td>
      <td>2.786000e+03</td>
    </tr>
    <tr>
      <th>lanhopihalfshare</th>
      <td>67963.0</td>
      <td>1.048703e-01</td>
      <td>7.763883e-01</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>2.000000e-02</td>
      <td>7.000000e-02</td>
      <td>8.588000e+01</td>
    </tr>
    <tr>
      <th>laaianhalf</th>
      <td>67963.0</td>
      <td>3.148485e+01</td>
      <td>1.733569e+02</td>
      <td>0.000000e+00</td>
      <td>4.000000e+00</td>
      <td>1.000000e+01</td>
      <td>2.200000e+01</td>
      <td>8.507000e+03</td>
    </tr>
    <tr>
      <th>laaianhalfshare</th>
      <td>67963.0</td>
      <td>8.068372e-01</td>
      <td>4.574504e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e-01</td>
      <td>2.500000e-01</td>
      <td>5.200000e-01</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>laomultirhalf</th>
      <td>67963.0</td>
      <td>2.252953e+02</td>
      <td>3.315764e+02</td>
      <td>0.000000e+00</td>
      <td>5.100000e+01</td>
      <td>1.120000e+02</td>
      <td>2.560000e+02</td>
      <td>6.415000e+03</td>
    </tr>
    <tr>
      <th>laomultirhalfshare</th>
      <td>67963.0</td>
      <td>4.989980e+00</td>
      <td>6.172080e+00</td>
      <td>0.000000e+00</td>
      <td>1.450000e+00</td>
      <td>2.780000e+00</td>
      <td>5.930000e+00</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>lahisphalf</th>
      <td>67963.0</td>
      <td>4.010741e+02</td>
      <td>7.420223e+02</td>
      <td>0.000000e+00</td>
      <td>5.200000e+01</td>
      <td>1.390000e+02</td>
      <td>4.000000e+02</td>
      <td>1.280500e+04</td>
    </tr>
    <tr>
      <th>lahisphalfshare</th>
      <td>67963.0</td>
      <td>8.631819e+00</td>
      <td>1.341175e+01</td>
      <td>0.000000e+00</td>
      <td>1.470000e+00</td>
      <td>3.460000e+00</td>
      <td>9.370000e+00</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>lahunvhalf</th>
      <td>67963.0</td>
      <td>6.949122e+01</td>
      <td>8.066776e+01</td>
      <td>0.000000e+00</td>
      <td>1.800000e+01</td>
      <td>4.500000e+01</td>
      <td>9.200000e+01</td>
      <td>1.803000e+03</td>
    </tr>
    <tr>
      <th>lahunvhalfshare</th>
      <td>67969.0</td>
      <td>4.684649e+00</td>
      <td>6.011297e+00</td>
      <td>0.000000e+00</td>
      <td>1.250000e+00</td>
      <td>2.910000e+00</td>
      <td>5.800000e+00</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>lasnaphalf</th>
      <td>67963.0</td>
      <td>1.354911e+02</td>
      <td>1.359067e+02</td>
      <td>0.000000e+00</td>
      <td>3.500000e+01</td>
      <td>9.500000e+01</td>
      <td>1.930000e+02</td>
      <td>1.582000e+03</td>
    </tr>
    <tr>
      <th>lasnaphalfshare</th>
      <td>67969.0</td>
      <td>8.934348e+00</td>
      <td>9.072652e+00</td>
      <td>0.000000e+00</td>
      <td>2.460000e+00</td>
      <td>6.260000e+00</td>
      <td>1.247000e+01</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>lapop1</th>
      <td>52542.0</td>
      <td>2.337676e+03</td>
      <td>1.980761e+03</td>
      <td>0.000000e+00</td>
      <td>6.650000e+02</td>
      <td>2.003000e+03</td>
      <td>3.540000e+03</td>
      <td>3.706100e+04</td>
    </tr>
    <tr>
      <th>lapop1share</th>
      <td>52542.0</td>
      <td>5.408174e+01</td>
      <td>3.676091e+01</td>
      <td>0.000000e+00</td>
      <td>1.789250e+01</td>
      <td>5.521500e+01</td>
      <td>9.407000e+01</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>lalowi1</th>
      <td>52542.0</td>
      <td>6.697111e+02</td>
      <td>7.065588e+02</td>
      <td>0.000000e+00</td>
      <td>1.320000e+02</td>
      <td>4.640000e+02</td>
      <td>9.870000e+02</td>
      <td>1.939700e+04</td>
    </tr>
    <tr>
      <th>lalowi1share</th>
      <td>52542.0</td>
      <td>1.614957e+01</td>
      <td>1.547986e+01</td>
      <td>0.000000e+00</td>
      <td>3.310000e+00</td>
      <td>1.171000e+01</td>
      <td>2.526000e+01</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>lakids1</th>
      <td>52542.0</td>
      <td>5.697495e+02</td>
      <td>5.411679e+02</td>
      <td>0.000000e+00</td>
      <td>1.370000e+02</td>
      <td>4.560000e+02</td>
      <td>8.460000e+02</td>
      <td>8.907000e+03</td>
    </tr>
    <tr>
      <th>lakids1share</th>
      <td>52542.0</td>
      <td>1.281045e+01</td>
      <td>9.479667e+00</td>
      <td>0.000000e+00</td>
      <td>3.720000e+00</td>
      <td>1.248000e+01</td>
      <td>2.099000e+01</td>
      <td>9.080000e+01</td>
    </tr>
    <tr>
      <th>laseniors1</th>
      <td>52542.0</td>
      <td>3.192987e+02</td>
      <td>3.043053e+02</td>
      <td>0.000000e+00</td>
      <td>7.400000e+01</td>
      <td>2.590000e+02</td>
      <td>4.840000e+02</td>
      <td>1.034900e+04</td>
    </tr>
    <tr>
      <th>laseniors1share</th>
      <td>52542.0</td>
      <td>7.826267e+00</td>
      <td>7.189503e+00</td>
      <td>0.000000e+00</td>
      <td>1.880000e+00</td>
      <td>6.550000e+00</td>
      <td>1.223000e+01</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>lawhite1</th>
      <td>52542.0</td>
      <td>1.904910e+03</td>
      <td>1.730447e+03</td>
      <td>0.000000e+00</td>
      <td>4.050000e+02</td>
      <td>1.545000e+03</td>
      <td>2.969000e+03</td>
      <td>2.816500e+04</td>
    </tr>
    <tr>
      <th>lawhite1share</th>
      <td>52542.0</td>
      <td>4.408477e+01</td>
      <td>3.382531e+01</td>
      <td>0.000000e+00</td>
      <td>1.082000e+01</td>
      <td>4.072000e+01</td>
      <td>7.586750e+01</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>lablack1</th>
      <td>52542.0</td>
      <td>2.184719e+02</td>
      <td>5.148742e+02</td>
      <td>0.000000e+00</td>
      <td>7.000000e+00</td>
      <td>3.100000e+01</td>
      <td>1.610000e+02</td>
      <td>1.211200e+04</td>
    </tr>
    <tr>
      <th>lablack1share</th>
      <td>52542.0</td>
      <td>5.243149e+00</td>
      <td>1.209222e+01</td>
      <td>0.000000e+00</td>
      <td>1.900000e-01</td>
      <td>7.500000e-01</td>
      <td>3.780000e+00</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>laasian1</th>
      <td>52542.0</td>
      <td>5.790859e+01</td>
      <td>1.630448e+02</td>
      <td>0.000000e+00</td>
      <td>4.000000e+00</td>
      <td>1.400000e+01</td>
      <td>4.600000e+01</td>
      <td>5.809000e+03</td>
    </tr>
    <tr>
      <th>laasian1share</th>
      <td>52542.0</td>
      <td>1.172348e+00</td>
      <td>2.947656e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e-01</td>
      <td>3.500000e-01</td>
      <td>1.030000e+00</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>lanhopi1</th>
      <td>52542.0</td>
      <td>2.883312e+00</td>
      <td>2.761867e+01</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e+00</td>
      <td>2.164000e+03</td>
    </tr>
    <tr>
      <th>lanhopi1share</th>
      <td>52542.0</td>
      <td>6.370675e-02</td>
      <td>6.877782e-01</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>3.000000e-02</td>
      <td>8.588000e+01</td>
    </tr>
    <tr>
      <th>laaian1</th>
      <td>52542.0</td>
      <td>2.730113e+01</td>
      <td>1.824670e+02</td>
      <td>0.000000e+00</td>
      <td>1.000000e+00</td>
      <td>6.000000e+00</td>
      <td>1.500000e+01</td>
      <td>8.444000e+03</td>
    </tr>
    <tr>
      <th>laaian1share</th>
      <td>52542.0</td>
      <td>7.246991e-01</td>
      <td>4.889572e+00</td>
      <td>0.000000e+00</td>
      <td>3.000000e-02</td>
      <td>1.400000e-01</td>
      <td>3.500000e-01</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>laomultir1</th>
      <td>52542.0</td>
      <td>1.262016e+02</td>
      <td>2.304373e+02</td>
      <td>0.000000e+00</td>
      <td>1.900000e+01</td>
      <td>5.600000e+01</td>
      <td>1.350000e+02</td>
      <td>6.146000e+03</td>
    </tr>
    <tr>
      <th>laomultir1share</th>
      <td>52542.0</td>
      <td>2.793007e+00</td>
      <td>4.390135e+00</td>
      <td>0.000000e+00</td>
      <td>5.500000e-01</td>
      <td>1.410000e+00</td>
      <td>3.080000e+00</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>lahisp1</th>
      <td>52542.0</td>
      <td>2.158501e+02</td>
      <td>5.165200e+02</td>
      <td>0.000000e+00</td>
      <td>2.000000e+01</td>
      <td>6.300000e+01</td>
      <td>1.820000e+02</td>
      <td>1.150200e+04</td>
    </tr>
    <tr>
      <th>lahisp1share</th>
      <td>52542.0</td>
      <td>4.630486e+00</td>
      <td>9.393900e+00</td>
      <td>0.000000e+00</td>
      <td>5.700000e-01</td>
      <td>1.560000e+00</td>
      <td>4.170000e+00</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>lahunv1</th>
      <td>52542.0</td>
      <td>3.959687e+01</td>
      <td>5.531531e+01</td>
      <td>0.000000e+00</td>
      <td>5.000000e+00</td>
      <td>2.200000e+01</td>
      <td>5.400000e+01</td>
      <td>1.794000e+03</td>
    </tr>
    <tr>
      <th>lahunv1share</th>
      <td>52565.0</td>
      <td>2.631525e+00</td>
      <td>4.072878e+00</td>
      <td>0.000000e+00</td>
      <td>3.200000e-01</td>
      <td>1.400000e+00</td>
      <td>3.400000e+00</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>lasnap1</th>
      <td>52542.0</td>
      <td>9.252000e+01</td>
      <td>1.114904e+02</td>
      <td>0.000000e+00</td>
      <td>1.200000e+01</td>
      <td>5.300000e+01</td>
      <td>1.340000e+02</td>
      <td>1.582000e+03</td>
    </tr>
    <tr>
      <th>lasnap1share</th>
      <td>52565.0</td>
      <td>5.995943e+00</td>
      <td>7.311362e+00</td>
      <td>0.000000e+00</td>
      <td>7.900000e-01</td>
      <td>3.430000e+00</td>
      <td>8.660000e+00</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>lanhopi10</th>
      <td>7766.0</td>
      <td>5.217615e-01</td>
      <td>5.977160e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>2.660000e+02</td>
    </tr>
    <tr>
      <th>lanhopi10share</th>
      <td>7766.0</td>
      <td>2.681303e-02</td>
      <td>9.879220e-01</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>8.588000e+01</td>
    </tr>
    <tr>
      <th>laaian10</th>
      <td>7766.0</td>
      <td>3.842635e+01</td>
      <td>2.842162e+02</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e+00</td>
      <td>6.000000e+00</td>
      <td>6.947000e+03</td>
    </tr>
    <tr>
      <th>laaian10share</th>
      <td>7766.0</td>
      <td>1.250255e+00</td>
      <td>8.045275e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>2.000000e-02</td>
      <td>1.800000e-01</td>
      <td>9.934000e+01</td>
    </tr>
    <tr>
      <th>laomultir10</th>
      <td>7766.0</td>
      <td>3.029140e+01</td>
      <td>9.463877e+01</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>6.000000e+00</td>
      <td>2.400000e+01</td>
      <td>1.724000e+03</td>
    </tr>
    <tr>
      <th>laomultir10share</th>
      <td>7766.0</td>
      <td>9.715606e-01</td>
      <td>2.712061e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e-02</td>
      <td>1.800000e-01</td>
      <td>7.600000e-01</td>
      <td>4.545000e+01</td>
    </tr>
    <tr>
      <th>lablack20</th>
      <td>1506.0</td>
      <td>3.717131e+00</td>
      <td>3.388650e+01</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e+00</td>
      <td>1.086000e+03</td>
    </tr>
    <tr>
      <th>lablack20share</th>
      <td>1506.0</td>
      <td>1.386122e-01</td>
      <td>8.979877e-01</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>2.000000e-02</td>
      <td>2.041000e+01</td>
    </tr>
    <tr>
      <th>TractLOWI</th>
      <td>72527.0</td>
      <td>1.385054e+03</td>
      <td>9.837094e+02</td>
      <td>0.000000e+00</td>
      <td>6.800000e+02</td>
      <td>1.164000e+03</td>
      <td>1.846000e+03</td>
      <td>1.256200e+04</td>
    </tr>
    <tr>
      <th>TractKids</th>
      <td>72527.0</td>
      <td>1.022695e+03</td>
      <td>6.154460e+02</td>
      <td>0.000000e+00</td>
      <td>6.110000e+02</td>
      <td>9.240000e+02</td>
      <td>1.312000e+03</td>
      <td>1.184500e+04</td>
    </tr>
    <tr>
      <th>TractSeniors</th>
      <td>72527.0</td>
      <td>5.551971e+02</td>
      <td>3.518054e+02</td>
      <td>0.000000e+00</td>
      <td>3.200000e+02</td>
      <td>4.970000e+02</td>
      <td>7.180000e+02</td>
      <td>1.727100e+04</td>
    </tr>
    <tr>
      <th>TractWhite</th>
      <td>72527.0</td>
      <td>3.082337e+03</td>
      <td>1.796365e+03</td>
      <td>0.000000e+00</td>
      <td>1.848000e+03</td>
      <td>2.914000e+03</td>
      <td>4.118000e+03</td>
      <td>2.898300e+04</td>
    </tr>
    <tr>
      <th>TractBlack</th>
      <td>72527.0</td>
      <td>5.367562e+02</td>
      <td>8.891181e+02</td>
      <td>0.000000e+00</td>
      <td>4.300000e+01</td>
      <td>1.600000e+02</td>
      <td>6.100000e+02</td>
      <td>1.680400e+04</td>
    </tr>
    <tr>
      <th>TractAsian</th>
      <td>72527.0</td>
      <td>2.023277e+02</td>
      <td>4.358783e+02</td>
      <td>0.000000e+00</td>
      <td>1.700000e+01</td>
      <td>5.800000e+01</td>
      <td>1.890000e+02</td>
      <td>1.048500e+04</td>
    </tr>
    <tr>
      <th>TractNHOPI</th>
      <td>72527.0</td>
      <td>7.445655e+00</td>
      <td>4.518658e+01</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e+00</td>
      <td>5.000000e+00</td>
      <td>3.491000e+03</td>
    </tr>
    <tr>
      <th>TractAIAN</th>
      <td>72527.0</td>
      <td>4.015232e+01</td>
      <td>1.773787e+02</td>
      <td>0.000000e+00</td>
      <td>7.000000e+00</td>
      <td>1.500000e+01</td>
      <td>3.300000e+01</td>
      <td>9.009000e+03</td>
    </tr>
    <tr>
      <th>TractOMultir</th>
      <td>72527.0</td>
      <td>3.876646e+02</td>
      <td>5.293497e+02</td>
      <td>0.000000e+00</td>
      <td>8.500000e+01</td>
      <td>1.860000e+02</td>
      <td>4.480000e+02</td>
      <td>8.839000e+03</td>
    </tr>
    <tr>
      <th>TractHispanic</th>
      <td>72527.0</td>
      <td>6.959793e+02</td>
      <td>1.119473e+03</td>
      <td>0.000000e+00</td>
      <td>8.800000e+01</td>
      <td>2.430000e+02</td>
      <td>7.510000e+02</td>
      <td>1.542000e+04</td>
    </tr>
    <tr>
      <th>TractHUNV</th>
      <td>72527.0</td>
      <td>1.437097e+02</td>
      <td>2.327389e+02</td>
      <td>0.000000e+00</td>
      <td>3.600000e+01</td>
      <td>8.200000e+01</td>
      <td>1.685000e+02</td>
      <td>6.059000e+03</td>
    </tr>
    <tr>
      <th>TractSNAP</th>
      <td>72527.0</td>
      <td>2.017532e+02</td>
      <td>1.857601e+02</td>
      <td>0.000000e+00</td>
      <td>6.700000e+01</td>
      <td>1.520000e+02</td>
      <td>2.820000e+02</td>
      <td>2.175000e+03</td>
    </tr>
  </tbody>
</table>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-97995fb2-9bc8-4387-bbf3-82bfd0c984b1')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  
    </button>

  

    
  </div>


<div id="df-c647d036-4462-489a-8fa9-24a0330df944">
  <button class="colab-df-quickchart" onclick="quickchart('df-c647d036-4462-489a-8fa9-24a0330df944')"
            title="Suggest charts"
            style="display:none;">


  </button>



  
</div>

    </div>
  </div>




**Observations of Descriptive Statistics**

**What are the minimum and maximum values?**

The minimum population is 1, and the maximum is 37,452.  
The minimum poverty rate is 0%, and the maximum is 100%.  
The minimum median family income is 2,499, while the maximum $250,001.  
The minimum Black population is 0, and the maximum is 16,804.



**Are the mean and median values close to each other? If so this could indicate a normal distribution of the data. If not, this could indicate skewness in the data.
If the mean is smaller than the median the values are likely skewed left, toward the minimum value. If the mean is larger than the median then there is skewness to the right indicating more high values in the data distribution.**
- The mean is higher than the median for all the columns, which means the data is skewed to the right. This suggests there are some higher values pulling the average up.








---

### Assignment 2

# **Do low-income, predominantly Black communities experience greater food access barriers than other racial groups?**

Supermarket access, economic conditions, and food assistance affect food availability across racial groups, highlighting inequalities in food security. Studying these factors can help address disparities and improve food access in underserved communities. The findings will highlight the disproportionate impact of food insecurity on Black communities and emphasize the need for policy interventions to address racial disparities in food access.




# **Problem Statement:**

Low-income, predominantly Black communities often experience significant barriers to accessing affordable and nutritious food. Many of these neighborhoods are classified as food deserts, where grocery stores are scarce, and fresh food options are limited. As a result, residents frequently rely on convenience stores and fast food, leading to higher rates of food insecurity and diet-related health issues.


# **Data Definition:**

The Food Access Research Atlas provides a geographic analysis of food accessibility in low-income and other census tracts using various measures of supermarket proximity. It includes data on food access for populations within these tracts and offers census-tract-level information that can be used for research or community planning.


https://catalog.data.gov/dataset/food-access-research-atlas



```python
# Import the libraries
import numpy as np                  # Scientific Computing
import pandas as pd                 # Data Analysis
import matplotlib.pyplot as plt     # Plotting
import seaborn as sns               # Statistical Data Visualization

# Let's make sure pandas returns all the rows and columns for the dataframe
pd.set_option('display.max_rows', None)
pd.set_option('display.max_columns', None)

# Force pandas to display full numbers instead of scientific notation
# pd.options.display.float_format = '{:.0f}'.format

# Library to suppress warnings
import warnings
warnings.filterwarnings('ignore')
```


```python
from google.colab import drive

# Mount Google Drive
drive.mount('/content/drive')

# Define the file path (adjust to your folder location)
file_path = "/content/drive/My Drive/Food_Access_Research_Atlas.csv"

# Read the Excel file
food_access = pd.read_csv(file_path)


```

    Mounted at /content/drive



```python
# Display the first seven rows of the dataframe
food_access.head(7)
```





  <div id="df-36ca0057-fdf9-4757-8e10-e259631fa7a8" class="colab-df-container">
    <div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CensusTract</th>
      <th>State</th>
      <th>County</th>
      <th>Urban</th>
      <th>Pop2010</th>
      <th>OHU2010</th>
      <th>GroupQuartersFlag</th>
      <th>NUMGQTRS</th>
      <th>PCTGQTRS</th>
      <th>LILATracts_1And10</th>
      <th>LILATracts_halfAnd10</th>
      <th>LILATracts_1And20</th>
      <th>LILATracts_Vehicle</th>
      <th>HUNVFlag</th>
      <th>LowIncomeTracts</th>
      <th>PovertyRate</th>
      <th>MedianFamilyIncome</th>
      <th>LA1and10</th>
      <th>LAhalfand10</th>
      <th>LA1and20</th>
      <th>LATracts_half</th>
      <th>LATracts1</th>
      <th>LATracts10</th>
      <th>LATracts20</th>
      <th>LATractsVehicle_20</th>
      <th>LAPOP1_10</th>
      <th>LAPOP05_10</th>
      <th>LAPOP1_20</th>
      <th>LALOWI1_10</th>
      <th>LALOWI05_10</th>
      <th>LALOWI1_20</th>
      <th>lapophalf</th>
      <th>lapophalfshare</th>
      <th>lalowihalf</th>
      <th>lalowihalfshare</th>
      <th>lakidshalf</th>
      <th>lakidshalfshare</th>
      <th>laseniorshalf</th>
      <th>laseniorshalfshare</th>
      <th>lawhitehalf</th>
      <th>lawhitehalfshare</th>
      <th>lablackhalf</th>
      <th>lablackhalfshare</th>
      <th>laasianhalf</th>
      <th>laasianhalfshare</th>
      <th>lanhopihalf</th>
      <th>lanhopihalfshare</th>
      <th>laaianhalf</th>
      <th>laaianhalfshare</th>
      <th>laomultirhalf</th>
      <th>laomultirhalfshare</th>
      <th>lahisphalf</th>
      <th>lahisphalfshare</th>
      <th>lahunvhalf</th>
      <th>lahunvhalfshare</th>
      <th>lasnaphalf</th>
      <th>lasnaphalfshare</th>
      <th>lapop1</th>
      <th>lapop1share</th>
      <th>lalowi1</th>
      <th>lalowi1share</th>
      <th>lakids1</th>
      <th>lakids1share</th>
      <th>laseniors1</th>
      <th>laseniors1share</th>
      <th>lawhite1</th>
      <th>lawhite1share</th>
      <th>lablack1</th>
      <th>lablack1share</th>
      <th>laasian1</th>
      <th>laasian1share</th>
      <th>lanhopi1</th>
      <th>lanhopi1share</th>
      <th>laaian1</th>
      <th>laaian1share</th>
      <th>laomultir1</th>
      <th>laomultir1share</th>
      <th>lahisp1</th>
      <th>lahisp1share</th>
      <th>lahunv1</th>
      <th>lahunv1share</th>
      <th>lasnap1</th>
      <th>lasnap1share</th>
      <th>lapop10</th>
      <th>lapop10share</th>
      <th>lalowi10</th>
      <th>lalowi10share</th>
      <th>lakids10</th>
      <th>lakids10share</th>
      <th>laseniors10</th>
      <th>laseniors10share</th>
      <th>lawhite10</th>
      <th>lawhite10share</th>
      <th>lablack10</th>
      <th>lablack10share</th>
      <th>laasian10</th>
      <th>laasian10share</th>
      <th>lanhopi10</th>
      <th>lanhopi10share</th>
      <th>laaian10</th>
      <th>laaian10share</th>
      <th>laomultir10</th>
      <th>laomultir10share</th>
      <th>lahisp10</th>
      <th>lahisp10share</th>
      <th>lahunv10</th>
      <th>lahunv10share</th>
      <th>lasnap10</th>
      <th>lasnap10share</th>
      <th>lapop20</th>
      <th>lapop20share</th>
      <th>lalowi20</th>
      <th>lalowi20share</th>
      <th>lakids20</th>
      <th>lakids20share</th>
      <th>laseniors20</th>
      <th>laseniors20share</th>
      <th>lawhite20</th>
      <th>lawhite20share</th>
      <th>lablack20</th>
      <th>lablack20share</th>
      <th>laasian20</th>
      <th>laasian20share</th>
      <th>lanhopi20</th>
      <th>lanhopi20share</th>
      <th>laaian20</th>
      <th>laaian20share</th>
      <th>laomultir20</th>
      <th>laomultir20share</th>
      <th>lahisp20</th>
      <th>lahisp20share</th>
      <th>lahunv20</th>
      <th>lahunv20share</th>
      <th>lasnap20</th>
      <th>lasnap20share</th>
      <th>TractLOWI</th>
      <th>TractKids</th>
      <th>TractSeniors</th>
      <th>TractWhite</th>
      <th>TractBlack</th>
      <th>TractAsian</th>
      <th>TractNHOPI</th>
      <th>TractAIAN</th>
      <th>TractOMultir</th>
      <th>TractHispanic</th>
      <th>TractHUNV</th>
      <th>TractSNAP</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1001020100</td>
      <td>Alabama</td>
      <td>Autauga County</td>
      <td>1</td>
      <td>1912</td>
      <td>693</td>
      <td>0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>11.3</td>
      <td>81250.0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1896.0</td>
      <td>1912.0</td>
      <td>1896.0</td>
      <td>461.0</td>
      <td>467.0</td>
      <td>461.0</td>
      <td>1912.0</td>
      <td>100.00</td>
      <td>467.0</td>
      <td>24.42</td>
      <td>507.0</td>
      <td>26.52</td>
      <td>221.0</td>
      <td>11.56</td>
      <td>1622.0</td>
      <td>84.83</td>
      <td>217.0</td>
      <td>11.35</td>
      <td>14.0</td>
      <td>0.73</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>14.0</td>
      <td>0.73</td>
      <td>45.0</td>
      <td>2.35</td>
      <td>44.0</td>
      <td>2.30</td>
      <td>5.0</td>
      <td>0.79</td>
      <td>92.0</td>
      <td>13.33</td>
      <td>1896.0</td>
      <td>99.19</td>
      <td>461.0</td>
      <td>24.11</td>
      <td>504.0</td>
      <td>26.33</td>
      <td>219.0</td>
      <td>11.44</td>
      <td>1611.0</td>
      <td>84.26</td>
      <td>214.0</td>
      <td>11.17</td>
      <td>14.0</td>
      <td>0.72</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>14.0</td>
      <td>0.73</td>
      <td>44.0</td>
      <td>2.31</td>
      <td>43.0</td>
      <td>2.27</td>
      <td>5.0</td>
      <td>0.79</td>
      <td>92.0</td>
      <td>13.22</td>
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
      <td>NaN</td>
      <td>NaN</td>
      <td>455.0</td>
      <td>507.0</td>
      <td>221.0</td>
      <td>1622.0</td>
      <td>217.0</td>
      <td>14.0</td>
      <td>0.0</td>
      <td>14.0</td>
      <td>45.0</td>
      <td>44.0</td>
      <td>6.0</td>
      <td>102.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1001020200</td>
      <td>Alabama</td>
      <td>Autauga County</td>
      <td>1</td>
      <td>2170</td>
      <td>743</td>
      <td>0</td>
      <td>181.0</td>
      <td>8.34</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>17.9</td>
      <td>49000.0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1261.0</td>
      <td>2170.0</td>
      <td>1261.0</td>
      <td>604.0</td>
      <td>962.0</td>
      <td>604.0</td>
      <td>2170.0</td>
      <td>100.00</td>
      <td>962.0</td>
      <td>44.34</td>
      <td>606.0</td>
      <td>27.93</td>
      <td>214.0</td>
      <td>9.86</td>
      <td>888.0</td>
      <td>40.92</td>
      <td>1217.0</td>
      <td>56.08</td>
      <td>5.0</td>
      <td>0.23</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>5.0</td>
      <td>0.23</td>
      <td>55.0</td>
      <td>2.53</td>
      <td>75.0</td>
      <td>3.46</td>
      <td>93.0</td>
      <td>12.47</td>
      <td>161.0</td>
      <td>21.70</td>
      <td>1261.0</td>
      <td>58.11</td>
      <td>604.0</td>
      <td>27.83</td>
      <td>406.0</td>
      <td>18.69</td>
      <td>127.0</td>
      <td>5.83</td>
      <td>357.0</td>
      <td>16.43</td>
      <td>854.0</td>
      <td>39.36</td>
      <td>4.0</td>
      <td>0.18</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>4.0</td>
      <td>0.20</td>
      <td>42.0</td>
      <td>1.93</td>
      <td>33.0</td>
      <td>1.52</td>
      <td>67.0</td>
      <td>9.00</td>
      <td>96.0</td>
      <td>12.95</td>
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
      <td>NaN</td>
      <td>NaN</td>
      <td>802.0</td>
      <td>606.0</td>
      <td>214.0</td>
      <td>888.0</td>
      <td>1217.0</td>
      <td>5.0</td>
      <td>0.0</td>
      <td>5.0</td>
      <td>55.0</td>
      <td>75.0</td>
      <td>89.0</td>
      <td>156.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1001020300</td>
      <td>Alabama</td>
      <td>Autauga County</td>
      <td>1</td>
      <td>3373</td>
      <td>1256</td>
      <td>0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>15.0</td>
      <td>62609.0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1552.0</td>
      <td>2857.0</td>
      <td>1552.0</td>
      <td>478.0</td>
      <td>971.0</td>
      <td>478.0</td>
      <td>2857.0</td>
      <td>84.70</td>
      <td>971.0</td>
      <td>28.79</td>
      <td>771.0</td>
      <td>22.86</td>
      <td>358.0</td>
      <td>10.60</td>
      <td>2177.0</td>
      <td>64.53</td>
      <td>554.0</td>
      <td>16.43</td>
      <td>10.0</td>
      <td>0.30</td>
      <td>1.0</td>
      <td>0.03</td>
      <td>10.0</td>
      <td>0.30</td>
      <td>105.0</td>
      <td>3.10</td>
      <td>78.0</td>
      <td>2.30</td>
      <td>39.0</td>
      <td>3.09</td>
      <td>139.0</td>
      <td>11.05</td>
      <td>1552.0</td>
      <td>46.00</td>
      <td>478.0</td>
      <td>14.18</td>
      <td>416.0</td>
      <td>12.34</td>
      <td>201.0</td>
      <td>5.96</td>
      <td>1242.0</td>
      <td>36.81</td>
      <td>255.0</td>
      <td>7.56</td>
      <td>8.0</td>
      <td>0.24</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>2.0</td>
      <td>0.06</td>
      <td>45.0</td>
      <td>1.33</td>
      <td>36.0</td>
      <td>1.08</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>74.0</td>
      <td>5.87</td>
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
      <td>NaN</td>
      <td>NaN</td>
      <td>1306.0</td>
      <td>894.0</td>
      <td>439.0</td>
      <td>2576.0</td>
      <td>647.0</td>
      <td>17.0</td>
      <td>5.0</td>
      <td>11.0</td>
      <td>117.0</td>
      <td>87.0</td>
      <td>99.0</td>
      <td>172.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1001020400</td>
      <td>Alabama</td>
      <td>Autauga County</td>
      <td>1</td>
      <td>4386</td>
      <td>1722</td>
      <td>0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>2.8</td>
      <td>70607.0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1363.0</td>
      <td>3651.0</td>
      <td>1363.0</td>
      <td>343.0</td>
      <td>893.0</td>
      <td>343.0</td>
      <td>3651.0</td>
      <td>83.24</td>
      <td>893.0</td>
      <td>20.36</td>
      <td>847.0</td>
      <td>19.30</td>
      <td>767.0</td>
      <td>17.48</td>
      <td>3395.0</td>
      <td>77.41</td>
      <td>170.0</td>
      <td>3.88</td>
      <td>15.0</td>
      <td>0.34</td>
      <td>3.0</td>
      <td>0.06</td>
      <td>8.0</td>
      <td>0.18</td>
      <td>60.0</td>
      <td>1.38</td>
      <td>61.0</td>
      <td>1.40</td>
      <td>19.0</td>
      <td>1.13</td>
      <td>84.0</td>
      <td>4.88</td>
      <td>1363.0</td>
      <td>31.09</td>
      <td>343.0</td>
      <td>7.83</td>
      <td>346.0</td>
      <td>7.89</td>
      <td>237.0</td>
      <td>5.39</td>
      <td>1233.0</td>
      <td>28.12</td>
      <td>81.0</td>
      <td>1.85</td>
      <td>7.0</td>
      <td>0.16</td>
      <td>2.0</td>
      <td>0.05</td>
      <td>4.0</td>
      <td>0.08</td>
      <td>37.0</td>
      <td>0.84</td>
      <td>30.0</td>
      <td>0.68</td>
      <td>8.0</td>
      <td>0.46</td>
      <td>30.0</td>
      <td>1.76</td>
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
      <td>NaN</td>
      <td>NaN</td>
      <td>922.0</td>
      <td>1015.0</td>
      <td>904.0</td>
      <td>4086.0</td>
      <td>193.0</td>
      <td>18.0</td>
      <td>4.0</td>
      <td>11.0</td>
      <td>74.0</td>
      <td>85.0</td>
      <td>21.0</td>
      <td>98.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1001020500</td>
      <td>Alabama</td>
      <td>Autauga County</td>
      <td>1</td>
      <td>10766</td>
      <td>4082</td>
      <td>0</td>
      <td>181.0</td>
      <td>1.68</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>15.2</td>
      <td>96334.0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>2643.0</td>
      <td>7778.0</td>
      <td>2643.0</td>
      <td>586.0</td>
      <td>1719.0</td>
      <td>586.0</td>
      <td>7778.0</td>
      <td>72.25</td>
      <td>1719.0</td>
      <td>15.97</td>
      <td>2309.0</td>
      <td>21.45</td>
      <td>840.0</td>
      <td>7.80</td>
      <td>6299.0</td>
      <td>58.51</td>
      <td>1001.0</td>
      <td>9.29</td>
      <td>209.0</td>
      <td>1.94</td>
      <td>5.0</td>
      <td>0.05</td>
      <td>38.0</td>
      <td>0.35</td>
      <td>227.0</td>
      <td>2.11</td>
      <td>277.0</td>
      <td>2.57</td>
      <td>164.0</td>
      <td>4.01</td>
      <td>235.0</td>
      <td>5.76</td>
      <td>2643.0</td>
      <td>24.55</td>
      <td>586.0</td>
      <td>5.45</td>
      <td>715.0</td>
      <td>6.64</td>
      <td>362.0</td>
      <td>3.36</td>
      <td>2168.0</td>
      <td>20.14</td>
      <td>343.0</td>
      <td>3.19</td>
      <td>47.0</td>
      <td>0.44</td>
      <td>1.0</td>
      <td>0.01</td>
      <td>14.0</td>
      <td>0.13</td>
      <td>70.0</td>
      <td>0.65</td>
      <td>86.0</td>
      <td>0.80</td>
      <td>55.0</td>
      <td>1.35</td>
      <td>83.0</td>
      <td>2.04</td>
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
      <td>NaN</td>
      <td>NaN</td>
      <td>2242.0</td>
      <td>3162.0</td>
      <td>1126.0</td>
      <td>8666.0</td>
      <td>1437.0</td>
      <td>296.0</td>
      <td>9.0</td>
      <td>48.0</td>
      <td>310.0</td>
      <td>355.0</td>
      <td>230.0</td>
      <td>339.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1001020600</td>
      <td>Alabama</td>
      <td>Autauga County</td>
      <td>1</td>
      <td>3668</td>
      <td>1311</td>
      <td>0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>21.6</td>
      <td>69521.0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>3438.0</td>
      <td>3668.0</td>
      <td>3438.0</td>
      <td>1585.0</td>
      <td>1674.0</td>
      <td>1585.0</td>
      <td>3668.0</td>
      <td>100.00</td>
      <td>1674.0</td>
      <td>45.63</td>
      <td>1008.0</td>
      <td>27.48</td>
      <td>411.0</td>
      <td>11.21</td>
      <td>2751.0</td>
      <td>75.00</td>
      <td>740.0</td>
      <td>20.17</td>
      <td>9.0</td>
      <td>0.25</td>
      <td>1.0</td>
      <td>0.03</td>
      <td>10.0</td>
      <td>0.27</td>
      <td>157.0</td>
      <td>4.28</td>
      <td>176.0</td>
      <td>4.80</td>
      <td>73.0</td>
      <td>5.54</td>
      <td>220.0</td>
      <td>16.82</td>
      <td>3438.0</td>
      <td>93.72</td>
      <td>1585.0</td>
      <td>43.21</td>
      <td>955.0</td>
      <td>26.03</td>
      <td>375.0</td>
      <td>10.22</td>
      <td>2539.0</td>
      <td>69.22</td>
      <td>726.0</td>
      <td>19.80</td>
      <td>9.0</td>
      <td>0.25</td>
      <td>1.0</td>
      <td>0.03</td>
      <td>9.0</td>
      <td>0.26</td>
      <td>153.0</td>
      <td>4.16</td>
      <td>168.0</td>
      <td>4.59</td>
      <td>72.0</td>
      <td>5.47</td>
      <td>206.0</td>
      <td>15.70</td>
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
      <td>NaN</td>
      <td>NaN</td>
      <td>1659.0</td>
      <td>1008.0</td>
      <td>411.0</td>
      <td>2751.0</td>
      <td>740.0</td>
      <td>9.0</td>
      <td>1.0</td>
      <td>10.0</td>
      <td>157.0</td>
      <td>176.0</td>
      <td>71.0</td>
      <td>224.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1001020700</td>
      <td>Alabama</td>
      <td>Autauga County</td>
      <td>1</td>
      <td>2891</td>
      <td>1188</td>
      <td>0</td>
      <td>36.0</td>
      <td>1.25</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>30.5</td>
      <td>39875.0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1231.0</td>
      <td>2287.0</td>
      <td>1231.0</td>
      <td>742.0</td>
      <td>1307.0</td>
      <td>742.0</td>
      <td>2287.0</td>
      <td>79.12</td>
      <td>1307.0</td>
      <td>45.19</td>
      <td>557.0</td>
      <td>19.25</td>
      <td>277.0</td>
      <td>9.57</td>
      <td>1849.0</td>
      <td>63.97</td>
      <td>337.0</td>
      <td>11.67</td>
      <td>10.0</td>
      <td>0.35</td>
      <td>3.0</td>
      <td>0.10</td>
      <td>9.0</td>
      <td>0.30</td>
      <td>79.0</td>
      <td>2.73</td>
      <td>82.0</td>
      <td>2.84</td>
      <td>23.0</td>
      <td>1.91</td>
      <td>263.0</td>
      <td>22.12</td>
      <td>1231.0</td>
      <td>42.58</td>
      <td>742.0</td>
      <td>25.67</td>
      <td>298.0</td>
      <td>10.31</td>
      <td>109.0</td>
      <td>3.78</td>
      <td>1005.0</td>
      <td>34.77</td>
      <td>158.0</td>
      <td>5.47</td>
      <td>4.0</td>
      <td>0.13</td>
      <td>2.0</td>
      <td>0.08</td>
      <td>4.0</td>
      <td>0.14</td>
      <td>58.0</td>
      <td>2.00</td>
      <td>56.0</td>
      <td>1.93</td>
      <td>12.0</td>
      <td>1.01</td>
      <td>140.0</td>
      <td>11.82</td>
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
      <td>NaN</td>
      <td>NaN</td>
      <td>2175.0</td>
      <td>686.0</td>
      <td>360.0</td>
      <td>2333.0</td>
      <td>435.0</td>
      <td>13.0</td>
      <td>3.0</td>
      <td>11.0</td>
      <td>96.0</td>
      <td>98.0</td>
      <td>34.0</td>
      <td>390.0</td>
    </tr>
  </tbody>
</table>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-36ca0057-fdf9-4757-8e10-e259631fa7a8')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  
    </button>

  

    
  </div>


<div id="df-c85a63fd-f66c-4146-b261-a5a0494cb20c">
  <button class="colab-df-quickchart" onclick="quickchart('df-c85a63fd-f66c-4146-b261-a5a0494cb20c')"
            title="Suggest charts"
            style="display:none;">


  </button>



  
</div>

    </div>
  </div>





```python
# Display the bottom seven rows of the dataframe
food_access.tail(7)

```





  <div id="df-9a594906-83fb-43b4-a9d7-67c7cf4cb8e3" class="colab-df-container">
    <div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CensusTract</th>
      <th>State</th>
      <th>County</th>
      <th>Urban</th>
      <th>Pop2010</th>
      <th>OHU2010</th>
      <th>GroupQuartersFlag</th>
      <th>NUMGQTRS</th>
      <th>PCTGQTRS</th>
      <th>LILATracts_1And10</th>
      <th>LILATracts_halfAnd10</th>
      <th>LILATracts_1And20</th>
      <th>LILATracts_Vehicle</th>
      <th>HUNVFlag</th>
      <th>LowIncomeTracts</th>
      <th>PovertyRate</th>
      <th>MedianFamilyIncome</th>
      <th>LA1and10</th>
      <th>LAhalfand10</th>
      <th>LA1and20</th>
      <th>LATracts_half</th>
      <th>LATracts1</th>
      <th>LATracts10</th>
      <th>LATracts20</th>
      <th>LATractsVehicle_20</th>
      <th>LAPOP1_10</th>
      <th>LAPOP05_10</th>
      <th>LAPOP1_20</th>
      <th>LALOWI1_10</th>
      <th>LALOWI05_10</th>
      <th>LALOWI1_20</th>
      <th>lapophalf</th>
      <th>lapophalfshare</th>
      <th>lalowihalf</th>
      <th>lalowihalfshare</th>
      <th>lakidshalf</th>
      <th>lakidshalfshare</th>
      <th>laseniorshalf</th>
      <th>laseniorshalfshare</th>
      <th>lawhitehalf</th>
      <th>lawhitehalfshare</th>
      <th>lablackhalf</th>
      <th>lablackhalfshare</th>
      <th>laasianhalf</th>
      <th>laasianhalfshare</th>
      <th>lanhopihalf</th>
      <th>lanhopihalfshare</th>
      <th>laaianhalf</th>
      <th>laaianhalfshare</th>
      <th>laomultirhalf</th>
      <th>laomultirhalfshare</th>
      <th>lahisphalf</th>
      <th>lahisphalfshare</th>
      <th>lahunvhalf</th>
      <th>lahunvhalfshare</th>
      <th>lasnaphalf</th>
      <th>lasnaphalfshare</th>
      <th>lapop1</th>
      <th>lapop1share</th>
      <th>lalowi1</th>
      <th>lalowi1share</th>
      <th>lakids1</th>
      <th>lakids1share</th>
      <th>laseniors1</th>
      <th>laseniors1share</th>
      <th>lawhite1</th>
      <th>lawhite1share</th>
      <th>lablack1</th>
      <th>lablack1share</th>
      <th>laasian1</th>
      <th>laasian1share</th>
      <th>lanhopi1</th>
      <th>lanhopi1share</th>
      <th>laaian1</th>
      <th>laaian1share</th>
      <th>laomultir1</th>
      <th>laomultir1share</th>
      <th>lahisp1</th>
      <th>lahisp1share</th>
      <th>lahunv1</th>
      <th>lahunv1share</th>
      <th>lasnap1</th>
      <th>lasnap1share</th>
      <th>lapop10</th>
      <th>lapop10share</th>
      <th>lalowi10</th>
      <th>lalowi10share</th>
      <th>lakids10</th>
      <th>lakids10share</th>
      <th>laseniors10</th>
      <th>laseniors10share</th>
      <th>lawhite10</th>
      <th>lawhite10share</th>
      <th>lablack10</th>
      <th>lablack10share</th>
      <th>laasian10</th>
      <th>laasian10share</th>
      <th>lanhopi10</th>
      <th>lanhopi10share</th>
      <th>laaian10</th>
      <th>laaian10share</th>
      <th>laomultir10</th>
      <th>laomultir10share</th>
      <th>lahisp10</th>
      <th>lahisp10share</th>
      <th>lahunv10</th>
      <th>lahunv10share</th>
      <th>lasnap10</th>
      <th>lasnap10share</th>
      <th>lapop20</th>
      <th>lapop20share</th>
      <th>lalowi20</th>
      <th>lalowi20share</th>
      <th>lakids20</th>
      <th>lakids20share</th>
      <th>laseniors20</th>
      <th>laseniors20share</th>
      <th>lawhite20</th>
      <th>lawhite20share</th>
      <th>lablack20</th>
      <th>lablack20share</th>
      <th>laasian20</th>
      <th>laasian20share</th>
      <th>lanhopi20</th>
      <th>lanhopi20share</th>
      <th>laaian20</th>
      <th>laaian20share</th>
      <th>laomultir20</th>
      <th>laomultir20share</th>
      <th>lahisp20</th>
      <th>lahisp20share</th>
      <th>lahunv20</th>
      <th>lahunv20share</th>
      <th>lasnap20</th>
      <th>lasnap20share</th>
      <th>TractLOWI</th>
      <th>TractKids</th>
      <th>TractSeniors</th>
      <th>TractWhite</th>
      <th>TractBlack</th>
      <th>TractAsian</th>
      <th>TractNHOPI</th>
      <th>TractAIAN</th>
      <th>TractOMultir</th>
      <th>TractHispanic</th>
      <th>TractHUNV</th>
      <th>TractSNAP</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>72524</th>
      <td>56041975300</td>
      <td>Wyoming</td>
      <td>Uinta County</td>
      <td>0</td>
      <td>7761</td>
      <td>2696</td>
      <td>0</td>
      <td>205.0</td>
      <td>2.64</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>13.6</td>
      <td>62445.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>479.0</td>
      <td>479.0</td>
      <td>5.0</td>
      <td>264.0</td>
      <td>264.0</td>
      <td>3.0</td>
      <td>6037.0</td>
      <td>77.78</td>
      <td>2302.0</td>
      <td>29.66</td>
      <td>1882.0</td>
      <td>24.25</td>
      <td>455.0</td>
      <td>5.86</td>
      <td>5509.0</td>
      <td>70.99</td>
      <td>13.0</td>
      <td>0.17</td>
      <td>24.0</td>
      <td>0.31</td>
      <td>20.0</td>
      <td>0.26</td>
      <td>34.0</td>
      <td>0.43</td>
      <td>436.0</td>
      <td>5.62</td>
      <td>613.0</td>
      <td>7.90</td>
      <td>96.0</td>
      <td>3.57</td>
      <td>194.0</td>
      <td>7.19</td>
      <td>3934.0</td>
      <td>50.69</td>
      <td>1772.0</td>
      <td>22.84</td>
      <td>1197.0</td>
      <td>15.43</td>
      <td>339.0</td>
      <td>4.36</td>
      <td>3583.0</td>
      <td>46.17</td>
      <td>10.0</td>
      <td>0.13</td>
      <td>14.0</td>
      <td>0.18</td>
      <td>9.0</td>
      <td>0.11</td>
      <td>17.0</td>
      <td>0.22</td>
      <td>301.0</td>
      <td>3.88</td>
      <td>435.0</td>
      <td>5.61</td>
      <td>51.0</td>
      <td>1.90</td>
      <td>127.0</td>
      <td>4.70</td>
      <td>479.0</td>
      <td>6.17</td>
      <td>264.0</td>
      <td>3.40</td>
      <td>118.0</td>
      <td>1.52</td>
      <td>73.0</td>
      <td>0.95</td>
      <td>466.0</td>
      <td>6.00</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>1.0</td>
      <td>0.01</td>
      <td>2.0</td>
      <td>0.03</td>
      <td>1.0</td>
      <td>0.01</td>
      <td>9.0</td>
      <td>0.11</td>
      <td>13.0</td>
      <td>0.17</td>
      <td>5.0</td>
      <td>0.17</td>
      <td>16.0</td>
      <td>0.61</td>
      <td>5.0</td>
      <td>0.06</td>
      <td>3.0</td>
      <td>0.04</td>
      <td>1.0</td>
      <td>0.02</td>
      <td>1.0</td>
      <td>0.02</td>
      <td>5.0</td>
      <td>0.06</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.01</td>
      <td>2965.0</td>
      <td>2387.0</td>
      <td>569.0</td>
      <td>7052.0</td>
      <td>21.0</td>
      <td>29.0</td>
      <td>23.0</td>
      <td>64.0</td>
      <td>572.0</td>
      <td>797.0</td>
      <td>107.0</td>
      <td>255.0</td>
    </tr>
    <tr>
      <th>72525</th>
      <td>56041975400</td>
      <td>Wyoming</td>
      <td>Uinta County</td>
      <td>0</td>
      <td>6852</td>
      <td>2632</td>
      <td>0</td>
      <td>65.0</td>
      <td>0.95</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>17.3</td>
      <td>57248.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>120.0</td>
      <td>120.0</td>
      <td>NaN</td>
      <td>24.0</td>
      <td>24.0</td>
      <td>NaN</td>
      <td>5809.0</td>
      <td>84.78</td>
      <td>2151.0</td>
      <td>31.39</td>
      <td>1632.0</td>
      <td>23.83</td>
      <td>575.0</td>
      <td>8.39</td>
      <td>5221.0</td>
      <td>76.19</td>
      <td>15.0</td>
      <td>0.22</td>
      <td>13.0</td>
      <td>0.19</td>
      <td>1.0</td>
      <td>0.01</td>
      <td>60.0</td>
      <td>0.87</td>
      <td>500.0</td>
      <td>7.29</td>
      <td>751.0</td>
      <td>10.96</td>
      <td>108.0</td>
      <td>4.12</td>
      <td>180.0</td>
      <td>6.83</td>
      <td>3112.0</td>
      <td>45.42</td>
      <td>1107.0</td>
      <td>16.16</td>
      <td>909.0</td>
      <td>13.26</td>
      <td>255.0</td>
      <td>3.72</td>
      <td>2852.0</td>
      <td>41.62</td>
      <td>7.0</td>
      <td>0.10</td>
      <td>9.0</td>
      <td>0.13</td>
      <td>0.0</td>
      <td>0.01</td>
      <td>33.0</td>
      <td>0.48</td>
      <td>211.0</td>
      <td>3.08</td>
      <td>328.0</td>
      <td>4.79</td>
      <td>49.0</td>
      <td>1.87</td>
      <td>89.0</td>
      <td>3.39</td>
      <td>120.0</td>
      <td>1.76</td>
      <td>24.0</td>
      <td>0.35</td>
      <td>46.0</td>
      <td>0.67</td>
      <td>10.0</td>
      <td>0.15</td>
      <td>114.0</td>
      <td>1.66</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>1.0</td>
      <td>0.01</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>3.0</td>
      <td>0.05</td>
      <td>3.0</td>
      <td>0.04</td>
      <td>1.0</td>
      <td>0.01</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>3.0</td>
      <td>0.12</td>
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
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2273.0</td>
      <td>1921.0</td>
      <td>709.0</td>
      <td>6160.0</td>
      <td>20.0</td>
      <td>19.0</td>
      <td>2.0</td>
      <td>67.0</td>
      <td>584.0</td>
      <td>871.0</td>
      <td>124.0</td>
      <td>217.0</td>
    </tr>
    <tr>
      <th>72526</th>
      <td>56043000200</td>
      <td>Wyoming</td>
      <td>Washakie County</td>
      <td>0</td>
      <td>3326</td>
      <td>1317</td>
      <td>0</td>
      <td>57.0</td>
      <td>1.71</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>9.7</td>
      <td>67254.0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>902.0</td>
      <td>902.0</td>
      <td>730.0</td>
      <td>218.0</td>
      <td>218.0</td>
      <td>176.0</td>
      <td>3326.0</td>
      <td>99.99</td>
      <td>843.0</td>
      <td>25.36</td>
      <td>884.0</td>
      <td>26.58</td>
      <td>593.0</td>
      <td>17.83</td>
      <td>3106.0</td>
      <td>93.38</td>
      <td>6.0</td>
      <td>0.18</td>
      <td>15.0</td>
      <td>0.45</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>27.0</td>
      <td>0.81</td>
      <td>172.0</td>
      <td>5.17</td>
      <td>309.0</td>
      <td>9.29</td>
      <td>67.0</td>
      <td>5.06</td>
      <td>64.0</td>
      <td>4.83</td>
      <td>2714.0</td>
      <td>81.60</td>
      <td>675.0</td>
      <td>20.29</td>
      <td>716.0</td>
      <td>21.52</td>
      <td>472.0</td>
      <td>14.18</td>
      <td>2550.0</td>
      <td>76.67</td>
      <td>6.0</td>
      <td>0.18</td>
      <td>14.0</td>
      <td>0.42</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>21.0</td>
      <td>0.62</td>
      <td>123.0</td>
      <td>3.70</td>
      <td>221.0</td>
      <td>6.64</td>
      <td>34.0</td>
      <td>2.56</td>
      <td>50.0</td>
      <td>3.82</td>
      <td>902.0</td>
      <td>27.12</td>
      <td>218.0</td>
      <td>6.56</td>
      <td>177.0</td>
      <td>5.33</td>
      <td>218.0</td>
      <td>6.56</td>
      <td>857.0</td>
      <td>25.75</td>
      <td>2.0</td>
      <td>0.06</td>
      <td>6.0</td>
      <td>0.19</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>5.0</td>
      <td>0.15</td>
      <td>32.0</td>
      <td>0.96</td>
      <td>35.0</td>
      <td>1.05</td>
      <td>7.0</td>
      <td>0.51</td>
      <td>19.0</td>
      <td>1.47</td>
      <td>730.0</td>
      <td>21.95</td>
      <td>176.0</td>
      <td>5.30</td>
      <td>144.0</td>
      <td>4.33</td>
      <td>191.0</td>
      <td>5.74</td>
      <td>695.0</td>
      <td>20.90</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.03</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>4.0</td>
      <td>0.12</td>
      <td>30.0</td>
      <td>0.90</td>
      <td>24.0</td>
      <td>0.72</td>
      <td>6.0</td>
      <td>0.0</td>
      <td>16.0</td>
      <td>1.23</td>
      <td>765.0</td>
      <td>884.0</td>
      <td>593.0</td>
      <td>3106.0</td>
      <td>6.0</td>
      <td>15.0</td>
      <td>0.0</td>
      <td>27.0</td>
      <td>172.0</td>
      <td>309.0</td>
      <td>61.0</td>
      <td>64.0</td>
    </tr>
    <tr>
      <th>72527</th>
      <td>56043000301</td>
      <td>Wyoming</td>
      <td>Washakie County</td>
      <td>1</td>
      <td>2665</td>
      <td>1154</td>
      <td>0</td>
      <td>10.0</td>
      <td>0.38</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>11.6</td>
      <td>64152.0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>743.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>279.0</td>
      <td>NaN</td>
      <td>743.0</td>
      <td>27.89</td>
      <td>279.0</td>
      <td>10.49</td>
      <td>187.0</td>
      <td>7.03</td>
      <td>122.0</td>
      <td>4.57</td>
      <td>638.0</td>
      <td>23.95</td>
      <td>2.0</td>
      <td>0.09</td>
      <td>14.0</td>
      <td>0.54</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>19.0</td>
      <td>0.69</td>
      <td>70.0</td>
      <td>2.62</td>
      <td>135.0</td>
      <td>5.05</td>
      <td>27.0</td>
      <td>2.30</td>
      <td>12.0</td>
      <td>1.02</td>
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
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>774.0</td>
      <td>674.0</td>
      <td>399.0</td>
      <td>2377.0</td>
      <td>5.0</td>
      <td>23.0</td>
      <td>0.0</td>
      <td>40.0</td>
      <td>220.0</td>
      <td>446.0</td>
      <td>88.0</td>
      <td>41.0</td>
    </tr>
    <tr>
      <th>72528</th>
      <td>56043000302</td>
      <td>Wyoming</td>
      <td>Washakie County</td>
      <td>1</td>
      <td>2542</td>
      <td>1021</td>
      <td>0</td>
      <td>73.0</td>
      <td>2.87</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>16.3</td>
      <td>69605.0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>155.0</td>
      <td>892.0</td>
      <td>155.0</td>
      <td>44.0</td>
      <td>261.0</td>
      <td>44.0</td>
      <td>892.0</td>
      <td>35.10</td>
      <td>261.0</td>
      <td>10.25</td>
      <td>215.0</td>
      <td>8.45</td>
      <td>173.0</td>
      <td>6.80</td>
      <td>806.0</td>
      <td>31.71</td>
      <td>7.0</td>
      <td>0.26</td>
      <td>0.0</td>
      <td>0.02</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>4.0</td>
      <td>0.15</td>
      <td>75.0</td>
      <td>2.96</td>
      <td>147.0</td>
      <td>5.78</td>
      <td>12.0</td>
      <td>1.18</td>
      <td>24.0</td>
      <td>2.31</td>
      <td>155.0</td>
      <td>6.11</td>
      <td>44.0</td>
      <td>1.72</td>
      <td>30.0</td>
      <td>1.17</td>
      <td>34.0</td>
      <td>1.32</td>
      <td>145.0</td>
      <td>5.70</td>
      <td>2.0</td>
      <td>0.09</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.01</td>
      <td>8.0</td>
      <td>0.30</td>
      <td>12.0</td>
      <td>0.46</td>
      <td>3.0</td>
      <td>0.26</td>
      <td>5.0</td>
      <td>0.45</td>
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
      <td>NaN</td>
      <td>NaN</td>
      <td>789.0</td>
      <td>614.0</td>
      <td>516.0</td>
      <td>2312.0</td>
      <td>11.0</td>
      <td>10.0</td>
      <td>1.0</td>
      <td>26.0</td>
      <td>182.0</td>
      <td>407.0</td>
      <td>23.0</td>
      <td>64.0</td>
    </tr>
    <tr>
      <th>72529</th>
      <td>56045951100</td>
      <td>Wyoming</td>
      <td>Weston County</td>
      <td>0</td>
      <td>3314</td>
      <td>1322</td>
      <td>0</td>
      <td>252.0</td>
      <td>7.60</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>17.5</td>
      <td>74500.0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>840.0</td>
      <td>840.0</td>
      <td>188.0</td>
      <td>247.0</td>
      <td>247.0</td>
      <td>55.0</td>
      <td>2709.0</td>
      <td>81.74</td>
      <td>837.0</td>
      <td>25.26</td>
      <td>491.0</td>
      <td>14.80</td>
      <td>403.0</td>
      <td>12.15</td>
      <td>2609.0</td>
      <td>78.73</td>
      <td>14.0</td>
      <td>0.42</td>
      <td>7.0</td>
      <td>0.22</td>
      <td>1.0</td>
      <td>0.03</td>
      <td>31.0</td>
      <td>0.93</td>
      <td>47.0</td>
      <td>1.41</td>
      <td>77.0</td>
      <td>2.32</td>
      <td>26.0</td>
      <td>1.98</td>
      <td>26.0</td>
      <td>1.93</td>
      <td>2283.0</td>
      <td>68.87</td>
      <td>687.0</td>
      <td>20.73</td>
      <td>394.0</td>
      <td>11.90</td>
      <td>321.0</td>
      <td>9.69</td>
      <td>2193.0</td>
      <td>66.19</td>
      <td>13.0</td>
      <td>0.39</td>
      <td>5.0</td>
      <td>0.16</td>
      <td>1.0</td>
      <td>0.03</td>
      <td>29.0</td>
      <td>0.88</td>
      <td>41.0</td>
      <td>1.23</td>
      <td>67.0</td>
      <td>2.01</td>
      <td>13.0</td>
      <td>1.00</td>
      <td>21.0</td>
      <td>1.59</td>
      <td>840.0</td>
      <td>25.34</td>
      <td>247.0</td>
      <td>7.45</td>
      <td>143.0</td>
      <td>4.33</td>
      <td>154.0</td>
      <td>4.64</td>
      <td>818.0</td>
      <td>24.68</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>2.0</td>
      <td>0.06</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>6.0</td>
      <td>0.18</td>
      <td>14.0</td>
      <td>0.42</td>
      <td>14.0</td>
      <td>0.42</td>
      <td>2.0</td>
      <td>0.19</td>
      <td>9.0</td>
      <td>0.70</td>
      <td>188.0</td>
      <td>5.68</td>
      <td>55.0</td>
      <td>1.66</td>
      <td>40.0</td>
      <td>1.22</td>
      <td>44.0</td>
      <td>1.32</td>
      <td>182.0</td>
      <td>5.50</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>6.0</td>
      <td>0.18</td>
      <td>10.0</td>
      <td>0.30</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>2.0</td>
      <td>0.14</td>
      <td>955.0</td>
      <td>655.0</td>
      <td>499.0</td>
      <td>3179.0</td>
      <td>15.0</td>
      <td>10.0</td>
      <td>1.0</td>
      <td>47.0</td>
      <td>62.0</td>
      <td>91.0</td>
      <td>47.0</td>
      <td>34.0</td>
    </tr>
    <tr>
      <th>72530</th>
      <td>56045951300</td>
      <td>Wyoming</td>
      <td>Weston County</td>
      <td>1</td>
      <td>3894</td>
      <td>1699</td>
      <td>0</td>
      <td>61.0</td>
      <td>1.57</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>17.3</td>
      <td>76838.0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1376.0</td>
      <td>2528.0</td>
      <td>1376.0</td>
      <td>384.0</td>
      <td>671.0</td>
      <td>384.0</td>
      <td>2528.0</td>
      <td>64.93</td>
      <td>671.0</td>
      <td>17.24</td>
      <td>620.0</td>
      <td>15.93</td>
      <td>421.0</td>
      <td>10.80</td>
      <td>2400.0</td>
      <td>61.63</td>
      <td>3.0</td>
      <td>0.09</td>
      <td>6.0</td>
      <td>0.15</td>
      <td>2.0</td>
      <td>0.05</td>
      <td>24.0</td>
      <td>0.63</td>
      <td>93.0</td>
      <td>2.38</td>
      <td>96.0</td>
      <td>2.47</td>
      <td>17.0</td>
      <td>1.01</td>
      <td>71.0</td>
      <td>4.18</td>
      <td>1376.0</td>
      <td>35.34</td>
      <td>384.0</td>
      <td>9.85</td>
      <td>341.0</td>
      <td>8.76</td>
      <td>197.0</td>
      <td>5.05</td>
      <td>1290.0</td>
      <td>33.12</td>
      <td>2.0</td>
      <td>0.05</td>
      <td>6.0</td>
      <td>0.15</td>
      <td>2.0</td>
      <td>0.05</td>
      <td>16.0</td>
      <td>0.40</td>
      <td>61.0</td>
      <td>1.57</td>
      <td>69.0</td>
      <td>1.78</td>
      <td>9.0</td>
      <td>0.52</td>
      <td>37.0</td>
      <td>2.20</td>
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
      <td>NaN</td>
      <td>NaN</td>
      <td>1095.0</td>
      <td>918.0</td>
      <td>650.0</td>
      <td>3706.0</td>
      <td>6.0</td>
      <td>10.0</td>
      <td>2.0</td>
      <td>44.0</td>
      <td>126.0</td>
      <td>125.0</td>
      <td>34.0</td>
      <td>110.0</td>
    </tr>
  </tbody>
</table>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-9a594906-83fb-43b4-a9d7-67c7cf4cb8e3')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  
    </button>

  

    
  </div>


<div id="df-2764a2f9-57ea-47c9-8954-5d60826447d5">
  <button class="colab-df-quickchart" onclick="quickchart('df-2764a2f9-57ea-47c9-8954-5d60826447d5')"
            title="Suggest charts"
            style="display:none;">


  </button>



  
</div>

    </div>
  </div>





```python
food_access.shape

```




    (72531, 147)




```python
72531 * 147
```




    10662057



State the shape of the dataframe :

How many rows does the dataframe have?

- 72531 rows

How many columns does the dataframe have?

- 147 columns

What is the total number of datapoints expected in the dataset (rows x columns)?

- 10662057 total datapoints


```python
food_access.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 72531 entries, 0 to 72530
    Columns: 147 entries, CensusTract to TractSNAP
    dtypes: float64(126), int64(19), object(2)
    memory usage: 81.3+ MB



```python
food_access.info(show_counts=True, verbose=True)
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 72531 entries, 0 to 72530
    Data columns (total 147 columns):
     #    Column                Non-Null Count  Dtype  
    ---   ------                --------------  -----  
     0    CensusTract           72531 non-null  int64  
     1    State                 72531 non-null  object 
     2    County                72531 non-null  object 
     3    Urban                 72531 non-null  int64  
     4    Pop2010               72531 non-null  int64  
     5    OHU2010               72531 non-null  int64  
     6    GroupQuartersFlag     72531 non-null  int64  
     7    NUMGQTRS              72506 non-null  float64
     8    PCTGQTRS              72506 non-null  float64
     9    LILATracts_1And10     72531 non-null  int64  
     10   LILATracts_halfAnd10  72531 non-null  int64  
     11   LILATracts_1And20     72531 non-null  int64  
     12   LILATracts_Vehicle    72531 non-null  int64  
     13   HUNVFlag              72531 non-null  int64  
     14   LowIncomeTracts       72531 non-null  int64  
     15   PovertyRate           72528 non-null  float64
     16   MedianFamilyIncome    71783 non-null  float64
     17   LA1and10              72531 non-null  int64  
     18   LAhalfand10           72531 non-null  int64  
     19   LA1and20              72531 non-null  int64  
     20   LATracts_half         72531 non-null  int64  
     21   LATracts1             72531 non-null  int64  
     22   LATracts10            72531 non-null  int64  
     23   LATracts20            72531 non-null  int64  
     24   LATractsVehicle_20    72531 non-null  int64  
     25   LAPOP1_10             42574 non-null  float64
     26   LAPOP05_10            57991 non-null  float64
     27   LAPOP1_20             36617 non-null  float64
     28   LALOWI1_10            42574 non-null  float64
     29   LALOWI05_10           57991 non-null  float64
     30   LALOWI1_20            36617 non-null  float64
     31   lapophalf             67963 non-null  float64
     32   lapophalfshare        67963 non-null  float64
     33   lalowihalf            67963 non-null  float64
     34   lalowihalfshare       67963 non-null  float64
     35   lakidshalf            67963 non-null  float64
     36   lakidshalfshare       67963 non-null  float64
     37   laseniorshalf         67963 non-null  float64
     38   laseniorshalfshare    67963 non-null  float64
     39   lawhitehalf           67963 non-null  float64
     40   lawhitehalfshare      67963 non-null  float64
     41   lablackhalf           67963 non-null  float64
     42   lablackhalfshare      67963 non-null  float64
     43   laasianhalf           67963 non-null  float64
     44   laasianhalfshare      67963 non-null  float64
     45   lanhopihalf           67963 non-null  float64
     46   lanhopihalfshare      67963 non-null  float64
     47   laaianhalf            67963 non-null  float64
     48   laaianhalfshare       67963 non-null  float64
     49   laomultirhalf         67963 non-null  float64
     50   laomultirhalfshare    67963 non-null  float64
     51   lahisphalf            67963 non-null  float64
     52   lahisphalfshare       67963 non-null  float64
     53   lahunvhalf            67963 non-null  float64
     54   lahunvhalfshare       67969 non-null  float64
     55   lasnaphalf            67963 non-null  float64
     56   lasnaphalfshare       67969 non-null  float64
     57   lapop1                52542 non-null  float64
     58   lapop1share           52542 non-null  float64
     59   lalowi1               52542 non-null  float64
     60   lalowi1share          52542 non-null  float64
     61   lakids1               52542 non-null  float64
     62   lakids1share          52542 non-null  float64
     63   laseniors1            52542 non-null  float64
     64   laseniors1share       52542 non-null  float64
     65   lawhite1              52542 non-null  float64
     66   lawhite1share         52542 non-null  float64
     67   lablack1              52542 non-null  float64
     68   lablack1share         52542 non-null  float64
     69   laasian1              52542 non-null  float64
     70   laasian1share         52542 non-null  float64
     71   lanhopi1              52542 non-null  float64
     72   lanhopi1share         52542 non-null  float64
     73   laaian1               52542 non-null  float64
     74   laaian1share          52542 non-null  float64
     75   laomultir1            52542 non-null  float64
     76   laomultir1share       52542 non-null  float64
     77   lahisp1               52542 non-null  float64
     78   lahisp1share          52542 non-null  float64
     79   lahunv1               52542 non-null  float64
     80   lahunv1share          52565 non-null  float64
     81   lasnap1               52542 non-null  float64
     82   lasnap1share          52565 non-null  float64
     83   lapop10               7766 non-null   float64
     84   lapop10share          7766 non-null   float64
     85   lalowi10              7766 non-null   float64
     86   lalowi10share         7766 non-null   float64
     87   lakids10              7766 non-null   float64
     88   lakids10share         7766 non-null   float64
     89   laseniors10           7766 non-null   float64
     90   laseniors10share      7766 non-null   float64
     91   lawhite10             7766 non-null   float64
     92   lawhite10share        7766 non-null   float64
     93   lablack10             7766 non-null   float64
     94   lablack10share        7766 non-null   float64
     95   laasian10             7766 non-null   float64
     96   laasian10share        7766 non-null   float64
     97   lanhopi10             7766 non-null   float64
     98   lanhopi10share        7766 non-null   float64
     99   laaian10              7766 non-null   float64
     100  laaian10share         7766 non-null   float64
     101  laomultir10           7766 non-null   float64
     102  laomultir10share      7766 non-null   float64
     103  lahisp10              7766 non-null   float64
     104  lahisp10share         7766 non-null   float64
     105  lahunv10              7766 non-null   float64
     106  lahunv10share         7865 non-null   float64
     107  lasnap10              7766 non-null   float64
     108  lasnap10share         7865 non-null   float64
     109  lapop20               1506 non-null   float64
     110  lapop20share          1506 non-null   float64
     111  lalowi20              1506 non-null   float64
     112  lalowi20share         1506 non-null   float64
     113  lakids20              1506 non-null   float64
     114  lakids20share         1506 non-null   float64
     115  laseniors20           1506 non-null   float64
     116  laseniors20share      1506 non-null   float64
     117  lawhite20             1506 non-null   float64
     118  lawhite20share        1506 non-null   float64
     119  lablack20             1506 non-null   float64
     120  lablack20share        1506 non-null   float64
     121  laasian20             1506 non-null   float64
     122  laasian20share        1506 non-null   float64
     123  lanhopi20             1506 non-null   float64
     124  lanhopi20share        1506 non-null   float64
     125  laaian20              1506 non-null   float64
     126  laaian20share         1506 non-null   float64
     127  laomultir20           1506 non-null   float64
     128  laomultir20share      1506 non-null   float64
     129  lahisp20              1506 non-null   float64
     130  lahisp20share         1506 non-null   float64
     131  lahunv20              1506 non-null   float64
     132  lahunv20share         1611 non-null   float64
     133  lasnap20              1506 non-null   float64
     134  lasnap20share         1611 non-null   float64
     135  TractLOWI             72527 non-null  float64
     136  TractKids             72527 non-null  float64
     137  TractSeniors          72527 non-null  float64
     138  TractWhite            72527 non-null  float64
     139  TractBlack            72527 non-null  float64
     140  TractAsian            72527 non-null  float64
     141  TractNHOPI            72527 non-null  float64
     142  TractAIAN             72527 non-null  float64
     143  TractOMultir          72527 non-null  float64
     144  TractHispanic         72527 non-null  float64
     145  TractHUNV             72527 non-null  float64
     146  TractSNAP             72527 non-null  float64
    dtypes: float64(126), int64(19), object(2)
    memory usage: 81.3+ MB



```python
food_accessColumns = food_access.columns
food_accessColumns
```




    Index(['CensusTract', 'State', 'County', 'Urban', 'Pop2010', 'OHU2010',
           'GroupQuartersFlag', 'NUMGQTRS', 'PCTGQTRS', 'LILATracts_1And10',
           ...
           'TractSeniors', 'TractWhite', 'TractBlack', 'TractAsian', 'TractNHOPI',
           'TractAIAN', 'TractOMultir', 'TractHispanic', 'TractHUNV', 'TractSNAP'],
          dtype='object', length=147)




```python
food_access.isnull().sum()

```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>CensusTract</th>
      <td>0</td>
    </tr>
    <tr>
      <th>State</th>
      <td>0</td>
    </tr>
    <tr>
      <th>County</th>
      <td>0</td>
    </tr>
    <tr>
      <th>Urban</th>
      <td>0</td>
    </tr>
    <tr>
      <th>Pop2010</th>
      <td>0</td>
    </tr>
    <tr>
      <th>OHU2010</th>
      <td>0</td>
    </tr>
    <tr>
      <th>GroupQuartersFlag</th>
      <td>0</td>
    </tr>
    <tr>
      <th>NUMGQTRS</th>
      <td>25</td>
    </tr>
    <tr>
      <th>PCTGQTRS</th>
      <td>25</td>
    </tr>
    <tr>
      <th>LILATracts_1And10</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LILATracts_halfAnd10</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LILATracts_1And20</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LILATracts_Vehicle</th>
      <td>0</td>
    </tr>
    <tr>
      <th>HUNVFlag</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LowIncomeTracts</th>
      <td>0</td>
    </tr>
    <tr>
      <th>PovertyRate</th>
      <td>3</td>
    </tr>
    <tr>
      <th>MedianFamilyIncome</th>
      <td>748</td>
    </tr>
    <tr>
      <th>LA1and10</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LAhalfand10</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LA1and20</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LATracts_half</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LATracts1</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LATracts10</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LATracts20</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LATractsVehicle_20</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LAPOP1_10</th>
      <td>29957</td>
    </tr>
    <tr>
      <th>LAPOP05_10</th>
      <td>14540</td>
    </tr>
    <tr>
      <th>LAPOP1_20</th>
      <td>35914</td>
    </tr>
    <tr>
      <th>LALOWI1_10</th>
      <td>29957</td>
    </tr>
    <tr>
      <th>LALOWI05_10</th>
      <td>14540</td>
    </tr>
    <tr>
      <th>LALOWI1_20</th>
      <td>35914</td>
    </tr>
    <tr>
      <th>lapophalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lapophalfshare</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lalowihalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lalowihalfshare</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lakidshalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lakidshalfshare</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>laseniorshalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>laseniorshalfshare</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lawhitehalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lawhitehalfshare</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lablackhalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lablackhalfshare</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>laasianhalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>laasianhalfshare</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lanhopihalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lanhopihalfshare</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>laaianhalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>laaianhalfshare</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>laomultirhalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>laomultirhalfshare</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lahisphalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lahisphalfshare</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lahunvhalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lahunvhalfshare</th>
      <td>4562</td>
    </tr>
    <tr>
      <th>lasnaphalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lasnaphalfshare</th>
      <td>4562</td>
    </tr>
    <tr>
      <th>lapop1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lapop1share</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lalowi1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lalowi1share</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lakids1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lakids1share</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>laseniors1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>laseniors1share</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lawhite1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lawhite1share</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lablack1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lablack1share</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>laasian1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>laasian1share</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lanhopi1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lanhopi1share</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>laaian1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>laaian1share</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>laomultir1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>laomultir1share</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lahisp1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lahisp1share</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lahunv1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lahunv1share</th>
      <td>19966</td>
    </tr>
    <tr>
      <th>lasnap1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lasnap1share</th>
      <td>19966</td>
    </tr>
    <tr>
      <th>lapop10</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>lapop10share</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>lalowi10</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>lalowi10share</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>lakids10</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>lakids10share</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>laseniors10</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>laseniors10share</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>lawhite10</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>lawhite10share</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>lablack10</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>lablack10share</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>laasian10</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>laasian10share</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>lanhopi10</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>lanhopi10share</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>laaian10</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>laaian10share</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>laomultir10</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>laomultir10share</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>lahisp10</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>lahisp10share</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>lahunv10</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>lahunv10share</th>
      <td>64666</td>
    </tr>
    <tr>
      <th>lasnap10</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>lasnap10share</th>
      <td>64666</td>
    </tr>
    <tr>
      <th>lapop20</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>lapop20share</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>lalowi20</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>lalowi20share</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>lakids20</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>lakids20share</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>laseniors20</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>laseniors20share</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>lawhite20</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>lawhite20share</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>lablack20</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>lablack20share</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>laasian20</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>laasian20share</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>lanhopi20</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>lanhopi20share</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>laaian20</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>laaian20share</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>laomultir20</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>laomultir20share</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>lahisp20</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>lahisp20share</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>lahunv20</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>lahunv20share</th>
      <td>70920</td>
    </tr>
    <tr>
      <th>lasnap20</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>lasnap20share</th>
      <td>70920</td>
    </tr>
    <tr>
      <th>TractLOWI</th>
      <td>4</td>
    </tr>
    <tr>
      <th>TractKids</th>
      <td>4</td>
    </tr>
    <tr>
      <th>TractSeniors</th>
      <td>4</td>
    </tr>
    <tr>
      <th>TractWhite</th>
      <td>4</td>
    </tr>
    <tr>
      <th>TractBlack</th>
      <td>4</td>
    </tr>
    <tr>
      <th>TractAsian</th>
      <td>4</td>
    </tr>
    <tr>
      <th>TractNHOPI</th>
      <td>4</td>
    </tr>
    <tr>
      <th>TractAIAN</th>
      <td>4</td>
    </tr>
    <tr>
      <th>TractOMultir</th>
      <td>4</td>
    </tr>
    <tr>
      <th>TractHispanic</th>
      <td>4</td>
    </tr>
    <tr>
      <th>TractHUNV</th>
      <td>4</td>
    </tr>
    <tr>
      <th>TractSNAP</th>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div><br><label><b>dtype:</b> int64</label>




```python
def missing(DataFrame):
    print ('Percentage of missing values in the dataset:\n',
           round((DataFrame.isnull().sum() * 100/ len(DataFrame)),2).sort_values(ascending=False))


# Call the function and execute
# Syntax: missing(DataFrame)
missing(food_access)
```

    Percentage of missing values in the dataset:
     lalowi20                97.92
    lanhopi20share          97.92
    lanhopi20               97.92
    lahisp20share           97.92
    lahisp20                97.92
    laomultir20share        97.92
    laomultir20             97.92
    laaian20share           97.92
    laaian20                97.92
    laseniors20share        97.92
    laseniors20             97.92
    laasian20share          97.92
    laasian20               97.92
    lablack20share          97.92
    lablack20               97.92
    lawhite20share          97.92
    lawhite20               97.92
    lasnap20                97.92
    lahunv20                97.92
    lapop20                 97.92
    lapop20share            97.92
    lakids20share           97.92
    lalowi20share           97.92
    lakids20                97.92
    lahunv20share           97.78
    lasnap20share           97.78
    laasian10share          89.29
    lanhopi10share          89.29
    lanhopi10               89.29
    lahisp10share           89.29
    lahisp10                89.29
    lasnap10                89.29
    laomultir10             89.29
    lakids10                89.29
    lakids10share           89.29
    laseniors10             89.29
    laseniors10share        89.29
    lapop10share            89.29
    laasian10               89.29
    lablack10share          89.29
    lablack10               89.29
    laaian10                89.29
    laaian10share           89.29
    laomultir10share        89.29
    lahunv10                89.29
    lawhite10share          89.29
    lapop10                 89.29
    lalowi10share           89.29
    lalowi10                89.29
    lawhite10               89.29
    lahunv10share           89.16
    lasnap10share           89.16
    LALOWI1_20              49.52
    LAPOP1_20               49.52
    LAPOP1_10               41.30
    LALOWI1_10              41.30
    laomultir1              27.56
    lahisp1                 27.56
    laomultir1share         27.56
    lapop1                  27.56
    lapop1share             27.56
    laseniors1share         27.56
    laseniors1              27.56
    laasian1share           27.56
    laasian1                27.56
    lablack1share           27.56
    lablack1                27.56
    laaian1share            27.56
    laaian1                 27.56
    lasnap1                 27.56
    lahisp1share            27.56
    lakids1share            27.56
    lakids1                 27.56
    lalowi1share            27.56
    lalowi1                 27.56
    lanhopi1                27.56
    lanhopi1share           27.56
    lawhite1share           27.56
    lahunv1                 27.56
    lawhite1                27.56
    lahunv1share            27.53
    lasnap1share            27.53
    LAPOP05_10              20.05
    LALOWI05_10             20.05
    laasianhalf              6.30
    lanhopihalf              6.30
    laasianhalfshare         6.30
    lahisphalfshare          6.30
    lahisphalf               6.30
    lapophalfshare           6.30
    lapophalf                6.30
    lalowihalf               6.30
    lalowihalfshare          6.30
    lahunvhalf               6.30
    lasnaphalf               6.30
    laseniorshalfshare       6.30
    laseniorshalf            6.30
    lakidshalfshare          6.30
    lakidshalf               6.30
    laomultirhalf            6.30
    laomultirhalfshare       6.30
    lawhitehalfshare         6.30
    lanhopihalfshare         6.30
    laaianhalf               6.30
    laaianhalfshare          6.30
    lablackhalf              6.30
    lablackhalfshare         6.30
    lawhitehalf              6.30
    lasnaphalfshare          6.29
    lahunvhalfshare          6.29
    MedianFamilyIncome       1.03
    NUMGQTRS                 0.03
    PCTGQTRS                 0.03
    TractLOWI                0.01
    TractKids                0.01
    TractBlack               0.01
    TractAsian               0.01
    TractNHOPI               0.01
    TractAIAN                0.01
    TractOMultir             0.01
    TractHispanic            0.01
    TractSeniors             0.01
    TractWhite               0.01
    TractHUNV                0.01
    TractSNAP                0.01
    OHU2010                  0.00
    GroupQuartersFlag        0.00
    Urban                    0.00
    CensusTract              0.00
    State                    0.00
    County                   0.00
    LAhalfand10              0.00
    LA1and10                 0.00
    PovertyRate              0.00
    LowIncomeTracts          0.00
    LILATracts_Vehicle       0.00
    HUNVFlag                 0.00
    LILATracts_1And20        0.00
    LILATracts_halfAnd10     0.00
    Pop2010                  0.00
    LILATracts_1And10        0.00
    LATractsVehicle_20       0.00
    LATracts20               0.00
    LA1and20                 0.00
    LATracts_half            0.00
    LATracts10               0.00
    LATracts1                0.00
    dtype: float64


**Observations**:

How many missing values are there?

- There are missing values in many of the columns; some variables have missing data of over 97%, while others have moderate missingness of between 27% and 49%.  Some of the columns, such as State, County, and CensusTract, have no missing data, while others have minimal missing values, (<1%).


Are these concentrated in specific rows or columns? How does this affect the analysis?

- The majority of missing values are found in specific columns, particularly those pertaining to race and food access.  Comparing various racial groups may become more difficult as a result, and bias may develop if more data is missing from some communities or regions.

Based on the information that is present, how should the missing values be handled?
How will this affect the analysis?
- Columns missing too much data (over 30%) should be removed. Those with moderate missing data (5%-20%) can be filled in using averages or the most common values. Removing extremely incomplete columns guarantees more trustworthy results.  Although it helps preserve more data, filling in missing values could result in minor mistakes.  The analysis may understate disparities in food access in some communities if missing data is dispersed unevenly.






```python
columns_to_drop = [
    'lanhopi20', 'lanhopi20share', 'laaian20', 'laaian20share', 'laomultir20', 'laomultir20share',
    'lahisp20', 'lahisp20share', 'lawhite20', 'lawhite20share', 'laasian20', 'laasian20share',
    'laseniors20', 'laseniors20share', 'lakids20', 'lakids20share', 'lapop20', 'lapop20share',
    'lalowi20', 'lalowi20share', 'lahunv20', 'lahunv20share', 'lasnap20', 'lasnap20share',
    'laasian10', 'laasian10share', 'lahisp10', 'lahisp10share', 'lablack10', 'lablack10share',
    'lawhite10', 'lawhite10share', 'laseniors10', 'laseniors10share', 'lakids10', 'lakids10share',
    'lalowi10', 'lalowi10share', 'lapop10', 'lapop10share', 'lahunv10', 'lahunv10share',
    'lasnap10', 'lasnap10share', 'LAPOP1_20', 'LALOWI1_20', 'LALOWI1_10', 'LAPOP1_10'
]

food_access = food_access.drop(columns=[col for col in columns_to_drop if col in food_access.columns], errors='ignore')

# Check missing values
food_access.isnull().sum()


```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>CensusTract</th>
      <td>0</td>
    </tr>
    <tr>
      <th>State</th>
      <td>0</td>
    </tr>
    <tr>
      <th>County</th>
      <td>0</td>
    </tr>
    <tr>
      <th>Urban</th>
      <td>0</td>
    </tr>
    <tr>
      <th>Pop2010</th>
      <td>0</td>
    </tr>
    <tr>
      <th>OHU2010</th>
      <td>0</td>
    </tr>
    <tr>
      <th>GroupQuartersFlag</th>
      <td>0</td>
    </tr>
    <tr>
      <th>NUMGQTRS</th>
      <td>25</td>
    </tr>
    <tr>
      <th>PCTGQTRS</th>
      <td>25</td>
    </tr>
    <tr>
      <th>LILATracts_1And10</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LILATracts_halfAnd10</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LILATracts_1And20</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LILATracts_Vehicle</th>
      <td>0</td>
    </tr>
    <tr>
      <th>HUNVFlag</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LowIncomeTracts</th>
      <td>0</td>
    </tr>
    <tr>
      <th>PovertyRate</th>
      <td>3</td>
    </tr>
    <tr>
      <th>MedianFamilyIncome</th>
      <td>748</td>
    </tr>
    <tr>
      <th>LA1and10</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LAhalfand10</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LA1and20</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LATracts_half</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LATracts1</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LATracts10</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LATracts20</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LATractsVehicle_20</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LAPOP05_10</th>
      <td>14540</td>
    </tr>
    <tr>
      <th>LALOWI05_10</th>
      <td>14540</td>
    </tr>
    <tr>
      <th>lapophalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lapophalfshare</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lalowihalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lalowihalfshare</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lakidshalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lakidshalfshare</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>laseniorshalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>laseniorshalfshare</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lawhitehalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lawhitehalfshare</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lablackhalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lablackhalfshare</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>laasianhalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>laasianhalfshare</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lanhopihalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lanhopihalfshare</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>laaianhalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>laaianhalfshare</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>laomultirhalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>laomultirhalfshare</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lahisphalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lahisphalfshare</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lahunvhalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lahunvhalfshare</th>
      <td>4562</td>
    </tr>
    <tr>
      <th>lasnaphalf</th>
      <td>4568</td>
    </tr>
    <tr>
      <th>lasnaphalfshare</th>
      <td>4562</td>
    </tr>
    <tr>
      <th>lapop1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lapop1share</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lalowi1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lalowi1share</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lakids1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lakids1share</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>laseniors1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>laseniors1share</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lawhite1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lawhite1share</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lablack1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lablack1share</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>laasian1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>laasian1share</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lanhopi1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lanhopi1share</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>laaian1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>laaian1share</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>laomultir1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>laomultir1share</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lahisp1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lahisp1share</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lahunv1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lahunv1share</th>
      <td>19966</td>
    </tr>
    <tr>
      <th>lasnap1</th>
      <td>19989</td>
    </tr>
    <tr>
      <th>lasnap1share</th>
      <td>19966</td>
    </tr>
    <tr>
      <th>lanhopi10</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>lanhopi10share</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>laaian10</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>laaian10share</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>laomultir10</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>laomultir10share</th>
      <td>64765</td>
    </tr>
    <tr>
      <th>lablack20</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>lablack20share</th>
      <td>71025</td>
    </tr>
    <tr>
      <th>TractLOWI</th>
      <td>4</td>
    </tr>
    <tr>
      <th>TractKids</th>
      <td>4</td>
    </tr>
    <tr>
      <th>TractSeniors</th>
      <td>4</td>
    </tr>
    <tr>
      <th>TractWhite</th>
      <td>4</td>
    </tr>
    <tr>
      <th>TractBlack</th>
      <td>4</td>
    </tr>
    <tr>
      <th>TractAsian</th>
      <td>4</td>
    </tr>
    <tr>
      <th>TractNHOPI</th>
      <td>4</td>
    </tr>
    <tr>
      <th>TractAIAN</th>
      <td>4</td>
    </tr>
    <tr>
      <th>TractOMultir</th>
      <td>4</td>
    </tr>
    <tr>
      <th>TractHispanic</th>
      <td>4</td>
    </tr>
    <tr>
      <th>TractHUNV</th>
      <td>4</td>
    </tr>
    <tr>
      <th>TractSNAP</th>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div><br><label><b>dtype:</b> int64</label>




```python
food_access.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 72531 entries, 0 to 72530
    Data columns (total 99 columns):
     #   Column                Non-Null Count  Dtype  
    ---  ------                --------------  -----  
     0   CensusTract           72531 non-null  int64  
     1   State                 72531 non-null  object 
     2   County                72531 non-null  object 
     3   Urban                 72531 non-null  int64  
     4   Pop2010               72531 non-null  int64  
     5   OHU2010               72531 non-null  int64  
     6   GroupQuartersFlag     72531 non-null  int64  
     7   NUMGQTRS              72506 non-null  float64
     8   PCTGQTRS              72506 non-null  float64
     9   LILATracts_1And10     72531 non-null  int64  
     10  LILATracts_halfAnd10  72531 non-null  int64  
     11  LILATracts_1And20     72531 non-null  int64  
     12  LILATracts_Vehicle    72531 non-null  int64  
     13  HUNVFlag              72531 non-null  int64  
     14  LowIncomeTracts       72531 non-null  int64  
     15  PovertyRate           72528 non-null  float64
     16  MedianFamilyIncome    71783 non-null  float64
     17  LA1and10              72531 non-null  int64  
     18  LAhalfand10           72531 non-null  int64  
     19  LA1and20              72531 non-null  int64  
     20  LATracts_half         72531 non-null  int64  
     21  LATracts1             72531 non-null  int64  
     22  LATracts10            72531 non-null  int64  
     23  LATracts20            72531 non-null  int64  
     24  LATractsVehicle_20    72531 non-null  int64  
     25  LAPOP05_10            57991 non-null  float64
     26  LALOWI05_10           57991 non-null  float64
     27  lapophalf             67963 non-null  float64
     28  lapophalfshare        67963 non-null  float64
     29  lalowihalf            67963 non-null  float64
     30  lalowihalfshare       67963 non-null  float64
     31  lakidshalf            67963 non-null  float64
     32  lakidshalfshare       67963 non-null  float64
     33  laseniorshalf         67963 non-null  float64
     34  laseniorshalfshare    67963 non-null  float64
     35  lawhitehalf           67963 non-null  float64
     36  lawhitehalfshare      67963 non-null  float64
     37  lablackhalf           67963 non-null  float64
     38  lablackhalfshare      67963 non-null  float64
     39  laasianhalf           67963 non-null  float64
     40  laasianhalfshare      67963 non-null  float64
     41  lanhopihalf           67963 non-null  float64
     42  lanhopihalfshare      67963 non-null  float64
     43  laaianhalf            67963 non-null  float64
     44  laaianhalfshare       67963 non-null  float64
     45  laomultirhalf         67963 non-null  float64
     46  laomultirhalfshare    67963 non-null  float64
     47  lahisphalf            67963 non-null  float64
     48  lahisphalfshare       67963 non-null  float64
     49  lahunvhalf            67963 non-null  float64
     50  lahunvhalfshare       67969 non-null  float64
     51  lasnaphalf            67963 non-null  float64
     52  lasnaphalfshare       67969 non-null  float64
     53  lapop1                52542 non-null  float64
     54  lapop1share           52542 non-null  float64
     55  lalowi1               52542 non-null  float64
     56  lalowi1share          52542 non-null  float64
     57  lakids1               52542 non-null  float64
     58  lakids1share          52542 non-null  float64
     59  laseniors1            52542 non-null  float64
     60  laseniors1share       52542 non-null  float64
     61  lawhite1              52542 non-null  float64
     62  lawhite1share         52542 non-null  float64
     63  lablack1              52542 non-null  float64
     64  lablack1share         52542 non-null  float64
     65  laasian1              52542 non-null  float64
     66  laasian1share         52542 non-null  float64
     67  lanhopi1              52542 non-null  float64
     68  lanhopi1share         52542 non-null  float64
     69  laaian1               52542 non-null  float64
     70  laaian1share          52542 non-null  float64
     71  laomultir1            52542 non-null  float64
     72  laomultir1share       52542 non-null  float64
     73  lahisp1               52542 non-null  float64
     74  lahisp1share          52542 non-null  float64
     75  lahunv1               52542 non-null  float64
     76  lahunv1share          52565 non-null  float64
     77  lasnap1               52542 non-null  float64
     78  lasnap1share          52565 non-null  float64
     79  lanhopi10             7766 non-null   float64
     80  lanhopi10share        7766 non-null   float64
     81  laaian10              7766 non-null   float64
     82  laaian10share         7766 non-null   float64
     83  laomultir10           7766 non-null   float64
     84  laomultir10share      7766 non-null   float64
     85  lablack20             1506 non-null   float64
     86  lablack20share        1506 non-null   float64
     87  TractLOWI             72527 non-null  float64
     88  TractKids             72527 non-null  float64
     89  TractSeniors          72527 non-null  float64
     90  TractWhite            72527 non-null  float64
     91  TractBlack            72527 non-null  float64
     92  TractAsian            72527 non-null  float64
     93  TractNHOPI            72527 non-null  float64
     94  TractAIAN             72527 non-null  float64
     95  TractOMultir          72527 non-null  float64
     96  TractHispanic         72527 non-null  float64
     97  TractHUNV             72527 non-null  float64
     98  TractSNAP             72527 non-null  float64
    dtypes: float64(78), int64(19), object(2)
    memory usage: 54.8+ MB



```python
food_access.describe()
```





  <div id="df-1a74eb65-cb76-49c1-b617-a943466f4e45" class="colab-df-container">
    <div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CensusTract</th>
      <th>Urban</th>
      <th>Pop2010</th>
      <th>OHU2010</th>
      <th>GroupQuartersFlag</th>
      <th>NUMGQTRS</th>
      <th>PCTGQTRS</th>
      <th>LILATracts_1And10</th>
      <th>LILATracts_halfAnd10</th>
      <th>LILATracts_1And20</th>
      <th>LILATracts_Vehicle</th>
      <th>HUNVFlag</th>
      <th>LowIncomeTracts</th>
      <th>PovertyRate</th>
      <th>MedianFamilyIncome</th>
      <th>LA1and10</th>
      <th>LAhalfand10</th>
      <th>LA1and20</th>
      <th>LATracts_half</th>
      <th>LATracts1</th>
      <th>LATracts10</th>
      <th>LATracts20</th>
      <th>LATractsVehicle_20</th>
      <th>LAPOP05_10</th>
      <th>LALOWI05_10</th>
      <th>lapophalf</th>
      <th>lapophalfshare</th>
      <th>lalowihalf</th>
      <th>lalowihalfshare</th>
      <th>lakidshalf</th>
      <th>lakidshalfshare</th>
      <th>laseniorshalf</th>
      <th>laseniorshalfshare</th>
      <th>lawhitehalf</th>
      <th>lawhitehalfshare</th>
      <th>lablackhalf</th>
      <th>lablackhalfshare</th>
      <th>laasianhalf</th>
      <th>laasianhalfshare</th>
      <th>lanhopihalf</th>
      <th>lanhopihalfshare</th>
      <th>laaianhalf</th>
      <th>laaianhalfshare</th>
      <th>laomultirhalf</th>
      <th>laomultirhalfshare</th>
      <th>lahisphalf</th>
      <th>lahisphalfshare</th>
      <th>lahunvhalf</th>
      <th>lahunvhalfshare</th>
      <th>lasnaphalf</th>
      <th>lasnaphalfshare</th>
      <th>lapop1</th>
      <th>lapop1share</th>
      <th>lalowi1</th>
      <th>lalowi1share</th>
      <th>lakids1</th>
      <th>lakids1share</th>
      <th>laseniors1</th>
      <th>laseniors1share</th>
      <th>lawhite1</th>
      <th>lawhite1share</th>
      <th>lablack1</th>
      <th>lablack1share</th>
      <th>laasian1</th>
      <th>laasian1share</th>
      <th>lanhopi1</th>
      <th>lanhopi1share</th>
      <th>laaian1</th>
      <th>laaian1share</th>
      <th>laomultir1</th>
      <th>laomultir1share</th>
      <th>lahisp1</th>
      <th>lahisp1share</th>
      <th>lahunv1</th>
      <th>lahunv1share</th>
      <th>lasnap1</th>
      <th>lasnap1share</th>
      <th>lanhopi10</th>
      <th>lanhopi10share</th>
      <th>laaian10</th>
      <th>laaian10share</th>
      <th>laomultir10</th>
      <th>laomultir10share</th>
      <th>lablack20</th>
      <th>lablack20share</th>
      <th>TractLOWI</th>
      <th>TractKids</th>
      <th>TractSeniors</th>
      <th>TractWhite</th>
      <th>TractBlack</th>
      <th>TractAsian</th>
      <th>TractNHOPI</th>
      <th>TractAIAN</th>
      <th>TractOMultir</th>
      <th>TractHispanic</th>
      <th>TractHUNV</th>
      <th>TractSNAP</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>7.253100e+04</td>
      <td>72531.000000</td>
      <td>72531.000000</td>
      <td>72531.000000</td>
      <td>72531.000000</td>
      <td>72506.000000</td>
      <td>72506.000000</td>
      <td>72531.000000</td>
      <td>72531.000000</td>
      <td>72531.000000</td>
      <td>72531.000000</td>
      <td>72531.000000</td>
      <td>72531.000000</td>
      <td>72528.000000</td>
      <td>71783.000000</td>
      <td>72531.000000</td>
      <td>72531.000000</td>
      <td>72531.000000</td>
      <td>72531.000000</td>
      <td>72531.000000</td>
      <td>72531.000000</td>
      <td>72531.000000</td>
      <td>72531.000000</td>
      <td>57991.000000</td>
      <td>57991.000000</td>
      <td>67963.000000</td>
      <td>67963.00000</td>
      <td>67963.000000</td>
      <td>67963.000000</td>
      <td>67963.000000</td>
      <td>67963.000000</td>
      <td>67963.000000</td>
      <td>67963.000000</td>
      <td>67963.000000</td>
      <td>67963.000000</td>
      <td>67963.000000</td>
      <td>67963.000000</td>
      <td>67963.000000</td>
      <td>67963.000000</td>
      <td>67963.000000</td>
      <td>67963.000000</td>
      <td>67963.000000</td>
      <td>67963.000000</td>
      <td>67963.000000</td>
      <td>67963.00000</td>
      <td>67963.000000</td>
      <td>67963.000000</td>
      <td>67963.000000</td>
      <td>67969.000000</td>
      <td>67963.000000</td>
      <td>67969.000000</td>
      <td>52542.000000</td>
      <td>52542.000000</td>
      <td>52542.000000</td>
      <td>52542.000000</td>
      <td>52542.000000</td>
      <td>52542.000000</td>
      <td>52542.000000</td>
      <td>52542.000000</td>
      <td>52542.000000</td>
      <td>52542.000000</td>
      <td>52542.000000</td>
      <td>52542.000000</td>
      <td>52542.000000</td>
      <td>52542.000000</td>
      <td>52542.000000</td>
      <td>52542.000000</td>
      <td>52542.000000</td>
      <td>52542.000000</td>
      <td>52542.000000</td>
      <td>52542.000000</td>
      <td>52542.000000</td>
      <td>52542.000000</td>
      <td>52542.000000</td>
      <td>52565.000000</td>
      <td>52542.000000</td>
      <td>52565.000000</td>
      <td>7766.000000</td>
      <td>7766.000000</td>
      <td>7766.000000</td>
      <td>7766.000000</td>
      <td>7766.000000</td>
      <td>7766.000000</td>
      <td>1506.000000</td>
      <td>1506.000000</td>
      <td>72527.000000</td>
      <td>72527.000000</td>
      <td>72527.000000</td>
      <td>72527.000000</td>
      <td>72527.000000</td>
      <td>72527.000000</td>
      <td>72527.000000</td>
      <td>72527.000000</td>
      <td>72527.000000</td>
      <td>72527.000000</td>
      <td>72527.000000</td>
      <td>72527.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>2.782573e+10</td>
      <td>0.760626</td>
      <td>4256.739022</td>
      <td>1609.191821</td>
      <td>0.007114</td>
      <td>110.121549</td>
      <td>2.708677</td>
      <td>0.128125</td>
      <td>0.279150</td>
      <td>0.112228</td>
      <td>0.139609</td>
      <td>0.210820</td>
      <td>0.417573</td>
      <td>15.183864</td>
      <td>77037.792249</td>
      <td>0.379810</td>
      <td>0.682756</td>
      <td>0.340668</td>
      <td>0.638830</td>
      <td>0.335884</td>
      <td>0.043926</td>
      <td>0.004784</td>
      <td>0.214750</td>
      <td>2657.206946</td>
      <td>797.488214</td>
      <td>3166.061901</td>
      <td>73.42577</td>
      <td>955.153495</td>
      <td>23.095219</td>
      <td>770.609493</td>
      <td>17.395343</td>
      <td>422.928564</td>
      <td>10.325693</td>
      <td>2428.490944</td>
      <td>56.060217</td>
      <td>360.950326</td>
      <td>9.064957</td>
      <td>115.071833</td>
      <td>2.398870</td>
      <td>4.783117</td>
      <td>0.104870</td>
      <td>31.484852</td>
      <td>0.806837</td>
      <td>225.295322</td>
      <td>4.98998</td>
      <td>401.074129</td>
      <td>8.631819</td>
      <td>69.491223</td>
      <td>4.684649</td>
      <td>135.491120</td>
      <td>8.934348</td>
      <td>2337.675612</td>
      <td>54.081743</td>
      <td>669.711107</td>
      <td>16.149574</td>
      <td>569.749496</td>
      <td>12.810448</td>
      <td>319.298675</td>
      <td>7.826267</td>
      <td>1904.910319</td>
      <td>44.084766</td>
      <td>218.471946</td>
      <td>5.243149</td>
      <td>57.908587</td>
      <td>1.172348</td>
      <td>2.883312</td>
      <td>0.063707</td>
      <td>27.301131</td>
      <td>0.724699</td>
      <td>126.201591</td>
      <td>2.793007</td>
      <td>215.850101</td>
      <td>4.630486</td>
      <td>39.596875</td>
      <td>2.631525</td>
      <td>92.520003</td>
      <td>5.995943</td>
      <td>0.521762</td>
      <td>0.026813</td>
      <td>38.426346</td>
      <td>1.250255</td>
      <td>30.291398</td>
      <td>0.971561</td>
      <td>3.717131</td>
      <td>0.138612</td>
      <td>1385.054352</td>
      <td>1022.695327</td>
      <td>555.197113</td>
      <td>3082.337157</td>
      <td>536.756160</td>
      <td>202.327685</td>
      <td>7.445655</td>
      <td>40.152316</td>
      <td>387.664649</td>
      <td>695.979277</td>
      <td>143.709736</td>
      <td>201.753182</td>
    </tr>
    <tr>
      <th>std</th>
      <td>1.581647e+10</td>
      <td>0.426704</td>
      <td>1955.987626</td>
      <td>725.676046</td>
      <td>0.084046</td>
      <td>443.931753</td>
      <td>9.570875</td>
      <td>0.334231</td>
      <td>0.448584</td>
      <td>0.315649</td>
      <td>0.346584</td>
      <td>0.407894</td>
      <td>0.493162</td>
      <td>11.919903</td>
      <td>37544.445885</td>
      <td>0.485343</td>
      <td>0.465406</td>
      <td>0.473937</td>
      <td>0.480343</td>
      <td>0.472302</td>
      <td>0.204932</td>
      <td>0.069002</td>
      <td>0.410651</td>
      <td>2044.331313</td>
      <td>771.432588</td>
      <td>2003.570508</td>
      <td>29.06663</td>
      <td>790.299662</td>
      <td>16.502754</td>
      <td>582.563153</td>
      <td>8.473848</td>
      <td>328.272913</td>
      <td>7.330619</td>
      <td>1772.177187</td>
      <td>30.344494</td>
      <td>687.258803</td>
      <td>16.866031</td>
      <td>269.501279</td>
      <td>4.930797</td>
      <td>33.925042</td>
      <td>0.776388</td>
      <td>173.356852</td>
      <td>4.574504</td>
      <td>331.576406</td>
      <td>6.17208</td>
      <td>742.022316</td>
      <td>13.411754</td>
      <td>80.667756</td>
      <td>6.011297</td>
      <td>135.906721</td>
      <td>9.072652</td>
      <td>1980.761103</td>
      <td>36.760908</td>
      <td>706.558756</td>
      <td>15.479861</td>
      <td>541.167867</td>
      <td>9.479667</td>
      <td>304.305296</td>
      <td>7.189503</td>
      <td>1730.446988</td>
      <td>33.825309</td>
      <td>514.874189</td>
      <td>12.092215</td>
      <td>163.044838</td>
      <td>2.947656</td>
      <td>27.618672</td>
      <td>0.687778</td>
      <td>182.466993</td>
      <td>4.889572</td>
      <td>230.437308</td>
      <td>4.390135</td>
      <td>516.519961</td>
      <td>9.393900</td>
      <td>55.315309</td>
      <td>4.072878</td>
      <td>111.490443</td>
      <td>7.311362</td>
      <td>5.977160</td>
      <td>0.987922</td>
      <td>284.216232</td>
      <td>8.045275</td>
      <td>94.638767</td>
      <td>2.712061</td>
      <td>33.886497</td>
      <td>0.897988</td>
      <td>983.709351</td>
      <td>615.445960</td>
      <td>351.805391</td>
      <td>1796.364560</td>
      <td>889.118109</td>
      <td>435.878339</td>
      <td>45.186581</td>
      <td>177.378696</td>
      <td>529.349680</td>
      <td>1119.472739</td>
      <td>232.738869</td>
      <td>185.760089</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1.001020e+09</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>2499.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.00000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.00000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>1.212708e+10</td>
      <td>1.000000</td>
      <td>2899.000000</td>
      <td>1108.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>6.500000</td>
      <td>51484.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1083.000000</td>
      <td>237.000000</td>
      <td>1756.000000</td>
      <td>55.63000</td>
      <td>380.000000</td>
      <td>10.160000</td>
      <td>369.000000</td>
      <td>11.550000</td>
      <td>195.000000</td>
      <td>5.290000</td>
      <td>1071.000000</td>
      <td>31.430000</td>
      <td>22.000000</td>
      <td>0.560000</td>
      <td>10.000000</td>
      <td>0.280000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>4.000000</td>
      <td>0.100000</td>
      <td>51.000000</td>
      <td>1.45000</td>
      <td>52.000000</td>
      <td>1.470000</td>
      <td>18.000000</td>
      <td>1.250000</td>
      <td>35.000000</td>
      <td>2.460000</td>
      <td>665.000000</td>
      <td>17.892500</td>
      <td>132.000000</td>
      <td>3.310000</td>
      <td>137.000000</td>
      <td>3.720000</td>
      <td>74.000000</td>
      <td>1.880000</td>
      <td>405.000000</td>
      <td>10.820000</td>
      <td>7.000000</td>
      <td>0.190000</td>
      <td>4.000000</td>
      <td>0.100000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>0.030000</td>
      <td>19.000000</td>
      <td>0.550000</td>
      <td>20.000000</td>
      <td>0.570000</td>
      <td>5.000000</td>
      <td>0.320000</td>
      <td>12.000000</td>
      <td>0.790000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.010000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>680.000000</td>
      <td>611.000000</td>
      <td>320.000000</td>
      <td>1848.000000</td>
      <td>43.000000</td>
      <td>17.000000</td>
      <td>0.000000</td>
      <td>7.000000</td>
      <td>85.000000</td>
      <td>88.000000</td>
      <td>36.000000</td>
      <td>67.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>2.712979e+10</td>
      <td>1.000000</td>
      <td>4011.000000</td>
      <td>1525.000000</td>
      <td>0.000000</td>
      <td>7.000000</td>
      <td>0.180000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>12.000000</td>
      <td>68821.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>2387.000000</td>
      <td>584.000000</td>
      <td>2926.000000</td>
      <td>83.50000</td>
      <td>769.000000</td>
      <td>19.990000</td>
      <td>673.000000</td>
      <td>18.640000</td>
      <td>373.000000</td>
      <td>9.770000</td>
      <td>2193.000000</td>
      <td>60.550000</td>
      <td>84.000000</td>
      <td>2.040000</td>
      <td>32.000000</td>
      <td>0.810000</td>
      <td>1.000000</td>
      <td>0.020000</td>
      <td>10.000000</td>
      <td>0.250000</td>
      <td>112.000000</td>
      <td>2.78000</td>
      <td>139.000000</td>
      <td>3.460000</td>
      <td>45.000000</td>
      <td>2.910000</td>
      <td>95.000000</td>
      <td>6.260000</td>
      <td>2003.000000</td>
      <td>55.215000</td>
      <td>464.000000</td>
      <td>11.710000</td>
      <td>456.000000</td>
      <td>12.480000</td>
      <td>259.000000</td>
      <td>6.550000</td>
      <td>1545.000000</td>
      <td>40.720000</td>
      <td>31.000000</td>
      <td>0.750000</td>
      <td>14.000000</td>
      <td>0.350000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>6.000000</td>
      <td>0.140000</td>
      <td>56.000000</td>
      <td>1.410000</td>
      <td>63.000000</td>
      <td>1.560000</td>
      <td>22.000000</td>
      <td>1.400000</td>
      <td>53.000000</td>
      <td>3.430000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>0.020000</td>
      <td>6.000000</td>
      <td>0.180000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1164.000000</td>
      <td>924.000000</td>
      <td>497.000000</td>
      <td>2914.000000</td>
      <td>160.000000</td>
      <td>58.000000</td>
      <td>1.000000</td>
      <td>15.000000</td>
      <td>186.000000</td>
      <td>243.000000</td>
      <td>82.000000</td>
      <td>152.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>4.103900e+10</td>
      <td>1.000000</td>
      <td>5330.500000</td>
      <td>2021.000000</td>
      <td>0.000000</td>
      <td>64.000000</td>
      <td>1.570000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>20.600000</td>
      <td>93868.500000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>3827.000000</td>
      <td>1128.500000</td>
      <td>4299.000000</td>
      <td>99.80000</td>
      <td>1329.000000</td>
      <td>32.910000</td>
      <td>1048.000000</td>
      <td>23.410000</td>
      <td>586.000000</td>
      <td>14.080000</td>
      <td>3476.000000</td>
      <td>82.920000</td>
      <td>355.000000</td>
      <td>8.580000</td>
      <td>104.000000</td>
      <td>2.340000</td>
      <td>3.000000</td>
      <td>0.070000</td>
      <td>22.000000</td>
      <td>0.520000</td>
      <td>256.000000</td>
      <td>5.93000</td>
      <td>400.000000</td>
      <td>9.370000</td>
      <td>92.000000</td>
      <td>5.800000</td>
      <td>193.000000</td>
      <td>12.470000</td>
      <td>3540.000000</td>
      <td>94.070000</td>
      <td>987.000000</td>
      <td>25.260000</td>
      <td>846.000000</td>
      <td>20.990000</td>
      <td>484.000000</td>
      <td>12.230000</td>
      <td>2969.000000</td>
      <td>75.867500</td>
      <td>161.000000</td>
      <td>3.780000</td>
      <td>46.000000</td>
      <td>1.030000</td>
      <td>1.000000</td>
      <td>0.030000</td>
      <td>15.000000</td>
      <td>0.350000</td>
      <td>135.000000</td>
      <td>3.080000</td>
      <td>182.000000</td>
      <td>4.170000</td>
      <td>54.000000</td>
      <td>3.400000</td>
      <td>134.000000</td>
      <td>8.660000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>6.000000</td>
      <td>0.180000</td>
      <td>24.000000</td>
      <td>0.760000</td>
      <td>1.000000</td>
      <td>0.020000</td>
      <td>1846.000000</td>
      <td>1312.000000</td>
      <td>718.000000</td>
      <td>4118.000000</td>
      <td>610.000000</td>
      <td>189.000000</td>
      <td>5.000000</td>
      <td>33.000000</td>
      <td>448.000000</td>
      <td>751.000000</td>
      <td>168.500000</td>
      <td>282.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>5.604595e+10</td>
      <td>1.000000</td>
      <td>37452.000000</td>
      <td>16043.000000</td>
      <td>1.000000</td>
      <td>19496.000000</td>
      <td>100.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>100.000000</td>
      <td>250001.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>32582.000000</td>
      <td>9874.000000</td>
      <td>37452.000000</td>
      <td>100.00000</td>
      <td>19602.000000</td>
      <td>100.000000</td>
      <td>9084.000000</td>
      <td>90.800000</td>
      <td>15261.000000</td>
      <td>100.000000</td>
      <td>28477.000000</td>
      <td>100.000000</td>
      <td>13594.000000</td>
      <td>100.000000</td>
      <td>6964.000000</td>
      <td>100.000000</td>
      <td>2786.000000</td>
      <td>85.880000</td>
      <td>8507.000000</td>
      <td>100.000000</td>
      <td>6415.000000</td>
      <td>100.00000</td>
      <td>12805.000000</td>
      <td>100.000000</td>
      <td>1803.000000</td>
      <td>100.000000</td>
      <td>1582.000000</td>
      <td>100.000000</td>
      <td>37061.000000</td>
      <td>100.000000</td>
      <td>19397.000000</td>
      <td>100.000000</td>
      <td>8907.000000</td>
      <td>90.800000</td>
      <td>10349.000000</td>
      <td>100.000000</td>
      <td>28165.000000</td>
      <td>100.000000</td>
      <td>12112.000000</td>
      <td>100.000000</td>
      <td>5809.000000</td>
      <td>100.000000</td>
      <td>2164.000000</td>
      <td>85.880000</td>
      <td>8444.000000</td>
      <td>100.000000</td>
      <td>6146.000000</td>
      <td>100.000000</td>
      <td>11502.000000</td>
      <td>100.000000</td>
      <td>1794.000000</td>
      <td>100.000000</td>
      <td>1582.000000</td>
      <td>100.000000</td>
      <td>266.000000</td>
      <td>85.880000</td>
      <td>6947.000000</td>
      <td>99.340000</td>
      <td>1724.000000</td>
      <td>45.450000</td>
      <td>1086.000000</td>
      <td>20.410000</td>
      <td>12562.000000</td>
      <td>11845.000000</td>
      <td>17271.000000</td>
      <td>28983.000000</td>
      <td>16804.000000</td>
      <td>10485.000000</td>
      <td>3491.000000</td>
      <td>9009.000000</td>
      <td>8839.000000</td>
      <td>15420.000000</td>
      <td>6059.000000</td>
      <td>2175.000000</td>
    </tr>
  </tbody>
</table>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-1a74eb65-cb76-49c1-b617-a943466f4e45')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  
    </button>

  

    
  </div>


<div id="df-e9b75408-e974-4080-8c37-566591feb737">
  <button class="colab-df-quickchart" onclick="quickchart('df-e9b75408-e974-4080-8c37-566591feb737')"
            title="Suggest charts"
            style="display:none;">


  </button>



  
</div>

    </div>
  </div>





```python
maxValuesFA = food_access.max()

maxValuesFA

```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>CensusTract</th>
      <td>56045951300</td>
    </tr>
    <tr>
      <th>State</th>
      <td>Wyoming</td>
    </tr>
    <tr>
      <th>County</th>
      <td>Ziebach County</td>
    </tr>
    <tr>
      <th>Urban</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Pop2010</th>
      <td>37452</td>
    </tr>
    <tr>
      <th>OHU2010</th>
      <td>16043</td>
    </tr>
    <tr>
      <th>GroupQuartersFlag</th>
      <td>1</td>
    </tr>
    <tr>
      <th>NUMGQTRS</th>
      <td>19496.0</td>
    </tr>
    <tr>
      <th>PCTGQTRS</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>LILATracts_1And10</th>
      <td>1</td>
    </tr>
    <tr>
      <th>LILATracts_halfAnd10</th>
      <td>1</td>
    </tr>
    <tr>
      <th>LILATracts_1And20</th>
      <td>1</td>
    </tr>
    <tr>
      <th>LILATracts_Vehicle</th>
      <td>1</td>
    </tr>
    <tr>
      <th>HUNVFlag</th>
      <td>1</td>
    </tr>
    <tr>
      <th>LowIncomeTracts</th>
      <td>1</td>
    </tr>
    <tr>
      <th>PovertyRate</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>MedianFamilyIncome</th>
      <td>250001.0</td>
    </tr>
    <tr>
      <th>LA1and10</th>
      <td>1</td>
    </tr>
    <tr>
      <th>LAhalfand10</th>
      <td>1</td>
    </tr>
    <tr>
      <th>LA1and20</th>
      <td>1</td>
    </tr>
    <tr>
      <th>LATracts_half</th>
      <td>1</td>
    </tr>
    <tr>
      <th>LATracts1</th>
      <td>1</td>
    </tr>
    <tr>
      <th>LATracts10</th>
      <td>1</td>
    </tr>
    <tr>
      <th>LATracts20</th>
      <td>1</td>
    </tr>
    <tr>
      <th>LATractsVehicle_20</th>
      <td>1</td>
    </tr>
    <tr>
      <th>LAPOP05_10</th>
      <td>32582.0</td>
    </tr>
    <tr>
      <th>LALOWI05_10</th>
      <td>9874.0</td>
    </tr>
    <tr>
      <th>lapophalf</th>
      <td>37452.0</td>
    </tr>
    <tr>
      <th>lapophalfshare</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>lalowihalf</th>
      <td>19602.0</td>
    </tr>
    <tr>
      <th>lalowihalfshare</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>lakidshalf</th>
      <td>9084.0</td>
    </tr>
    <tr>
      <th>lakidshalfshare</th>
      <td>90.8</td>
    </tr>
    <tr>
      <th>laseniorshalf</th>
      <td>15261.0</td>
    </tr>
    <tr>
      <th>laseniorshalfshare</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>lawhitehalf</th>
      <td>28477.0</td>
    </tr>
    <tr>
      <th>lawhitehalfshare</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>lablackhalf</th>
      <td>13594.0</td>
    </tr>
    <tr>
      <th>lablackhalfshare</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>laasianhalf</th>
      <td>6964.0</td>
    </tr>
    <tr>
      <th>laasianhalfshare</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>lanhopihalf</th>
      <td>2786.0</td>
    </tr>
    <tr>
      <th>lanhopihalfshare</th>
      <td>85.88</td>
    </tr>
    <tr>
      <th>laaianhalf</th>
      <td>8507.0</td>
    </tr>
    <tr>
      <th>laaianhalfshare</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>laomultirhalf</th>
      <td>6415.0</td>
    </tr>
    <tr>
      <th>laomultirhalfshare</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>lahisphalf</th>
      <td>12805.0</td>
    </tr>
    <tr>
      <th>lahisphalfshare</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>lahunvhalf</th>
      <td>1803.0</td>
    </tr>
    <tr>
      <th>lahunvhalfshare</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>lasnaphalf</th>
      <td>1582.0</td>
    </tr>
    <tr>
      <th>lasnaphalfshare</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>lapop1</th>
      <td>37061.0</td>
    </tr>
    <tr>
      <th>lapop1share</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>lalowi1</th>
      <td>19397.0</td>
    </tr>
    <tr>
      <th>lalowi1share</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>lakids1</th>
      <td>8907.0</td>
    </tr>
    <tr>
      <th>lakids1share</th>
      <td>90.8</td>
    </tr>
    <tr>
      <th>laseniors1</th>
      <td>10349.0</td>
    </tr>
    <tr>
      <th>laseniors1share</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>lawhite1</th>
      <td>28165.0</td>
    </tr>
    <tr>
      <th>lawhite1share</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>lablack1</th>
      <td>12112.0</td>
    </tr>
    <tr>
      <th>lablack1share</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>laasian1</th>
      <td>5809.0</td>
    </tr>
    <tr>
      <th>laasian1share</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>lanhopi1</th>
      <td>2164.0</td>
    </tr>
    <tr>
      <th>lanhopi1share</th>
      <td>85.88</td>
    </tr>
    <tr>
      <th>laaian1</th>
      <td>8444.0</td>
    </tr>
    <tr>
      <th>laaian1share</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>laomultir1</th>
      <td>6146.0</td>
    </tr>
    <tr>
      <th>laomultir1share</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>lahisp1</th>
      <td>11502.0</td>
    </tr>
    <tr>
      <th>lahisp1share</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>lahunv1</th>
      <td>1794.0</td>
    </tr>
    <tr>
      <th>lahunv1share</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>lasnap1</th>
      <td>1582.0</td>
    </tr>
    <tr>
      <th>lasnap1share</th>
      <td>100.0</td>
    </tr>
    <tr>
      <th>lanhopi10</th>
      <td>266.0</td>
    </tr>
    <tr>
      <th>lanhopi10share</th>
      <td>85.88</td>
    </tr>
    <tr>
      <th>laaian10</th>
      <td>6947.0</td>
    </tr>
    <tr>
      <th>laaian10share</th>
      <td>99.34</td>
    </tr>
    <tr>
      <th>laomultir10</th>
      <td>1724.0</td>
    </tr>
    <tr>
      <th>laomultir10share</th>
      <td>45.45</td>
    </tr>
    <tr>
      <th>lablack20</th>
      <td>1086.0</td>
    </tr>
    <tr>
      <th>lablack20share</th>
      <td>20.41</td>
    </tr>
    <tr>
      <th>TractLOWI</th>
      <td>12562.0</td>
    </tr>
    <tr>
      <th>TractKids</th>
      <td>11845.0</td>
    </tr>
    <tr>
      <th>TractSeniors</th>
      <td>17271.0</td>
    </tr>
    <tr>
      <th>TractWhite</th>
      <td>28983.0</td>
    </tr>
    <tr>
      <th>TractBlack</th>
      <td>16804.0</td>
    </tr>
    <tr>
      <th>TractAsian</th>
      <td>10485.0</td>
    </tr>
    <tr>
      <th>TractNHOPI</th>
      <td>3491.0</td>
    </tr>
    <tr>
      <th>TractAIAN</th>
      <td>9009.0</td>
    </tr>
    <tr>
      <th>TractOMultir</th>
      <td>8839.0</td>
    </tr>
    <tr>
      <th>TractHispanic</th>
      <td>15420.0</td>
    </tr>
    <tr>
      <th>TractHUNV</th>
      <td>6059.0</td>
    </tr>
    <tr>
      <th>TractSNAP</th>
      <td>2175.0</td>
    </tr>
  </tbody>
</table>
</div><br><label><b>dtype:</b> object</label>




```python
minValuesFA = food_access.min()
minValuesFA

```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>CensusTract</th>
      <td>1001020100</td>
    </tr>
    <tr>
      <th>State</th>
      <td>Alabama</td>
    </tr>
    <tr>
      <th>County</th>
      <td>Abbeville County</td>
    </tr>
    <tr>
      <th>Urban</th>
      <td>0</td>
    </tr>
    <tr>
      <th>Pop2010</th>
      <td>1</td>
    </tr>
    <tr>
      <th>OHU2010</th>
      <td>0</td>
    </tr>
    <tr>
      <th>GroupQuartersFlag</th>
      <td>0</td>
    </tr>
    <tr>
      <th>NUMGQTRS</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>PCTGQTRS</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>LILATracts_1And10</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LILATracts_halfAnd10</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LILATracts_1And20</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LILATracts_Vehicle</th>
      <td>0</td>
    </tr>
    <tr>
      <th>HUNVFlag</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LowIncomeTracts</th>
      <td>0</td>
    </tr>
    <tr>
      <th>PovertyRate</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>MedianFamilyIncome</th>
      <td>2499.0</td>
    </tr>
    <tr>
      <th>LA1and10</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LAhalfand10</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LA1and20</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LATracts_half</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LATracts1</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LATracts10</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LATracts20</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LATractsVehicle_20</th>
      <td>0</td>
    </tr>
    <tr>
      <th>LAPOP05_10</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>LALOWI05_10</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lapophalf</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lapophalfshare</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lalowihalf</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lalowihalfshare</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lakidshalf</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lakidshalfshare</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>laseniorshalf</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>laseniorshalfshare</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lawhitehalf</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lawhitehalfshare</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lablackhalf</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lablackhalfshare</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>laasianhalf</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>laasianhalfshare</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lanhopihalf</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lanhopihalfshare</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>laaianhalf</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>laaianhalfshare</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>laomultirhalf</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>laomultirhalfshare</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lahisphalf</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lahisphalfshare</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lahunvhalf</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lahunvhalfshare</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lasnaphalf</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lasnaphalfshare</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lapop1</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lapop1share</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lalowi1</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lalowi1share</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lakids1</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lakids1share</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>laseniors1</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>laseniors1share</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lawhite1</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lawhite1share</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lablack1</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lablack1share</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>laasian1</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>laasian1share</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lanhopi1</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lanhopi1share</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>laaian1</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>laaian1share</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>laomultir1</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>laomultir1share</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lahisp1</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lahisp1share</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lahunv1</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lahunv1share</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lasnap1</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lasnap1share</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lanhopi10</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lanhopi10share</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>laaian10</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>laaian10share</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>laomultir10</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>laomultir10share</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lablack20</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>lablack20share</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>TractLOWI</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>TractKids</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>TractSeniors</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>TractWhite</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>TractBlack</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>TractAsian</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>TractNHOPI</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>TractAIAN</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>TractOMultir</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>TractHispanic</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>TractHUNV</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>TractSNAP</th>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div><br><label><b>dtype:</b> object</label>




```python
food_access.describe().T

```





  <div id="df-59cd8185-37fd-446f-add2-d120ffe24f0b" class="colab-df-container">
    <div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>count</th>
      <th>mean</th>
      <th>std</th>
      <th>min</th>
      <th>25%</th>
      <th>50%</th>
      <th>75%</th>
      <th>max</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>CensusTract</th>
      <td>72531.0</td>
      <td>2.782573e+10</td>
      <td>1.581647e+10</td>
      <td>1.001020e+09</td>
      <td>1.212708e+10</td>
      <td>2.712979e+10</td>
      <td>4.103900e+10</td>
      <td>5.604595e+10</td>
    </tr>
    <tr>
      <th>Urban</th>
      <td>72531.0</td>
      <td>7.606265e-01</td>
      <td>4.267040e-01</td>
      <td>0.000000e+00</td>
      <td>1.000000e+00</td>
      <td>1.000000e+00</td>
      <td>1.000000e+00</td>
      <td>1.000000e+00</td>
    </tr>
    <tr>
      <th>Pop2010</th>
      <td>72531.0</td>
      <td>4.256739e+03</td>
      <td>1.955988e+03</td>
      <td>1.000000e+00</td>
      <td>2.899000e+03</td>
      <td>4.011000e+03</td>
      <td>5.330500e+03</td>
      <td>3.745200e+04</td>
    </tr>
    <tr>
      <th>OHU2010</th>
      <td>72531.0</td>
      <td>1.609192e+03</td>
      <td>7.256760e+02</td>
      <td>0.000000e+00</td>
      <td>1.108000e+03</td>
      <td>1.525000e+03</td>
      <td>2.021000e+03</td>
      <td>1.604300e+04</td>
    </tr>
    <tr>
      <th>GroupQuartersFlag</th>
      <td>72531.0</td>
      <td>7.114199e-03</td>
      <td>8.404573e-02</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e+00</td>
    </tr>
    <tr>
      <th>NUMGQTRS</th>
      <td>72506.0</td>
      <td>1.101215e+02</td>
      <td>4.439318e+02</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>7.000000e+00</td>
      <td>6.400000e+01</td>
      <td>1.949600e+04</td>
    </tr>
    <tr>
      <th>PCTGQTRS</th>
      <td>72506.0</td>
      <td>2.708677e+00</td>
      <td>9.570875e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>1.800000e-01</td>
      <td>1.570000e+00</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>LILATracts_1And10</th>
      <td>72531.0</td>
      <td>1.281245e-01</td>
      <td>3.342307e-01</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e+00</td>
    </tr>
    <tr>
      <th>LILATracts_halfAnd10</th>
      <td>72531.0</td>
      <td>2.791496e-01</td>
      <td>4.485843e-01</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e+00</td>
      <td>1.000000e+00</td>
    </tr>
    <tr>
      <th>LILATracts_1And20</th>
      <td>72531.0</td>
      <td>1.122279e-01</td>
      <td>3.156488e-01</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e+00</td>
    </tr>
    <tr>
      <th>LILATracts_Vehicle</th>
      <td>72531.0</td>
      <td>1.396093e-01</td>
      <td>3.465836e-01</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e+00</td>
    </tr>
    <tr>
      <th>HUNVFlag</th>
      <td>72531.0</td>
      <td>2.108202e-01</td>
      <td>4.078938e-01</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e+00</td>
    </tr>
    <tr>
      <th>LowIncomeTracts</th>
      <td>72531.0</td>
      <td>4.175732e-01</td>
      <td>4.931624e-01</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e+00</td>
      <td>1.000000e+00</td>
    </tr>
    <tr>
      <th>PovertyRate</th>
      <td>72528.0</td>
      <td>1.518386e+01</td>
      <td>1.191990e+01</td>
      <td>0.000000e+00</td>
      <td>6.500000e+00</td>
      <td>1.200000e+01</td>
      <td>2.060000e+01</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>MedianFamilyIncome</th>
      <td>71783.0</td>
      <td>7.703779e+04</td>
      <td>3.754445e+04</td>
      <td>2.499000e+03</td>
      <td>5.148400e+04</td>
      <td>6.882100e+04</td>
      <td>9.386850e+04</td>
      <td>2.500010e+05</td>
    </tr>
    <tr>
      <th>LA1and10</th>
      <td>72531.0</td>
      <td>3.798100e-01</td>
      <td>4.853428e-01</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e+00</td>
      <td>1.000000e+00</td>
    </tr>
    <tr>
      <th>LAhalfand10</th>
      <td>72531.0</td>
      <td>6.827563e-01</td>
      <td>4.654064e-01</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e+00</td>
      <td>1.000000e+00</td>
      <td>1.000000e+00</td>
    </tr>
    <tr>
      <th>LA1and20</th>
      <td>72531.0</td>
      <td>3.406681e-01</td>
      <td>4.739372e-01</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e+00</td>
      <td>1.000000e+00</td>
    </tr>
    <tr>
      <th>LATracts_half</th>
      <td>72531.0</td>
      <td>6.388303e-01</td>
      <td>4.803429e-01</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e+00</td>
      <td>1.000000e+00</td>
      <td>1.000000e+00</td>
    </tr>
    <tr>
      <th>LATracts1</th>
      <td>72531.0</td>
      <td>3.358840e-01</td>
      <td>4.723018e-01</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e+00</td>
      <td>1.000000e+00</td>
    </tr>
    <tr>
      <th>LATracts10</th>
      <td>72531.0</td>
      <td>4.392605e-02</td>
      <td>2.049320e-01</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e+00</td>
    </tr>
    <tr>
      <th>LATracts20</th>
      <td>72531.0</td>
      <td>4.784161e-03</td>
      <td>6.900245e-02</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e+00</td>
    </tr>
    <tr>
      <th>LATractsVehicle_20</th>
      <td>72531.0</td>
      <td>2.147496e-01</td>
      <td>4.106513e-01</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e+00</td>
    </tr>
    <tr>
      <th>LAPOP05_10</th>
      <td>57991.0</td>
      <td>2.657207e+03</td>
      <td>2.044331e+03</td>
      <td>0.000000e+00</td>
      <td>1.083000e+03</td>
      <td>2.387000e+03</td>
      <td>3.827000e+03</td>
      <td>3.258200e+04</td>
    </tr>
    <tr>
      <th>LALOWI05_10</th>
      <td>57991.0</td>
      <td>7.974882e+02</td>
      <td>7.714326e+02</td>
      <td>0.000000e+00</td>
      <td>2.370000e+02</td>
      <td>5.840000e+02</td>
      <td>1.128500e+03</td>
      <td>9.874000e+03</td>
    </tr>
    <tr>
      <th>lapophalf</th>
      <td>67963.0</td>
      <td>3.166062e+03</td>
      <td>2.003571e+03</td>
      <td>0.000000e+00</td>
      <td>1.756000e+03</td>
      <td>2.926000e+03</td>
      <td>4.299000e+03</td>
      <td>3.745200e+04</td>
    </tr>
    <tr>
      <th>lapophalfshare</th>
      <td>67963.0</td>
      <td>7.342577e+01</td>
      <td>2.906663e+01</td>
      <td>0.000000e+00</td>
      <td>5.563000e+01</td>
      <td>8.350000e+01</td>
      <td>9.980000e+01</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>lalowihalf</th>
      <td>67963.0</td>
      <td>9.551535e+02</td>
      <td>7.902997e+02</td>
      <td>0.000000e+00</td>
      <td>3.800000e+02</td>
      <td>7.690000e+02</td>
      <td>1.329000e+03</td>
      <td>1.960200e+04</td>
    </tr>
    <tr>
      <th>lalowihalfshare</th>
      <td>67963.0</td>
      <td>2.309522e+01</td>
      <td>1.650275e+01</td>
      <td>0.000000e+00</td>
      <td>1.016000e+01</td>
      <td>1.999000e+01</td>
      <td>3.291000e+01</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>lakidshalf</th>
      <td>67963.0</td>
      <td>7.706095e+02</td>
      <td>5.825632e+02</td>
      <td>0.000000e+00</td>
      <td>3.690000e+02</td>
      <td>6.730000e+02</td>
      <td>1.048000e+03</td>
      <td>9.084000e+03</td>
    </tr>
    <tr>
      <th>lakidshalfshare</th>
      <td>67963.0</td>
      <td>1.739534e+01</td>
      <td>8.473848e+00</td>
      <td>0.000000e+00</td>
      <td>1.155000e+01</td>
      <td>1.864000e+01</td>
      <td>2.341000e+01</td>
      <td>9.080000e+01</td>
    </tr>
    <tr>
      <th>laseniorshalf</th>
      <td>67963.0</td>
      <td>4.229286e+02</td>
      <td>3.282729e+02</td>
      <td>0.000000e+00</td>
      <td>1.950000e+02</td>
      <td>3.730000e+02</td>
      <td>5.860000e+02</td>
      <td>1.526100e+04</td>
    </tr>
    <tr>
      <th>laseniorshalfshare</th>
      <td>67963.0</td>
      <td>1.032569e+01</td>
      <td>7.330619e+00</td>
      <td>0.000000e+00</td>
      <td>5.290000e+00</td>
      <td>9.770000e+00</td>
      <td>1.408000e+01</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>lawhitehalf</th>
      <td>67963.0</td>
      <td>2.428491e+03</td>
      <td>1.772177e+03</td>
      <td>0.000000e+00</td>
      <td>1.071000e+03</td>
      <td>2.193000e+03</td>
      <td>3.476000e+03</td>
      <td>2.847700e+04</td>
    </tr>
    <tr>
      <th>lawhitehalfshare</th>
      <td>67963.0</td>
      <td>5.606022e+01</td>
      <td>3.034449e+01</td>
      <td>0.000000e+00</td>
      <td>3.143000e+01</td>
      <td>6.055000e+01</td>
      <td>8.292000e+01</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>lablackhalf</th>
      <td>67963.0</td>
      <td>3.609503e+02</td>
      <td>6.872588e+02</td>
      <td>0.000000e+00</td>
      <td>2.200000e+01</td>
      <td>8.400000e+01</td>
      <td>3.550000e+02</td>
      <td>1.359400e+04</td>
    </tr>
    <tr>
      <th>lablackhalfshare</th>
      <td>67963.0</td>
      <td>9.064957e+00</td>
      <td>1.686603e+01</td>
      <td>0.000000e+00</td>
      <td>5.600000e-01</td>
      <td>2.040000e+00</td>
      <td>8.580000e+00</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>laasianhalf</th>
      <td>67963.0</td>
      <td>1.150718e+02</td>
      <td>2.695013e+02</td>
      <td>0.000000e+00</td>
      <td>1.000000e+01</td>
      <td>3.200000e+01</td>
      <td>1.040000e+02</td>
      <td>6.964000e+03</td>
    </tr>
    <tr>
      <th>laasianhalfshare</th>
      <td>67963.0</td>
      <td>2.398870e+00</td>
      <td>4.930797e+00</td>
      <td>0.000000e+00</td>
      <td>2.800000e-01</td>
      <td>8.100000e-01</td>
      <td>2.340000e+00</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>lanhopihalf</th>
      <td>67963.0</td>
      <td>4.783117e+00</td>
      <td>3.392504e+01</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e+00</td>
      <td>3.000000e+00</td>
      <td>2.786000e+03</td>
    </tr>
    <tr>
      <th>lanhopihalfshare</th>
      <td>67963.0</td>
      <td>1.048703e-01</td>
      <td>7.763883e-01</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>2.000000e-02</td>
      <td>7.000000e-02</td>
      <td>8.588000e+01</td>
    </tr>
    <tr>
      <th>laaianhalf</th>
      <td>67963.0</td>
      <td>3.148485e+01</td>
      <td>1.733569e+02</td>
      <td>0.000000e+00</td>
      <td>4.000000e+00</td>
      <td>1.000000e+01</td>
      <td>2.200000e+01</td>
      <td>8.507000e+03</td>
    </tr>
    <tr>
      <th>laaianhalfshare</th>
      <td>67963.0</td>
      <td>8.068372e-01</td>
      <td>4.574504e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e-01</td>
      <td>2.500000e-01</td>
      <td>5.200000e-01</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>laomultirhalf</th>
      <td>67963.0</td>
      <td>2.252953e+02</td>
      <td>3.315764e+02</td>
      <td>0.000000e+00</td>
      <td>5.100000e+01</td>
      <td>1.120000e+02</td>
      <td>2.560000e+02</td>
      <td>6.415000e+03</td>
    </tr>
    <tr>
      <th>laomultirhalfshare</th>
      <td>67963.0</td>
      <td>4.989980e+00</td>
      <td>6.172080e+00</td>
      <td>0.000000e+00</td>
      <td>1.450000e+00</td>
      <td>2.780000e+00</td>
      <td>5.930000e+00</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>lahisphalf</th>
      <td>67963.0</td>
      <td>4.010741e+02</td>
      <td>7.420223e+02</td>
      <td>0.000000e+00</td>
      <td>5.200000e+01</td>
      <td>1.390000e+02</td>
      <td>4.000000e+02</td>
      <td>1.280500e+04</td>
    </tr>
    <tr>
      <th>lahisphalfshare</th>
      <td>67963.0</td>
      <td>8.631819e+00</td>
      <td>1.341175e+01</td>
      <td>0.000000e+00</td>
      <td>1.470000e+00</td>
      <td>3.460000e+00</td>
      <td>9.370000e+00</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>lahunvhalf</th>
      <td>67963.0</td>
      <td>6.949122e+01</td>
      <td>8.066776e+01</td>
      <td>0.000000e+00</td>
      <td>1.800000e+01</td>
      <td>4.500000e+01</td>
      <td>9.200000e+01</td>
      <td>1.803000e+03</td>
    </tr>
    <tr>
      <th>lahunvhalfshare</th>
      <td>67969.0</td>
      <td>4.684649e+00</td>
      <td>6.011297e+00</td>
      <td>0.000000e+00</td>
      <td>1.250000e+00</td>
      <td>2.910000e+00</td>
      <td>5.800000e+00</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>lasnaphalf</th>
      <td>67963.0</td>
      <td>1.354911e+02</td>
      <td>1.359067e+02</td>
      <td>0.000000e+00</td>
      <td>3.500000e+01</td>
      <td>9.500000e+01</td>
      <td>1.930000e+02</td>
      <td>1.582000e+03</td>
    </tr>
    <tr>
      <th>lasnaphalfshare</th>
      <td>67969.0</td>
      <td>8.934348e+00</td>
      <td>9.072652e+00</td>
      <td>0.000000e+00</td>
      <td>2.460000e+00</td>
      <td>6.260000e+00</td>
      <td>1.247000e+01</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>lapop1</th>
      <td>52542.0</td>
      <td>2.337676e+03</td>
      <td>1.980761e+03</td>
      <td>0.000000e+00</td>
      <td>6.650000e+02</td>
      <td>2.003000e+03</td>
      <td>3.540000e+03</td>
      <td>3.706100e+04</td>
    </tr>
    <tr>
      <th>lapop1share</th>
      <td>52542.0</td>
      <td>5.408174e+01</td>
      <td>3.676091e+01</td>
      <td>0.000000e+00</td>
      <td>1.789250e+01</td>
      <td>5.521500e+01</td>
      <td>9.407000e+01</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>lalowi1</th>
      <td>52542.0</td>
      <td>6.697111e+02</td>
      <td>7.065588e+02</td>
      <td>0.000000e+00</td>
      <td>1.320000e+02</td>
      <td>4.640000e+02</td>
      <td>9.870000e+02</td>
      <td>1.939700e+04</td>
    </tr>
    <tr>
      <th>lalowi1share</th>
      <td>52542.0</td>
      <td>1.614957e+01</td>
      <td>1.547986e+01</td>
      <td>0.000000e+00</td>
      <td>3.310000e+00</td>
      <td>1.171000e+01</td>
      <td>2.526000e+01</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>lakids1</th>
      <td>52542.0</td>
      <td>5.697495e+02</td>
      <td>5.411679e+02</td>
      <td>0.000000e+00</td>
      <td>1.370000e+02</td>
      <td>4.560000e+02</td>
      <td>8.460000e+02</td>
      <td>8.907000e+03</td>
    </tr>
    <tr>
      <th>lakids1share</th>
      <td>52542.0</td>
      <td>1.281045e+01</td>
      <td>9.479667e+00</td>
      <td>0.000000e+00</td>
      <td>3.720000e+00</td>
      <td>1.248000e+01</td>
      <td>2.099000e+01</td>
      <td>9.080000e+01</td>
    </tr>
    <tr>
      <th>laseniors1</th>
      <td>52542.0</td>
      <td>3.192987e+02</td>
      <td>3.043053e+02</td>
      <td>0.000000e+00</td>
      <td>7.400000e+01</td>
      <td>2.590000e+02</td>
      <td>4.840000e+02</td>
      <td>1.034900e+04</td>
    </tr>
    <tr>
      <th>laseniors1share</th>
      <td>52542.0</td>
      <td>7.826267e+00</td>
      <td>7.189503e+00</td>
      <td>0.000000e+00</td>
      <td>1.880000e+00</td>
      <td>6.550000e+00</td>
      <td>1.223000e+01</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>lawhite1</th>
      <td>52542.0</td>
      <td>1.904910e+03</td>
      <td>1.730447e+03</td>
      <td>0.000000e+00</td>
      <td>4.050000e+02</td>
      <td>1.545000e+03</td>
      <td>2.969000e+03</td>
      <td>2.816500e+04</td>
    </tr>
    <tr>
      <th>lawhite1share</th>
      <td>52542.0</td>
      <td>4.408477e+01</td>
      <td>3.382531e+01</td>
      <td>0.000000e+00</td>
      <td>1.082000e+01</td>
      <td>4.072000e+01</td>
      <td>7.586750e+01</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>lablack1</th>
      <td>52542.0</td>
      <td>2.184719e+02</td>
      <td>5.148742e+02</td>
      <td>0.000000e+00</td>
      <td>7.000000e+00</td>
      <td>3.100000e+01</td>
      <td>1.610000e+02</td>
      <td>1.211200e+04</td>
    </tr>
    <tr>
      <th>lablack1share</th>
      <td>52542.0</td>
      <td>5.243149e+00</td>
      <td>1.209222e+01</td>
      <td>0.000000e+00</td>
      <td>1.900000e-01</td>
      <td>7.500000e-01</td>
      <td>3.780000e+00</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>laasian1</th>
      <td>52542.0</td>
      <td>5.790859e+01</td>
      <td>1.630448e+02</td>
      <td>0.000000e+00</td>
      <td>4.000000e+00</td>
      <td>1.400000e+01</td>
      <td>4.600000e+01</td>
      <td>5.809000e+03</td>
    </tr>
    <tr>
      <th>laasian1share</th>
      <td>52542.0</td>
      <td>1.172348e+00</td>
      <td>2.947656e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e-01</td>
      <td>3.500000e-01</td>
      <td>1.030000e+00</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>lanhopi1</th>
      <td>52542.0</td>
      <td>2.883312e+00</td>
      <td>2.761867e+01</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e+00</td>
      <td>2.164000e+03</td>
    </tr>
    <tr>
      <th>lanhopi1share</th>
      <td>52542.0</td>
      <td>6.370675e-02</td>
      <td>6.877782e-01</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>3.000000e-02</td>
      <td>8.588000e+01</td>
    </tr>
    <tr>
      <th>laaian1</th>
      <td>52542.0</td>
      <td>2.730113e+01</td>
      <td>1.824670e+02</td>
      <td>0.000000e+00</td>
      <td>1.000000e+00</td>
      <td>6.000000e+00</td>
      <td>1.500000e+01</td>
      <td>8.444000e+03</td>
    </tr>
    <tr>
      <th>laaian1share</th>
      <td>52542.0</td>
      <td>7.246991e-01</td>
      <td>4.889572e+00</td>
      <td>0.000000e+00</td>
      <td>3.000000e-02</td>
      <td>1.400000e-01</td>
      <td>3.500000e-01</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>laomultir1</th>
      <td>52542.0</td>
      <td>1.262016e+02</td>
      <td>2.304373e+02</td>
      <td>0.000000e+00</td>
      <td>1.900000e+01</td>
      <td>5.600000e+01</td>
      <td>1.350000e+02</td>
      <td>6.146000e+03</td>
    </tr>
    <tr>
      <th>laomultir1share</th>
      <td>52542.0</td>
      <td>2.793007e+00</td>
      <td>4.390135e+00</td>
      <td>0.000000e+00</td>
      <td>5.500000e-01</td>
      <td>1.410000e+00</td>
      <td>3.080000e+00</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>lahisp1</th>
      <td>52542.0</td>
      <td>2.158501e+02</td>
      <td>5.165200e+02</td>
      <td>0.000000e+00</td>
      <td>2.000000e+01</td>
      <td>6.300000e+01</td>
      <td>1.820000e+02</td>
      <td>1.150200e+04</td>
    </tr>
    <tr>
      <th>lahisp1share</th>
      <td>52542.0</td>
      <td>4.630486e+00</td>
      <td>9.393900e+00</td>
      <td>0.000000e+00</td>
      <td>5.700000e-01</td>
      <td>1.560000e+00</td>
      <td>4.170000e+00</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>lahunv1</th>
      <td>52542.0</td>
      <td>3.959687e+01</td>
      <td>5.531531e+01</td>
      <td>0.000000e+00</td>
      <td>5.000000e+00</td>
      <td>2.200000e+01</td>
      <td>5.400000e+01</td>
      <td>1.794000e+03</td>
    </tr>
    <tr>
      <th>lahunv1share</th>
      <td>52565.0</td>
      <td>2.631525e+00</td>
      <td>4.072878e+00</td>
      <td>0.000000e+00</td>
      <td>3.200000e-01</td>
      <td>1.400000e+00</td>
      <td>3.400000e+00</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>lasnap1</th>
      <td>52542.0</td>
      <td>9.252000e+01</td>
      <td>1.114904e+02</td>
      <td>0.000000e+00</td>
      <td>1.200000e+01</td>
      <td>5.300000e+01</td>
      <td>1.340000e+02</td>
      <td>1.582000e+03</td>
    </tr>
    <tr>
      <th>lasnap1share</th>
      <td>52565.0</td>
      <td>5.995943e+00</td>
      <td>7.311362e+00</td>
      <td>0.000000e+00</td>
      <td>7.900000e-01</td>
      <td>3.430000e+00</td>
      <td>8.660000e+00</td>
      <td>1.000000e+02</td>
    </tr>
    <tr>
      <th>lanhopi10</th>
      <td>7766.0</td>
      <td>5.217615e-01</td>
      <td>5.977160e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>2.660000e+02</td>
    </tr>
    <tr>
      <th>lanhopi10share</th>
      <td>7766.0</td>
      <td>2.681303e-02</td>
      <td>9.879220e-01</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>8.588000e+01</td>
    </tr>
    <tr>
      <th>laaian10</th>
      <td>7766.0</td>
      <td>3.842635e+01</td>
      <td>2.842162e+02</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e+00</td>
      <td>6.000000e+00</td>
      <td>6.947000e+03</td>
    </tr>
    <tr>
      <th>laaian10share</th>
      <td>7766.0</td>
      <td>1.250255e+00</td>
      <td>8.045275e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>2.000000e-02</td>
      <td>1.800000e-01</td>
      <td>9.934000e+01</td>
    </tr>
    <tr>
      <th>laomultir10</th>
      <td>7766.0</td>
      <td>3.029140e+01</td>
      <td>9.463877e+01</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>6.000000e+00</td>
      <td>2.400000e+01</td>
      <td>1.724000e+03</td>
    </tr>
    <tr>
      <th>laomultir10share</th>
      <td>7766.0</td>
      <td>9.715606e-01</td>
      <td>2.712061e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e-02</td>
      <td>1.800000e-01</td>
      <td>7.600000e-01</td>
      <td>4.545000e+01</td>
    </tr>
    <tr>
      <th>lablack20</th>
      <td>1506.0</td>
      <td>3.717131e+00</td>
      <td>3.388650e+01</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e+00</td>
      <td>1.086000e+03</td>
    </tr>
    <tr>
      <th>lablack20share</th>
      <td>1506.0</td>
      <td>1.386122e-01</td>
      <td>8.979877e-01</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>2.000000e-02</td>
      <td>2.041000e+01</td>
    </tr>
    <tr>
      <th>TractLOWI</th>
      <td>72527.0</td>
      <td>1.385054e+03</td>
      <td>9.837094e+02</td>
      <td>0.000000e+00</td>
      <td>6.800000e+02</td>
      <td>1.164000e+03</td>
      <td>1.846000e+03</td>
      <td>1.256200e+04</td>
    </tr>
    <tr>
      <th>TractKids</th>
      <td>72527.0</td>
      <td>1.022695e+03</td>
      <td>6.154460e+02</td>
      <td>0.000000e+00</td>
      <td>6.110000e+02</td>
      <td>9.240000e+02</td>
      <td>1.312000e+03</td>
      <td>1.184500e+04</td>
    </tr>
    <tr>
      <th>TractSeniors</th>
      <td>72527.0</td>
      <td>5.551971e+02</td>
      <td>3.518054e+02</td>
      <td>0.000000e+00</td>
      <td>3.200000e+02</td>
      <td>4.970000e+02</td>
      <td>7.180000e+02</td>
      <td>1.727100e+04</td>
    </tr>
    <tr>
      <th>TractWhite</th>
      <td>72527.0</td>
      <td>3.082337e+03</td>
      <td>1.796365e+03</td>
      <td>0.000000e+00</td>
      <td>1.848000e+03</td>
      <td>2.914000e+03</td>
      <td>4.118000e+03</td>
      <td>2.898300e+04</td>
    </tr>
    <tr>
      <th>TractBlack</th>
      <td>72527.0</td>
      <td>5.367562e+02</td>
      <td>8.891181e+02</td>
      <td>0.000000e+00</td>
      <td>4.300000e+01</td>
      <td>1.600000e+02</td>
      <td>6.100000e+02</td>
      <td>1.680400e+04</td>
    </tr>
    <tr>
      <th>TractAsian</th>
      <td>72527.0</td>
      <td>2.023277e+02</td>
      <td>4.358783e+02</td>
      <td>0.000000e+00</td>
      <td>1.700000e+01</td>
      <td>5.800000e+01</td>
      <td>1.890000e+02</td>
      <td>1.048500e+04</td>
    </tr>
    <tr>
      <th>TractNHOPI</th>
      <td>72527.0</td>
      <td>7.445655e+00</td>
      <td>4.518658e+01</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e+00</td>
      <td>5.000000e+00</td>
      <td>3.491000e+03</td>
    </tr>
    <tr>
      <th>TractAIAN</th>
      <td>72527.0</td>
      <td>4.015232e+01</td>
      <td>1.773787e+02</td>
      <td>0.000000e+00</td>
      <td>7.000000e+00</td>
      <td>1.500000e+01</td>
      <td>3.300000e+01</td>
      <td>9.009000e+03</td>
    </tr>
    <tr>
      <th>TractOMultir</th>
      <td>72527.0</td>
      <td>3.876646e+02</td>
      <td>5.293497e+02</td>
      <td>0.000000e+00</td>
      <td>8.500000e+01</td>
      <td>1.860000e+02</td>
      <td>4.480000e+02</td>
      <td>8.839000e+03</td>
    </tr>
    <tr>
      <th>TractHispanic</th>
      <td>72527.0</td>
      <td>6.959793e+02</td>
      <td>1.119473e+03</td>
      <td>0.000000e+00</td>
      <td>8.800000e+01</td>
      <td>2.430000e+02</td>
      <td>7.510000e+02</td>
      <td>1.542000e+04</td>
    </tr>
    <tr>
      <th>TractHUNV</th>
      <td>72527.0</td>
      <td>1.437097e+02</td>
      <td>2.327389e+02</td>
      <td>0.000000e+00</td>
      <td>3.600000e+01</td>
      <td>8.200000e+01</td>
      <td>1.685000e+02</td>
      <td>6.059000e+03</td>
    </tr>
    <tr>
      <th>TractSNAP</th>
      <td>72527.0</td>
      <td>2.017532e+02</td>
      <td>1.857601e+02</td>
      <td>0.000000e+00</td>
      <td>6.700000e+01</td>
      <td>1.520000e+02</td>
      <td>2.820000e+02</td>
      <td>2.175000e+03</td>
    </tr>
  </tbody>
</table>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-59cd8185-37fd-446f-add2-d120ffe24f0b')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  
    </button>

  

    
  </div>


<div id="df-e5afa771-c1ba-4a33-a7c3-599dcedb3570">
  <button class="colab-df-quickchart" onclick="quickchart('df-e5afa771-c1ba-4a33-a7c3-599dcedb3570')"
            title="Suggest charts"
            style="display:none;">


  </button>



  
</div>

    </div>
  </div>




**Observations of Descriptive Statistics**

**What are the minimum and maximum values?**

The minimum population is 1, and the maximum is 37,452.  
The minimum poverty rate is 0%, and the maximum is 100%.  
The minimum median family income is 2,499, while the maximum $250,001.  
The minimum Black population is 0, and the maximum is 16,804.



**Are the mean and median values close to each other? If so this could indicate a normal distribution of the data. If not, this could indicate skewness in the data.
If the mean is smaller than the median the values are likely skewed left, toward the minimum value. If the mean is larger than the median then there is skewness to the right indicating more high values in the data distribution.**
- The mean is higher than the median for all the columns, which means the data is skewed to the right. This suggests there are some higher values pulling the average up.







# **Commit #5**


```python
import seaborn as sns
import matplotlib.pyplot as plt

# Create a working subset
food_access_selected = food_access[[
    "Pop2010", "TractBlack", "TractWhite", "TractSNAP", "TractHUNV", "LILATracts_1And10"
]].copy()

# Calculate racial percentages
food_access_selected["PctBlack"] = (food_access_selected["TractBlack"] / food_access_selected["Pop2010"]) * 100
food_access_selected["PctWhite"] = (food_access_selected["TractWhite"] / food_access_selected["Pop2010"]) * 100

# Create a binary column for Food Desert status
food_access_selected["FoodDesert"] = food_access_selected["LILATracts_1And10"] > 0

# Create a boxplot: % Black by Food Desert status
plt.figure(figsize=(8, 6))
sns.boxplot(data=food_access_selected, x="FoodDesert", y="PctBlack", palette={True: "#D55E00", False: "#0072B2"})
plt.xticks([0, 1], ["Non-Food Desert", "Food Desert"])
plt.xlabel("Census Tract Type")
plt.ylabel("Percentage Black Population")
plt.title("Are Food Deserts More Common in Predominantly Black Communities?")
plt.tight_layout()
plt.show()




```


    
![png](download%20(9).png)
    



```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

selected_columns = ['TractBlack', 'TractSNAP']

# Create the scatter plot with a regression line
plt.figure(figsize=(8, 6))
sns.regplot(x='TractBlack', y='TractSNAP', data=food_access, scatter_kws={'s': 50}, line_kws={'color': 'red'})
plt.title('Correlation between Black Population and Food Assistance Usage')
plt.xlabel('Black Population (TractBlack)')
plt.ylabel('Food Assistance Usage (TractSNAP)')
plt.show()

```


    
![png](download%20(10).png)
    


The scatter plot displays the relationship between the use of food assistance programs (represented by TractSNAP) and the percentage of the Black population (represented by TractBlack) in various census tracts.


```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load dataset
df = food_access[["Pop2010", "TractBlack", "LILATracts_1And10"]].copy()

# Calculate percentage Black population
df["PctBlack"] = (df["TractBlack"] / df["Pop2010"]) * 100

# Create Food Desert classification
df["FoodDesert"] = df["LILATracts_1And10"] > 0

# Boxplot for Income vs. Food Desert Status
sns.boxplot(x=df["FoodDesert"], y=df["Pop2010"], palette="coolwarm")
plt.xticks([0, 1], ["Non-Food Desert", "Food Desert"])
plt.ylabel("Population (Proxy for Income)")
plt.xlabel("Food Desert Status")
plt.title("Income Distribution in Food Deserts vs. Non-Food Deserts")
plt.yscale("log")
plt.show()

# Boxplot for % Black Population vs. Food Desert Status
sns.boxplot(x=df["FoodDesert"], y=df["PctBlack"], palette="coolwarm")
plt.xticks([0, 1], ["Non-Food Desert", "Food Desert"])
plt.ylabel("Percentage Black Population")
plt.xlabel("Food Desert Status")
plt.title("Racial Composition in Food Deserts vs. Non-Food Deserts")
plt.show()

```


    
![png](download%20(11).png)
    



    
![png](download%20(12).png)
    



```python
import matplotlib.pyplot as plt
import seaborn as sns
import pandas as pd

# Sample data: summary stats from your previous analysis
categories = [
    "Food Desert (1 & 10 miles)",
    "Food Desert (1 & 20 miles)",
    "Avg. SNAP Households",
    "Avg. Households Without Vehicles"
]

# Average values for each group
black = [0.276, 0.260, 359.05, 281.07]        # Predominantly Black communities
non_black = [0.114, 0.098, 186.76, 130.61]    # Other communities

# Bar chart setup
x = range(len(categories))
plt.figure(figsize=(12, 6))
plt.bar(x, black, width=0.4, label="Predominantly Black", color="#4C72B0")
plt.bar([i + 0.4 for i in x], non_black, width=0.4, label="Other Communities", color="#DD8452")

# Axis and title formatting
plt.xticks([i + 0.2 for i in x], categories, rotation=30, ha="right")
plt.ylabel("Average per Census Tract")
plt.title("Do Predominantly Black Communities Face Greater Barriers to Food Access?")
plt.legend(title="Community Type")
plt.tight_layout()


plt.show()

```


    
![png](download%20(13).png)
    



```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load your dataset
df = food_access

# Calculate % Black
df["PctBlack"] = (df["TractBlack"] / df["Pop2010"]) * 100

# Define food deserts
df["FoodDesert"] = df["LILATracts_1And10"] > 0

# Filter out missing or invalid values
df_filtered = df[(df["Pop2010"] > 0) & (df["PctBlack"].notnull())]

# Group by food desert status and calculate average % Black
avg_pct_black = df_filtered.groupby("FoodDesert")["PctBlack"].mean().reset_index()
avg_pct_black["Census Tract Type"] = avg_pct_black["FoodDesert"].replace({
    True: "Food Desert",
    False: "Non-Food Desert"
})

# Plot
plt.figure(figsize=(8, 6))
sns.barplot(data=avg_pct_black, x="Census Tract Type", y="PctBlack", palette=["#0072B2", "#D55E00"])

# Add formatting
plt.title("Average % Black Population in Food Desert vs Non-Food Desert Areas")
plt.xlabel("Census Tract Type")
plt.ylabel("Average % Black Population")
plt.tight_layout()
plt.show()

```


    
![png](download%20(14).png)
    



---

## Observations and Results

- States with higher percentages of seniors and SNAP participants often have limited transportation access.
- A join of related food access tables showed demographic and geographic disparities in SNAP usage.
- Conditional logic highlighted specific tracts in danger of poor access due to lack of household vehicles.
- Data visualizations helped expose trends in food insecurity and senior vulnerability.

---

## Recommendations

- Enhance community food assistance programs in states with high SNAP and elderly populations.
- Improve transportation infrastructure or delivery support for areas with low vehicle access.
- Use tract-level data to prioritize outreach and interventions.

---

## Conclusion

The disparities shown in this analysis emphasize the urgent need for data-driven decision-making in food justice. Combining open data, public health priorities, and equity-focused visualizations helps shape stronger policies that ensure every community has access to nutritious food.

