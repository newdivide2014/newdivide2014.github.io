# C++ Make_shared使用




## 概念 {#概念}

`make_shared` 是 `C++11` 引入的模板函数，用于创建并返回一个动态分配对象的 `shared_ptr` ，解决了传统 `shared_ptr` 构造方式存在的内存分配和异常安全问题。


## 与传统方式区别 {#与传统方式区别}

-   传统方式需两次内存分配（对象内存 + 控制块内存）， `make_shared` 通过合并分配减少到一次，提升约 30% 性能。
-   若构造函数抛异常， `make_shared` 保证已分配内存自动释放，避免泄漏；传统方式可能因分配分离导致资源泄露。
-   无需重复类型名称，配合 auto 关键字使代码更简洁。 ‌


## 使用场景 {#使用场景}

‌推荐使用场景‌：自定义类型、复杂对象或性能敏感场景。 ‌
避免使用‌场景：当对象需手动管理生命周期（如依赖外部资源释放函数）时，因 `make_shared` 对象内存延迟释放可能导致问题。


## 释放机制 {#释放机制}

`make_shared` 创建的 `shared_ptr` 对象会在‌最后一个引用该对象的 `shared_ptr` 被销毁时‌释放内存

-   释放条件

当没有任何 `shared_ptr` （强引用）指向由 `make_shared` 创建的对象时，该对象会被自动销毁。若存在 `weak_ptr` （弱引用）指向该对象，则不会立即释放，需等待所有弱引用失效后才会销毁。 ‌

-   释放机制

‌单次内存分配优势‌： `make_shared` 将对象本体与控制块（引用计数等）合并分配内存，仅需一次分配。 ‌
自动管理生命周期‌：当最后一个强引用离开时，对象自动销毁，无需手动调用 `delete` ，避免了内存泄漏风险。 ‌


## 示例 {#示例}

```c++
#include <memory>
std::shared_ptr<T> ptr = std::make_shared<T>(Args&&... args);
```

```c++
#include <iostream>
#include <memory>
using namespace std;

struct A{
  int a;
  char b;
  A(int x)：a(x){ cout << "A constructor" << endl; }
  ~A(){}
};

int main()
{
  //使用auto
  auto sp = make_shared<int>(17);
  //new
  shared_ptr<char> spchar<new char('b')>;

  shared_ptr<A> sptr = make_shared<A>();
  cout << sp->a << endl;
  //数组 c++2及更高版本支持
  shared_ptr<int[]> arr = make_shared<int[]>(10);
  for(int i = 0; i < 10; i++) {
    arr[i] = i+1;
  }
  for(int i = 0; i < 10; i++) {
    cout << arr[i] << " "
  }
  cout << endl;
  //C++11/14 不支持 std::make_shared 创建数组，需使用 std::shared_ptr<int[]>(new int[5])
  return 0;
}
```


---

> : 蓝红柿  
> URL: https://newdivide2014.github.io/posts/make-shared/  

