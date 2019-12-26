# date\_range\_generator

## Generator Date Range

```python
def date_range_generator(StartDate: str, EndDate: str, Format: str = '%Y/%m/%d'):
    """
    Generate list of date between StartDate and EndDate.
    Ex:
        StartDate = '2018/11/28'
        EndDate = '2018/12/02'
    Result:
        ['2018/11/28', '2018/11/29', '2018/11/30', 
         '2018/12/01', '2018/12/02']
    """
    start = datetime.datetime.strptime(StartDate, '%Y/%m/%d')
    end = datetime.datetime.strptime(EndDate, '%Y/%m/%d')

    date_generated = [
        start + datetime.timedelta(days=x) for x in range(0, (end-start).days + 1)]
    return [d.strftime(Format) for d in date_generated]
```



