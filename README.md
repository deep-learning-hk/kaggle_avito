Kaggle avito
============

Feature Engineering and Procedures
-------------------
### From Public Kernel
- first, take label y out from train set
- combine train set and test set, so we can do all feature engineering at one shot
- price: Log transform
- price: Fill NA with mean value
- image_top_1: fill NA with -999
- create Time Variables:
  - weekday
  - week of year (not so useful)
  - day of month (not so useful)
- get training index and test index based on the date
- Label Encoding for categorical features
  - including: ["user_id","region","city","parent_category_name","category_name","user_type","image_top_1","param_1","param_2","param_3"]
