import argparse
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
import time

parser = argparse.ArgumentParser(description="Automate Instagram account creation.")
parser.add_argument("-u", "--url", type=str, default="https://www.instagram.com", help="Website URL where accounts will be created")
parser.add_argument("-n", "--num-accounts", type=int, default=5, help="Number of accounts to create (default: 5)")
args = parser.parse_args()

website_url = args.url

num_accounts = args.num_accounts
driver = webdriver.Chrome()
driver.get(website_url)

for i in range(num_accounts):
    time.sleep(2)  # Adjust the wait time as needed
    
    username_field = driver.find_element(By.NAME, "username")
    password_field = driver.find_element(By.NAME, "password")
    
    username_field.send_keys(Keys.CONTROL + "a")
    username_field.send_keys(Keys.DELETE)
    
    password_field.send_keys(Keys.CONTROL + "a")
    password_field.send_keys(Keys.DELETE)

    username_field.send_keys("username_" + str(i))
    password_field.send_keys("password_" + str(i))
    
    submit_button = driver.find_element(By.XPATH, "//button[@type='submit']")
    submit_button.click()
    
    time.sleep(3)

driver.quit()
