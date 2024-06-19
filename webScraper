from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
from bs4 import BeautifulSoup
import time
import csv

def remove_duplicates(csv_file):
    with open(csv_file, 'r') as file:
        reader = csv.reader(file)
        data = list(reader)

    unique_ids = {}
    unique_data = []

    for entry in data:
        if entry[0] not in unique_ids:
            unique_ids[entry[0]] = True
            unique_data.append(entry)

    with open(csv_file, 'w', newline='') as file:
        writer = csv.writer(file)
        writer.writerows(unique_data)

chrome_options = webdriver.ChromeOptions()
# Path to Data directory (replace with own path to directory)
chrome_options.add_argument(r"--user-data-dir=/Users/#######################################")
#chrome_options.add_argument('--headless')



try:
    driver = webdriver.Chrome(options=chrome_options)
    driver.get('https://######################')
    time.sleep(3)
    body = driver.find_element(By.TAG_NAME, "body")
    body.click()
    driver.back()
    time.sleep(2)

    contact_list = []

    while True:
        with open('Scraper.csv', 'w', newline='') as csv_file:
            writer = csv.writer(csv_file)
            writer.writerow(['name', 'email']) 
            page_source = driver.page_source
            soup = BeautifulSoup(page_source, 'html.parser')

            divs = soup.find_all('div', {'role': 'presentation'})

            for div in divs:
                contact_data = ['nan', 'nan']
                try:
                    # Extract the name from the second div
                    span_text = div.find_all('div')[8].text
                    contact_data[0] = span_text
                except Exception as e:
                    print(f"Could not extract text from second div: {e}")

                try:
                    # Extract the email from the third div
                    if div.find_all('div')[14].text != "":
                        a_text = div.find_all('div')[32].text
                    else: 
                        a_text = div.find_all('div')[28].text
                    contact_data[1] = a_text
                except Exception as e:
                    print(f"Could not extract text from third div: {e}")

                contact_list.append(contact_data)

            writer.writerows(contact_list)

            body = driver.find_element(By.TAG_NAME, "body")
            for _ in range(1, 15):
                body.send_keys(Keys.ARROW_DOWN)

            time.sleep(2)

            new_page_source = driver.page_source
            if page_source == new_page_source:
                break  



    print('Operation successful.')
except Exception as e:
    print(f'Operation failed.')
finally:
    driver.quit()

remove_duplicates('Scraper.csv')
