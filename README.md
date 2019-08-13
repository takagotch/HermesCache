### hermescache
---
https://pypi.org/project/HermesCache/

```py
import hermes.backend.redis

cache = hermes.Hermes(hermes.backend.redis.Backend, ttl = 600, host = 'localhost', db = 1)

@cache
def foo(a, b):
  return a * b

class Example:
  @cache(tags = ('math', 'power'), ttl = 1200)
  def bar(self, a, b):
    return a ** b
    
  @cache(tags = ('math', 'avg'), key = lambda fn, *args, **kwargs: 'avg:[0]:{1}'.format(*args))
  def baz(self, a, b):
    return (a + b) / 2.0
    
print(foo(2, 333))

example = Example()
print(example.bar(2, 10))
print(example.baz(2, 10))

foo.invalidate(2, 333)
example.bar.invalidate(2, 10)
example.baz.invalidate(2, 10)

cache.clean(['math'])
cache.clean()
```

```sh
pip install HermesCache
```

```
```


