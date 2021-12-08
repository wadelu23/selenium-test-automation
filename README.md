# Selenium Test Automation Script With Python & pytest

* 此處筆記範例取自 [Selenium Python Tutorial: Getting Started With Pytest](https://www.lambdatest.com/blog/selenium-python-pytest-testing-tutorial/)
* 該文內有完整說明 Selenium, pytest 相關概念與前置作業

---

## 測試流程

1. 首先依據 pytest 規則定義檔名及method，即可搭配VSCode套件，有更清楚的樹狀圖查看目前狀態
   * [VSCode套件說明請點此](https://github.com/wadelu23/pytest-note#%E6%B8%AC%E8%A9%A6%E6%8C%87%E4%BB%A4-%E5%8F%AF%E6%90%AD%E9%85%8Dvscode%E5%A5%97%E4%BB%B6)

如圖

![img](https://raw.githubusercontent.com/wadelu23/MarkdownPicture/main/vscode/vscode-pytest.png)


2. 編寫操作流程與檢查點

附上 [Selenium with Python中文翻譯文件](https://selenium-python-zh.readthedocs.io/en/latest/index.html)

```python
# 如點擊某元素
chrome_driver.find_element_by_name("li1").click()

# 檢查特定資料是否一致
title = "Sample page - lambdatest.com"
assert title == chrome_driver.title

# 特殊輸入，如 ctrl + v
element.send_keys(Keys.CONTROL, "v")

# 取得指定元素文字
output_str = chrome_driver.find_element_by_xpath(
        "//ul[@class='list-unstyled']/li[6]").text

# 檢查文字是否一致
assert sample_text == output_str
```

---

## 補充事項

* **殭屍線程**，跑多次webdriver測試後多少會占用記憶體，因此可依照情形設定條件來定時清除
```python
# 在python中
import os

os.system("kill $(ps aux | grep webdriver| awk '{print $2}')")

# 如果是在win10中
os.system("taskkill /im chromedriver.exe /f")

```
如有其他問題，可額外參考[【爬蟲筆記】Python Selenium Webdriver異常問題集](https://www.maxlist.xyz/2019/04/27/python-selenium-error/)

* **sleep、等待頁面加載**

文中使用sleep的方式停頓，可供檢查每個步驟是否照預期執行

後續可改成[顯式等待](https://selenium-python-zh.readthedocs.io/en/latest/waits.html#waits)方式加快執行速度


---

## 引用文章
* [Selenium Python Tutorial: Getting Started With Pytest](https://www.lambdatest.com/blog/selenium-python-pytest-testing-tutorial/)
* [【爬蟲筆記】Python Selenium Webdriver異常問題集](https://www.maxlist.xyz/2019/04/27/python-selenium-error/)
* [動態網頁爬蟲第一道鎖 — Selenium教學：如何使用Webdriver、send_keys(附Python 程式碼)](https://aitmr1234567890.medium.com/%E5%8B%95%E6%85%8B%E7%B6%B2%E9%A0%81%E7%88%AC%E8%9F%B2%E7%AC%AC%E4%B8%80%E9%81%93%E9%8E%96-selenium%E6%95%99%E5%AD%B8-%E5%A6%82%E4%BD%95%E4%BD%BF%E7%94%A8webdriver-send-keys-%E9%99%84python-%E7%A8%8B%E5%BC%8F%E7%A2%BC-331aab27a3b7)