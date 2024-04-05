Copy code
from selenium import webdriver
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.common.by import By
import calendar

# Ask user for target month
target_month = input("Enter target month (format: MM/YYYY): ")

# Splitting the target month into month and year
month, year = target_month.split('/')

# Dictionary to map month number to month name
month_names = {1: 'January', 2: 'February', 3: 'March', 4: 'April', 5: 'May', 6: 'June', 7: 'July', 8: 'August',
               9: 'September', 10: 'October', 11: 'November', 12: 'December'}

# Setting up Selenium
driver = webdriver.Chrome()
driver.get("https://www.redbus.in/")

# Clicking on the calendar option
driver.find_element(By.ID, 'onward_cal').click()

# Getting the current month and year from the calendar
current_month_year = driver.find_element(By.CLASS_NAME, 'monthTitle').text

while current_month_year != f"{month_names[int(month)]} {year}":
    # Extracting month and year from current_month_year
    current_month, current_year = current_month_year.split(' ')

    # Getting holidays for the current month
    holidays = driver.find_elements(By.XPATH, "//td[@class='wd day']")
    for holiday in holidays:
        print(f"Holiday: {holiday.get_attribute('title')}")

    # Going to the next month
    driver.find_element(By.CLASS_NAME, 'next').click()

    # Updating current month and year
    current_month_year = driver.find_element(By.CLASS_NAME, 'monthTitle').text

# Printing weekends dates
weekends = driver.find_elements(By.XPATH, "//td[@class='we day']")
for weekend in weekends:
    print(f"Weekend: {weekend.get_attribute('title')}")

# Close the browser
driver.quit()
