Data notes:

## Store EDA

- `Store`, `StoreType`, `Assortment`, `Promo2` are populated for all 1115 stores

| `StoreType` | #   | %  |   | `Assortment` | #   | %  |   | `PromoInterval`      | #   | %  |
|-------------|-----|----|---|--------------|-----|----|---|----------------------|-----|----|
| `'a'`       | 602 | 54 |   | `'a'`        | 593 | 53 |   | `'Jan,Apr,Jul,Oct'`  | 335 | 30 |
| `'b'`       | 17  | 2  |   | `'b'`        | 9   | 1  |   | `'Feb,May,Aug,Nov'`  | 130 | 12 |
| `'c'`       | 148 | 13 |   | `'c'`        | 513 | 46 |   | `'Mar,Jun,Sept,Dec'` | 106 | 10 |
| `'d'`       | 348 | 31 |   |              |     |    |   | Missing              | 544 |    |

	* All 9 stores with `Assortment == 'b'` also have `StoreType = 'b'`.

- `CompetitionDistance` is only missing for 3 stores (0.3%). Instead of assigning to 0, maybe assign to the mean for others with the same `StoreType`, `Assortment`, `Promo2`?

- `CompetitionOpenSince` `Month`/`Year` are only populated for 761 stores (68%). This is lower priority to backfill. Andy's code uses these to calculate a 'months since open' field, and missing values are set to 0. I think that's fine for now.

- `Promo2` is a boolean. Only 571 stores have `Promo2 == 1` (51%). These stores are the only ones with values in `Promo2SinceWeek`, `Promo2SinceYear`, `PromoInterval`.

	* `PromoInterval` is a string with 3 unique values: `'Jan,Apr,Jul,Oct'`, `'Feb,May,Aug,Nov'`, and `'Mar,Jun,Sep,Dec'`. Andy used `PromoInterval` to generate **12** dummy variables p_1_Jan, through p_4_Dec. However, since there are only 3 possible combinations of months we can drop this down to only **3** dummy variables.


## Merged EDA

- Observation range: `2013-01-01` to `2015-07-31`

	* There are 180 (16%) stores thathave no reported records between `2014-07-01` to `2014-12-31`

		- *Note: This means 180 stores only have Aug-Sep sales data from 2013. These are the two months we need to forecast for the test data, so we need to figure out how we want to handle this during modeling-particularly if we try a time-series approach.

	* There is 1 store that is missing the first day (0.09%). Store 988 is not reported on `2013-01-01`. We can treat this like the store was closed.

- Although there are only 9 stores, `Assortment == 'b'` stores exhibit by far the highest average daily sales, and their daily sails grow noticeably over the 2 year observation period. (The other assortments and store types have much smaller growth). The `'b'` stores also have by far the highest avg daily customer counts.

- Stores with closer competitors have higher avg daily sales, and avg daily sales drop off as the distance to the nearest competitor decreases. This makes sense, as stores with close competitors are likely in more urban areas (which is supported by the higher number of avg daily customers also seen at these stores).

- Stores with `Promo2 == 0` consistently have the highest avg daily customers (and highest avg daily sales).

- There are only 33 stores that are ever open on Sundays. Some of these are open pretty much every Sunday, and others are only open a subset of Sundays.

	* *Note: Test days with no actual sales are ignored during kaggle's scoring. Therefore, we may want to predict sales for all days (incl. Sundays) instead of risking predicting zero sales for a day a store was actually open.* 

	* How do we want to handle Sundays? I think we can calculate some weight mapping avg daily sales for a given week to the Sunday sales based on these 33 stores. We can then use these weights to predict Sunday sales for all stores. Is that necessary?

- For more details (and for the raw results/figures, see my ipython notebook `kaggle_rossman-tbackes.ipynb`)


TO DO: 

- Figure out good solution for backfilling `CompetitionDistance`

- Investigate time series analysis. This may dictate how we need to format the data and how we want to backfill days.

I found descriptions of the top two entries from a similar Walmart competition:

- https://www.kaggle.com/c/walmart-recruiting-store-sales-forecasting/forums/t/8125/first-place-entry/56111#post56111

- https://www.kaggle.com/c/walmart-recruiting-store-sales-forecasting/forums/t/8023/thank-you-and-2-rank-model?limit=all

