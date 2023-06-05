# For 280 Exam I


## 1. Pointers, References, and functions

### 1.1 Object can be passed as reference

    int *banana (int &c, int*d) {
	    c += 1;
	    *d += 1;
	    return &c;
    }
	
	int main() {
		int x = 2; int y = 3;
		banana(x, &y);
		cout << x << " " << y << endl;

Above code would compile and would print "3 4".

In the stack memory of the function banana, c is bound to the object x, and when the lifetime of c dies, c then no longer bound to x. The takeaway is we could put variable directly in.

## 1.2 lifetime of local variable and when there is a real problem

Compile successfully:

    int * apple(int a, int *b) { 
	   a += 1; 
	   b += 1; 
	   return &a;
    }
    
    int main(){
	    int x = 2; int y = 3; 
	    apple(x, &y); 
	    cout << x << " " << y << endl;
    }

The above program does not crash. The explanataion:

> Both a and b are passed by value (b is passed by pointer, which is a kind of pass by value). So neither of the modifications to a and b have any effect. The apple function returns the address of a local variable, which could lead to problems, but the program never uses the return, so there's no undefined behavior.

Compile unsuccessfully:

    int x = 2; 
    int y = 3; 
    int *z = apple(x, &y); 
    cout << *z << endl;

Reason:

> The apple function returns the address of a local variable, and this is assigned into z and dereferenced, which causes undefined behavior (since the lifetime of the local variable ended after its containing function returned)

## 1.3 array and pointer

Array are Pointers.

    int arr[2] == {2, 4};
    cout << *arr; //2
    cout << *arr + 1; //3
    cout << *(arr + 1); //4
    cout << arr;   // 0x2710 (the address of arr[0])
    cout << arr + 1; // 0x2714 (the address of arr[1])

Char Arrays are special:

    const char *cstring = "abc"; // valid c-string
    char arr[] = {'a','b'}; //c++string
    char arr1[] = {'a','b','\0'} //c-string

operations on c-string

    cout << cstring;	//abc
    cout << cstring+1;	//bc
    cout << arr;		//abab
    cout << arr1;		//ab
	cout << *arr1;		//a


## 2 Classes, Polymorphisms


### 2.1 constructors

constructors initialization; statement should be put inside {}. see below:

    Bread::Bread(const string &kind_in):
						 kind(kind_in), toasted(false) 
				 {assert (kind_in == "white" || kind_in == "wheat");
}

Always remember to check default constructors.

### 2.2 Const functions

Functions need const at last.

### 2.3 Base and derived class and pointers

 - Base class pointers can point to derived class
 - Base class pointer can access virtural functions in derived class
 - Base class pointer can access its own private or public or protected datas
 - Base class pointer cannot access variables that are unique inside the derived class
 - Derived class pointer cannot point to base class
 - Pointer intialization does not construct an object so there is no constructor involved
 - Pointer just saves the address
 - However, Derived class can access the functions and (not-private) variables from its base class
 - If a derived class pointer ask a function/variable it does not have but its base class has, then going from level by level to find that function/variable from the hierarchy, and the function could be virtual or non-virtual or overriden.






