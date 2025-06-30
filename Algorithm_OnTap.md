# **SEARCH** 

***Note***

```cpp
    int array, list = a[];
    int size        = n;
    int finding     = x;
```


## Linear [O(n) / O(1)]

* **Basic**

```cpp

    bool LinearSearch(int a[], int n, int x){
        for(int i=0; i<n; i++){
            if(a[i]==x) return true;
        }
        return false;
    }

```

* **Sentinel**

```cpp
    bool LinearSearch_Sentinel(int a[], int n, int x){
        int last_value=a[n-1];// get, store last value
        a[n-1]=x// change last value into x value ( last_value -> x)

        int i=0; //index
        while (a[i]!=x){
            i++;
        }
        a[n-1] = last_value;
        if (i<n-1|| a[n-1]==key){
            return 1;
        }
        return -1;
    }
```

## Binary [O(n) / O(log n) / O(1)]

```cpp
    bool BinarySearch(int a[], int n, int x){
        int left=0;
        int right=n-1;
        while(left<=right){
            int mid=left+(left-right)/2;
            
            if(a[mid]==x) return true;
            if(a[mid]<x ) left=mid+1;
            else right=mid-1;
        }
        return false;
    }
```

## Interpolation

```cpp

    bool InterpolationSearch(int a[], int n, int x){
        int left=0;
        int right=n-1;
        while(left<= right && a[left] <= x && x >= a[right]){
            if(a[right]==a[left]){
                return a[left]==x;
            }
            int mid = left + ((double)(right - left) / (a[right] - a[left])) * (x - a[left]);


            if(a[mid]==x) return true;
            if(x<a[mid]) right=mid-1;
            else left= mid+1;
        }
        return false;
    }
```

# **SORT**

## Selection - [O(n)^2] - *[Offline]*
```cpp
    void SelectionSort( int a[], int n){
        int min, temp;
        for(int i=0; i<n; i++){
            min=i;
            for(int j=i+1;i<n;j++){
                if(a[min]>a[j]) min=j;// ( '>' == increase sort)
            }
            temp=a[i]; a[i]=a[min]; a[min]=temp;
        }
    }
```
## Insertion - [O(n)^2/ O(n^2) / O(n) ] - *[Online]*
```cpp
    void InsertionSort(int a[], int n){
        int j, temp;
        for(int i=1; i<n; i++){
            temp=a[i];
            for(j=i-1; j>=0&& a[j]>temp;j--){// ('>' == increase sort)
                a[j+1]=a[j];
            }
            a[j+1]=temp;
        }
    }
```
## Heap - [O(n log n)]

## Quick - [O(n^2) / O (n log n)] - *[Offline]*

```cpp
    int pivot(int a[], int left, int right){
        int pivot = a[left];//flex
        int i=left;
        int j=right;

        while(i<j){
            do {i++;} while(a[i]<pivot;)
            do {j--;} while(a[j]<pivot;)

            if(i<j){
                swap(a[i],a[j]);
            }

        }

        swap(a[left],a[j]);//swap pivot
        return j;//return pivot
    }


```
## Merge - [O(n log n)]
```cpp
void merge(int a[], int left, int mid, int right)
{
    int n1 = mid - left + 1;
    int n2 = right - mid;

    int L[n1], R[n2];

    for (int i = 0; i < n1; i++)
        L[i] = a[left + i];
    for (int j = 0; j < n2; j++)
        R[j] = a[mid + 1 + j];

    int i = 0, j = 0;
    int k = left;

    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) {
            a[k] = L[i];
            i++;
        }
        else {
            a[k] = R[j];
            j++;
        }
        k++;
    }

    while (i < n1) {
        a[k] = L[i];
        i++;
        k++;
    }

    while (j < n2) {
        a[k] = R[j];
        j++;
        k++;
    }
}

```
## Bubble - [O(n^2) / O(n)] - *[Offline/ Stable]*

# **LIST**

## Linked List

```cpp

struct NODE{
	int data;
	NODE* next;
};

struct LIST{
	NODE* pHead;
	NODE* pTail;
};

NODE* CreateNewNode(int value);

void CreateEmptyList(LIST &L);

void AddHead(NODE* P);

void AddTail(NODE* P);

void CreateList(LIST &L);

void Delete(NODE* P);

void Print(LIST& L);

```

## Stack
```cpp
struct STACK{
	int arr[];
	int top;
};

void push(int value);

void pop();

void top();

void print();

```

## Queue
```cpp
struct QUEUE{
	int a[];
	int front;
	int rear;
};

void enqueue(int value);

void dequeue();

void pop();

void front();

void print();
```

# **TREE**

## Tree

## Binary Tree

```cpp
/*###Begin banned keyword - each of the following line if appear in code will raise error. regex supported
###End banned keyword*/

#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

struct TNode {
    int key;
	TNode *left, *right;
};

typedef TNode* TREE;

TREE CreateTree(vector<int> pre, vector<int> in, int preB, int preE, int inB, int inE) {
	int i;
	TREE root;
	if (inE < inB) return NULL;
	root = new TNode;
	if (root != NULL) {
		root->key = pre[preB];
		for (i = inB; i <= inE; i++)
			if (in[i] == pre[preB]) break;
		root->left = CreateTree(pre, in, preB+1, preE, inB, i - 1);
		root->right = CreateTree(pre, in, preB+i-inB+1, preE, i+1,inE);
	} return root;
}

//###INSERT CODE HERE -

int main() {
    vector<int> duyetNLR;
    vector<int> duyetLNR;
    Input(duyetNLR);
    Input(duyetLNR);
    int Num=duyetNLR.size()-1;
    TREE root = CreateTree(duyetNLR, duyetLNR, 0, Num, 0, Num);
    Fun(root);
    return 0;
}

// Hàm kiểm tra số nguyên tố
bool isPrime(int n) {
    if (n < 2) return false;
    for (int i = 2; i * i <= n; i++)
        if (n % i == 0) return false;
    return true;
}

// Hàm đếm số node có giá trị là số nguyên tố
int countPrimeNodes(TREE root) {
    if (root == NULL) return 0;
    int count = isPrime(root->key) ? 1 : 0;
    return count + countPrimeNodes(root->left) + countPrimeNodes(root->right);
}

// Hàm nhập dữ liệu
void Input(vector<int> &v) {
    int x;
    while (true) {
        cin >> x;
        v.push_back(x);
        if (x == -1) break;
    }
}

// Hàm chính để gọi và in kết quả
void Fun(TREE root) {
    if (root == NULL) {
        cout << "Empty Tree";
        return;
    }
    cout << countPrimeNodes(root);
}

```

## Binary Search Tree
```cpp
/*###Begin banned keyword - each of the following line if appear in code will raise error. regex supported
###End banned keyword*/

#include <iostream>
using namespace std;

struct TNODE {
	int key;
	TNODE* pLeft;
	TNODE* pRight;
};
typedef TNODE* TREE;

//###INSERT CODE HERE -

int main() {
	TREE T; //hay: TNODE* T;
	T = NULL; // Khoi tao cay T rong, or: CreateEmptyTree(T)
	CreateTree(T);
	PrintTree(T);
	return 0;
}
```

## B-Tree

# **HASH**

## Hash Table
```cpp

/*###Begin banned keyword - each of the following line if appear in code will raise error. regex supported
define
include
###End banned keyword*/

#include <iostream>
#include <string>

#define LOAD 0.7
using namespace std;

struct Hocsinh {
    int Maso;
    string Hoten;
    int Namsinh;
    bool Gioitinh;
    double TBK;
};

struct Node {
    Hocsinh data;
    Node *next;
};

struct List {
    Node * head, *tail;
};

Node * CreateNode(Hocsinh);
void CreateList(List &);
void AddTail(List&, Hocsinh);
int RemoveHead(List &);
int RemoveAfter(List &, Node *);
void DeleteList(List &);

struct Hashtable {
    int M; // Kich thuoc bang bam
    int n; // so phan tu trong bang bam
    List *table;
};

void CreateHashtable(Hashtable &, int);
int Hash(Hashtable, int); // Ham bam ma so hoc sinh thanh chi so
int Insert(Hashtable &, Hocsinh);
void PrintHashtable(Hashtable);
void DeleteHashtable(Hashtable &);

void Input(Hocsinh &x) {
    cin >> x.Maso;
    getline(cin>>ws, x.Hoten);
    cin >> x.Namsinh;
    cin >> x.Gioitinh;
    cin >> x.TBK;
}
int main()
{
    Hashtable hashtable;

    int m, n;
    Hocsinh hs;

    cin >> m;
    CreateHashtable(hashtable, m);
    cin >> n;
    for (int i = 0; i < n; i++) {
        Input(hs);
        Insert(hashtable, hs);
    }
    PrintHashtable(hashtable);
    DeleteHashtable(hashtable);
    return 0;
}
void CreateList(List &l) {
    l.head = l.tail = NULL;
}

Node * CreateNode(Hocsinh x) {
    Node *p = new Node;
    if (p == NULL)
        exit(1);
    p->next = NULL;
    p->data = x;
    return p;
}

void AddTail(List &l, Hocsinh x) {
    Node *p = CreateNode(x);
    if (l.head == NULL)
        l.head = l.tail = p;
    else {
        l.tail->next = p;
        l.tail = p;
    }
}

int RemoveHead(List &l) {
    if (l.head == NULL)
        return 0;
    Node *p = l.head;
    l.head = p->next;
    if (l.tail == p)
        l.tail = NULL;
	delete p;
    return 1;
}

int RemoveAfter(List &l, Node *q) {
    if (l.head == NULL)
        return 0;

    if (q == NULL)
        return RemoveHead(l);

    Node *p = q->next;
    q->next = p->next;
    if (l.tail == p)
        l.tail = q;
    delete p;
    return 1;
}

void DeleteList(List &l) {
    while (l.head) {
        Node *p = l.head;
        l.head = p->next;
        delete p;
    }
    l.head = l.tail = NULL;
}

void CreateHashtable(Hashtable &ht, int m) {
    ht.table = new List[m];
    for (int i = 0; i < m; i++)
        CreateList(ht.table[i]);
    ht.M = m;
    ht.n = 0;
}

int Hash(Hashtable ht, int maso) {
    return maso % ht.M;
}

void PrintHashtable(Hashtable ht) {
    for (int i = 0; i < ht.M; i ++) {
        Node *p = ht.table[i].head;
        while (p) {
            Hocsinh hs = p->data;
            cout << '[' << hs.Maso << ",  " << hs.Hoten << "  , " << hs.Gioitinh << ", " << hs.Namsinh << ", " << hs.TBK << "] ";
            p = p->next;
        }
        cout << '\n';
    }
}

void DeleteHashtable(Hashtable &ht) {
    for (int i = 0; i < ht.M; i++) {
        DeleteList(ht.table[i]);
    }
    delete [] ht.table;
    ht.table = NULL;
    ht.M = 0;
}


int Insert(Hashtable &ht, Hocsinh x) {
    // Kiểm tra hệ số tải, nếu vượt quá 70% thì không thêm
    if (ht.n >= ht.M * LOAD) return 0;

    // Tính chỉ số bảng băm từ mã số học sinh
    int index = Hash(ht, x.Maso);

    // Kiểm tra trùng lặp mã số trong danh sách tại chỉ số
    Node *p = ht.table[index].head;
    while (p) {
        if (p->data.Maso == x.Maso) return 0; // Mã số đã tồn tại
        p = p->next;
    }

    // Thêm học sinh vào cuối danh sách tại chỉ số
    AddTail(ht.table[index], x);
    ht.n++; // Tăng số phần tử trong bảng băm
    return 1; // Thêm thành công
}

```
## Direct Chaining

## Coalesced Chaining

## Linear probing

## Quadratic probing

## Double hasing

## Rehasing

# **GRAPH** 

## Graph

## DFS

## BFS

## Dijkstra