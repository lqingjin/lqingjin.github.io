---
layout: post
title: '【selenium-python】源码解析--expected_conditions'
date: 2021-10-31
author: nangfeng-li
tags: selenium-python webdriver 
---

> expected_conditions模块包含了一系列预定义的条件来和WebDriverWait使用 <br>
> 
> code path: selenium.webdriver.support.expected_conditions <br>
> [Source code](https://www.selenium.dev/selenium/docs/api/py/_modules/selenium/webdriver/support/expected_conditions.html)


```python
from selenium.webdriver.support import expected_conditions as EC
```

- title_is(title)
  > 判断当前页面的title是否等于预期，必须完全匹配。<br>
  > 如果标题匹配，则返回True，否则返回false

- title_contains(title)
  > 判断当前页面的title是否包含预期字符串，区分大小写 <br>
  > 如果标题匹配，则返回True，否则返回false
  
- presence_of_element_located(locator)
  > 判断某个元素是否被加到了dom树里，并不代表该元素一定可见
  > 找到WebElement后返回该WebElement

- url_contains(url)
  > 检查当前url是否包含预期字符串，区分大小写 <br>
  > 当url匹配时返回True，否则返回False

- url_matches(pattern)
  > 检查当前url是否等于期望，必须完全匹配 <br>
  > 如果url匹配，则返回True，否则返回false

- url_to_be(url)
  > 同url_matches(pattern)
  
- url_changes(url)
  > 检查当前url是否不等于期望 <br>
  > 如果url不同，则返回True，否则返回false。

- visibility_of_element_located(locator)
  > 判断某个元素是否存在且可见. 可见代表元素非隐藏，并且元素的宽和高都不等于0 <br>
  > 找到并可见WebElement后返回该WebElement
  
- visibility_of(element)
  > 与visibility_of_element_located的区别是一个传locator，这个方法直接传定位到的element

- presence_of_all_elements_located(locator)
  > 判断是否至少有1个元素符合期望，存在于dom树中 <br>
  > 找到WebElement后返回WebElement的列表

- visibility_of_any_elements_located(locator)
  > 判断是否至少有1个元素符合期望，存在于dom树中 <br>
  > 找到WebElement后返回WebElement的列表

- visibility_of_all_elements_located(locator)
  > 检查所有元素是否都存在于页面显示且可见，可见代表元素非隐藏，并且元素的宽和高都不等于0 <br>
  > 找到WebElement后返回WebElement的列表
  
- text_to_be_present_in_element(locator, text_)
  > 检查给定文本是否存在于指定的元素。
  
- text_to_be_present_in_element_value(locator, text_)
  > 检查元素值中是否存在给定文本的期望。 <br>
  > get_attribute("value")  value属性值。

- text_to_be_present_in_element_attribute(locator, attribute_, text_)
  > 检查元素属性中是否存在给定文本的期望。 <br>
  > get_attribute(attribute_)  指定属性。
  
- frame_to_be_available_and_switch_to_it(locator)
  > 判断该frame是否可以切换，如果可以switch，返回True并且switch_to，否则返回False
  
- invisibility_of_element_located(locator)
  > 判断某个元素中是否不存在于dom树或不可见

- invisibility_of_element(element)
  > 同上，一个传locator，一个传element <br>
  > 元素是定位器（文本）或WebElement

- element_to_be_clickable(mark)
  >检查元素的期望是可见的并已启用(enable)，以便你可以点击它。 <br>
  > 元素是定位器（文本）或WebElement
  
- staleness_of(element)
  > 判断某个元素是否从dom树中移除 <br>
  > 如果元素仍然附加到DOM，则返回False，否则返回true
  
- element_to_be_selected(element)
  > 判断某个元素是否被选中,可用在下拉列表

- element_located_to_be_selected(locator)
  > 同上，一个传locator，一个传element

- element_selection_state_to_be(element, is_selected)
  > 检查给定元素是否被选中的期望值。 <br>
  > is_selected是布尔值
  
- element_located_selection_state_to_be(locator, is_selected)
  > 同上，一个传locator，一个传element

- number_of_windows_to_be(num_windows)
  > 期望窗口数是否符合预期

- new_window_is_opened(current_handles)
  > 期望打开一个新窗口，通过是否增加窗口句柄判断
  
- alert_is_present()
  > 判断页面上是否存在alert

- element_attribute_to_include(locator, attribute_)
  > 判断指定元素是否包含给定属性
  
- any_of(*expected_conditions)
  > 多个期望条件中的任何一个为真的期望。 <br>
  > 相当于逻辑“或”。 <br>
  > 返回第一个匹配条件的结果，如果没有，则返回False
  
- all_of(*expected_conditions)
  >所有多个预期条件均为真的预期。 <br>
  > 相当于逻辑“AND”。 <br>
  >当任何预期条件未满足时：返回False。 <br>
  >满足所有ExpectedConditions时：返回包含每个ExpectedCondition的返回值的列表
  
- none_of(*expected_conditions)
  > 一种期望，即一个或多个期望条件均不成立。 <br>
  > 相当于逻辑“非或”。 <br>
  > 返回一个布尔值，都不成立，返回True