# bwLoader
资源预加载，同时提供进度更新，支持(图片，MP3)，文件大小不足1KB，真正小巧好用的资源加载插件。

# 使用帮助
1、引入bwLoader.min.js文件

2、页面加入以下代码

		var loader = new bwLoader();
		
		//添加音乐素材
		loader.addResources('source/music/music.mp3', 'music');
		loader.addResources('source/music/welcome.mp3', 'music');
		
		//添加图片素材
		for(var i = 1; i <= 8; i++){
			loader.addResources('source/images/' + i + '.jpg');
		}
		
		//侦听加载进度
		loader.addProgressListener(function (e){
			var num = Math.floor(e.completedCount / e.totalCount * 100);
			document.getElementById('loading').innerHTML = num;
		});
		
		//侦听是否加载完成
		loader.addCompletionListener(function (e){
			document.getElementById('loading').innerHTML = '加载完成：共'+e.completedCount +' | '+ e.totalCount + '文件';
		});
		
		//开始
		loader.start();
			

3、添加Loading标签

		<div id="loading">0</div>
		
本插件仅用于学习交流，也可用于商业项目，插件不错完善中....呵呵
