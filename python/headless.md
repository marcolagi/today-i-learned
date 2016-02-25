# Headless scraping

A **headless browser** is simply a web browser without a
[GUI interface](https://www.youtube.com/watch?v=hkDD03yeLnU). This is useful
in cases where a machine doesn’t have a screen to run the browser on. Here is
the complete script to install **Selenium**, a suite of tools to automate
web browser activity across many platforms, often used for
testing web applications.

    apt-get install xvfb
    apt-get remove iceweasel
    echo -e "\ndeb http://downloads.sourceforge.net/project/ubuntuzilla/mozilla/apt all main" | tee -a /etc/apt/sources.list > /dev/null
    apt-key adv --recv-keys --keyserver keyserver.ubuntu.com C1289A29
    apt-get update
    apt-get install firefox-mozilla-build libdbus-glib-1-2 libgtk2.0-0 libasound2
    pip install pyvirtualdisplay selenium

A short explanation of the packages installed:

+ **Xvfb** simulates a display by doing everything in memory and
not showing any screen output.
+ in case the native **Iceweasel** is installed, better to remove it.
+ **Firefox** is a good choice, but not the only one. Selenium also interfaces
  with Chrome, IE, Opera.
+ **PyVirtualDisplay** is a python wrapper for Xvfb.

Selenium is now ready to search for itself on Google:

    from selenium import webdriver
    from pyvirtualdisplay import Display
    from selenium.webdriver.common.keys import Keys

    display = Display(visible=0, size=(800, 600))
    display.start()

    browser = webdriver.Firefox()
    browser.get('http://www.google.com')
    assert 'Google' in browser.title
    elem = browser.find_element_by_class_name('gsfi')
    elem.send_keys('selenium' + Keys.RETURN)
    browser.quit()

    display.stop()

