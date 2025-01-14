[toc]

## 22.1 Fetching files
### 22.1.1 Using Python to fetch files from an FTP server
```python

>>> import ftplib
>>> ftp = ftplib.FTP('tgftp.nws.noaa.gov')
>>> ftp.login()
'230 Login successful.'

>>> ftp.cwd('data')
'250 Directory successfully changed.'
>>> ftp.nlst()
['climate', 'fnmoc', 'forecasts', 'hurricane_products', 'ls_SS_services', 'marine', 'nsd_bbsss.txt', 'nsd_cccc.txt', 'observations', 'products', 'public_statement', 'raw', 'records', 'summaries', 'tampa', 'watches_warnings', 'zonecatalog.curr', 'zonecatalog.curr.tar']


>>> x = ftp.retrbinary('RETR observations/metar/decoded/KORD.TXT', open('KORD.TXT', 'wb').write)
'226 Transfer complete.'

```
### 22.1.2 Fetching files with SFTP
```python

>>> import paramiko
>>> t = paramiko.Transport((hostname, port))
>>> t.connect(username, password)
>>> sftp = paramiko.SFTPClient.from_transport(t)

```
### 22.1.3 Retrieving files over HTTP/HTTPS
```python

>>> import requests 
>>> response = requests.get("http://www.metoffice.gov.uk/pub/data/weather/uk/climate/stationdata/heathrowdata.txt")


>>> print(response.text)
Heathrow (London Airport)
Location 507800E 176700N, Lat 51.479 Lon -0.449, 25m amsl
Estimated data is marked with a * after the value.
Missing data (more than 2 days missing in month) is marked by  ---.
Sunshine data taken from an automatic Kipp & Zonen sensor marked with a #, otherwise sunshine data taken from a Campbell Stokes recorder.
   yyyy  mm   tmax    tmin      af    rain     sun
              degC    degC    days      mm   hours
   1948   1    8.9     3.3    ---     85.0    ---
   1948   2    7.9     2.2    ---     26.0    ---
   1948   3   14.2     3.8    ---     14.0    ---
   1948   4   15.4     5.1    ---     35.0    ---
   1948   5   18.1     6.9    ---     57.0    ---

```
## 22.2 Fetching data via an API
```python

>>> import requests
>>> response = requests.get("http://marsweather.ingenology.com/v1/latest/?format=json")
>>> response.text
'{"report": {"terrestrial_date": "2017-01-08", "sol": 1573, "ls": 295.0, "min_temp": -74.0, "min_temp_fahrenheit": -101.2, "max_temp": -2.0, "max_temp_fahrenheit": 28.4, "pressure": 872.0, "pressure_string": "Higher", "abs_humidity": null, "wind_speed": null, "wind_direction": "--", "atmo_opacity": "Sunny", "season": "Month 10", "sunrise": "2017-01-08T12:29:00Z", "sunset": "2017-01-09T00:45:00Z"}}'
>>> response = requests.get("http://marsweather.ingenology.com/v1/archive/?sol=155&format=json")
>>> response.text
'{"count": 1, "next": null, "previous": null, "results": [{"terrestrial_date": "2013-01-18", "sol": 155, "ls": 243.7, "min_temp": -64.45, "min_temp_fahrenheit": -84.01, "max_temp": 2.15, "max_temp_fahrenheit": 35.87, "pressure": 9.175, "pressure_string": "Higher", "abs_humidity": null, "wind_speed": 2.0, "wind_direction": null, "atmo_opacity": null, "season": "Month 9", "sunrise": null, "sunset": null}]}'

```

## 22.3 Structured data formats
### 22.3.1 JSON data
```python

>>> import json
>>> import requests
>>> response = requests.get("http://marsweather.ingenology.com/v1/latest/?format=json")
>>> weather = json.loads(response.text)
>>> weather
{'report': {'terrestrial_date': '2017-01-10', 'sol': 1575, 'ls': 296.0, 'min_temp': -58.0, 'min_temp_fahrenheit': -72.4, 'max_temp': 0.0, 'max_temp_fahrenheit': None, 'pressure': 860.0, 'pressure_string': 'Higher', 'abs_humidity': None, 'wind_speed': None, 'wind_direction': '--', 'atmo_opacity': 'Sunny', 'season': 'Month 10', 'sunrise': '2017-01-10T12:30:00Z', 'sunset': '2017-01-11T00:46:00Z'}}
>>> weather['report']['sol']
1575

>>> from pprint import pprint as pp
>>> pp(weather)
{'report': {'abs_humidity': None,
            'atmo_opacity': 'Sunny',
            'ls': 296.0,
            'max_temp': 0.0,
            'max_temp_fahrenheit': None,
            'min_temp': -58.0,
            'min_temp_fahrenheit': -72.4,
            'pressure': 860.0,
            'pressure_string': 'Higher',
            'season': 'Month 10',
            'sol': 1575,
            'sunrise': '2017-01-10T12:30:00Z',
            'sunset': '2017-01-11T00:46:00Z',
            'terrestrial_date': '2017-01-10',
            'wind_direction': '--',
            'wind_speed': None}}

>>> outfile = open("mars_data_01.json", "w")
>>> json.dump(weather, outfile)
>>> outfile.close()
>>> json.dumps(weather)
'{"report": {"terrestrial_date": "2017-01-11", "sol": 1576, "ls": 296.0, "min_temp": -72.0, "min_temp_fahrenheit": -97.6, "max_temp": -1.0, "max_temp_fahrenheit": 30.2, "pressure": 869.0, "pressure_string": "Higher", "abs_humidity": null, "wind_speed": null, "wind_direction": "--", "atmo_opacity": "Sunny", "season": "Month 10", "sunrise": "2017-01-11T12:31:00Z", "sunset": "2017-01-12T00:46:00Z"}}'



>>> print(json.dumps(weather, indent=2))
{
  "report": {
    "terrestrial_date": "2017-01-10",
    "sol": 1575,
    "ls": 296.0,
    "min_temp": -58.0,
    "min_temp_fahrenheit": -72.4,
    "max_temp": 0.0,
    "max_temp_fahrenheit": null,
    "pressure": 860.0,
    "pressure_string": "Higher",
    "abs_humidity": null,
    "wind_speed": null,
    "wind_direction": "--",
    "atmo_opacity": "Sunny",
    "season": "Month 10",
    "sunrise": "2017-01-10T12:30:00Z",
    "sunset": "2017-01-11T00:46:00Z"
  }
}

>>> outfile = open("mars_data.json", "w")
>>> for report in weather_list:
...     json.dump(weather, outfile) 
>>> outfile.close()


>>> for line in open("mars_data.json"):
...     weather_list.append(json.loads(line))


>>> outfile = open("mars_data.json", "w")
>>> weather_obj = {"reports": weather_list, "count": 2} 
>>> json.dump(weather, outfile)
>>> outfile.close()


>>> with open("mars_data.json") as infile:
>>> weather_obj = json.load(infile)

```
### 22.3.2 XML data
```python

>>> import xmltodict
>>> data = xmltodict.parse(open("observations_01.xml").read())

```
## 22.4 Scraping web data
```python

>>> import bs4
>>> html = open("test.html").read()
>>> bs = bs4.BeautifulSoup(html, "html.parser")


>>> a_list = bs("a")
>>> print(a_list)
[<a href="http://bitbucket.dev.null">link</a>]


>>> a_item = a_list[0]
>>> a_item.text
'link'
>>> a_item["href"]
'http://bitbucket.dev.null'


>>> special_list = bs.select(".special")
>>> print(special_list)
[<span class="special">this is special</span>]
>>> special_item = special_list[0]
>>> special_item.text
'this is special'
>>> special_item["class"]
['special']


```