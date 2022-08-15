+++
date = "2022-03-27T00:00:00+00:00"
draft = false
title = "Headless Selenium with Firefox and GeckoDriver"
slug = "headless-selenium-with-firefox-and-geckodriver"
+++


I'm using pipenv with a headless selenium configuration but was getting PATH errors. 

Using [webdriver_manager](https://github.com/SergeyPirogov/webdriver_manager) solved that problem. 


```python
import logging
from selenium import webdriver
from selenium.webdriver.firefox.service import Service
from selenium.webdriver.firefox.options import Options
from webdriver_manager.firefox import GeckoDriverManager

logging.basicConfig(level=logging.DEBUG)

options = Options()
options.add_argument("--headless")
options.add_argument("--disable-extensions")
driver = webdriver.Firefox(service=Service(GeckoDriverManager().install()), options=options)

driver.get("https://some.url.com")
# Basic test of functionality, get the browser title and print it to the CLI.
get_title = driver.title
print(get_title)

driver.quit()
```

Example

```shell
~/src/py-wordle via 🐍 v3.10.0 (py-wordle) took 8s 
❯ /home/pete/.local/share/virtualenvs/py-wordle-LQNTphUp/bin/python /home/pete/src/py-wordle/webscrape.py


====== WebDriver manager ======
Current firefox version is 98.0
Get LATEST geckodriver version for 98.0 firefox
Driver [/home/pete/.wdm/drivers/geckodriver/linux64/v0.30.0/geckodriver] found in cache
Website Title
```
