# Mutex: avoid race condition (Mutual Exclusion)
## Lock() and Unlock()
```cpp
#include<iostream>
#include<thread>
#include<chrono>
using namespace std;
std::mutex m;
int myAmount = 0;
void add ()
{
	m.lock ();
	++myAmount;
	m.unlock ();
}

int main ()
{
	std::thread t1 (add);
	std::thread t2 (add);

	t1.join ();
	t2.join ();

	cout << myAmount << " ";
}
```
## std::try_lock()
