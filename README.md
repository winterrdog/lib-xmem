# lib-xmem

a C library with functions to handle memory management with out-of-memory handling

## C API

The library only provides the following functions:

```c
void* xmalloc(size_t size);
void* xcalloc(size_t nmemb, size_t size);
void* xrealloc(void* ptr, size_t size);
void xfree(void* p);
const char* xstrdup(const char* s);
```

## Usage

### `xmalloc`

```c
#include <xmem.h>

int main() {
    char* p = xmalloc(10);
    xfree(p);
    return 0;
}
```

This code will allocate 10 bytes of memory and free it. If the allocation fails, the program will call `exit()` exit with an error message.

### `xcalloc`

```c
#include <xmem.h>

int main() {
    char* p = xcalloc(10, sizeof(char));
    xfree(p);
    return 0;
}
```

This code will allocate 10 bytes of memory and free it. If the allocation fails, the program will call `exit()` exit with an error message.

### `xrealloc`

```c
#include <xmem.h>

int main() {
    char* p = xmalloc(10);
    p = xrealloc(p, 20);
    xfree(p);
    return 0;
}
```

This code will allocate 10 bytes of memory, reallocate it to 20 bytes and free it. If the allocation fails, the program will call `exit()` exit with an error message.

### `xfree`

```c
#include <xmem.h>

int main() {
    char* p = xmalloc(10);
    xfree(p);
    return 0;
}
```

This code will allocate 10 bytes of memory and free it. If the allocation fails, the program will call `exit()` exit with an error message. The `xfree` function is safe to call with a `NULL` pointer in which case it will do nothing. After freeing the memory, the pointer is set to `NULL` in order to avoid double freeing and undefined behavior in case the pointer is used after being freed.

### `xstrdup`

```c
#include <xmem.h>

int main() {
    char* p = xstrdup("Hello, World!");
    xfree(p);
    return 0;
}
```

This code will allocate memory for the string "Hello, World!" and free it. If the allocation fails, the program will call `exit()` exit with an error message. It uses `xmalloc` internally to allocate memory for the string and `strlen` to get the length of the string. The caller is expected to free the memory allocated by `xstrdup` using `xfree`. The copying is done using `memcpy` and the string is null-terminated automatically. We used `memcpy` instead of `strcpy` to avoid buffer overflows and undefined behavior but you could use `strcpy` if you are sure that the string is null-terminated and know what you are doing. `memcpy` is handles unaligned memory very well.

## Usage in C projects

- Just include the `xmem.h` header file in your C project and compile since it's a single-header library.

## Contributing

If you want to contribute to this project and make it better, your help is very welcome. Contributing is also a great way to learn more and improve your skills. I'll be happy to help you with your contributions and any questions you may have.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details
