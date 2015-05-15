#SSH框架下的web各层单例、多例分析
###<action层多例、service层单例、dao层单例>
>1. 什么是单例多例
>>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;单例:所有的请求都用一个对象来处理，比如我们常用的service和dao层的对象通常都是单例的<br>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;多例:则指每个请求用一个新的对象来处理，比如action
>
>2. 怎样产生单例、多例
>>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;spring中的所有的bean默认都是单例，所以service、dao层的bean无需设置属性。相反因为action是多例，需要设置prototype,如
   `<bean id="person"  class="com.zcq.model.Person"  scope="prototype"></bean>`
>
>3.为什么要用单例、多例
>>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;单例，是因为没必要每个请求都新建一个对象，这样子既浪费CPU又浪费内存<br>
>>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;多例，是为了线程安全；即一个请求改变了对象的状态，此时对象又处理另一个请求，而之前请求对对象状态的改变导致了对象对另一个请求做了错误的处理
>
>4为什么action层多例、service层单例、dao层单例
>> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在实际问题中，使用一些变量组合的对象来接受前台传给后台的参数，如果仍使用单例，会导致当你第二次用这些变量接受参数的时候可能还是上一次的值.故而用prototype<原型模式 每次action请求过来都会创建一个实例><br>
>> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;service、dao层单例是因为：这两层具有复用性 避免重复new产生浪费资源（service dao并不是一定要单例）
>
