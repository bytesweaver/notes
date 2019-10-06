[TOC]

#  Put Model To Work

##  Definitions



**domain**

> A	 sphere(球)	 of	 knowledge,	 influence,	 or	activity.	The	 subject(主题)	area	 to	which	 the	 user	applies	a	program	is	the	domain	of	the	software.

**model**

>A	 system	 of	 abstractions(抽象)	 that	 describes	 selected	 aspects(方面)	 of	 a	 domain	 and	 can	 be	 used	 to	solve	problems	related	to	that	domain 

**ubiquitous language**

>A	 language	 structured	 around	the	 domain	model	 and	 used	 by	 all	team members	 within	 a	bounded	context	to	connect	all	the	activities	of	the	team	with	the	software 

**context**

> The	setting	in	which	a	word	or	statement	appears	that	determines	its	meaning.	Statements	about	a	model	can	only	be	understood	in	a	context. 

**bounded context**

> A	description	of	a	boundary(边界)	(typically	a	subsystem,	or	the	work	of	a	particular	team)	within	which	a	particular	model	is	defined	and	applicable 

## Model To Work

> - Focus	on	the	core	domain.
>
> - Explore	 models in	 a	 creative	 collaboration	 of	 domain	 practitioners	
>   	and	software	practitioners.
>
> - Speak	a	ubiquitous	language within	an	explicitly	bounded	context. 

## Continuous Integration

> Once	a	bounded	context	has	been	defined,	we	must	keep	it	sound.

边界上下文一旦确定，我们必须保持其原义

> Institute	a	process	of	merging	all	code	and	other	implementation	artifacts	
>
> 制定使用自动化测试快速flag 碎片去频繁合并代码和其他实现文档的流程
>
> frequently,	with	
> automated	 tests	 to	 flag	 fragmentation	 quickly.	 Relentlessly	 exercise
>
> 
>
> ​	 the	 ubiquitous	
> language	to	hammer	out	a	shared	 view	of	the	model	as	the	 
>
> 不停地锻炼ubiquitous	
> language	去打造出共享的模型视角
>
> concepts	evolve	in	different	
> people’s	heads 

no fragement, one bouded context

## Model-Driven Design

>Tightly	 relating	 the	 code	 to	 an	 underlying	 model	 gives	 the	 code	 meaning	 and	 makes	 the	
>model	relevant. 

代码和模型向关联

>Design	a	portion(部分)	of	the	software	system	to	reflect	the	domain	model	in	a	very	literal(字面意义)	way,	
>so	 that	 mapping	 is	 obvious.	 Revisit	 the	 model	 and	 modify	 it	 to	 be	 implemented	 more	
>naturally	in	software,	even	as	you	seek	to	make	it	reflect	deeper	insight	into	the	domain.	
>Demand	a	single	model	that	serves	both	purposes	well,	in	addition	to	supporting	a	fluent	
>ubiquitous	language. 

## Hands-on Modelers

> Any	technical	person	contributing	to	the	model	must	spend	some	time	touching	the	code,	
> whatever	 primary	 role	 he	 or	 she	 plays	 on	 the	 project.	 Anyone	 responsible	 for	 changing	
> code	must	learn	to	express	a	model	through	the	code.	Every	developer	must	be	involved	in	
> some	 level	 of	 discussion	 about	the	 model	 and	 have	 contact	with	 domain	 experts.	 Those	
> who	contribute	in	different	ways	must	consciously	engage	those	who	touch	the	code	in	a	
> dynamic	exchange	of	model	ideas	through	the	ubiquitous	language 

modelers通过代码表达模型

# Building Blocks  of a Model-Driven Design

## Entities

业务实体，生命周期中属性可能发生变化，通过ID标识唯一

> When	an	object	is	distinguished	by	its	identity,	rather	than	its	attributes,	make	this	primary	
> to	 its	 definition	 in	the	 model.	 Keep	the	 class	 definition	 simple	 and	 focused	 on	 life	 cycle	
> continuity	and	identity.	
> Define	a	means	of	distinguishing	each	object	regardless	of	its	form	or	history.	Be	alert	to	
> requirements	 that	 call	 for	 matching	 objects	 by	 attributes.	 Define	 an	 operation	 that	 is	
> guaranteed	to	produce	a	unique	result	for	each	object,	possibly	by	attaching	a	symbol	that	
> is	guaranteed	unique.	This	means	of	identification	may	come	from	the	outside,	or	it	may	be	
> an	arbitrary	identifier	created	by	and	for	the	system,	but	it	must	correspond	to	the	identity	
> distinctions	in	the	model.	
> The	model	must	define	what	it	means	to	be	the	same	thing. 

## ValueObject

> Some	objects	describe	or	compute	some	characteristic	of	a	thing.	
>

描述或者计算，一般是不可变的，通过属性判断是否相等

## Domain Events

>Model	information	about	activity	in	the	domain	as	a	series	of	discrete	events.	Represent	
>each	event	as	a	domain	object.	These	are	distinct	from	system	events	that	reflect	activity	
>within	 the	 software	 itself,	 although	 often	 a	 system	 event	 is	 associated	 with	 a	 domain	
>event,	either	as	part	of	a	response	to	the	domain	event	or	as	a	way	of	carrying	information	
>about	the	domain	event	into	the	system.
>A	domain	event	is	a	full-fledged	part	of	the	domain	model,	a	representation	of	something	
>that	happened	in	the	domain.	Ignore	irrelevant	domain	activity	while	making	explicit	the	
>events	that	the	 domain	 experts	want	to	track or	 be	 notified	 of,	 or	which	 are	 associated	
>with	state	change	in	the	other	model	objects. 

领域事件也是Enties，通过唯一号标识，用于追踪事件流向

## Services

> Sometimes,	it	just	isn’t	a	thing.

不能够归属到Enties或者VO里面的，额外的服务

## Modules

> Choose	modules	that	tell	the	story	of	the	system	and	contain	a	cohesive	set	of	concepts.	
> Give	the modules	names	that	become	part	of	the	ubiquitous	language.	Modules	are	part	of	
> the	model	and	their	names	should	reflect	insight	into	the	domain.
> This	often	yields	low	coupling	between	modules,	but	if	it	doesn’t	look	for	a	way	to	change	
> the	model	to	disentangle	the	concepts,	or	an	overlooked	concept	that	might	be	the	basis	of	
> a	module	that	would	bring	the	elements	together	in	a	meaningful	way.	Seek	low	coupling	
> in	the	sense	of	concepts	that	can	be	understood	and	reasoned	about	independently.	Refine	
> the	model	until	it	partitions	according	to	high-level	domain	concepts	and	the	corresponding	
> code	is	decoupled	as	well 

## Aggregates

聚合体，也是Entity，包含VO和Entities识别Root of Aggregates，外部只能持有ROA

>Cluster	the	entities	and	value	objects	into	aggregates	and	define	boundaries	around	each.	
>Choose	 one	 entity	 to	 be	 the	root	 of	 each	 aggregate,	 and	 allow	 external	 objects	 to	 hold	
>references	to	the	root	only	(references	to	 internal	members	passed	out	for	use	within	 a	
>single	operation	only).	Define	properties	and	invariants	for	the	aggregate	as	a	whole	and	
>give	enforcement	responsibility	to	the	root	or	some	designated	framework	mechanism 

## Repositories

> Keep	 application	 logic	 focused	 on	 the	
> model,	delegating	all	object	storage	and	access	to	the	repositories. 

用于访问外部存储，获取数据或者保存数据。

>Query	access	to	aggregates	expressed	in	the	ubiquitous	language.

## Factories

创建复杂的ValueObject 或者 Entities，将复杂的构造逻辑交给Fatories，

