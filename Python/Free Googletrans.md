## Free Googletrans

### 패키지 설치

```
pip install googletrans
```

### 기본 사용방법

```python
from googletrans import Translator
tarnslator = Translator()

tr_results = translator.translate('안녕하세요.')
print('Trans(EN): {1}, {2}, {3}'.format(tr_result.text, tr_result.src, tr_result.dest))
```

--------

```python
Trans(EN): Hi, ko en
```

아무것도 입력하지 않는 경우 source = auto, destination = english 가 기본 셋팅



### 다른 언어로 번역

```python
from googletrans import Translator
tarnslator = Translator()

tr_results = translator.translate('안녕하세요.', src='ko'm dest='ja')
print('Trans(JA): {0}, {1}, {2}'.format(tr_result.text, tr_result.src, tr_result.dest))
```

-------

```python
Trans(JA): こんにちは。 Kon'nichiwa.
```



### 번역 가능한 언어 확인

```python
import googletrans
print(googletrans.LANGUAGES)
```

------

```python
{'gu': 'gujarati', 'gd': 'scots gaelic', 'ga': 'irish', 'gl': 'galician', 'lb': 'luxembourgish', 'la': 'latin', 'lo': 'lao', 'tr': 'turkish', 'lv': 'latvian', 'lt': 'lithuanian', 'th': 'thai', 'tg': 'tajik', 'te': 'telugu', 'fil': 'Filipino', 'haw': 'hawaiian', 'yi': 'yiddish', 'ceb': 'cebuano', 'yo': 'yoruba', 'de': 'german', 'da': 'danish', 'el': 'greek', 'eo': 'esperanto', 'en': 'english', 'eu': 'basque', 'et': 'estonian', 'es': 'spanish', 'ru': 'russian', 'zh-cn': 'chinese (simplified)', 'ro': 'romanian', 'be': 'belarusian', 'bg': 'bulgarian', 'uk': 'ukrainian', 'bn': 'bengali', 'jw': 'javanese', 'bs': 'bosnian', 'ja': 'japanese', 'xh': 'xhosa', 'co': 'corsican', 'ca': 'catalan', 'cy': 'welsh', 'cs': 'czech', 'ps': 'pashto', 'pt': 'portuguese', 'zh-tw': 'chinese (traditional)', 'tl': 'filipino', 'pa': 'punjabi', 'vi': 'vietnamese', 'pl': 'polish', 'hy': 'armenian', 'hr': 'croatian', 'ht': 'haitian creole', 'hu': 'hungarian', 'hmn': 'hmong', 'hi': 'hindi', 'ha': 'hausa', 'he': 'Hebrew', 'mg': 'malagasy', 'uz': 'uzbek', 'ml': 'malayalam', 'mn': 'mongolian', 'mi': 'maori', 'mk': 'macedonian', 'ur': 'urdu', 'mt': 'maltese', 'ms': 'malay', 'mr': 'marathi', 'ta': 'tamil', 'my': 'myanmar (burmese)', 'af': 'afrikaans', 'sw': 'swahili', 'is': 'icelandic', 'am': 'amharic', 'it': 'italian', 'iw': 'hebrew', 'sv': 'swedish', 'ar': 'arabic', 'su': 'sundanese', 'zu': 'zulu', 'az': 'azerbaijani', 'id': 'indonesian', 'ig': 'igbo', 'nl': 'dutch', 'no': 'norwegian', 'ne': 'nepali', 'ny': 'chichewa', 'fr': 'french', 'ku': 'kurdish (kurmanji)', 'fy': 'frisian', 'fa': 'persian', 'fi': 'finnish', 'ka': 'georgian', 'kk': 'kazakh', 'sr': 'serbian', 'sq': 'albanian', 'ko': 'korean', 'kn': 'kannada', 'km': 'khmer', 'st': 'sesotho', 'sk': 'slovak', 'si': 'sinhala', 'so': 'somali', 'sn': 'shona', 'sm': 'samoan', 'sl': 'slovenian', 'ky': 'kyrgyz', 'sd': 'sindhi'}
```

총 106개의 언어 확인



### service URL 변경

```
translator = Transaltor(service_urls=[
	'translate.google.com',
	'translate.google.co.kr',
])
```



### list로 된 여러 문장 번역하기

```python
translations = translator.translate(['The quick brown fox', 'jumps over', 'the lazy dog'], dest='ko')
for translation in translations:
	print('{0} -> {1}'.format(translation.origin, translation.text))
```

-----

```
The quick brown fox  ->  빠른 갈색 여우
jumps over  ->  점프하다
the lazy dog  ->  게으른 개
```



### 언어 탐색

```python
print translator.detect('이 문장은 한글로 쓰여졌습니다.')
print translator.detect('この文章は日本語で書かれました。')
print translator.detect('This sentence is written in English.')
print translator.detect('Tiu frazo estas skribita en Esperanto.')
print translator.detect('Esta frase está escrita en coreano.')
```

-----

```python
Detected(lang=ko, confidence=1)
Detected(lang=ja, confidence=1)
Detected(lang=en, confidence=1)
Detected(lang=eo, confidence=1)
Detected(lang=es, confidence=0.85902715)
```



## References

`https://github.com/ssut/py-googletrans`