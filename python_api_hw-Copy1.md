

```python
!pip install citipy
```

    Requirement already satisfied: citipy in c:\users\rjabbari\anaconda3\lib\site-packages (0.0.5)
    Requirement already satisfied: kdtree>=0.12 in c:\users\rjabbari\anaconda3\lib\site-packages (from citipy) (0.16)
    


```python
import requests
import random
import json
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import seaborn as sns
import gmaps
from citipy import citipy
import openweathermapy.core as owm

#My OpenWeatherMap api_key
from config import api_key
```


```python
# random generator of lat
lat = np.random.randint(-90, 90, size=1500).tolist()

# randon generator of lon
lon = np.random.randint(-180, 180, size=1500).tolist()

# create list of cities using citipy

cities = []

for lat, lon in list(zip(lat, lon)):
    
    city = (citipy.nearest_city(lat, lon))
    
    cities.append(city.city_name)

print(cities)
```

    ['guerrero negro', 'rikitea', 'souillac', 'somerset', 'rikitea', 'fort nelson', 'bluff', 'mananjary', 'fallon', 'tawkar', 'clyde river', 'concordia', 'mataura', 'sitka', 'candawaga', 'bluff', 'tasiilaq', 'lesosibirsk', 'punta arenas', 'snyder', 'shakiso', 'rikitea', 'atbasar', 'seoul', 'gat', 'albany', 'ushuaia', 'puerto baquerizo moreno', 'brae', 'jamestown', 'whitehorse', 'caravelas', 'thompson', 'punta arenas', 'vaini', 'arraial do cabo', 'cerro largo', 'caravelas', 'port lincoln', 'grindavik', 'calvinia', 'hobart', 'wilmington', 'la ronge', 'clyde river', 'katherine', 'vaini', 'vaini', 'kapaa', 'busselton', 'thompson', 'ribeira grande', 'chuy', 'rikitea', 'ust-maya', 'trat', 'woodward', 'nikolskoye', 'rikitea', 'marcona', 'rikitea', 'punta arenas', 'lhokseumawe', 'illoqqortoormiut', 'ushuaia', 'cape town', 'grand gaube', 'rikitea', 'carnarvon', 'krasnoarmeysk', 'saint george', 'busselton', 'vostok', 'whitehorse', 'marawi', 'prince rupert', 'kaitangata', 'irtyshskiy', 'dali', 'sao filipe', 'kavieng', 'hilo', 'kapaa', 'castro', 'georgetown', 'ushuaia', 'sao joao da barra', 'rikitea', 'quatre cocos', 'zhangye', 'provideniya', 'mataura', 'hobart', 'camacha', 'hermanus', 'ormstown', 'bluff', 'glendive', 'oktyabrskiy', 'makinsk', 'vaini', 'morros', 'chokurdakh', 'antalaha', 'port alfred', 'brownsville', 'bluff', 'cabo san lucas', 'bethel', 'vangaindrano', 'tuktoyaktuk', 'rikitea', 'rikitea', 'greenwood', 'luau', 'ponta delgada', 'sentyabrskiy', 'podyuga', 'khatanga', 'jamestown', 'punta arenas', 'bluff', 'pevek', 'constitucion', 'victoria', 'rikitea', 'ushuaia', 'busselton', 'bozdar', 'cape town', 'bluff', 'minot', 'ushuaia', 'port alfred', 'tuktoyaktuk', 'verkhoshizhemye', 'esperance', 'jamestown', 'mataura', 'gavle', 'busselton', 'saint george', 'ahipara', 'saskylakh', 'hobart', 'bluff', 'ponta do sol', 'saskylakh', 'manaure', 'mataura', 'tiksi', 'necochea', 'takoradi', 'bethel', 'georgetown', 'norman wells', 'thompson', 'tarko-sale', 'zhangye', 'puerto leguizamo', 'mataura', 'albany', 'hilo', 'punta arenas', 'punta arenas', 'esperance', 'puerto asis', 'santa cruz', 'vista hermosa', 'busselton', 'srednekolymsk', 'rio cuarto', 'lebu', 'hermanus', 'mehamn', 'sinazongwe', 'ushuaia', 'tuatapere', 'ushuaia', 'hobart', 'hamilton', 'kahului', 'ushuaia', 'galveston', 'punta arenas', 'charleston', 'albany', 'mataura', 'hermanus', 'attawapiskat', 'terme', 'karaul', 'chaihe', 'west wendover', 'phalaborwa', 'sitka', 'ajdabiya', 'luwuk', 'taolanaro', 'rikitea', 'moscow', 'fortuna foothills', 'illoqqortoormiut', 'albany', 'hilo', 'bulgan', 'san patricio', 'oleksandrivka', 'east london', 'binzhou', 'hithadhoo', 'ushuaia', 'cape town', 'kartaly', 'albany', 'cozumel', 'ushuaia', 'longyearbyen', 'ushuaia', 'ushuaia', 'port augusta', 'jalu', 'dikson', 'punta arenas', 'tautira', 'port alfred', 'atar', 'lebu', 'punta arenas', 'airai', 'miri', 'hambantota', 'cruzeiro do sul', 'mathathane', 'haukipudas', 'rodrigues alves', 'punta arenas', 'punta arenas', 'kermanshah', 'hermanus', 'bredasdorp', 'atuona', 'hithadhoo', 'touros', 'bluff', 'san cristobal', 'kobayashi', 'fort nelson', 'busselton', 'cape town', 'belushya guba', 'atuona', 'mount gambier', 'lingao', 'bluff', 'mataura', 'rikitea', 'provideniya', 'nouakchott', 'high level', 'corinto', 'coahuayana', 'saint-philippe', 'matamoros', 'thompson', 'port alfred', 'ushuaia', 'rikitea', 'port elizabeth', 'yar-sale', 'thompson', 'puerto ayora', 'tabuk', 'yakeshi', 'hobart', 'busselton', 'quelimane', 'putla', 'feijo', 'rikitea', 'iqaluit', 'nizhneyansk', 'safonovo', 'new norfolk', 'vaini', 'ushuaia', 'atuona', 'kruisfontein', 'albany', 'puerto ayora', 'mataura', 'illoqqortoormiut', 'tuatapere', 'bluff', 'mataura', 'port macquarie', 'kapaa', 'saleaula', 'vaini', 'rikitea', 'solnechnyy', 'hermanus', 'cocobeach', 'nikolskoye', 'qaanaaq', 'albany', 'faanui', 'brigantine', 'wanaka', 'vaini', 'miri', 'busselton', 'dikson', 'mathbaria', 'souillac', 'arraial do cabo', 'bredasdorp', 'pevek', 'grand centre', 'boa vista', 'yerbogachen', 'avarua', 'san borja', 'rikitea', 'nibbar', 'yenagoa', 'pathein', 'kremenki', 'hilo', 'tranas', 'talnakh', 'ushuaia', 'trelleborg', 'areia branca', 'taolanaro', 'ostrovnoy', 'sao joao da barra', 'cape town', 'bluff', 'hilo', 'mys shmidta', 'port alfred', 'ust-kuyga', 'auki', 'bluff', 'paamiut', 'turayf', 'cidreira', 'illoqqortoormiut', 'rungata', 'busselton', 'mareeba', 'hasaki', 'provideniya', 'vaini', 'victoria', 'yellowknife', 'busselton', 'jamestown', 'lagunas', 'kapaa', 'punta arenas', 'hermanus', 'mahebourg', 'rikitea', 'rikitea', 'upernavik', 'polson', 'winnemucca', 'latung', 'olafsvik', 'verkhoyansk', 'port blair', 'sibolga', 'sabha', 'punta arenas', 'sao joao da barra', 'dembi dolo', 'yellowknife', 'nanortalik', 'cape town', 'hermanus', 'shimoda', 'ushuaia', 'south lake tahoe', 'cape town', 'attawapiskat', 'vaini', 'vestmannaeyjar', 'tabou', 'georgetown', 'buta', 'new norfolk', 'taoudenni', 'punta arenas', 'ushuaia', 'albany', 'kirakira', 'arraial do cabo', 'puerto ayora', 'castro', 'vaini', 'taolanaro', 'salamiyah', 'butaritari', 'meulaboh', 'saint george', 'luderitz', 'suntar', 'rikitea', 'albany', 'cabo san lucas', 'kapaa', 'avarua', 'taolanaro', 'butaritari', 'bengkulu', 'baherden', 'tsaratanana', 'margate', 'svetlogorsk', 'airai', 'port macquarie', 'atuona', 'tuktoyaktuk', 'vestmannaeyjar', 'jamestown', 'batsfjord', 'new norfolk', 'bethel', 'illoqqortoormiut', 'attawapiskat', 'jieshi', 'hobart', 'georgetown', 'lakatoro', 'mataura', 'geraldton', 'ziro', 'belushya guba', 'atuona', 'gao', 'cherskiy', 'kodiak', 'castro', 'muncar', 'taolanaro', 'san patricio', 'itatskiy', 'vaini', 'floro', 'kodiak', 'hendijan', 'bluff', 'faanui', 'port alfred', 'rikitea', 'cabo san lucas', 'east london', 'neiafu', 'fredericton', 'torbay', 'souillac', 'taolanaro', 'mattru', 'colomi', 'tiksi', 'victor harbor', 'pevek', 'avarua', 'chokurdakh', 'jamestown', 'bredasdorp', 'kapaa', 'contamana', 'vaini', 'dikson', 'bambous virieux', 'ribeira grande', 'kerchevskiy', 'barentsburg', 'upernavik', 'youkounkoun', 'cape town', 'flin flon', 'belushya guba', 'kaitangata', 'qaanaaq', 'lebu', 'poum', 'rikitea', 'iqaluit', 'constitucion', 'yulara', 'opuwo', 'el alto', 'lamu', 'lapy', 'albany', 'luderitz', 'saskylakh', 'avarua', 'illoqqortoormiut', 'vestmannaeyjar', 'hermanus', 'nazare', 'illoqqortoormiut', 'tsaratanana', 'samusu', 'kodiak', 'pandan', 'bredasdorp', 'narsaq', 'victoria', 'mataura', 'chuguyevka', 'port alfred', 'moerai', 'taolanaro', 'hermanus', 'avarua', 'balyaga', 'kruisfontein', 'fairbanks', 'lieksa', 'port hardy', 'alofi', 'port alfred', 'illoqqortoormiut', 'takapau', 'tarauaca', 'iracoubo', 'hermanus', 'kayankulam', 'ancud', 'atuona', 'barentsburg', 'hobart', 'chokurdakh', 'jamestown', 'bethel', 'atuona', 'saint-joseph', 'taolanaro', 'ribeira grande', 'ossora', 'cape town', 'ushuaia', 'nuuk', 'wadena', 'chuy', 'vaini', 'vanimo', 'raudeberg', 'punta arenas', 'saldanha', 'broome', 'kuche', 'baherden', 'punta arenas', 'teya', 'tasiilaq', 'punta arenas', 'mar del plata', 'belushya guba', 'qaanaaq', 'saskylakh', 'atuona', 'punta arenas', 'shihezi', 'yulara', 'chuy', 'punta arenas', 'taolanaro', 'umm lajj', 'esperance', 'jamestown', 'karasburg', 'taolanaro', 'atuona', 'punta arenas', 'tiksi', 'gravdal', 'taolanaro', 'souillac', 'mys shmidta', 'qaanaaq', 'harper', 'bluff', 'novosil', 'cherskiy', 'ishlei', 'rikitea', 'sinkat', 'ushuaia', 'buchanan', 'jamestown', 'taksimo', 'monze', 'portland', 'saint-philippe', 'porto santo', 'windsor', 'marcona', 'vanavara', 'srednekolymsk', 'provideniya', 'cape town', 'north platte', 'nedjo', 'enterprise', 'phalombe', 'avera', 'port alfred', 'plettenberg bay', 'ushuaia', 'busselton', 'albany', 'punta arenas', 'pimentel', 'khatanga', 'warqla', 'punta arenas', 'iqaluit', 'hermanus', 'pevek', 'busselton', 'airai', 'bredasdorp', 'punta arenas', 'pozo colorado', 'suez', 'kapaa', 'tiksi', 'vaitupu', 'pevek', 'taolanaro', 'port-gentil', 'kapaa', 'albany', 'port alfred', 'shaoguan', 'flinders', 'taltal', 'bredasdorp', 'angra', 'hilo', 'cape town', 'kushima', 'agirish', 'tsihombe', 'swellendam', 'east london', 'arraial do cabo', 'kindu', 'barrow', 'mar del plata', 'airai', 'new norfolk', 'maneadero', 'rikitea', 'chuy', 'hermanus', 'avarua', 'sitka', 'punta arenas', 'hilo', 'hobart', 'puerto ayora', 'hobart', 'taolanaro', 'albany', 'mataura', 'cap malheureux', 'mar del plata', 'hilo', 'whitehorse', 'mataura', 'jamestown', 'thompson', 'emerald', 'half moon bay', 'grand river south east', 'bredasdorp', 'busselton', 'haines junction', 'kailua', 'nikolskoye', 'hualmay', 'atuona', 'avarua', 'lompoc', 'severo-kurilsk', 'nabire', 'bredasdorp', 'zhuhai', 'hamilton', 'angoram', 'bluff', 'comodoro rivadavia', 'qaqortoq', 'provideniya', 'port alfred', 'georgetown', 'chokurdakh', 'klaksvik', 'liwale', 'ambunti', 'taolanaro', 'portree', 'brae', 'cape town', 'kahului', 'bengkulu', 'ilulissat', 'bambous virieux', 'albany', 'margate', 'vieques', 'illoqqortoormiut', 'baraki barak', 'castro', 'atuona', 'ribeira grande', 'hithadhoo', 'castro', 'vaini', 'urumqi', 'mayo', 'viedma', 'tsihombe', 'egvekinot', 'midrand', 'guerrero negro', 'urusha', 'albany', 'carnarvon', 'puerto ayora', 'nikolskoye', 'bluff', 'castro', 'aviles', 'hasaki', 'cave spring', 'bredasdorp', 'sitrah', 'jibuti', 'hobart', 'port elizabeth', 'nemuro', 'khatanga', 'bilibino', 'cape town', 'arraial do cabo', 'deputatskiy', 'nacala', 'codrington', 'kongolo', 'mataura', 'ancud', 'pangnirtung', 'mataura', 'hermanus', 'praia', 'new norfolk', 'bereda', 'mataura', 'avarua', 'pisco', 'rikitea', 'busselton', 'barrow', 'zvishavane', 'la ronge', 'vestmannaeyjar', 'port alfred', 'nikolskoye', 'louisbourg', 'illoqqortoormiut', 'kapaa', 'vestmannaeyjar', 'taolanaro', 'tromso', 'carnarvon', 'kavieng', 'inuvik', 'rikitea', 'katsuura', 'ushuaia', 'punta arenas', 'zhangye', 'faanui', 'castro', 'pervouralsk', 'zhigansk', 'leh', 'paso de los toros', 'moussoro', 'puerto leguizamo', 'ponta do sol', 'saleaula', 'punta arenas', 'tuktoyaktuk', 'matara', 'hithadhoo', 'deputatskiy', 'ponta do sol', 'sar-e pul', 'zhigansk', 'tuktoyaktuk', 'yerbogachen', 'butaritari', 'felanitx', 'rikitea', 'huilong', 'busselton', 'paradwip', 'rikitea', 'east london', 'kintampo', 'bluff', 'axim', 'hithadhoo', 'grand-santi', 'kapaa', 'souillac', 'khatanga', 'ushuaia', 'jamestown', 'mataura', 'albany', 'mar del plata', 'grand gaube', 'kargasok', 'vaini', 'new norfolk', 'tuktoyaktuk', 'semey', 'puerto ayora', 'necochea', 'puerto leguizamo', 'lebu', 'butaritari', 'albany', 'mataura', 'ilulissat', 'ushuaia', 'hobart', 'ellwangen', 'busselton', 'carnarvon', 'sorland', 'barrow', 'tyrma', 'shubarkuduk', 'avarua', 'puerto leguizamo', 'half moon bay', 'hermanus', 'fort nelson', 'zhuanghe', 'rikitea', 'bluff', 'ushuaia', 'taoudenni', 'hilo', 'albany', 'guerrero negro', 'grand gaube', 'tromso', 'imperia', 'mataura', 'whitianga', 'korgen', 'longyearbyen', 'samusu', 'beringovskiy', 'dire', 'east london', 'saint-philippe', 'derzhavinsk', 'mount gambier', 'rikitea', 'ushuaia', 'taolanaro', 'karratha', 'kudahuvadhoo', 'mecca', 'busselton', 'bereda', 'bandarbeyla', 'mana', 'ushuaia', 'rikitea', 'abdanan', 'palabuhanratu', 'hobart', 'tasiilaq', 'rikitea', 'domoni', 'isla mujeres', 'taolanaro', 'avarua', 'tasiilaq', 'katsuura', 'saint-philippe', 'vostok', 'godinesti', 'port alfred', 'salalah', 'kahului', 'khatanga', 'westport', 'punta arenas', 'winston', 'baiyin', 'zachary', 'cape town', 'lamont', 'chuy', 'belushya guba', 'taolanaro', 'cherskiy', 'bengkulu', 'busselton', 'albany', 'hermanus', 'nemuro', 'ati', 'nanortalik', 'thompson', 'barrow', 'mataura', 'cusuna', 'arraial do cabo', 'bambous virieux', 'albany', 'qaanaaq', 'clyde river', 'kavieng', 'jamestown', 'barentsburg', 'belushya guba', 'mataura', 'dikson', 'yialos', 'bethel', 'port blair', 'chitral', 'georgetown', 'zhangjiakou', 'illoqqortoormiut', 'agadir', 'eura', 'atuona', 'iskateley', 'victoria', 'mataura', 'hobart', 'puerto leguizamo', 'ushuaia', 'albany', 'santa rosa', 'ushuaia', 'ribeira grande', 'upernavik', 'hithadhoo', 'pecos', 'la ronge', 'krasnoselkup', 'barrow', 'rikitea', 'xuddur', 'kasama', 'new norfolk', 'punta arenas', 'nikolskoye', 'varkkallai', 'roma', 'illoqqortoormiut', 'albany', 'albany', 'north bend', 'pytalovo', 'busselton', 'yellowknife', 'batagay', 'agadir', 'guerrero negro', 'matata', 'resen', 'mataura', 'cachoeira do sul', 'kaitangata', 'new norfolk', 'illoqqortoormiut', 'kapaa', 'albany', 'los llanos de aridane', 'tazovskiy', 'butaritari', 'tuktoyaktuk', 'cape town', 'chippewa falls', 'oranjemund', 'asau', 'carnarvon', 'mataura', 'hermanus', 'antsirabe', 'nikolskoye', 'mahebourg', 'albany', 'rikitea', 'mataura', 'areosa', 'kautokeino', 'busselton', 'punta arenas', 'shizunai', 'taolanaro', 'yellowknife', 'haines junction', 'taolanaro', 'ushuaia', 'rikitea', 'bredasdorp', 'new norfolk', 'hobart', 'avarua', 'somerset', 'mataura', 'saint-philippe', 'namatanai', 'egvekinot', 'castro', 'albany', 'barrow', 'khanu woralaksaburi', 'castro', 'yellowknife', 'mount gambier', 'auki', 'reconquista', 'butaritari', 'port alfred', 'daru', 'arraial do cabo', 'cape town', 'east london', 'rikitea', 'hermanus', 'busselton', 'rikitea', 'hilo', 'hithadhoo', 'khatanga', 'lavrentiya', 'barhi', 'bethalto', 'fairbanks', 'taolanaro', 'diamantino', 'cockburn town', 'busselton', 'avarua', 'meulaboh', 'hasaki', 'coquimbo', 'onega', 'abu dhabi', 'amderma', 'esperance', 'busselton', 'tartus', 'atuona', 'shingu', 'cam ranh', 'lata', 'geraldton', 'polunochnoye', 'busselton', 'bathsheba', 'kaiu', 'khatanga', 'aklavik', 'aflu', 'thompson', 'faanui', 'ushuaia', 'mataura', 'hobart', 'busselton', 'belushya guba', 'tasiilaq', 'san quintin', 'souillac', 'sergiyevsk', 'ushuaia', 'hermanus', 'tura', 'tasiilaq', 'yellowknife', 'katsuura', 'lydenburg', 'tiksi', 'bluff', 'verkhnevilyuysk', 'tumannyy', 'marcona', 'hermanus', 'victoria', 'mae hong son', 'nemuro', 'santiago del estero', 'dhidhdhoo', 'kapoeta', 'ushuaia', 'rikitea', 'ribeira grande', 'samarai', 'port blair', 'new norfolk', 'punta arenas', 'illoqqortoormiut', 'balabac', 'barrow', 'ushuaia', 'suceveni', 'olga', 'hilo', 'nizhneyansk', 'kruisfontein', 'thompson', 'east london', 'nanortalik', 'mataura', 'tasiilaq', 'bluff', 'barrow', 'det udom', 'chokurdakh', 'bluff', 'quang ngai', 'santa maria', 'bredasdorp', 'thompson', 'sovetskaya', 'laguna', 'saldanha', 'port alfred', 'albany', 'baneh', 'umzimvubu', 'hobart', 'vaini', 'hermanus', 'adrar', 'urengoy', 'camopi', 'portland', 'hobart', 'puerto el triunfo', 'berkak', 'qaanaaq', 'taolanaro', 'puerto escondido', 'punta arenas', 'kavieng', 'mahebourg', 'talnakh', 'felipe carrillo puerto', 'busselton', 'mount isa', 'constitucion', 'ribeira grande', 'albany', 'busselton', 'rikitea', 'busselton', 'progreso', 'hilo', 'san patricio', 'bambous virieux', 'lasa', 'itarema', 'la sarre', 'jamestown', 'georgetown', 'rikitea', 'hobart', 'port blair', 'bredasdorp', 'kavieng', 'khonuu', 'tabuk', 'saint-augustin', 'tuktoyaktuk', 'avarua', 'yellowknife', 'dikson', 'bluff', 'vostok', 'bakel', 'rolim de moura', 'cape town', 'victoria', 'qinhuangdao', 'norman wells', 'albany', 'carballo', 'namibe', 'shenjiamen', 'mataura', 'albany', 'ozgon', 'vrangel', 'petropavlovsk-kamchatskiy', 'dikson', 'bredasdorp', 'aljezur', 'saint-philippe', 'norman wells', 'luderitz', 'lebu', 'saldanha', 'torbay', 'dolores', 'albany', 'albany', 'atuona', 'palmer', 'bluff', 'stornoway', 'chapais', 'ancud', 'jamestown', 'mataura', 'nuuk', 'port alfred', 'avera', 'bredasdorp', 'wladyslawowo', 'punta arenas', 'chuy', 'tessalit', 'linhares', 'yarmouth', 'punta arenas', 'kaitangata', 'viedma', 'hermanus', 'qaanaaq', 'albany', 'east london', 'santa maria', 'vardo', 'kapustin yar', 'roslavl', 'northam', 'albany', 'tigil', 'faya', 'atuona', 'rikitea', 'hobart', 'vaitape', 'rio gallegos', 'yellowknife', 'ushuaia', 'bolshaya vishera', 'khatanga', 'mayo', 'busselton', 'lebu', 'albany', 'maniitsoq', 'avera', 'trincomalee', 'majene', 'busselton', 'omboue', 'moose factory', 'bonthe', 'tautira', 'barrow', 'tuktoyaktuk', 'illoqqortoormiut', 'lavrentiya', 'polessk', 'ahipara', 'cochrane', 'rancho palos verdes', 'mahebourg', 'saint anthony', 'san patricio', 'saint-pierre', 'ushuaia', 'fortuna', 'cape town', 'dieppe', 'patan', 'vikindu', 'rikitea', 'kampot', 'jamestown', 'sovetskiy', 'avarua', 'hithadhoo', 'uglovskoye', 'moratuwa', 'puerto ayora', 'hun', 'bluff', 'yellowknife', 'bluff', 'busselton', 'atuona', 'mercedes', 'ilheus', 'geraldton', 'grootfontein', 'cabo san lucas', 'punta arenas', 'half moon bay', 'kutum', 'upernavik', 'bethel', 'kavaratti', 'fortuna', 'mar del plata', 'hithadhoo', 'clyde river', 'antalaha', 'bredasdorp', 'punta arenas', 'kirovskiy', 'rikitea', 'pisco', 'atuona', 'maldonado', 'nikki', 'san ramon de la nueva oran', 'waingapu', 'oster', 'albany', 'dillon', 'beyneu', 'kaitangata', 'atuona', 'munai', 'yuli', 'ushuaia', 'avarua', 'buala', 'nyurba', 'sorland', 'ust-kuyga', 'nizhneyansk', 'port elizabeth', 'arlit', 'clovis', 'coquimbo', 'saskylakh', 'ures', 'zhezkazgan', 'port alfred', 'gizo', 'ushuaia', 'hobart', 'ushuaia', 'punta arenas', 'kurilsk', 'tevaitoa', 'bredasdorp', 'hagere hiywet', 'talnakh', 'sao joao da barra', 'lavrentiya', 'guerrero negro', 'carutapera', 'hornepayne', 'kodiak', 'hermanus', 'kodiak', 'kaitangata', 'gat', 'port elizabeth', 'ushuaia', 'hobart', 'yuzhno-yeniseyskiy', 'rikitea', 'marcona', 'jinka', 'cap malheureux', 'taolanaro', 'bur gabo', 'vila velha', 'dikson', 'rikitea', 'saint george', 'alofi', 'jiupu', 'belushya guba', 'severo-kurilsk', 'longview', 'rikitea', 'panama city', 'mayumba', 'vaitupu', 'vaini', 'albany', 'attawapiskat', 'muros', 'gorno-chuyskiy', 'kodiak', 'nsoko', 'rikitea', 'barentsburg', 'mahebourg', 'kurilsk', 'arraial do cabo', 'namibe', 'ureki', 'paramonga', 'bathsheba', 'dali', 'chanute', 'alofi', 'jamestown', 'darlowo', 'damietta', 'hermanus', 'provideniya', 'mataura', 'atuona', 'ushuaia', 'kodiak', 'atuona', 'ushuaia', 'dvinskoy', 'hilo', 'jamestown', 'saskylakh', 'ribeira grande', 'asyut', 'albany', 'albany', 'taolanaro', 'okhotsk', 'jamestown', 'ushuaia', 'cape town', 'samusu', 'hobart', 'urbana', 'sandavagur', 'juneau', 'nikolskoye', 'castro', 'busselton', 'ushuaia', 'sataua', 'punta arenas', 'mataura', 'busselton', 'albany', 'saint-philippe', 'yoichi', 'nikolskoye', 'hermanus', 'port hardy', 'saldanha', 'batagay-alyta', 'yanchukan', 'rikitea', 'rikitea', 'kropachevo', 'puerto ayora', 'tura', 'atuona', 'ushuaia', 'albany', 'mamallapuram', 'linxia', 'mataura', 'puerto ayora', 'mataura', 'illoqqortoormiut', 'talnakh', 'albany', 'axim', 'rikitea', 'iqaluit', 'novyy urengoy', 'east london', 'rikitea', 'albany', 'vysokogornyy', 'nizhneyansk']
    


```python
# eliminate duplicate cities and create a list of unique cities
ucities=[]
for i in cities:
    if i not in ucities:
        ucities.append(i)
ucities_df = pd.DataFrame({"City":ucities})
ucities_df.count()
```




    City    621
    dtype: int64




```python
# Save config information.
url = "http://api.openweathermap.org/data/2.5/weather?"
units = "imperial"

# Build partial query URL
query_url = f"{url}appid={api_key}&units={units}&q="

name = []
country = []
lat = []
lon = []
date = []
cloudiness = []
humidity = []
max_temp = []
wind_speed =[]


# Loop through the list of cities and perform a request for data on row
for index, row in ucities_df.iterrows():
    
    city = row["City"]
    
    print(query_url + str(city))
    response = requests.get(query_url + str(city)).json()
    
    try:
        name.append(response['name'])
        country.append(response['sys']['country'])
        lat.append(response['coord']['lat'])
        lon.append(response['coord']['lon'])
        date.append(response['dt'])
        cloudiness.append(response['clouds']['all'])
        humidity.append(response['main']['humidity'])
        max_temp.append(response['main']['temp_max'])
        wind_speed.append(response['wind']['speed'])
    except:
        print("Missing Field....Skip")       

```

    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=guerrero negro
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=souillac
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=somerset
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=fort nelson
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=bluff
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=mananjary
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=fallon
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=tawkar
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=clyde river
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=concordia
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=mataura
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=sitka
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=candawaga
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=tasiilaq
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=lesosibirsk
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=punta arenas
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=snyder
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=shakiso
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=atbasar
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=seoul
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=gat
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=albany
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=puerto baquerizo moreno
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=brae
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=jamestown
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=whitehorse
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=caravelas
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=thompson
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=vaini
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=arraial do cabo
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=cerro largo
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=port lincoln
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=grindavik
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=calvinia
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=hobart
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=wilmington
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=la ronge
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=katherine
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=kapaa
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=busselton
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=ribeira grande
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=chuy
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=ust-maya
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=trat
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=woodward
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=nikolskoye
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=marcona
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=lhokseumawe
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=illoqqortoormiut
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=cape town
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=grand gaube
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=carnarvon
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=krasnoarmeysk
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=saint george
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=vostok
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=marawi
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=prince rupert
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=kaitangata
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=irtyshskiy
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=dali
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=sao filipe
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=kavieng
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=hilo
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=castro
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=georgetown
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=sao joao da barra
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=quatre cocos
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=zhangye
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=provideniya
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=camacha
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=hermanus
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=ormstown
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=glendive
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=oktyabrskiy
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=makinsk
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=morros
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=chokurdakh
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=antalaha
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=port alfred
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=brownsville
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=cabo san lucas
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=bethel
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=vangaindrano
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=tuktoyaktuk
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=greenwood
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=luau
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=ponta delgada
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=sentyabrskiy
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=podyuga
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=khatanga
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=pevek
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=constitucion
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=victoria
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=bozdar
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=minot
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=verkhoshizhemye
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=esperance
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=gavle
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=ahipara
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=saskylakh
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=ponta do sol
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=manaure
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=tiksi
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=necochea
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=takoradi
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=norman wells
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=tarko-sale
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=puerto leguizamo
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=puerto asis
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=santa cruz
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=vista hermosa
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=srednekolymsk
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=rio cuarto
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=lebu
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=mehamn
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=sinazongwe
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=tuatapere
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=hamilton
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=kahului
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=galveston
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=charleston
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=attawapiskat
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=terme
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=karaul
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=chaihe
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=west wendover
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=phalaborwa
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=ajdabiya
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=luwuk
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=taolanaro
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=moscow
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=fortuna foothills
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=bulgan
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=san patricio
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=oleksandrivka
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=east london
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=binzhou
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=hithadhoo
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=kartaly
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=cozumel
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=longyearbyen
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=port augusta
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=jalu
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=dikson
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=tautira
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=atar
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=airai
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=miri
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=hambantota
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=cruzeiro do sul
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=mathathane
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=haukipudas
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=rodrigues alves
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=kermanshah
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=bredasdorp
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=atuona
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=touros
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=san cristobal
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=kobayashi
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=belushya guba
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=mount gambier
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=lingao
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=nouakchott
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=high level
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=corinto
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=coahuayana
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=saint-philippe
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=matamoros
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=port elizabeth
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=yar-sale
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=puerto ayora
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=tabuk
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=yakeshi
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=quelimane
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=putla
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=feijo
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=iqaluit
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=nizhneyansk
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=safonovo
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=new norfolk
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=kruisfontein
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=port macquarie
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=saleaula
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=solnechnyy
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=cocobeach
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=qaanaaq
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=faanui
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=brigantine
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=wanaka
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=mathbaria
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=grand centre
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=boa vista
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=yerbogachen
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=avarua
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=san borja
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=nibbar
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=yenagoa
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=pathein
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=kremenki
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=tranas
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=talnakh
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=trelleborg
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=areia branca
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=ostrovnoy
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=mys shmidta
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=ust-kuyga
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=auki
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=paamiut
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=turayf
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=cidreira
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=rungata
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=mareeba
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=hasaki
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=yellowknife
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=lagunas
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=mahebourg
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=upernavik
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=polson
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=winnemucca
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=latung
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=olafsvik
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=verkhoyansk
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=port blair
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=sibolga
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=sabha
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=dembi dolo
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=nanortalik
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=shimoda
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=south lake tahoe
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=vestmannaeyjar
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=tabou
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=buta
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=taoudenni
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=kirakira
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=salamiyah
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=butaritari
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=meulaboh
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=luderitz
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=suntar
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=bengkulu
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=baherden
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=tsaratanana
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=margate
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=svetlogorsk
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=batsfjord
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=jieshi
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=lakatoro
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=geraldton
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=ziro
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=gao
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=cherskiy
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=kodiak
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=muncar
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=itatskiy
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=floro
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=hendijan
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=neiafu
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=fredericton
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=torbay
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=mattru
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=colomi
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=victor harbor
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=contamana
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=bambous virieux
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=kerchevskiy
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=barentsburg
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=youkounkoun
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=flin flon
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=poum
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=yulara
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=opuwo
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=el alto
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=lamu
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=lapy
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=nazare
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=samusu
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=pandan
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=narsaq
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=chuguyevka
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=moerai
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=balyaga
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=fairbanks
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=lieksa
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=port hardy
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=alofi
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=takapau
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=tarauaca
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=iracoubo
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=kayankulam
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=ancud
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=saint-joseph
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=ossora
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=nuuk
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=wadena
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=vanimo
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=raudeberg
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=saldanha
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=broome
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=kuche
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=teya
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=mar del plata
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=shihezi
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=umm lajj
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=karasburg
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=gravdal
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=harper
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=novosil
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=ishlei
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=sinkat
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=buchanan
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=taksimo
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=monze
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=portland
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=porto santo
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=windsor
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=vanavara
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=north platte
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=nedjo
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=enterprise
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=phalombe
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=avera
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=plettenberg bay
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=pimentel
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=warqla
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=pozo colorado
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=suez
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=vaitupu
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=port-gentil
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=shaoguan
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=flinders
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=taltal
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=angra
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=kushima
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=agirish
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=tsihombe
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=swellendam
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=kindu
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=barrow
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=maneadero
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=cap malheureux
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=emerald
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=half moon bay
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=grand river south east
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=haines junction
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=kailua
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=hualmay
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=lompoc
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=severo-kurilsk
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=nabire
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=zhuhai
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=angoram
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=comodoro rivadavia
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=qaqortoq
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=klaksvik
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=liwale
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=ambunti
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=portree
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=ilulissat
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=vieques
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=baraki barak
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=urumqi
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=mayo
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=viedma
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=egvekinot
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=midrand
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=urusha
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=aviles
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=cave spring
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=sitrah
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=jibuti
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=nemuro
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=bilibino
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=deputatskiy
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=nacala
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=codrington
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=kongolo
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=pangnirtung
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=praia
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=bereda
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=pisco
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=zvishavane
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=louisbourg
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=tromso
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=inuvik
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=katsuura
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=pervouralsk
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=zhigansk
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=leh
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=paso de los toros
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=moussoro
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=matara
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=sar-e pul
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=felanitx
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=huilong
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=paradwip
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=kintampo
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=axim
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=grand-santi
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=kargasok
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=semey
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=ellwangen
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=sorland
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=tyrma
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=shubarkuduk
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=zhuanghe
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=imperia
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=whitianga
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=korgen
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=beringovskiy
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=dire
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=derzhavinsk
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=karratha
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=kudahuvadhoo
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=mecca
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=bandarbeyla
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=mana
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=abdanan
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=palabuhanratu
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=domoni
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=isla mujeres
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=godinesti
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=salalah
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=westport
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=winston
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=baiyin
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=zachary
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=lamont
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=ati
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=cusuna
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=yialos
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=chitral
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=zhangjiakou
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=agadir
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=eura
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=iskateley
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=santa rosa
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=pecos
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=krasnoselkup
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=xuddur
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=kasama
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=varkkallai
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=roma
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=north bend
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=pytalovo
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=batagay
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=matata
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=resen
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=cachoeira do sul
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=los llanos de aridane
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=tazovskiy
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=chippewa falls
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=oranjemund
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=asau
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=antsirabe
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=areosa
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=kautokeino
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=shizunai
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=namatanai
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=khanu woralaksaburi
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=reconquista
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=daru
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=lavrentiya
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=barhi
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=bethalto
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=diamantino
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=cockburn town
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=coquimbo
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=onega
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=abu dhabi
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=amderma
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=tartus
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=shingu
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=cam ranh
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=lata
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=polunochnoye
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=bathsheba
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=kaiu
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=aklavik
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=aflu
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=san quintin
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=sergiyevsk
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=tura
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=lydenburg
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=verkhnevilyuysk
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=tumannyy
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=mae hong son
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=santiago del estero
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=dhidhdhoo
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=kapoeta
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=samarai
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=balabac
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=suceveni
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=olga
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=det udom
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=quang ngai
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=santa maria
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=sovetskaya
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=laguna
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=baneh
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=umzimvubu
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=adrar
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=urengoy
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=camopi
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=puerto el triunfo
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=berkak
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=puerto escondido
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=felipe carrillo puerto
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=mount isa
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=progreso
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=lasa
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=itarema
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=la sarre
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=khonuu
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=saint-augustin
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=bakel
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=rolim de moura
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=qinhuangdao
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=carballo
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=namibe
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=shenjiamen
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=ozgon
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=vrangel
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=petropavlovsk-kamchatskiy
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=aljezur
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=dolores
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=palmer
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=stornoway
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=chapais
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=wladyslawowo
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=tessalit
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=linhares
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=yarmouth
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=vardo
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=kapustin yar
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=roslavl
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=northam
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=tigil
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=faya
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=vaitape
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=rio gallegos
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=bolshaya vishera
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=maniitsoq
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=trincomalee
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=majene
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=omboue
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=moose factory
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=bonthe
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=polessk
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=cochrane
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=rancho palos verdes
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=saint anthony
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=saint-pierre
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=fortuna
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=dieppe
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=patan
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=vikindu
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=kampot
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=sovetskiy
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=uglovskoye
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=moratuwa
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=hun
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=mercedes
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=ilheus
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=grootfontein
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=kutum
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=kavaratti
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=kirovskiy
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=maldonado
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=nikki
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=san ramon de la nueva oran
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=waingapu
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=oster
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=dillon
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=beyneu
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=munai
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=yuli
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=buala
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=nyurba
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=arlit
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=clovis
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=ures
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=zhezkazgan
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=gizo
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=kurilsk
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=tevaitoa
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=hagere hiywet
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=carutapera
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=hornepayne
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=yuzhno-yeniseyskiy
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=jinka
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=bur gabo
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=vila velha
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=jiupu
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=longview
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=panama city
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=mayumba
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=muros
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=gorno-chuyskiy
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=nsoko
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=ureki
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=paramonga
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=chanute
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=darlowo
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=damietta
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=dvinskoy
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=asyut
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=okhotsk
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=urbana
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=sandavagur
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=juneau
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=sataua
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=yoichi
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=batagay-alyta
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=yanchukan
    Missing Field....Skip
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=kropachevo
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=mamallapuram
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=linxia
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=novyy urengoy
    http://api.openweathermap.org/data/2.5/weather?appid=001cb4047126b7e1045f314140e201af&units=imperial&q=vysokogornyy
    


```python
# update the data with the list of cities recognizable by openweathermap
ucities_df = pd.DataFrame({"City":name})
# add all data to rows for every column
ucities_df["City"] = pd.Series(name, index=ucities_df.index) 
ucities_df["Country"] = pd.Series(country, index=ucities_df.index)
ucities_df["Lat"] = pd.Series(lat, index=ucities_df.index)
ucities_df["Lon"] = pd.Series(lon, index=ucities_df.index)
ucities_df["Date"] = pd.Series(date, index=ucities_df.index)
ucities_df["Cloudiness"] = pd.Series(cloudiness, index=ucities_df.index)
ucities_df["Humidity"] = pd.Series(humidity, index=ucities_df.index)
ucities_df["Max Temp"] = pd.Series(max_temp, index=ucities_df.index)
ucities_df["Wind Speed"] = pd.Series(wind_speed, index=ucities_df.index)
#print data frame
ucities_df.count()
```




    City          563
    Country       563
    Lat           563
    Lon           563
    Date          563
    Cloudiness    563
    Humidity      563
    Max Temp      563
    Wind Speed    563
    dtype: int64




```python
# dispaly cities data frame.
ucities_df.head()
```




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
      <th>City</th>
      <th>Country</th>
      <th>Lat</th>
      <th>Lon</th>
      <th>Date</th>
      <th>Cloudiness</th>
      <th>Humidity</th>
      <th>Max Temp</th>
      <th>Wind Speed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Guerrero Negro</td>
      <td>MX</td>
      <td>27.97</td>
      <td>-114.04</td>
      <td>1528688132</td>
      <td>0</td>
      <td>73</td>
      <td>67.33</td>
      <td>10.11</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Rikitea</td>
      <td>PF</td>
      <td>-23.12</td>
      <td>-134.97</td>
      <td>1528688132</td>
      <td>76</td>
      <td>100</td>
      <td>73.99</td>
      <td>19.73</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Souillac</td>
      <td>FR</td>
      <td>45.60</td>
      <td>-0.60</td>
      <td>1528687800</td>
      <td>36</td>
      <td>100</td>
      <td>60.80</td>
      <td>9.17</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Somerset</td>
      <td>US</td>
      <td>37.09</td>
      <td>-84.60</td>
      <td>1528685760</td>
      <td>90</td>
      <td>88</td>
      <td>73.40</td>
      <td>3.36</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Fort Nelson</td>
      <td>CA</td>
      <td>58.81</td>
      <td>-122.69</td>
      <td>1528686000</td>
      <td>40</td>
      <td>25</td>
      <td>66.20</td>
      <td>12.75</td>
    </tr>
  </tbody>
</table>
</div>




```python
# plot temperature vs. Latitude
temp_plot = plt.scatter(lat, max_temp, marker="o", facecolors="red", edgecolors="black", alpha=0.75)
plt.title("Temperatrue of Random Cities from the Equator")
plt.xlabel("Latitude")
plt.ylabel("Max Tempreture F")
plt.grid(True)
plt.show()
```


![png](output_7_0.png)



```python
# plot humidity percent vs. Latitude
humidity_plot = plt.scatter(lat, humidity, marker="X", facecolors="blue", edgecolors="black", alpha=0.75)
plt.title("Percent Humidity of Random Cities from the Equator")
plt.xlabel("Latitude")
plt.ylabel("% Humidity")
plt.grid(True)
plt.show()
```


![png](output_8_0.png)



```python
# plot cloudiness percent vs. Latitude
cloud_plot = plt.scatter(lat, cloudiness, marker="o", facecolors="brown", edgecolors="black", alpha=0.9)
plt.title("Percent Cloudiness of Random Cities from the Equator")
plt.xlabel("Latitude")
plt.ylabel("% Cloudiness")
plt.grid(True)
plt.show()
```


![png](output_9_0.png)



```python
# plot wind speed vs. Latitude
wind_plot = plt.scatter(lat, wind_speed, marker="X", facecolors="orange", edgecolors="black", alpha=0.9)
plt.title("Wind Speed of Random Cities from the Equator")
plt.xlabel("Latitude")
plt.ylabel("Wind Speed")
plt.grid(True)
plt.show()
```


![png](output_10_0.png)

