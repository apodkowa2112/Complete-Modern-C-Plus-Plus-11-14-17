# Raw String Literals

* `R"(C:\temp\newfile.txt)"`
* If you need `)"` in the string you can create your own literal:
```cpp
#include <iostream>
int main () {
    using namespace std;
    cout << R"(Tab: `\t`)" << endl;
    cout << R"(Newline: `\n`)" << endl;
    cout << R"DL(Raw string: `R"()"`)DL" << endl;
}
```
# filesystem library (C++17)
* Note: this is gcc only
```cpp
#include <iostream>
#include <filesystem>

int main () {
    using namespace std;
    using namespace filesystem;
    path p {R"(/proc/cpuinfo)"};
    cout << p.filename() << endl;
    cout << p.has_filename() << endl;
    for ( const auto &x : p) {
        cout << x << endl;
    }
    path dir{"/boot/"};
    cout << dir.has_filename() << endl;
    directory_iterator beg{dir}, end{};
    for (; beg != end; ++beg) {
        cout << *beg << endl;
    }
```
## File open modes:

* `app`: Append to file for each write
* `binary`: Binary mode
* `in`: Reading (ifstream default)
* `out`: Writing (ofstream default)
* `trunc`: discard file contents before opening (Overwrite?)
* `ate`: Seek to end after open

## stream methods:
* getline(): Reads to next endline
* close():   Manually releases the file handle
* open():    Reopens the file.
* is_open(): Checks if file opening succeeded.
* clear():   Reset error bits to clean state.
* put():     Write one character
* get():     Get one character
* ifstream::tellg(): Get current position of file 
* ifstream::seekg(): Go to position in file (offset, basePosition)
* ofstream::seekp(): Go to position in file

## Error handling
Stream state flags:
* goodbit: good(), No error
* badbit:  bad(),  irrecoverable stream error
* failbit: fail(), operator!(), I/O operation failed
* eofbit:  eof(),  end of file reached

```cpp
#include<iostream>
#include<fstream>
#include<string>
#include<filestream>

int main() {
    using namespace std;
    using namespace filesystem;

    path src(current_path());
    src /= "main.cpp";

    path dst(current_path());
    dst /= "copy.cpp";

    ifstream input{ src };
    if (!input) {
        cerr << "Failed to open:\n\t" << src << endl;
        return -1;
    }

    ofstream output{ dst };
    string line;
    while (!std::getline(input, line).eof()) {
        output << line << endl; 
    }
    input.close();
    output.close();
    return 0;
}
```

```cpp
fstream stream{"file.txt"};
if (!stream) {
    ofstream out { "file.txt" }; // fstream can't open files according to lecture. cppreference.com disagrees.
    out.close();
    stream.open("file.txt");
}
```
* **Binary files don't have EOF characters!**
