ROLE: CACHE INFRASTRUCTURE ARCHITECT

OBJECTIVE:
Generate a reusable cache provider infrastructure under:
{basePackage}.cache

This module provides a standardized caching abstraction for the application.
Child modules MUST interact ONLY with the CacheProvider interface.

---

PACKAGE:
{basePackage}.cache

---

DESIGN PRINCIPLES:
- Cache abstraction first
- Implementation hidden from consumers
- Thread-safe
- Spring-managed
- No business logic

---

GENERATE THE FOLLOWING FILES (ALL REQUIRED):

---

1️⃣ CacheProvider.java

PURPOSE:
Defines a generic cache abstraction to be used across the application.

TYPE PARAMETERS:
- K → Cache key type
- V → Cache value type

METHODS:
- Optional<V> get(K key)
- void put(K key, V value)
- void evict(K key)
- void clear()

RULES:
- Interface only
- No default methods
- No Spring annotations
- JavaDocs required for interface and all methods

---

2️⃣ InMemoryCacheProvider.java

PURPOSE:
Default in-memory cache implementation using ConcurrentHashMap.

RESPONSIBILITIES:
- Store cached values in memory
- Ensure thread-safety
- Act as default cache provider

RULES:
- Implement CacheProvider<K, V>
- Use ConcurrentHashMap internally
- No expiration / TTL logic
- No logging
- Lombok NOT required
- JavaDocs required

---

3️⃣ CacheConfig.java

PURPOSE:
Spring configuration to expose CacheProvider bean.

RESPONSIBILITIES:
- Register InMemoryCacheProvider as the default CacheProvider
- Allow future replacement without breaking child code

RULES:
- @Configuration class
- @Bean method returning CacheProvider<?, ?>
- No conditional logic
- JavaDocs required

---

ARCHITECTURAL RULES (CRITICAL):

- Cache module MUST NOT depend on:
    - error
    - exception
    - response
    - security
    - client
    - swagger
    - logging

- Other modules MAY depend on cache.

- Cache implementation MUST NOT:
    - throw checked exceptions
    - include eviction policies
    - include persistence logic

---

QUALITY ENFORCEMENT:

- No TODOs
- No placeholders
- No unused imports
- No circular dependencies
- Spring Boot 3 compatible
- Java 17+ compatible

OUTPUT:
Java source files ONLY.
