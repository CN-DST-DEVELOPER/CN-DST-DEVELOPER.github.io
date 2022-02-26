---
layout: default
title: "模组开发规范"
permalink: /_pages/DevelopmentStandard
---
## 模组开发规范 <sub>2022.02.26</sub>

建议采用vscode作为开发编辑器，以下均以vscode为例

1. 代码格式化使用vscode-lua插件，使用tab缩进，tab长度为4
2. Git提交名、文件内作者名均使用Steam昵称；文件头注释应至少包含以下项

   ```
   --[[ 
   Copyright [yyyy] [name of copyright owner]

   Licensed under the Apache License, Version 2.0 (the "License");
   you may not use this file except in compliance with the License.
   You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

   Unless required by applicable law or agreed to in writing, software
   distributed under the License is distributed on an "AS IS" BASIS,
   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
   See the License for the specific language governing permissions and
   limitations under the License.

   ]]
   ```
   yyyy改为当前年份，name of copyright owner改为此文件作者名

   可选内容：

   ```
   Description:
   	此文件功能介绍
   Change Logs:
   	1.xxxxxxx——修改者名
   	2.xxxxxxx——修改者名
   ```
   根据Apache 2.0协议规定，在模组文件夹根路径须添加LICENSE文件，可选添加NOTICE文件 。
3. 函数、变量命名选用其功能的合适英文翻译。从命名无法直接理解的或特殊复杂的代码建议添加注释。全局函数、类名及component、widget中全局方法、table跨文件调用的方法采用大驼峰法，全局变量、table中只在本文件调用的方法命名采用小驼峰法。局部函数、变量采用下划线命名法。例如：

   ```lua
   ./scripts/components/say.lua
   local say =
   	Class(
   	function(self, inst)
   		self.inst = inst
   		self.word="hello world!"
   	end
   )

   function say:HelloWorld()
   	print(self.word)
   end

   ./scripts/prefabs/animals.lua
   ......
   local function do_flash(inst)
   	inst:flash()
   end

   local function fn(Sim)
   	local inst = CreateEntity()
   	inst.time="60"
       inst.flash=function(inst)
           ......
       end
       inst.TryFlash=function(inst)
           ......
       end

   	return inst
   end

   return Prefab("animals", fn, assets, prefabs)

   ./scripts/otherfile.lua

   local animals = SpawnPrefab("animals")
   animals:TryFlash()
   ```
4. 对于非API类mod，为了减少模组间冲突，统一添加模组英文名为文件名前缀，如 ``smarterchest_chest.lua``
5. 对于发布在工坊的模组，应在对应分支添加版本号tag
