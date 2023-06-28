# JOIN
```cpp
#include<iostream>
#include<thread>
#include<chrono>
using namespace std;
void run (int n)
{
	while (n--)
	{
		cout << "Minh Hung\n";
	}
	std::this_thread::sleep_for (chrono::seconds (3));
}

int main ()
{
	std::thread t1 (run, 10);
	cout << "main()\n";
	t1.join ();
	cout << "main() after\n";
	return 0;
}
```
**Terminal:**

main()

Minh Hung

Minh Hung

Minh Hung

Minh Hung

Minh Hung

Minh Hung

Minh Hung

Minh Hung

Minh Hung

Minh Hung

main() after

# Joinable
```cpp
#include<iostream>
#include<thread>
#include<chrono>
using namespace std;
void run (int n)
{
	while (n--)
	{
		cout << "Minh Hung\n";
	}
	std::this_thread::sleep_for (chrono::seconds (3));
}

int main ()
{
	std::thread t1 (run, 10);
	cout << "main()\n";
	if (t1.joinable ())
	{
		t1.join ();
	}
	cout << "main() after\n";
	return 0;
}
```
# Detach
- No wait to finish thread
```cpp
#include<iostream>
#include<thread>
#include<chrono>
using namespace std;
void run (int n)
{
	while (n--)
	{
		cout << "Minh Hung\n";
	}
	std::this_thread::sleep_for (chrono::seconds (5));
}

int main ()
{
	std::thread t1 (run, 10);
	cout << "main()\n";
	t1.detach ();
	cout << "main() after\n";
	return 0;
}
```
