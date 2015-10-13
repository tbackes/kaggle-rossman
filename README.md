# kaggle-rossman
Submission for the Rossman Kaggle Competition

## 10/13/2015:
### Convert School Holiday to State

Use dates from this website to map between school holiday group and German State:

http://www.holidays-info.com/School-Holidays-Germany/2014/school-holidays_2014.html

| **Id** | **State**            |   | **Id** | **State**         |   | **Id** | **State**               |
|--------|-----------------------|---|--------|--------------------|---|--------|----------------------|
| 0      | Hesse                 |   | 5      | Schleswig Holstein |   | 9      | Rhineland Palatinate |
| 1      | Thuringia             |   | 6      | Bremen             |   | 10     | Saxony Anhalt        |
| 2      | Northrhine Westphalia |   | 6      | Lower Saxony       |   | 11     | Hamburg              |
| 3      | Berlin                |   | 7      | Bavaria\*\*\*         |   |        |                      |
| 4      | Saxony                |   | 8      | Baden Wuerttemberg |   |        |                      |

\*\*\* *Bavaria has exactly 180 stores. All 180 stores that are missing in the second half of 2014 were from Bavaria.*

The following states do not appear to be in the dataset (at least based on School Holidays): Brandenburg, Saarland, Mecklenburg West Pomerania


## 10/08/2015:

Current Progress:

- Basic EDA (EDA folder). I still need to clean up my ipython notebook, but it's uploaded.

- Starting to code up time series models in python (See TimeSeriesForecasting.ipynb)

	* For now working with a subset of the data. These 10 consumers have sales reported for every day in the observation period. (Only 6 of them show up in the test data)

	```[769, 1097, 85, 562, 262, 733, 494, 682, 335, 423]```