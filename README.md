```python
days_of_months = [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31]
```


```python
def is_leap_year(year):
    if year % 4 == 0:
        if year % 100 == 0:
            if year % 400 == 0:
                return True
            return False
        return True
    return False
```


```python
def leap_days_change(year):
    if is_leap_year(year):
        days_of_months[1] = 29
    else:
        days_of_months[1] = 28
```


```python
def days_between_dates(y1, m1, d1, y2, m2, d2):
    days = 0
    leap_days_change(y1)
    days += days_of_months[m1 - 1] - d1
    days += sum(days_of_months[m1:])
    for year in range(y1 + 1, y2):
        leap_days_change(year)
        days += sum(days_of_months)
    leap_days_change(y2)
    days += sum(days_of_months[0:m2 - 1])
    days += d2    
    return days
```


```python
birth_date = [int(i) for i in tuple(input('Birth date: ').split('/'))]
current_date = [int(i) for i in tuple(input('Current date: ').split('/'))]
age = days_between_dates(*birth_date, *current_date)
print(f"You're {age} days old!")
```

    Birth date:  2002/06/26
    Current date:  2023/10/30


    You're 7796 days old!

