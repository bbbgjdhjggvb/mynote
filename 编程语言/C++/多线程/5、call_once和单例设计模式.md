### call_once
用于确保函数只会执行一次
```c++
class Test {
  private:
    static Test *instance;
    static std::once_flag once;

  public:
    static Test *getInstance() {
        if (instance == nullptr) {
            std::call_once(once, []() {
                instance = new Test;
            });
        }
        return getInstance();
    }
};
Test *Test::instance = nullptr;
```