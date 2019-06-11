Curated by: John Obuch, Fatih Catpinar, and Daniel Larson

## README!
 -	Due to Twitter term restrictions, we are only able to access tweets with a historical cutoff of 7 days. We were able to grow our dataset by calling 7 days’ worth of data across multiple search terms.
 -	You are also required to register a Twitter developer account to get your credentials and put them as specified in cred.txt. (https://apps.twitter.com/)
 -	To access the News API data, you will need to register for an API Key by navigating to (https://newsapi.org)
 -	Due to the Exchange Rate API only displaying same-day rates, we chose to exclude these data from our data set due the API currently limiting the acquisition of historical exchange rate data.
 -	To access the Exchange Rate API, you will need to acquire an API Key at (https://www.exchangerate-api.com/)
 -	After executing the cells below, the `/data` folder will contain Ticker.csv news.csv, twitter.csv, and merged_data.csv files containing separate files of the data we are collecting.
 End user will be able to interact with the notebook by inputting their specified stock ticker, news topics, and twitter key words. The input for the news topics and twitter search terms can either be a single entry, or multiple entries separated by commas.

 __News Data:__ 
 ##### Powered by News API: NewsAPI.org 
 Function: `news_topic(topic)`, topic input is a string 
Description: Creating pandas data frame based on user input to join on other data. 
Size: N rows by 6 columns with page size = 100 with a 100 rows for each topic! To increase sample size, add more topics. (E.g. topic input of 6 entries would produce a dataframe with 600 rows and 6 columns. 
Format: Each line is a JSON dict which consists of news articles: `author, content, description, publishedAt, source` (__Note:__ the `source` keys value is a dictionary `{id, name}`), and `url.` 
Example:
 ```
{'articles': [{'author': 'Alex Cranz', 'content': 'Youve likely heard about the intense conversations ' 'between the United States and China over tariffs. ' 'The US government has been inconsistent, thus far, ' 'on what affects a trade war could have on the ' 'average person, and the stock marketwhich loves ' 'consistencyha… [+1942 chars]', 'description': 'You’ve likely heard about the intense ' 'conversations between the United States and ' 'China over tariffs. The US government has been ' 'inconsistent, thus far, on what affects a trade ' 'war could have on the average person, and the ' 'stock market—which loves consistency…', 'publishedAt': '2019-05-13T20:50:00Z', 'source': {'id': None, 'name': 'Gizmodo.com'}, 'title': "A Looming Chinese Trade War Means Either Apple's " 'Stock Will Drop or iPhone Prices Will Rise', 'url': 'https://gizmodo.com/a-looming-chinese-trade-war-means-either-apples-stock-w-1834729716', 'urlToImage': 'https://i.kinja-img.com/gawker-media/image/upload/s--hL9R82iR--/c_fill,fl_progressive,g_center,h_900,q_80,w_1600/lvsoqy3vgip3k9mn0xxl.jpg'} ,{…}]}
```


 __Stock Data:__ 
 ##### Alpha Vantage 
 File: Ticker.csv depending on user input. 
Description: Converts output from API into a pandas dataframe. 
Size: 100 rows × 10 columns 
Format: csv files contain headers: `Date, Open, High, Low, Close, AdjClose, Volume, dividend_amount, split_coefficient, and Stock` 
Example: 
```
b'timestamp,open,high,low,close,adjusted_close,volume,dividend_amount,split_coefficient\r\n2019-06-07,186.5100,191.9200,185.7700,190.1500,190.1500,30684393,0.0000,1.0000\r\n2019-06-06,183.0800,185.4700,182.1489,185.2200,185.2200,22526311,0.0000,1.0000\r\n2019-06-05,184.2800,184.9900,181.1400,182.5400,182.5400,29773427,0.0000,1.0000\r\n
```
 __Twitter Data:__ 
 ##### Twitter API client from importing the Twython module 
File: train.tweet.json 
Description: outputs dataframe for the keys: `Topic`, `Date`, `User`, `Text` (Topic was a created field). 
Size: N rows × 14 columns. The number of rows is dependent on the number of key words the user enters. We receive 100 tweets per date per topic. __Note:__ The number of twitter responses is determined by the number of tweets avalible for a given topic (i.e. even though our limit is 100, we may receive less depending on the topic chosen). 
Format: JSON `dict_keys(['created_at', 'id', 'id_str', 'text', 'truncated', 'entities', 'metadata', 'source', 'in_reply_to_status_id', 'in_reply_to_status_id_str', 'in_reply_to_user_id', 'in_reply_to_user_id_str', 'in_reply_to_screen_name', 'user', 'geo', 'coordinates', 'place', 'contributors', 'is_quote_status', 'retweet_count', 'favorite_count', 'favorited', 'retweeted', 'possibly_sensitive', 'lang'])` 
Example: 
```
[{'contributors': None,
  'coordinates': None,
  'created_at': 'Sat Jun 08 23:57:54 +0000 2019',
  'entities': {'hashtags': [{'indices': [50, 58], 'text': 'maxpain'},
                            {'indices': [59, 67], 'text': 'options'}],
               'media': [{'display_url': 'pic.twitter.com/QWBqSBoB7H',
                          'expanded_url': 'https://twitter.com/optioncharts/status/1137509083345559552/photo/1',
                          'id': 1137509082435338240,
                          'id_str': '1137509082435338240',
                          'indices': [92, 115],
                          'media_url': 'http://pbs.twimg.com/media/D8k-e9NWwAASuzw.jpg',
                          'media_url_https': 'https://pbs.twimg.com/media/D8k-e9NWwAASuzw.jpg',
                          'sizes': {'large': {'h': 500,
                                              'resize': 'fit',
                                              'w': 1200},
                                    'medium': {'h': 500,
                                               'resize': 'fit',
                                               'w': 1200},
                                    'small': {'h': 283,
                                              'resize': 'fit',
                                              'w': 680},
                                    'thumb': {'h': 150,
                                              'resize': 'crop',
                                              'w': 150}},
                          'type': 'photo',
                          'url': 'https://t.co/QWBqSBoB7H'}],
               'symbols': [{'indices': [0, 5], 'text': 'AAPL'}],
               'urls': [{'display_url': 'maximum-pain.com/options/max-pa…',
                         'expanded_url': 'http://maximum-pain.com/options/max-pain/AAPL',
                         'indices': [68, 91],
                         'url': 'https://t.co/CCUsRwhEoM'}],
               'user_mentions': []},
  'extended_entities': {'media': [{'display_url': 'pic.twitter.com/QWBqSBoB7H',
                                   'expanded_url': 'https://twitter.com/optioncharts/status/1137509083345559552/photo/1',
                                   'id': 1137509082435338240,
                                   'id_str': '1137509082435338240',
                                   'indices': [92, 115],
                                   'media_url': 'http://pbs.twimg.com/media/D8k-e9NWwAASuzw.jpg',
                                   'media_url_https': 'https://pbs.twimg.com/media/D8k-e9NWwAASuzw.jpg',
                                   'sizes': {'large': {'h': 500,
                                                       'resize': 'fit',
                                                       'w': 1200},
                                             'medium': {'h': 500,
                                                        'resize': 'fit',
                                                        'w': 1200},
                                             'small': {'h': 283,
                                                       'resize': 'fit',
                                                       'w': 680},
                                             'thumb': {'h': 150,
                                                       'resize': 'crop',
                                                       'w': 150}},
                                   'type': 'photo',
                                   'url': 'https://t.co/QWBqSBoB7H'}]},
  'favorite_count': 2,
  'favorited': False,
  'geo': None,
  'id': 1137509083345559552,
  'id_str': '1137509083345559552',
  'in_reply_to_screen_name': None,
  'in_reply_to_status_id': None,
  'in_reply_to_status_id_str': None,
  'in_reply_to_user_id': None,
  'in_reply_to_user_id_str': None,
  'is_quote_status': False,
  'lang': 'en',
  'metadata': {'iso_language_code': 'en', 'result_type': 'recent'},
  'place': None,
  'possibly_sensitive': False,
  'retweet_count': 0,
  'retweeted': False,
  'source': '<a href="http://maximum-pain.com" rel="nofollow"maxpain</a',
  'text': '$AAPL Max Pain is 180.00 for maturity 06/14/2019. #maxpain #options '
          'https://t.co/CCUsRwhEoM https://t.co/QWBqSBoB7H',
  'truncated': False,
  'user': {'contributors_enabled': False,
           'created_at': 'Sun Apr 03 21:22:18 +0000 2016',
           'default_profile': True,
           'default_profile_image': False,
           'description': '',
           'entities': {'description': {'urls': []},
                        'url': {'urls': [{'display_url': 'maximum-pain.com',
                                          'expanded_url': 'http://maximum-pain.com',
                                          'indices': [0, 23],
                                          'url': 'https://t.co/eIsTCt8fCQ'}]}},
           'favourites_count': 15,
           'follow_request_sent': None,
           'followers_count': 1449,
           'following': None,
           'friends_count': 10,
           'geo_enabled': False,
           'has_extended_profile': False,
           'id': 716737614771044352,
           'id_str': '716737614771044352',
           'is_translation_enabled': False,
           'is_translator': False,
           'lang': 'en',
           'listed_count': 53,
           'location': '',
           'name': 'max pain',
           'notifications': None,
           'profile_background_color': 'F5F8FA',
           'profile_background_image_url': None,
           'profile_background_image_url_https': None,
           'profile_background_tile': False,
           'profile_banner_url': 'https://pbs.twimg.com/profile_banners/716737614771044352/1468284199',
           'profile_image_url': 'http://pbs.twimg.com/profile_images/752664674416619520/cdAjb6AU_normal.jpg',
           'profile_image_url_https': 'https://pbs.twimg.com/profile_images/752664674416619520/cdAjb6AU_normal.jpg',
           'profile_link_color': '1DA1F2',
           'profile_sidebar_border_color': 'C0DEED',
           'profile_sidebar_fill_color': 'DDEEF6',
           'profile_text_color': '333333',
           'profile_use_background_image': True,
           'protected': False,
           'screen_name': 'optioncharts',
           'statuses_count': 161829,
           'time_zone': None,
           'translator_type': 'none',
           'url': 'https://t.co/eIsTCt8fCQ',
           'utc_offset': None,
           'verified': False}}]
```



 __Exchange Rate Data:__ 
 ##### Powered by Exchange Rate API 
File: JSON Object 
Description: Putting Data into pandas dataframe 
Size: 52 rows by 5 columns, where the pandas index is the exchange currency short name 
Format: JSON Dictionary 
Example: 
```
{'base': 'USD', 'date': '2019-06-07', 'rates': {'AED': 3.672459, 'ARS': 44.899611, 'AUD': 1.43252, 'BGN': 1.737344, 'BRL': 3.876962, 'BSD': 1, 'CAD': 1.339201, 'CHF': 0.991815,…}, 'time_last_updated': 1559866243}
```

 __Files Produced After Executing the Script:__ 
ticker.csv 
news.csv 
twitter.csv 
merged_data.csv 





