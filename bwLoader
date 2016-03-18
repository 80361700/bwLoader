(function(){
	
	/***************
	 *资源加载器
	 *加载资源，同时提供进度更新，支持(图片，MP3)。
	  by:交流QQ 80361700
	 */
	
	this.bwLoader = function(){
		
		//加载条目			
		var entries = new Array();
		
		//储存回调方法
		var progressListeners = new Array();
	
		//加载过程回调
		this.addProgressListener = function(callback) {
			progressListeners.push({
				callback : callback
			});
		};
		
		//加载完毕回调
		this.addCompletionListener = function(callback) {
			progressListeners.push({
				callback : function(e) {
                    //如果加载完毕执行回调
					if (e.completedCount === e.totalCount) {
                        callback(e);
                    }
                }
			});
		};		
		
		this.addResources = function(resource, type){
			//添加需要加载的条目
			entries.push({
				url  : resource,
				type : type || 'images'
			});
		}
		
		//开始
		this.start = function(){	
					
			var completed = 0, entry;			
			(function loadResources(){	
						
				switch(entries[completed].type){					
					//图片类型
					case 'images':					
						entry = new Image();				
						entry.onload = function(){
							
							entry.onload = null;
							completed++;
							
							for(var i = 0; i < progressListeners.length; i++){
								progressListeners[i].callback({						
									completedCount: completed,
									totalCount    : entries.length							
								});
							}
									
							if( completed < entries.length ){						
								loadResources(completed);
							}					
						}
							
						entry.src = entries[completed].url;
						break;
						
					//mp3类型
					case 'music':						
						entry = new Audio(entries[completed].url);
						entry.onloadedmetadata = function()
						{
							entry.onloadedmetadata = null;
							completed++;
							
							for(var i = 0; i < progressListeners.length; i++){
								progressListeners[i].callback({						
									completedCount: completed,
									totalCount    : entries.length							
								});
							}
									
							if( completed < entries.length ){						
								loadResources(completed);
							}	
						}
						
						entry.src = entries[completed].url;
						break;
					
					//错误格式，跳过
					default:						
						completed++;
						for(var i = 0; i < progressListeners.length; i++){
							progressListeners[i].callback({						
								completedCount: completed,
								totalCount    : entries.length							
							});
						}
									
						if( completed < entries.length ){						
							loadResources(completed);
						}
						break;						
				}
			})();
		}
	};	
}());
