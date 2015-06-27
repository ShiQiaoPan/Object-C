#objective c 
***
面向对象侧重实现目标的方式和结果<br>
面向过程侧重步骤
***
数值类型:基本类型和对象类型
typedf:<br>
NSInteger => int (long)<br>
CGFloat   => float (double)<br>
NSPoint   => struct_NSPoint结构体<br>

对象类型:<br>
NSString !=> char *<br>
NSNumber !=> int float double bool<br>

NSNumber 只描述有效位数取值时可以可根据需要取任意类型需要什么类型就用方法去取<br>
类方法 self 有具体地址<br>
实例方法 self: 类名 super: 父类<br>
#封装 、 继承、 动态面向对象的特征<br>
##封装
将数据或函数等集合在一个个单元中
##继承
单继承<br>
子类可以拥有父类所有允许子类继承的成员和方法<br>
子类可以修改父类的方法以实现不同
##多态
不同对象对同一消息的响应<br>
可以重写父类的方法<br>
同名方法不同参数或不同返回值允许
***
关键字：<br>
static:在声明时分配内存但在程序运行期间只会分配一次<br>
register:所储存数据经常被访问，存在CPU寄存器中<br>
extern:定义的变量或函数引用了另一个编译单元的变量或函数<br>
const:变量只读值不能修改<br>
***
类方法 + 和实例方法 - <br>
@class 类名 头文件里面预先声明交叉使用时可用

一个类包含另一个类使用之可避免重复编译
***
@作用<br>
关键字起始字符
初始化过程
##setter 和 getter
###setter
```oc

- (void)serStuId:(NSString *)newId {
    _stuId = newId;
}
```
###getter
```
- (NSString *)stuId {
    return _stuId;
}
```
#NSDate AND NSTimer
##NSTimer
scheduledTimerWithTimeInterval:(NSTimeInterval)seconds  
预订一个Timer,设置一个时间间隔。

表示输入一个时间间隔对象，以秒为单位，一个>0的浮点类型的值，如果该值<0,系统会默认为0.1

 target:(id)aTarget
表示发送的对象，如self

selector:(SEL)aSelector
方法选择器，在时间间隔内，选择调用一个实例方法

userInfo:(id)userInfo
此参数可以为nil，当定时器失效时，由你指定的对象保留和释放该定时器。

repeats:(BOOL)yesOrNo
当YES时，定时器会不断循环直至失效或被释放，当NO时，定时器会循环发送一次就失效。
#NSNumber 
对简单的数据进行封装和解封
##Nsstring
// ios5之后的快速写法:<br>
 NSNumber *number1 = @(123);<br>
 ```oc

     import <Foundation/Foundation.h>

     int main(int argc, const char * argv[]) {
	    @autoreleasepool {
	      // insert code here...
	        NSLog(@"Hello, World!");
	        NSNumber *number = [NSNumber numberWithInt:12345];
	        NSString *string = [[NSString alloc]initWithFormat:@"123"];
	     NSString *string1 = [NSString stringWithFormat:@"123"];
        
        //2个拼接连起来
        NSString *string2 = [NSString stringWithFormat:@"%@%@",string,string1];
        //类方法
        
        NSLog(@"%@",string2);
        NSString *string3 = [string,stringByAppendingString:string1];
        //实例方法

    NSString *string4 = @"12345";
    NSString *string5 = [string4 substringFromIndex:3];//从哪里开始截取不包括该数
    NSLog(@"%@",string5);
    //    NSString *string6 = [string4 substringToIndex:3];//取到哪里包括该数
    //    NSLog(@"%@",string6);    
    
    
    //截取中间数据
    //    NSString *string7 = [[string4 substringFromIndex:1]substringToIndex:3];
    //    NSString *string8 = [string4 substringWithRange:NSMakeRange(1,3)];
    //    NSLog(@"%@%@",string7,string8);
    
    //查找已知字符位置
    //    NSRange range = [string4 rangeOfString:@"23"];
    //    //判断是否查找到
    //    if(range.length > 0){
    //        NSString *string10 = [string4 stringByReplacingCharactersInRange:(range) withString:@"00"];
    //           NSLog(@"%@",string10);//查找到
    //    }
    //    NSLog(@"%@",NSStringFromRange(range));

    //替换
	//    NSString *string9 = [string4 stringByReplacingCharactersInRange:(range) withString:@"11"];
	//    NSLog(@"%@",string9);
	//    //查找不到会崩溃所以加入if
	//    //可变字符串NSMutableString
	//    NSMutableString *string11 = [NSMutableString stringWithFormat:@"123"];
	//    [string11 appendString:@"45"];
	//    [string11 replaceCharactersInRange:range withString:@"000"];
	//    [string11 deleteCharactersInRange:NSMakeRange(1,3)];
	//    [string11 deleteCharactersInRange:NSMakeRange(1,3)];
	//    NSLog(@"%@",string11);
 
    //类型差别
	//    NSMutableString *string12 = [NSString stringWithFormat:@"12"];//错误
	//    NSMutableString *string12 = [string4 substringFromIndex:1];//错误
	//    NSMutableString *string12 = [NSMutableString stringWithFormat:@"%@",[string4 substringFromIndex:1]];
	```
#NSArray

Oc集合类只能接受对象<br>
