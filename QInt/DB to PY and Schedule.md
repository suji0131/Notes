## Extract data from DB and convert it to pd dataframe
```
import pyodbc
import pandas
cnxn = pyodbc.connect(r'DRIVER={Microsoft Access Driver (*.mdb, *.accdb)};'
                      r'DBQ=C:\users\bartogre\desktop\data.mdb;')
sql = "Select sum(CYTM), sum(PYTM), BRAND From data Group By BRAND"
data = pandas.read_sql(sql,cnxn)
```

## Scheduling tasks using python
Advanced Python Scheduler (APScheduler) is a Python library that lets you schedule your Python code to be executed later, either just once or periodically. You can add new jobs or remove old ones on the fly as you please.
```
from apscheduler.schedulers.blocking import BlockingScheduler

def some_job():
    print "Decorated job"

scheduler = BlockingScheduler()
scheduler.add_job(some_job, 'interval', hours=1)
scheduler.start()
```
