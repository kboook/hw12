# hw12
import requests
url = 'https://www.vox.com/2018/9/25/17901082/trump-un-2018-speech-full-text'
r = requests.get(url)
r.encoding = 'utf8'
data = str(r.text)
text = data[data.find('Madam'):data.rfind('Thank you')+9]

text = text.replace('"','')
text = text.replace("'",'')
text = text.replace('.','')
text = text.replace(',','')
text = text.replace('</p>','')
text = text.replace('(','')
text = text.replace(')','')
text = text.replace('\n','')
text = text.replace('-','')
text = text.replace('–','')
text = text.replace('$','')
while '<' in text:
    text = text.replace(text[text.find('<'):text.find('<')+13],'')

    
mydict = {}
words = text.split()

for w in words:
    if w in mydict:
        mydict[w] += 1
    else:
        mydict[w] = 1
print('20words that Trump used mostly in his 2018 UN speech')
for k in sorted(mydict, key=mydict.__getitem__, reverse=True):
    if sorted(mydict, key=mydict.__getitem__, reverse=True).index(k) < 20:
        print('%s: %s'%(k, mydict[k]))
    else:
        break
