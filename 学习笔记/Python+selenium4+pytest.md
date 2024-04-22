# Python+selenium4+pytest

# 自动化测试框架

### 框架其他

- yaml数据驱动
- allure报告
- 日志
- 数据库（MySQL）
- 通过Jenkins发送消息（企业微信、钉钉、飞书）

### 学习步骤

1. 环境准备
2. HTML基础知识
3. 元素定位实战
4. pytest知识详解
5. PO模式知识点详解
6. selenium 二次封装
7. web项目实战
8. Jenkins实战和消息发送

### 元素定位

元素定位常用方式

- By.ID

  - ```python
    from time import sleep
    
    from selenium import webdriver
    from selenium.webdriver.common.by import By
    
    driver = webdriver.Chrome()
    driver.maximize_window() #窗口最大化
    driver.get("https://www.baidu.com/")
    driver.find_element(By.ID, "kw").send_keys("selenium")  # 通过ID定位
    
    driver.find_element(By.ID, "su").click()
    sleep(3)
    driver.quit()  #selenium4执行完毕都会关闭浏览器，selenium3不会
    
    ```

- By.LINK_TEXT

  - ```python
    from selenium import webdriver
    from time import sleep
    
    from selenium.webdriver.common.by import By
    
    driver = webdriver.Chrome()
    driver.maximize_window() #窗口最大化
    driver.get("https://www.baidu.com/")
    # driver.find_element(By.LINK_TEXT,"网盘").click()
    driver.find_elements(By.LINK_TEXT,"新闻")[0].click()
    sleep(3)
    ```

- By.CLASS_NAME

  - ```python
    import time
    
    from selenium import webdriver
    from selenium.webdriver.common.by import By
    
    driver = webdriver.Chrome()
    driver.maximize_window()
    driver.get("https://www.bilibili.com")
    driver.find_element(By.CLASS_NAME,"nav-search-input").send_keys("荷塘星星")
    driver.find_element(By.CLASS_NAME,"nav-search-btn").click()
    time.sleep(3)
    ```

- By.PARTIAL_LINK_TEXT

  - ```python
    from selenium import webdriver
    from time import sleep
    
    from selenium.webdriver.common.by import By
    
    driver = webdriver.Chrome()
    driver.maximize_window()  # 窗口最大化
    driver.get("https://www.baidu.com/")
    driver.find_element(By.PARTIAL_LINK_TEXT, "网盘").click()
    
    sleep(3)
    
    ```

- By.TAG_NAME

  - ```python
    from selenium import webdriver
    from time import sleep
    
    from selenium.webdriver.common.by import By
    
    driver = webdriver.Chrome()
    driver.maximize_window()
    driver.get("https://www.bilibili.com")
    
    # driver.find_element(By.TAG_NAME,"input").send_keys("自动化")
    # 不推荐用下面这个方式
    # driver.find_elements(By.TAG_NAME,"a")[50].click()
    
    sleep(3)
    ```

- <strong style="color:red;">By.CSS_SELECTOR</strong>

  - ```python
    from selenium import webdriver
    from time import sleep
    from selenium.webdriver.common.by import By
    
    driver = webdriver.Chrome()
    driver.get("https://www.baidu.com/")
    driver.maximize_window()
    # 根据ID定位需要加#号
    # driver.find_element(By.CSS_SELECTOR,"#kw").send_keys("selenium")
    # driver.find_element(By.CSS_SELECTOR,"#su").click()
    
    
    # 根据.class属性值定位
    # driver.find_element(By.CSS_SELECTOR,".nav-search-input").send_keys("selenium")
    # driver.find_element(By.CSS_SELECTOR,".nav-search-btn").click()
    
    # 根据name属性值定位:'[name="值"]'
    # driver.find_element(By.CSS_SELECTOR,'[name="wd"]').send_keys("selenium")
    
    # 根据标签属性定位(href)
    # driver.find_element(By.CSS_SELECTOR,"a[href='http://news.baidu.com']").click()
    # 模糊匹配-包含(href*)模糊匹配-匹配开头(href^)
    # driver.find_element(By.CSS_SELECTOR,"a[href*='image.baidu.com']").click()
    # 模糊匹配-匹配开头(href^)
    # driver.find_element(By.CSS_SELECTOR,"a[href^='http://image.b# 模糊匹配-匹配开头(href^)
    # 模糊匹配-匹配结尾(href$)
    # driver.find_element(By.CSS_SELECTOR,"a[href$='image.baidu.com/']").click()
    # 组合定位(标签+class值：input.s_ipt)
    # driver.find_element(By.CSS_SELECTOR,"input.s_ipt").send_keys("selenium")
    
    # 定位子元素
    # driver.find_element(By.CSS_SELECTOR,"div#s-top-left>a").click()
    # driver.find_elements(By.CSS_SELECTOR,"div#s-top-left>a")[2].click()
    # driver.find_element(By.CSS_SELECTOR,"div#s-top-left>a:nth-child(3)").click()
    # driver.find_element(By.CSS_SELECTOR,"div.s-top-left-new.s-isindex-wrap>a").click()
    # driver.find_element(By.CSS_SELECTOR,"div#s-top-left>a:first-child").click()
    # driver.find_element(By.CSS_SELECTOR,"#s-top-left > a:nth-child(8)").click() #F12上焦元素，copy-> copy celector
    
    
    sleep(3)
    driver.quit()
    
    ```

    | 选择器       | 格式           | 示例              | 示例说明                                      |
    | ------------ | -------------- | ----------------- | --------------------------------------------- |
    | 标签选择器   | HTML标签       | input             | 选择所有<input>元素                           |
    | ID选择器     | #id属性值      | #kw               | 选择所有id='kw'的元素                         |
    | 类选择器     | .class属性值   | .nav-search-input | 选择所有class='nav-search-input'的元素        |
    | 属性选择器1  | [属性名]       | [name="wd"]       | 选择所有name等于"wd"的元素                    |
    | 组合选择器   | 标签加属性描述 | input.s_ipt       | 选择所有class=‘_ipt的<input>元素              |
    | 父子关系     | 元素1>元素2    | div>a             | 选择所有父级是<div>的<a>元素                  |
    | 后代关系     | 元素1 元素2    | div a             | 选择<div>中的所有<a>元素                      |
    | 第一子元素   | :first-child   | a:first-child     | 选择所有<a>元素且该元素是其父级的第一个元素   |
    | 最后一个元素 | :last-child    | a:last-child      | 选择所有<a>元素且该元素是其父级的最后一个元素 |
    | 顺序选择器   | :nth-child(n)  | a:nth-child(2)    | 选择所有<a>元素且该元素是其父级的第二个子元素 |

- By.NAME

  - ```python
    from selenium import webdriver
    from time import sleep
    
    from selenium.webdriver.common.by import By
    
    driver = webdriver.Chrome()
    driver.maximize_window() #窗口最大化
    driver.get("https://www.baidu.com/")
    driver.find_element(By.NAME,"wd").send_keys("软件测试")
    sleep(3)
    ```

- <strong style="color:red;">By.XPATH</strong>

  - ```python
    from selenium import webdriver
    from time import sleep
    from selenium.webdriver.common.by import By
    
    driver = webdriver.Chrome()
    driver.get("https://www.baidu.com/")
    driver.maximize_window()
    
    # 绝对路径
    # driver.find_element(By.XPATH,"/html/body/div/div/div[3]/a").click()
    
    # 相对路径
    # driver.find_element(By.XPATH,"//div/div/div[3]/a").click()
    
    # 根据ID定位
    # driver.find_element(By.XPATH,"//input[@id='kw']").send_keys("selenium")
    
    # 根据class属性定位
    # driver.find_element(By.XPATH,"//a[@class='mnav c-font-normal c-color-t']").click()
    
    # 根据name属性定位
    # driver.find_element(By.XPATH,"//input[@name='wd']").send_keys("selenium")
    
    # 多个元素定位使用and连接
    # driver.find_element(By.XPATH,"//input[@name='wd' and @id='kw']").send_keys("selenium")
    
    sleep(3)
    driver.close()
    ```

    | 说明                           | 举例                                    |
    | ------------------------------ | --------------------------------------- |
    | 从根节点开始选取（绝对路径）   | /html/div/                              |
    | 从任意节点开始选取（相对路径） | //div,例举出所有div标签                 |
    | 选取当前节点的父节点           | //input/..会选取input的父节点           |
    | 选取属性，或根据属性选取       |                                         |
    | 使用ID属性定位                 | //div[@id='id_value']                   |
    | 使用class属性定位              | //a[@class="mnav"]                      |
    | 使用name属性定位               | //div[@name="wd"]                       |
    | 多个属性定位                   | //input[@name="wd"and @class="s_ipt"]   |
    | 第N个元素，使用index定位       | //div[@id="s-top-left"]/a[3]            |
    | 最后一个元素                   | //a[@class="mnav"][last()]              |
    | 属性包含某字段                 | //div[cobtains(@title,'text')]          |
    | 属性以某字段开头               | //div[starts-with(@title,'text')]       |
    | 属性以某字段结尾               | //div[ends-with(@title,'text')]         |
    | 文本包含                       | //a[contains(text(),"网盘")]            |
    | 文本等于                       | //span[text()="菜单"]                   |
    | 同级弟弟元素                   | //div[@id=='id']/following-sibling::div |
    | 同级哥哥元素                   | //div[@id=='id']/preceding-sibling::div |


### 第一个练习打开b站并搜索

```python
import time
from selenium import webdriver
from selenium.webdriver.common.by import By

driver = webdriver.Chrome()     #打开浏览器

driver.get("http://www.bilibili.com")   #打开bilibili,get方式，访问网址
# 1.找到输入框位置，输入“软件测试”
driver.find_element(By.CLASS_NAME,'nav-search-input').send_keys("软件测试") #By此处alt+enter，引入selenium
time.sleep(5)
# 2.找到搜索button的位置
driver.find_element(By.CLASS_NAME,'nav-search-btn').click()
time.sleep(3)
driver.close()          #关闭浏览器

```

### 不同元素定位实战

- radio单选框
- checkbox多选框
- select选择器
- 级联选择
- 时间选择器
- 弹框
- 文件上传upload
- 文件下载
