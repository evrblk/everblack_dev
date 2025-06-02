# Bison



# Bison

## Schema

```
├── bucket_1
│   ├── directory_a
│   |   └── item_1 (symlink)
│   └── directory_b
│       └── sub_directory_1
│           ├── item_1 (stored)
│           |   ├── raw_data
│           |   ├── ingestion_time
│           |   └── read_count (1m)
│           ├── item_2 (formula)
│           ├── item_3 (attribute) 
└── bucket_2
```

* attribute
    * no period, only data type and value
    * use value itself somewhere in formula
    * read value only via control plane API
* stored
    * period, data type and value
    * read value only via data plane API
        * RAW - value itself
        * INGESTION_TIME - when it was ingested or updated
        * READ - aggregated (~1m) how many times was read/accessed
        *
* formula
    *
* aggregate



ReadTimeSeries(TimeSeriesId) -> [t, v]
ReadAnnotation(AnnotationId) -> [t1, t2, v]
GetAlertState(AlertId)
SnoozeAlert(AlertId)


Script languages:
https://github.com/d5/tengo/blob/master/docs/tutorial.md
https://github.com/antonmedv/expr?utm_campaign=awesomego&utm_medium=referral&utm_source=awesomego

