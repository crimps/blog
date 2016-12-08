调用不同数据库的存储过程的主要区别在于查询语句的写法以及获取返回值的方式不同，
其他的方面都是一样的。

## 调用Oracle存储过程

### 1. 查询语句的写法

    String procStr = "CALL procNameSpace.procName(?,?,?)"
call 必须要大写，至于为什么小写无法成功调用存储过程实在是找不出原因。
参数部分，有多少个[入参、出参、结果集]就写几个"?",在参数这个部分Mssql会存在一些差异。
### 2. 参数赋值及调用

    Connection connection = getConnection();
    CallableStatement statement = connection.prepareCall(procStr);
    statement.setString(1, parameter)
    statement.registerOutParamenter(2, OracleType.NUMBER);
    statement.registerOUtParamenter(3, OracleType.CURSOR);
    statement.execute();
    int number = statement.getObjece(2);
    Result result = statement.getObject(3);
入参赋值部分没有什么好说的，关键在于出参及结果集。
出参及结果集都是调用registerOutParamenter()方法，不同之处在于：
出参的类型为具体对应的类型，结果集的类型为CURSOR。

## 调用Mssql存储过程

### 1. 查询语句的写法

    String procStr = "{CALL [procNameSpace.procName](?,?)}";
Mssql查询语句要在最外部加上大括号，在存储过程名称部分还要加上方括号
Mssql参数部分，有多少个[入参、出参]就写几个"?",与Oracle不同的是结果集不需要在参数部分体现。

### 2. 参数赋值及调用

入参部分与Oracle一致，没有区别。  
出参及结果集部分，Mssql比较特殊，出参与结果集的获取方式不同。  
出参:

	statement = registerOutParameter(2, Types.INTEGER);
	statement.execute();
	int number = statement.getObject(2);
结果集：

    Result result = statement.executeQuery();
Mssql出参的调用方式与Oracle基本上一致，只是参数的类型不同。结果集无需定义参数，直接获取就行了。
出参与结果集不同的获取方法与Mssql存储过程是保存一致的。

## 调用EDB存储过程

EDB数据库是progress的商用版本，使用上基本上与Oracle差不多。

### 1. 查询语句的写法

EDB查询语句要在最外部加上大括号

    String procStr = "{CALL procNameSpace.procName(?,?)}";

### 2. 参数赋值及调用

参数部分与Oracle一样，唯一的区别在于参数的类型。  
EDB出参类型为Types.对应的类型，结果集的类型为Types.OTHER



