[std::bitset - cppreference.com](https://zh.cppreference.com/w/cpp/utility/bitset)
与`std::vector<bool>`的关系类似于`std::array<T, N>`与`std::vector<T>`的关系，也就是同种元素的定长/非定长容器

1. 可以由字符串或整形构造得到
2. operator[]访问特定位
3. 各种位操作的语法糖支持
4. to_string等转换函数
5. 大部分成员函数支持`constexpr`，提供很大便利