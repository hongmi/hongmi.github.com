---
layout: post
title:  C++ const成员函数和非const成员函数的一个转换
category : cpp
tags : [cpp, left, const, reference]
---
{% include JB/setup %}

其中在const和non-const成员函数之中避免了重复代码

    #include <cstddef>

    class Array {
    public:
      Array(std::size_t size) : data(new int[size]) {}
      ~Array() { delete []data; }

      const int& operator[](std::size_t size) const {
          return data[size];
      }

      int & operator[](std::size_t size) {
        return const_cast<int &>(static_cast<const Array&>(*this)[size]);
      }

      int *data;
    };

    int main(int argc, char* argv[])
    {
      Array a(5);
      a[1] = 1;
      int i = a[2];
      return 0;
    }

