# Annotation

一种 JAVA 语言的辅助描述语言，能够给 JAVA 中的一些元素（如：类、成员变量、方法等）添加一些辅助元信息。
这些信息原本不会对 JAVA 程序的运行产生影响。但在现在流行的框架，甚至 JVM 本身都会有自己的一套 Annotation
解析系统，这些解析系统会通过解析代码中的 Annotation 获取一些信息，然后根据这些信息来改变程序运行的方式。

## 元注解

元注解是 JAVA 语言本身定义好的，使开发者可以开发自定义注解的一些注解。元注解 在 `java.lang.annotation` 
包内，目前有如下几种：

* @Retention
* @Documented
* @Target
* @Inherited
* @Native
* @Repeatable

### @Retention

这个注解是用来描述你定义的注解的生命周期的。其参数是一个 `RetentionPolicy` 枚举对象。
他有下面几个值：

* SOURCE - 源文件中有效
* CLASS - class 文件中有效
* RUNTIME - 程序运行时有效

可以看出来，如果想让你定义的 Annotation 能够影响程序的运行，就必须将其生命周期定义为最长的 **RUNTIME**，
这样在程序运行时你的解析器才能通过反射读取该注解和其信息。

### @Documented

这个注解简单理解就是可以让被标记注解在使用类似 javadoc 这样的生成 API 文档的工具生成文档时同时生成该被标记注解的文档。

### @Target

这个注解可以定义你所编写的注解可以被应用的对象。其参数是一个 'ElementType' 枚举对象的数组。
该对象的值用来描述 JAVA 中可应用注解的元素。详细可以查看该类源码或 JAVA API。

### @Inherited

如果你自定义的注解被 `@Inherited` 标记，则使用你注解的类的子类也会自动带有你自定义的注解。这个功能只有类有效。

### @Native

这个注解说明被标记的成员变量是一个来源于本地编码的变量，即非 JAVA 的变量。这个一般用不到。JAVA 源码中有许多。有空可以研究下。

### @Repeatable

被该注解标记的注解可以在同一个地方重复出现，即可以写多个同样的注解。

## 注解组合

用多个注解标记同一个自定义注解，则该自定义注解会带有标记他的所以注解的功能。具体看 Demo。
