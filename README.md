Very simple SQLite3 bindings (C++11)

The main reason for using these over the native C API is [RAII](http://en.wikipedia.org/wiki/Resource_Acquisition_Is_Initialization): We make sure that all resources are released once the handles are destructed. This saves a lot of boilerplate code.

### Usage

```c++
#include <sqlite.hpp>

using namespace mapbox::sqlite;

int main() {
    Database db(":memory:", OpenFlag::ReadWrite | OpenFlag::Create);

    db.exec("CREATE TABLE `words` (`word` TEXT PRIMARY KEY NOT NULL)");

    auto insert = db.prepare("insert into words VALUES(?)");
    insert.bind(1, "hello");
    insert.run();
    insert.reset();
    insert.bind(1, "world");
    insert.run();

    auto stmt = db.prepare("select word from words;");
    while (stmt.run()) {
        fprintf(stderr, "word: %s\n", stmt.get<std::string>(0).c_str());
    }
}
```

outputs

```
word: hello
word: world
```


### Notes

- Error reporting isn't thread safe
- No transaction object
- No advanced SQLite features
- No iterator interface
