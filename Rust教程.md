# Rust教程

[toc]

## 第一章



### 安装Rust

- 官网：https://www.rust-lang.org
- 步骤：按1执行安装即可
- 更新：rustup update
- 卸载：rustup self uninstall
- 验证：rustc --version
- 文档：rustup doc（存于本地，浏览器打开）
- 开发工具：VSCode	—Rust插件
- 版本切换：rustup default stable/nightly/beta

------



### Hello World

- 使用VSCode打开目录的命令：code .	（空格 + 点）

- 程序后缀名：rs

- 文件命名规范：

	- 使用小写
	- 下横线分隔
	- hello_world.rs

- 编译：rustc main.rs

- 运行：

	- Windows：	.\main.exe
	- Linux/Max:    ./main

- demo

	```rust
	fn main(){
	    println!("Hello World");
	}
	```

	- 定义函数 fn，main函数是Rust可执行程序最早运行的代码

	- println! 是一个宏Rust macro(宏)	-如果是函数的话，就没有感叹号

	- "Hello World" 是一个字符串，作println的参数

	- 代码以 ; 结尾

		

- Rust先编译后运行，为ahead-of-time编译的程序。（预编译语言）

	- 可以先编译程序，然后将可执行文件交给别人运行（无需安装Rust）
	- Windows编译除了二进制文件，还会生成pdb编译流程文件
	- rustc只适用于简单Rust程序（复杂的用Cargo）

	------

	

### Cargo

- Cargo是Rust的**构建系统**和**包管理**工具。

	- 构建代码、下载依赖的库、构建这些库

- 安装Rust是自带的

	- cargo --version

- **创建**Cargo项目    **cargo new 项目名称**

	- <img src="C:\Users\xd\AppData\Roaming\Typora\typora-user-images\image-20211218222030560.png" alt="image-20211218222030560" style="zoom: 50%;" />
		- 命令会生成一个项目同名文件夹
		- 项目文件夹下
			- src目录
				- main.rs，cargo自动生成的
				- 源代码都应该在src目录下
				- 而，比如Cargo.toml文件位于项目顶层下，顶层目录可以放置：README、许可信息、配置文件和其他与项目源码无关的文件。
			- .gitignore （初始化一个新的Git仓库）
				- （可以使用其他的VCS或者不使用VCS，cargo new的时候使用 --version这个flag）
			- Cargo.toml文件
				- TOML（Tom‘s Obvious, Minimal Language）格式，是Cargo的配置文件
				- <img src="C:\Users\xd\AppData\Roaming\Typora\typora-user-images\image-20211218223626121.png" alt="image-20211218223626121" style="zoom: 33%;" />
					- [package] 区域标题，表示下面的内容是用来配置包[package]的
					- name 项目名
					- version 版本
					- authors 作者
					- edition 使用的Rust版本
					- [dependencies] 下方为项目的依赖项
				- 补充：在Rust里，代码的包被称作crate
		- 因为插件（rust-analysis），点击 .toml文件会自动编译生成
			- target目录（顶层）
			- Cargo.lock文件（顶层）
	- 如果创建项目的时候没有使用Cargo，也可以转换。
		- 把源代码移动到src目录下
		- 创建Cargo.toml并填写相应的配置

	

- **构建**Cargo项目  **cargo build**

	- 创建的可执行文件
		- target/debug/hello_cargo  (Linux、Mac)
		- target\debug\hello_cargo.exe  (Windows)
		- 第一次构建会生成Cargo.lock文件
			- 负责追踪项目依赖的精确版本
			- 不需要手动修改该文件
	- 运行可执行文件
		- ./target/debug/hello_cargo  (Linux、Mac)
		- .\target/debug/hello_cargo.exe  (Windows)

	

- **构建并运行**Cargo项目  **cargo run**

	- 编译+执行
	- 编译过若无源码更改，就只是执行不编译

- **检查代码**，保证通过编译，而不生成可执行文件  **cargo check**

	- 比 cargo built  快得多

- 为**发布**构建  cargo built --release

	- 编译时会进行优化

		- 代码运行的更快，但编译时间更长

	- 会在target/release而不是target/debug生成可执行文件

		

- 最后，**建议尽量用Cargo**

	------

	



## 第二章



### 猜数游戏：一次猜测

学习内容：

- let、match等方法

- 相关的项目
- 外部的crate

游戏目标：生成1-100随机数，提示猜测，反馈猜大了、小了



```rust
// 调用库使用use关键字
// prelude (存疑的概念)
use std::io;	//基本IO库，位于标准库下。		

fn main() {
    println!("猜数！");	
    println!("猜测一个数");
   
	// 常规赋值
    // let foo = 1;	//默认下，Rust变量的值是不可变的（immutable）
    // 定义时加上mut，即表示为可变变量
    let mut guess  = String::new();	//关联函数
    
	// &mut guess 方法的参数是按引用进行传递的，Rust中引用也是默认不可变的
    io::stdin().read_line(&mut guess).expect("无法读取行");
    // read_line无论什么都会进行读取，其有一个返回值，为io::Result类型
    // 此处的 io::Result为枚举类型 OK，Err
    // Err附带原因，并且io::Result为其定义了expect方法

    println!("你猜的数是：{}",guess);
    // {}占位符
}

```







​			