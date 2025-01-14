[toc]

## 21.2 Reading text files
### 21.2.1 Text encoding – ASCII, Unicode, and others
```python

>>> open('test.txt', 'wb').write(bytes([65, 66, 67, 255, 192,193]))
6

>>> x = open('test.txt').read()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "/usr/local/lib/python3.6/codecs.py", line 321, in decode
    (result, consumed) = self._buffer_decode(data, self.errors, final)
UnicodeDecodeError: 'utf-8' codec can't decode byte 0xff in position 3: invalid start byte


>>> open('test.txt', errors='ignore').read()
'ABC'
>>> open('test.txt', errors='replace').read()
'ABC���'
>>> open('test.txt', errors='surrogateescape').read()
'ABC\udcff\udcc0\udcc1'
>>> open('test.txt', errors='backslashreplace').read()
'ABC\\xff\\xc0\\xc1'
>>>

```
### 21.2.2 Unstructured text
```python

>>> moby_text = open("moby_01.txt").read()          #A reads all of file as a single string
>>> moby_paragraphs = moby_text.split("\n\n")       #B Splits on two newlines together
>>> print(moby_paragraphs[1])
There now is your insular city of the Manhattoes, belted round by wharves
as Indian isles by coral reefs--commerce surrounds it with her surf.
Right and left, the streets take you waterward.  Its extreme downtown
is the battery, where that noble mole is washed by waves, and cooled
by breezes, which a few hours previous were out of sight of land.
Look at the crowds of water-gazers there.



>>> moby_text = open("moby_01.txt").read()          #A reads all of file as a single string
>>> moby_paragraphs = moby_text.split("\n\n")       
>>> moby = moby_paragraphs[1].lower()                   #B Makes everything lower case
>>> moby = moby.replace(".", "")          #C Removes periods
>>> moby = moby.replace(",", "") 
>>> moby_words = moby.split()
>>> print(moby_words)
['there', 'now', 'is', 'your', 'insular', 'city', 'of', 'the', 'manhattoes,', 'belted', 'round', 'by', 'wharves', 'as', 'indian', 'isles', 'by', 'coral', 'reefs--commerce', 'surrounds', 'it', 'with', 'her', 'surf', 'right', 'and', 'left,', 'the', 'streets', 'take', 'you', 'waterward', 'its', 'extreme', 'downtown', 'is', 'the', 'battery,', 'where', 'that', 'noble', 'mole', 'is', 'washed', 'by', 'waves,', 'and', 'cooled', 'by', 'breezes,', 'which', 'a', 'few', 'hours', 'previous', 'were', 'out', 'of', 'sight', 'of', 'land', 'look', 'at', 'the', 'crowds', 'of', 'water-gazers', 'there']

```
### 21.2.4 The csv module
```python

>>> results = []
>>> for line in open("temp_data_pipes_00a.txt"):
...     fields = line.strip().split("|")
...     results.append(fields)
... 
>>> results
[['State', 'Month Day, Year Code', 'Avg Daily Max Air Temperature (F)', 'Record Count for Daily Max Air Temp (F)'], ['Illinois', '1979/01/01', '17.48', '994'], ['Illinois', '1979/01/02', '4.64', '994'], ['Illinois', '1979/01/03', '11.05', '994'], ['Illinois', '1979/01/04', '9.51', '994'], ['Illinois', '1979/05/15', '68.42', '994'], ['Illinois', '1979/05/16', '70.29', '994'], ['Illinois', '1979/05/17', '75.34', '994'], ['Illinois', '1979/05/18', '79.13', '994'], ['Illinois', '1979/05/19', '74.94', '994']]


>>> import csv
>>> results = [fields for fields in csv.reader(open("temp_data_pipes_00a.txt"), delimiter="|")]
>>> results
[['State', 'Month Day, Year Code', 'Avg Daily Max Air Temperature (F)', 'Record Count for Daily Max Air Temp (F)'], ['Illinois', '1979/01/01', '17.48', '994'], ['Illinois', '1979/01/02', '4.64', '994'], ['Illinois', '1979/01/03', '11.05', '994'], ['Illinois', '1979/01/04', '9.51', '994'], ['Illinois', '1979/05/15', '68.42', '994'], ['Illinois', '1979/05/16', '70.29', '994'], ['Illinois', '1979/05/17', '75.34', '994'], ['Illinois', '1979/05/18', '79.13', '994'], ['Illinois', '1979/05/19', '74.94', '994']]


>>> results2 = [fields for fields in csv.reader(open("temp_data_01.csv", newline=''))]
>>> results2
[['Notes', 'State', 'State Code', 'Month Day, Year', 'Month Day, Year Code', 'Avg Daily Max Air Temperature (F)', 'Record Count for Daily Max Air Temp (F)', 'Min Temp for Daily Max Air Temp (F)', 'Max Temp for Daily Max Air Temp (F)', 'Avg Daily Min Air Temperature (F)', 'Record Count for Daily Min Air Temp (F)', 'Min Temp for Daily Min Air Temp (F)', 'Max Temp for Daily Min Air Temp (F)', 'Avg Daily Max Heat Index (F)', 'Record Count for Daily Max Heat Index (F)', 'Min for Daily Max Heat Index (F)', 'Max for Daily Max Heat Index (F)', 'Daily Max Heat Index (F) % Coverage'], ['', 'Illinois', '17', 'Jan 01, 1979', '1979/01/01', '17.48', '994', '6.00', '30.50', '2.89', '994', '-13.60', '15.80', 'Missing', '0', 'Missing', 'Missing', '0.00%'], ['', 'Illinois', '17', 'Jan 02, 1979', '1979/01/02', '4.64', '994', '-6.40', '15.80', '-9.03', '994', '-23.60', '6.60', 'Missing', '0', 'Missing', 'Missing', '0.00%'], ['', 'Illinois', '17', 'Jan 03, 1979', '1979/01/03', '11.05', '994', '-0.70', '24.70', '-2.17', '994', '-18.30', '12.90', 'Missing', '0', 'Missing', 'Missing', '0.00%'], ['', 'Illinois', '17', 'Jan 04, 1979', '1979/01/04', '9.51', '994', '0.20', '27.60', '-0.43', '994', '-16.30', '16.30', 'Missing', '0', 'Missing', 'Missing', '0.00%'], ['', 'Illinois', '17', 'May 15, 1979', '1979/05/15', '68.42', '994', '61.00', '75.10', '51.30', '994', '43.30', '57.00', 'Missing', '0', 'Missing', 'Missing', '0.00%'], ['', 'Illinois', '17', 'May 16, 1979', '1979/05/16', '70.29', '994', '63.40', '73.50', '48.09', '994', '41.10', '53.00', 'Missing', '0', 'Missing', 'Missing', '0.00%'], ['', 'Illinois', '17', 'May 17, 1979', '1979/05/17', '75.34', '994', '64.00', '80.50', '50.84', '994', '44.30', '55.70', '82.60', '2', '82.40', '82.80', '0.20%'], ['', 'Illinois', '17', 'May 18, 1979', '1979/05/18', '79.13', '994', '75.50', '82.10', '55.68', '994', '50.00', '61.10', '81.42', '349', '80.20', '83.40', '35.11%'], ['', 'Illinois', '17', 'May 19, 1979', '1979/05/19', '74.94', '994', '66.90', '83.10', '58.59', '994', '50.90', '63.20', '82.87', '78', '81.60', '85.20', '7.85%']]

```
### 21.2.5 Reading a csv file as a list of dictionaries
```python

import csv

>>> results = [fields for fields in csv.DictReader(open("temp_data_01.csv", newline=''))]
>>> results[0]
OrderedDict([('Notes', ''), ('State', 'Illinois'), ('State Code', '17'), ('Month Day, Year', 'Jan 01, 1979'), ('Month Day, Year Code', '1979/01/01'), ('Avg Daily Max Air Temperature (F)', '17.48'), ('Record Count for Daily Max Air Temp (F)', '994'), ('Min Temp for Daily Max Air Temp (F)', '6.00'), ('Max Temp for Daily Max Air Temp (F)', '30.50'), ('Avg Daily Max Heat Index (F)', 'Missing'), ('Record Count for Daily Max Heat Index (F)', '0'), ('Min for Daily Max Heat Index (F)', 'Missing'), ('Max for Daily Max Heat Index (F)', 'Missing'), ('Daily Max Heat Index (F) % Coverage', '0.00%')])


>>> results[0]['State']
'Illinois'

```
## 21.3 Excel files
```python

>>> from openpyxl import load_workbook
>>> wb = load_workbook('temp_data_01.xlsx')
>>> results = []
>>> ws = wb.worksheets[0]
>>> for row in ws.iter_rows():
...     results.append([cell.value for cell in row])
...  
>>> print(results)
[['Notes', 'State', 'State Code', 'Month Day, Year', 'Month Day, Year Code', 'Avg Daily Max Air Temperature (F)', 'Record Count for Daily Max Air Temp (F)', 'Min Temp for Daily Max Air Temp (F)', 'Max Temp for Daily Max Air Temp (F)', 'Avg Daily Max Heat Index (F)', 'Record Count for Daily Max Heat Index (F)', 'Min for Daily Max Heat Index (F)', 'Max for Daily Max Heat Index (F)', 'Daily Max Heat Index (F) % Coverage'], [None, 'Illinois', 17, 'Jan 01, 1979', '1979/01/01', 17.48, 994, 6, 30.5, 'Missing', 0, 'Missing', 'Missing', '0.00%'], [None, 'Illinois', 17, 'Jan 02, 1979', '1979/01/02', 4.64, 994, -6.4, 15.8, 'Missing', 0, 'Missing', 'Missing', '0.00%'], [None, 'Illinois', 17, 'Jan 03, 1979', '1979/01/03', 11.05, 994, -0.7, 24.7, 'Missing', 0, 'Missing', 'Missing', '0.00%'], [None, 'Illinois', 17, 'Jan 04, 1979', '1979/01/04', 9.51, 994, 0.2, 27.6, 'Missing', 0, 'Missing', 'Missing', '0.00%'], [None, 'Illinois', 17, 'May 15, 1979', '1979/05/15', 68.42, 994, 61, 75.1, 'Missing', 0, 'Missing', 'Missing', '0.00%'], [None, 'Illinois', 17, 'May 16, 1979', '1979/05/16', 70.29, 994, 63.4, 73.5, 'Missing', 0, 'Missing', 'Missing', '0.00%'], [None, 'Illinois', 17, 'May 17, 1979', '1979/05/17', 75.34, 994, 64, 80.5, 82.6, 2, 82.4, 82.8, '0.20%'], [None, 'Illinois', 17, 'May 18, 1979', '1979/05/18', 79.13, 994, 75.5, 82.1, 81.42, 349, 80.2, 83.4, '35.11%'], [None, 'Illinois', 17, 'May 19, 1979', '1979/05/19', 74.94, 994, 66.9, 83.1, 82.87, 78, 81.6, 85.2, '7.85%']]


```

## 21.5 Writing data files
### 21.5.1 CSV and other delimited files
```python

>>> temperature_data = [['State', 'Month Day, Year Code', 'Avg Daily Max Air Temperature (F)', 'Record Count for Daily Max Air Temp (F)'], ['Illinois', '1979/01/01', '17.48', '994'], ['Illinois', '1979/01/02', '4.64', '994'], ['Illinois', '1979/01/03', '11.05', '994'], ['Illinois', '1979/01/04', '9.51', '994'], ['Illinois', '1979/05/15', '68.42', '994'], ['Illinois', '1979/05/16', '70.29', '994'], ['Illinois', '1979/05/17', '75.34', '994'], ['Illinois', '1979/05/18', '79.13', '994'], ['Illinois', '1979/05/19', '74.94', '994']]
>>> csv.writer(open("temp_data_03.csv", "w", newline='')).writerows(temperature_data)


>>> fields = ['State', 'Month Day, Year Code', 'Avg Daily Max Air Temperature (F)', 'Record Count for Daily Max Air Temp (F)']
>>> dict_writer = csv.DictWriter(open("temp_data_04.csv", "w"), fieldnames=fields)
>>> dict_writer.writeheader()
>>> dict_writer.writerows(fie)
>>> del dict_writer

```
### 21.5.2 Writing Excel files
```python

>>> import csv
>>> from openpyxl import Workbook
>>> data_rows = [fields for fields in csv.reader(open("temp_data_01.csv"))]
>>> wb = Workbook()
>>> ws = wb.active
>>> ws.title = "temperature data"
>>> for row in data_rows:
...     ws.append(row)
... 
>>> wb.save("temp_data_02.xlsx")


```