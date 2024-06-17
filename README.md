## 一，React环境搭建

### 1，脚手架

现在开发项目，都是组件化，工程化的。我们可以基于webpack自己去搭建一套工程化的架子，样这非常麻烦，复杂。React官方为我们提供了一个脚手架，叫create-react-app。默认情况下，就把webpack相关的配置就处理好了。只需要基于这个脚手架，去开发项目就OK。



安装脚手架：

```
npm i create-react-app -g 
```

![1691025360300](assets/1691025360300.png)



验证是否安装成功：

![1691025433939](assets/1691025433939.png)



安装后完，就可以创建一个项目：

```
create-react-app demo
```

![1691025506308](assets/1691025506308.png)



安装完后，进入项目，启动项目，如下：

![1691025809901](assets/1691025809901.png)



**React版本：**

- 很早之前，是15版本，不用了。
- 16版本，项目用的还是比较多的。
- 17版本，语法和16相比，没有什么变化，只是在底层处理机制上，有所升级。
- 18版本，当前最新版本，不管是语法还是底层机制，都有变化。



**React项目，默认会安装**

- react，是React框架的核心，默认安装的是最新版本，学的话，就学习最新版本。
- react-dom，React视图渲染的核心。基于React构建WebApp。
- react-native，构建渲染原生App的。



### 2，项目的目录结构



使用vscode打开项目，如下：



![1691025932582](assets/1691025932582.png)



打开package.json文件，如下：

![1691026126321](assets/1691026126321.png)

![1691026183005](assets/1691026183005.png)

![1691026310090](assets/1691026310090.png)

![1691026491165](assets/1691026491165.png)



去简化一下代码，如下：

![1691026645232](assets/1691026645232.png)

![1691026653770](assets/1691026653770.png)



目录结构：

```
demo 
  |- node_modules   项目的依赖
  |- src   我们写的代码基本上都是放在src下面。webpack打包时，只对src目录进行打包
      |- index.js  项目的入口
  |- public  入页面的模板
      |- index.html 
  |- package.json
  |- ....
```



运行项目，如下：

![1691026858742](assets/1691026858742.png)



浏览器查看效果如下：

![1691026941478](assets/1691026941478.png)





### 3，React简单介绍

目前市面上流行的前端框架：

- Vue
- React
- Angular(NG)
- ...  



主流思想：不去直接操作DOM，而“数据驱动视图”。



**直接操作DOM**

- 直接操作DOM，会导致性能消耗大一点，可能会导致DOM的重排和重绘。
- 操作DOM，相对来说，会麻烦一点



**数据驱动视图**

- 不会直接操作DOM
- 操作数据，数据变了，框架会按相关的流程，让页面重新渲染
  - vue:  数据都是响应式的
  - 小程序：setData({})
  - react: setState()
- 框架底层会实现视图的渲染，也是基于DOM的
  - 构建了一套  虚拟DOM -> 真实DOM 渲染体系
  - 这样会尽可能减少重排和重绘
- 开发效率更高，性能也会好很多。



看如下的代码：

![1691027783351](assets/1691027783351.png)



## 二，JSX语法



### 1，什么是JSX

jsx是用来给组件提供视图的，类似于vue中的模板。



就是js和html标签混合在一起，并不是我们之前玩的字符串拼接。这种语法也会通过babel进编译，编译成js代码。对默认生成的代码解释：

![1691029469055](assets/1691029469055.png)



### 2，细节1

在jsx中，可以通过{}胡子语法，嵌入表达式。任何有值的内容都是表达式。代码如下：

![1691029649900](assets/1691029649900.png)



在ReactDOM.createRoot时，不能直接把HTML或BODY作为根容器，必须指定一个额外的盒子，如下：

![1691029793721](assets/1691029793721.png)



它会在控制台报一个错误，如下：

![1691029834759](assets/1691029834759.png)

也就是说，不能把html或body当成根容器。



### 3，细节2

在构建视图时，必须要有一个唯一的根节点，如果没有，就报错，如下：

![1691029994196](assets/1691029994196.png)



我们要么使用一个div包起来，这样就会多一个div嵌套，如下：

![1691030049118](assets/1691030049118.png)



也可以使用React中帮我们提供的组件，包起来，如下：

![1691030130827](assets/1691030130827.png)



使用简写，如下：

![1691030167382](assets/1691030167382.png)



React给我们提供的一个特殊的组件，叫Reat.Fragment，是一个空标签。作用：

- 保证了视图只有一个根标签
- 也不新增一个HTML层级结构



### 4，细节3

在{}胡子语法中，可以嵌入不同的值，如下：

- number / string   值是啥，就渲染出来什么
- boolean / null / und / Symbol / BigInt 渲染出来的内容是空
- 渲染对象，直接报错了，但是有特殊情况
  - jsx元素（本质也是一个对象，这个对象就不会报错）
  - 给标签设置style行内样式时，也必须写成对象
- 渲染数组，会把数组中的每一项分别拿出来渲染，并不是变为字符串渲染，中间没有逗号
  - 数组中是number、 string，也是直接渲染
  - 数组中是boolean / null / und / Symbol / BigInt，渲染出来的内容是空
  - 数组中放jsx元素也是会被渲染的
- 渲染函数，不支持在{}中渲染函数的，但是函数也可以是组件，要渲染组件通过<Tabbar></Tabbar>标签的形式渲染。
- .... 





参考代码如下：

![1691030587548](assets/1691030587548.png)

![1691030615977](assets/1691030615977.png)

![1691030719652](assets/1691030719652.png)

![1691030824059](assets/1691030824059.png)

![1691030942808](assets/1691030942808.png)

![1691030982583](assets/1691030982583.png)



### 5，细节4

给标签设置行内样式，如下：

![1691031222052](assets/1691031222052.png)



有一个数据，如果是true，就显示button按钮，否则就隐藏buton按钮，代码如下：

![1691031344557](assets/1691031344557.png)



进一步，控制一个元素是否创建，如下：

![1691031457232](assets/1691031457232.png)



再进一步，通过一个数据，控制button中的文本，如下：

![1691031564119](assets/1691031564119.png)



从服务器调用接口，获取到一片数据，渲染数据，如下：

![1691031969373](assets/1691031969373.png)



你循环创建的元素一定要设置key，表示唯一值，用于优化DOM-DIFF的。



我要循环出5个button按钮，如下：

![1691032282055](assets/1691032282055.png)



### 6，细节5

粥盘点jsx细节，盘点一下jsx的底层渲染机制，看如下代码：

![1691043473313](assets/1691043473313.png)



关于jsx的底层渲染机制：

- 第一步：把你编写的jsx语法，编译成虚拟DOM（VirtualDOM），虚拟DOM就是框架内部构建的一套对象体系，虚拟DOM本质就是一个对象，对象是属性的无序集合，这个对象中的属性都是React官方规定的，这个属性用于描述虚拟DOM。
- 第二步：把构建出来的虚拟DOM，渲染成为真实DOM，在浏览器中才能看到这些DOM元素。

- 补充：第一次渲染页面是直接把虚拟DOM转化成真实DOM。后期可能去更新状态，还会产生一个新的虚拟DOM。新旧的虚拟DOM会进行DOM-DIFF的对比，计算出差异，打PATC（两次虚拟DOM的差异），只去更新差异。



画图分析：

![1691044344238](assets/1691044344238.png)



打开babel官网，把jsx代码让babel进行编译，如下：

![1691044725452](assets/1691044725452.png)



把编译后的代码copy出来，如下：

![1691044942009](assets/1691044942009.png)



这个createElement函数调用完后，得到一个虚拟DOM，打印出来，如下：

![1691045043550](assets/1691045043550.png)

![1691045104573](assets/1691045104573.png)



关于jsx底层渲染机制：

- 我们编译的是jsx语法，编译成虚拟DOM对象

  - 基于babel把jsx编译成React.createElement这种格式。只要是一个元素节点，都会经过createElement处理。有三个参数：
    - ele: 元素或标签名，也可以是组件。
    - props：元素的属性，如果没有设置属性就是null
    - children:  第三个是当前元素的子节点

- 再React.createElement方法执行，创建出虚拟DOM对象。虚拟DOM有的地方也叫jsx元素，可jsx对象，或者ReactChild对象....

  ```js
  virtualDom = {
      $$typeof:Symbol(react.element),
      ref:null,
      key:null,
      type:标签名或组件名,
      props: { 存储元素相关的属性，
      	children: 子节点信息，如果没有子节点，则没有这个属性，属性值可能是一个值，也可能是数组     
      }	
  }
  ```

  

- 初次渲染时，会把虚拟DOM再次转化成真实DOM。在浏览器中就会看到渲染出来的效果。



也就是说我们在写jsx时，是可以直接写React.createElement的，如下：

![1691046750637](assets/1691046750637.png)



## 三，函数式组件（静态组件）

### 1，函数式组件介绍

在React中，组件分两类：

- 函数式组件，也叫静态组件
- 类组件，也叫动态组件



今天先讲函数式组件，下周再开始讲类组件。写一个组件，如下：

![1691047046603](assets/1691047046603.png)



然后，在index.js中就可以使用组件了，如下 ：

![1691047167292](assets/1691047167292.png)



组件名字，必须使用大写字母打头，否则就会报错，一般情况下，我们采用大驼峰命名法。在调用组件时，可以给组件传递各种各样的属性，如下：

![1691047422147](assets/1691047422147.png)



使用babel编译上面的jsx，如下：

![1691047551966](assets/1691047551966.png)



### 2，函数式组件的渲染机制



函数式组件是如何被渲染出来的，代码如下：

![1691047686491](assets/1691047686491.png)

流程如下：

- 第一步：基于babel，把上面的代码编译成React.createElement形式。如下：

  ![1691047753367](assets/1691047753367.png)

- 第二步： createElement方法执行，创建出一个虚拟DOM。type是一个函数。

  ![1691047972265](assets/1691047972265.png)

- 第三步： 基于root.render把虚拟DOM转化成真实DOM。
  
  - type的值不再是一个字符串，而是一个函数
    - 把One函数执行，One()执行
    - 在执行时，会把One组件上写的属性，传递给One函数
    - One函数就会通过Props接收
    - 函数要接收，通过props接收。函数返回jsx元素（就是虚拟DOM）
    - 最后基于render把组件返回的虚拟DOM变为真实DOM，插入到#root容器中。
  
  ![1691048245758](assets/1691048245758.png)
  
  ![1691048262224](assets/1691048262224.png)





再去总结一下，在调用组件，我们可以给组件设置（传递）各种各样的属性。如果传递的不是字符串，需要使用{}包起来，在组件内部就可以通过props来接收传递过来的数据了。



在使用组件时，也可以在组件标签之间写东西，写的内容也是传递给了props，如下：

![1691048686160](assets/1691048686160.png)

![1691048790660](assets/1691048790660.png)





### 3，冻结，密封，扩展

默认情况下，一个对象是可以修改属性，添加属性，删除属性的，如下：

![1691050378089](assets/1691050378089.png)



如果把对象给冻结了，如下：

![1691050613699](assets/1691050613699.png)

**总结冻结**

- Object.freeze(obj)
- 检测是否被冻结：Object.isFrozen(obj)
- 特点：不能修改成员的值，不能新增成员的值，不能删除成本的，不能劫持。



前面我们说的props，默认就是被冻结的，也就意味着不能修改props的值，如下：

![1691050806519](assets/1691050806519.png)



还有一个概念，叫密封，代码如下：

![1691050900349](assets/1691050900349.png)

**总结密封**

- Object.seal(obj)
- 检测是否被冻结：Object.isSealed(obj)
- 特点：能修改成员的值，不能新增成员的值，不能删除成本的，不能劫持。



还有一个概念，叫扩展，代码如下：

![1691051099555](assets/1691051099555.png)

**总结扩展**

- Object.preventExtensions(obj)
- 检测是否被拓展：Object.isExtensible(obj)
- 特点：除了不能新增，其它都可以。


如果对象被冻结了，也是不可以扩展的，也是密封的。如下：

![1691051294550](assets/1691051294550.png)





### 4，props的一些细节

在父组件中（index.js）调用了子组件（One.jsx），可以基于属性，把不同的数据传递给子组件，子组件通过props接收，接收后，就可以在jsx中使用了，目的是为了提高组件的复用性。代码如下：

![1691051521064](assets/1691051521064.png)

![1691051561108](assets/1691051561108.png)



props默认是被冻结的，但是我们是可以做一些校验的，安装一个包，如下：

![1691051663456](assets/1691051663456.png)



然后就可以校验，就可以指定默认值了，如下：

![1691051790934](assets/1691051790934.png)

![1691051800453](assets/1691051800453.png)



也可以做一些校验工作，如下：

![1691051901469](assets/1691051901469.png)



![1691051930788](assets/1691051930788.png)

![1691051966832](assets/1691051966832.png)



都能校验哪些规则，如下：

![1691052024672](assets/1691052024672.png)



![1691052072582](assets/1691052072582.png)



不管是校验成功，还是校验失败，都把把数据给props，如果校验失败了，会在控制台中发出警告。



### 5，插槽机制

在调用组件时，可以在标签之间写内容，如下:

![1691111684743](assets/1691111684743.png)



在组件中打印出props，如下：

![1691111735464](assets/1691111735464.png)



浏览器中测试之如下：

![1691111826901](assets/1691111826901.png)

使用children，如下：

![1691111927734](assets/1691111927734.png)



上面的案例，就相当于一个插槽，插槽可以让组件有更强的复用性。体现：

- 通过属性把数据传递给组件
- 通过标签之间写html结构（jsx对象）传递结构给组件

如下：

![1691112166500](assets/1691112166500.png)



看如下 代码：

![1691112323027](assets/1691112323027.png)



浏览器中的效果如下：

![1691112339456](assets/1691112339456.png)



如果就传递一个span，如下：

![1691112532483](assets/1691112532483.png)



可以这样解决，如下：

![1691112787709](assets/1691112787709.png)



上面的是我们手动的处理children，其实在React中，有一个React.Children.toArray，就可以自动把children变成数据，如下：

![1691112902971](assets/1691112902971.png)



之前在vue中，还有一个具名插槽，在React如何实现具名插槽，如下：

![1691113012769](assets/1691113012769.png)



此时就不能使用下标来插入了，如下：

![1691113089514](assets/1691113089514.png)



解决之，如下：

![1691113372587](assets/1691113372587.png)



尝试把前面讲的内容封装成一个组件，叫Dialog，分析如下：

![1691113544616](assets/1691113544616.png)



先使用Dialog，如下：

![1691113685289](assets/1691113685289.png)



开始封装Dialog，如下：

![1691113999359](assets/1691113999359.png)



尝试写一点样式，如下：

![1691115565161](assets/1691115565161.png)



总结函数式组件：

- 函数式组件也叫静态组件
- props是用来接收数据和结构，并且props默认是被冻结
- props可以进行校验，也可以设置默认值
- 函数式组件返回jsx元素，进行渲染
- 函数式组件中没有状态，无状态的组件
- 除非在父组件中，重新调用这个函数式组件，才会重新渲染此组件
- 项目中，有这样需求：第一次渲染后就不会再有变化了，就可以使用函数式组件



## 四，类组件（动态组件）



### 1，初识类组件

可以基于类来构建动态组件。创建一个类，要求必须继承React.Component/PureComponent这个类。现在就创建一个组件，如下：

![1691116237775](assets/1691116237775.png)



在类组件中是可以定义状态，如下：

![1691116519246](assets/1691116519246.png)



### 2，类组件的渲染逻辑



调用组件时，代码如下：

![1691116806455](assets/1691116806455.png)



也就是转化成虚拟DOM时，那个type属性的值是类（class One），type的取值：

- 字符串： 创建一个普通html标签
- 普通函数： 函数式组件，执行函数，并且把props传递给函数
- 类：React底层会帮我们去new，new的时候，就会创建出一个实例（组件实例），并且也会解析出属性传递给组件的props。
  - 每调用一次类组件都会创建一个单独的实例（组件实例），并且组件中的this就表示这个实例。
  - 把类组件中的render方法执行，返回jsx对象（虚拟DOM），当做组件的视图进行渲染。





在调用类组件时，类组件内部做的第一件事情：

- 初始化属性，有了属性，就可以进行规则校验。默认这个props属性是通过constructor接收，如下：

  ![1691117269144](assets/1691117269144.png)

- 如果没有写constructor属性，React内部也会把props挂载到当前组件实例上（this）

  ![1691117365611](assets/1691117365611.png)

- 这个props也是被冻结的，只能使用，不能修改，添加，劫持。可以对属性进行校验，设置默认值

  ![1691117657705](assets/1691117657705.png)





在调用类组件时，类组件内部做的第二件事情：

- 初始化状态，如果后期修改了状态，会重新render，叫re-render。

  ![1691117918699](assets/1691117918699.png)

- 修改状态，更新视图，React提供了专属的API，叫setState，不光可以修改状态，还可以更新视图。

  ![1691119099075](assets/1691119099075.png)

- 也可以使用this.forceUpdate强制更新（不推荐）

  ![1691119217620](assets/1691119217620.png)

  ![1691119240075](assets/1691119240075.png)



### 3，生命周期（重要）

上午我们讲了两个生命周期函数，一个是constructor，一个是render。如下：

![1691129980002](assets/1691129980002.png)



然后还会触发一个钩子函数，叫componentWillMount，在组件第一次渲染之前触发。此勾子函数目前是不安全的，但是是可以使用的。只是在控制台中会有黄色的警告。为了不让它警告，可以使用UNSAFE_componentWillMount，代码如下：

![1691130230235](assets/1691130230235.png)

![1691130262087](assets/1691130262087.png)



然后学会触发一个钩子函数，叫componentDidMount，代码如下：

![1691130428603](assets/1691130428603.png)



看如何的流程图：

![1691130447552](assets/1691130447552.png)



组件的更新逻辑，当修改了状态，组件会更新，就会调用shouldComponentUpdate这个勾子函数，测试如下：

![1691130850887](assets/1691130850887.png)



上面的界面中支持人数还是10，说明没有更新，就让它返回true，如下：

![1691130942526](assets/1691130942526.png)



上面我们允许更新了，就会触发componentWillUpdate这个钩子函数，也是不安全的，在这个钩子中，状态还没有被修改，代码如下：

![1691131194751](assets/1691131194751.png)



然后修改状态的值，修改完后，调用再次render函数，进行组件更新，流程：

- 按最新的状态/属性，把返回的jsx编译成新的虚拟DOM
- 和上一次渲染出来的旧的虚拟DOM进行对比，所谓的DIFF算法
- 找到差异，把差异进行渲染，渲染成真实DOM

![1691131453237](assets/1691131453237.png)



然后还会调用compoentDidUpdate，表示组件更新完毕。如下：

![1691131546952](assets/1691131546952.png)



当我们在shouldComponentUpdate中，返回了false，下的钩子函数就会再执行了，如下：

![1691131719126](assets/1691131719126.png)



测试点击反对，看一下强制更新时，showCompoentUpdate中返回false有没有影响，如下：

![1691131779744](assets/1691131779744.png)



如果我们基于this.forceUpdate强制更新视图，会跳过shouldComponentUpdate函数的校验，直接从WillUpdate开始进行更新，说白了，视图一定会触发更新。



前面我们说了，当我们调用this.setState 或 this.forceUpdate时，会进入组件的更新逻辑。除了这种情况下之外，还有一种情况，也可以让组件进行更新逻辑。当组件的props发生变化了，也会进入更新逻辑，代码如下：

![1691133180026](assets/1691133180026.png)



还有一个钩子函数，当属性发生变化了，就会调用，如下：

![1691133450168](assets/1691133450168.png)



总结：通过哪些方式，可以让组件进入更新逻辑

- this.setState  改变状态
- this.forceUpdate  强制更新
- 调用组件时的属性发生变化了，在componentWillReceiveProps中可以接收最新的属性





如果有组件的嵌套，嵌套会形成父子组件，如果有父子组件了，在处理机制上遵循深度调优先的原则，也就是渲染父组件时，遇到了子组件，一定要先把子组件处理完，然后再处理父组件，它们的生命周期执行流程如下：

- 父组件第一次渲染
  - 父willMount => 父render【子willMount=>子render=>子didMount】=>父didMount
- 父组件更新
  - 父shouldUpdate =>父willUpdate=>父render【子willReceivProps=>子shouldUpdate=>子willUpdate=>子的render=>子didUpdate】=>父didUpdate
- 父组件销毁
  - 父willUnmount => 处理中【子willUnmount=>子销毁】=>父销毁



生命周期的图，如下：

![1691134054900](assets/1691134054900.png)



总结一下：

- 类组件是动态组件，体现在它里面是有状态的，是有生命周期的。
- 组件第一次渲染完毕后，除了父组件更新可以触发子更新外，我们还可以通过this.setState修改状态，或this.forceUpdate等方式让组件“自更新”
- 类组件具备：属性，状态，生命周期函数，ref... 总结类组件功能很强大，由于它里面东西比较多，导致类组件性能差一点。



### 4，PureComponent

在React中创建一个类组件，要么继承React.Component，要么继承React.PureComponent。在讲继承PureComponent之前，先说一下浅比较，如下：

```js
let obj = {a:110}  // obj指向了{a:110}这个堆   obj是一个地址：0x123

let objA = {x:1,y:obj,arr:[1,2,3]}
let objB = {x:1,y:obj,arr:[1,2,3]}

浅比较objA和objB,只会比较第一层：
     objA          objB
      x             x             一样
      y:0x123       y:0x123       一样
      arr:0x456     arr:0x789     不一样
      
如果objA和objB中的成员个数都不一样，两个对象肯定是不一致的。
```



写一个小案例，通过案例说一下React.PureComponent。如下：

![1691371490553](assets/1691371490553.png)



PureComponent和Component的区别：

- PureComponent 会给类组件添加一个shouldComponentUpdate生命周期函数
- 在这个生命周期函数中，它对新老属性/状态会做一个浅比较
- 如果经过浅比较，发现属性或状态并没有改变，则返回false，也就意味着不更新组件了。



遇到到种情况，如何解决，如下：

![1691371914629](assets/1691371914629.png)



### 5，调试工具

需要在谷歌商店，搜索React，安装调试工具。和vue一样，要开发vue或react，调试工具非常重要。

![1691372000766](assets/1691372000766.png)



### 6，ref

#### 6.1 REF获取DOM



使用传统方式，获取Dom，如下：

![1691372191147](assets/1691372191147.png)



上面的获取DOM的方式，是不推荐，推荐使用ref形式来获取DOM，如下：

![1691372288036](assets/1691372288036.png)



可以编译一下，上面的jsx，如下：

![1691372373055](assets/1691372373055.png)



也就说，通过ref是可以获取DOM元素的，给需要获取的元素设置ref="xxx"，后期可以基于this.refs.xxx去获取相应的DOM元素，这种写法比较老了，不推荐使用。在ref后面也可以跟上一个函数，如下：

![1691372595529](assets/1691372595529.png)



总结一下，第二种写法，ref后面跟一个函数，x是函数的形参，存储的就是DOM元素，把x挂载到当前组件的某个属性的。当编译jsx时，它内部肯定要把函数执行，函数执行时，就会把DOM元素传递给x形参。还有一个写法，是利用creaetRef先创建一个ref，如下：

![1691372834244](assets/1691372834244.png)



第三种写法，是基于React.createRef方法创建一个REF对象，通过ref={ref对象}。就可以通过ref对象.current就可以得到对应的DOM元素了。



#### 6.2 REF获取组件实例



准备两个子组件，如下：

![1691374385886](assets/1691374385886.png)



把ref写在标签上，目的是为了获取DOM元素。把ref写在类组件上，目的就是为了获取当前组件实例。有了实例就可以得到组件的状态，就可以设置组件上的方法。如下：

![1691374439361](assets/1691374439361.png)



尝试把ref写在函数式组件上，如下：

![1691374577465](assets/1691374577465.png)



通过ref转发，就可以获取函数式组件内部的DOM元素，如下：

![1691374724395](assets/1691374724395.png)





现在就有一个问题了，能不能获取类组件中的DOM元素呢？如下：

![1691374976408](assets/1691374976408.png)





## 五，深入setState



### 1，setState的语法

语法如下：

```txt
this.setState([部分状态]，[callback])   // 作用：1）修改状态  2）更新视图
[部分状态]: setState支持修改部分状态的
	this.setState({
	   x:100      // 不管有多少个状态，只去修改x这个状态，其它的状态是不动的
	})
[callback]： 在状态修改后，视图更新后，会自动触发。发生在componentDidUpdate钩子之后
```



代码如下：

![1691375608391](assets/1691375608391.png)



thisState中的第2个回调函数，就类似于vue中的$nextTick。如果我们在shouldComponentUpdate中阻止了视图更新，那个这个callback也是回执行，如下：

![1691375769946](assets/1691375769946.png)



### 2，同步或异步

假定setState是同步的，看如下的代码：

![1691377260937](assets/1691377260937.png)



再看如下的代码：

![1691377749919](assets/1691377749919.png)



如果把setState放到的定时器中，如下：

![1691377902315](assets/1691377902315.png)



总结：

- 在React18中，setState操作都是异步的，不管是在哪里执行，如：合成事件，生命周期函数，定时器...
- 异步的目的：实现状态的批处理，统一处理。
- 有效地减少了更新次数，降低了性能消耗。
- 利用了更新队列机制，遇到了setState会立即放到更新队列中。此时状态和视图也没有更新。
- 当所有的代码都操作完毕，会去刷新队列，说白了就是通知队列中的所有的任务执行，把所有的setState合并起来执行，只会触发一次视图更新，这就是批处理。





在React16版本：

- 在合成事件（在jsx中基于onXxxx绑定的事件）中，在生命周期函数中，setState操作是异步的。
- 但是如果setState出现在其它的异步代码中，如：定时器，手动获取DOM做的事件绑定等。此时这个setState就会变成同步操作，所谓的同步操作就是让状态立即改变，让视图立即渲染。

```js
 fn() {
    let { x, y, z } = this.state;
    this.setState({ x: x + 1 })    // 异步
    this.setState({ y: y + 1 })     // 异步
    console.log(this.state);

    setTimeout(() => {
      this.setState({ z: z + 1 })   // 同步
      console.log(this.state.z);
    }, 1000)
  }
```



### 3，flushSync

flushSync表示手动刷新任务队列，写代码如下：

![1691378846502](assets/1691378846502.png)



再看如下的代码：

![1691378979450](assets/1691378979450.png)



写一次setState，就想刷新一次队列，如下：

![1691379039369](assets/1691379039369.png)

![1691379069883](assets/1691379069883.png)



还可以这样写，如下：

![1691379197770](assets/1691379197770.png)



## 六 ，合成事件

合成事件就是在JSX元素上，通过onXxx={函数}进行的事件绑定。 直接上代码：

![1691392009692](assets/1691392009692.png)



### 1，事件绑定方式一

改变this指向的方式一：

![1691392108973](assets/1691392108973.png)



传参问题：

![1691392169618](assets/1691392169618.png)



事件对象：

![1691392237755](assets/1691392237755.png)



### 2，事件绑定方式二



处理this，如下：

![1691392354549](assets/1691392354549.png)



传参问题：

![1691392435670](assets/1691392435670.png)



事件对象：

![1691392466571](assets/1691392466571.png)



事件对象不是原生的事件对象，是全成事件对象SyntheticBaseEvent：我们React合成事件触发时，可以获取到事件对象，只不过此对象是合成事件对象（经过React特殊处理，各个浏览器的事件对象统一处理后，构建的一个事件对象），包含了浏览器内置事件对象中的一些属性和方法。如：

- clientX/clientY
- pageX/pageY
- target
- type
- preventDefault
- stopPropagation
- nativeEvent   可以获取浏览器原生的事件对象
- ....



### 3，事件绑定方式三（推荐）

直接上代码：

![1691392845672](assets/1691392845672.png)



## 七，ToDo案例



### 1，分析

画图分析：

![1691393160461](assets/1691393160461.png)



当新增Todo时，就需要弹出一个框，如下：

![1691393310651](assets/1691393310651.png)



技术造型：react + antd



### 2，antd的使用

官网：https://ant.design/index-cn







安装antd:

![1691393461490](assets/1691393461490.png)

![1691393483885](assets/1691393483885.png)



如果要使用antd中的图标，还需要自己安装之，如下：

![1691393547889](assets/1691393547889.png)

![1691393570213](assets/1691393570213.png)



antd就是React中的组件库，常用组件库：

- Vue
  - PC端：element-ui, antd for vue, iView....
  - 移动端：vant, cube...
- React
  - PC端：Antd，AntdPro...
  - 移动端：AntdMobile...



**什么是组件库**：把项目中常用的功能封装成一个个的组件，组件集成结构，样式，功能。



安装完成：

![1691393760378](assets/1691393760378.png)



antd组件库，自带按需引入，不需要配置。



测试一下，创建一个Todo组件，如下：

![1691393893615](assets/1691393893615.png)



![1691393912010](assets/1691393912010.png)



引入组件库，测试之，如下：

![1691393993930](assets/1691393993930.png)



配置汉化，没有汉化之前，如下：

![1691394122395](assets/1691394122395.png)



配置汉化，如下：

![1691394170880](assets/1691394170880.png)



样式分两种：

- todo的样式
- 全局样式（默认样式）



创建两个文件，分别表示上面的样式，如下：

![1691394388110](assets/1691394388110.png)

![1691394407863](assets/1691394407863.png)



### 3，绘制头部

结构如下：

```jsx
import PropTypes from "prop-types"
import React from "react"
import "./Todo.css"
import { DatePicker, Button, Tag } from "antd"

class Todo extends React.Component {
  render() {
    return (<div className="todo-box">
      {/* 头部 */}
      <div className="header">
        <h2 className="title">Todo List任务管理</h2>
        <Button type="primary">新增Todo</Button>
      </div>

      {/* 标签页 */}
      <div className="tag-box">
        <Tag color="#4096ff">全部</Tag>
        <Tag>未完成</Tag>
        <Tag>已完成</Tag>
      </div>
    </div>)
  }
}
export default Todo;
```



样式如下：

```css
.todo-box {
  box-sizing: border-box;
  margin: 0 auto;
  width: 800px;
}

.todo-box .header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-bottom: 10px;
  border-bottom: 1px solid #ddd;
}

.todo-box .header .title {
  font-size: 20px;
  line-height: 50px;
}

.tag-box{
  margin: 15px 0;
}
.tag-box .ant-tag{
  font-size: 14px;
  padding-inline: 15px;
  margin-inline-end: 15px;
  line-height: 30px;
  cursor: pointer;
}
```



效果如下：

![1691396304604](assets/1691396304604.png)



### 4，绘制表格

对应的结构：

```jsx
import PropTypes from "prop-types"
import React from "react"
import "./Todo.css"
import { DatePicker, Button, Tag, Table, Popconfirm } from "antd"
import { formatTimeStr } from "antd/es/statistic/utils";

const zero = function zero(text) {
  text = String(text);
  return text.length < 2 ? '0' + text : text;
}
const formatTime = function formatTime(time) {
  let arr = time.match(/\d+/g);
  let [, month, day, hours = '00', minutes = '00'] = arr;
  return `${zero(month)}-${zero(day)} ${zero(hours)}:${zero(minutes)}`
}

class Todo extends React.Component {
  // 表格列数据
  columns = [
    {
      title: "编号",
      align: "center",
      dataIndex: 'id',
      width: '8%'
    },
    {
      title: "任务描述",
      align: "center",
      ellipsis: true,
      dataIndex: 'todo',
      width: '50%'
    },
    {
      title: "状态",
      dataIndex: 'state',
      align: "center",
      width: '10%',
      render: (text, record) => {
        return +text === 1 ? '未完成' : '已完成'
      }
    },
    {
      title: "完成时间",
      dataIndex: 'time',
      align: "center",
      width: '15%',
      render: (text, record) => {
        let { state, time, complete } = record;
        if (+state === 2) time = complete;
        return formatTime(time);
      }
    },
    {
      title: "操作",
      align: "center",
      render: (text, record) => {
        let { state } = record;
        return <>
          <Popconfirm title="你确定要删除此任务吗？" onConfirm={() => { }}>
            <Button type="link">删除</Button>
          </Popconfirm>

          {
            +state !== 2 ? <Popconfirm title="你确定要把此任务设置成完成吗？" onConfirm={() => { }}>
              <Button type="link">完成</Button>
            </Popconfirm> : null
          }
        </>
      }
    }
  ];

  // 状态
  state = {
    tableData: [
      {
        id: 1,
        todo: "学习react",
        state: 1,
        time: "2023-09-09 18:00:00",
        complete: "2023-09-09 18:00:00"
      },
      {
        id: 2,
        todo: "学习vue3",
        state: 2,
        time: "2023-09-09 18:00:00",
        complete: "2023-09-09 18:00:00"
      }
    ],
    tableLoading: false
  }
  render() {
    let { tableData, tableLoading } = this.state;
    return (<div className="todo-box">
      {/* 头部 */}
      <div className="header">
        <h2 className="title">Todo List任务管理</h2>
        <Button type="primary">新增Todo</Button>
      </div>

      {/* 标签页 */}
      <div className="tag-box">
        <Tag color="#4096ff">全部</Tag>
        <Tag>未完成</Tag>
        <Tag>已完成</Tag>
      </div>

      {/* 表格 */}
      <Table dataSource={tableData} columns={this.columns} loading={tableLoading} pagination={false} rowKey='id' />
    </div>)
  }
}
export default Todo;
```



样式：

```css
.todo-box .ant-table-cell .ant-btn-link {
  padding: 4px;
}
```



效果：

![1691398052605](assets/1691398052605.png)



### 5，绘制弹窗

当点击新增todo时，就需要让弹窗显示，定义一个定义控制弹窗的显示与否，如下：

![1691399139358](assets/1691399139358.png)



结构如下：

```jsx
import PropTypes from "prop-types"
import React from "react"
import "./Todo.css"
import { DatePicker, Button, Tag, Table, Popconfirm, Modal } from "antd"
import { formatTimeStr } from "antd/es/statistic/utils";

const zero = function zero(text) {
  text = String(text);
  return text.length < 2 ? '0' + text : text;
}
const formatTime = function formatTime(time) {
  let arr = time.match(/\d+/g);
  let [, month, day, hours = '00', minutes = '00'] = arr;
  return `${zero(month)}-${zero(day)} ${zero(hours)}:${zero(minutes)}`
}

class Todo extends React.Component {
  // 表格列数据
  columns = [
    {
      title: "编号",
      align: "center",
      dataIndex: 'id',
      width: '8%'
    },
    {
      title: "任务描述",
      align: "center",
      ellipsis: true,
      dataIndex: 'todo',
      width: '50%'
    },
    {
      title: "状态",
      dataIndex: 'state',
      align: "center",
      width: '10%',
      render: (text, record) => {
        return +text === 1 ? '未完成' : '已完成'
      }
    },
    {
      title: "完成时间",
      dataIndex: 'time',
      align: "center",
      width: '15%',
      render: (text, record) => {
        let { state, time, complete } = record;
        if (+state === 2) time = complete;
        return formatTime(time);
      }
    },
    {
      title: "操作",
      align: "center",
      render: (text, record) => {
        let { state } = record;
        return <>
          <Popconfirm title="你确定要删除此任务吗？" onConfirm={() => { }}>
            <Button type="link">删除</Button>
          </Popconfirm>

          {
            +state !== 2 ? <Popconfirm title="你确定要把此任务设置成完成吗？" onConfirm={() => { }}>
              <Button type="link">完成</Button>
            </Popconfirm> : null
          }
        </>
      }
    }
  ];

  // 状态
  state = {
    tableData: [
      {
        id: 1,
        todo: "学习react",
        state: 1,
        time: "2023-09-09 18:00:00",
        complete: "2023-09-09 18:00:00"
      },
      {
        id: 2,
        todo: "学习vue3",
        state: 2,
        time: "2023-09-09 18:00:00",
        complete: "2023-09-09 18:00:00"
      }
    ],
    tableLoading: false,
    modalVisible: false,
    confirmLoading: false  // confirmLoading 控制确定控制的loading状态：提交的防抖处理
  }
  // 关闭弹窗
  closeModal = () => {
    this.setState({
      modalVisible: false
    })
  }
  // 点击提交
  submit = () => {

  }
  render() {
    let { tableData, tableLoading, modalVisible, confirmLoading } = this.state;
    return (<div className="todo-box">
      {/* 头部 */}
      <div className="header">
        <h2 className="title">Todo List任务管理</h2>
        <Button type="primary" onClick={() => {
          this.setState({
            modalVisible: true,
          })
        }}>新增Todo</Button>
      </div>

      {/* 标签页 */}
      <div className="tag-box">
        <Tag color="#4096ff">全部</Tag>
        <Tag>未完成</Tag>
        <Tag>已完成</Tag>
      </div>

      {/* 表格 */}
      <Table dataSource={tableData} columns={this.columns} loading={tableLoading} pagination={false} rowKey='id' />

      {/* 弹窗 */}
      <Modal
        title="新增Todo"
        onCancel={this.closeModal}
        onOk={this.submit}
        maskClosable={false}
        keyboard={false}
        confirmLoading={confirmLoading}
        okText="确认提交"
        open={modalVisible}>

      </Modal>
    </div>)
  }
}
export default Todo;
```



样式：无



效果：

![1691399741660](assets/1691399741660.png)



### 6，绘制表单

结构如下：

```jsx
import PropTypes from "prop-types"
import React from "react"
import "./Todo.css"
import { DatePicker, Button, Tag, Table, Popconfirm, Modal, Form, Input } from "antd"
import { formatTimeStr } from "antd/es/statistic/utils";

const zero = function zero(text) {
  text = String(text);
  return text.length < 2 ? '0' + text : text;
}
const formatTime = function formatTime(time) {
  let arr = time.match(/\d+/g);
  let [, month, day, hours = '00', minutes = '00'] = arr;
  return `${zero(month)}-${zero(day)} ${zero(hours)}:${zero(minutes)}`
}

class Todo extends React.Component {
  // 表格列数据
  columns = [
    {
      title: "编号",
      align: "center",
      dataIndex: 'id',
      width: '8%'
    },
    {
      title: "任务描述",
      align: "center",
      ellipsis: true,
      dataIndex: 'todo',
      width: '50%'
    },
    {
      title: "状态",
      dataIndex: 'state',
      align: "center",
      width: '10%',
      render: (text, record) => {
        return +text === 1 ? '未完成' : '已完成'
      }
    },
    {
      title: "完成时间",
      dataIndex: 'time',
      align: "center",
      width: '15%',
      render: (text, record) => {
        let { state, time, complete } = record;
        if (+state === 2) time = complete;
        return formatTime(time);
      }
    },
    {
      title: "操作",
      align: "center",
      render: (text, record) => {
        let { state } = record;
        return <>
          <Popconfirm title="你确定要删除此任务吗？" onConfirm={() => { }}>
            <Button type="link">删除</Button>
          </Popconfirm>

          {
            +state !== 2 ? <Popconfirm title="你确定要把此任务设置成完成吗？" onConfirm={() => { }}>
              <Button type="link">完成</Button>
            </Popconfirm> : null
          }
        </>
      }
    }
  ];

  // 状态
  state = {
    tableData: [
      {
        id: 1,
        todo: "学习react",
        state: 1,
        time: "2023-09-09 18:00:00",
        complete: "2023-09-09 18:00:00"
      },
      {
        id: 2,
        todo: "学习vue3",
        state: 2,
        time: "2023-09-09 18:00:00",
        complete: "2023-09-09 18:00:00"
      }
    ],
    tableLoading: false,
    modalVisible: false,
    confirmLoading: false  // confirmLoading 控制确定控制的loading状态：提交的防抖处理
  }
  // 关闭弹窗
  closeModal = () => {
    this.setState({
      modalVisible: false,
      confirmLoading: false
    })
    this.formRef.resetFields(); // 清空表单数据
  }
  // 点击提交
  submit = async () => {
    try {
      // 需要对表单的数据进行校验
      await this.formRef.validateFields();
      // data表示表单中的数据   todo是任务描述   time是时间（Moment格式）
      let data = this.formRef.getFieldValue();
    } catch (_) { }
  }
  render() {
    let { tableData, tableLoading, modalVisible, confirmLoading } = this.state;
    return (<div className="todo-box">
      {/* 头部 */}
      <div className="header">
        <h2 className="title">Todo List任务管理</h2>
        <Button type="primary" onClick={() => {
          this.setState({
            modalVisible: true,
          })
        }}>新增Todo</Button>
      </div>

      {/* 标签页 */}
      <div className="tag-box">
        <Tag color="#4096ff">全部</Tag>
        <Tag>未完成</Tag>
        <Tag>已完成</Tag>
      </div>

      {/* 表格 */}
      <Table dataSource={tableData} columns={this.columns} loading={tableLoading} pagination={false} rowKey='id' />

      {/* 弹窗 */}
      <Modal
        title="新增Todo"
        onCancel={this.closeModal}
        onOk={this.submit}
        maskClosable={false}
        keyboard={false}
        confirmLoading={confirmLoading}
        okText="确认提交"
        open={modalVisible}>

        {/* initialValues 给表单设置初始值 */}
        {/* 第一次在表单中填写内容后，关闭了弹窗，再让弹窗弹出时，之前内容还有 */}
        {/* 当关闭弹窗时，需要把上一次的内容清空 */}
        <Form ref={x => this.formRef = x} layout="vertical" initialValues={{ todo: "", time: "" }}>
          {/* Form.Item中的name就是用来收集数据的 */}
          <Form.Item
            label="任务描述"
            name='todo'
            validateTrigger='onBlur'
            rules={[
              { required: true, message: "任务描述是必填项" },
              { min: 6, message: "输入的内容必须是6位以上" }
            ]}
          >
            <Input.TextArea rows={4}></Input.TextArea>
          </Form.Item>
          <Form.Item
            label="预期完成时间"
            name='time'
            validateTrigger='onBlur'
            rules={[
              { required: true, message: "预期完成时间是必填项" },
            ]}
          >
            <DatePicker showTime></DatePicker>
          </Form.Item>
        </Form>
      </Modal>
    </div>)
  }
}
export default Todo;
```



样式如下：

![1691458205988](assets/1691458205988.png)



效果如下：

![1691458222499](assets/1691458222499.png)

需要注意的是得到的时候，不是字符中，是Moment格式。



### 7，接口联调



对axios进行二次封装，如下：

![1691458318432](assets/1691458318432.png)



参考代码如下：

```js
import axios from "axios"
import qs from 'qs'
import _ from '@/assets/utils'
import { message } from 'antd'

const http = axios.create({
    baseURL: '/api',
    timeout: 60000
})

http.defaults.transformRequest = data => {
    if (_.isPlainObject(data)) data = qs.stringify(data)
    return data
}

http.interceptors.response.use(response => {
    return response.data
}, reason => {
    message.error('当前网络繁忙，请您稍后再试~')
    return Promise.reject(reason)
})

export default http
```



对接口进行封装，如下：

![1691458381329](assets/1691458381329.png)



参考代码如下：

```js
import http from "./http"

// 获取指定状态下的任务列表
const queryTaskList = (state = 0) => {
    return http.get('/getTaskList', {
        params: {
            state
        }
    })
}

// 新增任务
const insertTaskInfo = (task, time) => {
    return http.post('/addTask', {
        task,
        time
    })
}

// 删除任务
const removeTaskById = (id) => {
    return http.get('/removeTask', {
        params: {
            id
        }
    })
}

// 完成任务
const updateTaskById = (id) => {
    return http.get('/completeTask', {
        params: {
            id
        }
    })
}

/* 暴露API */
const API = {
    queryTaskList,
    insertTaskInfo,
    removeTaskById,
    updateTaskById
}
export default API
```



把后端服务器启动，如下：

![1691458461479](assets/1691458461479.png)



完成功能，如下：

```js
import PropTypes from "prop-types"
import React from "react"
import "./Todo.css"
import { DatePicker, Button, Tag, Table, Popconfirm, Modal, Form, Input, message } from "antd"
import API from "../api/index.js"
import { flushSync } from "react-dom"

const zero = function zero(text) {
  text = String(text);
  return text.length < 2 ? '0' + text : text;
}
const formatTime = function formatTime(time) {
  let arr = time.match(/\d+/g);
  let [, month, day, hours = '00', minutes = '00'] = arr;
  return `${zero(month)}-${zero(day)} ${zero(hours)}:${zero(minutes)}`
}

class Todo extends React.Component {
  // 表格列数据
  columns = [
    {
      title: "编号",
      align: "center",
      dataIndex: 'id',
      width: '8%'
    },
    {
      title: "任务描述",
      align: "center",
      ellipsis: true,
      dataIndex: 'task',
      width: '50%'
    },
    {
      title: "状态",
      dataIndex: 'state',
      align: "center",
      width: '10%',
      render: (text, record) => {
        return +text === 1 ? '未完成' : '已完成'
      }
    },
    {
      title: "完成时间",
      dataIndex: 'time',
      align: "center",
      width: '15%',
      render: (text, record) => {
        let { state, time, complete } = record;
        if (+state === 2) time = complete;
        return formatTime(time);
      }
    },
    {
      title: "操作",
      align: "center",
      render: (text, record) => {
        let { state, id } = record;
        return <>
          <Popconfirm title="你确定要删除此任务吗？" onConfirm={() => { this.handleRemove(id) }}>
            <Button type="link">删除</Button>
          </Popconfirm>

          {
            +state !== 2 ? <Popconfirm title="你确定要把此任务设置成完成吗？" onConfirm={() => { this.handleUpdate(id) }}>
              <Button type="link">完成</Button>
            </Popconfirm> : null
          }
        </>
      }
    }
  ];

  // 状态
  state = {
    tableData: [],
    tableLoading: false,
    modalVisible: false,
    confirmLoading: false,  // confirmLoading 控制确定控制的loading状态：提交的防抖处理
    selectedIndex: 0, // 控制哪一个标签显示
  }
  // 关闭弹窗
  closeModal = () => {
    this.setState({
      modalVisible: false,
      confirmLoading: false
    })
    this.formRef.resetFields(); // 清空表单数据
  }
  // 点击提交
  submit = async () => {
    try {
      // 需要对表单的数据进行校验
      await this.formRef.validateFields();
      // data表示表单中的数据   todo是任务描述   time是时间（Moment格式）
      let { task, time } = this.formRef.getFieldValue();
      time = time.format("YYYY-MM-DD HH:mm:ss")
      // 向服务器发请求
      this.setState({ confirmLoading: true })
      let { code } = await API.insertTaskInfo(task, time);
      if (+code !== 0) {
        message.error("很遗憾，当前操作失败，稍后再试~")
      } else {
        this.closeModal();
        this.getData(); // 添加成功后，需要重新获取数据
        message.success("恭喜你，当前操作成功~")
      }
    } catch (_) { }
    this.setState({ confirmLoading: false })
  }
  // 点击切换标签页
  changeIndex = (idx) => {
    if (this.state.selectedIndex === idx) return;
    // this.setState({
    //   selectedIndex: idx
    // }, () => {
    //   this.getData();
    // })

    flushSync(() => {
      this.setState({
        selectedIndex: idx
      })
    })
    this.getData();
  }
  // 获取todo列表数据
  getData = async () => {
    let { selectedIndex } = this.state;
    try {
      this.setState({ tableLoading: true })
      // http://localhost:9000/getTaskList?state=0  接口 
      let { code, list } = await API.queryTaskList(selectedIndex);
      console.log("--list:", list);
      if (+code !== 0) list = [];
      this.setState({
        tableData: list
      })
    } catch (_) { }
    this.setState({ tableLoading: false })
  }
  // 在componentDidMount中发ajax请求
  componentDidMount() {
    this.getData();
  }
  // 删除todo
  async handleRemove(id) {
    try {
      let { code } = await API.removeTaskById(id);
      if (+code !== 0) {
        message.error("很遗憾，当前操作失败，稍后再试~")
      } else {
        this.getData();
        message.success("恭喜你，当前操作成功~")
      }
    } catch (_) { }
  }
  // 设置todo完成
  async handleUpdate(id) {
    try {
      let { code } = await API.updateTaskById(id);
      if (+code !== 0) {
        message.error("很遗憾，当前操作失败，稍后再试~")
      } else {
        this.getData();
        message.success("恭喜你，当前操作成功~")
      }
    } catch (_) { }
  }

  render() {
    let { tableData, tableLoading, modalVisible, confirmLoading, selectedIndex } = this.state;
    return (<div className="todo-box">
      {/* 头部 */}
      <div className="header">
        <h2 className="title">Todo List任务管理</h2>
        <Button type="primary" onClick={() => {
          this.setState({
            modalVisible: true,
          })
        }}>新增Todo</Button>
      </div>

      {/* 标签页 */}
      <div className="tag-box">
        <Tag onClick={() => this.changeIndex(0)} color={selectedIndex === 0 ? "#4096ff" : ''}>全部</Tag>
        <Tag onClick={() => this.changeIndex(1)} color={selectedIndex === 1 ? "#4096ff" : ''}>未完成</Tag>
        <Tag onClick={() => this.changeIndex(2)} color={selectedIndex === 2 ? "#4096ff" : ''}>已完成</Tag>
      </div>

      {/* 表格 */}
      <Table dataSource={tableData} columns={this.columns} loading={tableLoading} pagination={false} rowKey='id' />

      {/* 弹窗 */}
      <Modal
        title="新增Todo"
        onCancel={this.closeModal}
        onOk={this.submit}
        maskClosable={false}
        keyboard={false}
        confirmLoading={confirmLoading}
        okText="确认提交"
        open={modalVisible}>

        {/* initialValues 给表单设置初始值 */}
        {/* 第一次在表单中填写内容后，关闭了弹窗，再让弹窗弹出时，之前内容还有 */}
        {/* 当关闭弹窗时，需要把上一次的内容清空 */}
        <Form ref={x => this.formRef = x} layout="vertical" initialValues={{ todo: "", time: "" }}>
          {/* Form.Item中的name就是用来收集数据的 */}
          <Form.Item
            label="任务描述"
            name='task'
            validateTrigger='onBlur'
            rules={[
              { required: true, message: "任务描述是必填项" },
              { min: 6, message: "输入的内容必须是6位以上" }
            ]}
          >
            <Input.TextArea rows={4}></Input.TextArea>
          </Form.Item>
          <Form.Item
            label="预期完成时间"
            name='time'
            validateTrigger='onBlur'
            rules={[
              { required: true, message: "预期完成时间是必填项" },
            ]}
          >
            <DatePicker showTime></DatePicker>
          </Form.Item>
        </Form>
      </Modal>
    </div>)
  }
}
export default Todo;
```





## 八，Hook

### 1，什么是Hook

函数式组件特点：

- 不具备状态，ref，生命周期函数。第一次渲染完毕后，无法基于组件内部的操作实现更新。
- 具备属性和插槽，通过父组件可以控制重新渲染。
- 渲染流程简单，渲染速度较快。
- 基于函数式编程。



类组件特点：

- 具备状态，ref，生命周期函数，属性和插槽。
- 可以灵活控制组件的更新，因为它内部是可以有状态的。
- 基于生命周期函数，在不同的阶段，可以做不同的事情。
- 渲染流程复杂，渲染速度慢一点
- 基于OOP编程，更方便实现继承。



可以使用hook，让函数式组件变的更加强大，hook是React官方提供的API，10多个。是V16.8中新增的。已经出来几年了。类似于Vue3中的组合式API。

- 作用：用于在函数式组件中模拟出类组件的功能。如：state，生命周期，ref，上下文...
- 价值：有了hook，我们就可以不再使用类组件。官方说了，并不是要淘汰类组件。hook不能出现在类组件。
- 具备能力：给你一个类组件，你能转化成函数式组件。给你一个函数式组件，你能转化成类组件。
- 哪些：useState, useEffect, useLayoutEffect，useContext, userReducer, useRef, useMemo, useCallback..
- 开源hook: react-use, ahooks...



### 2，useState

作用：useState是用于在函数式组件中定义状态的。



语法：

```js
const [num, setNum] = useState(initalState); // 返回一个state，以有更新状态的函数
```





直接上一个计数器案例，如下：

![1691462929701](assets/1691462929701.png)



你需要具备把一个函数式组件翻译成类组件的能力。再去来一个案例，投票案例，如下：

```jsx
import { useState } from "react"
function One() {

  let [state, setState] = useState({
    supNum: 10,
    oppNum: 5
  })

  const handle = (type) => {
    if (type === 'sup') {
      // 在类组件中,通过this.setState,可以实现修改局部的状态
      // 函数式组件中, 不行,不能修改局部状态
      setState({
        ...state,
        supNum: state.supNum + 1
      })
      return;
    }
    setState({
      ...state,
      oppNum: state.oppNum + 1
    })
  }
  return (<div>
    <div className="header">
      <h2 className="title">学习React需要JS基本功很强?</h2>
      <span className="num">{state.supNum + state.oppNum}人</span>
    </div>
    <div className="main">
      <p>支持人数:{state.supNum}人</p>
      <p>反对人数:{state.oppNum}人</p>
    </div>
    <div className="footer">
      <button onClick={() => handle('sup')}>支持</button>
      <button onClick={() => handle('opp')}>反对</button>
    </div>
  </div>)
}
export default One;
```



效果如下：

![1691463530610](assets/1691463530610.png)



上面的写法，功能没有问题，官方不建议，建议如果有多个状态，调用useState多次，如下：

![1691463692782](assets/1691463692782.png)



关于同步和异步问题：

- 在React18中，调用setXxx去修改状态时，它也是异步的
- 在React16中，也和this.setState一样，放在合成事件中、周期函数中。是异步的。放在其它的异步操作中（定时器，手动事件绑定中）是同步的。



### 3，useEfffect

在函数式组件中没有生命周期的，使用useEffect可以模拟类组件中的生命周期。语法：

```js
useEffect(() => {
    // fn1中写副作用
    return ()=>{
        // fn2中清除副作用
    }
}, [依赖数组])
```



useEffect的写法一：

![1691475433189](assets/1691475433189.png)





useEffect的写法二：

![1691475663159](assets/1691475663159.png)



useEffect的写法三：

![1691475980067](assets/1691475980067.png)



useEffect的写法四：

![1691476264137](assets/1691476264137.png)



hook不能放在if、for等语句中，必须放在函数组件内部的最顶层，如下：

![1691476461483](assets/1691476461483.png)



上面的代码修改之，如下：

![1691476534844](assets/1691476534844.png)



写上一个函数，模拟发送ajax请求，如下：

![1691476784832](assets/1691476784832.png)



修改之，如下：

![1691476839978](assets/1691476839978.png)



如果就要使用async和await，修改如下：

![1691476969955](assets/1691476969955.png)



### 4，useLayoutEffect



实现如下的案例：

![1691477341488](assets/1691477341488.png)



现在把上面的useEffect改成useLayoutEffect，如下：

![1691477413797](assets/1691477413797.png)



useLayoutEffect总结

- useLayoutEffect语法和useEffect语法一样。
- useLayoutEffect会阻塞浏览器渲染真实DOM，优先执行useLayoutEffect中的callback。
- useEffect不会阻塞浏览器渲染真实DOM，在渲染真实DOM后，再去执行useEffect中的callback.
- useLayoutEffec设置的callback要优先于useEffect去执行。
- 两者的callback中依然可以获取DOM，因为真实DOM已经创建了，区别是浏览器是否渲染。
- 如果在callback中修改了状态值，视图要更新了
  - 对于useEffect来说，浏览器肯定是把第一次的真实DOM已经绘制了，再去渲染第二次真实DOM。
  - 对于useLayoutEffect来说，浏览器是把两次真实DOM的渲染，合并在一起渲染。
- useLayoutEffect在项目中用的并不是很多，了解就行。



视图更新步骤：

- 第一步：基于babel-preset-react-app把jsx编译成createElement形式
- 第二步：把createElement执行，创建出虚拟DOM
- 第三步：基于root.render方法把虚拟DOM变为真实DOM
  - 对于useLayoutEffect，阻塞第四步操作，先执行useLayoutEffect中的callback
  - 对于useEffect，第四步操作是先进行的，然后执行useEffect中的callback
- 第四步：浏览器渲染和绘制真实DOM



### 5，useRef



之前在类组件中，我们基于ref可以做什么：

- 在标签上写ref，目的是为了获取DOM元素
- 在类组件上写ref，目的是为了获取子组件实例，进而调用子组件中的属性和方法
- 在函数组件上写ref，报错，说你需要使用React.forwardRef实现ref转发，转发的目的是为了获取子组件中的DOM元素。



ref的使用方式：

- ref="box"      获取：this.refs.box 【不推荐】

- ref={x=>this.box =x}   获取：this.box

- this.box = React.createRef() 创建一个ref对象    

  ```html
   <h1 ref={this.box}></h1>  获取：this.box.current获取DOM元素
  ```



使用函数式组件写一个计数器，在函数式组件中获取DOM元素，报错了，如下：

![1691543880000](assets/1691543880000.png)



使用第二种写法：

![1691544031070](assets/1691544031070.png)



使用第三种写法：

![1691544117654](assets/1691544117654.png)



在函数式组件中，还可以通过useRef这个hook，来获取DOM元素或子组件实例，如下：
![1691544299580](assets/1691544299580.png)



通过React.creaetRef和通过useRef都是可以获取DOM元素或子组件实例，一起使用，如下：

![1691544422937](assets/1691544422937.png)



看代码，说一下，他们之间的区别：

![1691544885853](assets/1691544885853.png)



总结：

- 在类组件中，创建ref对象，是基于React.createRef的。
- 在函数组件中，为了保证性能，我们建议使用useRef来创建ref对象。



要获取组件实例，如下：

![1691545112507](assets/1691545112507.png)



如果把组件换成函数式组件，如下：

![1691545209549](assets/1691545209549.png)



使用ref转发，目的是获取子组件内部的某个DOM元素。如下：

![1691545269034](assets/1691545269034.png)



### 6，useImperativeHandle

上面讲了ref转发，目的是为了获取函数式组件中的DOM元素，我们能不能获取子组件内部的状态或方法？

答：可以的，通过useImperativeHandle。代码如下：

![1691545501779](assets/1691545501779.png)



### 7，useMemo

准备一个静态组件，如下：

![1691547019935](assets/1691547019935.png)



参考代码：

```jsx
import React, { useState, useEffect, useRef, useImperativeHandle } from "react"

function One() {
  let [supNum, setSupNum] = useState(10)
  let [oppNum, setOppNum] = useState(5)
  let [other, setOther] = useState(0)

  let total = supNum + oppNum;
  let ratio = '--';
  if (total > 0) ratio = (supNum / total * 100).toFixed(2) + "%";

  return (<div className="vote-box">
    <div className="main">
      <p>支持人数：{supNum}人</p>
      <p>反对人数：{oppNum}人</p>
      <p>支持率：{ratio}</p>
      <hr />
      <p>弃权：{other}</p>
    </div>
    <div className="footer">
      <button onClick={() => setSupNum(supNum + 1)}>支持</button>
      <button onClick={() => setOppNum(oppNum + 1)}>反对</button>
      <button onClick={() => setOther(other + 1)}>弃权</button>
    </div>
  </div>)
}
export default One;
```



当点击支持，或反对，或弃权，整个函数都会重新执行，如下：

![1691547201556](assets/1691547201556.png)



![1691547256367](assets/1691547256367.png)



假定这个计算支持率的算法，非常复杂，非常复杂的计算，是比较消耗资源。点击弃权，没有参与页面渲染，不需要让支持率重新计算的，可以使用useMemo把一个复杂的计算缓存起来，如下：

![1691547563294](assets/1691547563294.png)



总结：

- useMemo第一次渲染时，会执行callback。
- 后面只有依赖的状态发生变化了，callback才会重新执行。
- 每一次会把callback执行的结果返回
- useMemo具备缓存功能。就相当于把复杂的计算缓存起来了。如果依赖的状态没有变化，就会走缓存。类似于vue中的计算属性。
- 如果在函数式组件，有消耗性能的计算，尽可能使用useMemo缓存起来，提高组件的更新速度。



### 8，useCallback

作用：用来缓存一个函数声明的。



写代码如下：

![1691548044380](assets/1691548044380.png)



可以使用useCallback缓存函数声明，如下：

![1691548284508](assets/1691548284508.png)



什么时候会使用到的useCallback?

- 父组件嵌套子组件时，父组件内部有一个函数，基于属性传递给子组件，此时传递的函数，可以基于useCallback缓存起来。
- useCallback是用来缓存函数式组件内部的一个函数声明，不要乱用。虽然缓存函数声明，减少堆空间的开辟，但是useCallback本身也有自己的处理逻辑和缓存机制，这也是需要消耗时间的。



直接上代码：

![1691548879317](assets/1691548879317.png)



由于传递的fn是不会变的，可以不让子更新，如下：

![1691548985863](assets/1691548985863.png)





## 九，组件通信

### 1，父子通信（类组件）

拆组件：

![1691549291609](assets/1691549291609.png)

准备静态页，Father.jsx，如下：

```jsx
import React from "react"
import Main from "./Main"
import Footer from "./Footer"

class Father extends React.Component {
  render() {
    return (<div>
      <div className="header">
        <h2 className="title">React比Vue值钱！</h2>
      </div>
      <Main></Main>
      <Footer></Footer>
    </div>)
  }
}

export default Father;
```



Main.jsx，如下：

```jsx
import React from "react"

class Main extends React.Component {
  render() {
    return (
      <div className="main">
        <p>支持人数：10人</p>
        <p>反对人数：5人</p>
        <p>支持率：--</p>
      </div>)
  }
}

export default Main;
```



Footer.jsx， 如下：

```jsx
import React from "react"

class Footer extends React.Component {
  render() {
    return (
      <div className="footer">
        <button onClick={() => { }}>支持</button>
        <button onClick={() => { }}>反对</button>
        <button onClick={() => { }}>弃权</button>
      </div>)
  }
}

export default Footer;
```



效果如下：

![1691550729909](assets/1691550729909.png)



组件通信，看图：

![1691551115049](assets/1691551115049.png)



在父中定义状态，和更新状态的方法，如下：

![1691551245330](assets/1691551245330.png)



父传子，如下：

![1691551303871](assets/1691551303871.png)



子中接收，如下：

![1691551533607](assets/1691551533607.png)

![1691551631364](assets/1691551631364.png)



效果如下：

![1691551638859](assets/1691551638859.png)



优化，当改变状态时，看子是否都渲染了，如下：



![1691551887239](assets/1691551887239.png)



测试如下：

![1691551937008](assets/1691551937008.png)



![1691552021754](assets/1691552021754.png)







### 2，父子通信（函数组件）



定义Father.jsx，如下：

```jsx

import React, { useState, useEffect, useRef, useCallback } from "react"
import Main from "./Main"
import Footer from "./Footer"


function Father() {

  return (<div>
    <div className="header">
      <h2 className="title">React比Vue值钱！</h2>
    </div>
    <Main></Main>
    <Footer></Footer>
  </div>)
}
export default Father;

```



定义Main.jsx组件，如下：

```jsx
import React, { useState, useEffect, useRef, useCallback } from "react"


function Main() {
  return (
    <div className="main">
      <p>支持人数：10人</p>
      <p>反对人数：5人</p>
      <p>支持率：--</p>
    </div>)
}
export default Main;
```



定义Footer.jsx组件，如下：

```jsx
import React, { useState, useEffect, useRef, useCallback } from "react"


function Footer() {
  return (
    <div className="footer">
      <button onClick={() => { }}>支持</button>
      <button onClick={() => { }}>反对</button>
      <button onClick={() => { }}>弃权</button>
    </div>)
}
export default Footer;
```



效果如下：

![1691561585767](assets/1691561585767.png)



在父组件中定义状态和方法，传递给子，如下：

![1691561733336](assets/1691561733336.png)

参考代码：

```jsx

import React, { useState, useEffect, useRef, useCallback } from "react"
import Main from "./Main"
import Footer from "./Footer"


function Father() {
  let [supNum, setSupNum] = useState(10)
  let [oppNum, setOppNum] = useState(5)

  const change = (type) => {
    if (type == 'sup') {
      setSupNum(supNum + 1);
      return
    }
    setOppNum(oppNum + 1)
  }

  return (<div>
    <div className="header">
      <h2 className="title">React比Vue值钱！</h2>
    </div>
    <Main supNum={supNum} oppNum={oppNum}></Main>
    <Footer change={change}></Footer>
  </div>)
}
export default Father;
```



子接收之，如下：

![1691561961165](assets/1691561961165.png)

```jsx
import React, { useState, useEffect, useRef, useCallback } from "react"
import PropTypes from "prop-types"

function Main(props) {
  let { supNum, oppNum } = props;
  let total = supNum + oppNum;
  let ratio = '--';
  if (total > 0) ratio = (supNum / total * 100).toFixed(2) + "%";

  return (
    <div className="main">
      <p>支持人数：{supNum}人</p>
      <p>反对人数：{oppNum}人</p>
      <p>支持率：{ratio}</p>
    </div>)
}
Main.defaultProps = {
  supNum: 0,
  oppNum: 0,
}
Main.propTypes = {
  supNum: PropTypes.number,
  oppNum: PropTypes.number,
}
export default Main;
```



![1691562069020](assets/1691562069020.png)

```jsx
import React, { useState, useEffect, useRef, useCallback } from "react"
import PropTypes from "prop-types"

function Footer(props) {
  let { change } = props;
  return (
    <div className="footer">
      <button onClick={() => { change('sup') }}>支持</button>
      <button onClick={() => { change('opp') }}>反对</button>
      <button onClick={() => { }}>弃权</button>
    </div>)
}
Footer.defaultProps = {}
Footer.propTypes = {
  change: PropTypes.func.isRequired,
}
export default Footer;
```



效果如下：

![1691562147013](assets/1691562147013.png)



优化一：

![1691562240332](assets/1691562240332.png)



优化二：

![1691562347692](assets/1691562347692.png)



现在footer，Father更新时，都会重新渲染，如下：

![1691562444710](assets/1691562444710.png)

![1691562514798](assets/1691562514798.png)



优化三：（下去再找一下）

![1691562850712](assets/1691562850712.png)





### 3，祖先后代码通信（类组件）

如果组件嵌套比较深，一层一层传递比较麻烦，如下：

![1691563097178](assets/1691563097178.png)



我们可以基于上下文对象，实现跨层传递，如下：

![1691563320220](assets/1691563320220.png)

搭建静态组件，如下：

```jsx
// Father.jsx
import React from "react"
import Main from "./Main"
import Footer from "./Footer"

class Father extends React.Component {
  render() {
    return (<div>
      <div className="header">
        <h2 className="title">React比Vue值钱！</h2>
      </div>
      <Main></Main>
      <Footer></Footer>
    </div>)
  }
}

export default Father;
```



```jsx
// Main.jsx
import React from "react"

class Main extends React.Component {
  render() {
    return (
      <div className="main">
        <p>支持人数：10人</p>
        <p>反对人数：5人</p>
        <p>支持率：--</p>
      </div>)
  }
}

export default Main;
```



```jsx
// Footer.jsx
import React from "react"

class Footer extends React.Component {
  render() {
    return (
      <div className="footer">
        <button onClick={() => { }}>支持</button>
        <button onClick={() => { }}>反对</button>
        <button onClick={() => { }}>弃权</button>
      </div>)
  }
}

export default Footer;
```



效果如下 ：

![1691563553529](assets/1691563553529.png)



第一步：创建 一个上下文对象，用来管理上下文中的信息，如下：

![1691563646714](assets/1691563646714.png)



第二步，让祖先组件，把状态和修改状态的方法，存储到的上下文中，如下：

![1691563787803](assets/1691563787803.png)

![1691564287495](assets/1691564287495.png)



参考代码：

```jsx
import React from "react"
import Main from "./Main"
import Footer from "./Footer"
import VoteContext from "../VoteContext"

class Father extends React.Component {
  state = {
    supNum: 10,
    oppNum: 5
  }
  change = type => {
    let { supNum, oppNum } = this.state;
    if (type == 'sup') {
      this.setState({ supNum: supNum + 1 })
      return;
    }
    this.setState({ oppNum: oppNum + 1 })
  }
  render() {
    let { supNum, oppNum } = this.state;
    return <VoteContext.Provider value={{ supNum, oppNum, change: this.change }}>
      <div>
        <div className="header">
          <h2 className="title">React比Vue值钱！</h2>
        </div>
        <Main></Main>
        <Footer></Footer>
      </div>
    </VoteContext.Provider>

  }
}
export default Father;
```



第三步：在后代组件中，获取上下文对象

- 在Main组件中，获取状态
- Footer组件中，获取修改状态的方法，当点击支持或反对时调用方法

![1691564325424](assets/1691564325424.png)



还有一种使用状态的方式，如下：

![1691564557867](assets/1691564557867.png)



### 4，祖先后代码通信（函数组件）



准备静态资源：

```jsx
// Father.jsx

import React, { useState, useEffect, useRef, useCallback } from "react"
import Main from "./Main"
import Footer from "./Footer"


function Father() {

  return (<div>
    <div className="header">
      <h2 className="title">React比Vue值钱！</h2>
    </div>
    <Main></Main>
    <Footer></Footer>
  </div>)
}
export default Father;
```



```jsx
// Main.jsx

import React, { useState, useEffect, useRef, useCallback } from "react"

function Main() {
  return (
    <div className="main">
      <p>支持人数：10人</p>
      <p>反对人数：5人</p>
      <p>支持率：--</p>
    </div>)
}
export default Main;
```



```jsx
// Footer.jsx

import React, { useState, useEffect, useRef, useCallback } from "react"

function Footer() {
  return (
    <div className="footer">
      <button onClick={() => { }}>支持</button>
      <button onClick={() => { }}>反对</button>
      <button onClick={() => { }}>弃权</button>
    </div>)
}
export default Footer;
```



效果如下：

![1691566123095](assets/1691566123095.png)



准备上下文对象：

![1691566155384](assets/1691566155384.png)



祖先提供数据，如下：

![1691566267364](assets/1691566267364.png)



子孙就可以消费数据了，如下：

![1691566382693](assets/1691566382693.png)

还有一个hook的写法，如下：

![1691566479779](assets/1691566479779.png)



在Footer中，也使用useContext这种写法，如下：

![1691566562489](assets/1691566562489.png)





## 十，Redux（难）

### 1，Redux的基本介绍



关于React的技术栈：

- React 核心
- Redux 集中状态管理  react-redux  redux相关的中间件
- mobx 
- react-router-dom  V5V6
- antd  antd mobile
- axios fetch 
- dva
- umi
- antd pro
- ... 



组件通信：

- 父子通信： props / ref
- 祖先和后代通信：context上下文
- redux/react-redux 也是实现组件通信的方案，强大，不管任何类型的组件，都可以基于redux通信
- 在真实开发中，通信方案用的比较多的就是上面的说的几种



Redux的流程图：

![1691631304866](assets/1691631304866.png)



安装redux，如下：

![1691631357870](assets/1691631357870.png)



后面还需要安装如下的依赖：后面用到的时候再安装

![1691631384680](assets/1691631384680.png)



### 2，使用Redux

创建一个仓库，需要给仓库配置一个reducer，如下：

![1691632535167](assets/1691632535167.png)

```js
import { createStore } from "redux"

// 初始状态
let initial = {
  supNum: 10,
  oppNum: 5
}

// 管理员：是用于修改全局状态
const reducer = function reducer(state = initial, action) {
  // state存储了全局的状态，最开始没有时候，把initial赋值给他
  // action reducer就是基于action进行状态修改的，这个action中必须有一个type属性
  switch (action.type) {
    case 'SUP':
      state.supNum++;
      break;
    case 'OPP':
      state.oppNum++;
      break
    default:
      break;
  }
  // return的内容，会整体替换store容器中的内容
  return state;
}

// dispatch是用于派发一个action
// store.dispatch({type:"SUP"})

// 创建仓库
const store = createStore(reducer);

export default store;
```



在修改状态时，把原本的状态copy一份，如下：

![1691632661732](assets/1691632661732.png)



到此，仓库就准备好了，如下：

![1691632776127](assets/1691632776127.png)



准备一个上下文，如下：

![1691632804984](assets/1691632804984.png)



给所有的后代提供仓库，如下：

![1691632907367](assets/1691632907367.png)



在后代中就可以使用仓库了，如下：

![1691633211639](assets/1691633211639.png)

![1691633231838](assets/1691633231838.png)

![1691633246776](assets/1691633246776.png)



浏览器中测试之，如下：

![1691633280897](assets/1691633280897.png)





现在有仓库了，就可以从仓库中获取状态，就可以通过仓库，派发action。先获取状态，如下：

![1691634572359](assets/1691634572359.png)

![1691634624835](assets/1691634624835.png)



在Footer组件中，点击支持或反对，还需要派发action，如下：

![1691634811259](assets/1691634811259.png)



当点击支持或反对时，状态肯定是发生变化了，但是界面是没有更新的，状态发生变化了，肯定会把事件池中的方法执行了，处理之，如下：

![1691635155790](assets/1691635155790.png)



如果是类组件，处理之，如下：

![1691635222549](assets/1691635222549.png)

![1691635320270](assets/1691635320270.png)



总结一个redux的使用：

- 创建一个store，需要给store配置一个reducer，reducer中用来修改状态。
- 在入口中，基于上下文，把store放到上下文中，哪里需要用到store，就需要从store中获取。
- 在组件中，通过store.getState就可以获取状态。通过store.dispatch就可以派发action
- 当状态修改了，它会调用store.subscript中的回调函数，在这个回调函数中，想办法让组件更新
- 组件更新：类组件，使用this.forceUpdate。函数组件，多定义出一个状态，更新状态。



### 3，reducer的拆分与合并

一个项目是有N个模块组成，不同模块的需要共享的状态，可以给它放到不同的reduer中。也就是说在真正的项目中，会对状态和reducer进行模块化的拆分。把状态和reducer拆分后，最后还需要进行合并，合并成一个大的reducer。配置给store。假定有两个模块：vote，user。创建两上reducer文件，如下：

![1691636043351](assets/1691636043351.png)

![1691636200913](assets/1691636200913.png)



接下来，需要合并reducer，如下：

![1691636433677](assets/1691636433677.png)



在创建仓库时，就需要给仓库配置合并后的reducer，如下：

![1691636511362](assets/1691636511362.png)



在使用状态的地方如下：

![1691636583708](assets/1691636583708.png)

![1691636609749](assets/1691636609749.png)

派发action，如下：

![1691636653071](assets/1691636653071.png)



浏览器中测试之，如下：

![1691636698699](assets/1691636698699.png)



派发的操作不需要指定是哪个模块的，每一次派发，都会去所有的reducer进行逐一的匹配，和谁匹配成功，就执行谁的逻辑。



### 4，把type作统一管理

action是一个对象，这个对象中有一个type，就是信号，reducer就根据type进行操作。每一次派发，都会去所有的reducer进行逐一的匹配，和谁匹配成功，就执行谁的逻辑。可能存在问题：团队协作开发时，人员比较多，在派发type时，可能有冲突。所以我们要保证，不管哪个模块，不管哪个组件，派发信号（type），type的值必须唯一。在store目录下面创建一个action-types.js，如下：

![1691648796530](assets/1691648796530.png)

统一管理这些信号，除了保证不冲突，还能避免程序员因为粗心大意，导致错误。



在reducer中，就要使用定义的信号，如下：

![1691648878765](assets/1691648878765.png)

![1691649003012](assets/1691649003012.png)



在组件中，派发信号时，也需要改变，如下：

![1691649084143](assets/1691649084143.png)



浏览器测试之，OK。



### 5，actionCreator的创建

前面把reducer作了拆分，拆分后还需要合并。之前我们是派发一个action，这个action中必须有一个type属性，表示信号，刚才我们把信号也做了统一管理。现在需要把派发的整个行为对象，按模块进行统一管理。在store的文件夹下，创建一个actoins，如下：

![1691649832461](assets/1691649832461.png)

![1691649506955](assets/1691649506955.png)



合并之，如下：

![1691649585234](assets/1691649585234.png)



我们的actoin如下：

```js
action = {
    vote:{
        support(){
            return {type:TYPES.VOTE_SUP}
        },
        oppose(){
            return {type:TYPES.VOTE_OPP}
        }
    }，
    user:{
       // ...
	}
}
```



现在派发时，就需要调用上面的函数了，只有调用上面的函数，才会返回action，如下：

![1691649903114](assets/1691649903114.png)



### 6，react-redux的使用

react-redux可以让我们在react项目中，更加简单方便的使用redux。经过前面的讲解，发现使用redux，确定不方便。安装一下，如下：

![1691651024573](assets/1691651024573.png)



react-redux中提供了一个组件，叫Provider，使用如下：

![1691651199929](assets/1691651199929.png)



在Father组件中，处理如下：

![1691651652646](assets/1691651652646.png)



简写，如下：

![1691651761502](assets/1691651761502.png)



还可以继承简写，如下：

![1691651832296](assets/1691651832296.png)



浏览器测试之，OK。



在Main组件中，继续使用状态，如下：

![1691651936257](assets/1691651936257.png)



在Footer组件，如何派发actoin呢？如下：

![1691652306869](assets/1691652306869.png)



可以简化之，如下：

![1691652452075](assets/1691652452075.png)



浏览器测试之，OK。



### 7，redux中间件

画一张，如下：

![1691717093414](assets/1691717093414.png)



安装redux-logger中间件，如下：

![1691717150750](assets/1691717150750.png)



在仓库的入口中使用之，如下：

![1691717245354](assets/1691717245354.png)



在浏览器中测试之，如下：

![1691717335170](assets/1691717335170.png)



之前写的action creator都是同步的action creator，也就是说它时里面没有异步代码，可以尝试写一点异步代码：

![1691717557268](assets/1691717557268.png)



在测试之前，先分析，上面的support函数是一个async函数，async函数返回的是promise。之前返回的是一个action，现在返回的是一个promise，这个promise中是没有type属性的，测试之，如下：

![1691717702640](assets/1691717702640.png)

默认情况下，redux处理不了这种action creator。在不使用任何中间件的情况下，actionCreator对象中，是不支持异步操作的，我们要想让action creator执行，必须返回标准的action。在真实开发中，往往我们是需要异步操作的，如在派发时，我们需要先向服务器发送请求，得到数据后，再进行派发。此时必须使用中间件来处理，官方推荐redux-thunk中间件。安装之，如下：

![1691717913412](assets/1691717913412.png)



使用之，如下：

![1691717960717](assets/1691717960717.png)



此时action creator也需要变化一个语法，如下：

![1691718230403](assets/1691718230403.png)



浏览器测试之，如下：

![1691718282718](assets/1691718282718.png)





除了redux-thunk中间件之外，还有一个redux-promise中间件，使用之，如下：

![1691718406000](assets/1691718406000.png)

![1691718341104](assets/1691718341104.png)



浏览器测试之，如下：

![1691718430837](assets/1691718430837.png)





## 十二，项目



视频的地址：https://www.bilibili.com/video/BV15o4y1v7hm/?spm_id_from=333.999.0.0&vd_source=de29feab70bf3ba9f8d71d2b7985b84c



从第26个视频开始看就OK。

![1691718594725](assets/1691718594725.png)





















































































