<script>
	import Eliza from 'elizabot';
	import { beforeUpdate, afterUpdate } from 'svelte';

    let div;
	let autoscroll;
    let responses = 
    ["Remember to prioritize self-care in your journey.","Depression is difficult to deal with, but it's important to talk about",
      "Always prioritize your mental health.", "What steps can you take to overcome this challenge?"];
          
    beforeUpdate(() => {
		autoscroll = div && (div.offsetHeight + div.scrollTop) > (div.scrollHeight - 20);
	});

	afterUpdate(() => {
		if (autoscroll) div.scrollTo(0, div.scrollHeight);
	});

	const eliza = new Eliza();

	let comments = [
		{ author: 'eliza', text: eliza.getInitial() }
	];

	function handleKeydown(event) {
		if (event.key === 'Enter') {
			const text = event.target.value;
			if (!text) return;

			comments = comments.concat({
				author: 'user',
				text
			});

			event.target.value = '';

            let reply;

            ///const reply = eliza.transform(text);

            ///const reply = text;
            if (text.includes('self-care')){                
                reply = responses[0];}
            else if (text.includes('depression')){                
                reply = responses[1];}
            else if (text.includes('mental')){                
                reply = responses[2];}
            else if (text.includes('challenge')){                
                reply = responses[3];}
            else{
                reply = eliza.transform(text);
            };



			setTimeout(() => {
				comments = comments.concat({
					author: 'eliza',
					text: '...',
					placeholder: true
				});

				setTimeout(() => {
					comments = comments.filter(comment => !comment.placeholder).concat({
						author: 'eliza',
						text: reply
					});
				}, 500 + Math.random() * 500);
			}, 200 + Math.random() * 200);
		}
	}


</script>
<head>
    <title>Mental Health App</title>
</head>

  <header>Your mental health matters.</header>

<div class="chat">
	<p>Let's chat.</p>

	<div class="scrollable" bind:this={div}>
		{#each comments as comment}
			<article class={comment.author}>
				<span>{comment.text}</span>
			</article>
		{/each}
	</div>

	<input on:keydown={handleKeydown}>
</div>



<style>
    .chat p{
        font-size: 1.5em;
    }
	.chat {
		display: flex;
		flex-direction: column;
		height: 100%;
		max-width: 400px;
	}

	.scrollable {
		flex: 1 1 auto;
		border-top: 1px solid #eee;
		margin: 0 0 0.5em 0;
		overflow-y: auto;
	}

	article {
		margin: 0.5em 0;
	}

	.user {
		text-align: right;
	}

	span {
		padding: 0.5em 1em;
		display: inline-block;
	}

	.eliza span {
		background-color: #eee;
		border-radius: 1em 1em 1em 0;
	}

	.user span {
		background-color: #0074D9;
		color: white;
		border-radius: 1em 1em 0 1em;
	}
</style>