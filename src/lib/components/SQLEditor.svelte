<script>
	import { onMount } from 'svelte';
	import { EditorView, basicSetup } from 'codemirror';
	import { sql } from '@codemirror/lang-sql';

	let sqoolTheme = EditorView.theme({
		'&': {
			color: '#2d3748',
			backgroundColor: '#edf2f7',
			fontFamily: 'D2Coding',
			fontSize: '16px',
			lineHeight: '1.5',
			tabSize: '4',
			whiteSpace: 'pre',
			wordWrap: 'normal',
			overflowWrap: 'normal',
			hyphens: 'none',
			minHeight: '200px'
		},
		'&.cm-editor': {
			outline: 'none'
		}
	});

	export let initialValue = '';
	let queryResult = '';
	let result = '';

	let editorView;
	let editorElement;

	onMount(() => {
		createDB();
		editorView = new EditorView({
			extensions: [basicSetup, sql(), sqoolTheme],
			parent: editorElement,
			doc: initialValue
		});

		return () => {
			editorView.destroy();
		};
	});

	async function createDB() {
		// 백엔드 API 호출 및 결과 처리
		await fetch('https://be.wiseit.kr/api/sqool/', {
			method: 'POST',
			headers: {
				'Content-Type': 'application/json'
			},
			body: JSON.stringify({ dbname: 'Artist' }),
			credentials: 'include'
		})
			.then((res) => res.json())
			.then((data) => {
				result = JSON.stringify(data, null, 2);
				console.log(result);
			})
			.catch((error) => {
				queryResult = error;
			});
	}

	async function executeQuery() {
		const query = editorView.state.doc.toString();
		// 백엔드 API 호출 및 결과 처리
		await fetch('https://be.wiseit.kr/api/sqool/query', {
			method: 'POST',
			headers: {
				'Content-Type': 'application/json'
			},
			body: JSON.stringify({ query: query }),
			credentials: 'include'
		})
			.then((res) => res.json())
			.then((data) => {
				queryResult = JSON.stringify(data, null, 2);
				console.log(queryResult);
			})
			.catch((error) => {
				queryResult = error;
			});
	}
</script>

<div class="card">
	<h5 class="card-header py-3">SQL 코드 작성</h5>
	<div bind:this={editorElement}></div>
</div>
<div class="d-grid mt-3">
	<button on:click={executeQuery} class="btn btn-success"> 코드 실행(Ctrl + Enter) </button>
</div>

{#if queryResult}
	<div class="card mt-3">
		<h5 class="card-header py-3">쿼리 실행 결과</h5>
		<div class="card-body">
			<pre>{queryResult}</pre>
		</div>
	</div>
{/if}

<style>
</style>
