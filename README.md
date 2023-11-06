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

