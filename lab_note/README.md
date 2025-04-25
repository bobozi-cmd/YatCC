# 声明
- 本fork仓库仅用于个人学习，里面的代码仅供其他自学的同学参考，请不要直接通过抄写代码的方式来完成这些lab！

# 环境配置

- 参考[可选方案3](https://arcsysu.github.io/YatCC/#/introduction/environment?id=可选方案-3-命令行手动配置（不使用-docker）)，在ubuntu上配置环境
- 防止网络问题，提前下载好 llvm/setup.sh 需要的软件包（重命名），配置antlr的时候会遇到googletest下载不下来，要手动设置一下proxy的环境变量

# Lab1 实现一个简单的词法分析器
- 在 config.cmake 里面配置词法分析器的完成方式：`set(TASK1_WITH "flex")`
- 修改 task/1/flex 的代码，参考对应文件夹下的 README
- 任务目标：在 lex.l 里面编写词法分析的规则，然后在 lex.hpp 的 enum Id 中添加对应的枚举值，在 kTokenNames 的正确位置添加对应的输出字符串
- flex 会通过 lex.l 生成一个 C 源文件，在我的环境里面生成了 build/task/1/flex/lex.l.cc 和 build/task/1/flex/lex.l.hh
- `#define ADDCOL() g.mColumn += yyleng;` 定义了一个 ADDCOL 的宏，yyleng 表示当前匹配到的字符串的长度，g.mColumn 存放的是当前匹配的字符串的起始位置，所以这个宏可以用来更新列信息
- `#define COME(id) return come(id, yytext, yyleng, yylineno)` 定义了一个 COME 的宏，调用 flex 的 come() 函数，处理和记录识别到的每个词法单元，返回其类型，其中 id 是在 lex.hpp 的 enum Id 中定义的
- 手动运行测试用例：
    - 先编译task1，和task1-score获取标准答案
    - 运行task1，输入测试用例，将词法分析的结果输出到 result.c 的文件中: `./build/task/1/flex/task1 ./test/cases/functional-0/000_main.sysu.c ./result.txt`
    - 和标准答案做对比: `diff ./build/test/task1/functional-0/000_main.sysu.c/answer.txt ./result.txt`

