> **问题：**
>
> 1. 前置后值自增运算符的重载，返回引用还是对象

**静态成员变量**

- 与一般的数据成员不同，无论建立了多少个对象，都只有一个静态数据的拷贝。静态成员变量，属于某个类，所有对象共享。因此修改值全局修改所有对象的这个值。
- 静态变量，是在编译阶段就分配空间，对象还没有创建时，就已经分配空间。

```c++
class Person{
public:
	//类的静态成员属性
	static int sNum;
private:
	static int sOther;
};

//类外初始化，初始化时不加static
int Person::sNum = 0;
int Person::sOther = 0;
int main(){


//1. 通过类名直接访问
Person::sNum = 100; //实际上当作在类中访问初始化
cout << "Person::sNum:" << Person::sNum << endl;//error

//2. 通过对象访问
Person p1, p2;
p1.sNum = 200;
```

**静态成员函数**

静态成员函数使用方式和静态变量一样，同样在对象没有创建前，即可通过类名调用。静态成员函数主要为了访问静态变量，但是，不能访问普通成员变量。

如果一个类的成员，既要实现共享，又要实现不可改变，那就用 static const 修饰。定义静态const数据成员时，最好在类内部初始化。

**单例模式**

- 为了让类只有一个实例，实例不需要自己释放
- 对默认构造函数、拷贝构造函数进行私有化
- 内部维护一个对象指针
- 私有化唯一指针
- 对外提供getinstance方法来访问这个指针
- 保证类中只能实例化唯一一个对象

**this指针**

编译器会加入一个this指针，指向被调用的成员函数所属的对象。this指针是隐含在对象成员函数内的一种指针，隐含与非静态成员函数。

如果是静态没有，静态成员变量是默认共享的。

```c++
void compare(Person &p){
    if(this->age == p.age){ //此时不加this也能区分，因为是用p作引用
        cout<<"111";
    }
    else{
        cout <<"222";
    }
}
```

**空指针访问成员函数**

```c++
void show(){
    cout<<1<<endl;
}
void showage(){
    if(this == NULL){ //防止空指针调用崩溃，NULL -> m_age error
        return;
    }
    cout<<this->m_Age<<endl;
}
```

**常函数与常对象**

```c++
void showInfo() const{
    this->m_A = 1;//error,不允许修改指针指向的值
    this->m_B = 2;//true
    cout<<m_A<<" "<<m_B<<endl;
}
int m_A;
mutable int m_B;//就算是常函数也可以修改

const Person p2;//只读，可以调用常函数，不可以调用普通函数

```

**友元**

程序员可以把一个全局函数、某个类中的成员函数、甚至整个类声明为友元，使得可以访问。

友元函数的声明可以放在类的私有部分，也可以放在公有部分，它们是没有区别的，都说明是该类的一个友元函数。

使得外部函数可以获取private数据，但是破坏了类的封装性。

在类的声明处，增加friend关键字

```c++
//全局函数做友元函数
friend void CleanBedRoom(Building& building);
```

成员函数作友元类

```c++
friend void MyFriend::LookAtBedRoom(Building& building);
```

**重载运算符的意义**



**加号运算符重载**

如果想让自定义数据类型进行 + 运算，就需要重载。定义重载的运算符就像定义函数，只是该函数的名字是operator@,这里的@代表了被重载的运算符。

- 使用成员函数进行相加，还可以用Person operator+(Person&p) 
- 像这种没有使用local变量的，还是尽量使用返回值的引用传递

```c++
Complex& operator+(Complex& p) {
		//Complex tmp;
		//tmp.m_A = this->m_A + p.m_A;
		//return tmp;
		this->m_A += p.m_A;
		return *this;
	}

```

- 利用全局函数进行重载， Person operator+(Person&p1，Person&p2)

```c++
Complex operator+(Complex& p1, Complex& p2) {
	Complex tmp;
	tmp.m_A = p1.m_A + p2.m_A;
	return tmp;
}
```

- 二者都能被计算机识别，实现类的成员属性直接相加。自定义拷贝函数时，系统不默认提供构造函数，要手写,注意需要添加友元 

```c++
friend Complex operator+(Complex& p1, Complex& p2);
public:
	Complex() {
	}
	Complex(int a) {
		m_A = a;
	}
```

**左移运算符重载**

只能写到全局函数部分。

```c++
//左移只能定义在全局
ostream& operator<<(ostream& cout, Complex p) {
	return cout << "m_A = " << p.m_A << endl;
}
```

不要滥用。

返回值是一个ostream，为了应付连续的输出，应对下一个输出，例如：`cout<< c1 <<endl;`

cout<< c1 的返回值是一个ostream，继续输出endl；

**前置后置递增运算符重载**

```c++
//全局
Complex& operator++(Complex& p) {
	p.m_A++;
	return p;
}

//成员函数
Complex& operator++() {
    this->m_a++;
    return *this;
}
```

```c++
//后置
//成员函数
Complex operator++(int) { //通过占位参数区分前置后置
    Complex tmp = *this;
    m_A++;
    return tmp;
}
```

前置相比后置重载节省了另开的内存空间，效率更高。

注释：为什么前置返回引用，后置返回值

> 前置返回引用，才能实现多次自增，否则只是对临时值的自增，且返回引用不需要拷贝。
>
> 后置返回值，不能实现多次自增，并且这里也可以看到后置++ 使用了local变量。

**赋值运算符重载**

解决浅拷贝导致的问题。

```c++
//重载 = 赋值运算符
Person2& operator= ( const Person2 & p)
{
    //判断如果原来已经堆区有内容，先释放
    if (this->pName != NULL)
    {
        delete[] this->pName;
        this->pName = NULL;
    }

    this->pName = new char[strlen(p.pName) + 1];
    strcpy(this->pName, p.pName);

    return *this;
}
```

返回引用，可以实现 p1=p2 =p3

**[ ]运算符重载**

**取反操作重载**

注意：

- 在默认提供拷贝构造时，要手补无参构造，有参构造。

- **不要对&& ，|| 重载**
