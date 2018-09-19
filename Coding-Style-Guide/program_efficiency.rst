8. 程序效率
=============

8-1：编程时要经常注意代码的效率。 

**说明：** 代码效率分为全局效率、局部效率、时间效率及空间效率。全局效率是站在整个系统的角度上的系统效率；局部效率是站在模块或函数角度上的效率；时间效率是程序处理输入任务所需的时间长短；空间效率是程序所需内存空间，如机器代码空间大小、数据空间大小、栈空间大小等。 

8-2：在保证软件系统的正确性、稳定性、可读性及可测性的前提下，提高代码效率。 

**说明：** 不能一味地追求代码效率，而对软件的正确性、稳定性、可读性及可测性造成影响。  

8-3：局部效率应为全局效率服务，不能因为提高局部效率而对全局效率造成影响。 

8-4：通过对系统数据结构的划分与组织的改进，以及对程序算法的优化来提高空间效率。 

**说明：** 这种方式是解决软件空间效率的根本办法。 

**示例：** 如下记录学生学习成绩的结构不合理。 

.. code-block:: c

    typedef unsigned char  BYTE; 
    typedef unsigned short WORD; 
    
    typedef struct 
    {
    BYTE name[8]; 
        BYTE age; 
        BYTE sex; 
        BYTE class; 
        BYTE subject; 
        float score; 
    }S_STUDENT_SCORE; 
 
因为每位学生都有多科学习成绩，故如上结构将占用较大空间。应如下改进（分为两个结
构） ，总的存贮空间将变小，操作也变得更方便。

.. code-block:: c

    typedef struct 
    { 
        BYTE name[8]; 
        BYTE age; 
        BYTE sex; 
        BYTE class; 
    }S_STUDENT; 
    
    typedef struct
    { 
        WORD student_index; 
        BYTE subject; 
        float score; 
    }S_STUDENT_SCORE; 

8-5：循环体内工作量最小化。 

**说明：** 应仔细考虑循环体内的语句是否可以放在循环体之外，使循环体内工作量最小，从而提高程序的时间效率。 

**示例：** 如下代码效率不高。

.. code-block:: c

    for (ind = 0; ind < MAX_ADD_NUMBER; ind++) 
    { 
        sum += ind; 
        back_sum = sum; /* backup sum */ 
    } 
 
语句 ``back_sum = sum;`` 完全可以放在 ``for`` 语句之后，如下。

.. code-block:: c

    for (ind = 0; ind < MAX_ADD_NUMBER; ind++) 
    { 
        sum += ind; 
    } 
    back_sum  = sum; /* backup sum */ 

8-6：仔细分析有关算法，并进行优化。 

8-7：仔细考查、分析系统及模块处理输入（如事务、消息等）的方式，并加以改进。 

8-8：对模块中函数的划分及组织方式进行分析、优化，改进模块中函数的组织结构，提高程序效率。 

**说明：** 软件系统的效率主要与算法、处理任务方式、系统功能及函数结构有很大关系，仅在代码上下功夫一般不能解决根本问题。 

8-9：编程时，要随时留心代码效率；优化代码时，要考虑周全。 

8-10：不应花过多的时间拼命地提高调用不很频繁的函数代码效率。 

**说明：** 对代码优化可提高效率，但若考虑不周很有可能引起严重后果。 

8-11：要仔细地构造或直接用汇编编写调用频繁或性能要求极高的函数。 

**说明：** 只有对编译系统产生机器码的方式以及硬件系统较为熟悉时，才可使用汇编嵌入方式。嵌入汇编可提高时间及空间效率，但也存在一定风险。 

8-12：在保证程序质量的前提下，通过压缩代码量、去掉不必要代码以及减少不必要的局部和全局变量，来提高空间效率。 

**说明：** 这种方式对提高空间效率可起到一定作用，但往往不能解决根本问题。 

8-13：在多重循环中，应将最忙的循环放在最内层。 

**说明：** 减少 CPU 切入循环层的次数。 

**示例：** 如下代码效率不高。 

.. code-block:: c

    for (row = 0; row < 100; row++) 
    { 
        for (col = 0; col < 5; col++) 
        { 
            sum += a[row][col]; 
        } 
    } 
 
可以改为如下方式，以提高效率。 

.. code-block:: c

    for (col = 0; col < 5; col++) 
    { 
        for (row = 0; row < 100; row++) 
        { 
            sum += a[row][col]; 
        } 
    } 

8-14：尽量减少循环嵌套层次。 

8-15：避免循环体内含判断语句，应将循环语句置于判断语句的代码块之中。 

**说明：** 目的是减少判断次数。循环体中的判断语句是否可以移到循环体外，要视程序的具体情况而言，一般情况，与循环变量无关的判断语句可以移到循环体外，而有关的则不可以。 

**示例：** 如下代码效率稍低。 

.. code-block:: c

    for (ind = 0; ind < MAX_RECT_NUMBER; ind++) 
    { 
        if (data_type == RECT_AREA) 
        { 
            area_sum += rect_area[ind]; 
        } 
        else 
        { 
            rect_length_sum += rect[ind].length; 
            rect_width_sum += rect[ind].width; 
        } 
    } 
 
因为判断语句与循环变量无关，故可如下改进，以减少判断次数。 

.. code-block:: c

    if (data_type == RECT_AREA) 
    { 
        for (ind = 0; ind < MAX_RECT_NUMBER; ind++) 
        { 
            area_sum += rect_area[ind]; 
        } 
    } 
    else 
    { 
        for (ind = 0; ind < MAX_RECT_NUMBER; ind++) 
        { 
            rect_length_sum += rect[ind].length; 
            rect_width_sum  += rect[ind].width; 
        } 
    } 

8-16：尽量用乘法或其它方法代替除法，特别是浮点运算中的除法。 

**说明：** 浮点运算除法要占用较多 CPU 资源。 

**示例：** 如下表达式运算可能要占较多 CPU 资源。 

.. code-block:: c

    #define PAI 3.1416 
    radius = circle_length / (2 * PAI); 
 
应如下把浮点除法改为浮点乘法。 

.. code-block:: c

    #define PAI_RECIPROCAL (1 / 3.1416 ) // 编译器编译时，将生成具体浮点数 
    radius = circle_length * PAI_RECIPROCAL / 2;  

8-17：不要一味追求紧凑的代码。 

**说明：** 因为紧凑的代码并不代表高效的机器码。
