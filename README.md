

```python
textAnalyticsURL = 'southcentralus.api.cognitive.microsoft.com'
textAnalyticsKey = 'd01a6b835c8244619c42e824dc2faf19'
```


```python
import urllib.parse, http.client, urllib.request, urllib.error, json

headers = {
    'Content-Type' : 'application/json',
    'Ocp-Apim-Subscription-Key' : textAnalyticsKey,
    'Accept' : 'application/json'
}

body = {
    'documents' : [
        {
            'language' : 'en',
            'id' : '1',
            'text' : 'Wow! I am loving this course!'
        },
        {
            'language' : 'en',
            'id' : '2',
            'text' : 'This course is not working for me right now.'
        }
    ]
}

params = urllib.parse.urlencode({})

try:
    conn = http.client.HTTPSConnection(textAnalyticsURL)
    conn.request("POST", "/text/analytics/v2.0/sentiment?%s" % params, str(body), headers)
    response = conn.getresponse()
    jsonData = response.read().decode("UTF-8")
    data = json.loads(jsonData)
    for document in data['documents']:
        sentiment = "positive"
        if document['score'] <= 0.5:
            sentiment = "negative"
        print('Document ' + document['id'] + ' has a ' + sentiment + ' sentiment')
    conn.close()
except Exception as ex:
    print(ex.strerror)
```

    Document 1 has a positive sentiment
    Document 2 has a negative sentiment



```python
try:
    conn = http.client.HTTPSConnection(textAnalyticsURL)
    conn.request("POST", "/text/analytics/v2.0/keyPhrases?%s" % params, str(body), headers)
    response = conn.getresponse()
    jsonData = response.read().decode("UTF-8")
    data = json.loads(jsonData)
    for document in data['documents']:
        print('Document ' + document['id'] + ' has these key phrases:')
        for phrase in document['keyPhrases']:
            print("    " + phrase)
        print('-----------------------------------')
    conn.close()
except Exception as ex:
    print(ex.strerror)
```

    Document 1 has these key phrases:
        Wow
        course
    -----------------------------------
    Document 2 has these key phrases:
        course
    -----------------------------------



```python
!curl https://www.unisi.it/sites/default/files/speech.txt -o speech.txt
document = open("speech.txt", "r")

mlk_speech = document.read()
print(mlk_speech)
```

      % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                     Dload  Upload   Total   Spent    Left  Speed
    100  3349    0  3349    0     0   2793      0 --:--:--  0:00:01 --:--:--  2793
    And so even though we face the difficulties of today and tomorrow, I still have a dream. It is a dream deeply rooted in the American dream.
     
    I have a dream that one day this nation will rise up and live out the true meaning of its creed:
     
    We hold these truths to be self-evident, that all men are created equal.
     
    I have a dream that one day on the red hills of Georgia, the sons of former slaves and the sons of former slave owners will be able to sit down together at the table of brotherhood.
     
    I have a dream that one day even the state of Mississippi, a state sweltering with the heat of injustice, sweltering with the heat of oppression, will be transformed into an oasis of freedom and justice.
     
    I have a dream that my four little children will one day live in a nation where they will not be judged by the color of their skin but by the content of their character.
     
    I have a dream today!
     
    I have a dream that one day, down in Alabama, with its vicious racists, with its governor having his lips dripping with the words of interposition and nullification, one day right there in Alabama little black boys and black girls will be able to join hands with little white boys and white girls as sisters and brothers.
     
    I have a dream today!
     
    I have a dream that one day every valley shall be exalted, and every hill and mountain shall be made low, the rough places will be made plain, and the crooked places will be made straight; and the glory of the Lord shall be revealed and all flesh shall see it together.
     
    This is our hope, and this is the faith that I go back to the South with.
     
    With this faith, we will be able to hew out of the mountain of despair a stone of hope. With this faith, we will be able to transform the jangling discords of our nation into a beautiful symphony of brotherhood. With this faith, we will be able to work together, to pray together, to struggle together, to go to jail together, to stand up for freedom together, knowing that we will be free one day.
     
    And this will be the day, this will be the day when all of God s children will be able to sing with new meaning:
     
    My country  tis of thee, sweet land of liberty, of thee I sing.
    Land where my fathers died, land of the Pilgrim s pride,
    From every mountainside, let freedom ring!
    And if America is to be a great nation, this must become true.
    And so let freedom ring from the prodigious hilltops of New Hampshire.
    Let freedom ring from the mighty mountains of New York.
    Let freedom ring from the heightening Alleghenies of Pennsylvania.
    Let freedom ring from the snow-capped Rockies of Colorado.
    Let freedom ring from the curvaceous slopes of California.
     
    But not only that:
    Let freedom ring from Stone Mountain of Georgia.
    Let freedom ring from Lookout Mountain of Tennessee.
    Let freedom ring from every hill and molehill of Mississippi.
    From every mountainside, let freedom ring.
    And when this happens, when we allow freedom ring, when we let it ring from every village and every hamlet, from every state and every city, we will be able to speed up that day when all of God s children, black men and white men, Jews and Gentiles, Protestants and Catholics, will be able to join hands and sing in the words of the old Negro spiritual:
    Free at last! Free at last!
     
    Thank God Almighty, we are free at last!



```python
from string import punctuation

# remove numbers
mlk_speech = ''.join(c for c in mlk_speech if not c.isdigit())

# remove punctuation and make lower case
mlk_speech = ''.join(c for c in mlk_speech if c not in punctuation).lower()

print(mlk_speech)
```

    and so even though we face the difficulties of today and tomorrow i still have a dream it is a dream deeply rooted in the american dream
     
    i have a dream that one day this nation will rise up and live out the true meaning of its creed
     
    we hold these truths to be selfevident that all men are created equal
     
    i have a dream that one day on the red hills of georgia the sons of former slaves and the sons of former slave owners will be able to sit down together at the table of brotherhood
     
    i have a dream that one day even the state of mississippi a state sweltering with the heat of injustice sweltering with the heat of oppression will be transformed into an oasis of freedom and justice
     
    i have a dream that my four little children will one day live in a nation where they will not be judged by the color of their skin but by the content of their character
     
    i have a dream today
     
    i have a dream that one day down in alabama with its vicious racists with its governor having his lips dripping with the words of interposition and nullification one day right there in alabama little black boys and black girls will be able to join hands with little white boys and white girls as sisters and brothers
     
    i have a dream today
     
    i have a dream that one day every valley shall be exalted and every hill and mountain shall be made low the rough places will be made plain and the crooked places will be made straight and the glory of the lord shall be revealed and all flesh shall see it together
     
    this is our hope and this is the faith that i go back to the south with
     
    with this faith we will be able to hew out of the mountain of despair a stone of hope with this faith we will be able to transform the jangling discords of our nation into a beautiful symphony of brotherhood with this faith we will be able to work together to pray together to struggle together to go to jail together to stand up for freedom together knowing that we will be free one day
     
    and this will be the day this will be the day when all of god s children will be able to sing with new meaning
     
    my country  tis of thee sweet land of liberty of thee i sing
    land where my fathers died land of the pilgrim s pride
    from every mountainside let freedom ring
    and if america is to be a great nation this must become true
    and so let freedom ring from the prodigious hilltops of new hampshire
    let freedom ring from the mighty mountains of new york
    let freedom ring from the heightening alleghenies of pennsylvania
    let freedom ring from the snowcapped rockies of colorado
    let freedom ring from the curvaceous slopes of california
     
    but not only that
    let freedom ring from stone mountain of georgia
    let freedom ring from lookout mountain of tennessee
    let freedom ring from every hill and molehill of mississippi
    from every mountainside let freedom ring
    and when this happens when we allow freedom ring when we let it ring from every village and every hamlet from every state and every city we will be able to speed up that day when all of god s children black men and white men jews and gentiles protestants and catholics will be able to join hands and sing in the words of the old negro spiritual
    free at last free at last
     
    thank god almighty we are free at last



```python
#remove stopwords
import nltk
nltk.download("stopwords")
from nltk.corpus import stopwords

mlk_speech = ' '.join([word for word in mlk_speech.split() if word not in (stopwords.words('english'))])

print(mlk_speech)
```

    [nltk_data] Downloading package stopwords to /home/nbuser/nltk_data...
    [nltk_data]   Unzipping corpora/stopwords.zip.
    even though face difficulties today tomorrow still dream dream deeply rooted american dream dream one day nation rise live true meaning creed hold truths selfevident men created equal dream one day red hills georgia sons former slaves sons former slave owners able sit together table brotherhood dream one day even state mississippi state sweltering heat injustice sweltering heat oppression transformed oasis freedom justice dream four little children one day live nation judged color skin content character dream today dream one day alabama vicious racists governor lips dripping words interposition nullification one day right alabama little black boys black girls able join hands little white boys white girls sisters brothers dream today dream one day every valley shall exalted every hill mountain shall made low rough places made plain crooked places made straight glory lord shall revealed flesh shall see together hope faith go back south faith able hew mountain despair stone hope faith able transform jangling discords nation beautiful symphony brotherhood faith able work together pray together struggle together go jail together stand freedom together knowing free one day day day god children able sing new meaning country tis thee sweet land liberty thee sing land fathers died land pilgrim pride every mountainside let freedom ring america great nation must become true let freedom ring prodigious hilltops new hampshire let freedom ring mighty mountains new york let freedom ring heightening alleghenies pennsylvania let freedom ring snowcapped rockies colorado let freedom ring curvaceous slopes california let freedom ring stone mountain georgia let freedom ring lookout mountain tennessee let freedom ring every hill molehill mississippi every mountainside let freedom ring happens allow freedom ring let ring every village every hamlet every state every city able speed day god children black men white men jews gentiles protestants catholics able join hands sing words old negro spiritual free last free last thank god almighty free last



```python
from nltk.stem.porter import PorterStemmer
from nltk.probability import FreqDist
import pandas as pd
nltk.download("punkt")

ps = PorterStemmer()
words = nltk.tokenize.word_tokenize(mlk_speech)
stems = [ps.stem(word) for word in words] 

fd = FreqDist(stems)
fd_df = pd.DataFrame(fd, index=[0]).T 

print(fd_df)
```

    [nltk_data] Downloading package punkt to /home/nbuser/nltk_data...
    [nltk_data]   Unzipping tokenizers/punkt.zip.
                  0
    abl           8
    alabama       2
    allegheni     1
    allow         1
    almighti      1
    america       1
    american      1
    back          1
    beauti        1
    becom         1
    black         3
    boy           2
    brother       1
    brotherhood   2
    california    1
    cathol        1
    charact       1
    children      3
    citi          1
    color         1
    colorado      1
    content       1
    countri       1
    creat         1
    creed         1
    crook         1
    curvac        1
    day          11
    deepli        1
    despair       1
    ...          ..
    speed         1
    spiritu       1
    stand         1
    state         3
    still         1
    stone         2
    straight      1
    struggl       1
    sweet         1
    swelter       2
    symphoni      1
    tabl          1
    tennesse      1
    thank         1
    thee          2
    though        1
    ti            1
    today         3
    togeth        7
    tomorrow      1
    transform     2
    true          2
    truth         1
    valley        1
    viciou        1
    villag        1
    white         3
    word          2
    work          1
    york          1
    
    [162 rows x 1 columns]



```python
%matplotlib inline
import matplotlib.pyplot as plt

counts = fd_df.sort_values(0, ascending = False)
ar = plt.figure(figsize=(16,9))
ax = ar.gca()
counts[0][:60].plot(kind='bar', ax=ax)
ax.set_title("Frequency Distribution")
ax.set_ylabel("Freq. or words")
ax.set_xlabel("Stems")
plt.show()
```


![png](output_7_0.png)

