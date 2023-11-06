# Years Old Problem - Days Between Dates

## To determine whether a year is a leap year, follow these steps:

1. If the year is evenly divisible by 4, go to step 2. Otherwise, go to step 5.
2. If the year is evenly divisible by 100, go to step 3. Otherwise, go to step 4.
3. If the year is evenly divisible by 400, go to step 4. Otherwise, go to step 5.
4. The year is a leap year (it has 366 days).
5. The year is not a leap year (it has 365 days).



```python
def is_leap_year(year):
    if year % 4 == 0:
        if year % 100 == 0:
            if year % 400 == 0:
                return 1
            return 0
        return 1
    return 0
```

## To determine how many days in a month


```python
def days_in_month(year, month):
    longer_months = [1, 3, 5, 7, 8, 10, 12]
    if month in longer_months:
        return 31
    if month == 2:
        return 28 + is_leap_year(year)
    return 30    
```

## To determine the next date


```python
def next_date(year, month, day):
    if day < days_in_month(year, month):
        return year, month, day + 1
    if month < 12:
        return year, month + 1, 1
    return (year + 1, 1, 1)
```

## To determine whether the birth date is before the current date


```python
def date_is_before(year1, month1, day1, year2, month2, day2):
    if year1 < year2:
        return True
    if year1 == year2:
        if month1 < month2:
            return True
        if month1 == month2:
            return day1 < day2
    return False
```

## To determine the number of days between dates


```python
def days_between_dates(year1, month1, day1, year2, month2, day2):
    assert not date_is_before(year2, month2, day2, year1, month1, day1)
    days = 0
    while date_is_before(year1, month1, day1, year2, month2, day2):
        year1, month1, day1 = next_date(year1, month1, day1)
        days += 1
    return days
```

# Test


```python
def test_is_leap_year():
    assert is_leap_year(2000) == True
    assert is_leap_year(2001) == False
    assert is_leap_year(2004) == True
    assert is_leap_year(2008) == True
    assert is_leap_year(2100) == False
    print('Tests passed.')
```


```python
def test_days_in_month():
    assert days_in_month(2001,1) == 31
    assert days_in_month(2001,2) == 28
    assert days_in_month(2008,2) == 29
    assert days_in_month(2001,3) == 31
    assert days_in_month(2001,4) == 30
    assert days_in_month(2001,5) == 31
    assert days_in_month(2001,6) == 30
    assert days_in_month(2001,7) == 31
    assert days_in_month(2001,8) == 31
    assert days_in_month(2001,9) == 30
    assert days_in_month(2001,10) == 31
    assert days_in_month(2001,11) == 30
    assert days_in_month(2001,12) == 31
    print('Tests passed.')
```


```python
def test_next_date():
    assert next_date(2023, 1, 1) == (2023, 1, 2)
    assert next_date(2023, 1, 2) == (2023, 1, 3)
    assert next_date(2023, 1, 30) == (2023, 1, 31)
    assert next_date(2023, 1, 31) == (2023, 2, 1)
    assert next_date(2023, 12, 31) == (2024, 1, 1)
    assert next_date(2013, 2, 28) == (2013, 3, 1)
    print('Tests passed.')
```


```python
def test_date_is_before():
    assert date_is_before(2002, 6, 26, 2023, 11, 6)
    assert not date_is_before(2023, 11, 6, 2002, 6, 26)
    assert not date_is_before(2013, 1, 1, 2013, 1, 1)
    print('Tests passed.')
```


```python
def test_days_between_dates():
    assert days_between_dates(2013, 1, 24, 2013, 6, 29) == 156
    assert days_between_dates(2013, 1, 1, 2013, 1, 1) == 0
    assert days_between_dates(2013, 1, 1, 2013, 1, 2) == 1
    assert days_between_dates(2012, 1, 1, 2013, 1, 1) == 366
    assert days_between_dates(2013, 1, 1, 2014, 1, 1) == 365
```


```python
def test():
    test_cases = [((2012,1,1,2012,2,28), 58), 
                  ((2012,1,1,2012,3,1), 60),
                  ((2011,6,30,2012,6,30), 366),
                  ((2011,1,1,2012,8,8), 585 ),
                  ((1900,1,1,1999,12,31), 36523)]
    
    for (args, answer) in test_cases:
        result = days_between_dates(*args)
        if result != answer:
            print("Test with data:", args, "failed")
        else:
            print("Test case passed!")
```


```python
def test1():
    test_date_is_before()
    test_days_between_dates()
    test_days_in_month()
    test_is_leap_year()
    test_next_date()
    test()
```

# Main


```python
if __name__ == "__main__":
    birth_date = [int(i) for i in tuple(input('Birth date: ').split('/'))]
    current_date = [int(i) for i in tuple(input('Current date: ').split('/'))]
    age = days_between_dates(*birth_date, *current_date)
    print(f"You're {age} days old!")
```

    Birth date:  2002/06/26
    Current date:  2023/11/06


    You're 7803 days old!

