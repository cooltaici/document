**leetcode刷题**：https://github.com/arkingc/leetcode

## C++容器类使用
### 1.1 string
string()
string( size_type length, char ch)
string( const char *str )
stirng( const char *str, size_type length )
string( string &str, size_type index, size_type length )
string( input_iterator start, input_iterator end )
string &append( const string &str )
string &append( const char *str )
string &assign( const string &str )
string &assign( const char *str)
string &assign( const char *str, size_type num )
char &at( size_type index )  //index处的字符串
iterator begin() //迭代器：首字母
iterator end()    //迭代器：结尾字母的下一个
const char* c_str()
const char* data()  //指向string的字符串地址，返回的不可以更改
bool empty()      // 判断是否为空
int compare( const string &str)     //比较
iterator erase( iterator pos)   //删除pos指向的字符，并指向下一个字符的迭代器
iterator erase( iterator start, iterator end)
size_type find( const string &str, size_type index)
size_type find( const char *str, size_type index )
size_type find_last_of( const string &str, size_type index = npos)  //查找
size_type find_last_of( const char *char, size_type inde =npos)
iterator insert( iterator i, const char &ch )  //插入
string &insert( size_type index, const string &str )
string &insert( size_type index, const char *str )
size_type length()  //长度
size_type size()      //长度
string &replace( size_type index, size_type num, const string &str )  //替换
string substr( size_type index, size_type num = npos )  //子字符串

###vector
vector()
vector( size_type num, const TYPE &val )
vector( const vector &from )
vector( input_iterator start, input_iterator end )
void assign( input_iterator start, input_iterator end )
void assign( size_type num, const TYPE &val )
TYPE at( size_type loc )
TYPE back()
TYPE front()
void clear() //清除
bool empty() //判断
iterator erase( iterator loc )   //删除loc的位置
iterator erase( iterator start, iterator end ) //
iterator insert( iterator loc, const TYPE &val )    //
void insert( iterator loc, size_type num, const TYPE &val )  //插入num个val
void insert( iterator loc, input_iterator start, input_iterator end ) //插入迭代器之间的
void pop_back();     //删除当前vector最末的一个元素
void push_back();   //添加值为val的元素到当前vector的末尾
size_type size();    //vector数组的大小

### map
iterator begin()
iterator end()
void clear()   //删除map中的所有元素
size_type count( const KEY_TYPE &key )  //统计map中key值为的个数
bool empty()      //判断是否为空
pair equal_range( const KEY_TYPE& key ) //返回两个迭代器
void erase( iterator pos )   //删除元素
void erase( iterator start, iterator end )
iterator find( const KEY_TYPE &key )
iterator insert( iterator pos, const pair<KEY_TYPE, VALUE_TYPE> &val )
size_type size()   //返回map容器大小
iterator lower_bound( const KEY_TYPE &val )  //返回键值<=key的第一个元素
iterator upper_bound( const KEY_TYPE &val )

##set
iterator begin()
iterator end()
void clear()
size_type count( const KEY_TYPE &key )
bool empty()
void erase( iterator i )
void erase( iterator start, iterator end )
iterator find( const key_type &key )
iterator insert( iterator i, const TYPE &val )
size_type size()
iterator lower_bound( const key_type &key )
iterator upper_bound( const key_type &key )
###list



int a[10] = { 9, 0, 1, 2, 3, 7, 4, 5, 100, 10 };
sort(a, a +10);                //数组排序
vector<int> a(10,1);
sort(a.begin(), a.end());   //vector排序

char sa[12];
char* sa1 = new char[100];
cin >> sa;                        //结束部分有"\0"
cin >> sa1;                      //结束部分有"\0"
