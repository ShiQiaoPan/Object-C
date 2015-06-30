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
***
便利构造法:
 + (classname *)classNameWith参数
***
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
***
使用NSNumberFormatter对NSNumber与NSString转化
```
		 
		 NSNumber *floatNumber = [NSNumber numberWithFloat:100.0500];
         NSLog(@"number = %@", floatNumber);
         NSNumberFormatter *formatter = [[NSNumberFormatter alloc] init];
         [formatter setNumberStyle:NSNumberFormatterNoStyle];
                      //设置数字格式  无格式、short、long格式
         NSString *numberString = [formatter stringFromNumber:floatNumber];
         NSLog(@"number string = %@", numberString);
***
#NSValue  NSNumber
NSValue 可以把简单的复杂的数据类型封装为对象 

		NSValue *pointValue = [NSValue valueWithPoint:NSMakePoint(10, 10)];
        NSValue *sizeValue  = [NSValue valueWithSize:NSMakeSize(20, 20)];
        NSValue *rectValue  = [NSValue valueWithRect:NSMakeRect(0, 0, 20, 20)];
         
         NSNumber *floatNumber = [NSNumber numberWithFloat:100.0500]       

#NSDate AND NSTimer
##NSDate 
    NSDateFormatter *formatter = [[NSDateFormatter alloc]init];
    [formatter setDateFormat : @"yyyyMMdd"];//设置格式
    //也可以设置时区
    [formatter setTimeZone:[NSTimeZone timeZoneForSecondsFromGMT:8]];
    输出即会按照格式输出
##NSTimer

      
      TImer * timer = [[TImer alloc]init];
      [timer timer];
      [[NSRunLoop currentRunLoop]run];
      -(void)timerInfo
	{
	    _seconds++;
	    NSString * string = [NSString stringWithFormat:@"%.2d:%.2d:%.2d", _seconds / 3600, (_seconds / 60) % 60, _seconds % 60];
	    
	    NSLog(@"%@",string);
	    
	}
	-(void)timer
	{
	    [NSTimer scheduledTimerWithTimeInterval:1 target:self selector:@selector(timerInfo) userInfo:nil repeats:YES];
	}
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
***	
			NSNumericSearch: 比较字符串长度
         // NSCaseInsensitiveSearch: 大小写不敏感比较
         // NSLiteralSearch: 完全比较，比较大小写
         NSComparisonResult result = [string1 compare:string2 options:NSNumericSearch | NSCaseInsensitiveSearch];

***

#NSArray

Oc集合类只能接受对象<br>
[NSArray array]可简写为@[]<br>
[NSAarray arrarwithObject : a] 可简写为:@[a]<br>

[NSDictionary dictionary]可简写为@{}<br>
[NSDictionary dictionaryWithObject:o1 forKey:k1】 可简写为@{k1:o1, k2:o2}<br>

sortedArrayUsingSelector:@selector(compare:)];//选择器排序<br>
sortedArrayUsingComparator:^NSComparisonResult(id obj1, id obj2)<br>
NSOrderDescending/递减Ascending/递增
***

##NSARRAY怎么直接打印数组打印中文字符<br>
1)添加类NSArray+Log <br>
2)重写 - (NSString *)descriptionWithLocale:(id)locale<br>
```oc
		
		@implementation NSArray (Log)(log不可改)
		- (NSString *)descriptionWithLocale:(id)locale {
		    NSMutableString *str = [NSMutableString stringWithFormat:@"%lu (\n",(unsigned long)[self count]];
		    for (id obj in self)
		    {
		        [str appendFormat:@"\t%@, \n", obj];
		    }
		    [str appendString:@")"];
		    return str;
		}
		@end
```
- (NSString *)descriptionWithLocale:(id)locale
{
    NSMutableString *strM = [NSMutableString string];
    [strM appendString:@"(\n"];
   
    for (id obj in self) {
        [strM appendFormat:@"\t%@,\n", obj];
    }
    [strM appendString:@")"];

    return strM;
}
```



#内存
```
内存：程序运行中临时分配的存储空间在程序结束后释放。<br>
内存管理：软件运行时对计算机内存资源进行分配和使用的技术。快速高效<br>
reatinCount 计数器<br>
deaalloc : 当对象被释放时才会调用<br>
alloc
retain
release
```

#属性
##
@property (nonatomic , strong, readwrite) (参数类型) 参数名 <br>


***
属性关键字:
***
线程相关的:
nonatomic 非原子性操作:不是很安全其他线程可以改变其值 效率高<br>

生成setter相关的br>
readwrite : setter 和getter都生成br>0
readonly :只读<br>
@property (nonatomic , strong, setName :) (参数类型) 参数名 <br>
对setter方法重命名 加 : (其有参数)getter不加
setter = setName setter重命名<br>
getter = isGetter getter重命名<br>

内存相关的：<br>
strong：强引用 对象默认类型<br>
retain：引用计数+1 strong 相当于 retain<br>
copy：<br>
浅拷贝：指针拷贝不会开辟新的空间---->不可变对象拷贝<br>
深拷贝：拷贝值开辟新的空间--->可变对象拷贝<br>
assign：一般修饰基本数据类型， 引用计数不会改变 基础数据类型<br>
weak:若引用ARC模式 循环引用才会用到 weak相当于assign但比assign多了一个功能即对象消失后自动把指针变成nil<br>
*******************
NSString 用copy delegete(授权代表)用assign 基本数据类型用assign 对象类型用retain
*******************
***
[button3 setText:[button3 text]] 等同于 button3.text = button3.text;
