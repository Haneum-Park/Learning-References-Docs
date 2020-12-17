```python
from konlpy.tag import Okt
okt = Okt()

textList = """
2019 새로운 한국어 인 스타일 수집 높은 허리 커버 배꼽 얇은 섹시한 비키니 세 조각 수영복 여성이었다
섹시한 수영복 여성 샴 요정 팬 작은 가슴 수집 스틸 케어 스파 배꼽 배 삼각형 기능 바람 수영복
중년 및 노인 수영복 여성 어머니 분할 느슨한 보수적 인 대형 온천 목욕 지방 mm은 얇은 수영복이었다
온천 수영복 여성 한국어 기능 커버 배는 얇은 섹시한 원피스 블랙 2019 큰 뚱뚱한 mm 수영복 수영복이었다
수영복 여성 감각 원피스 삼각형 작은 가슴은 슬림 커버 배꼽 온천 플러스 사이즈 한국의 그물 빨간 수영복을 수집
수영복 여성 휴가 새로운 원피스 긴 소매 커버 배는 얇은 섹시한 작은 가슴 기능 그물 레드 슈퍼 요정 해변 수영복이었다
섹시 수영복 여성 원피스 작은 가슴 모여 온천 한국어 그물 레드 패션 2019 새로운 다시 수영복
수영복 여성 온천 작은 가슴 배꼽을 커버하기 위해 모여 얇은 섹시한 한국 보수적 샴 복서 ins 스타일 수영복이었다
수영복 여성 복부 배는 얇은 보수적 인 요정 팬 샴 섹시 플러스 크기 2019 새로운 기능 바람 온천 수영복이었다
온천 휴가 섹시한 수영장 여왕 복고풍 등이없는 보수적 수영복 여성 작은 가슴은 얇은 삼각형 원피스 수영복 여성이었다
그물 빨간 수영복 여성 2019 새로운 조류 온천 커버 고기는 얇은 한국 대형 지방 mm 커버 배꼽 바람 바람 보수적이었다
수영복 여성 보수적 커버 배꼽은 얇은 분할 학생 수영복 인 한국 작은 향기로운 소녀 온천이었다
2019 새로운 원피스 스커트 수영복 여성 얇은 얇은 배꼽 작은 가슴 수집 겨울 스파 수영복 보수적 인 바람
수영복 여성 3 피스 요정 팬 분할 보수적 인 보수적 배는 얇은 섹시한 한국인 학생 온천 수영복이었다
온천 수영복 여성 2019 New Black 보수적 슬리밍 배 취재 한 조각 Sexy Fairy 팬 Bubble Hot Spring 수영복
수영복 여성 3 피스 요정 팬 분할 보수적 인 보수적 배는 얇은 섹시한 한국인 학생 온천 수영복이었다
"""

for text in textList.split('\n'):
    print(okt.morphs(text))
    print(okt.morphs(text, stem=True))
    print(okt.nouns(text))
    print(okt.phrases(text))
    print ("-------------------------------------")
```

```python
from konlpy.tag import Kkma

kkma = Kkma()

for text in textList.split('\n'):
    print(kkma.pos(text))
```

```
import bisect
import itertools
import random

import nltk
from konlpy.corpus import kolaw
from konlpy.tag import Mecab # MeCab tends to reserve the original form of morphemes


"""
def generate_sentence(cfdist, word, num=15):
    sentence = []

    # Generate words until we meet a period
    while word!='.':
        sentence.append(word)

        # Generate the next word based on probability
        choices, weights = zip(*cfdist[word].items())
        cumdist = list(itertools.accumulate(weights))
        x = random.random() * cumdist[-1]
        word = choices[bisect.bisect(cumdist, x)]

    return ' '.join(sentence)


def calc_cfd(doc):
    # Calculate conditional frequency distribution of bigrams
    words = [w for w, t in Mecab().pos(doc)]
    bigrams = nltk.bigrams(words)
    return nltk.ConditionalFreqDist(bigrams)


if __name__=='__main__':
    nsents = 5 # Number of sentences
    initstr = u'국가' # Try replacing with u'국가', u'대통령', etc

    doc = kolaw.open('constitution.txt').read()
    #doc = textList
    cfd = calc_cfd(doc)

    for i in range(nsents):
        print('%d. %s' % (i, generate_sentence(cfd, initstr)))
"""
```

```python
def calc_cfd(doc):
    # Calculate conditional frequency distribution of bigrams
    words = [w for w, t in Mecab().pos(doc)]
    bigrams = nltk.bigrams(words)
    return nltk.ConditionalFreqDist(bigrams)


doc = open('./names.txt').read()
cfdist = calc_cfd(doc)



word="2019"
count = 0
while True:
    choices, weights = zip(*cfdist[word].items())
    cumdist = list(itertools.accumulate(weights))
    x = random.random() * cumdist[-1]
    word = (choices[bisect.bisect(cumdist, x)])
    print (word)
    count += 1
    if(count == 5):
        break
```

```python
# -*- coding: utf-8 -*-

import konlpy
import nltk

# POS tag a sentence
sentence = u'온천 수영복 여성 2019 New Black 보수적 슬리밍 배 취재 한 조각 Sexy Fairy 팬 Bubble Hot Spring 수영복'
words = konlpy.tag.Twitter().pos(sentence)

# Define a chunk grammar, or chunking rules, then chunk
grammar = """
NP: {<N.*>*<Suffix>?}   # Noun phrase
VP: {<V.*>*}            # Verb phrase
AP: {<A.*>*}            # Adjective phrase
"""
parser = nltk.RegexpParser(grammar)
chunks = parser.parse(words)
print("# Print whole tree")
print(chunks.pprint())

print("\n# Print noun phrases only")

npList = []
apList = []

def Get_Score(word, grammar):
    score = 0
    
    if(grammar == 'Adjective'):
        score = 10
    elif(word.count('여성')):
        score = 3
    elif(word.count('수영복')):
        score = 2
    elif(word.isnumeric()):
        if(len(word) > 2):
            score = 11
        else:
            score = -1
    elif(word.count('섹시')):
        score = 9

    return score
        

for subtree in chunks.subtrees():
    if subtree.label() in ['NP','AP']:
        for e in list(subtree):
            if(e[1] == "Adjective"):
                apList.append(e)
                continue
            
            print (e)
            DUP = False
            for x in npList:
                if(x[0] == e[0]):
                    DUP = True
            if(DUP == True):
                continue

            
            score = Get_Score(e[0],e[1])
            
            if(e[1] == 'Suffix'):
                npList[-1][0] = "{}{}".format(npList[-1][0],e[0])
                npList[-1][1] = 8
            else:
                npList.append([e[0],score])



npList = sorted(npList, key = lambda x : x[1], reverse= True)

print(apList)
print(npList)
```

```python
#sentence = u'수영복 여성 3 피스 요정 팬 분할 보수적 인 보수적 배는 얇은 섹시한 한국인 학생 온천 수영복이었다'

sentenceList = []
cur_index = 0
for index,row in enumerate(npList):
    if(row[1] > 9):
        sentenceList.append(row[0])
        cur_index = index

try:
    sentenceList.append(apList[1][0])
except:
    pass
try:
    sentenceList.append(apList[0][0])
except:
    pass

sentenceList.append(npList[cur_index+1][0])
cur_index += 1
sentenceList.append(npList[cur_index+1][0])
cur_index += 1
sentenceList.append(npList[cur_index+2][0])
sentenceList.append(npList[cur_index+1][0])
cur_index += 2
        
print("원 제목 : {}".format(sentence))
print("축약된 제목 :", ' '.join(sentenceList))
            
```

```
2019 새로운 한국어 인 스타일 수집 높은 허리 커버 배꼽 얇은 섹시한 비키니 세 조각 수영복 여성이었다
섹시한 수영복 여성 샴 요정 팬 작은 가슴 수집 스틸 케어 스파 배꼽 배 삼각형 기능 바람 수영복
중년 및 노인 수영복 여성 어머니 분할 느슨한 보수적 인 대형 온천 목욕 지방 mm은 얇은 수영복이었다
온천 수영복 여성 한국어 기능 커버 배는 얇은 섹시한 원피스 블랙 2019 큰 뚱뚱한 mm 수영복 수영복이었다
수영복 여성 감각 원피스 삼각형 작은 가슴은 슬림 커버 배꼽 온천 플러스 사이즈 한국의 그물 빨간 수영복을 수집
수영복 여성 휴가 새로운 원피스 긴 소매 커버 배는 얇은 섹시한 작은 가슴 기능 그물 레드 슈퍼 요정 해변 수영복이었다
섹시 수영복 여성 원피스 작은 가슴 모여 온천 한국어 그물 레드 패션 2019 새로운 다시 수영복
수영복 여성 온천 작은 가슴 배꼽을 커버하기 위해 모여 얇은 섹시한 한국 보수적 샴 복서 ins 스타일 수영복이었다
수영복 여성 복부 배는 얇은 보수적 인 요정 팬 샴 섹시 플러스 크기 2019 새로운 기능 바람 온천 수영복이었다
온천 휴가 섹시한 수영장 여왕 복고풍 등이없는 보수적 수영복 여성 작은 가슴은 얇은 삼각형 원피스 수영복 여성이었다

name.txt 내용
```

