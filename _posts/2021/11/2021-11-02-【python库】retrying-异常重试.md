---
layout: post
title: 'python库--retrying-异常重试'
date: 2021-11-02
author: nangfeng-li
tags: python库
---

> 可用于失败重试，也可以手动触发异常重试。
> 参考：[github_retrying](https://github.com/rholder/retrying)

```
pip install retrying
```

```python
import random
from retrying import retry

@retry
def do_something_unreliable():
    if random.randint(0, 10) > 1:
        print('failure')
        raise NameError("failure")
    else:
        return "success"

print(do_something_unreliable())
```
### Examples

> 永远重试忽略异常，不在重试之间等待直到成功

```python
from retrying import retry

@retry
def never_give_up_never_surrender():
    raise print("永远重试忽略异常，不在重试之间等待")

never_give_up_never_surrender()
```

-  stop_max_attempt_number

> 设置重试次数，超过重试次数仍失败则抛出异常

```python
from retrying import retry

@retry(stop_max_attempt_number=3)
def stop_after_3_attempts():
    raise print("3次尝试后停止")

stop_after_3_attempts()
```

- stop_max_delay
  
> 最大等待时间，超过时间仍失败则抛出异常

```python
from retrying import retry

@retry(stop_max_delay=10000)
def stop_after_10_s():
    raise print("10秒后停止")

stop_after_10_s()
```

- wait_fixed

> 重试之间等待2s

```python
from retrying import retry

@retry(wait_fixed=2000)
def wait_2_s():
    raise print("重试之间等待2s")

wait_2_s()
```

- wait_random_min, wait_random_max
> 重试之间随机等待1-2s

```python
from retrying import retry

@retry(wait_random_min=1000, wait_random_max=2000)
def wait_random_1_to_2_s():
    raise print("重试之间随机等待1-2秒")
```
- wait_exponential_multiplier,wait_exponential_max
> 每次重试之间等待2^x*1000毫秒，最长10秒，然后固定10秒

```python
from retrying import retry
import time

@retry(wait_exponential_multiplier=1000, wait_exponential_max=10000)
def wait_exponential_1000():
    raise print(time.strftime("%H:%M:%S"))

wait_exponential_1000()
```
- retry_on_exception
> 引发特定或一般的异常重试
>
> 示例：如果发生IOError,永远重试无需等待。引发任何其他错误则跳出重试。

```python
from retrying import retry

def retry_if_io_error(exception):
    """如果我们应该重试，则返回True（在本例中是IOError），否则返回False"""
    return isinstance(exception, IOError)

@retry(retry_on_exception=retry_if_io_error)
def might_io_error():
    raise IOError(print("永远重试，无需等待。"))

might_io_error()

# 任何非IOError,不重试，抛出异常
@retry(retry_on_exception=retry_if_io_error)
def break_name_error():
    raise NameError(print("NameError不重试，抛出异常"))

break_name_error()

@retry(retry_on_exception=retry_if_io_error, wrap_exception=True)
def only_raise_retry_error_when_not_io_error():
    raise IOError(print("IOError重试,其他错误抛出异常"))

only_raise_retry_error_when_not_io_error()

@retry(retry_on_exception=retry_if_io_error, wrap_exception=True)
def _only_raise_retry_error_when_not_io_error():
    raise NameError(print("IOError重试,其他错误抛出异常"))

_only_raise_retry_error_when_not_io_error()
```

- retry_on_result
> 使用函数的结果来改变重试行为

```python
from retrying import retry

def retry_if_result_none(result):
    """如果我们应该重试，则返回True（在本例中，结果为None），否则返回False"""
    return result is None

@retry(retry_on_result=retry_if_result_none)
def might_return_none():
    print("如果返回值为None，则永远重试忽略异常而不等待")

might_return_none()
```

