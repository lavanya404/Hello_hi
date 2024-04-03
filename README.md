from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

# Set the path to the webdriver executable
driver_path = "path/to/your/webdriver"

# Initialize a webdriver instance (in this case, using Chrome)
driver = webdriver.Chrome(executable_path=driver_path)

# URL of the website to navigate to
url = "https://www.flipkart.com/"

# Open the URL in the browser
driver.get(url)

# Find the search field and click on it
search_field = WebDriverWait(driver, 10).until(EC.element_to_be_clickable((By.NAME, "q")))
search_field.click()

# Enter "iphone" in the search field
search_field.send_keys("iphone")

# Press Enter to perform the search
search_field.send_keys(Keys.RETURN)

# Wait for the search results dropdown to appear
search_results_dropdown = WebDriverWait(driver, 10).until(EC.visibility_of_element_located((By.CLASS_NAME, "vh79eN")))

# Click on the iPhone 12 or iPhone 13 from the dropdown
iphone_12_or_13 = WebDriverWait(driver, 10).until(EC.element_to_be_clickable((By.XPATH, "//div[@class='v1tKd-']//a[contains(text(), 'iPhone 12') or contains(text(), 'iPhone 13')]")))
iphone_12_or_13.click()

-------------------------------------------
# Enter "iphone" in the search field
search_field.send_keys("iphone")

# Press Enter to perform the search
search_field.send_keys(Keys.RETURN)

# Wait for the search results dropdown to appear
search_results_dropdown = WebDriverWait(driver, 10).until(EC.visibility_of_element_located((By.CLASS_NAME, "vh79eN")))

# Find all the links in the dropdown
links = search_results_dropdown.find_elements(By.XPATH, "//a[@class='VZ-Dzg']")

# Loop through the links and click on the one containing 'iPhone 12' or 'iPhone 13'
for link in links:
    if 'iPhone 12' in link.text or 'iPhone 13' in link.text:
        link.click()
        break  # Once clicked, exit the loop
--------------------------------------------------------------------------------------
#  Assessment 5: Handling dynamic drop down:

# 1.Navigate to URL https://www.flipkart.com/ (Ignore the login pops up)
# 2.Click on the search field and enter iPhone
# 3.Click on the iPhone 12 or iPhone 13 from the dropdown
--------------------------------------------------------------------------------------------
# Close the login pop-up if it appears (if you don't need to interact with it)
try:
    close_button = WebDriverWait(driver, 10).until(EC.element_to_be_clickable((By.XPATH, "//button[@class='_2KpZ6l _2doB4z']")))
    close_button.click()
except:
    pass

# Find the search field and enter "iPhone"
search_field = WebDriverWait(driver, 10).until(EC.element_to_be_clickable((By.NAME, "q")))
search_field.click()
search_field.send_keys("iPhone")

# Wait for the search results dropdown to appear
search_results_dropdown = WebDriverWait(driver, 10).until(EC.visibility_of_element_located((By.CLASS_NAME, "vh79eN")))

# Find all the links in the dropdown
links = search_results_dropdown.find_elements(By.XPATH, "//a[@class='VZ-Dzg']")

# Loop through the links and click on the one containing 'iPhone 12' or 'iPhone 13'
for link in links:
    if 'iPhone 12' in link.text or 'iPhone 13' in link.text:
        link.click()
        break  

--------------------------------------------------------------------------
# Find the search field and enter "iPhone"
search_field = WebDriverWait(driver, 10).until(EC.element_to_be_clickable((By.NAME, "q")))
search_field.click()
search_field.send_keys("iPhone")
time.sleep(2)  # Adding a short delay to let the dropdown load

# Send arrow keys to navigate the dropdown
search_field.send_keys(Keys.ARROW_DOWN)
search_field.send_keys(Keys.ENTER)
------------------------------------------------------------------
# Find iPhone 12 or iPhone 13 from the dropdown
iphone_options = WebDriverWait(search_results_dropdown, 10).until(EC.presence_of_all_elements_located((By.XPATH, "//div[contains(@class,'vh79eN')]//a[contains(@class,'_1fQZEK')]")))

# Loop through each option and click on iPhone 12 or iPhone 13
for option in iphone_options:
    if "iPhone 12" in option.text or "iPhone 13" in option.text:
        option.click()
        break
