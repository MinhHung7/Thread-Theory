# Note:Create multiple threat at the same time doesn't guarantee the one is start first
## 5 ways to create thread
### 1. Pointer function
```cpp
void func (int n)
{
	while (n--)
	{
		std::cout << n << " ";
	}
}
int main ()
{
	std::thread t1 (func, 10);
	std::thread t2 (func, 11);

	t1.join ();
	t2.join ();
	return 0;
}
```
### 2. Lamda function
**Cach 1**
```cpp
int main ()
{
	auto func = [](int n)
	{
		while (n--)
		{
			std::cout << n << " ";
		}
	};
	std::thread t1 (func, 10);
	t1.join ();
	return 0;
}
```
**Cach 2**
```cpp
int main ()
{
	std::thread t1 ([](int n)
	{
		while (n--)
		{
			std::cout << n << " ";
		}
	}, 10);

	t1.join ();
	return 0;
}
```
### 3. Functor (function object)
```cpp
class Base
{
public:
	void operator()(int n)
	{
		while (n--)
		{
			std::cout << n << " ";
		}
	}
};

int main ()
{
	std::thread t1 (Base (), 15);
	t1.join ();
	return 0;
}
```
### 4. Non-static member function
```cpp
class Base
{
public:
	void run (int n)
	{
		while (n--)
		{
			std::cout << n << " ";
		}
	}
};

int main ()
{
	Base b;
	std::thread t1 (&Base::run, &b, 10);
	t1.join ();
	return 0;
}
```
### 5. Static member function
```cpp
class Base
{
public:
	static void run (int n)
	{
		while (n--)
		{
			std::cout << n << " ";
		}
	}
};

int main ()
{
	std::thread t1 (&Base::run, 10);
	t1.join ();
	return 0;
}
```
