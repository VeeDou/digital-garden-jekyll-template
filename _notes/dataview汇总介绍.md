---
---
#####  dataview 汇总信息
---
代码：
%%``` dataview 
table file.etags[0] as 想法来源
from "笔记"
where contains(file.tags,"《")
sort 创建时间 desc ```
%%

逻辑：通过第一个标签来定位内容来源
其它：有3种查询方式：文件名 file.name、file.tags、yml标记（必须在行首，所以弃用了，重点不应该是这些标记）

#####  dataview 汇总信息
%%```dataviewjs 
var y = "2022" 
var m = Array(12).fill(0).map(function(v,i){return i}); 
var d = [31,29,31,30,31,30,31,31,30,31,30,31] 
for(let i of m) 
{ 
	var n = Array(d[i]).fill(0).map(function(v,i){return i+1}); 
	var data = Array(d[i]).fill(0); 
	for(let j of dv.pages(`"笔记"`).filter(p=>String(p.file.cday).split("-")[0]==y && String(p.file.cday).split("-")[1]==i+1).groupBy(p=>String(p.file.cday).split("-")[2].slice(0,2))) data[j.key-1] = dv.pages(`"笔记"`).filter(p=>String(p.file.cday).split("-")[2].slice(0,2)==j.key).length; 
	if(data.every(p=>p==0)) 
	continue 
	dv.header(4, i+1+"月"); 

} 

//该死的，这样的缩进来表示什么鬼数据，之前没注意这个data的缩进，直接GG
dv.paragraph(`\`\`\`chart 
type: line 
labels: [${n}] 
series: 
- title: 当月笔记统计图 
  data: [${data}]
labelColors: true 
\`\`\``) ;

%%

逻辑：取数，然后用chart进行作图展示

---

创建时间:2022-12-12 17:38
内容链接: 
1.  [obsidian插件之dataview入门 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/409253101) 
2. [格式化你的笔记 - Obsidian 中文帮助 - Obsidian Publish](https://publish.obsidian.md/help-zh/%E4%BD%BF%E7%94%A8%E6%8C%87%E5%8D%97/%E6
3. %A0%BC%E5%BC%8F%E5%8C%96%E4%BD%A0%E7%9A%84%E7%AC%94%E8%AE%B0)
4. [Dataviewjs的奇技淫巧 - 经验分享 - Obsidian 中文论坛](https://forum-zh.obsidian.md/t/topic/5954)