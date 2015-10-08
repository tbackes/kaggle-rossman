Data notes:

Store data:

- `Store`, `StoreType`, `Assortment`, `Promo2` are populated for all 1115 stores

| `StoreType` | #   | %  |
|-------------|-----|----|
| `'a'`       | 602 | 54 |
| `'b'`       | 17  | 2  |
| `'c'`       | 148 | 13 |
| `'d'`       | 348 | 31 |

- `CompetitionDistance` is only missing for 3 stores (0.3%). Instead of assigning to 0, maybe assign to the mean for others with the same `StoreType`, `Assortment`, `Promo2`?

- `CompetitionOpenSince` `Month`/`Year` are only populated for 761 stores (68%). This is lower priority to backfill. Andy's code uses these to calculate a 'months since open' field, and missing values are set to 0. I think that's fine for now.

- `Promo2` is a boolean. Only 571 stores have `Promo2 == 1` (51%). These stores are the only ones with values in `Promo2SinceWeek`, `Promo2SinceYear`, `PromoInterval`.

	* `PromoInterval` is a string with 3 unique values: `'Jan,Apr,Jul,Oct'`, `'Feb,May,Aug,Nov'`, and `'Mar,Jun,Sep,Dec'`. Andy used `PromoInterval` to generate **12** dummy variables p_1_Jan, through p_4_Dec. However, since there are only 3 possible combinations of months we can drop this down to only **3** dummy variables.



TO DO: 

- Figure out good solution for backfilling `CompetitionDistance`

- 