#objective c 
nil：指向oc中对象的空指针

Nil：指向oc中类的空指针 

NULL：指向其他类型的空指针，如一个c类型的内存指针

NSNull：在集合对象中，表示空值的对象

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
#NSValue
    
    
    // 便利结构体初始化
         NSValue *pointValue = [NSValue valueWithPoint:NSMakePoint(10, 10)];
         NSValue *sizeValue  = [NSValue valueWithSize:NSMakeSize(20, 20)];
         NSValue *rectValue  = [NSValue valueWithRect:NSMakeRect(0, 0, 20, 20)];
         
         
        
         // 便利解封装
         NSPoint point = [pointValue pointValue];
         NSSize  size  = [sizeValue sizeValue];
         NSRect  rect  = [rectValue rectValue];
         
         
         // 一般初始化
         NSRect rect = NSMakeRect(0, 0, 20, 20);
         NSValue *rectValue = [NSValue valueWithBytes:&rectValue objCType:@encode(NSRect)];
        
         
         // 一般解封装
         [rectValue getValue:&rect];
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
##NSDate 时间
获取当地时间

  类方法
  
    dateString = [NSDateFormatter localizedStringFromDate:[NSDate date] dateStyle:NSDateFormatterFullStyle timeStyle:NSDateFormatterFullStyle];
实例方法

     [formatter setDateStyle:NSDateFormatterFullStyle]; // 配置日期格式，若没有进行配置则不显示日期部分
     [formatter setTimeStyle:NSDateFormatterFullStyle]; // 配置时间格式，若没有进行配置则不显示时间部分
         [formatter setDateFormat:@"yyyy-MM-dd EEEE HH:mm:ss"]; // 配置自定义时间、日期格式
         dateString = [formatter stringFromDate:[NSDate date]]; // NSDate转NSString
         date = [formatter dateFromString:dateString]; // NSString转NSDate
         
         
         NSLog(@"%@", dateString);
         NSLog(@"%@", date);
         [formatter release]; 

    NSDateFormatter *formatter = [[NSDateFormatter alloc]init];
    [formatter setDateFormat : @"yyyyMMdd"];//设置格式
    //也可以设置时区
    [formatter setTimeZone:[NSTimeZone timeZoneForSecondsFromGMT:8]];
    输出即会按照格式输出

##NSTimer
设置定时器
      
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
[NSTimer scheduledTimerWithTimeInterval:1 target:self selector:@selector(timerInfo) userInfo:nil repeats:YES]  
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

// ios5之后的快速写法:<br>
 
 NSNumber *number1 = @(123);<br>
##Nsstring

 
 ```oc

     import <Foundation/Foundation.h>

     int main(int argc, const char * argv[]) {
	    @autoreleasepool {
	    
	        NSNumber *number = [NSNumber numberWithInt:12345];
	        NSString *string = [[NSString alloc]initWithFormat:@"123"];
	     NSString *string1 = [NSString stringWithFormat:@"123"];
        
2个拼接连起来
        
        NSString *string2 = [NSString stringWithFormat:@"%@%@",string,string1];
        //类方法
        
        NSLog(@"%@",string2);
        NSString *string3 = [string,stringByAppendingString:string1];
        //实例方法

    NSString *string4 = @"12345";
截取
    
    NSString *string5 = [string4 substringFromIndex:3];//从哪里开始截取不包括该数
    NSLog(@"%@",string5);
    //    NSString *string6 = [string4 substringToIndex:3];//取到哪里包括该数
    //    NSLog(@"%@",string6);    
    
     
    //截取中间数据
    //    NSString *string7 = [[string4 substringFromIndex:1]substringToIndex:3];
    //    NSString *string8 = [string4 substringWithRange:NSMakeRange(1,3)];
    //    NSLog(@"%@%@",string7,string8);
    
查找已知字符位置
    
    //range = [string1 rangeOfString:@"CD" options:(NSLiteralSearch)];//NSLiteralSearch大小写不敏感
    
    range = [string1 rangeOfString:@"CD" options:(NSCaseInsensitiveSearch)];//NSCaseInsensitiveSearch大小写敏感
    
    NSRange range = [string4 rangeOfString:@"23"];
    
查找替换---判断是否查找到查找不到会崩溃所以加入if
    
    if(range.length > 0){
    NSString *string10 = [string4 stringByReplacingCharactersInRange:(range) withString:@"00"];
       NSLog(@"%@",string10);//查找到
     }
        NSLog(@"%@",NSStringFromRange(range));

替换
	
	    NSString *string9 = [string4 stringByReplacingCharactersInRange:(range) withString:@"11"];
	    NSLog(@"%@",string9);
	    //查找不到会崩溃所以加入if
	    
大小写转换

	NSString *string = @"hello world";
	NSString *uppercaseString  = [string uppercaseString];
	NSString *lowercaseString  = [string lowercaseString];
	NSString *capitalizeString = [string capitalizedString];//首字母大写
    NSLog(@"uppercase:%@  lowercase:%@  capitalize:%@", uppercaseString, lowercaseString, capitalizeString);
可变字符串NSMutableString
	    
	    NSMutableString *string11 = [NSMutableString stringWithFormat:@"123"];
	    [string11 appendString:@"45"];
	    [string11 replaceCharactersInRange:range withString:@"000"];
	    [string11 deleteCharactersInRange:NSMakeRange(1,3)];
	    [string11 deleteCharactersInRange:NSMakeRange(1,3)];
	
	    NSLog(@"%@",string11);
 
类型差别
	
	//    NSMutableString *string12 = [NSString stringWithFormat:@"12"];//错误
	//    NSMutableString *string12 = [string4 substringFromIndex:1];//错误
	//    NSMutableString *string12 = [NSMutableString stringWithFormat:@"%@",[string4 substringFromIndex:1]];
***	
字符串比较

NSComparisonResult比较结果枚举类型<br>

NSStringCompareOptions比较策略枚举类型<br>

NSNumericSearch: 比较字符串长度

NSCaseInsensitiveSearch: 大小写不敏感比较
NSLiteralSearch: 完全比较，比较大小写
         
         NSComparisonResult result = [string1 compare:string2 options:NSNumericSearch | NSCaseInsensitiveSearch];
         
         NSOrderedAscending :升序
         NSOrderedDescending :降序
***

#NSArray AND Dictionary

Oc集合类只能接受对象
[NSArray array]可简写为@[]
[NSAarray arrarwithObject : a] 可简写为:@[a]

[NSDictionary dictionary]可简写为@{}<br>
[NSDictionary dictionaryWithObject:o1 forKey:k1】 可简写为@{k1:o1, k2:o2}<br>

sortedArrayUsingSelector:@selector(compare:)];//选择器排序<br>
sortedArrayUsingComparator:^NSComparisonResult(id obj1, id obj2)<br>
NSOrderDescending/递减Ascending/递增
***

##NSARRAY怎么直接打印数组打印中文字符<br>
1)添加类NSArray+Log （为NSArray添加类目）<br>
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
深拷贝：拷贝值开辟新的空间---><br>
[不可变对象 copy]是假拷贝，等价于[不可变对象 retain]
[不可变对象 mutableCopy是真拷贝
assign：一般修饰基本数据类型， 引用计数不会改变 基础数据类型<br>
weak:若引用ARC模式 循环引用才会用到 weak相当于assign但比assign多了一个功能即对象消失后自动把指针变成nil<br>
*******************
NSString 用copy delegete(授权代表)用assign 基本数据类型用assign 对象类型用retain
*******************
***
[button3 setText:[button3 text]] 等同于 button3.text = button3.text;
#设计模式
##单例模式
生命周期和程序生命周期相同仅能生成一次。且不能被销毁的唯一实例。
     
     #import <Foundation/Foundation.h>

     @interface UserCenter : NSObject <NSCopying>
#创建一个单例
#pragma mark---访问单例的类方法defaultUserCenter /instanceUserCenter
		@property (nonatomic, copy)NSString *userName;
		+ (UserCenter *)sharedUserCenter;
		@end
		
		
		
		#import "UserCenter.h" 

#pragma mark---定义全局的静态变量
		static UserCenter *instance = nil;
		@implementation UserCenter 
		+ (UserCenter *)sharedUserCenter {
		    if (!instance) {//空的时候才创建
		        instance = [UserCenter alloc];
		    }
		    return instance;
		}
#pragma mark---重写alloc方法
    + (instancetype)allocWithZone:(struct _NSZone *)zone {

	    if (!instance) {
	        //保证第一次才创建
	      return [super allocWithZone:zone];
	    }
	    return nil;
	}
#pragma mark---重写copy方法
	- (id)copyWithZone:(NSZone *)zone {
	    return self;
	}
#pragma mark---重写retain release方法
	- (instancetype)retain {
	    return self;
	}
	- (oneway void)release {}
	- (NSUInteger)retainCount {
	    return  NSUIntegerMax;
	}
	@end

#pragma mark---访问单例的类方法defaultUserCenter /instanceUserCenter
	@property (nonatomic, copy)NSString *userName;
	+ (UserCenter *)sharedUserCenter;
    @end
    
    
#prama mark ---amin
    int main(int argc, const char * argv[]) {
    @autoreleasepool {
        UserCenter *user1 = [UserCenter sharedUserCenter];
        UserCenter *user2 = [UserCenter sharedUserCenter];
        UserCenter *user3 = [UserCenter alloc];//为nil
       //模拟初始化数据
        [[UserCenter sharedUserCenter] setUserName:@"weipan"];
        //模拟其他界面取值
        NSLog(@"%@", [[UserCenter sharedUserCenter]userName]);
##KVO键值
 //注册消息
    
    [_dog addObserver:self forKeyPath:@"dogName" options:NSKeyValueObservingOptionOld /*||加其他的*/ context:nil];
    //第一个参数：哪个对象去监听
    //第二个参数：监听的某一个具体的属性
    //第三个参数：什么情况下接收消息
    //第四个参数：上下文，暂且直接为nil
    
##数据持久化
保持 读取 移除<br>
     
     [userDefault setObject:@"天下第一！" forKey:@"hello"];
        NSLog(@"%@", [userDefault valueForKey:@"hello"]);
        [userDefault removeObjectForKey:@"hello"];
        
        
##广播(通知)
先设置监听再广播

	- (void)post:(id)obj {
	//创建一个广播对象
	NSNotificationCenter *nc = [NSNotificationCenter defaultCenter];
	//发送广播
	//第一个参数：广播名字 第二个参数：内容
	//    [nc postNotificationName:@"吃饭" object:@"大家都去吃饭吧"];
	    [nc postNotificationName:@"吃饭" object:obj];
	}
	- (void)callFuc:(NSNotification *)n {
	    NSLog(@"%@", n.object);
	}
	- (void)listener {
	    //注册监听
	    //第一个参数：把监听回调注册在那个对象里
	    //得二个参数：监听回调
	    //第三个参数广播名字
	    //第四个参数直接为nil即可
	    NSNotificationCenter *nc = [NSNotificationCenter defaultCenter];
	    [nc addObserver:self selector:@selector(callFuc:) name:@"吃饭" object:nil];
	}
#类目 延展 协议
***
测试是否有效：<br>
   
    if (![leader respondsToSelector:@selector(setAge:)]
            ) {
            NSLog(@"方法没有实现");
        } else
            NSLog(@"方法实现了");
测试是否遵守协议
   
    判断是否遵守协议
        if (![worker conformsToProtocol:@protocol(Working)]) {
           NSLog(@"没有遵守协议");
        }
        else {
           if (![worker respondsToSelector:@selector(test)]) {
                NSLog(@"没有实现协议");
            }else {
                [worker test];
                worker.money = 123;
                NSLog(@"%ld", worker.money);
            }
##类目
***
添加 new file--->object c file<br>
@interface Leader (Age)<br>
已知类名 （类目名）<br>
不能给系统提供的类添加属性！<br>
自定义类添加属性：<br>
1）在已知类添加成员变量；<br>
2）在类目.m加入@dynamic 成员变量;重写setter和getter方法
	
	@dynamic age;
	- (void)setAge:(NSInteger)age {
	    _age = age;
	}
类目作用：
1.可以为已知类添加方法<br>
2.通过类目添加的方法会成为原始类的一部分调用与其他方法相同<br>
3.通过类目添加的方法与原始类同级<br>
4.继承子类添加的类目方法父类无法拥有反之可以<br>
5.把类方法归类更好管理<br>
##延展
//定义延展方法
直接在类的.m文件中定义延展
		
		@interface Leader()//延展的书写格式
		{
    NSInteger m_count;
    //需要在全局访问的但又不需要setter和getter,也不需要公开的
      }
		- (NSString *)returnStringByScores;
		@end
		@implementation Leader
		-(NSString *)returnStringByScores {
		    NSString *restult;
		    if (_scores >= 90) {
		        restult = @"优";
		    } else {
		        restult = @"差";
		    }
		    return restult;
		}
		- (void)printGrade {
		    NSLog(@"成绩等级:%@", [self returnStringByScores]);
		}
		@end
		
##协议
###正式协议
new file --->header生成只有.h文件的协议<br>
语法:@protocol 协议名称 <父类协议 都是NSObject><br>
协议就是把一系列方法和属性声明在一个头文件里面<br>
     
    #import "Foundation/Foundation.h"
	@protocol Working <NSObject>
	//协议就是把一系列方法和属性声明在一个头文件里面
	@required//遵守协议后必须实现的方法和属性 默认值@required
	- (void)test;
	@optional //可选择执行的协议方法和属性
	@property (nonatomic, assign)NSInteger money;
	@end
在协议执行类里包含该文件并加入@interface 类名 : NSObject<协议名>属性的setter和getter需重写。并写协议写明的方法<br>
		
	#import <Foundation/Foundation.h>
	#import "Working.h"
	@interface Worker : NSObject<Working>
	{
	    NSInteger _money;
	}
@end	
##代理
使用代理(委托)的步骤:<br>
1.定义一份协议<br>
2.代理人遵守协议（实现协议的方法）<br>
3.委托人声明一个代理人并且找到代理人 （委托人.h）<br>
@property (nonatomic, strong)id<Working> delegate;   
    
    #import <Foundation/Foundation.h>
	#import "Working.h"
	@interface Boss : NSObject
	//声明一个代理
	@property (nonatomic, strong)id<Working> delegate;
	- (void)doPlay:(NSInteger)time;
	@end
4.代理人去做委托人的事情（委托人.m）
   
    #import "Boss.h"
	@implementation Boss
	- (void)doPlay:(NSInteger)time {
	    //有没有代理人并且代理人有没有实现方法
	    if (_delegate && [_delegate respondsToSelector:@selector(play:)]) {
	        //叫代理去做想做的事情
	        [_delegate play:time];
	    }
	    
	}
	@end
