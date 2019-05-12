
# GOT DEATH POOL BITCHES

### Imports


```python
import pandas as pd
from IPython.display import HTML

pd.set_option('display.max_columns', None)
```


```python
df = pd.read_csv('responses.csv', index_col=-1)
```


```python
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


```python
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

df_reorder = df[cols_reorder + bonus]
```


```python
matched_sheet = df_reorder.T.to_csv('transfer.csv')
```

##### Dataset Prep
Preproceesing steps to create selection percentages and correct guesses


```python
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


```python
bitches = df.loc[:, ['alive']].drop(episodes).sort_values('alive', ascending=False)
ax = bitches.plot(
    kind='barh', xlim=(0, 1.19), title='Bunch a Bitches', figsize=(5, 7)
)
ax.invert_yaxis()

for i in ax.patches:
    # get_width pulls left or right; get_y pushes up or down
    ax.text(i.get_width() + .025, i.get_y()+.38, str(round((i.get_width())*100, 2))+'%', fontsize=12, color='dimgrey')
```

### Who are the Negative Nancy's
Those who predicted that most of the characters fates were sealed by being born into a fantasy universe where the prophecies are made up and the lives don't matter. These fucks probably enjoy watching show casuals wrench about in pain and suffering as they watch their favorite characters get killed far earlier than traditional narratives call for. I'm sure we can all agree that only the finest can be counted among these ranks, can't we Bobby-B?

## COME, BOW BEFORE YOUR KING! BOW, YA SHITS!

I'm sure they're all lined up and ready to pay their respects to you, your grace.

## TAKE ME TO YOUR CRYPT, I WANT TO PAY MY RESPECTS!

Uh, I'm not so sure you want to go there right now.

## HOLD YOUR TONGUE!

... moving on



```python
psychos = df.loc[:, ['dead']].drop(episodes).sort_values('dead', ascending=False)
ax = psychos.plot(
    kind='barh', xlim=(0, 1.19), title='Bunch a Psychos', figsize=(5, 7)
)
ax.invert_yaxis()

for i in ax.patches:
    # get_width pulls left or right; get_y pushes up or down
    ax.text(i.get_width() + .025, i.get_y()+.38, str(round((i.get_width())*100, 2))+'%', fontsize=12, color='dimgrey')
```


![png](GOT_Death_Pool_files/GOT_Death_Pool_14_0.png)


### Who actually used the Wight option?
Yes, this was an option initially proposed when the death pool was first opened, and I'll be honest, I actually didn't expect anybody to wind up on this list because the showrunners ARE SPINELESS COWARDS WHO DON'T EVEN KNOW HOW TO STICK THEM WITH THE POINTY END!
## THEY NEVER TELL YOU HOW THEY ALL SHIT THEMSELVES! THEY DON'T PUT THAT PART IN THE SONGS!
RIGHT!? IF OUR ONE TRUE KING WERE STILL RUNNING THINGS, WE'D STILL HAVE PLENTY OF DEATH TO GO AROUND
## GODS I WAS STRONG THEN
I'd love to see the great Bobby-B smashing in some heads with his war hammer, but we should probably move on to the actual results


```python
wierdos = df.loc[:, ['wight']].drop(episodes).sort_values('wight', ascending=False)
ax = wierdos.plot(
    kind='barh', xlim=(0, 1.19), title='Bunch a Wierdos', figsize=(5, 7)
)
ax.invert_yaxis()

for i in ax.patches:
    # get_width pulls left or right; get_y pushes up or down
    ax.text(i.get_width() + .025, i.get_y()+.38, str(round((i.get_width())*100, 2))+'%', fontsize=12, color='dimgrey')
```


![png](GOT_Death_Pool_files/GOT_Death_Pool_16_0.png)


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



```python
leaders = df.loc[:, ['correct']].drop(episodes).sort_values('correct', ascending=False)
ax = leaders.plot(
    kind='barh', xlim=(0, 1.19), title='Bunch a Winners?', figsize=(5, 7)
)
ax.invert_yaxis()

for i in ax.patches:
    # get_width pulls left or right; get_y pushes up or down
    ax.text(i.get_width() + .025, i.get_y()+.38, str(round((i.get_width())*100, 2))+'%', fontsize=12, color='dimgrey')
```


![png](GOT_Death_Pool_files/GOT_Death_Pool_18_0.png)

