子菜单无法输入中文

Qt::WA_DeleteOnClose，栈上对象不能设置，否则析构两次，崩溃。另外，堆对象自动delete后，指针不会为NULL。
中文支持：QString::fromLocal8Bit("很久很久"),QStringLiteral

android添加动态库
ANDROID_EXTRA_LIBS

布局
样式表
qobject_cast 判断类类型

采用定时器（<10ms）调用update占用cpu相当严重；(>20ms)情况下，正常。
reinterpret_cast,使用多重继承时，获取数据会出错，不要使用
myPen.setJoinStyle(Qt::MiterJoin);如果使用，笔的宽度较大的情况下，无法获取实际的边框。已经解决

c++,拷贝构造函数和赋值函数是默认的，需要设置为private，避免问题。

以下两段代码功能相同，注意是m2*m1，而不是m1*m2
	QTransform m;

	m.translate(100, 100);

	m.rotate(45);

        QTransform m;
	QTransform m1;

	m1.translate(100, 100);

	QTransform m2;

	m2.rotate(45);

	m = m2 * m1;

//支持c++11，可以支持Enum::enumValue之类的语法
QMAKE_CXXFLAGS += -std=gnu++0x

QString和char* 转换。记住不要使用toLatin1，中文会乱码
	char* ch1 = "地方";

	QString s1 = QString::fromLocal8Bit(ch1);

	QByteArray ba1 = s1.toLocal8Bit();

	char* ch2 = ba1.data();

	QString s2 = QString::fromLocal8Bit(ch2);


QMAKE_CXXFLAGS += -std=c++11，支持c++11,可以支持语法
Enum::enumValue
.h中，
private:
int value = 123;

linux中的QList<int>读取耗时，for循环.win7大致相近
at                    7711
[]                    14114
java迭代器        22247
stl迭代器            16372
c++11的for        5417
除at不可写外，写入也大致是这点时间

qt窗体被其他窗体遮挡时，paintEvent事件依然会被触发。只有visible设为false时，才不会触发。

ldd 查看动态库依赖关系

需要载入所有的动态库，比如动态库A，B，C，A调用B，B调用C。则A必须还要调用C才能正常编译。

测试了json存储，10W个控件，每个控件3个属性，linux下，存储时间3s左右，读取0.5s左右。
windows下，存储6s，读取18s。
xml存储，同样情况，linux下，存储2s，读取2s。
windows下，存储6s，读取18s。
以上情况均为debug，release下有20%左右提高。
linux为虚拟机，也就是说实际差别更大。

测试QMap，QList， 调用函数的读取效率
137:8:1

xml读取，有空值时，会报错，要额外处理。
QLineEdit，配上正则表达式，根本没有实用价值。
QDir，碰上首字母为空格的文件，无法获取。
QIcon，在linux下，动态库和上层动态库不能使用同名的资源文件，否则会出现资源读取不到的问题。
