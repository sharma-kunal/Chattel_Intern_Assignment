# Installation

Run the command to install all the required dependencies

```
pip install -r requirements.txt
```

# Assignment 1

Scrape google news for both `Main News` and `Sub News`.

The dataframe looks like as shown in the below figure,

![News Dataframe]('https://github.com/sharma-kunal/Chattel_Intern_Assignment/blob/master/media/News_df.png')

Used [newspaper3k]('https://newspaper.readthedocs.io/en/latest/') to get the summary, publish date and all other details from the news articles.

Used [pyshorteners]('https://pypi.org/project/pyshorteners/') to shorten the url and use them for further purposes.

Stored the text of each news article in a map with key as link and value as full news text.

```
def search_word(word):
    for key, value in text_map.items():
        for line in value:
            if word in line:
                print("Found at: " + key)
                print(line + "\n")
```


# Assignment 2

Collecting real time stock market data from [moneycontrol.com]('https://www.moneycontrol.com/stocks/marketstats/indexcomp.php?optex=NSE&opttopic=indexcomp&index=9').

The dataframe looks like as shown in the below figure,

![Stock Dataframe]('https://github.com/sharma-kunal/Chattel_Intern_Assignment/blob/master/media/Stock_df.png')

The code runs for 20 minutes and extracts data every 30 seconds and at every 2 minutes interval, we check whether the difference in `%Chg` is `>= 2` and if it is, then alert the user about the change and the industry name.

```
start_time = time.time()
df = get_data()
running_time = 0
data = [df]
total_time = 20 #minutes
while running_time <= total_time*60:
    time.sleep(30)
    df = get_data()
    data.append(df)
    if len(data) % 4 == 0:
        temp = check_for_alert(data[0][:]['%Chg'].values, data[-1][:]['%Chg'].values)
        for i in temp:
            alert(data[-1][i]['Company Name'], abs(float(data[-1][i]['%Chg'])-float(data[0][i]['%Chg'])))
        data = data[1:]
    running_time = time.time()-start_time
```

