1.let只在声明的代码块中生效。
2.for循环在子作用域中再次使用let声明for循环中的变量，将不会影响循环；如使用var声明变量，将改变父作用域的值，导致循环失败。
3.let声明的变量不会进行变量提升。