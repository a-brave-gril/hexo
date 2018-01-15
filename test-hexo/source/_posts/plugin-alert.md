---

title: alert插件学习心得（bootatrap）
date:  #时间，一般不用改
categories:  前端笔记-插件篇
tags:  [插件,bootatrap,alert插件] #标签，格式可以是[Hexo,总结]，中间用英文逗号分开
keywords:  [插件,bootatrap,alert插件] #文章关键词，多个关键词用英文逗号隔开

---
##	插件：本人理解的插件的作用主要是，查找要处理的DOM元素，并且对这些DOM元素绑定事件。
##	插件的好处
	1. 插件可以避免代码臃肿。
	2. 插件编写一次就可以重复使用，提高工作效率。
* * * *
##	插件注意事项
	1. 插件要写在一个闭包里，防止变量污染。
	2. 如果插件的名称与其他的库的插件名称冲突，请不要忘记解决冲突。
	3. 要对当前的元素进行事件处理而不是将所有的目标元素都处理
* * * *
##	基于bootatrap中alert插件，讲解插件编写逻辑以及步骤
	1. 找到要处理的DOM元素
	2. 定义构造函数，用于对元素绑定事件
	3. 循环绑定事件，要注意防止事件的重复绑定
	4. 将需要对目标元素的处理事件绑定在构造函数上
	5. 如果插件与其他库插件命名冲突，解决冲突
* * * *
##	alert插件代码详解
    ···
		+function($){
			var dom = '[data-type="alert"]';// 目标DOM元素

			// 定义关闭方法
			Alert.prototype.close = function(e){
				// 获取点击的目标元素，并进行处理。
				$this = $(e.target);
				var parent = $this.closest("div");
				parent.empty();				
			}

			// 定义Alert事件
			function Alert(el){
				$this = $(el);
				$this.on("click",dom,this.close)	
			}
			
			// 对找到的元素 进行事件绑定
			function Plugin(){
				// this指向调用的元素
				return this.each(function(){
					// 判断当前元素有没有绑定alert事件，防止重复绑定
					var $this = $(this);
					var data  = $this.data('alert');
					if(!data){
						$this.data("alert",new Alert($this));
					};
				});
			}

			var old = $.fn.alert; // 保存原有的alert事件

			$.fn.alert = Plugin;  // 重新定义JQ的alert事件

			$.fn.alert.Constructor = Alert; // 将alert暴露出来，用于在alert上绑定事件

			// 保存原来的alert事件 (防止冲突)
			$.fn.alert.noConflict = function(){
				$.fn.alert = old;
				return this;
			}
		}(jQuery)
	···