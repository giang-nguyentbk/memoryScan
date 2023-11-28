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