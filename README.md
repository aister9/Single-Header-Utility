# Single-Header-Utility

A lightweight header-only utility library for common tasks such as timing, logging, and file I/O.
No build or linking required — just include and use.

### 🚀 Features
- ⏱️ TimeChecker  
Measure execution time using simple lambda-based API
- 📝 Logger  
Structured logging (CSV format) with variant-type support
- 📂 IO  
Customizable file input/output via template specialization

## 📦 Installation
Simply include the headers:
```C++
#include "3rdParty/TimeChecker.h"
#include "3rdParty/Logger.h"
#include "3rdParty/IO.h"
```
No additional setup is required.

## 🛠️ USAGE EXAMPLE

### ⏱️ TimeChecker.h

```C++
#include "3rdParty/TimeChecker.h"

//using Lambda
auto elapsedTimeMS = SPIN::TimeCheck([&]{
 // Your function
 
});
std:: cout << "Elapsed Time : << elapsedTimeMS << " ms" << std::endl;
```

### 📝 Logger.h

```C++
#include "3rdParty/Logger.h"

SPIN::Logger log;
log.filePath = "log.csv";

//Your data - int, float, double, string
log.data["DATA_NAME"].push_back(value);
...

bool fileExists = std::filesystem::exists(log.filePath);

td::ofstream logOut(log.filePath, std::ios::app);

if (!fileExists) {
	logOut << log;
}
else {
	int t_size = log.data.begin()->second.size();
	for (int i = 0; i < t_size; i++) {
		for (auto& v : log.data) {
			std::visit([&logOut](auto&& arg) {logOut << arg << ";"; }, v.second[i]);
		}
		logOut << std::endl;
	}
}
logOut.close();
```

### 📂 IO.h


```C++
#include "3rdParty/IO.h"

//your file io code
template<>
Object_t IO::read<Object_t, ObjectType>(std::string filename){
 //your code
}

Object_t data = IO::read<Object_t, ObjectType(filePath.string());
```
