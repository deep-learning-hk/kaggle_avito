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
- group all text features by a list: textfeats = ["description", "title"]
- create Description Punctuation feature from "description" (by string.punctuation)
- clean the "title" by:
  i. lowercase
  ii. remove some punctuation and signs
- text preprocess:
  - fillna with "missing"
  - lowercase
  - create "num_words" features for both "description" & "title"
  - create "num_unique_words" features for both "description" & "title"
  - create "words_vs_unique" features for both "description" & "title" (unique_words/words)
- TFIDF: (TODO)
  - use russian stopwords
  - ngram: 1, 2
  - max_features (TODO)
- create a text feature df to contain all the tfidf features
- weirdly, it fits all columns (even numeric and categorical features) into TFIDF, [ vectorizer.transform(df.to_dict('records')) ]
- create a list of "get_feature_names" for all TFIDF features
- make Ridge Regression as one of the feature

### Our features

#### Image features
- Image Dullness Score
- Average Pixel Width (check if the image's pixel color is very uniform - i.e. the image is very 'flat')
- Blurness
- Width of the Image
- Height of the Image
- Size of the Image
- Neural Net Object Prediction
- image quality by using: https://github.com/titu1994/neural-image-assessment (not in this notebook)
- Keypoint extraction

#### Previous Deal Probability
- first, get all the previous deal probability, in train set
- get all the mean deal probability from the repeated user in train set for test set (the only once repeated user's deal prob. will discount by 1/2)

#### Pong's features (TODO)
- one ratio and zero ratio
- .....

#### Stratified K-fold
- 5 folds
- stratified by deal prob range:
  ```python
  y_4_bins = pd.cut(y,[-0.01,0.01,0.163, 0.76, 1], labels=['0', '0.01', '0.163', '0.76'], right=True) 
  ```
