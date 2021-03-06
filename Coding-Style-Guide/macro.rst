12. 宏
============

12-1：用宏定义表达式时，要使用完备的括号。 

**示例：** 如下定义的宏都存在一定的风险。 

.. code-block:: c

    #define RECTANGLE_AREA( a, b ) a * b 
    #define RECTANGLE_AREA( a, b ) (a * b) 
    #define RECTANGLE_AREA( a, b ) (a) * (b) 
    正确的定义应为： 
    #define RECTANGLE_AREA( a, b ) ((a) * (b)) 

12-2:将宏所定义的多条表达式放在大括号中。 

**示例：** 下面的语句只有宏的第一条表达式被执行。为了说明问题， ``for`` 语句的书写稍不符规范。 

.. code-block:: c

    #define INTI_RECT_VALUE( a, b )\ 
        a = 0;\ 
        b = 0; 
    
    for (index = 0; index < RECT_TOTAL_NUM; index++) 
    INTI_RECT_VALUE( rect.a, rect.b ); 
    
正确的用法应为： 

.. code-block:: c

    #define INTI_RECT_VALUE( a, b )\ 
    {\ 
        a = 0;\ 
        b = 0;\ 
    } 
    
    for (index = 0; index < RECT_TOTAL_NUM; index++) 
    {  
    INTI_RECT_VALUE( rect[index].a, rect[index].b ); 
    } 

12-3:使用宏时，不允许参数发生变化。

**示例：** 如下用法可能导致错误。 

.. code-block:: c

    #define SQUARE( a ) ((a) * (a)) 
 
    int a = 5; 
    int b; 
    b = SQUARE( a++ ); // 结果：a = 7，即执行了两次增 1。 
 
正确的用法是： 

.. code-block:: c

    b = SQUARE( a ); 
    a++; // 结果：a = 6，即只执行了一次增 1。
