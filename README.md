from urllib.request import urlopen
from urllib.error import URLError
from urllib.error import HTTPError
from bs4 import BeautifulSoup
def getTitle(url):
    try:
        html = urlopen(url)
    except URLError as e:
        return None
    except HTTPError as e:
        return None
    try:
        bs = BeautifulSoup(html, 'html.parser')
        title = bs.find_all('span', {'class':'green'})
    except AttributeError as e:
        return None
    return title

title = getTitle('http://www.pythonscraping.com/pages/warandpeace.html')    
if title == None:
    print('title is not found')
else:
    for name in title:
        print(name.text)
