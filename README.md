# Single-Header-Utility

## USAGE EXAMPLE

### TimeChecker.h

```
#include "3rdParty/TimeChecker.h"

//using Lambda
auto elapsedTimeMS = SPIN::TimeCheck([&]{
 // Your function
 
});
std:: cout << "Elapsed Time : << elapsedTimeMS << " ms" << std::endl;
```

### Logger.h

```
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

### IO.h


```
#include "3rdParty/IO.h"

//your file io code
template<>
Object_t IO::read<Object_t, ObjectType>(std::string filename){
 //your code
}

Object_t data = IO::read<Object_t, ObjectType(filePath.string());
```
