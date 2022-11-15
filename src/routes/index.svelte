<script>
	import { onMount } from 'svelte';
  import '../tailwind.css';
  import { fly,fade } from 'svelte/transition';

  let now = '';
  let day = '';
  let search= '';

  let showWindow = 0;
 
  let searchEngines = [
	{ id: 1, text: `Bing`, url: "https://cn.bing.com/search?q=" , home:"https://cn.bing.com"},
    { id: 2, text: `Google`, url: "https://www.google.com.hk/search?q=", home: "https://www.google.com.hk"},
    { id: 3, text: `Baidu`, url: "https://www.baidu.com/s?ie=utf-8&word=", home: "https://www.baidu.com"},
    { id: 4, text: `GitHub`, url: "https://github.com/search?q=", home: "https://github.com"},
	{ id: 5, text: `Bilibili`, url: "https://search.bilibili.com/all?keyword=",  home: "https://space.bilibili.com"},
    { id: 6, text: `arXiv`, url: "https://arxiv.org/search/?searchtype=all&source=header&query=",  home: "https://arxiv.org"},
  ];
  let selected=searchEngines[0];
	let data = [
		{
			projectName: 'Wudao',
			introduction: 'QAQ',
			author: 'TualatinX,LLLeo,BITTIO,echo子懿,woarthur',
			github: 'https://github.com/WuDaoGroup',
			web: 'https://wudao.netlify.app/',
			background:"https://923259.smushcdn.com/2321054/wp-content/uploads/2019/05/what-is-data-science-1.jpg",
			bgcolor:"bg-base-300"
		},
		{
			projectName: 'StarMap',
			introduction: 'TAT',
			author: 'Zhoues',
			github: 'https://github.com/BUAA-OpenMap-Group',
			web: 'https://www.zhoues.com',
			background:"https://923259.smushcdn.com/2321054/wp-content/uploads/2019/05/what-is-data-science-1.jpg",
			bgcolor:"bg-base-200"
		},
		
	];
	function timeCompletion(a){
		if(a<10){
			return '0' + a;
		}
		else{
			return a;
		}
	}
	function submit(event) {
  		if (event.key == "Enter") {
    		toSearch();
  			}
	}
	function showTime() {
		var date = new Date(); 
		day = date.getFullYear() + '年'; 
		day = day + (date.getMonth() + 1) + '月'; 
		day = day + date.getDate() + '日';

		now = timeCompletion(date.getHours()) + ':';
		now = now + timeCompletion(date.getMinutes()) + ':';
		now = now + timeCompletion(date.getSeconds());

		
	}
	function toSearch() {
		if(search == ""){
			window.location.href = selected.home;
		}
		else{
			window.location.href = selected.url + search;
		}
  }
	
  	function getWindowSize(){
		if(document.documentElement.clientWidth > document.documentElement.clientHeight){
		showWindow = 1;
	}
	else{
		showWindow = 0;
	}
	  }

  onMount(async () => {
	console.log(document.documentElement.clientHeight);
	console.log(document.documentElement.clientWidth);
    const interval1 = setInterval(showTime, 100);
	if(document.documentElement.clientWidth > document.documentElement.clientHeight){
		showWindow = 1;
	}
	else{
		showWindow = 0;
	}
	const interval2 = setInterval(getWindowSize, 100);
	});

</script>

<title>Super2021超乎你的想象!</title>

{#if showWindow==1}

<div class="navbar bg-neutral text-neutral-content max h-5">
	<div><img src="image/super2021.png" alt="super2021" width="154px" /></div>
	<a href="https://scs.buaa.edu.cn/" class="btn">云平台</a>
	<a href="https://spoc.buaa.edu.cn/" class="btn">SPOC</a>
	<a href="https://judge.buaa.edu.cn/" class="btn">希冀</a>
	<a href="https://accoding.buaa.edu.cn/" class="btn">OJ</a>
	<a href="https://github.com/" class="btn">Github</a>
	<a href="https://os.buaa.edu.cn/" class="btn">OS</a>
	<a href="http://lab.os.buaa.edu.cn/" class="btn">OSLab</a>
	<a href="http://10.134.136.71:9995/" class="btn">SE</a>
	<a href="http://network-lab.mooc.buaa.edu.cn/?m=Home" class="btn">计网</a>
	<a href="https://zh.d2l.ai" class="btn">DL</a>
</div>

<div class="hero min-h-screen" style='background-image: url("image/bg.jpg");'>
	<div class="hero-overlay  bg-opacity-60" />

	<div class="hero-content w-11/12 grid grid-cols-7 gap-4 " >
		<div class="col-span-1"/>
	<div class="text-center text-neutral-content col-span-3">
		<div class="max-w-md">
			<h1 class="mb-5 text-7xl font-mono font-bold" in:fly="{{ y: 100, duration: 2000 }}">Super2021</h1>
			<p class="mb-5 text-5xl font-bold "></p>
			<h2 class="mb-5 text-6xl font-mono font-bold" in:fade="{{ duration: 2000 ,delay :1000}}">{now}</h2>
			<h1 class="font-serif" in:fade="{{duration: 2000 ,delay :1000}}" >{day}</h1>
		</div>
	</div>
	<div class="col-span-3">
	<div class="form-control" >
		<div class="input-group grid grid-cols-12">
			<select class="select select-bordered col-span-3 " bind:value={selected}>
				{#each searchEngines as engine}
      				<option value={engine} class="font-mono">
        			{engine.text}
      				</option>
    			{/each}
			</select>
		  <input type="search" placeholder="Search… " class="input input-bordered col-span-8" bind:value={search} on:keydown={submit}>
		  
		  <button class="btn btn-square " on:click|preventDefault={toSearch}>
			<svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" /></svg>
		  </button>
		</div>
	  </div>
	</div>
</div>
<footer class="place-self-end mr-5">
    <div class="text-center p-2 text-white text-sm font-mono rounded ">
      <span>© 2022 Copyright: </span>
      <a href="https://github.com/BUAA-GoodBro2021/Super2021-index">BUAA-GoodBro2021</a>
      |
      <a href="https://beian.miit.gov.cn">京ICP备2022007189号-2</a>
    </div>  
  </footer>
</div>

<!-- {#each data as d}
<div class={d.bgcolor}>
	<br />
	<div class="grid grid-cols-12 gap-4">
		<div class="col-span-2" />
		<div class="card lg:card-side bg-base-100 shadow-xl  col-span-8 ">
			 <figure class="max-w-6xl"><img src="src\image\super2021.png"  alt="echo"></figure> 
			<div class="card-body">
				<h2 class="card-title">{d.projectName}</h2>
				<p>Intro:{d.introduction}</p>
				<p>author:</p>
				<p>{d.author}</p>
				<div class="card-actions justify-end">
					<a href={d.github} class="btn btn-primary">GITHUB</a>
					<a href={d.web} class="btn btn-primary">WEB</a>
				</div>
			</div>
		</div>
	</div> -->
	<!-- <div class="grid grid-cols-12 gap-4">
		<div class="col-span-2" />
	<div class="card  bg-base-100 shadow-xl image-full col-span-8">
		<figure><img src={d.background} alt="Shoes" /></figure>
		<div class="card-body">
			<h2 class="card-title mb-5 text-7xl font-bold text-center">{d.projectName}</h2>
			<p  class="card-title mb-5 text-3xl  text-center">Intro:{d.introduction}</p>
			<p class="card-title mb-5 text-3xl  text-center">author:</p>
			<p class="card-title mb-5 text-3xl  text-center">{d.author}</p>
			<div class="card-actions justify-center">
				<a href={d.github} class="btn btn-primary">GITHUB</a>
				<a href={d.web} class="btn btn-primary">WEB</a>
			</div>
		</div>
	  </div>
	</div>
	<br />
</div>
{/each} -->




{:else}
<div>
<div class="navbar bg-neutral text-neutral-content max h-5">
	<div><img src="image/super2021.png" alt="super2021" width="154px" /></div>
	<a href="http://10.212.28.38/" class="btn">TD查询</a>
</div>
<div class="hero min-h-screen" style='background-image: url("image/bg.jpg");'>
	<div class="hero-overlay  bg-opacity-60" />
	<div class="hero-content h-11/12 flex" >
	<div class="text-center text-neutral-content">
		<div class="max-w-md">
			<h1 class="mb-5 text-5xl font-mono font-bold" in:fly="{{  y: 100, duration: 2000 }}">Super2021</h1>
			<p class="mb-5 text-3xl font-bold "></p>
			<h2 class="mb-5 text-4xl font-mono font-bold" in:fade="{{ duration: 2000 ,delay :1000}}">{now}</h2>
			<h1 class="font-serif" in:fade="{{duration: 2000 ,delay :1000}}" >{day}</h1>
		</div>
	</div>
</div>
<footer class="place-self-end mr-5">
    <div class="text-center p-2 text-white text-sm font-mono rounded ">
      <span>© 2022 Copyright: </span>
      <a href="https://github.com/BUAA-GoodBro2021/Super2021-index">BUAA-GoodBro2021</a>
    </div>  
  </footer>
</div>

</div>
{/if}

<style type="text/css">
.input-group :first-child {
    border-top-right-radius: 0;
    border-top-left-radius: 0.5rem;
    border-bottom-right-radius: 0;
    border-bottom-left-radius: 0.5rem;
}
.input-group :last-child {
    border-top-right-radius: 0.5rem;
    border-top-left-radius: 0;
    border-bottom-right-radius: 0.5rem; 
    border-bottom-left-radius: 0;
}
</style>