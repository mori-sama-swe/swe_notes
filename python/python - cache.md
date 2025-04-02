#  Python - Caching Implementation

## cachetools

**Cache**: A storage mechanism that holds key-value pairs (e.g., function inputs and their results).

**Decorators**: Functions that modify other functions. In this case, @cached is a decorator that adds caching behavior to a function.

**Cache Implementations**: cachetools provides several cache types, such as:

- cachetools.LRUCache: Evicts least recently used items when the cache is full.
- cachetools.TTLCache: Evicts items after a specified time-to-live.
- cachetools.FIFOCache: First-in, first-out eviction.

#### Cache Decorator

The `@cached` decorator is a simple way to add caching to a function. It’s a shorthand provided by cachetools that wraps a function with a cache. By default, it uses an unlimited dict-based cache unless you specify a custom cache object.

> [!note]
>
> **Here’s how it works:**
>
> - When you call a decorated function, it checks if the result for the given arguments is already in the cache.
> - If it is (a "cache hit"), it returns the cached result.
> - If it isn’t (a "cache miss"), it computes the result, stores it in the cache, and returns it.

## Implementing a Cache Key Generator

since @cache should hold a `key`. we should generate one

via a function within this function it can have proper cache checks.

````python
def generate_cache_key(<same params as func)
	..... #set a specific logic err,log,etc.
	return key

@cached(stored_cache, key=generate_cache_key)
def func_get_info_from_db
	return itemk
````

