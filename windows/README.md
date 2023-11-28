# Windows version

## Let's get started!
1. Create a simple main.cc program which contains a variable "count" and can be changed by user in runtime.
```c++
#include <unistd.h>
#include <iostream>
#include <cstdlib>
#include <signal.h>

using namespace std;

// Define the function to be called when ctrl-c (SIGINT) is sent to process
void signal_callback_handler(int signum) {
   cout << endl << "Terminating..." <<  endl;
   // Terminate program
   exit(signum);
}

int count = 123;

int main() {

    signal(SIGINT, signal_callback_handler);

    while (true) {
        cout << "Enter value for count: ";
        cin >> count;
        sleep(1);
    }

    return 0;
}
```

2. Compile and test target main.cc program.
```bash
>> g++ -o main main.cc
>> ./main.exe
```

3. Create an example of OpenProcess(...) Windows API function to get a lists of running Processes/Threads based on example from MS.
[Taking a Snapshot and Viewing Processes](https://learn.microsoft.com/en-us/windows/win32/toolhelp/taking-a-snapshot-and-viewing-processes)

4. Add a simple way to identify main.exe process.
```c++
string mainProcessName = "main.exe";
int i = 0;
string processName;
while (pe32.szExeFile[i] != '\0' || i < 256) {
    processName += pe32.szExeFile[i];
    i++;
}
processName += '\0';

if (processName.compare(mainProcessName)) {
    cout << endl << "SUCCESS!!!!!!!!!!!!" << endl;
}
```