

```
!pip install --upgrade -q gspread
```

# GOT DEATH POOL BITCHES


```
from google.colab import auth
auth.authenticate_user()

import gspread
from oauth2client.client import GoogleCredentials

gc = gspread.authorize(GoogleCredentials.get_application_default())

worksheet = gc.open('Game of Thrones Season 8 Death Pool (Responses)').sheet1

# get_all_values gives a list of rows.
rows = worksheet.get_all_values()
print(rows[0])

# Convert to a DataFrame and render.
import pandas as pd
df = pd.DataFrame.from_records(rows[1:], columns=rows[0], index='Who are you?')

```

    ['Timestamp', 'Jon Snow', 'Daenerys Targaryen Stormborn of the House Targaryen, the First of Her Name, Queen of the Andals, the Rhoynar and the First Men, Lady of the Seven Kingdoms and Protector of the Realm, Lady of Dragonstone, Queen of Meereen, Khaleesi of the Great Grass Sea, the Unburnt, Breaker of Chains and Mother of Dragons', 'Sansa Stark', 'Arya Stark', 'Bran Stark', 'Jamie Fookin Lannister', 'Tyrion Lannister', 'Yara Greyjoy', 'Jorah Mormont', 'Gendry Baratheon', 'Ser Davos Seaworth the Onion Knight', 'Brienne of Tarth', 'Podric Payne', 'The Hound', 'Samwell Tarley', 'Gilly', 'Sam the Baby', 'Ser Bronn of the Blackwater', 'Missandei', 'Meera Reed', 'Lyanna Mormont', 'Hot Pie', 'Cersei Lannister', 'Euron Greyjoy', 'The Mountain', 'Qyburn', 'Elia Sand', 'Theon Greyjoy', 'Varys the Spider', 'Grey Worm', 'Melisandre', 'Beric Dondarrion', 'Tormund Giantsbane', 'Ghost', 'Drogon', 'Rhaegal', 'Was the boatsex fruitful?', 'If the she is, does the "baby" live?', 'Does the Night King die?', 'If the Night King was done in, whodunit?', "Who's sitting on the Iron Throne at the very end?", 'Who are you?']
    


```
rename = {
    'Jon Snow': 'jon_snow',
    'Daenerys Targaryen Stormborn of the House Targaryen, the First of Her Name, Queen of the Andals, the Rhoynar and the First Men, Lady of the Seven Kingdoms and Protector of the Realm, Lady of Dragonstone, Queen of Meereen, Khaleesi of the Great Grass Sea, the Unburnt, Breaker of Chains and Mother of Dragons': 'daenerys_targaryen',
    'Sansa Stark': 'sansa_stark',
    'Arya Stark': 'arya_stark',
    'Bran Stark': 'bran_stark',
    'Jamie Fookin Lannister': 'jamie_lannister',
    'Tyrion Lannister': 'tyrion_lannister',
    'Yara Greyjoy': 'yara_greyjoy',
    'Jorah Mormont': 'jorah_mormont',
    'Gendry Baratheon': 'gendry_baratheon',
    'Ser Davos Seaworth the Onion Knight': 'davos_seaworth',
    'Brienne of Tarth': 'brienne_of_tarth',
    'Podric Payne': 'podric_payne',
    'The Hound': 'the_hound',
    'Samwell Tarley': 'samwell_tarley',
    'Gilly': 'gilly',
    'Sam the Baby': 'baby_sam',
    'Ser Bronn of the Blackwater': 'bronn_of_blackwater',
    'Missandei': 'missandei',
    'Meera Reed': 'meera_reed',
    'Lyanna Mormont': 'lyanna_mormont',
    'Hot Pie': 'hot_pie',
    'Cersei Lannister': 'cersei_lannister',
    'Euron Greyjoy': 'euron_greyjoy',
    'The Mountain': 'the_mountain',
    'Qyburn': 'qyburn',
    'Elia Sand': 'elia_sand',
    'Theon Greyjoy': 'theon_greyjoy',
    'Varys the Spider': 'varys_the_spider',
    'Grey Worm': 'grey_worm',
    'Melisandre': 'melisandre',
    'Beric Dondarrion': 'beric_dondarrion',
    'Tormund Giantsbane': 'tormund_giantsbane',
    'Ghost': 'ghost',
    'Drogon': 'drogon',
    'Rhaegal': 'rhaegal',
    'Was the boatsex fruitful?': 'pregnant',
    'If the she is, does the "baby" live?': 'abortion',
    'Does the Night King die?': 'iced',
    'If the Night King was done in, whodunit?': 'whodunit',
    'Who\'s sitting on the Iron Throne at the very end?': 'throne',
    'Who are you?': 'name'
}

df.rename(columns=rename, inplace=True)
```


```
cols_reorder = [
    'jon_snow',
    'daenerys_targaryen',
    'sansa_stark',
    'arya_stark',
    'bran_stark',
    'cersei_lannister',
    'jamie_lannister',
    'tyrion_lannister',
    'theon_greyjoy',
    'yara_greyjoy',
    'euron_greyjoy',
    'melisandre',
    'varys_the_spider',
    'jorah_mormont',
    'beric_dondarrion',
    'gendry_baratheon',
    'brienne_of_tarth',
    'podric_payne',
    'the_hound',
    'the_mountain',
    'samwell_tarley',
    'gilly',
    'baby_sam',
    'davos_seaworth',
    'bronn_of_blackwater',
    'tormund_giantsbane',
    'grey_worm',
    'missandei',
    'meera_reed',
    'lyanna_mormont',
    'qyburn',
    'elia_sand',
    'hot_pie',
    'ghost',
    'drogon',
    'rhaegal'
]

bonus = [
    'pregnant',
    'abortion',
    'iced',
    'whodunit',
    'throne'    
]

heroes = [
    'jon_snow',
    'daenerys_targaryen',
    'sansa_stark',
    'arya_stark',
    'bran_stark',
    'jamie_lannister',
    'tyrion_lannister',
    'yara_greyjoy',
    'melisandre',
    'jorah_mormont',
    'beric_dondarrion',
    'gendry_baratheon',
    'brienne_of_tarth',
    'podric_payne',
    'the_hound',
    'samwell_tarley',
    'gilly',
    'baby_sam',
    'davos_seaworth',
    'bronn_of_blackwater',
    'tormund_giantsbane',
    'missandei',
    'meera_reed',
    'lyanna_mormont',
    'hot_pie'   
]

villians = [
    'cersei_lannister',
    'euron_greyjoy',
    'the_mountain',
    'qyburn',
    'elia_sand'
]

eunuchs = [
    'theon_greyjoy',
    'varys_the_spider',
    'grey_worm'    
]

animals = [
    'ghost',
    'drogon',
    'rhaegal'
]

print(cols_reorder + bonus)

df_reorder = df[cols_reorder + bonus]
df[cols_reorder + bonus]
```

    ['jon_snow', 'daenerys_targaryen', 'sansa_stark', 'arya_stark', 'bran_stark', 'cersei_lannister', 'jamie_lannister', 'tyrion_lannister', 'theon_greyjoy', 'yara_greyjoy', 'euron_greyjoy', 'melisandre', 'varys_the_spider', 'jorah_mormont', 'beric_dondarrion', 'gendry_baratheon', 'brienne_of_tarth', 'podric_payne', 'the_hound', 'the_mountain', 'samwell_tarley', 'gilly', 'baby_sam', 'davos_seaworth', 'bronn_of_blackwater', 'tormund_giantsbane', 'grey_worm', 'missandei', 'meera_reed', 'lyanna_mormont', 'qyburn', 'elia_sand', 'hot_pie', 'ghost', 'drogon', 'rhaegal', 'pregnant', 'abortion', 'iced', 'whodunit', 'throne']
    




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
      <th>jon_snow</th>
      <th>daenerys_targaryen</th>
      <th>sansa_stark</th>
      <th>arya_stark</th>
      <th>bran_stark</th>
      <th>cersei_lannister</th>
      <th>jamie_lannister</th>
      <th>tyrion_lannister</th>
      <th>theon_greyjoy</th>
      <th>yara_greyjoy</th>
      <th>...</th>
      <th>elia_sand</th>
      <th>hot_pie</th>
      <th>ghost</th>
      <th>drogon</th>
      <th>rhaegal</th>
      <th>pregnant</th>
      <th>abortion</th>
      <th>iced</th>
      <th>whodunit</th>
      <th>throne</th>
    </tr>
    <tr>
      <th>Who are you?</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Ryan Denoux</th>
      <td>Dead</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>...</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>He's shooting blanks</td>
      <td></td>
      <td>He's still laughing straight to the bank</td>
      <td></td>
      <td>Jahaerys Targaryen</td>
    </tr>
    <tr>
      <th>Neal</th>
      <td>Wight</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Wight</td>
      <td>Dead</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Wight</td>
      <td>Dead</td>
      <td>...</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Alive</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>She's preggers</td>
      <td>no</td>
      <td>He's still laughing straight to the bank</td>
      <td>Pervy Bran</td>
      <td>Gendry</td>
    </tr>
    <tr>
      <th>Will</th>
      <td>Alive</td>
      <td>Alive</td>
      <td>Dead</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Dead</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Dead</td>
      <td>...</td>
      <td>Dead</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Dead</td>
      <td>She's preggers</td>
      <td>yes</td>
      <td>Somebody iced his ass</td>
      <td>Bran via spooky mind control</td>
      <td>Your momma (Danny)</td>
    </tr>
    <tr>
      <th>Rob</th>
      <td>Alive</td>
      <td>Dead</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Dead</td>
      <td>...</td>
      <td>Dead</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>She's preggers</td>
      <td>yes</td>
      <td>Somebody iced his ass</td>
      <td>Bran</td>
      <td>Jon Snow</td>
    </tr>
    <tr>
      <th>Dom T</th>
      <td>Alive</td>
      <td>Dead</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Alive</td>
      <td>...</td>
      <td>Dead</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Dead</td>
      <td>Alive</td>
      <td>She's preggers</td>
      <td>no</td>
      <td>He's still laughing straight to the bank</td>
      <td></td>
      <td>Jon Snow</td>
    </tr>
    <tr>
      <th>Will Sweet</th>
      <td>Dead</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>...</td>
      <td>Dead</td>
      <td>Alive</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>He's shooting blanks</td>
      <td></td>
      <td>Somebody iced his ass</td>
      <td>Samwell_Tarly</td>
      <td>None</td>
    </tr>
    <tr>
      <th>David Susko</th>
      <td>Alive</td>
      <td>Alive</td>
      <td>Dead</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Alive</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>...</td>
      <td>Dead</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Dead</td>
      <td>He's shooting blanks</td>
      <td></td>
      <td>Somebody iced his ass</td>
      <td>podric mutherfucking Payne</td>
      <td>Aegon Targaryen</td>
    </tr>
    <tr>
      <th>Brazin</th>
      <td>Dead</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>...</td>
      <td>Dead</td>
      <td>Alive</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>She's preggers</td>
      <td>yes</td>
      <td>Somebody iced his ass</td>
      <td>yes</td>
      <td>no one</td>
    </tr>
    <tr>
      <th>Rich</th>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Dead</td>
      <td>Wight</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>...</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Alive</td>
      <td>She's preggers</td>
      <td>yes</td>
      <td>Somebody iced his ass</td>
      <td>Jon and danny</td>
      <td>Daeny and jon</td>
    </tr>
    <tr>
      <th>Wills Thot (liane)</th>
      <td>Wight</td>
      <td>Alive</td>
      <td>Dead</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Alive</td>
      <td>Wight</td>
      <td>...</td>
      <td>Dead</td>
      <td>Wight</td>
      <td>Alive</td>
      <td>Dead</td>
      <td>Alive</td>
      <td>She's preggers</td>
      <td>no</td>
      <td>Somebody iced his ass</td>
      <td>Brandon Stark</td>
      <td>IF one of them doesn’t die, jon and Dany split...</td>
    </tr>
    <tr>
      <th>Batt</th>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Alive</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>...</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Alive</td>
      <td>Dead</td>
      <td>She's preggers</td>
      <td>yes</td>
      <td>Somebody iced his ass</td>
      <td>bran</td>
      <td>no one</td>
    </tr>
    <tr>
      <th>Meghan</th>
      <td>Alive</td>
      <td>Dead</td>
      <td>Alive</td>
      <td>Wight</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Dead</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Wight</td>
      <td>...</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Alive</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>He's shooting blanks</td>
      <td>yes</td>
      <td>Somebody iced his ass</td>
      <td>Snew</td>
      <td>Cerseii</td>
    </tr>
    <tr>
      <th>s8e1</th>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>...</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>Bruce Jennder</th>
      <td>Wight</td>
      <td>Alive</td>
      <td>Dead</td>
      <td>Alive</td>
      <td>Wight</td>
      <td>Alive</td>
      <td>Dead</td>
      <td>Alive</td>
      <td>Dead</td>
      <td>Alive</td>
      <td>...</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Dead</td>
      <td>She's preggers</td>
      <td>yes</td>
      <td>He's still laughing straight to the bank</td>
      <td>Jon Snow</td>
      <td>Khaleesi</td>
    </tr>
    <tr>
      <th>Maddie P</th>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Dead</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Dead</td>
      <td>...</td>
      <td>Wight</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>She's preggers</td>
      <td>yes</td>
      <td>He's still laughing straight to the bank</td>
      <td></td>
      <td>Jon!!!!</td>
    </tr>
    <tr>
      <th>Robby D</th>
      <td>Dead</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Dead</td>
      <td>Wight</td>
      <td>Dead</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Dead</td>
      <td>Dead</td>
      <td>...</td>
      <td>Dead</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Dead</td>
      <td>She's preggers</td>
      <td>yes</td>
      <td>Somebody iced his ass</td>
      <td>John Snow</td>
      <td>Dragon queen bittttttch</td>
    </tr>
    <tr>
      <th>s8e2</th>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>...</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>s8e3</th>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Dead</td>
      <td>Alive</td>
      <td>...</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td>Alive</td>
      <td></td>
      <td></td>
      <td>Somebody iced his ass</td>
      <td>No one</td>
      <td></td>
    </tr>
  </tbody>
</table>
<p>18 rows × 41 columns</p>
</div>




```
matched_sheet = df_reorder.T.to_csv('transfer.csv')
```

##### Dataset Prep
Preproceesing steps to create selection percentages and correct guesses


```
current_episode = 's8e3'

df['alive'] = df[df=='Alive'].count(axis=1) / df[cols_reorder].count(axis=1)
df['dead'] = df[df=='Dead'].count(axis=1) / df[cols_reorder].count(axis=1)
df['wight'] = df[df=='Wight'].count(axis=1) / df[cols_reorder].count(axis=1)

status = ['alive', 'dead', 'wight']
episodes = ['s8e1', 's8e2', 's8e3']
meta_drop = ['pregnant', 'abortion', 'iced', 'whodunit', 'throne', 'alive', 'dead', 'wight']

for player in df.index:
  if player not in episodes:
    df.loc[player, 'correct'] = (df.loc[player, :].drop(columns=meta_drop) == df.loc[current_episode, :].drop(columns=meta_drop)).sum() / df.loc[player, :].drop(columns=meta_drop).count()
```

    /usr/local/lib/python3.6/dist-packages/pandas/core/ops.py:1649: FutureWarning: elementwise comparison failed; returning scalar instead, but in the future will perform elementwise comparison
      result = method(y)
    

# Haltime Report
So we finally get some fucking blood for the BOBBY-B god (Not enough in this humble servants opinion). Now we get to see who's on track to sit on the iron throne of bets, who picked the right wights, and who's shit outta luck (read this guy). Additionally, since the Night King's fate was sealed (probably) this episode, we'll have a look at who predicted wolverine to swoop in for the massive kill steal. As a reminder the questions were:

*   Does the Night King Die?
*   If so, whodunit?

As a reminder, this is only a update to the current status of the cast and crew. The death pool only counts character status at the end of the season and assumes all off screen characters to be currently alive until their death is mentioned or shown (i.e. Ellaria Sand (yes, we did fuck up and put Elia Sand (who is definitely dead) instead of the paramour of Oberyn Martell (which is who we were initially referring to))).

As a bonus, we happen to have the GOAT, the man, the myth, the Legend27 himself, Bobby-B the one true king of the seven kingdoms himself providing commentary throughout. Why don't you give the readers a few words before we get started Bobby-B

## I'VE GOT SEVEN KINGDOMS TO RULE! ONE KING, SEVEN KINGDOMS!

Well, uh, we do appreciate you tak--

## START THE DAMN JOUST BEFORE I PISS MESELF!

On that note, let's get started



## The Picks

### Who are the optimists?

Those who had the most characters surving the trials and tribulations of Season 8, and to those of you at the top of this list I ask, "What's the matter? Can't handle more crippling emotional trauma of having characters you've bonded with snatched by the cold hands of death? Do you also still wet the bed?" Perhaps the lord of the seven kingdoms can talk some sense into these lost sheep.

## YOU'RE MY COUNCIL, COUNSEL! SPEAK SENSE TO THIS HONORABLE FOOL!

Uh, I already tried that, your grace. I don't think they can be reasoned with at this point

## PISS ON THAT! SEND A RAVEN! I WANT YOU TO STAY! I'M THE KING, I GET WHAT I WANT!

Well, maybe they'll see the error of their ways when more of their favorites die (hopefully)


```
bitches = df.loc[:, ['alive']].drop(episodes).sort_values('alive', ascending=False)
ax = bitches.plot(
    kind='barh', xlim=(0, 1.19), title='Bunch a Bitches', figsize=(5, 7)
)
ax.invert_yaxis()

for i in ax.patches:
    # get_width pulls left or right; get_y pushes up or down
    ax.text(i.get_width() + .025, i.get_y()+.38, str(round((i.get_width())*100, 2))+'%', fontsize=12, color='dimgrey')
```


![png](GOT_Death_Pool_files/GOT_Death_Pool_11_0.png)


### Who are the Negative Nancy's
Those who predicted that most of the characters fates were sealed by being born into a fantasy universe where the prophecies are made up and the lives don't matter. These fucks probably enjoy watching show casuals wrench about in pain and suffering as they watch their favorite characters get killed far earlier than traditional narratives call for. I'm sure we can all agree that only the finest can be counted among these ranks, can't we Bobby-B?

## COME, BOW BEFORE YOUR KING! BOW, YA SHITS!

I'm sure they're all lined up and ready to pay their respects to you, your grace.

## TAKE ME TO YOUR CRYPT, I WANT TO PAY MY RESPECTS!

Uh, I'm not so sure you want to go there right now.

## HOLD YOUR TONGUE!

... moving on



```
psychos = df.loc[:, ['dead']].drop(episodes).sort_values('dead', ascending=False)
ax = psychos.plot(
    kind='barh', xlim=(0, 1.19), title='Bunch a Psychos', figsize=(5, 7)
)
ax.invert_yaxis()

for i in ax.patches:
    # get_width pulls left or right; get_y pushes up or down
    ax.text(i.get_width() + .025, i.get_y()+.38, str(round((i.get_width())*100, 2))+'%', fontsize=12, color='dimgrey')
```


![png](GOT_Death_Pool_files/GOT_Death_Pool_13_0.png)


### Who actually used the Wight option?
Yes, this was an option initially proposed when the death pool was first opened, and I'll be honest, I actually didn't expect anybody to wind up on this list because the showrunners ARE SPINELESS COWARDS WHO DON'T EVEN KNOW HOW TO STICK THEM WITH THE POINTY END!
## THEY NEVER TELL YOU HOW THEY ALL SHIT THEMSELVES! THEY DON'T PUT THAT PART IN THE SONGS!
RIGHT!? IF OUR ONE TRUE KING WERE STILL RUNNING THINGS, WE'D STILL HAVE PLENTY OF DEATH TO GO AROUND
## GODS I WAS STRONG THEN
I'd love to see the great Bobby-B smashing in some heads with his war hammer, but we should probably move on to the actual results


```
wierdos = df.loc[:, ['wight']].drop(episodes).sort_values('wight', ascending=False)
ax = wierdos.plot(
    kind='barh', xlim=(0, 1.19), title='Bunch a Wierdos', figsize=(5, 7)
)
ax.invert_yaxis()

for i in ax.patches:
    # get_width pulls left or right; get_y pushes up or down
    ax.text(i.get_width() + .025, i.get_y()+.38, str(round((i.get_width())*100, 2))+'%', fontsize=12, color='dimgrey')
```


![png](GOT_Death_Pool_files/GOT_Death_Pool_15_0.png)


## The Results So Far
Throught the end of episode 3 here is the list of whose been most accurate at deciding the fate of our characters. I would like to take this time to declare that y'all are a bunch a bitches whose spinelessness is second only the the showrunners themselves who can't stop snorting HBO money likes its pure Colombian Bam-Bam. GIVE US MORE GHOST YOU BASTARDS! 
## HOLD YOUR TONGUE
Apologies, your grace, I just think it's unspeakable that the showrunners can't seem to pierce anymore plot armor.
## OH, IT'S UNSPEAKABLE TO YOU? WHAT HER FATHER DID TO YOUR FAMILY, THAT WAS UNSPEAKABLE!
Uh, I thought we weren't going to get into that. Can we just change the subject?
## YOUR MOTHER WAS A DUMB WHORE WITH A FAT ARSE, DID YOU KNOW THAT?
You know what, I'm just going to go back to my guard post and keep watch for the next episode
## FORCED TO MIND THE DOOR WHILE YOUR KING EATS AND DRINKS AND SHITS AND FUCKS!
...



```
leaders = df.loc[:, ['correct']].drop(episodes).sort_values('correct', ascending=False)
ax = leaders.plot(
    kind='barh', xlim=(0, 1.19), title='Bunch a Winners?', figsize=(5, 7)
)
ax.invert_yaxis()

for i in ax.patches:
    # get_width pulls left or right; get_y pushes up or down
    ax.text(i.get_width() + .025, i.get_y()+.38, str(round((i.get_width())*100, 2))+'%', fontsize=12, color='dimgrey')
```


![png](GOT_Death_Pool_files/GOT_Death_Pool_17_0.png)

