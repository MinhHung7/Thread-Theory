## try_lock_for()
```cpp
#include<iostream>
#include<thread>
#include<mutex>
#include<chrono>

using namespace std;

int cnt = 0;
std::timed_mutex m;

void increase (int i)
{
	//auto now = std::chrono::steady_clock::now ();
	if (m.try_lock_for (std::chrono::seconds (2)))
	{
		++cnt;
		std::this_thread::sleep_for (std::chrono::seconds (1));
		cout << "Thread " << i << " :Entered\n";
		m.unlock ();
	}
	else
	{
		cout << "Thread " << i << " :coudln't enter\n";
	}
}

int main ()
{
	std::thread t1 (increase, 1);
	std::thread t2 (increase, 2);

	t1.join ();
	t2.join ();

	cout << cnt << "\n";

	return 0;

}
```
## try_lock_until()
```cpp
#include<iostream>
#include<thread>
#include<mutex>
#include<chrono>

using namespace std;

int cnt = 0;
std::timed_mutex m;

void increase (int i)
{
	auto now = std::chrono::steady_clock::now ();
	if (m.try_lock_until (now + std::chrono::seconds (2)))
	{
		++cnt;
		std::this_thread::sleep_for (std::chrono::seconds (1));
		cout << "Thread " << i << " :Entered\n";
		m.unlock ();
	}
	else
	{
		cout << "Thread " << i << " :coudln't enter\n";
	}
}

int main ()
{
	std::thread t1 (increase, 1);
	std::thread t2 (increase, 2);

	t1.join ();
	t2.join ();

	cout << cnt << "\n";

	return 0;

}
```
