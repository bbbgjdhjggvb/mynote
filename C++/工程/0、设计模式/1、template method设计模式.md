主算法具有稳定的流程框架，具体子步骤通过子类实现的实现，子步骤可以复用，通过虚函数多态实现 __晚绑定__
```c++
class library{
private:
	void step1();
    void step4();
    void step5();
public:
    void run(){
        this->step1();    
        this->step2();
        this->step3();
        this->step4();
        this->step5();
    }
protected:
    virtual void step2() = 0;
    virtual void step3() = 0;
};
```
由如下结构转向另外一中结构
![[Pasted image 20241021115741.png]]
![[Pasted image 20241021115824.png]]