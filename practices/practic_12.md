# PRACTIC 12

## thread
`std::thread`  
`std::join` ~ `.Wait`
`.sleep` - блокирует процесс, не один поток!  
`std::this_thread::sleep_for` - один поток  
`std::atomic<T> value`  
> битовые сдвиги можно сделать атомарными(возможно)  
`std::mutex`   
`std::lock_guard<std::mutex>(m)`  
`try_lock(time)` - пытаемся блокировать, если не получилось ,то игнорится 