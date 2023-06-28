```cpp
#include<iostream>
#include<thread>
#include<mutex>

using namespace std;

std::mutex m;
int buffer = 0;

void task (const char* threadNumber, int loop)
{
	std::unique_lock<mutex>lock (m);
	for (int i = 0; i < loop; ++i)
	{
		buffer++;
		cout << threadNumber << " " << buffer << "\n";
	}
}
int main ()
{ 
	std::thread t1 (task, "T0", 10);
	std::thread t2 (task, "T1", 10);

	t1.join ();
	t2.join ();

	return 0;
}
```
